---
layout: Conceptual
title: Configure Skills Base for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/skillsbase-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Skills Base.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
locale: en-us
document_id: 510e184d-fd24-9e6b-4a61-fe85da32b931
document_version_independent_id: d32db9f3-b09f-ccd3-e711-a025aadaa271
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/skillsbase-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/skillsbase-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/skillsbase-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d2eccab6-6766-a290-08df-39392b8fcc02
---

# Configure Skills Base for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you will learn how to integrate Skills Base with Microsoft Entra ID. When you integrate Skills Base with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Skills Base.
- Enable your users to be automatically signed-in to Skills Base with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Skills Base is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Skills Base instance with a license that includes the **Single Sign-On Module**.
- A Skills Base Administrator account (with local login email/password).
- **Single Sign On** feature is enabled (in **Administration &gt; Modules &gt; Single Sign-On Module**).

## Scenario description

In this article, you will configure and test Microsoft Entra single sign-on with Skills Base.

- Skills Base supports **SP** initiated SSO.
- Skills Base supports **Just In Time** user provisioning.

Note

Skills Base doesn't support **IdP** initiated SSO.

## Add Skills Base from the gallery

To configure the integration of Skills Base with Microsoft Entra ID, you need to add Skills Base from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Skills Base** in the search box.
4. Select **Skills Base** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Skills Base

Configure and test Microsoft Entra SSO with Skills Base using a test user called **B.Simon**. If **Just In Time** user provisioning is not enabled, for SSO to work you need to establish a link relationship between a Microsoft Entra user and the related user in Skills Base.

To configure and test Microsoft Entra SSO with Skills Base, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Skills Base SSO**- to configure the single sign-on settings on application side.
    1. **Create Skills Base test user** - to have a counterpart of B.Simon in Skills Base that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Skills Base** Enterprise Application Overview page.
3. Under **Getting Started** section select **Get started** under **2. Set up single sign on**.
4. On the **Select a single sign-on method** page, select **SAML**.
5. On the **Set up Single Sign-On with SAML** page, select the **Upload metadata file** button at the top of the page.
6. Select the **Select a file** icon and select the metadata file that you downloaded from Skills Base.
7. Select **Add**

    ![Screenshot of showing Upload SP metadata.](common/browse-upload-metadata.png)
8. On the **Basic SAML Configuration** page, in the **Sign on URL** text box, enter your Skills Base shortcut link, which should be in the format: `https://app.skills-base.com/o/<customer-unique-key>`

    Note

    You can get the Sign on URL from the Skills Base application. Please log in as an Administrator and to go to **Administration &gt; Settings &gt; Instance details &gt; Shortcut link**. Copy the shortcut link and paste it into the **Sign on URL** textbox in Microsoft Entra ID.
9. Select **Save**
10. Close the **Basic SAML Configuration** dialog.
11. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, next to **Federation Metadata XML**, select **Download** to download the Federation Metadata XML and save it on your computer.

![Screenshot of showing The Certificate download link.](common/metadataxml.png)

## Configure Skills Base SSO

1. Log in to Skills Base as an Administrator.
2. From the left side of menu, select **Administration &gt; Authentication**.

    ![Screenshot of showing The Authentication menu.](media/skillsbase-tutorial/admin.png)
3. On the **Authentication** page in the **Identity Providers** section, select **Add identity provider**.

    ![Screenshot shows the &quot;Add identity provider&quot; button.](media/skillsbase-tutorial/configuration.png)
4. Select **Add** to use the default settings.

    ![Screenshot shows the Authentication page where you can enter the values described.](media/skillsbase-tutorial/save-configuration.png)
5. In the **Application Details** panel, next to **SAML SP Metadata**, select **Download XML File** and save the resulting file on your computer.

    ![Screenshot shows the Application Details panel where you can download the SP Metadata file.](media/skillsbase-tutorial/download-sp-metadata.png)
6. In the **Identity Providers** section, select the **edit** button (denoted by a pencil icon) for the Identity Provider record you added.

    ![Screenshot of showing Edit Identity Providers button.](media/skillsbase-tutorial/edit-identity-provider.png)
7. In the **Edit identity provider** panel, for **SAML IdP Metadata** select **Upload an XML file**
8. Select **Browse** to choose a file. Select the Federation Metadata XML file that you downloaded from Microsoft Entra ID and select **Save**.

    ![Screenshot of showing Upload certificate type.](media/skillsbase-tutorial/browse-and-save.png)
9. In the **Authentication** panel, for **Single Sign-On** select the Identity Provider you added.

    ![Screenshot for Authentication panel for S S O.](media/skillsbase-tutorial/select-identity-provider.png)
10. Make sure the option to bypass the Skills Base login screen is **deselected** for now. You can enable this option later, once the integration is proved to be working.
11. If you would like to enable **Just In Time** user provisioning, enable the **Automatic user account provisioning** option.
12. Select **Save changes**.

![Screenshot for Just in Time provisioning.](media/skillsbase-tutorial/identity-provider-enabled.png)

Note

The Identity Provider you added in the **Identity Providers** panel should now have a green **Enabled** badge in the **Status** column.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Create Skills Base test user

Skills Base supports just-in-time user provisioning, which is enabled by default. As such, there's no action required for this step. If a user doesn't already exist in Skills Base, a new one is created after authentication.

Note

If you need to create a user manually, follow the instructions [here](https://support.skills-base.com/kb/articles/11000024831-adding-people-and-enabling-them-to-log-in).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Skills Base Sign-on URL where you can initiate the login flow, or
- Use your Skills Base Shortcut link to initiate login flow from there, or
- You can use Microsoft My Apps. When you select the Skills Base tile in the My Apps, this option redirects to your Skills Base Shortcut link. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Renewing Token signing certificate

After some time (by default, 3 years), the Token signing certificate you generated in Microsoft Entra will expire. You may receive advance notice of the pending certificate expiry via email from **Microsoft Security** with subject "**Action required: Renew your application certificate in Microsoft Entra ID**". This email is sent to the email address recorded in **Microsoft Entra &gt; Enterprise apps &gt; Skills Base &gt; Single sign-on &gt; SAM Certificates &gt; Token signing certificate &gt; Notification Email**. The email will include the certificate's expiration date. To avoid service disruption, the certificate must be renewed before this date.

### Steps to renew

1. In **Microsoft Entra** navigate to **Enterprise apps &gt; Skills Base &gt; Single sign-on &gt; SAML Certificates** and select **Edit**.
2. Select **New certificate**, but don't make it active yet.
3. Next to **Federation Metadata XML**, click **Download**.
4. In **Skills Base** navigate to **Administration &gt; Authentication**.
5. Under **Identity Providers**, find your Identity Provider and select the edit button (denoted by a pencil icon) in the **Actions** column.
6. For **SAML IdP Metadata** select **Upload an XML file**.
7. Upload the Federation Metadata XML file that you downloaded in step 3 above. and select **Save**.
8. In **Microsoft Entra** navigate to **Enterprise apps &gt; Skills Base &gt; Single sign-on &gt; SAML Certificates** and select **Edit**.
9. Select the three dots beside the new certificate you created and select **Make certificate active** followed by **Yes**.
10. Ensure that the new certificate expiry date is shown in the **Expiration** field of the **SAML Certificates** section.