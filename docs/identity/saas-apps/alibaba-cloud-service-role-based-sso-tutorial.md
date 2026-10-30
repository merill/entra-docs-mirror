---
layout: Conceptual
title: Configure Alibaba Cloud Service (Role-based SSO) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/alibaba-cloud-service-role-based-sso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Alibaba Cloud Service (Role-based SSO).
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1d85c3ba-4401-e23e-337c-1bc549634f8a
document_version_independent_id: 62e48b29-3592-ed64-7a93-bf5dfa119bee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/alibaba-cloud-service-role-based-sso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/alibaba-cloud-service-role-based-sso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/alibaba-cloud-service-role-based-sso-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/486161dc-fa28-4625-9b1c-1a21d690bc8d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5dd28c86-729c-4723-ab5a-57e26fcec2a8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b39855db-88d1-1162-eabf-d76c8bd8876b
---

# Configure Alibaba Cloud Service (Role-based SSO) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Alibaba Cloud Service (Role-based SSO) with Microsoft Entra ID. When you integrate Alibaba Cloud Service (Role-based SSO) with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Alibaba Cloud Service (Role-based SSO).
- Enable your users to be automatically signed-in to Alibaba Cloud Service (Role-based SSO) with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Alibaba Cloud Service is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Alibaba Cloud Service (Role-based SSO) single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Alibaba Cloud Service (Role-based SSO) supports **IDP** initiated SSO

## Adding Alibaba Cloud Service (Role-based SSO) from the gallery

To configure the integration of Alibaba Cloud Service (Role-based SSO) into Microsoft Entra ID, you need to add Alibaba Cloud Service (Role-based SSO) from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Alibaba Cloud Service (Role-based SSO)** in the search box.
4. Select **Alibaba Cloud Service (Role-based SSO)** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.
5. On the **Alibaba Cloud Service (Role-based SSO)** page, select **Properties** in the left-side navigation pane, and copy the **object ID** and save it on your computer for subsequent use.

    ![Properties config](media/alibaba-cloud-service-role-based-sso-tutorial/properties.png)

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Alibaba Cloud Service (Role-based SSO)

Configure and test Microsoft Entra SSO with Alibaba Cloud Service (Role-based SSO) using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Alibaba Cloud Service (Role-based SSO).

