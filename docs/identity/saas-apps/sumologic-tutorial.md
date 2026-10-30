---
layout: Conceptual
title: Configure SumoLogic for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sumologic-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SumoLogic.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: acb82bd6-d934-691a-efb6-9c35d90ad1c7
document_version_independent_id: a32e3c30-8f89-e36f-2244-9ac01b485285
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sumologic-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sumologic-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sumologic-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: eaecf2a5-6d79-ce6e-1192-bcbb717e31c5
---

# Configure SumoLogic for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SumoLogic with Microsoft Entra ID. When you integrate SumoLogic with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SumoLogic.
- Enable your users to be automatically signed-in to SumoLogic with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SumoLogic single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SumoLogic supports **IDP** initiated SSO.

## Add SumoLogic from the gallery

To configure the integration of SumoLogic into Microsoft Entra ID, you need to add SumoLogic from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SumoLogic** in the search box.
4. Select **SumoLogic** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SumoLogic

Configure and test Microsoft Entra SSO with SumoLogic using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SumoLogic.

To configure and test Microsoft Entra SSO with SumoLogic, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SumoLogic SSO**- to configure the single sign-on settings on application side.
    1. **Create SumoLogic test user** - to have a counterpart of B.Simon in SumoLogic that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SumoLogic** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Set up single sign-on with SAML** page, perform the following steps:

    a. In the **Identifier** text box, type a URL using one of the following patterns:

    | Identifier URL |
    | --- |
    | `https://service.sumologic.com` |
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.jp.sumologic.com` |
    | `https://<tenantname>.de.sumologic.com` |
    | `https://<tenantname>.ca.sumologic.com` |
    |  |

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Reply URL |
    | --- |
    | `https://service.sumologic.com/sumo/saml/consume/<tenantname>` |
    | `https://service.us2.sumologic.com/sumo/saml/consume/<tenantname>` |
    | `https://service.us4.sumologic.com/sumo/saml/consume/<tenantname>` |
    | `https://service.eu.sumologic.com/sumo/saml/consume/<tenantname>` |
    | `https://service.jp.sumologic.com/sumo/saml/consume/<tenantname>` |
    | `https://service.de.sumologic.com/sumo/saml/consume/<tenantname>` |
    | `https://service.ca.sumologic.com/sumo/saml/consume/<tenantname>` |
    | `https://service.au.sumologic.com/sumo/saml/consume/<tenantname>` |
    |  |

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. SumoLogic application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, SumoLogic application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Roles | user.assignedroles |

    Note

    Please select [here](../../identity-platform/enterprise-app-role-management) to know how to configure **Role** in Microsoft Entra ID.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/certificatebase64.png)
9. On the **Set up SumoLogic** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SumoLogic SSO

1. In a different web browser window, sign in to your SumoLogic company site as an administrator.
2. Go to **Manage** &gt; **Security**.

    ![Manage](media/sumologic-tutorial/security.png)
3. Select **SAML**.

    ![Global security settings](media/sumologic-tutorial/settings.png)
4. From the **Select a configuration or create a new one** list, select **Microsoft Entra ID**, and then select **Configure**.

    ![Screenshot shows Configure SAML 2.0 where you can select Microsoft Entra ID.](media/sumologic-tutorial/configure.png)
5. On the **Configure SAML 2.0** dialog, perform the following steps:

    ![Screenshot shows the Configure SAML 2.0 dialog box where you can enter the values described.](media/sumologic-tutorial/configuration.png)

    a. In the **Configuration Name** textbox, type **Microsoft Entra ID**.

    b. Select **Debug Mode**.

    c. In the **Issuer** textbox, paste the value of **Microsoft Entra Identifier**.

    d. In the **Authn Request URL** textbox, paste the value of **Login URL**.

    e. Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.

    f. As **Email Attribute**, select **Use SAML subject**.

    g. Select **SP initiated Login Configuration**.

    h. In the **Login Path** textbox, type **Azure** and select **Save**.

### Create SumoLogic test user

In order to enable Microsoft Entra users to sign in to SumoLogic, they must be provisioned to SumoLogic. In the case of SumoLogic, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to your **SumoLogic** tenant.
2. Go to **Manage** &gt; **Users**.

    ![Screenshot shows Users selected from the Manage menu.](media/sumologic-tutorial/user.png)
3. Select **Add**.

    ![Screenshot shows the Add button for Users.](media/sumologic-tutorial/add-user.png)
4. On the **New User** dialog, perform the following steps:

    ![New User](media/sumologic-tutorial/new-account.png)

    a. Type the related information of the Microsoft Entra account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.

    b. Select a role.

    c. As **Status**, select **Active**.

    d. Select **Save**.

Note

You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the SumoLogic for which you set up the SSO.
- You can use Microsoft My Apps. When you select the SumoLogic tile in the My Apps, you should be automatically signed in to the SumoLogic for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).