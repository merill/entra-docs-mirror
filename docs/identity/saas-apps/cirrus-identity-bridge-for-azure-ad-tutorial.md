---
layout: Conceptual
title: Configure Cirrus Identity Bridge for Microsoft Entra ID for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cirrus-identity-bridge-for-azure-ad-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Cirrus Identity Bridge for Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: c30c41e8-379b-d2a2-d2e7-15472562b9a0
document_version_independent_id: e9ddb507-8775-dfcc-1569-a2eea5e2a606
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cirrus-identity-bridge-for-azure-ad-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cirrus-identity-bridge-for-azure-ad-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cirrus-identity-bridge-for-azure-ad-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ad4ccd21-8883-56c8-75a1-e4881fc19849
---

# Configure Cirrus Identity Bridge for Microsoft Entra ID for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Cirrus Identity Bridge for Microsoft Entra ID with Microsoft Entra ID using the Microsoft Graph API based integration pattern. When you integrate Cirrus Identity Bridge for Microsoft Entra ID with Microsoft Entra ID in this way, you can:

- Control who has access to InCommon or other multilateral federation service providers from Microsoft Entra ID.
- Enable your users to SSO to InCommon or other multilateral federation service providers with their Microsoft Entra accounts.
- Enable your users to access Central Authentication Service (CAS) applications with their Microsoft Entra accounts.
- Manage your application access in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Cirrus Identity Bridge for Microsoft Entra single sign-on (SSO) enabled subscription. If you aren't already a subscriber, please visit the [Cirrus Identity Microsoft Entra ID Bridge Registration Page](https://info.cirrusidentity.com/cirrus-identity-azure-ad-app-gallery-registration).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Cirrus Identity Bridge for Microsoft Entra ID supports **SP** and **IDP** initiated SSO.

## Before adding the Cirrus Identity Bridge for Microsoft Entra ID from the gallery

When subscribing to the Cirrus Identity Bridge for Microsoft Entra ID, you are asked for your Microsoft Entra TenantID. To view this:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Properties**.
3. Scroll down to the **Tenant ID** section and you can find your tenant ID in the box.
4. Copy the value and send it to the Cirrus Identity contract representative you're working with.

To use the Microsoft Graph API integration, you must grant the Cirrus Identity Bridge for Microsoft Entra ID access to use the API in your tenant. To do this:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Edit the URL `https://login.microsoftonline.com/$TENANT_ID/adminconsent?client_id=ea71bc49-6159-422d-84d5-6c29d7287974&state=12345&redirect_uri=https://admin.cirrusidentity.com/azure-registration` replacing **$TENANT\_ID** with the value for your Microsoft Entra tenant.
3. Paste the URL into the browser where you're signed in.
4. You be asked to consent to grant access.
5. When successful, there should be a new application called Cirrus Bridge API.
6. Advise the Cirrus Identity contract representative you're working with that you have successfully granted API access to the Cirrus Identity Bridge for Microsoft Entra ID.

Once Cirrus Identity has the Tenant ID, and access has been granted, we will provision Cirrus Identity Bridge for Microsoft Entra infrastructure and provide you with the following information unique to your subscription:

- Identifier URI/ Entity ID
- Redirect URI / Reply URL
- Single-logout URL
- SP Encryption Cert (if using encrypted assertions or logout)
- A URL for testing
- Additional instructions depending on the options included with your subscription

Note

If you're unable to grant API access to the Cirrus Identity Bridge for Microsoft Entra ID, the Bridge can be integrated using a traditional SAML2 integration. Advise the Cirrus Identity contract representative you're working with that you aren't able to use MS Graph API integration.

## Add Cirrus Identity Bridge for Microsoft Entra ID from the gallery

To configure the integration of Cirrus Identity Bridge for Microsoft Entra ID into Microsoft Entra ID, you need to add Cirrus Identity Bridge for Microsoft Entra ID from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Cirrus Identity Bridge for Microsoft Entra ID** in the search box.
4. Select **Cirrus Identity Bridge for Microsoft Entra ID** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Cirrus Identity Bridge for Microsoft Entra ID

Configure and test Microsoft Entra SSO with Cirrus Identity Bridge for Microsoft Entra ID using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Cirrus Identity Bridge for Microsoft Entra ID.

