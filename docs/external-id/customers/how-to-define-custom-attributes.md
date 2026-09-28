---
layout: Conceptual
title: Define custom attributes - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-define-custom-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to create and define new custom attributes to be collected from users during sign-up and sign-in.
ms.topic: how-to
ms.date: 2026-03-27T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 14bfe426-f69b-e7ce-d2c9-e67cd0c86e8a
document_version_independent_id: 9ee885d3-a6b2-0db6-3685-28f9ec2440e2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-define-custom-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-define-custom-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-define-custom-attributes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0a635b4d-c29d-89cb-55a9-5eaebdc95edd
---

# Define custom attributes - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Tip

This article applies to user flows in external tenants. For information about workforce tenants, see [Collect custom user attributes during B2B collaboration sign-up](../user-flow-add-custom-attributes).

Note

This article covers attribute collection for **browser-delegated authentication** using user flows. If you use **native authentication**, you collect attributes through the MSAL SDK with the [native authentication user attribute builder](/en-us/entra/identity-platform/concept-native-authentication-user-attribute-builder?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json). For help choosing an approach, see [Choose an authentication approach](concept-choose-authentication-approach).

If your app requires more information than the built-in user attributes provide, you can add your own attributes. These attributes are called *custom user attributes*.

To define a custom user attribute, you first create the attribute at the tenant level so it can be used in any user flow in the tenant. Then you assign the attribute to your sign-up user flow and configure how you want it to appear on the sign-up page.

Learn more about custom user attributes in the [User profile attributes](concept-user-attributes) article.

