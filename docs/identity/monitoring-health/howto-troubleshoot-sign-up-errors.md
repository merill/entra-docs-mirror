---
layout: Conceptual
title: How to troubleshoot sign-up errors - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-troubleshoot-sign-up-errors
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to troubleshoot sign-up errors using Microsoft Entra reports in the Microsoft Entra admin center
ms.topic: troubleshooting
ms.date: 2025-06-30T00:00:00.0000000Z
locale: en-us
document_id: 3935803a-6fc0-0321-741c-fff561965dc4
document_version_independent_id: 3935803a-6fc0-0321-741c-fff561965dc4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-troubleshoot-sign-up-errors.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-troubleshoot-sign-up-errors
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-troubleshoot-sign-up-errors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a64540fe-8527-d2e4-ba05-88c466b3362e
---

# How to troubleshoot sign-up errors - Microsoft Entra ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../../includes/media/applies-to/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra sign-up logs help you troubleshoot sign-up failures for users of applications in your external tenant. This article describes how to isolate sign-up failures and understand the root causes.

### Sign-up error codes

To research information about specific sign-up error codes, you can use the following tools:

- Enter the error code into the **[Error code lookup tool](https://login.microsoftonline.com/error)** to get the error code description and remediation information.
- Search for an error code in the **[authentication and authorization error codes reference](../../identity-platform/reference-error-codes)**.

The following error codes are associated with sign-up events, but this list isn't exhaustive:

- **50181**: Unable to validate the OTP.

    - This error code appears when the one-time passcode the user is trying to enter can't be validated.
    - The user should request a new one-time passcode.
- **50182**: OTP is already expired.

    - This error code appears when the one-time passcode the user is trying to enter is expired.
    - The user should request a new one-time passcode.
- **1002027**: Some of the collected attributes were invalid.

    - One or more attributes entered by the user during sign-up weren't in a valid format.
    - The user should reenter the attributes.
- **399279**: User creation failed during self-service sign-up.

    - The user's account couldn't be created.
    - The user should retry the sign-up process.

The following codes are not actual errors. They indicate expected interruptions that occur due to the interactive nature of the sign-up process.

- **1002013**: User is prompted to enter Email One-Time-Passcode to verify ownership of email address.

    - This is an expected part of the signup flow, where a user is prompted to enter the one-time-passcode emailed to them to verify ownership of email address.
- **50140**: User is prompted with option to 'Keep me signed in' during the sign-in following sign-up.

    - This is an expected part of the sign-in flow, where a user is asked if they want to remain signed into this browser to make further sign-ins easier.

If an issue persists despite taking the recommended course of action, open a support request. For more information, see [how to get support for Microsoft Entra ID](../../fundamentals/how-to-get-support).