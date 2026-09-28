---
layout: Conceptual
title: Configure Cisco Secure Firewall - Secure Client for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cisco-secure-firewall-secure-client
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: celested
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra ID and Cisco Secure Firewall - Secure Client.
ms.topic: how-to
ms.date: 2024-05-20T00:00:00.0000000Z
locale: en-us
document_id: adaeb481-1bdc-7862-97ea-f6694e8113a9
document_version_independent_id: adaeb481-1bdc-7862-97ea-f6694e8113a9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cisco-secure-firewall-secure-client.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cisco-secure-firewall-secure-client
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cisco-secure-firewall-secure-client.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 32a61f46-f052-6c8c-847a-d37abb1809c6
---

# Configure Cisco Secure Firewall - Secure Client for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Cisco Secure Firewall - Secure Client with Microsoft Entra ID. When you integrate Cisco Secure Firewall - Secure Client with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Cisco Secure Firewall - Secure Client.
- Enable your users to be automatically signed-in to Cisco Secure Firewall - Secure Client with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Cisco Secure Firewall - Secure Client single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Cisco Secure Firewall - Secure Client supports only **IDP** initiated SSO.

## Adding Cisco Secure Firewall - Secure Client from the gallery

To configure the integration of Cisco Secure Firewall - Secure Client into Microsoft Entra ID, you need to add Cisco Secure Firewall - Secure Client from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Cisco Secure Firewall - Secure Client** in the search box.
4. Select **Cisco Secure Firewall - Secure Client** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Cisco Secure Firewall - Secure Client

Configure and test Microsoft Entra SSO with Cisco Secure Firewall - Secure Client using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Cisco Secure Firewall - Secure Client.

To configure and test Microsoft Entra SSO with Cisco Secure Firewall - Secure Client, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Cisco Secure Firewall - Secure Client SSO**- to configure the single sign-on settings on application side.
    1. **Create Cisco Secure Firewall - Secure Client test user** - to have a counterpart of B.Simon in Cisco Secure Firewall - Secure Client that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Cisco Secure Firewall - Secure Client** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Set up single sign-on with SAML** page, enter the values for the following fields:

    1. In the **Identifier** text box, type a URL using the following pattern:`https://<SUBDOMAIN>.YourCiscoServer.com/saml/sp/metadata/<Tunnel_Group_Name>`
    2. In the **Reply URL** text box, type a URL using the following pattern:`https://<YOUR_CISCO_ANYCONNECT_FQDN>/+CSCOE+/saml/sp/acs?tgname=<Tunnel_Group_Name>`

    Note

    `<Tunnel_Group_Name>` is a case-sensitive and the value must not contain dots "." and slashes "/".

    Note

    For clarification about these values, contact Cisco TAC support. Update these values with the actual Identifier and Reply URL provided by Cisco TAC. Contact the [Cisco Secure Firewall - Secure Client support team](https://www.cisco.com/c/en/us/support/index.html) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate file and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
7. On the **Set up Cisco Secure Firewall - Secure Client** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

Note

If you would like to on board multiple TGTs of the server then you need to add multiple instances of the Cisco Secure Firewall - Secure Client application from the gallery. You can also choose to upload your own certificate in Microsoft Entra ID for all these application instances. That way you can have same certificate for the applications but you can configure different Identifier and Reply URL for every application.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Cisco Secure Firewall - Secure Client SSO

1. You're going to do this on the CLI first, you might come back through and do an ASDM walk-through at another time.
2. Connect to your VPN Appliance, you're going to be using an ASA running 9.8 code train, and your VPN clients are 4.6+.
3. First you create a Trustpoint and import our SAML cert.

    ```
     config t
    
     crypto ca trustpoint AzureAD-AC-SAML
       revocation-check none
       no id-usage
       enrollment terminal
       no ca-check
     crypto ca authenticate AzureAD-AC-SAML
     -----BEGIN CERTIFICATE-----
     …
     PEM Certificate Text from download goes here
     …
     -----END CERTIFICATE-----
     quit
    ```
4. The following commands will provision your SAML IdP.

    ```
     webvpn
     saml idp https://sts.windows.net/xxxxxxxxxxxxx/ (This is your Azure AD Identifier from the Set up Cisco Secure Firewall - Secure Client section in the Azure portal)
     url sign-in https://login.microsoftonline.com/xxxxxxxxxxxxxxxxxxxxxx/saml2 (This is your Login URL from the Set up Cisco Secure Firewall - Secure Client section in the Azure portal)
     url sign-out https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0 (This is Logout URL from the Set up Cisco Secure Firewall - Secure Client section in the Azure portal)
     trustpoint idp AzureAD-AC-SAML
     trustpoint sp (Trustpoint for SAML Requests - you can use your existing external cert here)
     no force re-authentication
     no signature
     base-url https://my.asa.com
    ```
5. Now you can apply SAML Authentication to a VPN Tunnel Configuration.

    ```
    tunnel-group AC-SAML webvpn-attributes
       saml identity-provider https://sts.windows.net/xxxxxxxxxxxxx/
       authentication saml
    end
    
     write mem
    ```

    Note

    There's a work around with the SAML IdP configuration. If you make changes to the IdP configuration you need to remove the saml identity-provider configuration from your Tunnel Group and re-apply it for the changes to become effective.

### Create Cisco Secure Firewall - Secure Client test user

In this section, you create a user called Britta Simon in Cisco Secure Firewall - Secure Client. Work with [Cisco Secure Firewall - Secure Client support team](https://www.cisco.com/c/en/us/support/index.html) to add the users in the Cisco Secure Firewall - Secure Client platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Cisco Secure Firewall - Secure Client for which you set up the SSO
- You can use Microsoft Access Panel. When you select the Cisco Secure Firewall - Secure Client tile in the Access Panel, you should be automatically signed in to the Cisco Secure Firewall - Secure Client for which you set up the SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).