---
layout: Conceptual
title: Configure ADP for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/adpfederatedsso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and ADP.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9a0b8b88-1ed5-3601-b74f-8544843a5f98
document_version_independent_id: aad80f23-2da2-6599-f875-e9a000d2239a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/adpfederatedsso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/adpfederatedsso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/adpfederatedsso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1105995a-b722-6cb8-be5f-234f5a1571ba
---

# Configure ADP for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ADP with Microsoft Entra ID. When you integrate ADP with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ADP.
- Enable your users to be automatically signed-in to ADP with their Microsoft Entra accounts.
- Manage your accounts in one central location.

ADP is available in the following [national cloud deployments](/en-us/graph/deployments).

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

- ADP single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- ADP supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add ADP from the gallery

To configure the integration of ADP into Microsoft Entra ID, you need to add ADP from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ADP** in the search box.
4. Select **ADP** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for ADP

Configure and test Microsoft Entra SSO with ADP using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ADP.

To configure and test Microsoft Entra SSO with ADP, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ADP SSO**- to configure the single sign-on settings on application side.
    1. **Create ADP test user** - to have a counterpart of B.Simon in ADP that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ADP** application integration page, select **Properties tab** and perform the following steps:

    ![Single sign-on properties](media/adpfederatedsso-tutorial/properties.png)

    a. Set the **Enabled for users to sign-in** field value to **Yes**.

    b. Copy the **User access URL** and you have to paste it in **Configure Sign-on URL section**, which is explained later in the article.

    c. Set the **User assignment required** field value to **Yes**.

    d. Set the **Visible to users** field value to **No**.
3. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
4. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ADP** application integration page, find the **Manage** section and select **Single sign-on**.
5. On the **Select a Single sign-on method** page, select **SAML**.
6. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
7. On the **Basic SAML Configuration** section, perform the following steps:

    In the **Identifier (Entity ID)** text box, type the URL: `https://fed.adp.com`
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up ADP** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure ADP SSO

1. In a different web browser window, sign in to your up ADP company site as an administrator
2. Select **Federation Setup** and go to **Identity Provider** then, select the **Microsoft Azure**.

    ![Screenshot for identity provider.](media/adpfederatedsso-tutorial/microsoft-azure.png)
3. In the **Services Selection**, select all applicable service(s) for connection, and then select **Next**.

    ![Screenshot for services selection.](media/adpfederatedsso-tutorial/services.png)
4. In the **Configure** section, select the **Next**.
5. In the **Upload Metadata**, select **Browse** to upload the metadata XML file which you have downloaded and select **UPLOAD**.

    ![Screenshot for uploading metadata.](media/adpfederatedsso-tutorial/metadata.png)

### Configure your ADP service(s) for federated access

Important

Your employees who require federated access to your ADP services must be assigned to the ADP service app and subsequently, users must be reassigned to the specific ADP service. Upon receipt of confirmation from your ADP representative, configure your ADP service(s) and assign/manage users to control user access to the specific ADP service.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **ADP** in the search box.
4. Select **ADP** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select the **ADP** application integration page, select **Properties tab** and perform the following steps:

    ![Single sign-on linked properties tab](media/adpfederatedsso-tutorial/application.png)

    1. Set the **Enabled for users to sign-in** field value to **Yes**.
    2. Set the **User assignment required** field value to **Yes**.
    3. Set the **Visible to users** field value to **Yes**.
4. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
5. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ADP** application integration page, find the **Manage** section and select **Single sign-on**.
6. On the **Select a Single sign-on method** dialog, select **Mode** as **Linked** to link your application to **ADP**.
7. Navigate to the **Configure Sign-on URL** section, perform the following steps:

    ![Configure Single sign-on](media/adpfederatedsso-tutorial/users.png)

    1. Paste the **User access URL**, which you have copied from above **properties tab** (from the main ADP app).
    2. Following are the 5 apps that support different **Relay State URLs**. You have to append the appropriate **Relay State URL** value for particular application manually to the **User access URL**.

        - **ADP Workforce Now**

            `<User access URL>&relaystate=https://fed.adp.com/saml/fedlanding.html?WFN`
        - **ADP Workforce Now Enhanced Time**

            `<User access URL>&relaystate=https://fed.adp.com/saml/fedlanding.html?EETDC2`
        - **ADP Vantage HCM**

            `<User access URL>&relaystate=https://fed.adp.com/saml/fedlanding.html?ADPVANTAGE`
        - **ADP Enterprise HR**

            `<User access URL>&relaystate=https://fed.adp.com/saml/fedlanding.html?PORTAL`
        - **MyADP**

            `<User access URL>&relaystate=https://fed.adp.com/saml/fedlanding.html?REDBOX`
8. **Save** your changes.
9. Upon receipt of confirmation from your ADP representative, begin test with one or two users.

    1. Assign few users to the ADP service App to test federated access.
    2. Test is successful when users access the ADP service app on the gallery and can access their ADP service.
10. On confirmation of a successful test, assign the federated ADP service to individual users or user groups, which is explained later in the article and roll it out to your employees.

### Configure ADP to support multiple instances in the same tenant

1. Go to **Basic SAML Configuration** section and enter any instance specific URL in the **Identifier (Entity ID)** textbox.

    Note

    Please note that this can be any random value which you feel relevant for your instance.
2. To support multiple instances in the same tenant, please follow the below steps:

    ![Screenshot shows how to configure audience claim value.](media/adpfederatedsso-tutorial/audience.png)

    1. Navigate to **Attributes & Claims** section &gt; **Advanced settings** &gt; **Advanced SAML claims options** and select **Edit**.
    2. Enable **Append application ID to issuer** checkbox.
    3. Enable **Override audience claim** checkbox.
    4. In the **Audience claim value** textbox, enter `https://fed.adp.com` and select **Save**.
3. Navigate to **Properties** tab under Manage section and copy **Application ID**.

    ![Screenshot shows how to copy application value from properties tab.](media/adpfederatedsso-tutorial/app.png)
4. Download and open the **Federation Metadata XML** file and edit the **entityID** value by adding **Application ID** manually at the end.

    ![Screenshot shows how to add the application value in the federation file.](media/adpfederatedsso-tutorial/federation.png)
5. **Save** the xml file and use in the ADP side.

### Create ADP test user

The objective of this section is to create a user called B.Simon in ADP. Work with [ADP support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP account.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the ADP for which you set up the SSO.
- You can use Microsoft My Apps. When you select the ADP tile in the My Apps, you should be automatically signed in to the ADP for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).