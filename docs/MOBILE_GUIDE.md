# MAUI integration guide

The [OpenAPI contract](../openapi.yaml) defines the current public CRC API. The
[generated reference](API_REFERENCE.md) lists every operation and field. This
guide covers the choices a mobile team needs to make when using those routes.

## First request

Reference the [client library](../generated/Crc.Mobile.Api.csproj) from a .NET 10
MAUI project, or add [the generated source file](../generated/CrcDirectoryApiClient.cs)
to an existing project. It uses only .NET's `HttpClient` and `System.Text.Json`. Configure one
long-lived client with the base address of a CRC-approved development or mock
server (including the trailing slash):

```csharp
// MauiProgram.cs, after creating the builder
builder.Services.AddSingleton(_ => new HttpClient
{
    BaseAddress = new Uri("https://YOUR-APPROVED-DEV-API/")
});
builder.Services.AddSingleton<CrcDirectoryApiClient>();
```

Add `using Crc.Mobile.Api;` and inject `CrcDirectoryApiClient` into a view model
or service. The production public origin is `https://app.crc-coc.org/`, but
coursework and automated tests should use approved mock or development data.
These public routes currently need no API key. Mobile apps can call HTTPS
directly; browser CORS settings do not apply to native `HttpClient` requests.

```csharp
var matches = await api.SearchChurchesAsync("Little Rock", cancellationToken);
var codes = await api.GetCharacteristicCodesAsync(cancellationToken);
```

Cancel an in-flight search when the user changes the query or leaves the view.
Debounce typing so each keystroke does not trigger a network request. Handle
empty results, timeouts, loss of connectivity, and malformed search expressions
separately. `CrcApiException.StatusCode` and `.Detail` expose server errors;
`HttpRequestException` and `TaskCanceledException` cover network failure and
cancellation. Avoid displaying raw server response bodies to users.

## Directory flow

- `SearchChurchesAsync(q)` returns up to 250 open, geocoded matches, sorted by
  church name. Simple text such as `Little Rock` and fielded expressions such
  as `state = AR AND code = OC` are supported. A malformed expression returns
  HTTP 400.
- `GetChurchesAsync()` returns up to 15,000 open, geocoded rows, with no paging
  or promised sort order. Use it only when a full map or offline cache requires
  the larger payload. Do not treat an empty search as a full-directory request.
- There is no public church-by-ID endpoint. Open a detail screen from a row
  already returned by search or list. Ask CRC to add a server endpoint before
  designing a direct-link feature that depends on one.
- `char_codes` is a space-separated string. Split it for display and look up
  descriptions from `GetCharacteristicCodesAsync()`; keep unknown codes visible.
- Some address and contact fields are null. Coordinates exist on returned
  churches, but location permission is only needed for device-centered features.
- Congregation photos, when present, are served separately at
  `https://app.crc-coc.org/images/churches/{id}.jpg`. Show a fallback if absent.
  Validate external website and social URLs before opening them.

The current API does not offer server-side pagination, location filtering,
ETags, or a stated rate limit for reads. Cache conservatively and refresh when
the user requests current data. If the app needs these features, propose the
backend contract change before building the UI around them.

## Feedback flow

The existing feedback route can carry a correction request or a general
message; it does not edit a church record directly. Capture `opened_at` when
the feedback screen opens, then send that value when the visitor submits:

```csharp
var openedAt = DateTimeOffset.UtcNow.ToUnixTimeMilliseconds();
// Store openedAt with the visible form state; submit only after the user fills it in.
var result = await api.SubmitFeedbackAsync(new FeedbackSubmission
{
    Message = message,
    Name = name ?? "",
    Email = email ?? "",
    OpenedAt = openedAt,
    Website = "",
    Context = new Dictionary<string, object?>
    {
        ["selected_church_id"] = selectedChurch?.Id
    }
}, cancellationToken);
```

Messages shorter than three characters, submissions within three seconds of
opening the form, and submissions after 24 hours fail. The route may also
return HTTP 429 for rate limiting or 502/503 for mail service problems. A 202
response means accepted, not that a church record was changed. Never include
secrets or private account data in feedback context.

## Contract maintenance

Edit `openapi.yaml` when the backend contract changes, review that change with
CRC backend maintainers, then run:

```sh
python3 -m pip install -r tools/requirements.txt
python3 tools/generate_api.py
python3 tools/generate_api.py --check
```

Commit the spec, `docs/API_REFERENCE.md`, and
`generated/CrcDirectoryApiClient.cs` together. The generated files should not
be edited by hand. `openapi.yaml` can also be loaded into Swagger UI, Scalar,
Postman, or a compatible mock server for exploration; the YAML is the source
of truth. The document version is not a versioned API path: the live routes
still begin with `/api/`.
