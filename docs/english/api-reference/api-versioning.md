---
title: Version Management
excerpt: ""  
category: 62159fe61eda1d0047f76c9a
slug: api-versioning
---

# Smile API Version Management Guide

## Introduction

Welcome to the Smile API Version Management guide. This document outlines the versioning strategy and lifecycle policies for the Smile API, helping developers integrate smoothly with our platform while adapting to changes effectively.

## Semantic Versioning and Release Phases

The Smile API uses a semantic versioning pattern focused on the **major version number**, combined with distinct release phases. Each API version may go through up to three phases:

- **Alpha**
- **Beta**
- **General Availability** (GA)

### Version Numbering Format

The API version is specified using only the **major version number**, following this URL pattern:

```
/v{major}/{phase}
```

- For **Alpha** and **Beta** phases, include the `{phase}` in the URL.
- For the **General Availability** phase, the `{phase}` segment is **omitted**.

**Examples:**

- Alpha version: `/v1/alpha`
- Beta version: `/v1/beta`
- General Availability version: `/v1`

## Version Lifecycle and Evolution

### Phases Overview

#### Alpha Phase (Optional)

- **Purpose:** Invite-only testing with selected customers.
- **Access:** Not publicly available.
- **Usage:** Gathering feedback on new features.

#### Beta Phase (Optional)

- **Purpose:** Early access for all customers after Alpha validation.
- **Access:** Publicly available to all developers.
- **Usage:** Refining features with broader feedback.

#### General Availability Phase

- **Purpose:** Official, stable release for production use.
- **Access:** Publicly available and recommended for all integrations.
- **Usage:** Reliable operation with backward compatibility within the major version.

### Transition Between Phases

- **Alpha to Beta:** May involve breaking changes based on feedback.
- **Beta to General Availability:** May involve breaking changes; aiming for stability.
- **Skipping Phases:** Some API versions may go directly to Beta or General Availability, omitting earlier phases.

**Note:** Breaking changes are expected during transitions between phases.

## Breaking and Non-Breaking Changes

To maintain stability, Smile API differentiates between breaking and non-breaking (additive) changes.

### Breaking Changes

Breaking changes can disrupt existing integrations. These changes will be introduced only in a **new major API version**.

**Examples of Breaking Changes:**

- Removing an entire operation (endpoint).
- Removing or renaming a parameter.
- Removing or renaming a response field.
- Adding a new **required** parameter.
- Making a previously optional parameter required.
- Changing the type of a parameter or response field.
- Removing enum values.
- Adding a new validation rule to an existing parameter.
- Changing authentication or authorization requirements.

### Non-Breaking (Additive) Changes

Non-breaking changes enhance the API without affecting existing integrations. These changes will be available in all supported API versions within the same major version.

**Examples of Non-Breaking Changes:**

- Adding a new operation (endpoint).
- Adding a new **optional** parameter.
- Adding an optional request header.
- Adding a response field.
- Adding a response header.
- Adding enum values.

## API Version Support Policy

To provide ample time for migration and development, the Smile API supports each version according to the following timelines:

| **Phase**                | **Support Duration**                                                | **Recommendation**                                                                 |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Alpha**                | Supported for **6 months** after Beta release                       | Not for production use; intended for testing and feedback                          |
| **Beta**                 | Supported for **12 months** after General Availability release      | Suitable for early adopters; migration to GA is encouraged                         |
| **General Availability** | Supported for **24 months** after the next GA API version is released | Recommended for all production integrations                                        |

**Example Timeline:**

- **v1 Alpha:** Released January 2022
- **v1 Beta:** Released April 2022
  - **v1 Alpha** support ends **October 2022**
- **v1 General Availability:** Released July 2022
  - **v1 Beta** support ends **July 2023**
- **v2 General Availability:** Released January 2024
  - **v1 General Availability** support ends **January 2026**

## Specifying the API Version in Requests

Include the API version in your API requests using the major version number and, if applicable, the phase.

**URL Format:**
```
https://open.smileapi.io/v{major}/{phase}/...
```

- For **General Availability** versions, omit the `{phase}`.

**Examples:**

- **Alpha Version (v1):**
    ```
    https://open.smileapi.io/v1/alpha/resource
    ```

- **Beta Version (v1):**
    ```
    https://open.smileapi.io/v1/beta/resource
    ```

- **General Availability Version (v1):**
    ```
    https://open.smileapi.io/v1/resource
    ```


## Migration Guidelines

To ensure seamless integration with the Smile API, follow these guidelines when migrating between API versions:

### Before Migration

- **Review Documentation:** Read the release notes and updated API documentation.
- **Identify Breaking Changes:** Pay attention to any listed breaking changes in the new version.
- **Plan Updates:** Allocate resources to update and test your integration.

### During Migration

- **Use Beta Versions for Testing:** Utilize the Beta phase to test your integration and provide feedback.
- **Implement Incrementally:** Gradually update your codebase, starting with non-critical components.
- **Maintain Backward Compatibility:** If possible, support both the old and new API versions during the transition.

### After Migration

- **Monitor Performance:** Keep an eye on logs and analytics to catch any issues early.
- **Provide Feedback:** Share your experiences with the Smile API team to help improve future versions.
- **Deprecate Old Integrations:** Once confident, remove support for the deprecated API versions.
