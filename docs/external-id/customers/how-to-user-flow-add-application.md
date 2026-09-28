---
layout: Conceptual
title: Add an application to a user flow - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-user-flow-add-application
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add an application to a user flow to associate the application with a sign-up and sign-in user experience. Get guidance for updating the application configuration with application registration and tenant information.
ms.topic: how-to
ms.date: 2025-04-14T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 9234f64f-dde5-c7ce-e976-0ecc7bacee32
document_version_independent_id: c4571be1-217b-6a4e-54d7-928c2aeaa162
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-user-flow-add-application.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-user-flow-add-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-user-flow-add-application.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 712da614-b807-db59-0f55-3eabfcc12cbd
---

# Add an application to a user flow - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

A user flow defines the authentication methods a customer can use to sign in to your application and the information they need to provide during sign-up. After you [create a user flow](how-to-user-flow-sign-up-sign-in-customers), you can associate it with one or more of the applications registered in your external tenant.

Because you might want the same sign-in experience for all of your apps, you can add multiple apps to the same user flow. But only one sign-in experience is needed for an application, so you can add each application to just one user flow.

## Prerequisites

- **A sign-up and sign-in user flow**: Before you begin, [create the user flow](how-to-user-flow-sign-up-sign-in-customers) that you want to associate with your application.
- **Application registration**: In your external tenant, [register your application](/en-us/entra/identity-platform/quickstart-register-app).

## Add the application to the user flow

If you already registered your application in your external tenant, you can add it to the new user flow. This step activates the sign-up and sign-in experience for users who visit your application. An application can have only one user flow, but a user flow can be used by multiple applications.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
3. From the list, select your user flow.
4. In the left menu, under **Use**, select **Applications**.
5. Select **Add application**.

    ![Screenshot showing selecting an application for the user flow.](media/how-to-user-flow-add-application/assign-user-flow.png)
6. Select the application from the list. Or use the search box to find the application, and then select it.
7. Choose **Select**.

## Extension app

You might find an app named **b2c-extensions-app** in the application list. This app is created automatically inside the new directory, and it contains all extension attributes for your external tenant. If you want to collect information beyond the built-in attributes, you can create [custom user attributes](how-to-define-custom-attributes) and add them to your sign-up user flow. Custom attributes are also known as directory extension attributes, as they extend the user profile information stored in your customer directory. All extension attributes for your external tenant are stored in the **b2c-extensions-app**. Do not delete this app. You can learn more about this app [here](/en-us/azure/active-directory-b2c/extensions-app).