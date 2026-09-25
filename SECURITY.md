# Security Policy

## Reporting a vulnerability

Do not open a public issue for a suspected vulnerability or exposed secret. Contact a CRC repository administrator privately and include only the minimum information needed to investigate.

## Repository boundaries

- Never commit secrets, credentials, API tokens, private keys, or environment files.
- Never copy production user data or private administrative data into this repository.
- The mobile app must access CRC data through documented APIs, not through direct database connections.
- Student accounts must not receive production deployment or production database permissions.
- Use mock data or an approved development environment for coursework and testing.
- Treat location, contact, congregation, and account information according to CRC privacy requirements.
- Rotate any credential immediately if it is accidentally exposed.

## Supported versions

Until the first public release, security fixes apply to the current `main` branch.
