# CRC API Contract

This document is the coordination point between CRC Mobile and the existing CRC service.

## Principles

- Mobile features consume documented, versioned HTTPS endpoints.
- Contract changes are reviewed by maintainers of both repositories.
- Breaking changes require a migration plan and an agreed deprecation window.
- Development and automated tests use mock responses or a CRC-approved non-production service.
- Production credentials are never stored in the app source or distributed to student contributors.

## Endpoint inventory

Add each endpoint before implementation:

| Capability | Method and path | Authentication | Owner | Status |
| --- | --- | --- | --- | --- |
| Directory search | To be defined | To be defined | CRC backend | Planned |
| Congregation details | To be defined | To be defined | CRC backend | Planned |

For each endpoint, document request fields, response fields, errors, pagination, rate limits, caching, and sample redacted payloads.
