---
layout: Conceptual
title: Microsoft Entra user data collection - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-mfa-reporting-datacollection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: What information is used to help authenticate users by self-service password reset and Microsoft Entra multifactor authentication?
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: jpettere
locale: en-us
document_id: 7bc4198c-498c-adc5-ef47-9be82f2e39bd
document_version_independent_id: 754b007e-edc8-0f48-fba5-06d5dbd62b31
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-mfa-reporting-datacollection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-mfa-reporting-datacollection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-mfa-reporting-datacollection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 61f8547d-ba35-d8db-db23-4a612b0dd0c3
---

# Microsoft Entra user data collection - Microsoft Entra ID | Microsoft Learn

This article explains how to find user information collected by Microsoft Entra multifactor authentication (Cloud-based) and self-service password reset (SSPR) in the event you would like to remove it.

Note

For information about viewing or deleting personal data, please review Microsoft's guidance on the [Windows data subject requests for the GDPR](/en-us/microsoft-365/compliance/gdpr-dsr-windows) site. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## MFA information collected

MFA Server, the NPS Extension, and the Windows Server 2016 Microsoft Entra multifactor authentication AD FS Adapter collect and store the following information for 90 days.

Authentication Attempts (used for reporting and troubleshooting):

- Timestamp
- Username
- First Name
- Last Name
- Email Address
- User Group
- Authentication Method (Phone Call, Text Message, Mobile App, OATH Token)
- Phone Call Mode (Standard, PIN)
- Text Message Direction (One-Way, Two-Way)
- Text Message Mode (OTP, OTP + PIN)
- Mobile App Mode (Standard, PIN)
- OATH Token Mode (Standard, PIN)
- Authentication Type
- Application Name
- Primary Call Country Code
- Primary Call Phone Number
- Primary Call Extension
- Primary Call Authenticated
- Primary Call Result
- Backup Call Country Code
- Backup Call Phone Number
- Backup Call Extension
- Backup Call Authenticated
- Backup Call Result
- Overall Authenticated
- Overall Result
- Results
- Authenticated
- Result
- Initiating IP Address
- Devices
- Device Token
- Device Type
- Mobile App Version
- OS Version
- Result
- Used Check for Notification

Activations (attempts to activate an account in the Microsoft Authenticator mobile app):

- Username
- Account Name
- Timestamp
- Get Activation Code Result
- Activate Success
- Activate Error
- Activation Status Result
- Device Name
- Device Type
- App Version
- OATH Token Enabled

Blocks (used to determine blocked state and for reporting):

- Block Timestamp
- Block By Username
- Username
- Country Code
- Phone Number
- Phone Number Formatted
- Extension
- Clean Extension
- Blocked
- Block Reason
- Completion Timestamp
- Completion Reason
- Account Lockout
- Fraud Alert
- Fraud Alert Not Blocked
- Language

Bypasses (used for reporting):

- Bypass Timestamp
- Bypass Seconds
- Bypass By Username
- Username
- Country Code
- Phone Number
- Phone Number Formatted
- Extension
- Clean Extension
- Bypass Reason
- Completion Timestamp
- Completion Reason
- Bypass Used

Changes (used to sync user changes to MFA Server or Microsoft Entra ID):

- Change Timestamp
- Username
- New Country Code
- New Phone Number
- New Extension
- New Backup Country Code
- New Backup Phone Number
- New Backup Extension
- New PIN
- PIN Change Required
- Old Device Token
- New Device Token

## Gather data from NPS extension

Use the Microsoft Privacy portal to make a request for Export.

- MFA information is included in the export, which may take hours or days to complete.
- Occurrences of the username in the AzureMfa/AuthN/AuthNOptCh, AzureMfa/AuthZ/AuthZAdminCh, and AzureMfa/AuthZ/AuthZOptCh event logs are considered operational and duplicative to the information provided in the export.

## Delete data from NPS extension

Use the Microsoft Privacy portal to make a request for Account Close to delete all MFA cloud service information collected for this user.

- It may take up to 30 days for data to be fully removed.

## Gather data from Microsoft Entra multifactor authentication AD FS adapter

Use the Microsoft Privacy portal to make a request for Export.

- MFA information is included in the export, which may take hours or days to complete.
- Occurrences of the username in the AD FS Tracing/Debug event logs (if enabled) are considered operational and duplicative to the information provided in the export.

## Delete data from Microsoft Entra multifactor authentication AD FS adapter

Use the Microsoft Privacy portal to make a request for Account Close to delete all MFA cloud service information collected for this user.

- It may take up to 30 days for data to be fully removed.

## Gather data for Microsoft Entra multifactor authentication

Use the Microsoft Privacy portal to make a request for Export.

- MFA information is included in the export, which may take hours or days to complete.

## Delete data for Microsoft Entra multifactor authentication

Use the Microsoft Privacy portal to make a request for Account Close to delete all MFA cloud service information collected for this user.

- It may take up to 30 days for data to be fully removed.

## Delete data for self-service password reset

Users can add answers to security questions as part of SSPR. Security questions and answers are hashed to prevent unauthorized access. Only the hashed data is saved, so the security questions and answers can't be exported. Users can go to [My sign-ins](https://mysignins.microsoft.com/security-info) to edit or delete them. The only other information saved for SSPR is the user email address.

Those assigned the [Privileged Authentication Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#privileged-authentication-administrator) role can remove data collected for any user. On the **Users** page in Microsoft Entra ID, select **Authentication methods** and select a user to remove their phone or email address.