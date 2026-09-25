# CRC Mobile

CRC Mobile is the mobile client for the Churches of Christ Research Council directory. It is maintained separately from the deployed CRC web application so university student teams can contribute safely without receiving direct access to production code, data, or credentials.

## Project status

The repository is in its foundation phase. The team should choose the mobile framework only after confirming course constraints, target platforms, accessibility requirements, and CRC's long-term maintenance capacity.

## Collaboration model

- Students work on short-lived feature branches.
- Changes enter `main` through reviewed pull requests.
- A CRC maintainer approves every merge.
- Work is tracked through issues with acceptance criteria.
- Production deployment and credentials remain under CRC control.

Read [CONTRIBUTING.md](CONTRIBUTING.md) before starting. Security and production boundaries are in [SECURITY.md](SECURITY.md).

## Integration with CRC

This app is a separate client of the existing CRC service. It communicates through documented, versioned APIs and must never connect directly to the production database. See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) and [docs/API_CONTRACT.md](docs/API_CONTRACT.md).

## Getting started

1. Review the contribution and security guidance.
2. Select an approved issue.
3. Confirm the development API or mock-data approach with a CRC maintainer.
4. Create a feature branch and open a draft pull request early.
5. Add framework-specific setup instructions after the architecture decision is approved.

## Repository map

- `.github/`: review ownership and contribution templates
- `docs/`: architecture, API contracts, and future decision records
- `CONTRIBUTING.md`: student workflow and definition of done
- `SECURITY.md`: reporting process and production safeguards

## License

No license has been selected. Until CRC adds one, the repository remains private and its contents may not be redistributed.
