---
layout: Conceptual
title: Configure VECOS Releezme Locker management system for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/vecos-releezme-locker-management-system-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and VECOS Releezme Locker management system.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: ad0b3851-2a8e-bcd5-7f4e-e0bf6202f05c
document_version_independent_id: 1d087f5c-16bb-e102-2c21-ff6b5c048970
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/vecos-releezme-locker-management-system-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/vecos-releezme-locker-management-system-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/vecos-releezme-locker-management-system-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ea557b5d-36cf-5d6c-ecae-0acf815e7b3b
---

# Configure VECOS Releezme Locker management system for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate VECOS Releezme Locker management system with Microsoft Entra ID. When you integrate VECOS Releezme Locker management system with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to VECOS Releezme Locker management system. Access to the VECOS Releezme Locker Management System is only needed for users who need to manage the lockers, that is, facility managers, service desk employees, and so on.
- Enable your users to be automatically signed-in to VECOS Releezme Locker management system with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- VECOS Releezme Locker management system single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- VECOS Releezme Locker management system supports **SP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add VECOS Releezme Locker management system from the gallery

To configure the integration of VECOS Releezme Locker management system into Microsoft Entra ID, you need to add VECOS Releezme Locker management system from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **VECOS Releezme Locker management system** in the search box.
4. Select **VECOS Releezme Locker management system** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for VECOS Releezme Locker management system

Configure and test Microsoft Entra SSO with VECOS Releezme Locker management system using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in VECOS Releezme Locker management system.

To configure and test Microsoft Entra SSO with VECOS Releezme Locker management system, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure VECOS Releezme Locker management system SSO**- to configure the single sign-on settings on application side.
    1. **Create VECOS Releezme Locker management system test user** - to have a counterpart of B.Simon in VECOS Releezme Locker management system that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **VECOS Releezme Locker management system** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier(Entity ID)** text box, type a URL using the following pattern: `https://<baseURL>/`

    b. In the **Reply URL** textbox, type a URL using the following pattern: `https://<baseURL>/Saml2/Acs`

    c. In the **Sign on URL** text box, type a URL using the following pattern:`https://<baseURL>/sso` (optionally add the `?companycode=` query parameter with the company code value given by VECOS.)

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [VECOS Releezme Locker management system support team](mailto:servicedesk@vecos.com) what region you're connecting to. Depending on your region, the URL's below is different:

    | **Region** | **baseURL** |
    | --- | --- |
    | Europe | `https://www.releezme.net` |
    | North America | `https://na.releezme.net` |
    | Asia Pacific | `https://au.releezme.net` |
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)

## Configure VECOS Releezme Locker management system Roles

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations**, and then select **All applications**.
3. In the app registrations list, select **VECOS Releezme Locker management system**.
4. In the app registration open **App roles**.
5. In the app roles page, create a new app role by selecting **Create app role**
6. In the **display name** field enter a name for the role, e.g., `VECOS Company Facility Manager`.
7. Select **Users/Groups** as the **Allowed member types** value.
8. Enter the VECOS Releezme Locker management system role name in the **Value** field. See table below.
9. Select **Apply**.

| Role | Role Value | Description |
| --- | --- | --- |
| Service Desk | CompanyServiceDesk | Limited access service desk. Mostly read-only access |
| Service Desk+ | CompanyServiceDeskPlus | Advanced version of the service desk with more read/write access |
| Facility Manager | CompanyFacilityManager | Facility Manager with access to setup of the company |
| Facility Manager+ | CompanyFacilityManagerPlus | Advanced Facility Manager with additional access within the company. |
| Administrator | CompanyAdmin | Administrator with full company access |

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure VECOS Releezme Locker management system SSO

To configure single sign-on on **VECOS Releezme Locker management system** side, you need to send the **App Federation Metadata Url** to [VECOS Releezme Locker management system support team](mailto:servicedesk@vecos.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create VECOS Releezme Locker management system test user

In this section, you create a user called Britta Simon in VECOS Releezme Locker management system. Work with [VECOS Releezme Locker management system support team](mailto:servicedesk@vecos.com) to add the users in the VECOS Releezme Locker management system platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to VECOS Releezme Locker management system Sign-on URL where you can initiate the login flow.
- Go to VECOS Releezme Locker management system Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the VECOS Releezme Locker management system tile in the My Apps, this option redirects to VECOS Releezme Locker management system Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).