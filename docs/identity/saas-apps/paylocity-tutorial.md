---
layout: Conceptual
title: Configure Paylocity for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/paylocity-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Paylocity.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: cfd59449-07aa-fc74-1e9b-e274bd064bb8
document_version_independent_id: d31219d9-9877-dc7f-e565-1ab1cfc2b3f0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/paylocity-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/paylocity-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/paylocity-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 58ef1fd1-c935-ae00-4b36-0728a466c0cc
---

# Configure Paylocity for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Paylocity with Microsoft Entra ID. When you integrate Paylocity with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Paylocity.
- Enable your users to be automatically signed-in to Paylocity with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Paylocity single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Paylocity supports **SP and IDP** initiated SSO

## Add Paylocity from the gallery

To configure the integration of Paylocity into Microsoft Entra ID, you need to add Paylocity from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Paylocity** in the search box.
4. Select **Paylocity** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Paylocity

Configure and test Microsoft Entra SSO with Paylocity using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Paylocity.

To configure and test Microsoft Entra SSO with Paylocity, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Paylocity SSO**- to configure the single sign-on settings on application side.
    - **Create Paylocity test user** - to have a counterpart of B.Simon in Paylocity that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Paylocity** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, the user doesn't have to perform any step as the app is already pre-integrated with Azure.
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL: `https://access.paylocity.com/`
7. Select **Save**.
8. Paylocity application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
9. In addition to above, Paylocity application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated, but you have to update these attributes with the real values.

    | Name | Source Attribute |
    | --- | --- |
    | PartnerID | `P8000010` |
    | PaylocityUser | `user.mail` |
    | PaylocityEntity | &lt; `PaylocityEntity` &gt; |

    Note

    The PaylocityEntity is Paylocity Company ID.
10. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
11. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, select **Edit Icon**.

    ![Screenshot that shows the &quot;S A M L Signing Certificate&quot; with the &quot;Download&quot; action for &quot;Federation Metadata X M L&quot; selected.](media/paylocity-tutorial/edit-samlassertion.png)
12. Select **Signing Option** as **Sign SAML response and assertion** and select **Save**.

    ![The SAML Signing Certificate Edit](media/paylocity-tutorial/saml-assertion.png)
13. On the **Set up Paylocity** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Paylocity SSO

To configure single sign-on on the **Paylocity** side,

1. Download the **Federation Metadata XML**.
2. In Paylocity, navigate to **HR & Payroll** &gt; **User Access** &gt; **SSO Configuration**.
3. Select **Add SSO Integration** under **SSO Integrations**. A new drawer opens.
4. Select **Microsoft Azure** as the SSO Provider from dropdown.
5. Select **Status** from dropdown.
6. Drag and drop metadata file in the drop area. Paylocity attempts to parse the Issuer, Post Redirect and Binding URLs and Security Certificate(s).
7. Select **Save** to confirm the changes. The integration should display under **SSO Integrations**.

### Create Paylocity test user

In this section, you create a user called B.Simon in Paylocity. Work with [Paylocity support team](mailto:service@paylocity.com) to add the users in the Paylocity platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Paylocity Sign on URL where you can initiate the login flow.
- Go to Paylocity Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Paylocity for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Paylocity tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Paylocity for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).