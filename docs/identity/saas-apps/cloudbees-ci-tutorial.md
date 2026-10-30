---
layout: Conceptual
title: Configure CloudBees CI for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/cloudbees-ci-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and CloudBees CI.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
locale: en-us
document_id: a15abaf5-1e47-7992-ff2d-c02cd9116c9e
document_version_independent_id: 0f98293b-4e34-e7ed-33a5-1aabf2d39adf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/cloudbees-ci-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/cloudbees-ci-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/cloudbees-ci-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 304beff9-5208-b95e-608a-be08a8b84461
---

# Configure CloudBees CI for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate CloudBees CI with Microsoft Entra ID. Centralize management, ensure compliance, and automate at scale with CloudBees CI - the secure, scalable, and flexible CI solution based on Jenkins. When you integrate CloudBees CI with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to CloudBees CI.
- Enable your users to be automatically signed-in to CloudBees CI with their Microsoft Entra accounts.
- Manage your accounts in one central location.

You'll configure and test Microsoft Entra single sign-on for CloudBees CI in a test environment. CloudBees CI supports only **SP** initiated single sign-on.

## Prerequisites

To integrate Microsoft Entra ID with CloudBees CI, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- CloudBees CI single sign-on (SSO) enabled subscription.

## Add application and assign a test user

Before you begin the process of configuring single sign-on, you need to add the CloudBees CI application from the Microsoft Entra gallery. You need a test user account to assign to the application and test the single sign-on configuration.

### Add CloudBees CI from the Microsoft Entra gallery

Add CloudBees CI from the Microsoft Entra application gallery to configure single sign-on with CloudBees CI. For more information on how to add application from the gallery, see the [Quickstart: Add application from the gallery](../enterprise-apps/add-application-portal).

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) article to create a test user account called B.Simon.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, and assign roles. The wizard also provides a link to the single sign-on configuration pane. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure Microsoft Entra SSO

Complete the following steps to enable Microsoft Entra single sign-on.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **CloudBees CI** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a value using the following pattern: `<Customer_EntityID>`

    b. In the **Reply URL** textbox, type a URL using one of the following patterns:

    | **Reply URL** |
    | --- |
    | `https://<CustomerDomain>/cjoc/securityRealm/finishLogin` |
    | `https://<CustomerDomain>/<Environment>/securityRealm/finishLogin` |
    | `https://cjoc.<CustomerDomain>/securityRealm/finishLogin` |
    | `https://<Environment>.<CustomerDomain>/securityRealm/finishLogin` |

    c. In the **Sign on URL** textbox, type the URL using one of the following patterns:

    | **Sign on URL** |
    | --- |
    | `https://<CustomerDomain>/cjoc` |
    | `https://<CustomerDomain>/<Environment>` |
    | `https://cjoc.<CustomerDomain>` |
    | `https://<Environment>.<CustomerDomain>` |

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [CloudBees CI support team](mailto:support@cloudbees.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. CloudBees CI application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![Screenshot shows the image of attributes configuration.](common/default-attributes.png)
7. In addition to above, CloudBees CI application expects few more attributes to be passed back in SAML response, which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | email | user.mail |
    | username | user.userprincipalname |
    | displayname | user.givenname |
    | groups | user.groups |
8. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
9. On the **Set up CloudBees CI** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

## Configure CloudBees CI SSO

To configure single sign-on in CloudBees CI, please follow [Configure Azure](https://github.com/jenkinsci/saml-plugin/blob/main/doc/CONFIGURE_AZURE.md) using the Federation Metadata XML and copied URLs.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to CloudBees CI Sign-on URL where you can initiate the login flow.
- Go to CloudBees CI Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the CloudBees CI tile in the My Apps, this option redirects to CloudBees CI Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).