---
layout: Conceptual
title: Terms of Service and privacy statement for apps - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-add-terms-of-service-privacy-statement
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how you can configure the terms of service and privacy statement for apps registered to use Microsoft Entra ID.
manager: pmwongera
ms.custom: 
ms.date: 2023-12-15T00:00:00.0000000Z
ms.reviewer: sureshja
ms.topic: how-to
locale: en-us
document_id: 95fd06da-3a29-58f8-5e13-c86a6e5163f5
document_version_independent_id: c11c7199-53dd-51ab-4c48-3ba8b9978122
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-add-terms-of-service-privacy-statement.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-add-terms-of-service-privacy-statement
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-add-terms-of-service-privacy-statement.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 6fed63c4-69fe-92f2-a6ce-e638ad9e5811
---

# Terms of Service and privacy statement for apps - Microsoft identity platform | Microsoft Learn

Developers who build and manage multi-tenant apps that integrate with Microsoft Entra ID and Microsoft accounts should include links to the app's terms of service and privacy statement. The terms of service and privacy statement are surfaced to users through the user consent experience. They help your users know that they can trust your app. The terms of service and privacy statement are especially critical for user-facing multi-tenant apps--apps that are used by multiple directories or are available to any Microsoft account.

You are responsible for creating the terms of service and privacy statement documents for your app, and for providing the URLs to these documents. For multi-tenant apps that fail to provide these links, the user consent experience for your app will show an alert, which may discourage users from consenting to your app.

Note

- The terms of service and privacy statement links are not applicable to single-tenant apps
- If one or both of the two links are missing, your app will show an alert.

## User consent experience

The following example shows the user consent experience for a multi-tenant app when the terms of service and privacy statement are configured and when these links are not configured.

![Screenshots with and without a privacy statement and terms of service provided](media/howto-add-terms-of-service-privacy-statement/user-consent-exp-privacy-statement-terms-service.png)

## Formatting links to the terms of service and privacy statement documents

Before you add links to your app's terms of service and privacy statement documents, make sure the URLs follow these guidelines.

| Guideline | Description |
| --- | --- |
| Format | Valid URL |
| Valid schemas | HTTP and HTTPSWe recommend HTTPS |
| Max length | 2048 characters |

Examples: `https://myapp.com/terms-of-service` and `https://myapp.com/privacy-statement`

## Adding links to the terms of service and privacy statement

When the terms of service and privacy statement are ready, you can add links to these documents in your app using one of these methods:

- Through the Microsoft Entra admin center
- Using the app object JSON
- Using the Microsoft Graph API

### Using the Microsoft Entra admin center

Follow these steps to add links:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer).
2. Browse to **Entra ID** &gt; **Custom Branding**.
3. Select **Getting started**, and then select **Edit** for the **Default sign-in experience**.
4. Select **Footer** and fill out the URL for **Terms of Use** and **Privacy & Cookies**.
5. Select **Review + save**.

### Using the app object JSON

If you prefer to modify the app object JSON directly, you can use the manifest editor to include links to your app's terms of service and privacy statement.

1. Navigate to the **App Registrations** section and select your app.
2. Open the **Manifest** pane.
3. Ctrl+F, Search for "informationalUrls". Fill in the information.
4. Save your changes by downloading the app manifest, modifying it, and uploading it.

```json
    "informationalUrls": { 
        "termsOfService": "<your_terms_of_service_url>", 
        "privacy": "<your_privacy_statement_url>" 
    }
```

### Using the Microsoft Graph API

To programmatically [update your app](/en-us/graph/api/application-update), you can use the Microsoft Graph API to update all your apps to include links to the terms of service and privacy statement documents.

```
PATCH https://graph.microsoft.com/v1.0/applications/{applicationObjectId}
{ 
    "appId": "{your application object id}", 
    "info": { 
        "termsOfServiceUrl": "<your_terms_of_service_url>", 
        "supportUrl": null, 
        "privacyStatementUrl": "<your_privacy_statement_url>", 
        "marketingUrl": null, 
        "logoUrl": null 
    }
}
```

Note

- Be careful not to overwrite any pre-existing values you have assigned to any of these fields: `supportUrl`, `marketingUrl`, and `logoUrl`
- The Microsoft Graph API only works when you sign in with a Microsoft Entra account. Personal Microsoft accounts are not supported.