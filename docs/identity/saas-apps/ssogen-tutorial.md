---
layout: Conceptual
title: Configure SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/ssogen-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 298f9eeb-c50e-98f0-fee9-a91319c676b1
document_version_independent_id: 66eeed93-3744-a47f-81ee-54af0bb9ec9f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/ssogen-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/ssogen-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/ssogen-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5eadaf61-2b8e-deab-6f66-b6022b7ee1a1
---

# Configure SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE with Microsoft Entra ID. When you integrate SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE.
- Enable your users to be automatically signed-in to SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE supports **SP and IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE from the gallery

To configure the integration of SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE into Microsoft Entra ID, you need to add SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE** in the search box.
4. Select **SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE

Configure and test Microsoft Entra SSO with SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE.

To configure and test Microsoft Entra SSO with SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE SSO**- to configure the single sign-on settings on application side.
    1. **Create SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE test user** - to have a counterpart of B.Simon in SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    In the **Reply URL** text box, type a URL using the following pattern: `https://<customer_name>.ssogen.com/ssogen/login?client_name=<customer_name>`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<customer_name>.ssogen.com/ssogen/login?client_name=<customer_name>`

    Note

    These values aren't real. Update these values with the actual Reply URL and Sign-On URL. Contact [SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE Client support team](mailto:support@ssogen.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. Your SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes, whereas **nameidentifier** is mapped with **user.userprincipalname**. SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE application expects **nameidentifier** to be mapped with **user.onpremisessamaccountname**, so you need to edit the attribute mapping by selecting **Edit** icon and change the attribute mapping.

    ![image](common/edit-attribute.png)
8. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE SSO

To configure single sign-on on **SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE** side, Please find application-specific SSO registration documentation below:

- Oracle EBS - Microsoft Entra SSO Integration: https://www.ssogen.com/oracle-ebs-sso-ldap/
- PeopleSoft - Microsoft Entra SSO Integration: https://www.ssogen.com/peoplesoft-sso/
- JD Edwards - Microsoft Entra SSO Integration: https://www.ssogen.com/oracle-jde-sso/
- Apache - Microsoft Entra SSO Integration: https://www.ssogen.com/apache-sso-authentication/

### Create SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE test user

Microsoft Entra ID sends Unique User Identifier (Name ID) to the user application, after the authentication is successful. Please make sure that Unique User Identifier (Name ID) matches user record in your application, FND\_USER.USER\_NAME in Oracle EBS for example.

Please contact info@ssogen.com and support@ssogen.com for any support.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE Sign on URL where you can initiate the login flow.
- Go to SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the SSOGEN - Microsoft Entra SSO Gateway for Oracle E-Business Suite - EBS, PeopleSoft, and JDE for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).