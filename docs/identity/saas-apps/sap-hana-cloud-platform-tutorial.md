---
layout: Conceptual
title: Configure SAP Business Technology Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sap-hana-cloud-platform-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAP Business Technology Platform.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 86180988-3156-5ea5-4e9b-59cfb15a8b58
document_version_independent_id: 6163c71c-67c7-e766-4ba7-f95a81af1522
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sap-hana-cloud-platform-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sap-hana-cloud-platform-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sap-hana-cloud-platform-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1571c021-2015-3511-f531-e2e8865b95a6
---

# Configure SAP Business Technology Platform for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAP Business Technology Platform with Microsoft Entra ID. When you integrate SAP Business Technology Platform with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SAP Business Technology Platform.
- Enable your users to be automatically signed-in to SAP Business Technology Platform with their Microsoft Entra accounts.
- Manage your accounts in one central location.
- Assign users in Microsoft Entra to SAP Business technology Platform roles.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SAP Business Technology Platform single sign-on (SSO) enabled subscription.

Important

You need to deploy your own application or subscribe to an application on your SAP Business Technology Platform account to test single sign on. In this article, an application is deployed in the account.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- SAP Business Technology Platform supports **SP** initiated SSO.

## Add SAP Business Technology Platform from the gallery

To configure the integration of SAP Business Technology Platform into Microsoft Entra ID, you need to add SAP Business Technology Platform from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAP Business Technology Platform** in the search box.
4. Select **SAP Business Technology Platform** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SAP Business Technology Platform

Configure and test Microsoft Entra SSO with SAP Business Technology Platform using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SAP Business Technology Platform.

To configure and test Microsoft Entra SSO with SAP Business Technology Platform, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure SAP Business Technology Platform SSO**- to configure the Single Sign-On settings on application side.
    1. **Create SAP Business Technology Platform test user** - to have a counterpart of Britta Simon in SAP Business Technology Platform that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAP Business Technology Platform** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier** textbox you provide your SAP Business Technology Platform's type a URL using one of the following patterns:

    | **Identifier** |
    | --- |
    | `https://hanatrial.ondemand.com/<instancename>` |
    | `https://hana.ondemand.com/<instancename>` |
    | `https://us1.hana.ondemand.com/<instancename>` |
    | `https://ap1.hana.ondemand.com/<instancename>` |

    b. In the **Reply URL** textbox, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://<subdomain>.hanatrial.ondemand.com/<instancename>` |
    | `https://<subdomain>.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.us1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.dispatcher.us1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.ap1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.dispatcher.ap1.hana.ondemand.com/<instancename>` |
    | `https://<subdomain>.dispatcher.hana.ondemand.com/<instancename>` |

    c. In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP Business Technology Platform** application. This is the account-specific URL of a protected resource in your SAP Business Technology Platform application. The URL is based on the following pattern: `https://<applicationName><accountName>.<landscape host>.ondemand.com/<path_to_protected_resource>`

    Note

    This is the URL in your SAP Business Technology Platform application that requires the user to authenticate.

    | **Sign On URL** |
    | --- |
    | `https://<subdomain>.hanatrial.ondemand.com/<instancename>` |
    | `https://<subdomain>.hana.ondemand.com/<instancename>` |

    Note

    These values aren't real. Update these values with the actual Identifier,Reply URL and Sign on URL. Contact [SAP Business Technology Platform Client support team](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/5dd739823b824b539eee47b7860a00be.html) to get Sign-On URL and Identifier. Reply URL you can get from trust management section which is explained later in the article.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAP Business Technology Platform SSO

