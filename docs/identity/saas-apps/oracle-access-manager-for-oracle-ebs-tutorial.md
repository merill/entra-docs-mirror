---
layout: Conceptual
title: Configure Oracle Access Manager for Oracle E-Business Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/oracle-access-manager-for-oracle-ebs-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Oracle Access Manager for Oracle E-Business Suite.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: e63eb1e7-6c81-da83-4fb3-0114f85d5771
document_version_independent_id: 374c05d0-cab8-4b33-11e4-133e124b1306
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/oracle-access-manager-for-oracle-ebs-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/oracle-access-manager-for-oracle-ebs-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/oracle-access-manager-for-oracle-ebs-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d5fb95c9-7bc0-2248-e859-a4a042657ad4
---

# Configure Oracle Access Manager for Oracle E-Business Suite for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Oracle Access Manager for Oracle E-Business Suite with Microsoft Entra ID. When you integrate Oracle Access Manager for Oracle E-Business Suite with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Oracle Access Manager for Oracle E-Business Suite.
- Enable your users to be automatically signed-in to Oracle Access Manager for Oracle E-Business Suite with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for Oracle Access Manager for Oracle E-Business Suite in a test environment. Oracle Access Manager for Oracle E-Business Suite supports only **SP** initiated single sign-on.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Prerequisites

To integrate Microsoft Entra ID with Oracle Access Manager for Oracle E-Business Suite, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Oracle Access Manager for Oracle E-Business Suite single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the Oracle Access Manager for Oracle E-Business Suite application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add Oracle Access Manager for Oracle E-Business Suite from the Microsoft Entra gallery

Add Oracle Access Manager for Oracle E-Business Suite from the Microsoft Entra application gallery to configure single sign-on with Oracle Access Manager for Oracle E-Business Suite. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Oracle Access Manager for Oracle E-Business Suite** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a URL using the following pattern: ` https://<SUBDOMAIN>.oraclecloud.com/`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.oraclecloud.com/v1/saml/<UNIQUEID>>`

    c. In the **Sign on URL** textbox, type a URL using the following pattern: ` https://<SUBDOMAIN>.oraclecloud.com/`
6. Your Oracle Access Manager for Oracle E-Business Suite application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows an example for this. The default value of **Unique User Identifier** is **user.userprincipalname** but Oracle Access Manager for Oracle E-Business Suite expects this to be mapped with the user's email address. For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.

    ![image](common/default-attributes.png)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)

## Configure Oracle Access Manager for Oracle E-Business Suite SSO

1. Sign to the Oracle Access Manager console as an Administrator.
2. Select the **Federation** tab at the top of the console.
3. In the **Federation** area of the **Launch Pad** tab, select **Service Provider Management**.
4. On the Service Provider Administration tab, select **Create Identity Provider Partner**.
5. In the **General** area, enter a name for the **Identity Provider partner** and select both **Enable Partner and Default Identity Provider Partner**. Go to the next step before saving.
6. In the **Service Information** area:

    a. Select **SAML2.0** as the protocol.

    b. Select **Load from provider metadata**.

    c. Select **Browse** (for Windows) or **Choose File** (for Mac) and select the **Federation Metadata XML** file that you downloaded previously.

    d. Go to the next step before saving.
7. In the **Mapping Options** area:

    a. Select the **User Identity Store** option that's used as the Oracle Access Manager LDAP identity store that's checked for E-Business Suite users. Typically, this is already configured as the Oracle Access Manager identity store.

    b. Leave **User Search Base DN** blank. The search base is automatically picked from the identity store configuration.

    c. Select **Map assertion Name ID to User ID Store attribute** and enter mail in the text box.
8. Select **Save** to save the identity provider partner.
9. After the partner is saved, come back to the **Advanced** area at the bottom of the tab. Ensure that the options are configured as follows:

    a. **Enable global logout** is selected.

    b. **HTTP POST SSO** Response Binding is selected.

### Create Oracle Access Manager for Oracle E-Business Suite test user

In this section, you create a user called Britta Simon at Oracle Access Manager for Oracle E-Business Suite. Work with [Oracle Access Manager for Oracle E-Business Suite support team](https://www.oracle.com/support/advanced-customer-services/cloud/) to add the users in the Oracle Access Manager for Oracle E-Business Suite platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Oracle Access Manager for Oracle E-Business Suite Sign-on URL where you can initiate the login flow.
- Go to Oracle Access Manager for Oracle E-Business Suite Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Oracle Access Manager for Oracle E-Business Suite tile in the My Apps, this option redirects to Oracle Access Manager for Oracle E-Business Suite Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).