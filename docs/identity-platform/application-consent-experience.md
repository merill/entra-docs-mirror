---
layout: Conceptual
title: Consent experience for applications in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/application-consent-experience
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn more about the Microsoft Entra consent experiences to see how you can use it when managing and developing applications on Microsoft Entra ID
manager: pmwongera
ms.date: 2025-02-27T00:00:00.0000000Z
ms.reviewer: jawoods
ms.topic: concept-article
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3eef3157-a963-a2d8-0af7-e930d268c455
document_version_independent_id: e1331dee-44bc-2ef2-f8c2-2efa71638a06
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/application-consent-experience.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/application-consent-experience
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/application-consent-experience.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ece9eb7a-5236-fc66-939e-cdceb14476e1
---

# Consent experience for applications in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn

In this article, learn about the Microsoft Entra application consent user experience. You can intelligently manage applications for your organization and/or develop applications with a more seamless consent experience.

Consent is the process of a user granting authorization to an application to access protected resources on their behalf. An admin or user can be asked for consent to allow access to their organization/individual data.

The actual user experience of granting consent differs depending on policies set on the user's tenant, the user's scope of authority (or role), and the type of [permissions](permissions-consent-overview) requested by the client application. This means that application developers and tenant admins have some control over the consent experience. Admins have the flexibility of setting and disabling policies on a tenant or app to control the consent experience in their tenant. Application developers can dictate what types of permissions are being requested. They can also decide if they want to guide users through the user consent flow or the admin consent flow.

- **User consent flow** is when an application developer directs users to the authorization endpoint with the intent to record consent for only the current user.
- **Admin consent flow** is when an application developer directs users to the admin consent endpoint with the intent to record consent for the entire tenant. To ensure the admin consent flow works properly, application developers must list all permissions in the `RequiredResourceAccess` property in the application manifest. For more info, see [Application manifest](reference-app-manifest).

Note

For applications in external tenants customers can't consent to permissions themselves. An administrator will need to grant consent for the application to access resources on their behalf. For more information, see [Grant admin consent](quickstart-register-app#grant-admin-consent-external-tenants-only).

## Building blocks of the consent prompt

The consent prompt is designed to ensure users have enough information to determine if they trust the client application to access protected resources on their behalf. Understanding the building blocks helps users granting consent make more informed decisions and helps developers build better user experiences.

The following diagram and table provide information about the building blocks of the consent prompt.

![Building blocks of the consent prompt](media/application-consent-experience/consent_prompt.png)

| # | Component | Purpose |
| --- | --- | --- |
| 1 | User identifier | This identifier represents the user that the client application is requesting to access protected resources on behalf of. |
| 2 | Title | The title changes based on whether the users are going through the user or admin consent flow. In user consent flow, the title is "Permissions requested” while in the admin consent flow the title has another line "Accept for your organization." |
| 3 | App logo | This image should help users have a visual cue of whether this app is the app they intended to access. This image is provided by application developers and the ownership of this image isn't validated. |
| 4 | App name | This value should inform users which application is requesting access to their data. Note this name is provided by the developers and the ownership of this app name isn't validated. |
| 5 | Publisher name and verification | The blue "verified" badge means that the app publisher verified their identity using a Microsoft Partner Network account and completed the verification process. If the app is publisher verified, the publisher name is displayed. If the app isn't publisher verified, "Unverified" is displayed instead of a publisher name. For more information, read about [Publisher Verification](publisher-verification-overview). Selecting the publisher name displays more app information as available. The information includes the publisher name, publisher domain, date created, certification details, and reply URLs. |
| 6 | Microsoft 365 Certification | The Microsoft 365 Certification logo means that an app is vetted against controls derived from leading industry standard frameworks. It shows that strong security and compliance practices are in place to protect customer data. For more information, read about [Microsoft 365 Certification](/en-us/microsoft-365-app-certification/docs/certification). |
| 7 | Publisher information | Displays whether the application is published by Microsoft. |
| 8 | Permissions | This list contains the permissions being requested by the client application. Users should always evaluate the types of permissions being requested to understand what data the client application is authorized to access on their behalf. As an application developer, it's best to request access to the permissions with the least privilege. |
| 9 | Permission description | This value is provided by the service exposing the permissions. To see the permission descriptions, you must toggle the chevron next to the permission. |
| 10 | `https://myapps.microsoft.com` | This link allows users to review and remove any non-Microsoft applications that currently have access to their data. |
| 11 | Report it here | This link is used to report a suspicious app if you don't trust the app, if you believe it's impersonating another app, if it's likely to misuse your data, or for some other reason. |

