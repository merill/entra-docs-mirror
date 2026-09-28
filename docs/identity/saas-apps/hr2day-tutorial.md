---
layout: Conceptual
title: Configure HR2day by Merces for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/hr2day-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra ID and HR2day by Merces.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: e66ec85a-9da9-9ffe-9f83-03862edfea52
document_version_independent_id: 8f3bd495-4a0c-14a1-1d31-477d293dd830
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/hr2day-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/hr2day-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/hr2day-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9b350801-a43f-1913-a3cf-afa4f4f1621f
---

# Configure HR2day by Merces for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate HR2day by Merces with Microsoft Entra ID. When you integrate HR2day by Merces with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to HR2day by Merces.
- Enable your users to be automatically signed-in to HR2day by Merces with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To configure Microsoft Entra integration with HR2day by Merces, you need the following items:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- HR2day by Merces single sign-on enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- HR2day by Merces supports **SP** initiated SSO.

## Add HR2day by Merces from the gallery

To configure the integration of HR2day by Merces into Microsoft Entra ID, you need to add HR2day by Merces from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **HR2day by Merces** in the search box.
4. Select **HR2day by Merces** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for HR2day by Merces

Configure and test Microsoft Entra SSO with HR2day by Merces using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in HR2day by Merces.

To configure and test Microsoft Entra SSO with HR2day by Merces, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure HR2day by Merces SSO**- to configure the single sign-on settings on application side.
    1. **Create HR2day by Merces test user** - to have a counterpart of B.Simon in HR2day by Merces that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **HR2day by Merces** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://hr2day.force.com/<companyname>`

    b. In the **Sign on URL** text box, type a URL using the following pattern: `https://<tenantname>.force.com/<instancename>`

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. Select **Edit** icon to open **User Attributes** dialog.

    ![Screenshot shows User Attributes with the Edit icon selected.](common/edit-attribute.png)

    Note

    Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant. You need this value to complete the steps in the next section.
7. In the **User Claims** section on the **User Attributes** dialog, edit the claims by using **Edit icon** or add the claims by using **Add new claim** to configure SAML token attribute as shown in the image above and perform the following steps:

    | Name | Source Attribute |
    | --- | --- |
    | ATTR\_LOGINCLAIM | `join([mail],"102938475Z","@"` |
    |  |  |

    a. Select **Add new claim** to open the **Manage user claims** dialog.

    ![Screenshot shows User claims with the option to Add new claim.](common/new-save-attribute.png)

    ![Screenshot shows the Manage user claims dialog box where you can enter the values described.](common/new-attribute-details.png)

    b. In the **Name** textbox, type the attribute name shown for that row.

    c. Leave the **Namespace** blank.

    d. Select Source as **Attribute**.

    e. From the **Source attribute** list, type the attribute value shown for that row.

    f. Select **Ok**

    g. Select **Save**.
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
9. On the **Set up HR2day by Merces** section, copy the appropriate URL(s) as per your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to HR2day by Merces.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **HR2day by Merces**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure HR2day by Merces SSO

To configure single sign-on on **HR2day by Merces** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [HR2day by Merces support team](mailto:servicedesk@merces.nl). They set this setting to have the SAML SSO connection set properly on both sides.

Note

Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.

### Create HR2day by Merces test user

In this section, you create a user called Britta Simon in HR2day by Merces. Work with [HR2day by Merces support team](mailto:servicedesk@merces.nl) to add the users in the HR2day by Merces platform. Users must be created and activated before you use single sign-on.

Note

If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to HR2day by Merces Sign-on URL where you can initiate the login flow.
- Go to HR2day by Merces Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the HR2day by Merces tile in the My Apps, this option redirects to HR2day by Merces Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).