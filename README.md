# CRC Mobile

CRC Mobile is the mobile client for the Churches of Christ Research Council directory. It is maintained separately from the deployed CRC web application so university student teams can contribute safely without receiving direct access to production code, data, or credentials.

## Project status

The repository is in its foundation phase. The client will use .NET MAUI. The student team and CRC maintainers still need to agree on supported iOS and Android versions, accessibility goals, and release support before starting the app shell.

## Collaboration model

- Contributors fork the public repository and work on short-lived branches in their forks. Invited collaborators may create branches here.
- Changes enter `main` through reviewed pull requests.
- A CRC maintainer approves every merge.
- Work is tracked through issues with acceptance criteria.
- Production deployment and credentials remain under CRC control.

Read [CONTRIBUTING.md](CONTRIBUTING.md) before starting. Security and production boundaries are in [SECURITY.md](SECURITY.md).

## Integration with CRC

This app is a separate client of the existing CRC service. It communicates through the documented HTTPS API and must never connect directly to the production database. The current routes are unversioned. See the [OpenAPI contract](openapi.yaml), [MAUI integration guide](docs/MOBILE_GUIDE.md), [generated API reference](docs/API_REFERENCE.md), and [generated C# client](generated/CrcDirectoryApiClient.cs).

## Getting started

1. Review the contribution and security guidance.
2. Select an approved issue.
3. Confirm an approved mock or development API with a CRC maintainer.
4. Fork the repository, create a feature branch, and open a draft pull request early.
5. Use the generated client and add MAUI app setup instructions as the app is built.

## Repository map

- `.github/`: review ownership and contribution templates
- `openapi.yaml`: source of truth for the current public API
- `docs/`: architecture, API reference, mobile guide, and future decision records
- `generated/`: C# client generated from the OpenAPI contract
- `tools/`: generator and its dependency list
- `CONTRIBUTING.md`: student workflow and definition of done
- `SECURITY.md`: reporting process and production safeguards

## License

CRC Mobile is available under the [MIT License](LICENSE), matching the CRC backend's license.
