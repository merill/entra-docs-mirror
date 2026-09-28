---
layout: Conceptual
title: Add custom attributes - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/user-flow-add-custom-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add custom attributes to self-service sign-up flows in Microsoft Entra External ID. Extend the set of attributes stored on a guest account and customize the user experience.
ms.topic: how-to
ms.date: 2026-04-17T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 76c8fb28-412f-3743-8277-7b00eaf4d16d
document_version_independent_id: 17926e31-2e9e-f5bd-fb45-b835538cf82a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/user-flow-add-custom-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/user-flow-add-custom-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/user-flow-add-custom-attributes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c8985862-db23-734a-a985-5ccaa2b66cda
---

# Add custom attributes - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Tip

This article applies to B2B collaboration user flows in workforce tenants. For information about external tenants, see [Collect custom user attributes during external tenant sign-up](customers/how-to-define-custom-attributes).

For each application, you might have different requirements for the information you want to collect during sign-up. Microsoft Entra External ID comes with a built-in set of information stored in attributes, such as Given Name, Surname, City, and Postal Code. With Microsoft Entra External ID, you can extend the set of attributes stored on a guest account when the external user signs up through a user flow.

You can create custom attributes in the Microsoft Entra admin center and use them in your [self-service sign-up user flows](self-service-sign-up-user-flow). You can also read and write these attributes by using the [Microsoft Graph API](/en-us/azure/active-directory-b2c/microsoft-graph-operations). Microsoft Graph API supports creating and updating a user with extension attributes. Extension attributes in the Graph API are named by using the convention `extension_<extensions-app-id>_attributename`. For example:

```JSON
"extension_831374b3bd5041bfaa54263ec9e050fc_loyaltyNumber": "212342"
```

The `<extensions-app-id>` is specific to your tenant. To find this identifier, navigate to **Entra ID** &gt; **App registrations** &gt; **All applications**. Search for the app that starts with "aad-extensions-app" and select it. On the app's Overview page, note the Application (client) ID.

## Create a custom attribute

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **External identities** &gt; **Overview**.
3. Select **Custom user attributes**. The available user attributes are listed.

    [![Screenshot of the External identities overview page in the Microsoft Entra admin center, with Custom user attributes selected.](media/user-flow-add-custom-attributes/user-attributes.png)](media/user-flow-add-custom-attributes/user-attributes.png#lightbox)
4. To add an attribute, select **Add**.
5. In the **Add an attribute** pane, enter the following values:

    - **Name** - Provide a name for the custom attribute (for example, "Shoe size").
    - **Data Type** - Choose a data type (**String**, **Boolean**, or **Int**).
    - **Description** - Optionally, enter a description of the custom attribute for internal use. This description isn't visible to the user.

    ![Screenshot of the Add an attribute pane showing Name, Data Type, and Description fields before creating a custom user attribute.](media/user-flow-add-custom-attributes/add-an-attribute.png)
6. Select **Create**.

When you add a custom attribute to the list of user attributes, it becomes available for use in your user flows. However, the attribute is only created the first time it’s used in any user flow. Once you’ve created a new user through a user flow that includes the newly added custom attribute, the object can be queried in [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer). You should now see **ShoeSize** in the list of attributes collected during the sign-up journey on the user object. You can call the Graph API from your application to get the data from this attribute after it's added to the user object.