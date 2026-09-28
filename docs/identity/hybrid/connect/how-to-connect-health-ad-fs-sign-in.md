---
layout: Conceptual
title: AD FS sign-ins in Microsoft Entra ID with Connect Health - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-health-ad-fs-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document describes how to integrate AD FS sign-ins with the Microsoft Entra Connect Health sign-ins report.
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-05-15T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, sfi-ropc-nochange, msecd-doc-authoring-1012
locale: en-us
document_id: 0e449d4e-d2ac-89db-7967-2f16608059e3
document_version_independent_id: c21c845d-cba9-19ff-8cdd-d8a0a68c6f5b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-health-ad-fs-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-health-ad-fs-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-health-ad-fs-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 81d7f048-a121-eee9-fb4b-32131ab1cd25
---

# AD FS sign-ins in Microsoft Entra ID with Connect Health - Microsoft Entra ID | Microsoft Learn

AD FS sign-ins can now be integrated into the Microsoft Entra sign-ins report by using Connect Health. The [Microsoft Entra sign-ins Report](../../monitoring-health/concept-sign-ins) report includes information about when users, applications, and managed resources sign in to Microsoft Entra ID and access resources.

The Connect Health for AD FS agent correlates multiple Event IDs from AD FS, dependent on the server version, to provide information about the request and error details if the request fails. This information is correlated to the Microsoft Entra sign-in report schema and displayed in the Microsoft Entra sign-in report UX. Alongside the report, a new Log Analytics stream is available with the AD FS data and a new Azure Monitor Workbook template. The template can be used and modified for an in-depth analysis for scenarios such as AD FS account lockouts, bad password attempts, and spikes of unexpected sign-in attempts.

## Prerequisites

- Microsoft Entra Connect Health for AD FS installed and upgraded to the latest version (4.5.2466.0 or higher).
- Reports Reader role to view the Microsoft Entra sign-ins report.

## What data is displayed in the report?

The data available mirrors the same data available for Microsoft Entra sign-ins. Five tabs with information are available based on the type of sign-in, either Microsoft Entra ID or AD FS. Connect Health correlates events from AD FS, dependent on the server version, and matches them to the AD FS schema.

### User sign-ins

Each tab in the sign-ins blade shows the default values below:

- Sign-in date
- Request ID
- User name or user ID
- Status of the sign-in
- IP Address of the device used for the sign-in
- Sign-In Identifier

### Authentication Method Information

The following values may be displayed in the authentication tab. The authentication method is taken from the AD FS audit logs.

| Authentication Method | Description |
| --- | --- |
| Forms | Username/password authentication |
| Windows | Windows-integrated Authentication |
| Certificate | Authentication with SmartCard / VirtualSmart certificates |
| WindowsHelloForBusiness | This field is for auth with Windows Hello for Business. (Microsoft Passport Authentication) |
| Device | Displayed if Device Authentication is selected as “Primary” Authentication from intranet/extranet and Device Authentication is performed. There's no separate user authentication in this scenario. |
| Federated | AD FS didn't do the authentication but sent it to a third party identity provider |
| SSO | If a single-sign-on token was used, this field is visible. If the SSO has an MFA, it shows as Multifactor |
| Multifactor | If a single sign-on token has an MFA and that was used for authentication, this field displays as Multifactor |
| Microsoft Entra multifactor authentication | Microsoft Entra multifactor authentication is selected as the Additional Authentication Provider in AD FS and was used for authentication |
| ADFSExternalAuthenticationProvider | This field is if a third-party authentication provider was registered and used for authentication |

### AD FS Additional Details

The following details are available for AD FS sign-ins:

- Server Name
- IP Chain
- Protocol

### Enabling Log Analytics and Azure Monitor

Log Analytics can be enabled for the AD FS sign-ins and can be used with any other Log Analytics integrated components, such as Sentinel.

Note

AD FS sign-ins may increase Log Analytics cost significantly, depending on the amount of sign-ins to AD FS in your organization. To enable and disable Log Analytics, select the checkbox for the stream.

To enable Log Analytics for the feature, navigate to the Log Analytics blade and select "ADFSSignIns" stream. This selection allows AD FS sign-ins to flow into Log Analytics.

To access the updated Azure Monitor Workbook template, navigate to "Azure Monitor Templates", and select the "sign-ins" Workbook. For more information about Workbooks, visit [Azure Monitor Workbooks](https://aka.ms/adfssigninspreview).

### Frequently Asked Questions

***What are the types of sign-ins that I may see?*** The sign-in report supports sign-ins through O-Auth, WS-Fed, SAML, and WS-Trust protocols.

***How are different types of sign-ins shown in the sign-in report?*** If a Seamless SSO sign-in is performed, there is one row for the sign-in with one correlation ID. If a single factor authentication is performed, two rows are populated with the same correlation ID, but with two different authentication methods (that is, Forms, SSO). In cases of multifactor authentication, there are three rows with a shared correlation ID and three corresponding Authentication Methods (that is, Forms, Microsoft Entra multifactor authentication, Multifactor). In this particular example, the multifactor in this case shows that the SSO has an MFA.

***What are the errors that I can see in the report?***

For a full list of AD FS related errors that are populated in the sign-in report and descriptions, visit [Microsoft Entra Connect Health Alert Catalog](how-to-connect-health-alert-catalog#alerts-for-active-directory-federation-services)

***I am seeing “00000000-0000-0000-0000-000000000000” in the “User” section of a sign-in. What does that mean?*** If the sign-in failed and the attempted UPN doesn't match an existing UPN, the “User”, “Username”, and “User ID” fields are “00000000-0000-0000-0000-000000000000” and the “Sign-in Identifier” populated with the attempted value the user entered. In these cases, the user attempting to sign-in doesn't exist.

***How can I correlate my on-premises events to the Microsoft Entra sign-ins report?*** The Microsoft Entra Connect Health agent for AD FS correlates event IDs from AD FS dependent on server version. The events are available on the Security Log of the AD FS servers.

***Why do I see NotSet or NotApplicable in the Application ID/Name for some AD FS sign-ins?*** The AD FS sign-in report displays OAuth Ids in the Application ID field for OAuth sign-ins. In the WS-Fed, WS-Trust sign-in scenarios, the application ID is NotSet or NotApplicable and the Resource IDs and Relying Party identifiers are present in the Resource ID field.

***Why do I see Resource ID and Resource Name fields as "Not Set"?*** The ResourceId/Name fields are "NotSet" in some error cases, such as "Username and Password incorrect" and in WSTrust based failed sign-ins.

***Are there any more known issues with the report in preview?*** The report has a known issue where the "Authentication Requirement" field in the "Basic Info" tab are populated as a single factor authentication value for AD FS sign-ins regardless of the sign-in. Additionally, the Authentication Details tab displays "Primary or Secondary" under the Requirement field, with a fix in progress to differentiate Primary or Secondary authentication types.