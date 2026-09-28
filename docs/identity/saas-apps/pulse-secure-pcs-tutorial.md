---
layout: Conceptual
title: Configure Pulse Secure PCS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/pulse-secure-pcs-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Pulse Secure PCS.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6b912673-6f7b-881b-cd6a-9435019cef79
document_version_independent_id: 6b66e430-db5e-0d3e-a74f-3097af84c4e0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/pulse-secure-pcs-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/pulse-secure-pcs-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/pulse-secure-pcs-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4eb9c292-15f9-5506-1ff5-cf0bc9a8f5d0
---

# Configure Pulse Secure PCS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Pulse Secure PCS with Microsoft Entra ID. When you integrate Pulse Secure PCS with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Pulse Secure PCS.
- Enable your users to be automatically signed-in to Pulse Secure PCS with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Pulse Secure PCS single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Pulse Secure PCS supports **SP** initiated SSO

## Adding Pulse Secure PCS from the gallery

To configure the integration of Pulse Secure PCS into Microsoft Entra ID, you need to add Pulse Secure PCS from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Pulse Secure PCS** in the search box.
4. Select **Pulse Secure PCS** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Pulse Secure PCS

Configure and test Microsoft Entra SSO with Pulse Secure PCS using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Pulse Secure PCS.

To configure and test Microsoft Entra SSO with Pulse Secure PCS, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Pulse Secure PCS SSO**- to configure the single sign-on settings on application side.
    1. **Create Pulse Secure PCS test user** - to have a counterpart of B.Simon in Pulse Secure PCS that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Pulse Secure PCS** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<FQDN of PCS>/dana-na/auth/saml-consumer.cgi`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<FQDN of PCS>/dana-na/auth/saml-endpoint.cgi?p=sp1`

    c. In the **Reply URL** text box, type a URL using the following pattern: `https://[FQDN of PCS]/dana-na/auth/saml-consumer.cgi`

    Note

    These values aren't real. Update these values with the actual Sign on URL,Reply URL and Identifier. Contact [Pulse Secure PCS Client support team](mailto:support@pulsesecure.net) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up Pulse Secure PCS** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Pulse Secure PCS SSO

This section covers the SAML configurations required to configure PCS as SAML SP. The other basic configurations like creating Realms and Roles aren't covered.

**Pulse Connect Secure configurations include:**

- Configuring Microsoft Entra ID as SAML Metadata Provider
- Configuring SAML Auth Server
- Assigning to respective Realms and Roles

#### Configuring Microsoft Entra ID as SAML Metadata Provider

Perform the following steps in the following page:

![Pulse Connect Secure configuration](media/pulse-secure-pcs-tutorial/saml-configuration.png)

1. Log into the Pulse Connect Secure admin console
2. Navigate to **System -&gt; Configuration -&gt; SAML**
3. Select **New Metadata Provider**
4. Provide the valid Name in the **Name** textbox
5. Upload the downloaded metadata XML file from Azure portal into the **Microsoft Entra metadata file**.
6. Select **Accept Unsigned Metadata**
7. Select Roles as **Identity Provider**
8. Select **Save changes**.

#### Steps to create a SAML Auth Server:

1. Navigate to **Authentication -&gt; Auth Servers**
2. Select **New: SAML Server** and select **New Server**

    ![Pulse Connect Secure auth server](media/pulse-secure-pcs-tutorial/new-saml-server.png)
3. Perform the following steps in the settings page:

    ![Pulse Connect Secure auth server settings](media/pulse-secure-pcs-tutorial/server-settings.png)

    a. Provide **Server Name** in the textbox.

    b. Select **SAML Version 2.0** and **Configuration Mode** as **Metadata**.

    c. Copy the **Connect Secure Entity Id** value and paste it into the **Identifier URL** box in the **Basic SAML Configuration** dialog box.

    d. Select Microsoft Entra Entity Id value from the **Identity Provider Entity Id drop down list**.

    e. Select Microsoft Entra Login URL value from the **Identity Provider Single Sign-On Service URL drop down list**.

    f. **Single Logout** is an optional setting. If this option is selected, it prompts for a new authentication after logout. If this option isn't selected and you have not closed the browser, you can reconnect without authentication.

    g. Select the **Requested Authn Context Class** as **Password** and the **Comparison Method** as **exact**.

    h. Set the **Metadata Validity** in terms of number of days.

    i. Select **Save Changes**

### Create Pulse Secure PCS test user

In this section, you create a user called Britta Simon in Pulse Secure PCS. Work with [Pulse Secure PCS support team](mailto:support@pulsesecure.net) to add the users in the Pulse Secure PCS platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

1. Select **Test this application**, this option redirects to Pulse Secure PCS Sign-on URL where you can initiate the login flow.
2. Go to Pulse Secure PCS Sign-on URL directly and initiate the login flow from there.
3. You can use Microsoft Access Panel. When you select the Pulse Secure PCS tile in the Access Panel, this option redirects to Pulse Secure PCS Sign-on URL. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).