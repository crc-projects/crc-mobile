# Architecture

## Purpose

CRC Mobile is a separate client for the existing CRC directory. It remains independently deployable while integrating with CRC through documented web APIs.

## System boundaries

- The mobile app owns presentation, navigation, local state, caching, and device-specific behavior.
- The existing CRC service owns directory data, validation, authentication, authorization, and administrative workflows.
- Shared behavior is defined in `openapi.yaml` rather than copied server code. The current backend URLs are not versioned.
- The app never connects directly to the CRC production database.
- Environments use separate configuration, credentials, and endpoints.

## Initial structure

The framework is .NET MAUI. The app's detailed folder structure should be decided after the student team confirms supported platforms, accessibility goals, and maintainership expectations. The generated C# API client is a starting integration component, not an app skeleton.

Suggested first decisions:

1. Supported iOS and Android versions.
2. Accessibility requirements and testing devices.
3. Offline and caching expectations.
4. Whether a future backend release will add paging or API versioning.
5. Automated testing and release workflow.

Record significant decisions in `docs/decisions/` as short architecture decision records.
