---
layout: Conceptual
title: How to configure app instance property lock in your applications - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-configure-app-instance-property-locks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: How to increase app security by configuring property modification locks for sensitive properties of the application.
manager: pmwongera
ms.date: 2023-10-26T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3a4c0d6a-08c8-8015-27e8-016e918a605c
document_version_independent_id: 81cda09b-1d45-4762-9940-b5f77da182ae
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-configure-app-instance-property-locks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-configure-app-instance-property-locks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-configure-app-instance-property-locks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 6ecb8fe6-c62e-b363-7265-aa082e2cec31
---

# How to configure app instance property lock in your applications - Microsoft identity platform | Microsoft Learn

Application instance lock is a feature in Microsoft Entra ID that allows sensitive properties of a multitenant application object to be locked for modification after the application is provisioned in another tenant. This feature provides application developers with the ability to lock certain properties if the application doesn't support scenarios that require configuring those properties.

## What are sensitive properties?

The following property usage scenarios are considered as sensitive:

- Credentials where usage type is `Sign`. This is a scenario where your application supports a SAML flow.
- Credentials where usage type is `Verify`. In this scenario, your application supports an OIDC client credentials flow.
- `TokenEncryptionKeyId` which specifies the keyId of a public key from the keyCredentials collection. When configured, Microsoft Entra ID encrypts all the tokens it emits by using the key to which this property points. The application code that receives the encrypted token must use the matching private key to decrypt the token before it can be used for the signed-in user.

Note

App instance lock is enabled by default for all new applications created using the Microsoft Entra admin center.

## Configure an app instance lock

To configure an app instance lock:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the tenant containing the app registration from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **App registrations**.
4. Select the application you want to configure.
5. Select **Authentication**, and then select **Configure** under the *App instance property lock* section.

    ![Screenshot of an app registration's app instance lock.](media/howto-configure-app-instance-property-locks/app-instance-lock-configure-overview.png)
6. In the **App instance property lock** pane, enter the settings for the lock. The table following the image describes each setting and their parameters.

    ![Screenshot of an app registration's app instance property lock context pane.](media/howto-configure-app-instance-property-locks/app-instance-lock-configure-properties.png)

    | Field | Description |
    | --- | --- |
    | **Enable property lock** | Specifies if the property locks are enabled. |
    | **All properties** | Locks all sensitive properties without needing to select each property scenario. |
    | **Credentials used for verification** | Locks the ability to add or update credential properties used for verification. |
    | **Credentials used for signing tokens** | Locks the ability to add or update credential properties used for signing tokens. |
    | **Token Encryption KeyId** | Locks the ability to change the `tokenEncryptionKeyId` property. |
7. Select **Save** to save your changes.

## Configure app instance lock using Microsoft Graph

You manage the app instance lock feature through the **servicePrincipalLockConfiguration** property of the [application](/en-us/graph/api/resources/application) object of the multitenant app. For more information, see [Lock sensitive properties for service principals](/en-us/graph/tutorial-applications-basics#lock-sensitive-properties-for-service-principals).