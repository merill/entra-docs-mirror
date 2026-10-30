---
layout: Conceptual
title: Configure LoginRadius for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/lr-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and LoginRadius.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: bfc37d09-4df3-2ade-5f9e-4f388190c0dc
document_version_independent_id: ab9e030c-5c04-4eb0-2d64-fd10cec19bfd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/lr-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/lr-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/lr-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8ba48f21-317c-5b03-6c14-c3b0485f15b0
---

# Configure LoginRadius for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate LoginRadius with Microsoft Entra ID. When you integrate LoginRadius with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to LoginRadius.
- Enable your users to be automatically signed-in to LoginRadius with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A LoginRadius single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- LoginRadius supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add LoginRadius from the gallery

To configure the integration of LoginRadius into Microsoft Entra ID, you need to add LoginRadius from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **LoginRadius** in the search box.
4. Select **LoginRadius** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for LoginRadius

Configure and test Microsoft Entra SSO with LoginRadius using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in LoginRadius.

To configure and test Microsoft Entra SSO with LoginRadius, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure LoginRadius SSO**- to configure the single sign-on settings on application side.
    1. **Create LoginRadius test user** - to have a counterpart of B.Simon in LoginRadius that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **LoginRadius** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    1. In the **Identifier (Entity ID)** text box, enter the URL `https://lr.hub.loginradius.com/`
    2. In the **Reply URL (Assertion Consumer Service URL)** textbox, enter the LoginRadius ACS URL `https://lr.hub.loginradius.com/saml/serviceprovider/AdfsACS.aspx`
    3. In the **Sign on URL** text box, enter the URL `https://secure.loginradius.com/login`
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. In the **Set up LoginRadius** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure LoginRadius SSO

In this section, you enable Microsoft Entra single sign-on in the LoginRadius Admin Console.

1. Log in to your LoginRadius [Admin Console](https://adminconsole.loginradius.com/login) account.
2. Go to your **Team Management** section in the [LoginRadius Admin Console](https://www.loginradius.com/legacy/docs/api/v2/admin-console/overview/).
3. Select the **Single Sign-On** tab, and then select **Microsoft Entra ID**:

    ![Screenshot that shows the single-sign-on menu in the LoginRadius Team Management console](media/loginradius-tutorial/azure-ad.png)
4. In the Microsoft Entra setup page, complete the following steps:

    ![Screenshot that shows Microsoft Entra configuration in the LoginRadius Team Management console](media/loginradius-tutorial/single-sign-on.png)

    1. In **ID Provider Location**, enter the SIGN-ON ENDPOINT, which you get from your Microsoft Entra account.
    2. In **ID Provider Logout URL**, enter the SIGN-OUT ENDPOINT, which you get from your Microsoft Entra account.
    3. In **ID Provider Certificate**, enter the Microsoft Entra certificate, which you get from your Microsoft Entra account. Enter the certificate value with the header and footer. Example: `-----BEGIN CERTIFICATE-----<certificate value>-----END CERTIFICATE-----`
    4. In **Service Provider Certificate** and **Server Provider Certificate Key**, enter your certificate and key.

        You can create a self-signed certificate by running the following commands on the command line (Linux/Mac):

        - Command to get the certificate key for SP: `openssl genrsa -out lr.hub.loginradius.com.key 2048`
        - Command to get the certificate for SP: `openssl req -new -x509 -key lr.hub.loginradius.com.key -out lr.hub.loginradius.com.cert -days 3650 -subj /CN=lr.hub.loginradius.com`

        Note

        Be sure to enter the certificate and certificate key values with the header and footer:

        - Certificate value example format: `-----BEGIN CERTIFICATE-----<certificate value>-----END CERTIFICATE-----`
        - Certificate key value example format: `-----BEGIN RSA PRIVATE KEY-----<certificate key value>-----END RSA PRIVATE KEY-----`
5. In the **Data Mapping** section, select the fields (SP fields) and enter the corresponding Microsoft Entra ID fields(IdP fields).

    Following are some listed field names for Microsoft Entra ID.

    | Fields | Profile Key |
    | --- | --- |
    | Email | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` |
    | FirstName | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` |
    | LastName | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` |

    Note

    The **Email** field mapping is required. **FirstName** and **LastName** field mappings are optional.

### Create LoginRadius test user

1. Log in to your LoginRadius [Admin Console](https://adminconsole.loginradius.com/login) account.
2. Go to your team management section in the LoginRadius Admin Console.

    ![Screenshot that shows the LoginRadius Admin Console](media/loginradius-tutorial/team-management.png)
3. Select **Add Team Member** in the side menu to open the form.
4. In the **Add Team Member** form, you create a user called Britta Simon in your LoginRadius site by providing the user's details and assigning the permissions you want the user to have. To know more about the permissions based on roles, see the [Role Access Permissions](https://www.loginradius.com/docs/) section of the LoginRadius [Manage Team Members](https://www.loginradius.com/docs/) document. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration using MyApps.

1. In a browser, go to https://accounts.loginradius.com/auth.aspx and select **Fed SSO log in**.
2. Enter your LoginRadius app name, and then select **Login**.
3. It should open a pop-up for asking you to sign in to your Microsoft Entra account.
4. After the authentication, your pop-up will close and you be logged in to the LoginRadius Admin Console.