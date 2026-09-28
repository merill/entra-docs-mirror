---
layout: Conceptual
title: Configure Citrix Cloud SAML SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/citrix-cloud-saml-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Citrix Cloud SAML SSO.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: cc2e801a-a207-b1b7-ddc9-e6edf873494e
document_version_independent_id: 09c0ad99-ce5d-928f-8642-edee9eca0f9b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/citrix-cloud-saml-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/citrix-cloud-saml-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/citrix-cloud-saml-sso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c9af6af4-7d57-6a25-d63e-1bbbaa5a603c
---

# Configure Citrix Cloud SAML SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Citrix Cloud SAML SSO with Microsoft Entra ID. When you integrate Citrix Cloud SAML SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Citrix Cloud SAML SSO.
- Enable your users to be automatically signed-in to Citrix Cloud SAML SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Citrix Cloud subscription. If you don’t have a subscription, sign up for one.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Citrix Cloud SAML SSO supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Citrix Cloud SAML SSO from the gallery

To configure the integration of Citrix Cloud SAML SSO into Microsoft Entra ID, you need to add Citrix Cloud SAML SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Citrix Cloud SAML SSO** in the search box.
4. Select **Citrix Cloud SAML SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Citrix Cloud SAML SSO

Configure and test Microsoft Entra SSO with Citrix Cloud SAML SSO using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Citrix Cloud SAML SSO. This user must also exist in your Active Directory that's synced with Microsoft Entra Connect to your Microsoft Entra subscription.

To configure and test Microsoft Entra SSO with Citrix Cloud SAML SSO, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Citrix Cloud SAML SSO** - to configure the single sign-on settings on application side.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Citrix Cloud SAML SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following step:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.cloud.com`

    Note

    The value isn't real. Update the value with your Citrix Workspace URL. Access your Citrix Cloud account to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Citrix Cloud SAML SSO application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, Citrix Cloud SAML SSO application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre-populated but you can review them as per your requirements. The values passed in the SAML response should map to the Active Directory attributes of the user.

    | Name | Source Attribute |
    | --- | --- |
    | cip\_sid | user.onpremisesecurityidentifier |
    | cip\_upn | user.userprincipalname |
    | cip\_oid | ObjectGUID (Extension Attribute) |
    | cip\_email | user.mail |
    | displayName | user.displayname |

    Note

    ObjectGUID must be configured manually according to your requirements.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (PEM)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificate-base64-download.png)
9. On the **Set up Citrix Cloud SAML SSO** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Citrix Cloud SAML SSO

1. In a different web browser window, sign in to your up Citrix Cloud SAML SSO company site as an administrator
2. Navigate to the Citrix Cloud menu and select **Identity and Access Management**.

    ![Screenshot shows Account page.](media/citrix-cloud-saml-sso-tutorial/menu.png)
3. Under **Authentication**, locate **SAML 2.0** and select **Connect** from the ellipsis menu.
4. In the **Configure SAML** page, perform the following steps.

    ![Screenshot shows Configuration.](media/citrix-cloud-saml-sso-tutorial/connect.png)

    a. In the **Entity ID** textbox, paste the **Microsoft Entra Identifier** value which you copied previously.

    b. In the **Sign Authentication Request**, select **Yes**, if you want to use `SAML Request signing`, else select **No**.

    c. In the **SSO Service URL** textbox, paste the **Login URL** value which you copied previously.

    d. Select **Binding Mechanism** from the drop-down, you can select either **HTTP-POST** or **HTTP-Redirect** binding.

    e. Under **SAML Response**, select **Sign Either Response or Assertion** from the dropdown.

    f. Upload the **Certificate (PEM)** into the **X.509 Certificate** section.

    g. In the **Authentication Context**, select **Unspecified** and **Exact** from the dropdown.

    h. Select **Test and Finish**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Access your Citrix Workspace URL directly and initiate the login flow from there.
- Log in with your AD-Synced Active Directory user into your Citrix Workspace to complete the test.