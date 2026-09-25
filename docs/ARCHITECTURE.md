# Architecture

## Purpose

CRC Mobile is a separate client for the existing CRC directory. It remains independently deployable while integrating with CRC through documented web APIs.

## System boundaries

- The mobile app owns presentation, navigation, local state, caching, and device-specific behavior.
- The existing CRC service owns directory data, validation, authentication, authorization, and administrative workflows.
- Shared behavior is defined through versioned API contracts rather than copied server code.
- The app never connects directly to the CRC production database.
- Environments use separate configuration, credentials, and endpoints.

## Initial structure

The framework and detailed folder structure should be selected through an architecture decision after the student team confirms course constraints, supported platforms, accessibility goals, and maintainership expectations.

Suggested first decisions:

1. Native versus cross-platform framework.
2. Supported iOS and Android versions.
3. Authentication and anonymous-use requirements.
4. Offline and caching expectations.
5. API versioning and error conventions.
6. Automated testing and release workflow.

Record significant decisions in `docs/decisions/` as short architecture decision records.
