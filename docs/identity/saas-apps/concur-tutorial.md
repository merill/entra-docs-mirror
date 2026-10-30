---
layout: Conceptual
title: Configure Concur for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/concur-tutorial
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
description: Learn how to configure SSO between Microsoft Entra ID and Concur.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: b611e5ec-8c62-ba14-adca-88293f803b04
document_version_independent_id: 063525f2-ce00-fb24-5282-4f21970c5308
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/concur-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/concur-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/concur-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3a8ef601-5921-c7dd-5f31-98bf36ff86b9
---

# Configure Concur for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Concur with Microsoft Entra ID. When you integrate Concur with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Concur.
- Enable your users to be automatically signed-in to Concur with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Note

The guidance provided in this article doesn't cover the new **Manage Single Sign-On** offering that's available from SAP Concur as of mid 2019. This new self-service SSO offering relies on **IdP initiated** sign-in which the current gallery app doesn't allow, due to the **Sign on URL** not being optional. The **Sign on URL** must be empty for IdP initiated sign-in via MyApps portal to work as intended. For these reason you must start out with a custom non-gallery application to set up SSO when using the **Manage Single Sign-On** feature in SAP Concur.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Concur single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Concur supports **SP** initiated SSO.
- Concur supports **Just In Time** user provisioning.

## Adding Concur from the gallery

To configure the integration of Concur into Microsoft Entra ID, you need to add Concur from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Concur** in the search box.
4. Select **Concur** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Concur

Configure and test Microsoft Entra SSO with Concur using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Concur.

To configure and test Microsoft Entra SSO with Concur, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Concur SSO**- to configure the Single Sign-On settings on application side.
    1. **Create Concur test user** - to have a counterpart of B.Simon in Concur that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Concur** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`

    c. For **Reply URL**, enter one of the following URL pattern:

    | Reply URL |
    | --- |
    | `https://www.concursolutions.com/SAMLRedirector/SAMLReceiver.ashx` |
    | `https://<customer-domain>.concursolutions.com/<OrganizationId>` |
    | `https://<customer-domain>.concur.com` |
    | `https://<customer-domain>.concursolutions.com` |

    Note

    These values aren't real. Update these values with the actual Sign-on URL, Identifier and Reply URL. Contact Concur Client support team to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Concur** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Concur SSO

To configure single sign-on on **Concur** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to Concur support team. They set this setting to have the SAML SSO connection set properly on both sides.

Note

The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact Concur Client support team to perform.

### Create Concur test user

In this section, a user called B.Simon is created in Concur. Concur supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Concur, a new one is created after authentication.

Concur also supports automatic user provisioning via SAP Cloud Identity Services. For more information, see how to configure provisioning of users [from Microsoft Entra ID to SAP Cloud Identity Services](sap-cloud-platform-identity-authentication-provisioning-tutorial), and how to configure provisioning of users [from SAP Cloud Identity Services to SAP Concur](https://help.sap.com/docs/cloud-identity-services/cloud-identity-services/target-sap-concur).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Concur Sign-on URL where you can initiate the login flow.
- Go to Concur Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Concur tile in the My Apps, this option redirects to Concur Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).