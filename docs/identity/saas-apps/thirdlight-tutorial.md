---
layout: Conceptual
title: Configure ThirdLight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/thirdlight-tutorial
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
description: In this article,  you learn how to configure single sign-on between Microsoft Entra ID and ThirdLight.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 027f5db6-17a3-c274-42f7-b770e51e2145
document_version_independent_id: 17fc848c-f880-5441-00ab-7d3f36be4221
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/thirdlight-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/thirdlight-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/thirdlight-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1816a784-8f61-e626-69ff-f891d9316c0b
---

# Configure ThirdLight for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ThirdLight with Microsoft Entra ID. When you integrate ThirdLight with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ThirdLight.
- Enable your users to be automatically signed-in to ThirdLight with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To configure Microsoft Entra integration with ThirdLight, you need to have:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A ThirdLight subscription that has single sign-on enabled.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- ThirdLight supports SP-initiated SSO.

## Add ThirdLight from the gallery

To configure the integration of ThirdLight into Microsoft Entra ID, you need to add ThirdLight from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ThirdLight** in the search box.
4. Select **ThirdLight** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for ThirdLight

Configure and test Microsoft Entra SSO with ThirdLight using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ThirdLight.

To configure and test Microsoft Entra SSO with ThirdLight, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ThirdLight SSO**- to configure the single sign-on settings on application side.
    1. **Create ThirdLight test user** - to have a counterpart of B.Simon in ThirdLight that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ThirdLight** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. In the **Basic SAML Configuration** dialog box, perform the following steps:

    1. In the **Identifier (Entity ID)** box, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`
    2. In the **Sign on URL** box, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`

        Note

        These values are placeholders. You need to use the actual Identifier and Sign on URL. Contact the [ThirdLight support team](https://www.thirdlight.com/support) to get the values. You can also refer to the patterns shown in the **Basic SAML Configuration** dialog box.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Federation Metadata XML**, per your requirements, and save the file on your computer:

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
7. In the **Set up ThirdLight** section, copy the appropriate URLs, based on your requirements:

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ThirdLight SSO

1. In a new web browser window, sign in to your ThirdLight company site as an admin.
2. Go to **Configuration** &gt; **System Administration** &gt; **SAML2**:

    ![Screenshot shows the System Administration.](media/thirdlight-tutorial/admin.png)
3. In the SAML2 configuration section, take the following steps.

    ![Screenshot shows the S A M L configuration section.](media/thirdlight-tutorial/source.png)

    1. Select **Enable SAML2 Single Sign-On**.
    2. Under **Source for IdP Metadata**, select **Load IdP Metadata from XML**.
    3. Open the metadata file that you downloaded in the previous section. Copy the file's content and paste it into the **IdP Metadata XML** box.
    4. Select **Save SAML2 settings**.

### Create ThirdLight test user

To enable Microsoft Entra users to sign in to ThirdLight, you need to add them to ThirdLight. You need to add them manually.

To create a user account, take these steps:

1. Sign in to your ThirdLight company site as an admin.
2. Go to the **Users** tab.
3. Select **Users and Groups**.
4. Select **Add new User**.
5. Enter the user name, a name or description, and the email address of a valid Microsoft Entra account that you want to provision. Choose a Preset or Group of New Members.
6. Select **Create**.

Note

You can use any user account creation tool or API provided by ThirdLight to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to ThirdLight Sign-on URL where you can initiate the login flow.
- Go to ThirdLight Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the ThirdLight tile in the My Apps, this option redirects to ThirdLight Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).