1. In a different web browser window, sign on to the SAP Business Technology Platform Cockpit at `https://account.<landscape host>.ondemand.com/cockpit`(for example: https://account.hanatrial.ondemand.com/cockpit).
2. Select the **Trust** tab.

    ![Trust](media/sap-hana-cloud-platform-tutorial/account.png)
3. In the Trust Management section, under **Local Service Provider**, perform the following steps:

    ![Screenshot that shows the &quot;Trust Management&quot; section with the &quot;Local Service Provider&quot; tab selected and all text boxes highlighted.](media/sap-hana-cloud-platform-tutorial/service.png)

    a. Select **Edit**.

    b. As **Configuration Type**, select **Custom**.

    c. As **Local Provider Name**, leave the default value. Copy this value and paste it into the **Identifier** field in the Microsoft Entra configuration for SAP Business Technology Platform.

    d. To generate a **Signing Key** and a **Signing Certificate** key pair, select **Generate Key Pair**.

    e. As **Principal Propagation**, select **Disabled**.

    f. As **Force Authentication**, select **Disabled**.

    g. Select **Save**.
4. After saving the **Local Service Provider** settings, perform the following to obtain the Reply URL:

    ![Get Metadata](media/sap-hana-cloud-platform-tutorial/certificate.png)

    a. Download the SAP Business Technology Platform metadata file by selecting **Get Metadata**.

    b. Open the downloaded SAP Business Technology Platform metadata XML file, and then locate the **ns3:AssertionConsumerService** tag.

    c. Copy the value of the **Location** attribute, and then paste it into the **Reply URL** field in the Microsoft Entra configuration for SAP Business Technology Platform.
5. Select the **Trusted Identity Provider** tab, and then select **Add Trusted Identity Provider**.

    ![Screenshot that shows the &quot;Trust Management&quot; page with the &quot;Trusted Identity Provider&quot; tab selected.](media/sap-hana-cloud-platform-tutorial/add-service.png)

    Note

    To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section. For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service. For None, you don't have any trust settings.
6. Select the **General** tab, and then select **Browse** to upload the downloaded metadata file.

    ![Trust Management](media/sap-hana-cloud-platform-tutorial/general.png)

    Note

    After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL**, and **Signing Certificate** are populated automatically.
7. Select the **Attributes** tab.
8. On the **Attributes** tab, perform the following step:

    ![Attributes](media/sap-hana-cloud-platform-tutorial/principal-attribute.png)

    a. Select **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:

    | Assertion Attribute | Principal Attribute |
    | --- | --- |
    | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` | firstname |
    | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` | lastname |
    | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` | email |

    Note

    The configuration of the Attributes depends on how the application(s) on SCP are developed, that is, which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.

    b. The **Default Attribute** in the screenshot is just for illustration purposes. It isn't required to make the scenario work.

    c. The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed. It's possible that your application requires different mappings.

### Assertion-based groups

As an optional step, you can configure assertion-based groups for your Microsoft Entra identity Provider.

Using groups on SAP Business Technology Platform allows you to dynamically assign one or more users to one or more roles in your SAP Business Technology Platform applications, determined by values of attributes in the SAML 2.0 assertion.

For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*". The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP Business Technology Platform account.

Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP Business Technology Platform account. If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP Business Technology Platform cockpit.

### Create SAP Business Technology Platform test user

In order to enable Microsoft Entra users to log in to SAP Business Technology Platform, you must assign roles in the SAP Business Technology Platform to them.

**To assign a role to a user, perform the following steps:**

1. Log in to your **SAP Business Technology Platform** cockpit.
2. Perform the following:

    ![Authorizations](media/sap-hana-cloud-platform-tutorial/roles.png)

    a. Select **Authorization**.

    b. Select the **Users** tab.

    c. In the **User** textbox, type the user’s email address.

    d. Select **Assign** to assign the user to a role.

    e. Select **Save**.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to SAP Business Technology Platform Sign-on URL where you can initiate the login flow.
- Go to SAP Business Technology Platform Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the SAP Business Technology Platform tile in the My Apps, you should be automatically signed in to the SAP Business Technology Platform for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Create groups for SAP Business Technology Platform application roles and assign groups to the Business Technology Platform role collection

You can create Microsoft Entra security groups and map those group IDs to the application roles. For more information, see [Managing access to SAP BTP](https://community.sap.com/t5/technology-blogs-by-members/identity-and-access-management-with-microsoft-entra-part-i-managing-access/ba-p/13873276).