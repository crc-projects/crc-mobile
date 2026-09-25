# Contributing to CRC Mobile

Thank you for contributing to the CRC mobile app. This repository is designed for collaboration between CRC maintainers, university students, faculty advisers, and other approved contributors.

## Working agreement

- Create a short-lived branch for each issue: `feature/<issue>-short-name`, `fix/<issue>-short-name`, or `docs/<issue>-short-name`.
- Keep pull requests focused and small enough to review.
- Link every pull request to an issue or clearly explain the reason for the change.
- Require at least one CRC maintainer review before merging.
- Do not push directly to `main`.
- Never commit passwords, tokens, private keys, production data, or personal information.

## Development flow

1. Choose or create an issue with clear acceptance criteria.
2. Create a branch from the latest `main`.
3. Make the change and add or update tests.
4. Run the project's checks locally.
5. Open a draft pull request early for feedback.
6. Mark it ready when the acceptance criteria are met.
7. Address review comments and keep the branch current.
8. A CRC maintainer merges approved work.

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
