---
layout: Conceptual
title: Configure Printix for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/printix-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Printix.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8de4192b-3687-dab6-83cb-07e3350d1454
document_version_independent_id: 4ea12d24-eae6-d1c9-a15d-bcf0039fc61f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/printix-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/printix-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/printix-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a2bd7180-8bc1-fcd8-8caf-609875fe1889
---

# Configure Printix for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Printix with Microsoft Entra ID. When you integrate Printix with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Printix.
- Enable your users to be automatically signed-in to Printix with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Printix single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

Note

To test the steps in this article, we don't recommend using a production environment.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Rootly supports **SP** initiated SSO.
- Rootly supports **Just In Time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Printix from the gallery

To configure the integration of Printix into Microsoft Entra ID, you need to add Printix from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Printix** in the search box.
4. Select **Printix** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configuring and testing Microsoft Entra SSO for Printix

In this section, you configure and test Microsoft Entra single sign-on with Printix based on a test user called "Britta Simon".

For single sign-on to work, Microsoft Entra ID needs to know what the counterpart user in Printix is to a user in Microsoft Entra ID. In other words, a link relationship between a Microsoft Entra user and the related user in Printix needs to be established.

In Printix, assign the value of the **user name** in Microsoft Entra ID as the value of the **Username** to establish the link relationship.

To configure and test Microsoft Entra single sign-on with Printix, you need to perform the following steps:

1. **Configuring Microsoft Entra SSO** - to enable your users to use this feature.

    1. **Creating a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assigning the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Creating a Printix test user** - to have a counterpart of Britta Simon in Printix that's linked to the Microsoft Entra representation of user.
3. **Testing SSO** - to verify whether the configuration works.

## Configuring Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Printix** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Printix Domain and URLs** section, perform the following step:

    In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`

    Note

    The value isn't real. Update the value with the actual Sign-On URL. Contact [Printix Client support team](mailto:support@printix.net) to get the value.
6. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
7. Select **Save** button.
8. Sign on to your Printix tenant as an administrator.
9. In the menu on the top, select the icon at the upper right corner and select "**Authentication**".

    ![Screenshot shows Authentication selected from the menu.](media/printix-tutorial/menu.png)
10. On the **Setup** tab, select **Enable Azure/Office 365 authentication**.
11. On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".

    Attach the metadata xml file, which you downloaded from Microsoft Entra ID to [Printix support team](mailto:support@printix.net). Then they upload the xml file and provide a federation metadata URL.

    ![Screenshot shows the Printix.net page where you can specify a Federation metadata document.](media/printix-tutorial/metadata.png)
12. Select the "**Test**" button and select "**OK**" button if the test was successful.

    Microsoft Entra ID page will show after selecting the **test** button. "The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then select the **OK** button.

    ![Screenshot shows the results of the test.](media/printix-tutorial/test.png)
13. Select the **Save** button on "**Authentication**" page.

Tip

You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you're setting up the app! After adding this app from the **Active Directory &gt; Enterprise Applications** section, simply select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Microsoft Entra ID embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)

### Creating a Microsoft Entra test user

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

### Assigning the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to Printix.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Printix**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Creating a Printix test user

The objective of this section is to create a user called Britta Simon in Printix. Printix supports just-in-time provisioning, which is by default enabled.

There's no action item for you in this section. A new user is created during an attempt to access Printix if it doesn't exist yet.

Note

If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).

## Testing SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Printix Sign-on URL where you can initiate the login flow.
- Go to Printix Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Printix tile in the My Apps, this option redirects to Printix Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).