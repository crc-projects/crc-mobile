# Contributing to CRC Mobile

Thank you for contributing to the CRC mobile app. Anyone may propose changes through a fork and pull request. CRC maintainers review and merge changes to `main`.

## Working agreement

- Fork the repository, then create a short-lived branch for each issue: `feature/<issue>-short-name`, `fix/<issue>-short-name`, or `docs/<issue>-short-name`. Invited collaborators may branch directly in this repository.
- Keep pull requests focused and small enough to review.
- Link every pull request to an issue or clearly explain the reason for the change.
- Require CRC maintainer approval before merging. GitHub branch protection enforces the review gate on `main`.
- Do not push directly to `main`.
- Never commit passwords, tokens, private keys, production data, or personal information.

## Development flow

1. Choose or create an issue with clear acceptance criteria.
2. Create a branch from the latest `main` in your fork, or in this repository if you have write access.
3. Make the change and add or update tests.
4. Run the project's checks locally.
5. Open a draft pull request early for feedback.
6. Mark it ready when the acceptance criteria are met.
7. Address review comments and keep the branch current.
8. A CRC maintainer merges approved work.

For API changes, update `openapi.yaml`, run `python3 tools/generate_api.py`, and
commit the regenerated reference and C# client in the same pull request.

## Definition of done

A change is complete when it:

- Meets the issue's acceptance criteria.
- Includes relevant tests and documentation.
- Passes automated checks.
- Handles loading, empty, error, and offline states where relevant.
- Does not expose secrets or production-only access.
- Has been reviewed and approved by a CRC maintainer.

## Environments

Student development must use local fixtures, mock services, or a CRC-approved non-production API. Production credentials and direct production database access are out of scope.