To configure and test Microsoft Entra SSO with Cirrus Identity Bridge for Microsoft Entra ID, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Cirrus Identity Bridge for Microsoft Entra SSO**- to configure the single sign-on settings on application side.
    1. **Setup Cirrus Identity Bridge for Microsoft Entra testing** - to have a counterpart of B.Simon in Cirrus Identity Bridge for Microsoft Entra ID that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Cirrus Identity Bridge for Microsoft Entra ID** application integration page, find the **Manage** section and select **Properties**.
3. On the **Properties** page, toggle **Assignment Required** based on your access requirements. If set to **Yes**, you need to assign the **Cirrus Identity Bridge for Microsoft Entra ID** application to an access control group on the **Users and Groups** page.
4. While still on the **Properties** page, toggle **Visible to users** to **No**. The initial integration will always represent the default integration used for multiple service providers. In this case, there isn't any one service provider to direct end users to. To make specific applications visible to end users, you have to use linking single sign-on to give end user access in My Apps to specific service providers. [See here](../enterprise-apps/configure-linked-sign-on) for more details.
5. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
6. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Cirrus Identity Bridge for Microsoft Entra ID** &gt; **Single sign-on**.
7. On the **Select a single sign-on method** page, select **SAML**.
8. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
9. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<DOMAIN>/bridge`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<NAME>.proxy.cirrusidentity.com/module.php/saml/sp/saml2-acs.php/<NAME>_proxy`
10. Select Set additional URLs and perform the following step if you wish to configure the application in SP initiated mode:

    In the **Sign on URL** text box, type a value using the following pattern: `<CUSTOMER_LOGIN_URL>`

    Note

    These values aren't real. Update these values with the actual Identifier,Reply URL and Sign on URL. If you have not yet subscribed to the Cirrus Bridge, please visit the [registration page](https://info.cirrusidentity.com/cirrus-identity-azure-ad-app-gallery-registration). If you're an existing Cirrus Bridge customer, contact [Cirrus Identity Bridge for Microsoft Entra Client support team](https://www.cirrusidentity.com/resources/service-desk) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
11. Cirrus Identity Bridge for Microsoft Entra application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
12. Cirrus Identity Bridge for Microsoft Entra pre-populates **Attributes & Claims** which are typical for use with the InCommon trust federation. You can review and modify them to meet your requirements. Consult the [eduPerson schema specification](https://wiki.refeds.org/display/STAN/eduPerson) for more details.

    | Name | Source Attribute |
    | --- | --- |
    | urn:oid:2.5.4.42 | user.givenname |
    | urn:oid:2.5.4.4 | user.surname |
    | urn:oid:0.9.2342.19200300.100.1.3 | user.mail |
    | urn:oid:1.3.6.1.4.1.5923.1.1.1.6 | user.userprincipalname |
    | cirrus.nameIdFormat | "urn:oasis:names:tc:SAML:2.0:nameid-format:transient" |

    Note

    These defaults assume the Microsoft Entra UPN is suitable to use as an eduPersonPrincipalName.
13. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Cirrus Identity Bridge for Microsoft Entra SSO

More documentation on configuring the Cirrus Bridge is available [from Cirrus Identity](https://blog.cirrusidentity.com/documentation/azure-bridge-setup). To also configure the Cirrus Bridge to support access for CAS services, CAS support is also available [for the Cirrus Bridge](https://blog.cirrusidentity.com/documentation/cas-bridge-setup).

### Setup Cirrus Identity Bridge for Microsoft Entra testing

In this section, you verify a user called Britta Simon can be used for testing. The [Cirrus Identity Bridge for Microsoft Entra support team](https://www.cirrusidentity.com/resources/service-desk) will provide a testing URL to verify Britta Simon is ready to use with the Cirrus Identity Bridge for Microsoft Entra platform. The test user Britta Simon will need to also be added to any applications using the Cirrus Identity Bridge for Microsoft Entra ID as a method to authenticate (for example, applications in multilateral federation metadata).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Cirrus Identity Bridge for Microsoft Entra ID Sign on URL where you can initiate the login flow.
- Go to Cirrus Identity Bridge for Microsoft Entra Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Cirrus Identity Bridge for Microsoft Entra ID for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Cirrus Identity Bridge for Microsoft Entra ID tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Cirrus Identity Bridge for Microsoft Entra ID for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).