To configure and test Microsoft Entra SSO with Alibaba Cloud Service (Role-based SSO), perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure Role-Based Single Sign-On in Alibaba Cloud Service**- to enable your users to use this feature.
    1. **Configure Alibaba Cloud Service (Role-based SSO) SSO** - to configure the Single Sign-On settings on application side.
    2. **Create Alibaba Cloud Service (Role-based SSO) test user** - to have a counterpart of Britta Simon in Alibaba Cloud Service (Role-based SSO) that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Alibaba Cloud Service (Role-based SSO)** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    a. Select **Upload metadata file**.

    b. Select **folder logo** to select the metadata file and select **Upload**.

    Note

    1. For Alibaba Cloud International Site, please download the Service Provider metadata from [this](https://signin.alibabacloud.com/saml-role/sp-metadata.xml) link.
    2. For Alibaba Cloud Service(CN) Site, please download the Service Provider metadata from [this](https://signin.aliyun.com/saml-role/sp-metadata.xml) link.

    c. Once the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Alibaba Cloud Service (Role-based SSO) section textbox:

    Note

    If the **Identifier** and **Reply URL** values don't get auto populated, then fill in the values manually according to your requirement.
6. Alibaba Cloud Service (Role-based SSO) require roles to be configured in Microsoft Entra ID. The role claim is pre-configured so you don't have to configure it but you still need to create them in Microsoft Entra ID using this [article](../../identity-platform/howto-add-app-roles-in-apps#app-roles-ui).
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up Alibaba Cloud Service (Role-based SSO)** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Role-Based Single Sign-On in Alibaba Cloud Service

1. Sign in to the Alibaba Cloud [RAM console](https://account.alibabacloud.com/login/login.htm?oauth_callback=https%3A%2F%2Fram.console.aliyun.com%2F%3Fspm%3Da2c63.p38356.879954.8.7d904e167h6Yg9) by using Account1.
2. In the left-side navigation pane, select **SSO**.
3. On the **Role-based SSO** tab, select **Create IdP**.
4. On the displayed page, enter `AAD` in the IdP Name field, enter a description in the **Note** field, select **Upload** to upload the federation metadata file you downloaded before, and select **OK**.
5. After the IdP is successfully created, select **Create RAM Role**.
6. In the **RAM Role Name** field enter `AADrole`, select `AAD` from the **Select IdP** drop-down list and select OK.

    Note

    You can grant permission to the role as needed. After creating the IdP and the corresponding role, we recommend that you save the ARNs of the IdP and the role for subsequent use. You can obtain the ARNs on the IdP information page and the role information page.
7. Associate the Alibaba Cloud RAM role (AADrole) with the Microsoft Entra user (u2):

    To associate the RAM role with the Microsoft Entra user, you must create a role in Microsoft Entra ID by following these steps:

    1. Sign in to the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
    2. Select **modify permissions** to obtain required permissions for creating a role.

        ![Graph config1](media/alibaba-cloud-service-role-based-sso-tutorial/graph01.png)
    3. Select the following permissions from the list and select **Modify Permissions**, as shown in the following figure.

        ![Graph config2](media/alibaba-cloud-service-role-based-sso-tutorial/graph02.png)

        Note

        After permissions are granted, sign in to the Graph Explorer again.
    4. On the Graph Explorer page, select **GET** from the first drop-down list and **beta** from the second drop-down list. Then enter `https://graph.microsoft.com/beta/servicePrincipals` in the field next to the drop-down lists, and select **Run Query**.

        ![Graph config3](media/alibaba-cloud-service-role-based-sso-tutorial/graph03.png)

        Note

        If you're using multiple directories, you can enter `https://graph.microsoft.com/beta/contoso.com/servicePrincipals` in the field of the query.
    5. In the **Response Preview** section, extract the appRoles property from the 'Service Principal' for subsequent use.

        ![Graph config4](media/alibaba-cloud-service-role-based-sso-tutorial/graph05.png)

        Note

        You can locate the appRoles property by entering `https://graph.microsoft.com/beta/servicePrincipals/<objectID>` in the field of the query. Note that the `objectID` is the object ID you have copied from the Microsoft Entra ID **Properties** page.
    6. Go back to the Graph Explorer, change the method from **GET** to **PATCH**, paste the following content into the **Request Body** section, and select **Run Query**:

        ```json
          {
            "appRoles": [
              {
                "allowedMemberTypes": [
                  "User"
                ],
                "description": "msiam_access",
                "displayName": "msiam_access",
                "id": "41be2db8-48d9-4277-8e86-f6d22d35****",
                "isEnabled": true,
                "origin": "Application",
                "value": null
              },
              {
                "allowedMemberTypes": [
                  "User"
                ],
                "description": "Admin,AzureADProd",
                "displayName": "Admin,AzureADProd",
                "id": "68adae10-8b6b-47e6-9142-6476078cdbce",
                "isEnabled": true,
                "origin": "ServicePrincipal",
                "value": "acs:ram::187125022722****:role/aadrole,acs:ram::187125022722****:saml-provider/AAD"
              }
            ]
          }
        ```

        Note

        The `value` is the ARNs of the IdP and the role you created in the RAM console. Here, you can add multiple roles as needed. Microsoft Entra ID sends the value of these roles as the claim value in SAML response. However, you can only add new roles after the `msiam_access` part for the patch operation. To smooth the creation process, we recommend that you use an ID generator, such as GUID Generator, to generate IDs in real time.
    7. After the 'Service Principal' is patched with the required role, attach the role with the Microsoft Entra user (u2) by following the steps of **Assign the Microsoft Entra test user** section of the article.

### Configure Alibaba Cloud Service (Role-based SSO) SSO

To configure single sign-on on **Alibaba Cloud Service (Role-based SSO)** side, you need to send the downloaded **Federation Metadata XML** and appropriate copied URLs from the application configuration to [Alibaba Cloud Service (Role-based SSO) support team](https://www.aliyun.com/service/). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Alibaba Cloud Service (Role-based SSO) test user

In this section, you create a user called Britta Simon in Alibaba Cloud Service (Role-based SSO). Work with [Alibaba Cloud Service (Role-based SSO) support team](https://www.aliyun.com/service/) to add the users in the Alibaba Cloud Service (Role-based SSO) platform. Users must be created and activated before you use single sign-on.

## Test SSO

After the preceding configurations are completed, test Alibaba Cloud Service (Role-based SSO) by following these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Alibaba Cloud Service (Role-based SSO)**.
3. Select **Single sign-on**, and select **Test**.

    ![Test config1](media/alibaba-cloud-service-role-based-sso-tutorial/test03.png)
4. Select **Sign in as current user**.

    ![Test config2](media/alibaba-cloud-service-role-based-sso-tutorial/test04.png)
5. On the account selection page, select u2.

    ![Test config3](media/alibaba-cloud-service-role-based-sso-tutorial/test05.png)
6. The following page is displayed, indicating that role-based SSO is successful.

    ![Test config4](media/alibaba-cloud-service-role-based-sso-tutorial/test06.png)