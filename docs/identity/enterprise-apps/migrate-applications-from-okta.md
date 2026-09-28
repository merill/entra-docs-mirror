---
layout: Conceptual
title: Migrate applications from Okta to Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-applications-from-okta
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Discover the process of migrating applications from Okta to Microsoft Entra ID, covering SAML, OpenID Connect, and OAuth 2.0 configurations.
ms.topic: how-to
ms.date: 2024-12-06T00:00:00.0000000Z
ms.reviewer: gasinh
ms.custom: not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 07e1a021-a944-1814-5e91-d1c53e1bf27c
document_version_independent_id: ef33c18c-d416-cf30-464b-f323c86ef5a9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migrate-applications-from-okta.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migrate-applications-from-okta
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migrate-applications-from-okta.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 94a54b15-0928-06a7-fc10-c042a3ab0889
---

# Migrate applications from Okta to Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this tutorial, you learn how to migrate your applications from Okta to Microsoft Entra ID.

## Prerequisites

To manage the application in Microsoft Entra ID, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, Application Administrator, or owner of the service principal.

## Create an inventory of current Okta applications

Before migration, document the current environment and application settings. You can use the Okta API to collect this information. Use an API explorer tool such as [Postman](https://www.postman.com/).

To create an application inventory:

1. With the Postman app, from the Okta admin console, generate an API token.
2. On the API dashboard, under **Security**, select **Tokens** &gt; **Create Token**.

    ![Screenshot of the Tokens and Create Tokens options under Security.](media/migrate-applications-from-okta/token-creation.png)
3. Enter a token name and then select **Create Token**.

    ![Screenshot of the Name entry under Create Token.](media/migrate-applications-from-okta/token-created.png)
4. Record the token value and save it. After you select **OK, got it**, it isn't accessible.

    ![Screenshot of the Token Value field and the OK got it option.](media/migrate-applications-from-okta/record-created.png)
5. In the Postman app, in the workspace, select **Import**.
6. On the **Import** page, select **Link**. To import the API, insert the following link:

`https://developer.okta.com/docs/api/postman/example.oktapreview.com.environment`

![Screenshot of the Link and Continue options on Import.](media/migrate-applications-from-okta/link-to-import.png)

Note

Don't modify the link with your tenant values.

1. Select **Import**.

    ![Screenshot of the Import option on Import.](media/migrate-applications-from-okta/next-import-menu.png)
2. After the API is imported, change the **Environment** selection to **{yourOktaDomain}**.
3. To edit your Okta environment, select the **eye** icon. Then select **Edit**.

    ![Screenshot of the eye icon and Edit option on Overview.](media/migrate-applications-from-okta/edit-environment.png)
4. In the **Initial Value** and **Current Value** fields, update the values for the URL and API key. Change the name to reflect your environment.
5. Save the values.

    ![Screenshot of Initial Value and Current Value fields on Overview.](media/migrate-applications-from-okta/update-values-for-api.png)
6. [Load the API into Postman](https://app.getpostman.com/run-collection/377eaf77fdbeaedced17).
7. Select **Apps** &gt; **Get List Apps** &gt; **Send**.

Note

You can print the applications in your Okta tenant. The list is in JSON format.

![Screenshot of the Send option and the Apps list.](media/migrate-applications-from-okta/list-of-applications.png)

We recommend you copy and convert this JSON list to a CSV format:

- Use a public converter such as [Konklone](https://konklone.io/json/)
- Or for PowerShell, use [ConvertFrom-Json](/en-us/powershell/module/microsoft.powershell.utility/convertfrom-json) and [ConvertTo-CSV](/en-us/powershell/module/microsoft.powershell.utility/convertto-csv)

Note

To have a record of the applications in your Okta tenant, download the CSV.

## Migrate a SAML application to Microsoft Entra ID

To migrate a SAML 2.0 application to Microsoft Entra ID, configure the application in your Microsoft Entra tenant for application access. In this example, we convert a Salesforce instance.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**, then select **New application**.
3. In **Microsoft Entra Gallery**, search for **Salesforce**, select the application, and then select **Create**.

    ![Screenshot of applications in the Microsoft Entra Gallery.](media/migrate-applications-from-okta/salesforce-application.png)
4. After the application is created, on the **Single sign-on (SSO)** tab, select **SAML**.

    ![Screenshot of the SAML option on Single sign-on.](media/migrate-applications-from-okta/saml-application.png)
5. Download the **Certificate (Raw)** and **Federation Metadata XML** to import it into Salesforce.
6. On the Salesforce administration console, select **Identity** &gt; **Single Sign-On Settings** &gt; **New from Metadata File**.

    ![Screenshot of the New from Metadata File option under Single Sign On Settings.](media/migrate-applications-from-okta/salesforce-admin-console.png)
7. Upload the XML file you downloaded from the Microsoft Entra admin center. Then select **Create**.
8. Upload the certificate you downloaded from Azure. Select **Save**.
9. Record the values in the following fields. The values are in Azure.

    - **Entity ID**
    - **Login URL**
    - **Logout URL**
10. Select **Download Metadata**.
11. To upload the file to the Microsoft Entra admin center, in the Microsoft Entra ID **Enterprise applications** page, in the SAML SSO settings, select **Upload metadata file**.
12. Ensure the imported values match the recorded values. Select **Save**.

    ![Screenshot of entries for SAML-based sign-on, and Basic SAML Configuration.](media/migrate-applications-from-okta/upload-metadata-file.png)
13. In the Salesforce administration console, select **Company Settings** &gt; **My Domain**. Go to **Authentication Configuration** and then select **Edit**.

    ![Screenshot of the Edit option under My Domain.](media/migrate-applications-from-okta/edit-company-settings.png)
14. For a sign-in option, select the new SAML provider you configured. Select **Save**.

    ![Screenshot of Authentication Service options under Authentication Configuration.](media/migrate-applications-from-okta/save-saml-provider.png)
15. In Microsoft Entra ID, on the **Enterprise applications** page, select **Users and groups**. Then add test users.

    ![Screenshot of Users and groups with a list of test users.](media/migrate-applications-from-okta/add-test-user.png)
16. To test the configuration, sign in as a test user. Go to the Microsoft [apps gallery](https://aka.ms/myapps) and then select **Salesforce**.

    ![Screenshot of the Salesforce option under All Apps, on My Apps.](media/migrate-applications-from-okta/test-user-sign-in.png)
17. To sign in, select the configured identity provider (IdP).

    ![Screenshot of the Salesforce sign-in page.](media/migrate-applications-from-okta/new-identity-provider.png)

Note

If configuration is correct, the test user lands on the Salesforce home page. For troubleshooting help, see the [debugging guide](debug-saml-sso-issues).

1. On the **Enterprise applications** page, assign the remaining users to the Salesforce application, with the correct roles.

Note

After you add the remaining users to the Microsoft Entra application, users can test the connection to ensure they have access. Test the connection before the next step.

1. On the Salesforce administration console, select **Company Settings** &gt; **My Domain**.
2. Under **Authentication Configuration**, select **Edit**. For authentication service, clear the selection for **Okta**.

    ![Screenshot of the Save option and Authentication Service options, under Authentication Configuration.](media/migrate-applications-from-okta/deselect-okta.png)

## Migrate an OpenID Connect or OAuth 2.0 application to Microsoft Entra ID

To migrate an OpenID Connect (OIDC) or OAuth 2.0 application to Microsoft Entra ID, in your Microsoft Entra tenant, configure the application for access. In this example, we convert a custom OIDC app.

To complete the migration, repeat configuration for all applications in the Okta tenant.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select **New application**.
4. Select **Create your own application**.
5. On the menu that appears, name the OIDC app and then select **Register an application you're working on to integrate with Microsoft Entra ID**.
6. Select **Create**.
7. On the next page, set up the tenancy of your application registration. For more information, see [Tenancy in Microsoft Entra ID](../../identity-platform/single-and-multi-tenant-apps). Go to **Accounts in any organizational directory (Any Microsoft Entra directory - Multitenant)** &gt; **Register**.

    ![Screenshot of the option for Accounts in any organizational directory (Any Microsoft Entra directory - Multitenant).](media/migrate-applications-from-okta/multitenant-register-app.png)
8. On the **App registrations** page, under **Microsoft Entra ID**, open the created registration.

Note

Depending on the [application scenario](../../identity-platform/authentication-flows-app-scenarios), there are various configuration actions. Most scenarios require an app client secret.

1. On the **Overview** page, record the **Application (client) ID**. You use this ID in your application.
2. On the left, select **Certificates & secrets**. Then select **+ New client secret**. Name the client secret and set its expiration.
3. Record the value and ID of the secret.

Note

If you misplace the client secret, you can't retrieve it. Instead, regenerate a secret.

1. On the left, select **API permissions**. Then grant the application access to the OIDC stack.
2. Select **+ Add permission** &gt; **Microsoft Graph** &gt; **Delegated permissions**.
3. In the **OpenId permissions** section, select **email**, **openid**, and **profile**. Then select **Add permissions**.
4. To improve user experience and suppress user consent prompts, select **Grant admin consent for Tenant Domain Name**. Wait for the **Granted** status to appear.

    ![Screenshot of the Successfully granted admin consent for the requested permissions message, under API permissions.](media/migrate-applications-from-okta/grant-admin-consent.png)
5. If your application has a redirect URI, enter the URI. If the reply URL targets the **Authentication** tab, followed by **Add a platform** and **Web**, enter the URL.
6. Select **Access tokens** and **ID tokens**.
7. Select **Configure**.
8. If needed, on the **Authentication** menu, under **Advanced settings** and **Allow public client flows**, select **Yes**.

    ![Screenshot of the Yes option on Authentication.](media/migrate-applications-from-okta/allow-client-flows.png)
9. Before you test, in your OIDC-configured application, import the application ID and client secret.

Note

Use the previous steps to configure your application with settings such as Client ID, Secret, and Scopes.

## Migrate a custom authorization server to Microsoft Entra ID

Okta authorization servers map one-to-one to application registrations that [expose an API](../../identity-platform/quickstart-configure-app-expose-web-apis#add-a-scope).

Map the default Okta authorization server to Microsoft Graph scopes or permissions.

![Screenshot of the Add a scope option on Expose and API.](media/migrate-applications-from-okta/default-okta-authorization.png)