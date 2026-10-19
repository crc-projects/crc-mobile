# CRC API Contract

The [OpenAPI document](../openapi.yaml) is the machine-readable contract for the existing public CRC service. [API_REFERENCE.md](API_REFERENCE.md) and the [C# client](../generated/CrcDirectoryApiClient.cs) are generated from it. [MOBILE_GUIDE.md](MOBILE_GUIDE.md) explains MAUI usage.

## Principles

- Mobile features consume documented HTTPS endpoints. The current `/api/` routes are unversioned; `info.version` in the spec versions this document only.
- Contract changes are reviewed by maintainers of both repositories.
- Breaking changes require a migration plan and an agreed deprecation window.
- Development and automated tests use mock responses or a CRC-approved non-production service.
- Production credentials are never stored in the app source or distributed to student contributors.

## Endpoint inventory

| Capability | Method and path | Authentication | Owner | Status |
| --- | --- | --- | --- | --- |
| Directory list | `GET /api/churches` | None | CRC backend | Available |
| Directory search | `GET /api/search?q=...` | None | CRC backend | Available |
| Characteristic codes | `GET /api/char-codes` | None | CRC backend | Available |
| Visitor feedback | `POST /api/feedback` | None | CRC backend | Available |
| Shallow service check | `GET /api/ping` | None | CRC backend | Available |
| Congregation by ID | No public endpoint | TBD | CRC backend | Proposed, not available |

The spec records request fields, response fields, and known errors. The current list and search routes have fixed result limits and no pagination. A direct church-by-ID feature requires a backend change before mobile implementation.
