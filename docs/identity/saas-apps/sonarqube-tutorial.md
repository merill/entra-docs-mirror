---
layout: Conceptual
title: Configure SonarQube for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sonarqube-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SonarQube.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5afd778b-76b5-b410-266b-046a437ee6b0
document_version_independent_id: 3eb0aa0f-4135-8193-6b0d-915ec703fbcb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sonarqube-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sonarqube-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sonarqube-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5eaa74df-be13-c352-e6aa-336d179fccf9
---

# Configure SonarQube for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SonarQube with Microsoft Entra ID. When you integrate SonarQube with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SonarQube.
- Enable your users to be automatically signed-in to SonarQube with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SonarQube single sign-on (SSO) enabled subscription.
- Steps to get SonarQube "SAML group attribute" setup correctly to use AzureAD groups for permissions (detailed below).

Note

Help on installing SonarQube can be found in the [online documentation](https://docs.sonarsource.com/sonarqube-server/latest/setup-and-upgrade/overview/).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SonarQube supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add SonarQube from the gallery

To configure the integration of SonarQube into Microsoft Entra ID, you need to add SonarQube from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SonarQube** in the search box.
4. Select **SonarQube** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SonarQube

Configure and test Microsoft Entra SSO with SonarQube using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SonarQube.

To configure and test Microsoft Entra SSO with SonarQube, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SonarQube SSO**- to configure the single sign-on settings on application side.
    1. **Create SonarQube test user** - to have a counterpart of B.Simon in SonarQube that's linked to the Microsoft Entra representation of user.
    2. \*\*Configure SAML Group Attribute for SonarQube - to enable B.Simon to use Microsoft Entra single sign-on.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SonarQube** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Reply URL** text box, type a URL using the following pattern: ` https://sonar.<companyspecificurl>.io/oauth2/callback/saml`

    b. In the **Sign-on URL** text box, type one of the following URLs:

    - **For Production Environment**

        `https://servicessonar.corp.microsoft.com/`
    - **For Dev Environment**

        `https://servicescode-dev.westus.cloudapp.azure.com`

    Note

    This value isn't real. Update the value with actual Reply URL which are explained later in the article.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
7. On the **Set up SonarQube** section, copy the appropriate URLs based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SonarQube SSO

1. Open a new web browser window and sign into your SonarQube company site as an administrator.
2. Select **Administration &gt; Configuration &gt; Security** and go to the **SAML Plugin** perform the following steps.
3. Copy the following details from the IdP metadata and paste them into the corresponding text fields in the SonarQube plugin.

    1. IdP Entity ID
    2. Sign-in URL
    3. X.509 Certificate
4. Save all the details.

    ![saml plugin IDP](media/sonarqube-tutorial/metadata.png)
5. On the **SAML** page, perform the following steps:

    ![Sonarqube configuration](media/sonarqube-tutorial/configuration.png)

    a. Toggle the **Enabled** option to **yes**.

    b. In **Application ID** text box, enter the name like **sonarqube**.

    c. In **Provider Name** text box, enter the name like **SAML**.

    d. In **Provider ID** text box, paste the value of **Microsoft Entra Identifier**.

    e. In **SAML login url** text box, paste the value of **Login URL**.

    f. Open the Base 64 encoded certificate in notepad, copy its content and paste it into the **Provider certificate** text box.

    g. In **SAML user login attribute** text box, enter the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.

    h. In **SAML user name attribute** text box, enter the value `http://schemas.microsoft.com/identity/claims/displayname`.

    i. In **SAML user email attribute** text box, enter the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    j. Select **Save**.

### Configure SAML Group Attribute for SonarQube

To set up SAML group attribute and use AzureAD groups for permissions in SonarQube, follow this steps:

1. In the Administration tab of SonarQube, navigate to Configuration &gt; Security &gt; Saml/
2. In the SAML group attribute text box, enter the following value: 'http://schemas.microsoft.com/ws/2008/06/identity/claims/role'
3. Save the changes
4. Go to Administration &gt; Security &gt; Groups in SonarQube
5. Map the AzureAD groups to SonarQube groups:
    - For each AzureAD group, create a corresponding group in SonarQube if it doesn't exist.
    - Ensure the names of the groups match exactly between AzureAD and SonarQube.

### Create SonarQube test user

In this section, you create a user called B.Simon in SonarQube. Work with [SonarQube Client support team](https://sonarsource.com/company/contact/) to add the users in the SonarQube platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to SonarQube Sign-on URL where you can initiate the sign-in flow.
- Go to SonarQube Sign-on URL directly and initiate the sign-in flow from there.
- You can use Microsoft My Apps. When you select the SonarQube tile in the My Apps, this option redirects to SonarQube Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).