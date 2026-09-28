---
layout: Conceptual
title: Configure OIDC SSO for gallery and custom applications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/add-application-portal-setup-oidc-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to configure OpenID Connect-based single sign-on (SSO) in Microsoft Entra ID for both gallery applications and your own custom (non-gallery) applications.
ms.topic: how-to
ms.date: 2025-07-22T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: enterprise-apps
locale: en-us
document_id: 92406442-8660-21d8-c0ce-a29e91351739
document_version_independent_id: 70ce205a-9019-2a4a-087e-6b0239e77a21
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/add-application-portal-setup-oidc-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/add-application-portal-setup-oidc-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/add-application-portal-setup-oidc-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 56f953a5-b118-dbb0-43f5-97902ec861e3
---

# Configure OIDC SSO for gallery and custom applications - Microsoft Entra ID | Microsoft Learn

This article shows you how to configure OpenID Connect (OIDC) Single sign-on (SSO) in Microsoft Entra ID for both gallery applications and custom (non-gallery) applications. With OIDC SSO, your users can sign in to applications using their Microsoft Entra credentials, providing a seamless authentication experience.

OIDC is an authentication protocol built on top of OAuth 2.0 that enables secure user authentication and single sign-on. For detailed information about the OIDC protocol, see [OIDC authentication with the Microsoft identity platform](../../identity-platform/v2-protocols-oidc).

We recommend you use a nonproduction environment to test the steps in this article.

Before configuring OIDC SSO, it's helpful to understand the following core concepts:

- **App registrations vs. Enterprise applications**: App registrations define your application's identity and configuration, while enterprise applications represent instances of those apps in your tenant. To learn more, see [Application and service principal objects in Microsoft Entra ID](../../identity-platform/app-objects-and-service-principals).
- **Permissions and consent**: Applications request permissions to access resources, and users or administrators grant consent. For details on the consent framework, see [Permissions and consent in the Microsoft identity platform](../../identity-platform/permissions-consent-overview).
- **Multi-tenant applications**: Applications that can be used by multiple organizations. For guidance on multi-tenancy, see [How to: Convert your app to be multitenant](../../identity-platform/howto-convert-app-to-be-multi-tenant).
- **Authentication flows**: Different methods for authenticating users, such as the Authorization Code flow with PKCE for single-page applications. For more information, see [Microsoft identity platform authentication flows](../../identity-platform/msal-authentication-flows).
- **OIDC SSO**: A method of single sign-on that uses the OIDC protocol to authenticate users across applications. It allows users to sign in once and access multiple applications without needing to reenter credentials.

## Prerequisites

To configure OIDC-based SSO, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - Cloud Application Administrator
    - Application Administrator
    - Owner of the service principal
- For custom applications: Details about your application including its redirect URIs and authentication requirements

## Configure OIDC SSO for Microsoft Entra app gallery apps

Gallery applications in Microsoft Entra ID come preconfigured with OIDC support, making setup straightforward through a consent-based process.

When you add an enterprise application that uses the OIDC standard for SSO, you select the **Sign Up** button. The button is on the right hand side pane when you select the app from the app gallery. When you select the button, you complete the sign-up process for the application.

