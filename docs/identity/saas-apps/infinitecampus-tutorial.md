---
layout: Conceptual
title: Configure Infinite Campus for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/infinitecampus-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Infinite Campus.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: da940d95-9a6c-6fcf-5390-8a88e4d45ee2
document_version_independent_id: 2ca34c67-3ba4-c92c-1c21-c17234078c77
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/infinitecampus-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/infinitecampus-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/infinitecampus-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b9f741da-2af5-6e4b-0a31-ee6886ec1b69
---

# Configure Infinite Campus for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Infinite Campus with Microsoft Entra ID. When you integrate Infinite Campus with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Infinite Campus.
- Enable your users to be automatically signed-in to Infinite Campus with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To configure Microsoft Entra integration with Infinite Campus, you need the following items:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Infinite Campus single sign-on enabled subscription.
- At minimum, you need to be a Microsoft Entra administrator, and have a Campus Product Security Role of "Student Information System (SIS)" to complete the configuration.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Infinite Campus supports **SP** initiated SSO.

## Add Infinite Campus from the gallery

To configure the integration of Infinite Campus into Microsoft Entra ID, you need to add Infinite Campus from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Infinite Campus** in the search box.
4. Select **Infinite Campus** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Infinite Campus

Configure and test Microsoft Entra SSO with Infinite Campus using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Infinite Campus.

To configure and test Microsoft Entra SSO with Infinite Campus, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Infinite Campus SSO** - to configure the single sign-on settings on application side.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Infinite Campus** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the Basic SAML Configuration section, perform the following steps (note that the domain varies with Hosting Model, but the **FULLY-QUALIFIED-DOMAIN** value must match your Infinite Campus installation):

    a. In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<DOMAIN>.infinitecampus.com/campus/SSO/<DISTRICTNAME>/SIS`

    b. In the **Identifier** textbox, type a URL using the following pattern: `https://<DOMAIN>.infinitecampus.com/campus/<DISTRICTNAME>`

    c. In the **Reply URL** textbox, type a URL using the following pattern: `https://<DOMAIN>.infinitecampus.com/campus/SSO/<DISTRICTNAME>`
6. On the **Set up Single Sign-On with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Infinite Campus SSO

For detailed steps on how to configure SSO within Infinite Campus, [please follow the steps in this document](https://kb.infinitecampus.com/help/sso-service-provider-configuration#SSOServiceProviderConfiguration-EnableandConfigureSAMLSSOFunctionality).

Once you have completed configuring SSO within Infinite Campus, if you would like users to be signed out their Azure SSO connection when logging out of Infinite Campus, [follow these steps](https://kb.infinitecampus.com/help/sso-service-provider-configuration#SSOServiceProviderConfiguration-AddtheInfiniteCampusLogoutURLtotheMicrosoftAzureSAMLSSOConfiguration).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Infinite Campus Sign-on URL where you can initiate the login flow.
- Go to Infinite Campus Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Infinite Campus tile in the My Apps, this option redirects to Infinite Campus Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Configure Azure SSO for Non-Production Infinite Campus Environments (Sandbox, Staging)

If your district has other Infinite Campus environments, this entire setup process must be repeated for each environment. For example, if your district has an Infinite Campus sandbox site, add the Infinite Campus app from the gallery again and complete the process while referencing the SSO Service Provider Configuration screen within your Infinite Campus sandbox site. If your district also has, for example, an Infinite Campus staging site, you need to complete this process a third time.

See Infinite Campus [documentation](https://kb.infinitecampus.com/help/sso-service-provider-configuration#sandbox/staging/non-production-environments) for more information about this process.

## Replacing an Expiring SAML Certificate

The SAML certificate of this integration relies on which eventually need to be renewed so users can continue logging into Infinite Campus through single sign-on. For districts with proper Campus Messenger Email Settings established, Infinite Campus sends warning emails as the certificate expiration approaches. (Subject: "Action required: Your certificate is expiring.")

These are the steps to take to replace an expiring SAML certificate:

1. Have your district's Microsoft Entra admin sign in to the Azure portal.
2. On the left navigation pane, select the Microsoft Entra service.
3. Navigate to Enterprise Applications and select your Infinite Campus application set up previously. (If you have multiple Infinite Campus environments like a sandbox or staging site, you have multiple Infinite Campus applications set up here. You need to complete this process in each respective Infinite Campus environment for any with an expiring certificate.)
4. Select Single sign-on.
5. Navigate to the SAML Certificate and copy the App Federation Metadata URL.
6. Within Infinite Campus, navigate to the SSO Service Provider Configuration tool, select the configuration, and paste the App Federation Metadata URL copied in the previous step into the Metadata URL field.
7. In a separate window, go back to the Azure portal. Under SAML Certificates, in the Token Signing Certificate area, select Edit.
8. Select New Certificate. Modify the expiration date if desired.
9. Select Save. (Leave the Signing Option and Signing Algorithm as-is)
10. Return to the Infinite Campus window and select the Sync button next to the Metadata URL. It says "IDP Synchronization successful". Select OK and Save.
11. Return to the Azure portal, still on the SAML Signing Certificate edit screen, select the three dots (...) next to the new certificate. Select Make Certificate Active and select Save.
12. Select the three dots next to the old certificate. Select Delete Certificate.
13. Return to Infinite Campus and hit the Sync button next to the Metadata URL again. It says "IDP Synchronization successful" again. Hit OK and Save again.

This completes the process of replacing an expiring certificate. For more information, see Infinite Campus [documentation](https://kb.infinitecampus.com/help/sso-service-provider-configuration#SSOServiceProviderConfiguration-CertificateExpirationWarnings).