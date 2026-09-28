---
layout: Conceptual
title: Configure on-premises Confluence for Single sign-on in application proxy mode - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/confluence-app-proxy-tutorial
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
description: Learn application proxy configuration for Microsoft Entra SAML SSO for Confluence.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 55f51416-3ae1-a90c-d199-2874bb460b45
document_version_independent_id: 72c1d577-f0f4-607a-0e30-4b6390a9328d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/confluence-app-proxy-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/confluence-app-proxy-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/confluence-app-proxy-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 32d78f08-55b8-d30d-4c23-1b1b5eeac1d7
---

# Configure on-premises Confluence for Single sign-on in application proxy mode - Microsoft Entra ID | Microsoft Learn

This article helps to configure Microsoft Entra SAML SSO for your on-premises Confluence application using Application Proxy.

## Prerequisites

To configure Microsoft Entra integration with Confluence SAML SSO by Microsoft, you need the following items:

- A Microsoft Entra subscription.
- Confluence server application installed on a Windows 64-bit server (on-premises or on the cloud IaaS infrastructure).
- Confluence server is HTTPS enabled.
- Note the supported versions for Confluence Plugin are mentioned in below section.
- Confluence server is reachable on internet particularly to Microsoft Entra Login page for authentication and should able to receive the token from Microsoft Entra ID.
- Admin credentials are set up in Confluence.
- WebSudo is disabled in Confluence.
- Test user created in the Confluence server application.

To get started, you need the following items:

- Don't use your production environment, unless it's necessary.
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Confluence SAML SSO by Microsoft single sign-on (SSO) enabled subscription.

## Supported versions of Confluence

As of now, following versions of Confluence are supported:

- Confluence: 5.0 to 5.10
- Confluence: 6.0.1 to 6.15.9
- Confluence: 7.0.1 to 7.17.0

Note

Please note that our Confluence Plugin also works on Ubuntu Version 16.04

## Scenario description

In this article, you configure and test Microsoft Entra SSO for on-premises confluence setup using application proxy mode.

1. Download and Install Microsoft Entra private network connector.
2. Add Application Proxy in Microsoft Entra ID.
3. Add a Confluence SAML SSO app in Microsoft Entra ID.
4. Configure SSO for SAML SSO Confluence Application in Microsoft Entra ID.
5. Create a Microsoft Entra test user.
6. Assigning the test user for the Confluence Microsoft Entra App.
7. Configure SSO for Confluence SAML SSO by Microsoft Confluence plugin in your Confluence Server.
8. Assigning the test user for the Microsoft Confluence plugin in your Confluence Server.
9. Test the SSO.

## Download and Install the private network connector Service

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application proxy**.
3. Select **Download connector service**.

    ![Screenshot for Download connector service.](media/confluence-app-proxy-tutorial/download-connector-service.png)
4. Accept terms & conditions to download connector. Once downloaded, install it to the system, which hosts the confluence application.

## Add an On-premises Application in Microsoft Entra ID

To add an Application proxy, we need to create an enterprise application.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. Choose **Add an on-premises application**.
4. Type the name of the application and select the create button at the bottom left column.
5. In the **Add your own on-premises application**, enter the following settings.

    1. **Internal URL** is your Confluence application URL.
    2. **External URL** is auto-generated based on the Name you choose.
    3. **Pre Authentication** can be left to Microsoft Entra ID as default.
    4. Choose **Connector Group** which lists your connector agent under it as active.
    5. Leave the **Additional Settings** as default.
6. Select the **Save** from the top options to configure an application proxy.

## Add a Confluence SAML SSO app in Microsoft Entra ID

Now that you've prepared your environment and installed a connector, you're ready to add confluence applications to Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. Select **Confluence SAML SSO by Microsoft** widget from the Microsoft Entra Gallery.

## Configure SSO for Confluence SAML SSO Application in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Open the **Confluence SAML SSO by Microsoft** &gt; **Single sign-on**.
4. On the **Select a single sign-on method** page, select **SAML**.
5. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot for Edit Basic SAML Configuration.](common/edit-urls.png)
6. On the Basic SAML Configuration section, enter the **External Url** value for the following fields: identifier, Reply URL, SignOn URL.

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assigning the test user for the Confluence Microsoft Entra App

In this section, you enable B.Simon to use single sign-on by granting access to Confluence Microsoft Entra App.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Confluence SAML SSO by Microsoft**.
3. In the app's overview page, find the **Manage** section and select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment** dialog.
5. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
6. In the **Add Assignment** dialog, select the **Assign** button.
7. Verify the application proxy setup by checking if the configured test user is able to SSO using the external URL mentioned in the on-premises application.

Note

Complete the setup of the JIRA SAML SSO by Microsoft application by following [this](jiramicrosoft-tutorial) article.