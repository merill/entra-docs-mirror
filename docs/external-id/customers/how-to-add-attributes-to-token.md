---
layout: Conceptual
title: Add attributes to token claims - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-add-attributes-to-token
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add built-in user attributes and custom attributes as claims to the application token. Use directory extension attributes for sending user data to applications in token claims.
ms.topic: how-to
ms.date: 2025-09-16T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: cb1f59c6-312d-7e5c-3c70-175bfb6006ff
document_version_independent_id: dd701916-2f00-e62e-686c-a2fc384861d8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-add-attributes-to-token.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-add-attributes-to-token
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-add-attributes-to-token.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1a6bf396-290b-6a25-db0b-c115f691fbb9
---

# Add attributes to token claims - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

User attributes are values collected from the user during self-service sign-up. In addition to built-in user attributes, you can create custom attributes when you need to collect additional information. Because your application might rely on certain user attributes to function as designed, you can add any of these attributes to the token that is sent from Microsoft Entra ID to your application.

You can specify which built-in or custom attributes you want to include as claims in the token that Microsoft Entra ID sends to your application.

## Prerequisites

- [Register the application](/en-us/entra/identity-platform/quickstart-register-app) with Microsoft Entra ID.
- [Create a sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers) and selected the attributes you want to collect during sign-up.
- [Create the custom attributes](how-to-define-custom-attributes) you want to include.

## Add built-in or custom attributes to the token

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select your application in the list to open the application's **Overview** page.

    ![Screenshot of the overview page of the app registration.](media/how-to-add-attributes-to-token/select-app.png)
4. In the **Essentials** section, under **Managed application in local directory**, select the link showing the name of your application.

    ![Screenshot of the managed application in local directory link.](media/how-to-add-attributes-to-token/managed-app-in-local-directory-link.png)
5. Under **Manage**, select **Single Sign-on**.
6. In the **Attributes & Claims** section, select the **Edit** icon.

    ![Screenshot of the attributes and claims section and the edit icon.](media/how-to-add-attributes-to-token/single-sign-on-edit.png)

### To add a built-in attribute to the token as a claim

1. On the **Attributes & Claims** page, select **Add new claim**.
2. Enter a **Name**.
3. Next to **Source**, select **Attribute**. Then use the drop-down list to select the built-in attribute.

    ![Screenshot of the drop-down list of built-in attributes.](media/how-to-add-attributes-to-token/add-built-in-claim.png)
4. Select **Save**. Repeat for all built-in attributes you want to add.

### To add a custom attribute to the token as a claim

1. On the **Attributes & Claims** page, select **Add new claim**.
2. Enter a **Name**.
3. Next to **Source**, select **Directory schema extension**.

    ![Screenshot of the Directory schema extension option.](media/how-to-add-attributes-to-token/manage-claim-directory-schema.png)
4. In the **Select Application** pane, select **b2c-extensions-app** (the app that contains all extension attributes for your external tenant), and then choose **Select**.
5. In the **Add Extension Attributes** pane, find the custom attribute you want to add as a claim to the token, and then select it.
6. Select **Add**.
7. Select **Save**. Repeat for each custom attribute you want to add.

### Update the application manifest to accept mapped claims in Microsoft Graph App Manifest(New)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select your application in the list to open the application's **Overview** page.
4. In the left menu, under **Manage**, select **Manifest** to open the application manifest.
5. Find the **acceptMappedClaims** key and set its value to **true**.
6. Find the **isFallbackPublicClient** key and set its value to **true**.
7. Select **Save**.