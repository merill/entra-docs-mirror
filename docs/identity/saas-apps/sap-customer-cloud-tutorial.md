---
layout: Conceptual
title: Configure SAP Cloud for Customer for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sap-customer-cloud-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAP Cloud for Customer.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d33e9a4e-b5e2-cdfb-b3e0-0565e91fb78d
document_version_independent_id: 22602ede-b2c2-a9c1-4929-8cd7cfa8cef9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sap-customer-cloud-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sap-customer-cloud-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sap-customer-cloud-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d5af129a-a400-1088-de84-87ac820db95a
---

# Configure SAP Cloud for Customer for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAP Cloud for Customer with Microsoft Entra ID. When you integrate SAP Cloud for Customer with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SAP Cloud for Customer.
- Enable your users to be automatically signed-in to SAP Cloud for Customer with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SAP Cloud for Customer single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SAP Cloud for Customer supports **SP** initiated SSO.

## Add SAP Cloud for Customer from the gallery

To configure the integration of SAP Cloud for Customer into Microsoft Entra ID, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAP Cloud for Customer** in the search box.
4. Select **SAP Cloud for Customer** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SAP Cloud for Customer

Configure and test Microsoft Entra SSO with SAP Cloud for Customer using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SAP Cloud for Customer.

To configure and test Microsoft Entra SSO with SAP Cloud for Customer, complete the following building blocks:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SAP Cloud for Customer SSO**- to configure the single sign-on settings on application side.
    1. **Create SAP Cloud for Customer test user** - to have a counterpart of B.Simon in SAP Cloud for Customer that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAP Cloud for Customer** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign on URL** text box, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`

    Note

    These values aren't real. Update these values with the actual Sign on URL and Identifier. Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. SAP Cloud for Customer application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. Select **Edit** icon to open User Attributes dialog.

    ![Screenshot that shows the &quot;User Attributes&quot; dialog with the &quot;Edit&quot; icon selected.](common/edit-attribute.png)
7. In the **User Attributes** section on the **User Attributes & Claims** dialog, perform the following steps:

    a. Select **Edit icon** to open the **Manage user claims** dialog.

    ![Screenshot that shows the &quot;User Attributes &amp; Claims&quot; with the &quot;Edit&quot; icon selected.](media/sap-customer-cloud-tutorial/tutorial_usermail.png)

    ![image](media/sap-customer-cloud-tutorial/tutorial_usermailedit.png)

    b. Select **Transformation** as **source**.

    c. From the **Transformation** list, select **ExtractMailPrefix()**.

    d. From the **Parameter 1** list, select the user attribute you want to use for your implementation. For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.

    e. Select **Save**.
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up SAP Cloud for Customer** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAP Cloud for Customer SSO

1. Open a new web browser window and sign into your SAP Cloud for Customer company site as an administrator.
2. Go to **Applications & Resources** &gt; **Tenant Settings** and select **SAML 2.0 Configuration**.

    ![Screenshot that shows the Identity Providers page selected.](media/sap-customer-cloud-tutorial/configure.png)
3. On the **SAML 2.0 Configuration** section, perform the following steps:

    ![Screenshot that shows the &quot;S A M L 2.0 Configuration&quot; with the &quot;Browse&quot; button selected.](media/sap-customer-cloud-tutorial/configure02.png)

    a. Select **Browse** to upload the Federation Metadata XML file, which you have downloaded previously.

    b. Once the XML file is successfully uploaded, the below values get auto populated automatically then select **Save**.

### Create SAP Cloud for Customer test user

To enable Microsoft Entra users to sign in to SAP Cloud for Customer, they must be provisioned into SAP Cloud for Customer. In SAP Cloud for Customer, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to SAP Cloud for Customer as a Security Administrator.
2. From the left side of the menu, select on **Users & Authorizations** &gt; **User Management** &gt; **Add User**.

    ![Screenshot that shows the &quot;User Management&quot; page with the &quot;Add User&quot; button selected.](media/sap-customer-cloud-tutorial/configure03.png)
3. On the **Add New User** section, perform the following steps:

    ![SAP configuration](media/sap-customer-cloud-tutorial/configure04.png)

    a. In the **First Name** text box, enter the name of user like **B**.

    b. In the **Last Name** text box, enter the name of user like **Simon**.

    c. In **E-Mail** text box, enter the email of user like `B.Simon@contoso.com`.

    d. In the **Login Name** text box, enter the name of user like **B.Simon**.

    e. Select **User Type** as per your requirement.

    f. Select **Account Activation** option as per your requirement.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to SAP Cloud for Customer Sign-on URL where you can initiate the login flow.
- Go to SAP Cloud for Customer Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the SAP Cloud for Customer tile in the My Apps, this option redirects to SAP Cloud for Customer Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).