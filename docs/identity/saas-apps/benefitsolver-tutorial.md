---
layout: Conceptual
title: Configure Benefitsolver for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/benefitsolver-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Benefitsolver.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: 64a4870f-bb82-a4d5-8d15-417816541896
document_version_independent_id: 7310813c-e2b2-7a20-ab47-e33e771c4009
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/benefitsolver-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/benefitsolver-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/benefitsolver-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 19360dc7-52a6-344c-cf09-26d8df081a20
---

# Configure Benefitsolver for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Benefitsolver with Microsoft Entra ID. When you integrate Benefitsolver with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Benefitsolver.
- Enable your users to be automatically signed-in to Benefitsolver with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Benefitsolver single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Benefitsolver supports **SP** initiated SSO.

## Add Benefitsolver from the gallery

To configure the integration of Benefitsolver into Microsoft Entra ID, you need to add Benefitsolver from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Benefitsolver** in the search box.
4. Select **Benefitsolver** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Benefitsolver

Configure and test Microsoft Entra SSO with Benefitsolver using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Benefitsolver.

To configure and test Microsoft Entra SSO with Benefitsolver, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Benefitsolver SSO**- to configure the single sign-on settings on application side.
    1. **Create Benefitsolver test user** - to have a counterpart of B.Simon in Benefitsolver that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Benefitsolver** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** box, type a URL using the following pattern: `https://<companyname>.benefitsolver.com/saml20`

    b. In the **Reply URL** text box, type the URL using the following pattern: `https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `http://<companyname>.benefitsolver.com`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Benefitsolver Client support team](https://www.businessolver.com/contact-us/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. Benefitsolver application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the **User Attributes** section on application integration page. On the **Set up Single Sign-On with SAML** page, select **Edit** button to open **User Attributes** dialog.

    ![Screenshot shows User Attributes with the edit control called out.](common/edit-attribute.png)
7. In the **User Claims** section on the **User Attributes** dialog, edit the claims by using **Edit icon** or add the claims by using **Add new claim** to configure SAML token attribute as shown in the image above and perform the following steps:

    | Name | Source Attribute |
    | --- | --- |
    | ClientID | You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact-us/). |
    | ClientKey | You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact-us/). |
    | LogoutURL | You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact-us/). |
    | EmployeeID | You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact-us/). |
    |  |  |

    a. Select **Add new claim** to open the **Managed user claims** dialog.

    ![Screenshot shows User claims with Add new claim and Save called out.](common/new-save-attribute.png)

    ![Screenshot shows Manage user claims where you can enter the values described in this step.](common/new-attribute-details.png)

    b. In the **Name** textbox, type the attribute name shown for that row.

    c. Leave the **Namespace** blank.

    d. Select Source as **Attribute**.

    e. From the **Source attribute** list, type the attribute value shown for that row.

    f. Select **Ok**

    g. Select **Save**.
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up Benefitsolver** section, copy one or more appropriate URLs as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Benefitsolver SSO

To configure single sign-on on **Benefitsolver** side, you need to send the downloaded **Metadata XML** and appropriate copied URLs from the application configuration to [Benefitsolver support team](https://www.businessolver.com/contact-us/). They set this setting to have the SAML SSO connection set properly on both sides.

Note

Your Benefitsolver support team has to do the actual SSO configuration. You'll get a notification when SSO has been enabled for your subscription.

### Create Benefitsolver test user

In this section, you create a user called Britta Simon in Benefitsolver. Work with [Benefitsolver support team](https://www.businessolver.com/contact-us/) to add the users in the Benefitsolver platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Benefitsolver Sign-on URL where you can initiate the sign in flow.
- Go to Benefitsolver Sign-on URL directly and initiate the sign in flow from there.
- You can use Microsoft My Apps. When you select the Benefitsolver tile in the My Apps, this option redirects to Benefitsolver Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).