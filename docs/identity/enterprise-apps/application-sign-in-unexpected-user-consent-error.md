---
layout: Conceptual
title: Unexpected Error When Performing Consent to an Application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/application-sign-in-unexpected-user-consent-error
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: This article discusses errors that can occur during the process of consenting to an application and what you can do about them.
ms.topic: troubleshooting
ms.date: 2025-02-27T00:00:00.0000000Z
ms.reviewer: phsignor
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps
locale: en-us
document_id: 798bc53c-2589-c67c-a304-d820dae21476
document_version_independent_id: 5183fd8e-fd87-dd63-4686-79879186ba86
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/application-sign-in-unexpected-user-consent-error.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/application-sign-in-unexpected-user-consent-error
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/application-sign-in-unexpected-user-consent-error.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 4db0eb1a-48b4-aab5-ea36-d7e67f9975bb
---

# Unexpected Error When Performing Consent to an Application - Microsoft Entra ID | Microsoft Learn

This article discusses errors that can occur during the process of consenting to an application. If you're troubleshooting unexpected consent prompts that don't contain any error messages, see [Authentication scenarios for Microsoft Entra ID](../../identity-platform/authentication-vs-authorization).

Many applications that integrate with Microsoft Entra ID require permissions to access other resources in order to function. When these resources are also integrated with Microsoft Entra ID, the permission to access them is often requested through the common consent framework. A consent prompt appears, generally the first time that an application is in use. It can also occur on a subsequent use of the application.

Certain conditions must be true for a user to consent to the permissions that an application requires. If these conditions aren't met, the following errors can occur.

## Requesting unauthorized permissions

- **AADSTS90093**: `clientAppDisplayName` is requesting one or more permissions that you aren't authorized to grant. Contact an administrator, who can consent to this application on your behalf.
- **AADSTS90094**: `clientAppDisplayName` needs permission to access resources in your organization that only an admin can grant. Ask an admin to grant permission to this app before you can use it.

This error occurs when a user who isn't an administrator attempts to use an application that's requesting permissions that only an administrator can grant. To resolve this error, an administrator should grant access to the application on behalf of their organization.

This error can also occur when a user is prevented from consenting to an application because Microsoft detects that the permissions request is risky. In this case, an audit event is also logged with a category of **ApplicationManagement**, activity type of **Consent to application**, and status reason of **Risky application detected**.

Another scenario in which this error might occur is when the user assignment is required for the application, but no administrator consent was provided. In this case, the administrator must first provide tenant-wide admin consent for the application.

## Policy prevents granting permissions

- **AADSTS90093**: An administrator of `tenantDisplayName` set a policy that prevents you from granting `name of app` the permissions it's requesting. Contact an administrator of `tenantDisplayName`, who can grant permissions to this app on your behalf.

This error occurs when an administrator turns off the ability for users to consent to applications. Then a non-administrator user attempts to use an application that requires consent. To resolve this error, an administrator should grant access to the application on behalf of their organization.

## Intermittent problem

- **AADSTS90090**: The sign-in process encountered an intermittent problem recording the permissions you attempted to grant to `clientAppDisplayName`. Try again later.

This error indicates that an intermittent service-side problem occurred. The resolution is to attempt to consent to the application again.

## Resource not available in the tenant

- **AADSTS65005**: `clientAppDisplayName` is requesting access to a resource `resourceAppDisplayName` that isn't available in your organization `tenantDisplayName`.

Ensure that the resources that provide the requested permissions are available in your tenant, or contact an administrator of `tenantDisplayName`. Otherwise, there's a misconfiguration in how the application requests resources, and you should contact the application developer.

## Permissions mismatch

- **AADSTS65005**: The app requested consent to access resource `resourceAppDisplayName`. This request failed because it doesn't match how the app was preconfigured during app registration. Contact the app vendor.

This error occurs when the app that a user is trying to consent to requests permissions to access a resource application that can't be found in the organization's directory (tenant). This situation can occur for these reasons:

- The client application developer configured the application incorrectly, causing it to request access to an invalid resource. In this case, the application developer must update the configuration of the client application to resolve this problem.
- A service principal that represents the target resource application doesn't exist in the organization, or it existed in the past but is removed. To resolve this problem, you must provision a service principal for the resource application in the organization so that the client application can request permissions to it. The method that you use for provisioning the service principal depends on the type of application:

    - Acquiring a subscription for the resource application (Microsoft-published applications)
    - Consenting to the resource application
    - Granting the application permissions via the Microsoft Entra admin center
    - Adding the application from the Microsoft Entra application gallery

## Risky app

- **AADSTS900941**: Administrator consent is required. App is considered risky. (AdminConsentRequiredDueToRiskyApp)

    This app might be risky. If you trust this app, ask your admin to grant you access.
- **AADSTS900981**: An admin consent request was received for a risky app. (AdminConsentRequestRiskyAppWarning)

    This app might be risky. Only continue if you trust this app.

These messages appear when Microsoft determines that the consent request might be risky. Among many other factors, these errors might occur if a [verified publisher](../../identity-platform/publisher-verification-overview) isn't added to the app registration. The first error code and message appear to users when the [admin consent workflow](configure-admin-consent-workflow) is turned off. The second code and message appear to users and to admins when the admin consent workflow is turned on.

Users can't grant consent to apps that Microsoft detects as risky. Admins can grant the consent, but they should evaluate the app carefully and proceed with caution. If the app seems suspicious upon further review, admins can report it to Microsoft from the consent dialog.

## User declined to consent to access the app

- **AADSTS65004**: User declined to consent to access the app.

This error occurs during the admin consent workflow. After a user submits an admin consent approval for an application, another dialog appears with a **Back to app** button. When the user selects the button, Microsoft Entra ID sends an AADSTS65004 error to the redirect URI specified in the original authentication request. This error is an expected part of the admin consent workflow.

After the administrator review, and after the user approves the submitted admin consent, the user needs to begin a new authentication process with the application.