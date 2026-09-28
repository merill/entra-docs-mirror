---
layout: Conceptual
title: Configure RedBrick Health for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/redbrick-health-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and RedBrick Health.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 5b386afe-c5ed-a6b8-a65e-5d1fe24400bd
document_version_independent_id: 830538e0-7b71-77de-7f8f-8d9be68432fb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/redbrick-health-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/redbrick-health-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/redbrick-health-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4d9515fb-5433-a6ec-01f3-7d35fde998e4
---

# Configure RedBrick Health for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate RedBrick Health with Microsoft Entra ID. When you integrate RedBrick Health with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to RedBrick Health.
- Enable your users to be automatically signed-in to RedBrick Health with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- RedBrick Health single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- RedBrick Health supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add RedBrick Health from the gallery

To configure the integration of RedBrick Health into Microsoft Entra ID, you need to add RedBrick Health from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **RedBrick Health** in the search box.
4. Select **RedBrick Health** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for RedBrick Health

Configure and test Microsoft Entra SSO with RedBrick Health using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in RedBrick Health.

To configure and test Microsoft Entra SSO with RedBrick Health, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure RedBrick Health SSO**- to configure the single sign-on settings on application side.
    1. **Create RedBrick Health test user** - to have a counterpart of B.Simon in RedBrick Health that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **RedBrick Health** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL: `https://www.redbrickhealth.com`

    b. In the **Reply URL** text box, type a URL: `https://sso-intg.redbrickhealth.com/sp/ACS.saml2`

    For Production Environment: `https://sso.redbrickhealth.com/sp/ACS.saml2`

    c. Select **Set additional URLs**.

    d. In the **Relay State** text box, type a URL using the following pattern: `https://api-sso2.redbricktest.com/identity/sso/nbound?target=https://vanity9-sso2.redbrickdev.com/portal&connection=<companyname>conn1`

    Note

    Relay State value isn't real. Update this value with the actual Relay State. Contact [RedBrick Health Client support team](https://home.redbrickhealth.com/contact/) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. RedBrick Health application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the **User Attributes** section on application integration page. On the **Set up Single Sign-On with SAML** page, select **Edit** button to open **User Attributes** dialog.

    ![Screenshot shows User Attributes with the Edit icon selected.](common/edit-attribute.png)
7. In the **User Claims** section on the **User Attributes** dialog, configure SAML token attribute as shown in the image above and perform the following steps:

    | Name | Source Attribute |
    | --- | --- |
    | principal name | \*\*\*\*\*\*\*\*\*\* |
    | client id | \*\*\*\*\*\*\*\*\*\* |
    | participant id | \*\*\*\*\*\*\*\*\*\* |

    Note

    These values are for reference purpose only. You need to define the attributes as per your organization's requirement. Please contact [RedBrick Health support team](https://home.redbrickhealth.com/contact/) to get more info about the required claims.

    a. Select **Add new claim** to open the **Manage user claims** dialog.

    ![Screenshot shows User claims with the option to Add new claim.](common/new-save-attribute.png)

    ![Screenshot shows the Manage user claims dialog box where you can enter the values described.](common/new-attribute-details.png)

    b. In the **Name** textbox, type the attribute name shown for that row.

    c. Leave the **Namespace** blank.

    d. Select Source as **Attribute**.

    e. From the **Source attribute** list, type the attribute value shown for that row.

    f. Select **Ok**

    g. Select **Save**.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up RedBrick Health** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure RedBrick Health SSO

To configure single sign-on on **RedBrick Health** side, you need to send the downloaded **Certificate (Base64)** and appropriate copied URLs from the application configuration to [RedBrick Health support team](https://home.redbrickhealth.com/contact/). They set this setting to have the SAML SSO connection set properly on both sides.

### Create RedBrick Health test user

In this section, you create a user called B.Simon in RedBrick Health. Work with [RedBrick Health support team](https://home.redbrickhealth.com/contact/) to add the users in the RedBrick Health platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the RedBrick Health for which you set up the SSO.
- You can use Microsoft My Apps. When you select the RedBrick Health tile in the My Apps, you should be automatically signed in to the RedBrick Health for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).