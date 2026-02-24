# Extended Prisma SASE Integration with Prisma Browser

> ⚠️ **Disclaimer: POC Grade Code**
>
> This code is currently at **Proof of Concept (POC) grade**. It is intended for testing and development purposes only. It has not been fully vetted for production environments and is not officially supported by Palo Alto Networks. Use at your own risk.

## Overview

This repository contains a modified version of the Content Pack for the **Palo Alto Networks - Prisma SASE** integration (formerly Prisma Access) for Cortex XSOAR/XSIAM.

The primary goal of this modification is to introduce support for the **Prisma Browser API**, enabling programmatic management of browser users, devices, and policies directly from Cortex.

This extends the capabilities of the official marketplace pack found here:
[Prisma Access on Cortex Marketplace](https://cortex.marketplace.pan.dev/marketplace/details/PrismaAccess/)

## New Capabilities

The script has been updated to support the `/seb-api/v1/` endpoints. The following capabilities have been added:

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

### 4. Group & Policy Objects
* **List Device Groups:** View device groups.
* **List User Groups:** View user groups.
* **List Applications:** View configured applications.
* **List User Requests:** View access requests made by users.

## Added Commands

The following commands have been implemented in this version:

| Command | Description |
| :--- | :--- |
| `!prisma-sase-pb-user-list` | Lists all users in the Browser Management scope. |
| `!prisma-sase-pb-user-suspend` | Suspends a specific users (by ID or list of IDs). |
| `!prisma-sase-pb-user-resume` | Resumes a specific users (by ID or list of IDs). |
| `!prisma-sase-pb-device-list` | Lists devices (supports filtering by hostname/username). |
| `!prisma-sase-pb-device-get` | Returns details for a specific device by ID. |
| `!prisma-sase-pb-device-suspend` | Suspends a specific device (by ID or list of IDs). |
| `!prisma-sase-pb-device-resume` | Resumes a suspended device. |
| `!prisma-sase-pb-device-archive` | Archives a device. |
| `!prisma-sase-pb-device-restore` | Restores an archived device. |
| `!prisma-sase-pb-device-delete` | Deletes a device record. |
| `!prisma-sase-pb-device-group-list` | Lists device groups. |
| `!prisma-sase-pb-user-group-list` | Lists user groups. |
| `!prisma-sase-pb-application-list` | Lists applications. |
| `!prisma-sase-pb-user-request-list` | Lists user access requests. |
| `!prisma-sase-pb-user-request-get` | Returns details for a specific request by ID. |
| `!prisma-sase-pb-user-request-approve` | Approves a user request (optional `message` arg). |
| `!prisma-sase-pb-user-request-decline` | Declines a user request (optional `message` arg). |
| `!prisma-sase-pb-user-request-revoke` | Revokes an approved request (optional `message` arg). |

## Configuration

To use this script:
1.  Ensure your **Prisma SASE** instance is configured with the correct **TSG ID**, **Client ID**, and **Client Secret**.
2.  The Base URL should remain the standard API gateway (e.g., `https://api.sase.paloaltonetworks.com`). The script automatically handles the `/seb-api/v1/` routing.
3.  Upload the yaml file into Cortex BYOI

## Things to know
XSIAM supports real-time correlation rule while XDR not, hence specific correlation rules. 
