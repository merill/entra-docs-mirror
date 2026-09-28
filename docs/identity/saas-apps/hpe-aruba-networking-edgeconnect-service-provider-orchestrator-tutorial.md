---
layout: Conceptual
title: Configure HPE Aruba Networking EdgeConnect Service Provider Orchestrator for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and HPE Aruba Networking EdgeConnect Service Provider Orchestrator.
services: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 2024-08-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1686a29c-d8be-c1b7-9549-a8a657979ec8
document_version_independent_id: 1686a29c-d8be-c1b7-9549-a8a657979ec8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5bfc2259-d89d-4d6b-97d7-584a51208ec1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e3dafb9-38f2-4708-bb18-eecf2c0a9843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5bfc9a09-c94b-f7f8-4b5b-201e68552e7d
---

# Configure HPE Aruba Networking EdgeConnect Service Provider Orchestrator for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate HPE Aruba Networking EdgeConnect Service Provider Orchestrator with Microsoft Entra ID. When you integrate HPE Aruba Networking EdgeConnect Service Provider Orchestrator with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to HPE Aruba Networking EdgeConnect Service Provider Orchestrator.
- Enable your users to be automatically signed-in to HPE Aruba Networking EdgeConnect Service Provider Orchestrator with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- HPE Aruba Networking EdgeConnect Service Provider Orchestrator single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- HPE Aruba Networking EdgeConnect Service Provider Orchestrator supports **SP and IDP** initiated SSO.

## Add HPE Aruba Networking EdgeConnect Service Provider Orchestrator from the gallery

To configure the integration of HPE Aruba Networking EdgeConnect Service Provider Orchestrator into Microsoft Entra ID, you need to add HPE Aruba Networking EdgeConnect Service Provider Orchestrator from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **HPE Aruba Networking EdgeConnect Service Provider Orchestrator** in the search box.
4. Select **HPE Aruba Networking EdgeConnect Service Provider Orchestrator** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for HPE Aruba Networking EdgeConnect Service Provider Orchestrator

Configure and test Microsoft Entra SSO with HPE Aruba Networking EdgeConnect Service Provider Orchestrator using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in HPE Aruba Networking EdgeConnect Service Provider Orchestrator.

To configure and test Microsoft Entra SSO with HPE Aruba Networking EdgeConnect Service Provider Orchestrator, perform the following steps:

1. **Configure Microsoft Entra SSO** - This step will enable your users to use this feature.
2. **Create a Microsoft Entra test user** - This step allows you to test Microsoft Entra single sign-on with B.Simon.
3. **Assign the Test user to the HPE Aruba Networking EdgeConnect Service Provider Orchestrator application** - This step allows you to enable B.Simon to use Microsoft Entra single sign-on on EdgeConnect Orchestrator.
4. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **HPE Aruba Networking EdgeConnect Service Provider Orchestrator** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. Enter the values in **Identifier (Entity ID)** text box, **Reply URL (Assertion Consumer Service URL)** text box, and **Logout URL (Optional)** in the **Basic SAML Configuration** section. To find these values, first log in to Service Provider Orchestrator and navigate to the **Remote Authentication** dialog box **(Administration &gt; Remote Authentication)**.

    ![Screenshot shows the system settings of the Enterprise Authentication.](media/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial/remote.png)

    b. In the **Remote Authentication** dialog, select **+Add New Server**.

    c. Select **SAML** from the **Type** field.

    d. In the **Name** field, enter a name for your SAML configuration.

    e. Select the copy icon next to the **ACS URL** field.

    f. Navigate back to **Basic SAML Configuration** section on **Microsoft Set up single sign-on with SAML** page and paste the values as shown in the image below:

    ![Screenshot shows the configuration of the Enterprise Authentication.](media/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial/server.png)

    g. Select **Save** to close the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **Attributes & Claims** section, select the edit icon and copy the highlighted entry below, and paste the information into the **Username Attribute** field in Orchestrator as shown below:

    ![Screenshot shows the attributes settings of the Enterprise Authentication.](media/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial/global.png)
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
8. Open the certificate using a text editor such as Notepad. Copy and paste the content of the certificate on the **IdP X.509 Cert** field in Orchestrator as shown below:

    ![Screenshot shows the certificate editor of the Enterprise Authentication.](media/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial/point.png)
9. On the **Set up single sign-on with SAML** page, in the **Set up HPE Aruba Networking EdgeConnect Service Provider Orchestrator** section, copy the **Microsoft Entra Identifier** and paste it into the **Issuer URL** field. Copy the **Login URL** and paste it into the **SSO Endpoint** field:

    ![Screenshot shows the login settings of the Enterprise Authentication.](media/hpe-aruba-networking-edgeconnect-service-provider-orchestrator-tutorial/admin.png)
10. On the **Remote Authentication Server** dialog, set the **Default role** field. Example: SuperAdmin. (This is the last item on the dropdown list.) The Default role is needed if you did not define Role Based Access Control (RBAC) in the roles attributes in the Attributes & Claims section.
11. Select **Save** on the Remote Authentication Server dialog.
12. You have successfully configured SAML SSO authentication on the Orchestrator. The next step is to create a test user and assign the Orchestrator application to that user to verify if SAML is configured successfully.

### Create a Microsoft Entra ID test user

In this section, you create a test user in the Microsoft Entra admin center called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Test user to the HPE Aruba Networking EdgeConnect Service Provider Orchestrator application

In this section, you enable B.Simon to use Microsoft Entra single sign-on by granting access to HPE Aruba Networking EdgeConnect Service Provider Orchestrator.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **HPE Aruba Networking EdgeConnect Service Provider Orchestrator**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment** dialog.

    a. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.

    b. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.

    c. In the **Add Assignment** dialog, select the **Assign** button.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application** in Microsoft Entra admin center. this option redirects to HPE Aruba Networking EdgeConnect Service Provider Orchestrator Sign on URL where you can initiate the login flow.
- Go to HPE Aruba Networking EdgeConnect Service Provider Orchestrator Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application** in Microsoft Entra admin center and you should be automatically signed in to the HPE Aruba Networking EdgeConnect Service Provider Orchestrator for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the HPE Aruba Networking EdgeConnect Service Provider Orchestrator tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the HPE Aruba Networking EdgeConnect Service Provider Orchestrator for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).