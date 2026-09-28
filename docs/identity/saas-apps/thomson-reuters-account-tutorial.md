---
layout: Conceptual
title: Configure Thomson Reuters Account for single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/thomson-reuters-account-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Thomson Reuters Account.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2026-05-07T00:00:00.0000000Z
locale: en-us
document_id: 349aa516-c107-0b61-b0a3-214ccda14804
document_version_independent_id: 349aa516-c107-0b61-b0a3-214ccda14804
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/thomson-reuters-account-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/thomson-reuters-account-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/thomson-reuters-account-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3fb1df4b-1cfe-9fe9-9bc8-2ad72ebf03b0
---

# Configure Thomson Reuters Account for single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Thomson Reuters Account with Microsoft Entra ID. When you integrate Thomson Reuters Account with Microsoft Entra ID, users have a seamless single sign-on experience with the wide range of applications from Thomson Reuters that their organization has subscribed to. Also, you can:

- Control in Microsoft Entra ID who has access to Thomson Reuters Account.
- Enable your users to be automatically signed-in to Thomson Reuters Account with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Thomson Reuters Account single sign-on (SSO) enabled subscription.

## Add Thomson Reuters Account from the gallery

To configure the integration of Thomson Reuters Account into Microsoft Entra ID, you need to add Thomson Reuters Account from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **+ New application**.
3. In the **Add from the gallery** section, enter **Thomson Reuters Account** in the search box.
4. Select **Thomson Reuters Account** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Thomson Reuters Account** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. For the **Identifier (Entity ID)** value, configure as follows:

    - In the **Identifier (Entity ID)** select `trtasso.thomson.com` (by default) and proceed to step 5.b.
    - In the **Identifier (Entity ID)** text box, enter the URL: `trtasso.thomson.com_TRAccount `.

    Note

    If there’s an existing SSO configuration that is used to access Thomson Reuters products, then you won’t be able to select and save `trtasso.thomson.com` as the Identifier/Entity ID. In such a case you’ll get the below error. So, switch to `trtasso.thomson.com_TRAccount` as default by checking the checkbox next to it and delete the `trtasso.thomson.com` Entity ID else you won’t be able to save the configuration.

    [![Screenshot that shows the identifier checkbox.](media/thomson-reuters-account-tutorial/identifier.png)](media/thomson-reuters-account-tutorial/identifier.png#lightbox)

    b. In the **Reply URL** text box, type the URL: `https://trtasso.thomson.com/sp/ACS.saml2`
6. Thomson Reuters Account application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes, whereas **nameidentifier** is mapped with **user.userprincipalname**. Thomson Reuters Account application expects **nameidentifier** to be mapped with **user.objectid**, so you need to edit the attribute mapping by selecting **Edit** icon and change the attribute mapping.

    | Name | Microsoft Entra ID attribute mapping | Value |
    | --- | --- | --- |
    | Unique UserIdentifier (Name ID) | user.objectid | A value that is both unique and persistent. Don't use an email address as that can change over time. |
    | emailaddress | user.emailaddress | Email address of the user |
    | givenname | user.givenname | First name of user |
    | surname | user.surname | Last name of user |
    | name | user.displayname | Full name of user |
7. If you have chosen the **Identifier (Entity ID)** as `trtasso.thomson.com_TRAccount`, then select the **Edit** option in **Attributes and Claims** and in the next page, select and expand **Advanced settings**, select the **Edit** option right next to **Advanced SAML claims** options. Once you do that, a pane will appear to the right from which you have to check the **Append application ID to issuer** and select **Save**.
8. On the **Set up single sign-on with SAML** page, in the SAML Signing Certificate section, select copy button to copy **App Federation Metadata Url**.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

## Configure Thomson Reuters Account SSO

To configure single sign-on on Thomson Reuters' side, you need to send the below details to the representative from Thomson Reuters whom you are working with to set up SSO:

1. The **App Federation Metadata Url** of your configuration on Microsoft Entra ID.
2. The **Identifier (Entity ID)** that was chosen (`trtasso.thomson.com` or `trtasso.thomson.com_TRAccount`).
3. The **Email domains** of users from your organization that would access Thomson Reuters applications (This is used by the Thomson Reuters team to enable SSO for those email domains).