## Create custom user attributes

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **External Identities** &gt; **Overview**.
4. Select **Custom user attributes**. The list contains all user attributes available in the tenant, including any custom user attributes that have been created. The **Attribute type** column indicates whether an attribute is built-in or custom.
5. Select **Add**. In the **Add an attribute** pane, enter a **Name** for the custom attribute (for example, "Terms of use").
6. In **Data Type**, choose **String**, **Boolean**, or **Int** depending on the [type of data and user input control](concept-user-attributes#custom-user-attributes-input-types) you want to create. **String** attributes have a default user input type value of **TextBox**, but you're able to change this in a later step (for example if you want to configure radio buttons or multiselect checkboxes).
7. (Optional) In **Description**, enter a description of the custom attribute for internal use. This description isn't visible to the user.

    [![Screenshot of the pane for adding an attribute.](media/how-to-define-custom-attributes/add-attribute.png)](media/how-to-define-custom-attributes/add-attribute.png#lightbox)
8. Select **Create**. The custom attribute is now available in the list of user attributes and can be added to your user flows.

## Include the custom user attribute in a sign-up flow

Follow these steps to add custom user attributes to a user flow you've already created. (If you need to create a new user flow, see [Create a sign-up and sign-in user flow for customers](how-to-user-flow-sign-up-sign-in-customers).)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
4. Select the user flow from the list.
5. Select **User attributes**. The list includes any custom user attributes you defined as described in the previous section. For example, the new **Terms of use** attribute now appears in the list. Choose all the attributes you want to collect from the user during sign-up.

    [![Screenshot of the user attribute options on the Create a user flow page.](media/how-to-define-custom-attributes/user-attributes.png)](media/how-to-define-custom-attributes/user-attributes.png#lightbox)
6. Select **Save**.

### Configure the user input types and page layout

On the **Page layout** page, you can indicate which attributes are required and arrange the display order. You can also edit attribute labels, create radio buttons or checkboxes, and add hyperlinks to more content (such as terms of use or a privacy policy).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
3. From the list, select your user flow.
4. Under **Customize**, select **Page layouts**. The attributes you chose to collect appear.
5. Edit the label for any attribute by selecting the value in the **Label** column and modifying the text.
6. Configure checkboxes or radio buttons:

    - **Single-select checkbox**: A Boolean attribute type renders as a single-select checkbox on the sign-up page. To configure the text that displays next to the checkbox, select and edit the value in the **Label** column. Use Markdown language to add hyperlinks. For details, see To configure a single-select checkbox (CheckboxSingleSelect)
    - **Multiselect checkboxes**: Find the **String** data type attribute you want to configure, and select the value in the **User Input Type** column to open the editor pane. Choose the **CheckboxMultiSelect** user input type and enter the values. For details, see To configure multiselect checkboxes (CheckboxMultiSelect).
    - **Radio buttons**: Find the **String** data type attribute you want to configure, and select the value in the **User Input Type** column to open the editor pane. Choose the **RadioSingleSelect** user input type and enter the values. For details, see To configure radio buttons (RadioSingleSelect)
7. Change the order of display by selecting an attribute and choosing **Move up**, **Move down**, **Move to top**, or **Move to bottom**.
8. Make an attribute required by selecting the checkbox in the **Required** column. All attributes can be marked as required. For multiselect checkboxes, "Required" means that the user must select at least one checkbox.
9. When all your changes are complete, select **Save**.

### Configure a single-select checkbox (CheckboxSingleSelect)

An attribute with a Boolean data type has a user input type of CheckboxSingleSelect. You can modify the text that displays next to the checkbox and include hyperlinks.

To configure a single-select checkbox, follow these steps:

1. On the **Page layouts** page, find the attribute with data type of **Boolean** that you want to configure.
2. Select the value in the **Label** column and enter the text you want to display next to the checkbox. Use Markdown language to add hyperlinks. For example:

    - To configure the label for a **Terms of use** attribute, you could enter:

        `I have read and agree to the [terms of use](https://woodgrove.com/terms-of-use)`.
    - Or, you could combine your terms of use and privacy policy into a single required checkbox:

        `I have read and agree to the [terms of use](https://woodgrove.com/terms-of-use) and the [privacy policy](https://woodgrove.com/privacy)`.
3. Select **Ok**.

    [![Screenshot of updating the checkbox label in the page layout options.](media/how-to-define-custom-attributes/page-layout-single-checkbox.png)](media/how-to-define-custom-attributes/page-layout-single-checkbox.png#lightbox)
4. On the **Page layouts** page, select **Save**.

### Configure multiselect checkboxes (CheckboxMultiSelect)

An attribute with a String data type can be configured as a CheckboxMultiSelect user input type, which is a series of one or more checkboxes that appear under the attribute label. The user can select one or more checkboxes. You can define the text for individual checkboxes and include hyperlinks to other content. Making this attribute "Required" means that the user must select at least one of the checkboxes.

1. On the **Page layouts** page, find the attribute with data type of **String** that you want to configure as a series of checkboxes.
2. Select the value in the **Label** column and enter the heading you want to display above the series of checkboxes, for example `How did you hear about us?`.
3. Select the value in the **User Input Type** column to open the editor pane.
4. In the editor pane, under **User input type**, select **CheckboxMultiSelect**.
5. For each checkbox you want to add, start on a new line and enter the following information:

    - Under **Text**, enter the text you want to display next to the checkbox. Use Markdown language to add hyperlinks.
    - Under **Values**, enter a value to be written on the user object and returned as the claim if the user selects the checkbox.
6. Select **Ok**.

    [![Screenshot of adding a multiselect checkbox to a string attribute in the page layout options.](media/how-to-define-custom-attributes/page-layout-multicheckbox.png)](media/how-to-define-custom-attributes/page-layout-multicheckbox.png#lightbox)
7. On the **Page layouts** page, select **Save**.

### Configure radio buttons (RadioSingleSelect)

An attribute with a String data type can be configured as a RadioSingleSelect user input type, which is a series of radio buttons that appear under the attribute label. The user can select only one radio button. You can define the text for individual radio buttons and include hyperlinks to other content.

1. On the **Page layouts** page, find the attribute with data type of **String** that you want to configure as a radio button or series of radio buttons.
2. Select the value in the **Label** column and enter the heading you want to display above the series of radio buttons, for example `Sweatshirt size`.
3. Select the value in the **User Input Type** column to open the editor pane.
4. In the editor pane, under **User input type**, select **RadioSingleSelect**.
5. For each radio button you want to add, start on a new line and enter the following information:

    - Under **Text**, enter the text you want to display next to the radio button. Use Markdown language to add hyperlinks.
    - Under **Values**, enter a value to be written on the user object and returned as the claim if the user selects the radio button.
6. Select **Ok**.

    [![Screenshot of adding a radio button to a string attribute in the page layout options.](media/how-to-define-custom-attributes/page-layout-radio-button.png)](media/how-to-define-custom-attributes/page-layout-radio-button.png#lightbox)
7. On the **Page layouts** page, select **Save**.

## Configure attribute visibility and editability with Microsoft Graph

You can control which attributes are shown or collected from users during sign-up by configuring the hidden and editable flags for each attribute. These settings aren't currently available in the admin center UI, but you can configure them using Microsoft Graph.

Each attribute supports the following flags:

- `hidden`: This flag is `false` by default so the attribute displays on the sign-up page, but you can set it to `true` to hide the attribute.
- `editable`: This flag is `true` by default to allow users to edit the attribute, but you can set it to `false` to make the attribute read-only.

Examples:

- To show the attribute on the page but prevent users from editing it, set `hidden` to `false` and `editable` to `false` .
- To hide the attribute from the page while still allowing it to be set programmatically, set `hidden` to `true` and `editable` to `true`. For example, you can assign a value to the attribute by [creating a custom authentication extension for an attribute collection submit event](../../identity-platform/custom-extension-attribute-collection?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json).

To set the hidden and editable flags using Microsoft Graph, use the [authenticationAttributeCollectionInputConfiguration](/en-us/graph/api/resources/authenticationattributecollectioninputconfiguration) resource type. For reference, see the example on [updating the page layout of a self-service sign up user flow](/en-us/graph/api/authenticationeventsflow-update#example-2-update-the-page-layout-of-a-self-service-sign-up-user-flow).

## Find the application ID for the extensions app

[Custom user attributes](concept-user-attributes#custom-user-attributes) are [stored in an app named *b2c-extensions-app*](concept-user-attributes#where-custom-user-attributes-are-stored). After a user enters a value for the custom attribute during sign-up, it's added to the user object and can be called via the Microsoft Graph API using the naming convention `extension_{appId-without-hyphens}_{custom-attribute-name}` where:

- `{appId-without-hyphens}` is the stripped version of the client ID for the *b2c-extensions-app*.
- `{custom-attribute-name}` is the name you assigned to the custom attribute.

Use these steps to find the application ID for the extensions app:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **App registrations** &gt; **All applications**.
3. Select the application **b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.**
4. On the **Overview** page, use the **Application (client) ID** value, for example: `12345678-abcd-1234-1234-ab123456789`, but remove the hyphens.

For example, if you create a custom attribute named **loyaltyNumber**, refer to it as `extension_12345678abcd12341234ab123456789_loyaltyNumber`

## Add custom user attributes to the ID token

When users sign-in to your app, the app receives an ID token, which includes the user details. These details are called token claims. If needed, you can include a custom user attribute to be available as a claim in the ID token that's returned to your app. To do so, follow the steps in [Add attributes to the ID token returned to your application](how-to-add-attributes-to-token) article.