---
layout: Conceptual
title: Configure Snowflake for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/snowflake-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Snowflake.
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: a5733ec0-25ee-bd16-58d4-6a921f6ab1fd
document_version_independent_id: d80fe5dc-505f-5f7b-0f01-8e86233cd64a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/snowflake-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/snowflake-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/snowflake-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fca57e2b-1bf0-82cd-299c-2b0980f20b97
---

# Configure Snowflake for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Snowflake with Microsoft Entra ID. When you integrate Snowflake with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Snowflake.
- Enable your users to be automatically signed-in to Snowflake with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Snowflake is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

To configure Microsoft Entra integration with Snowflake, you need the following items:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Snowflake account and administrator role in that account.
- An administrator role in Microsoft Entra. Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Snowflake supports **SP and IDP** initiated SAML SSO.
- Snowflake also has an OpenID Connect (OIDC) integration, but that is not discussed in this article. For more information, see [Configuring OpenID Connect (OIDC) federated authentication](https://docs.snowflake.com/en/user-guide/admin-security-fed-auth-oidc).
- Snowflake supports [automated user provisioning and deprovisioning](snowflake-provisioning-tutorial) (recommended).
- Snowflake also supports Workload Identity Federation and OAuth for applications and agents using Microsoft Entra.

## Add Snowflake from the gallery

To configure the integration of Snowflake into Microsoft Entra ID, you need to add Snowflake from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Snowflake** in the search box.
4. Select **Snowflake** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Snowflake

Configure and test Microsoft Entra SSO with Snowflake using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Snowflake.

To configure and test Microsoft Entra SSO with Snowflake, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Snowflake SSO**- to configure the single sign-on settings on application side.
    1. **Create Snowflake test user** - to have a counterpart of B.Simon in Snowflake that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Snowflake** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, perform the following steps, if you wish to configure the application in **IDP** initiated mode:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com/fed/login`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    a. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com`

    b. In the **Logout URL** text box, type a URL using the following pattern: `https://<SNOWFLAKE-URL>.snowflakecomputing.com/fed/logout`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL, Sign-on URL, and sign out URL. For more information, see [Configuring SAML 2.0 federated authentication](https://docs.snowflake.com/en/user-guide/admin-security-fed-auth-security-integration). You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
8. On the **Set up Snowflake** section, copy one or more appropriate URLs as per your requirement.

    ![Screenshot shows to copy configuration appropriate U R L.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Snowflake SSO

1. In a different web browser window, sign in to Snowflake as a Security Administrator.
2. **Switch Role** to **ACCOUNTADMIN**, by selecting **profile** on the top right side of page.

    Note

    This is separate from the context you have selected in the top-right corner under your User Name.

    ![The Snowflake admin](media/snowflake-tutorial/account.png)
3. Open the **downloaded Base 64 certificate** in notepad. Copy the value between “-----BEGIN CERTIFICATE-----” and “-----END CERTIFICATE-----" and paste this content into the **SAML2\_X509\_CERT**.
4. In the **SAML2\_ISSUER**, paste **Identifier** value, which you copied previously.
5. In the **SAML2\_SSO\_URL**, paste **Login URL** value, which you copied previously.
6. In the **SAML2\_PROVIDER**, give the value like `CUSTOM`.
7. Select the **All Queries** and select **Run**.

    ![Snowflake sql](media/snowflake-tutorial/certificate.png)

    ```
    CREATE [ OR REPLACE ] SECURITY INTEGRATION [ IF NOT EXISTS ]
    TYPE = SAML2
    ENABLED = TRUE | FALSE
    SAML2_ISSUER = '<EntityID/Issuer value which you have copied>'
    SAML2_SSO_URL = '<Login URL value which you have copied>'
    SAML2_PROVIDER = 'CUSTOM'
    SAML2_X509_CERT = '<Paste the content of downloaded certificate from Azure portal>'
    [ SAML2_SP_INITIATED_LOGIN_PAGE_LABEL = '<string_literal>' ]
    [ SAML2_ENABLE_SP_INITIATED = TRUE | FALSE ]
    [ SAML2_SNOWFLAKE_X509_CERT = '<string_literal>' ]
    [ SAML2_SIGN_REQUEST = TRUE | FALSE ]
    [ SAML2_REQUESTED_NAMEID_FORMAT = '<string_literal>' ]
    [ SAML2_POST_LOGOUT_REDIRECT_URL = '<string_literal>' ]
    [ SAML2_FORCE_AUTHN = TRUE | FALSE ]
    [ SAML2_SNOWFLAKE_ISSUER_URL = '<string_literal>' ]
    [ SAML2_SNOWFLAKE_ACS_URL = '<string_literal>' ]
    ```

If you're using a new Snowflake URL with an organization name as the sign in URL, it's necessary to update the following parameters:

Alter the integration to add Snowflake Issuer URL and SAML2 Snowflake ACS URL, please follow the step-6 in [this](https://community.snowflake.com/s/knowledgebase) article for more information.

1. [ SAML2\_SNOWFLAKE\_ISSUER\_URL = '&lt;string\_literal&gt;' ]

    alter security integration `<your security integration name goes here>` set SAML2\_SNOWFLAKE\_ISSUER\_URL = `https://<organization_name>-<account name>.snowflakecomputing.com`;
2. [ SAML2\_SNOWFLAKE\_ACS\_URL = '&lt;string\_literal&gt;' ]

    alter security integration `<your security integration name goes here>` set SAML2\_SNOWFLAKE\_ACS\_URL = `https://<organization_name>-<account name>.snowflakecomputing.com/fed/login`;

Note

Follow [this](https://docs.snowflake.com/en/sql-reference/sql/create-security-integration.html) guide to know more about how to create a SAML2 security integration.

Note

If you have an existing SSO setup using `saml_identity_provider` account parameter, then follow [this](https://docs.snowflake.com/en/user-guide/admin-security-fed-auth-advanced.html) guide to migrate it to the SAML2 security integration.

### Create Snowflake test user

To enable Microsoft Entra users to sign in to Snowflake, they must be provisioned into Snowflake. In Snowflake, provisioning is a manual task.

**To provision a user account, perform the following steps:**

1. Sign in to Snowflake as a Security Administrator.
2. **Switch Role** to **ACCOUNTADMIN**, by selecting **profile** on the top right side of page.

    ![The Snowflake admin](media/snowflake-tutorial/account.png)
3. Create the user by running the below SQL query, ensuring "sign in name" is set to the Microsoft Entra username on the worksheet as shown below.

    ![The Snowflake adminsql](media/snowflake-tutorial/user.png)

    ```
     use role accountadmin;
     CREATE USER britta_simon PASSWORD = '' LOGIN_NAME = 'BrittaSimon@contoso.com' DISPLAY_NAME = 'Britta Simon';
    ```

Note

Manually provisioning is unnecessary, if users and groups are provisioned with a SCIM integration. See how to enable auto provisioning for [Snowflake](snowflake-provisioning-tutorial).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options. For more information on SAML error codes returned by Snowflake, see [Federated authentication and SSO troubleshooting](https://docs.snowflake.com/en/user-guide/errors-saml).

#### SP initiated:

- Select **Test this application**, this option redirects to Snowflake Sign on URL where you can initiate the login flow.
- Go to Snowflake Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Snowflake for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Snowflake tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Snowflake for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).

## Prevent application access through local accounts

Once you've validated that SSO works and rolled it out in your organization, we recommend disabling application access using local credentials. This ensures that your Conditional Access policies, MFA, etc. is in place to protect sign-ins to Snowflake. Review the Snowflake documentation for [configuring SSO](https://docs.snowflake.com/en/user-guide/admin-security-fed-auth-use), and use the ALTER USER commandlet to remove user passwords.