## Common scenarios and consent experiences

The following section describes the common scenarios and the expected consent experience for each of them.

### App requires a permission that the user has the right to grant

In this consent scenario, the user accesses an app that requires a permission set that is within the user's scope of authority. The user is directed to the user consent flow.

Admins see another control on the traditional consent prompt that allows them to give consent on behalf of the entire tenant. The control is defaulted to off, so only when admins explicitly check the box is consent granted on behalf of the entire tenant. The check box only shows for at least the [Privileged Role Administrator role](../identity/role-based-access-control/permissions-reference#privileged-role-administrator), so Cloud Admin and App Admin don't see this checkbox.

![Consent prompt for scenario 1a](media/application-consent-experience/consent_prompt_1a.png)

Users see the traditional consent prompt.

![Screenshot that shows the traditional consent prompt.](media/application-consent-experience/consent_prompt_1b.png)

### App requires a permission that the user has no right to grant

In this consent scenario, the user accesses an app that requires at least one permission that is outside the user's scope of authority.

Admins see another control on the traditional consent prompt that allows them consent on behalf of the entire tenant.

![Consent prompt for scenario 1a](media/application-consent-experience/consent_prompt_1a.png)

Users who aren't an administrator are blocked from granting consent to the application, and they're told to ask their admin for access to the app. If admin consent workflow is enabled in the user's tenant, users are able to submit a request for admin approval from the consent prompt. For more information on admin consent workflow, see [Admin consent workflow](../identity/enterprise-apps/admin-consent-workflow-overview).

![Screenshot of the consent prompt telling the user to ask an admin for access to the app.](media/application-consent-experience/consent_prompt_2b.png)

### User is directed to the admin consent flow

In this consent scenario, the user navigates to or is directed to the admin consent flow.

Admin users see the admin consent prompt. The title and the permission descriptions changed on this prompt, the changes highlight the fact that accepting this prompt grants the app access to the requested data on behalf of the entire tenant.

![Consent prompt for scenario 3a](media/application-consent-experience/consent_prompt_3a.png)

Users are blocked from granting consent to the application, and they're told to ask their admin for access to the app.

![Screenshot of the consent prompt telling the user to ask an admin for access to the app.](media/application-consent-experience/consent_prompt_2b.png)

### Admin consent through the Microsoft Entra admin center

In this scenario, an administrator consents to all of the permissions that an application requests, which can include delegated permissions on behalf of all users in the tenant. The administrator grants consent through the **API permissions** page of the application registration in the [Microsoft Entra admin center](https://entra.microsoft.com).

[![Screenshot of explicit admin consent through the Microsoft Entra admin center.](media/consent-framework/grant-consent.png)](media/consent-framework/grant-consent.png#lightbox)

All users in that tenant don't see the consent dialog unless the application requires new permissions. To learn which administrator roles can consent to delegated permissions, see [Administrator role permissions in Microsoft Entra ID](../identity/role-based-access-control/permissions-reference).

Important

Granting explicit consent using the **Grant permissions** button is currently required for single-page applications (SPA) that use MSAL.js. Otherwise, the application fails when the access token is requested.

## Common Issues

This section outlines the common issues with the consent experience and possible troubleshooting tips.

- 403 error

    - Is the case a [delegated scenario](permissions-consent-overview)? What permissions does a user have?
    - Are necessary permissions added to use the endpoint?
    - Check the [token](https://jwt.ms/) to see if it has necessary claims to call the endpoint.
    - What permissions are consented to? Who consented?
- User is unable to consent

    - Check if tenant admin disabled user consent for your organization
    - Confirm if the permissions you requesting are admin-restricted permissions.
- User is still blocked even after admin consents

    - Check if [static permissions](consent-types-developer) are configured to be a superset of permissions requested dynamically.
    - Check if user assignment is required for the app.

## Troubleshoot known errors

For troubleshooting steps, see [Unexpected error when performing consent to an application](../identity/enterprise-apps/application-sign-in-unexpected-user-consent-error).