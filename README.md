# Prisma Browser integration for Cortex

> ⚠️ **Disclaimer: POC Grade Code**
>
> This code is currently at **Proof of Concept (POC) grade**. It is intended for testing and development purposes only. It has not been fully vetted for production environments and is not officially supported by Palo Alto Networks. Use at your own risk.

## Overview

The primary goal of this integration is to introduce support for the **Prisma Browser API**, enabling programmatic management of browser users, devices, and policies directly from Cortex.


## New Capabilities

The script has been updated to support the `/seb-api/v1/` endpoints from https://pan.dev/prisma-browser/. The following capabilities have been added:

### 1. User Management
* **List Users:** Retrieve a list of users configured for Browser Access.
* **Lifecycle Actions:** Perform the following actions on users:
    * Suspend
    * Resume

### 2. Device Management
* **List Devices:** Search and list devices with filtering options.
* **Get Device Details:** Retrieve detailed information for a specific device.
* **Lifecycle Actions:** Perform the following actions on devices:
    * Suspend
    * Resume
    * Archive
    * Restore
    * Delete

### 3. User Request Management
* **List Requests:** View access requests submitted by users.
* **Get Request Details:** Retrieve specific details for a single request.
* **Decision Actions:** Approve or Decline pending requests with optional justification messages.
* **Revocation:** Revoke previously approved requests.

### 4. Group Objects
* **List Device Groups:** View device groups.
* **List User Groups:** View user groups.
* **List Applications:** View configured applications.
* **List User Requests:** View access requests made by users.

### 5. Policy access and data
* **List policies:** Lists policy access and data rules.
* **Update policy to add a user:** Updates/patches a policy access and data rule by adding users.

### 6. Publishes the draft configuration
* **Config Publish:** Publishes the draft configuration.

## Added Commands

The following commands have been implemented in this version:

| Command | Description |
| :--- | :--- |
| `!pb-user-list` | Lists all users in the Browser Management scope. |
| `!pb-user-suspend` | Suspends a specific users (by ID or list of IDs). |
| `!pb-user-resume` | Resumes a specific users (by ID or list of IDs). |
| `!pb-device-list` | Lists devices (supports filtering by hostname/username). |
| `!pb-device-get` | Returns details for a specific device by ID. |
| `!pb-device-suspend` | Suspends a specific device (by ID or list of IDs). |
| `!pb-device-resume` | Resumes a suspended device. |
| `!pb-device-archive` | Archives a device. |
| `!pb-device-restore` | Restores an archived device. |
| `!pb-device-delete` | Deletes a device record. |
| `!pb-device-group-list` | Lists device groups. |
| `!pb-user-group-list` | Lists user groups. |
| `!pb-application-list` | Lists applications. |
| `!pb-user-request-list` | Lists user access requests. |
| `!pb-user-request-get` | Returns details for a specific request by ID. |
| `!pb-user-request-approve` | Approves a user request (optional `message` arg). |
| `!pb-user-request-decline` | Declines a user request (optional `message` arg). |
| `!pb-user-request-revoke` | Revokes an approved request (optional `message` arg). |
| `!pb-policy-access-and-data-list` | Lists policy access and data rules. |
| `!pb-policy-access-and-data-rule-update-user` | Updates/patches a policy access and data rule by adding users with their unique User IDs. |
| `!pb-config-publish` | Publishes the draft configuration. |

## Configuration

To use this script:
1.  Ensure your **Prisma Broswer** instance is configured with the correct **TSG ID**, **Client ID**, and **Client Secret**.
2.  The Base URL should remain the standard API gateway (e.g., `https://api.strata.paloaltonetworks.com`). The script automatically handles the `/seb-api/v1/` routing.
3.  Upload the yaml file into Cortex BYOI

## Things to know
XSIAM supports real-time correlation rule while XDR not, hence specific correlation rules. 
