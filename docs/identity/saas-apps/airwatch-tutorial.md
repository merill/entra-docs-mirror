---
layout: Conceptual
title: Configure AirWatch for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/airwatch-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and AirWatch.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e69b84a3-f907-118d-8a02-76b1c4ba267c
document_version_independent_id: c1468889-6502-372c-a718-3b59fe399375
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/airwatch-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/airwatch-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/airwatch-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8786f9a8-41e6-3097-a7ce-c83731121e41
---

# Configure AirWatch for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate AirWatch with Microsoft Entra ID. When you integrate AirWatch with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to AirWatch.
- Enable your users to be automatically signed-in to AirWatch with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- AirWatch single sign-on (SSO)-enabled subscription.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- AirWatch supports **SP** initiated SSO.

## Add AirWatch from the gallery

To configure the integration of AirWatch into Microsoft Entra ID, you need to add AirWatch from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **AirWatch** in the search box.
4. Select **AirWatch** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for AirWatch

Configure and test Microsoft Entra SSO with AirWatch using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in AirWatch.

To configure and test Microsoft Entra SSO with AirWatch, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure AirWatch SSO**- to configure the single sign-on settings on application side.
    1. **Create AirWatch test user** - to have a counterpart of B.Simon in AirWatch that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **AirWatch** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** page, enter the values for the following fields:

    a. In the **Identifier (Entity ID)** text box, type the value as: `AirWatch`

    b. In the **Reply URL** text box, type a URL using one of the following patterns:

    | Reply URL |
    | --- |
    | `https://<SUBDOMAIN>.awmdm.com/<COMPANY_CODE>` |
    | `https://<SUBDOMAIN>.airwatchportals.com/<COMPANY_CODE>` |
    |  |

    c. In the **Sign on URL** text box, type a URL using the following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    Note

    These values aren't the real. Update these values with the actual Reply URL and Sign-on URL. Contact [AirWatch Client support team](https://customerconnect.omnissa.com/home) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. AirWatch application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the **User Attributes** section on application integration page. On the **Set up Single Sign-On with SAML** page, select **Edit** button to open **User Attributes** dialog.

    ![image](common/edit-attribute.png)
7. In the **User Claims** section on the **User Attributes** dialog, edit the claims by using **Edit icon** or add the claims by using **Add new claim** to configure SAML token attribute as shown in the image above and perform the following steps:

    | Name | Source Attribute |
    | --- | --- |
    | UID | user.userprincipalname |
    |  |  |

    a. Select **Add new claim** to open the **Manage user claims** dialog.

    b. In the **Name** textbox, type the attribute name shown for that row.

    c. Leave the **Namespace** blank.

    d. Select Source as **Attribute**.

    e. From the **Source attribute** list, type the attribute value shown for that row.

    f. Select **Ok**

    g. Select **Save**.
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the Metadata XML and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up AirWatch** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure AirWatch SSO

1. In a different web browser window, sign in to your AirWatch company site as an administrator.
2. In the left navigation pane, select **Groups & Settings**, and then select **All Settings**.
3. Next, go to **System &gt; Enterprise Integration &gt; Directory Services**.
4. Select the **User** tab, in the **Base DN** field, type your `domain name`, and then select **Save**.
5. Select the **Group** tab, in the **Base DN** field, type your `domain name`, and then select **Save**.
6. Select the **Server** tab and perform the following steps:

    1. As **Directory Type**, select **None**.
    2. Enable the **Use SAML For Authentication** option.
    3. Select the **Import Identity Provider Settings** and select **Upload** to upload the XML file that you downloaded in Step4 above.
7. In the **Request** section, perform the following steps:

    1. As **Request Binding Type**, select **POST**.
    2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **AirWatch**.
    3. Under the **AirWatch Configuration** section, select **Configure AirWatch** to open **Configure sign-on** window
    4. Copy the **SAML Single Sign-On Service URL** from the **Quick Reference** section, and then paste it into the **Identity Provider Single Sign-On URL** textbox.
    5. As **NameID Format**, select **Email Address**.
    6. Select **Save**.
8. In the **Response** section, under **Response Binding Type**, select **Post**.
9. Select the **User** tab again.
10. Select **Show Advanced** to display the advanced user settings.
11. In the **Attribute** section, perform the following steps:

    ![Attribute](media/airwatch-tutorial/attributes.png)

    1. In the **Object Identifier** textbox, type `http://schemas.microsoft.com/identity/claims/objectidentifier`.
    2. In the **Username** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    3. In the **Display Name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    4. In the **First Name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    5. In the **Last Name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    6. In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    7. Select **Save**.

### Create AirWatch test user

To enable Microsoft Entra users to sign in to AirWatch, they must be provisioned in to AirWatch. In the case of AirWatch, provisioning is a manual task.

**To configure user provisioning, perform the following steps:**

1. Sign in to your **AirWatch** company site as administrator.
2. In the navigation pane on the left side, select **Accounts**, and then select **Users**.
3. In the **Users** menu, select **List View**, and then select **Add &gt; Add User**.
4. On the **Add / Edit User** dialog, perform the following steps:

    a. Type the **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Microsoft Entra account you want to provision into the related textboxes.

    b. Select **Save**.

Note

You can use any other AirWatch user account creation tools or APIs provided by AirWatch to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to AirWatch Sign-on URL where you can initiate the login flow.
- Go to AirWatch Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the AirWatch tile in the My Apps, this option redirects to AirWatch Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).