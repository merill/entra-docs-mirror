---
layout: Conceptual
title: Configure VIDA for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/vida-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and VIDA.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 822c9929-2fed-cf30-9091-d1effe182e29
document_version_independent_id: d6640840-55a7-92b1-cd95-f0b52a67b204
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/vida-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/vida-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/vida-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c4ead23c-551b-6dd6-0254-a1865a990907
---

# Configure VIDA for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate VIDA with Microsoft Entra ID. When you integrate VIDA with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to VIDA.
- Enable your users to be automatically signed-in to VIDA with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- VIDA single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- VIDA supports **SP** initiated SSO.
- VIDA supports **Just In Time** user provisioning.

## Adding VIDA from the gallery

To configure the integration of VIDA into Microsoft Entra ID, you need to add VIDA from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **VIDA** in the search box.
4. Select **VIDA** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for VIDA

Configure and test Microsoft Entra SSO with VIDA using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in VIDA.

To configure and test Microsoft Entra SSO with VIDA, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure VIDA SSO**- to configure the single sign-on settings on application side.
    1. **Create VIDA test user** - to have a counterpart of B.Simon in VIDA that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **VIDA** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier (Entity ID)** text box, type the value: `urn:amazon:cognito:sp:eu-west-2_IDmTxjGr6`

    b. In the **Reply URL** text box, type the URL: `https://vitruevida.auth.eu-west-2.amazoncognito.com/saml2/idpresponse`

    c. In the **Sign-on URL** text box, type a URL using the following pattern:

    `https://vitruevida.com/?teamid=<ID>&idp=<IDP_NAME>`

    Note

    The Sign-on URL value isn't real. Update the value with the actual Sign-On URL. Contact [VIDA Client support team](mailto:support@vitruehealth.com) to get the value. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. VIDA application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, VIDA application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | assignedroles | user.assignedroles |
8. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
9. On the **Set up VIDA** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Role-Based Single Sign-On in VIDA

1. To associate a VIDA role with the Microsoft Entra user, you must create a role in Microsoft Entra ID by following these steps:

    a. Sign on to the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).

    b. Select **modify permissions** to obtain required permissions for creating a role.

    ![Graph config1](media/vida-tutorial/graph.png)

    c. Select the following permissions from the list and select **Modify Permissions**, as shown in the following figure.

    ![Graph config2](media/vida-tutorial/modify-permissions.png)

    Note

    After permissions are granted, log on to the Graph Explorer again.

    d. On the Graph Explorer page, select **GET** from the first drop-down list and **beta** from the second drop-down list. Then enter `https://graph.microsoft.com/beta/servicePrincipals` in the field next to the drop-down lists, and select **Run Query**.

    ![Graph configuration.](media/vida-tutorial/get-beta.png)

    Note

    If you're using multiple directories, you can enter `https://graph.microsoft.com/beta/contoso.com/servicePrincipals` in the field of the query.

    e. In the **Response Preview** section, extract the appRoles property from the 'Service Principal' for subsequent use.

    ![Response Preview.](media/vida-tutorial/preview.png)

    Note

    You can locate the appRoles property by entering `https://graph.microsoft.com/beta/servicePrincipals/<objectID>` in the field of the query. Note that the `objectID` is the object ID you have copied from the Microsoft Entra ID **Properties** page.

    f. Go back to the Graph Explorer, change the method from **GET** to **PATCH**, paste the following content into the **Request Body** section, and select **Run Query**:

    ```
    { 
    "appRoles": [
        {
            "allowedMemberTypes": [
            "User"
            ],
            "description": "User",
            "displayName": "User",
            "id": "18d14569-c3bd-439b-9a66-3a2aee01****",
            "isEnabled": true,
            "origin": "Application",
            "value": null
        },
        {
            "allowedMemberTypes": [
            "User"
            ],
            "description": "msiam_access",
            "displayName": "msiam_access",
            "id": "b9632174-c057-4f7e-951b-be3adc52****",
            "isEnabled": true,
            "origin": "Application",
            "value": null
        },
        {
        "allowedMemberTypes": [
            "User"
        ],
        "description": "VIDACompanyAdmin",
        "displayName": "VIDACompanyAdmin",
        "id": "293414bb-2215-48b4-9864-64520937d437",
        "isEnabled": true,
        "origin": "ServicePrincipal",
        "value": "VIDACompanyAdmin"
        },
        {
        "allowedMemberTypes": [
            "User"
        ],
        "description": "VIDATeamAdmin",
        "displayName": "VIDATeamAdmin",
        "id": "2884f1ae-5c0d-4afd-bf28-d7d11a3d7b2c",
        "isEnabled": true,
        "origin": "ServicePrincipal",
        "value": "VIDATeamAdmin"
        },
        {
        "allowedMemberTypes": [
            "User"
        ],
        "description": "VIDAUser",
        "displayName": "VIDAUser",
        "id": "37b3218c-0c06-484f-90e6-4390ce5a8787",
        "isEnabled": true,
        "origin": "ServicePrincipal",
        "value": "VIDAUser"
        }
    ]
    }
    ```

    Note

    Microsoft Entra ID will send the value of these roles as the claim value in SAML response. However, you can only add new roles after the `msiam_access` part for the patch operation. To smooth the creation process, we recommend that you use an ID generator, such as GUID Generator, to generate IDs in real time.

    g. After the 'Service Principal' is patched with the required role, attach the role with the Microsoft Entra user (B.Simon) by following the steps of **Assign the Microsoft Entra test user** section of the article.

## Configure VIDA SSO

To configure single sign-on on **VIDA** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [VIDA support team](mailto:support@vitruehealth.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create VIDA test user

In this section, a user called Britta Simon is created in VIDA. VIDA supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in VIDA, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to VIDA Sign-on URL where you can initiate the login flow.
- Go to VIDA Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the VIDA tile in the My Apps, this option redirects to VIDA Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).