To configure OIDC-based SSO for a gallery application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. In the **All applications** pane, select **New application**.
4. The **Browse Microsoft Entra Gallery** pane opens. In this example, we use **SmartSheet**.
5. Select **Sign-up for SmartSheet**. Sign in with the user account credentials from Microsoft Entra ID. If you already have a subscription to the application, then user details and tenant information is validated. If the application isn't able to verify the user, then it redirects you to sign up for the application service.

    [![Complete the consent screen for an application.](media/add-application-portal-setup-oidc-sso/oidc-sso-configuration.png)](media/add-application-portal-setup-oidc-sso/oidc-sso-configuration.png#lightbox)

    After entering the sign-in credentials, the consent screen appears. The consent screen provides information about the application and the permissions it requires.
6. Select **Consent on behalf of your organization** and then select **Accept**. The application is added to your tenant and the application home page appears.

Contact the application vendor to learn about any additional configuration steps required for the application.

Note

You can add only one instance of a gallery application. Once you add an application and try to provide consent again, you can't add it again to the tenant.

For more information about user and admin consent, see [Understand user and admin consent](../../identity-platform/howto-convert-app-to-be-multi-tenant#understand-user-and-admin-consent-and-make-appropriate-code-changes). For comprehensive information about the consent framework, see [Permissions and consent in the Microsoft identity platform](../../identity-platform/permissions-consent-overview).

## Configure OIDC SSO for custom (non-gallery) applications

For applications not available in the Microsoft Entra gallery, you need to manually register and configure the application. This section provides step-by-step guidance for setting up OIDC SSO with a custom application.

### Step 1: Register your application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations** &gt; **New registration**.
3. Enter a **Name** for your application (for example, "My Custom Web App").
4. Under **Supported account types**, select the appropriate option:
    - **Accounts in this organizational directory only** for single-tenant applications
    - **Accounts in any organizational directory** for more information on multitenant applications, see [multitenant applications](../../identity-platform/howto-convert-app-to-be-multi-tenant)
    - **Accounts in any organizational directory and personal Microsoft accounts** if you want to support both work/school and personal accounts
5. For **Redirect URI**, select the platform type and enter your application's redirect URI:
    - **Web**: For server-side web applications (for example, `https://contoso.com/auth/callback`)
    - **Single-page application (SPA)**: For client-side applications using modern auth flows (for example, `https://contoso.com` or `http://localhost:3000` for development)
    - **Public client/native**: For mobile and desktop applications
6. Select **Register**.

### Step 2: Configure authentication settings

1. In your app registration, navigate to **Authentication**.
2. Verify your redirect URIs are correctly configured for your platform type.
3. **Configure authentication flows** (important for security):

    **For Single-Page Applications (SPAs):**

    - Ensure your redirect URIs are listed under the **Single-page application** platform. This option automatically configures the secure **Authorization Code flow with PKCE**, which is the recommended approach for SPAs
    - **Do NOT enable** the implicit grant option unless necessary for legacy applications

    **For Web Applications:**

    - Ensure your redirect URIs are listed under the **Web** platform. This option configures the standard **Authorization Code flow**.

    Warning

    The implicit grant flow is **not recommended** for new applications due to security vulnerabilities, including token leakage in browser history. Microsoft strongly recommends using the **Authorization Code flow with PKCE** for single-page applications instead. Only enable these options if you have a legacy application that can't be updated to support more secure flows and you understand the associated security risks.

    For more information on authentication flows, see [Microsoft identity platform authentication flows](../../identity-platform/msal-authentication-flows).

### Step 3: Configure client credentials (for web applications)

If your application is a confidential client (server-side web application that can securely store secrets):

1. Navigate to **Certificates & secrets**.
2. Select **New client secret**.
3. Add a description and select an expiration period.
4. Select **Add** and copy the secret value immediately (it can't be shown again).
5. Store the client secret securely in your application configuration.

Tip

For production applications, consider using certificates instead of client secrets for enhanced security. See [Certificate credentials](../../identity-platform/certificate-credentials).

### Step 4: Configure API permissions

1. Navigate to **API permissions**.
2. The `User.Read` permission for Microsoft Graph is added by default.
3. For OIDC authentication, you typically need these delegated permissions:
    - **openid**: Required for OIDC authentication
    - **profile**: To access user's profile information
    - **email**: To access user's email address
4. To add more permissions:
    - Select **Add a permission**
    - Choose **Microsoft Graph**
    - Select **Delegated permissions**
    - Search for and select the required permissions (for example, openid, profile, email)
    - Select **Add permissions**
5. If your application requires permissions that need admin consent, select **Grant admin consent for [your tenant]**.

For an introduction to permissions and consent, see [Permissions and consent in the Microsoft identity platform](../../identity-platform/permissions-consent-overview).

### Step 5: Configure optional claims (if needed)

1. Navigate to **Token configuration**.
2. Select **Add optional claim**.
3. Choose the optional claims you want to add (for example, `email`, `given_name`, `family_name`).
4. Select **Add** to apply the changes.

### Step 6: Gather application details

After registration and configuration, collect the following information needed for your application:

1. From the **Overview**page, note:
    - **Application (client) ID**: Your app's unique identifier
    - **Directory (tenant) ID**: Your tenant's unique identifier
2. Select **Endpoints**to view the OIDC metadata and endpoints:
    - **OIDC metadata document**: `https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid_configuration`
    - **Authorization endpoint**: For initiating sign-in flows
    - **Token endpoint**: For exchanging authorization codes for tokens
    - **JWKS URI**: For token signature validation

These details are used in your application's OIDC library configuration.

### Step 7: Configure your application code

Use the gathered information to configure your application's OIDC library with:

- **Client ID**: The Application (client) ID from step 5
- **Client Secret**: If applicable (for web applications)
- **Redirect URI**: The same URI configured in step 1
- **Authority/Issuer**: `https://login.microsoftonline.com/{tenant}/v2.0/` (replace {tenant} with your tenant ID)
- **Scopes**: Typically `openid profile email` for basic OIDC authentication

For specific implementation guidance, see [Authorization Code flow with PKCE](../../identity-platform/v2-oauth2-auth-code-flow) for web applications.

### Step 8: Test your OIDC SSO configuration

1. **Using an online tool**: You can test the basic authentication flow using https://jwt.ms:

    - Construct a sign-in URL: `https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?client_id={client_id}&response_type=id_token&redirect_uri=https://jwt.ms&scope=openid&nonce={random_value}`
    - Replace `{tenant}` and `{client_id}` with your values
    - Navigate to this URL in a browser to test the authentication flow
2. **Within your application**: Integrate the OIDC library in your application and test the complete sign-in experience.
3. **Assign users**: Navigate to **Enterprise applications**, find your app, and assign users or groups under **Users and groups**.

## Multitenant app considerations

If your application needs to support users from multiple organizations:

- Configure the app registration with **Accounts in any organizational directory**
- Use the common endpoint: `https://login.microsoftonline.com/common/`
- Implement proper tenant validation in your application logic

For detailed guidance, see [How to: Convert your app to be multitenant](../../identity-platform/howto-convert-app-to-be-multi-tenant).

## Troubleshooting common issues

- **Invalid redirect URI**: Ensure the redirect URI in your app registration exactly matches what your application sends
- **Consent issues**: Check if admin consent is required for the requested permissions
- **Token validation errors**: Verify you're using the correct JWKS URI and validating the token signature
- **Multi-tenant issues**: Ensure you're using the correct endpoint (common vs. tenant-specific)

For comprehensive troubleshooting guidance, see [Microsoft identity platform error codes](../../identity-platform/reference-error-codes).