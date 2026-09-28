---
layout: Conceptual
title: 'Custom claims provider: Configure a token issuance event - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-extension-tokenissuancestart-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure a custom claims provider for a token issuance start event in Microsoft Entra ID. You can add custom claims to a token before it's issued.
manager: pmwongera
ms.date: 2025-05-04T00:00:00.0000000Z
ms.reviewer: stsoneff
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 40fcb5f9-70d5-51ce-2112-f5de2d9fada1
document_version_independent_id: 40fcb5f9-70d5-51ce-2112-f5de2d9fada1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-extension-tokenissuancestart-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-extension-tokenissuancestart-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-extension-tokenissuancestart-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: afe732aa-3950-68b8-e2f2-c12243c312e0
---

# Custom claims provider: Configure a token issuance event - Microsoft identity platform | Microsoft Learn

This article describes how to configure a custom claims provider for a [token issuance start event](custom-claims-provider-overview#token-issuance-start-event-listener). Using an existing Azure Functions REST API, you'll register a custom authentication extension and add attributes that you expect it to parse from your REST API. To test the custom authentication extension, you'll register a sample OpenID Connect application to get a token and view the claims.

This video outlines the procedure of mapping claims from external systems into security tokens using Microsoft Entra custom claims provider.

## Prerequisites

- An Azure subscription with the ability to create Azure Functions. If you don't have an existing Azure account, sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) or use your [Visual Studio Subscription](https://visualstudio.microsoft.com/subscriptions/) benefits when you [create an account](https://account.windowsazure.com/Home/Index).
- An HTTP trigger function configured for a token issuance event deployed to Azure Functions. If you don't have one, follow the steps in [create a REST API for a token issuance start event in Azure Functions](custom-extension-tokenissuancestart-setup).
- A basic understanding of the concepts covered in [Custom authentication extensions overview](custom-extension-overview).
- A Microsoft Entra ID tenant. You can use either a customer or workforce tenant for this how-to guide.
    - For external tenants, use a [sign-up and sign-in user flow](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers).

## Step 1: Register a custom authentication extension

You'll now configure a custom authentication extension, which will be used by Microsoft Entra ID to call your Azure function. The custom authentication extension contains information about your REST API endpoint, the claims that it parses from your REST API, and how to authenticate to your REST API. Follow these steps to register a custom authentication extension to your Azure Function app.

Note

You can have a maximum of 100 custom extension policies.

# [Azure portal](#tab/azure-portal)
### Register a custom authentication extension

1. Sign in to the [Azure portal](https://portal.azure.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-developer) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator).
2. Search for and select **Microsoft Entra ID** and select **Enterprise applications**.
3. Select **Custom authentication extensions**, and then select **Create a custom extension**.
4. In **Basics**, select the **TokenIssuanceStart** event type and select **Next**.
5. In **Endpoint Configuration**, fill in the following properties:
    - **Name** - A name for your custom authentication extension. For example, *Token issuance event*.
    - **Target Url** - The `{Function_Url}` of your Azure Function URL. Navigate to the **Overview** page of your Azure Function app, then select the function you created. In the function **Overview** page, select **Get Function Url** and use the copy icon to copy the **customauthenticationextension\_extension (System key)** URL.
    - **Description** - A description for your custom authentication extensions.
6. Select **Next**.
7. In **API Authentication**, select the **Create new app registration** option to create an app registration that represents your *function app*.
8. Give the app a name, for example **Azure Functions authentication events API**.
9. Select **Next**.
10. In **Claims**, enter the attributes that you expect your custom authentication extension to parse from your REST API and will be merged into the token. Add the following claims:
    - DateOfBirth
    - CustomRoles
    - ApiVersion
    - CorrelationId
11. Select **Next**, then **Create**, which registers the custom authentication extension and the associated application registration.
12. Note the **App ID** under **API Authentication**, which is needed to [configure authentication for your Azure Function](custom-extension-tokenissuancestart-setup#configure-authentication-for-your-azure-function) in your Azure Function app.

# [Microsoft Graph](#tab/microsoft-graph)
### Register an application

1. Sign in to [Graph Explorer](https://aka.ms/ge) using an account whose home tenant is the tenant in which you wish to manage your custom authentication extension in. This account must have privileges to create and manage an application registration in the tenant.
2. Run the following request.

    ```http
    POST https://graph.microsoft.com/v1.0/applications
    Content-type: application/json
    
    {
        "displayName": "authenticationeventsAPI"
    }
    ```
3. From the response, record the value of **id** and **appId** of the newly created app registration. These values are referenced in this article as `{authenticationeventsAPI_ObjectId}` and `{authenticationeventsAPI_AppId}` respectively.

### Create a service principal in the tenant for the authenticationeventsAPI app registration.

While in Graph Explorer, run the following request. Replace `{authenticationeventsAPI_AppId}` with the value of **appId** that you recorded from the previous step.

```http
POST https://graph.microsoft.com/v1.0/servicePrincipals
Content-type: application/json
    
{
    "appId": "{authenticationeventsAPI_AppId}"
}
```

### Set the App ID URI, access token version, and required resource access

Update the newly created application to set the application ID URI value, the access token version, and the required resource access.

In Graph Explorer, run the following request.

- Set the application ID URI value in the *identifierUris* property. Replace `{Function_Url_Hostname}` with the hostname of the `{Function_Url}` you recorded earlier.
- Set the `{authenticationeventsAPI_AppId}` value with the **appId** that you recorded earlier.
- An example value is `api://authenticationeventsAPI.azurewebsites.net/00001111-aaaa-2222-bbbb-3333cccc4444`. Take note of this value as you'll use it later in this article in place of `{functionApp_IdentifierUri}`.

```http
POST https://graph.microsoft.com/v1.0/applications/{authenticationeventsAPI_ObjectId}
Content-type: application/json

{
"identifierUris": [
    "api://{Function_Url_Hostname}/{authenticationeventsAPI_AppId}"
],    
"api": {
    "requestedAccessTokenVersion": 2,
    "acceptMappedClaims": null,
    "knownClientApplications": [],
    "oauth2PermissionScopes": [],
    "preAuthorizedApplications": []
},
"requiredResourceAccess": [
    {
        "resourceAppId": "00000003-0000-0000-c000-000000000000",
        "resourceAccess": [
            {
                "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
                "type": "Role"
            }
        ]
    }
]
}
```

### Register a custom authentication extension

To register the custom authentication extension, you associate it with the app registration for the Azure Function, and your Azure Function endpoint `{Function_Url}`.

1. In Graph Explorer, run the following request. Replace `{Function_Url}` with the hostname of your Azure Function app. Replace `{functionApp_IdentifierUri}` with the identifierUri used in the previous step.

    - You need the *CustomAuthenticationExtension.ReadWrite.All* delegated permission.

    ```http
    POST https://graph.microsoft.com/beta/identity/customAuthenticationExtensions
    Content-type: application/json
    
    {
        "@odata.type": "#microsoft.graph.onTokenIssuanceStartCustomExtension",
        "displayName": "onTokenIssuanceStartCustomExtension",
        "description": "Fetch additional claims from custom user store",
        "endpointConfiguration": {
            "@odata.type": "#microsoft.graph.httpRequestEndpoint",
            "targetUrl": "{Function_Url}"
        },
        "authenticationConfiguration": {
            "@odata.type": "#microsoft.graph.azureAdTokenAuthentication",
            "resourceId": "{functionApp_IdentifierUri}"
        },
        "claimsForTokenConfiguration": [
            {
                "claimIdInApiResponse": "DateOfBirth"
            },
            {
                "claimIdInApiResponse": "CustomRoles"
            }
        ]
    }
    ```
2. Record the `id` value of the created custom claims provider object. You'll use the value later in this tutorial in place of `{customExtensionObjectId}`.

---

### 1.2 Grant admin consent

Once the custom authentication extension is created, you need to grant permissions to the API. The custom authentication extension uses `client_credentials` to authenticate to the Azure Function App using the `Receive custom authentication extension HTTP requests` permission.

1. Open the **Overview** page of your new custom authentication extension. Take a note of the **App ID** under **API Authentication**, as it will be needed when adding an identity provider.
2. Under **API Authentication**, select **Grant permission**.
3. A new window opens, and once signed in, it requests permissions to receive custom authentication extension HTTP requests. This allows the custom authentication extension to authenticate to your API. Select **Accept**.

    [![Screenshot that shows how grant admin consent.](media/custom-extension-tokenissuancestart-configuration/custom-extensions-overview.png)](media/custom-extension-tokenissuancestart-configuration/custom-extensions-overview.png#lightbox)

## Step 2: Configure an OpenID Connect app to receive enriched tokens

To get a token and test the custom authentication extension, you can use the https://jwt.ms app. It's a Microsoft-owned web application that displays the decoded contents of a token (the contents of the token never leave your browser).

### 2.1 Register a test web application

Follow these steps to register the **jwt.ms** web application:

1. From the **Home** page in the Azure portal, select **Microsoft Entra ID**.
2. Select **App registrations** &gt; **New registration**.
3. Enter a **Name** for the application. For example, **My Test application**.
4. Under **Supported account types**, select **Accounts in this organizational directory only**.
5. In the **Select a platform** dropdown in **Redirect URI**, select **Web** and then enter `https://jwt.ms` in the URL text box.
6. Select **Register** to complete the app registration.

    ![Screenshot that shows how to select the supported account type and redirect URI.](media/custom-extension-tokenissuancestart-configuration/register-test-web-application.png)
7. In the **Overview** page of your app registration, copy the **Application (client) ID**. The app ID is referred to as the `{App_to_enrich_ID}` in later steps. In Microsoft Graph, it's referenced by the **appId** property.

    ![Screenshot that shows how to copy the application ID.](media/custom-extension-tokenissuancestart-configuration/get-the-test-application-id.png)

### 2.2 Enable implicit flow

The **jwt.ms** test application uses the implicit flow. Enable implicit flow in your *My Test application* registration:

Important

Microsoft recommends using the most secure authentication flow available. The authentication flow used for testing in this procedure requires a very high degree of trust in the application, and carries risks that are not present in other flows. This approach shouldn't be used for authenticating users to your production apps ([learn more](v2-oauth2-implicit-grant-flow)).

1. Under **Manage**, select **Authentication**.
2. Under **Implicit grant and hybrid flows**, select the **ID tokens (used for implicit and hybrid flows)** checkbox.
3. Select **Save**.

### 2.3 Enable your App for a claims mapping policy

A claims mapping policy is used to select which attributes returned from the custom authentication extension are mapped into the token. To allow tokens to be augmented, you must explicitly enable the application registration to accept mapped claims:

1. In your *My Test application* registration, under **Manage**, select **Manifest**.
2. In the manifest, locate the `acceptMappedClaims` attribute, and set the value to `true`.
3. Set the `requestedAccessTokenVersion` to `2`.
4. Select **Save** to save the changes.

The following JSON snippet demonstrates how to configure these properties.

```json
{"id": "22222222-0000-0000-0000-000000000000","acceptMappedClaims": true,"requestedAccessTokenVersion": 2,  
    ...
}
```

Warning

Do not set `acceptMappedClaims` property to `true` for multitenant apps, which can allow malicious actors to create claims-mapping policies for your app. Instead [configure a custom signing key](/en-us/graph/application-saml-sso-configure-api#option-2-create-a-custom-signing-certificate).

# [Workforce tenant](#tab/workforce-tenant)
Continue to the next step, Assign a custom claims provider to your app.

# [External tenant](#tab/external-tenant)
### 3.4 Associate your app with a user flow

For external tenants, you need to associate your app with a user flow. A user flow defines the authentication methods a customer can use to sign in to your application and the information they need to provide during sign-up. Ensure that you complete the steps in [Add an application to a user flow](../external-id/customers/how-to-user-flow-add-application) before continuing to add *My Test application* to the user flow.

---

## Step 3: Assign a custom claims provider to your app

For tokens to be issued with claims incoming from the custom authentication extension, you must assign a custom claims provider to your application. This is based on the token audience, so the provider must be assigned to the client application to receive claims in an ID token, and to the resource application to receive claims in an access token. The custom claims provider relies on the custom authentication extension configured with the **token issuance start** event listener. You can choose whether all, or a subset of claims, from the custom claims provider are mapped into the token.

Note

You can only create 250 unique assignments between applications and custom extensions. If you wish to apply the same custom extension call to multiple apps, we recommend using [authenticationEventListeners](/en-us/graph/api/identitycontainer-post-authenticationeventlisteners) Microsoft Graph API to create listeners for multiple applications. This is not supported in the Azure portal.

Follow these steps to connect the *My Test application* with your custom authentication extension:

# [Azure portal](#tab/azure-portal)
To assign the custom authentication extension as a custom claims provider source;

1. From the **Home** page in the Azure portal, select **Microsoft Entra ID**.
2. Select**Enterprise applications**, then under **Manage**, select **All applications**. Find and select *My Test application* from the list.
3. From the **Overview** page of *My Test application*, navigate to **Manage**, and select **Single sign-on**.
4. Under **Attributes & Claims**, select **Edit**.

    [![Screenshot that shows how to configure app claims.](media/custom-extension-tokenissuancestart-configuration/open-id-connect-based-sign-on.png)](media/custom-extension-tokenissuancestart-configuration/open-id-connect-based-sign-on.png#lightbox)
5. Expand the **Advanced settings** menu.
6. Next to **Custom claims provider**, select **Configure**.
7. Expand the **Custom claims provider** drop-down box, and select the *Token issuance event* you created earlier.
8. Select **Save**.

Next, assign the attributes from the custom claims provider, which should be issued into the token as claims:

1. Select **Add new claim** to add a new claim. Provide a name to the claim you want to be issued, for example *DateOfBirth*.
2. Under **Source**, select **Attribute**, and choose *customClaimsProvider.DateOfBirth* from the **Source attribute** drop-down box.

    [![Screenshot that shows how to add a claim mapping to your app.](media/custom-extension-tokenissuancestart-configuration/manage-claim.png)](media/custom-extension-tokenissuancestart-configuration/manage-claim.png#lightbox)
3. Select **Save**.
4. Repeat this process to add the *customClaimsProvider.customRoles*, *customClaimsProvider.apiVersion* and *customClaimsProvider.correlationId* attributes, and the corresponding name. It's a good idea to match the name of the claim to the name of the attribute.

# [Microsoft Graph](#tab/microsoft-graph)
First create an event listener to trigger a custom authentication extension for the *My Test application* using the token issuance start event.

1. Sign in to [Graph Explorer](https://aka.ms/ge) using an account whose home tenant is the tenant you wish to manage your custom authentication extension in.
2. Run the following request. Replace `{App_to_enrich_ID}` with the app ID of *My Test application* recorded earlier. Replace `{customExtensionObjectId}` with the custom authentication extension ID recorded earlier.

    - You need the *EventListener.ReadWrite.All* delegated permission.

    ```http
    POST https://graph.microsoft.com/beta/identity/authenticationEventListeners
    Content-type: application/json
    
    {
        "@odata.type": "#microsoft.graph.onTokenIssuanceStartListener",
        "conditions": {
            "applications": {
                "includeAllApplications": false,
                "includeApplications": [
                    {
                        "appId": "{App_to_enrich_ID}"
                    }
                ]
            }
        },
        "priority": 500,
        "handler": {
            "@odata.type": "#microsoft.graph.onTokenIssuanceStartCustomExtensionHandler",
            "customExtension": {
                "id": "{customExtensionObjectId}"
            }
        }
    }
    ```

Next, create the claims mapping policy, which describes which claims can be issued to an application from a custom claims provider.

1. Still in Graph Explorer, run the following request. You'll need the *Policy.ReadWrite.ApplicationConfiguration* delegated permission.

    ```http
    POST https://graph.microsoft.com/v1.0/policies/claimsMappingPolicies
    Content-type: application/json
    
    {
        "definition": [
            "{\"ClaimsMappingPolicy\":{\"Version\":1,\"IncludeBasicClaimSet\":\"true\",\"ClaimsSchema\":[{\"Source\":\"CustomClaimsProvider\",\"ID\":\"DateOfBirth\",\"JwtClaimType\":\"dob\"},{\"Source\":\"CustomClaimsProvider\",\"ID\":\"CustomRoles\",\"JwtClaimType\":\"my_roles\"},{\"Source\":\"CustomClaimsProvider\",\"ID\":\"CorrelationId\",\"JwtClaimType\":\"correlationId\"},{\"Source\":\"CustomClaimsProvider\",\"ID\":\"ApiVersion\",\"JwtClaimType\":\"apiVersion \"},{\"Value\":\"tokenaug_V2\",\"JwtClaimType\":\"policy_version\"}]}}"
        ],
        "displayName": "MyClaimsMappingPolicy",
        "isOrganizationDefault": false
    }
    ```
2. Record the `ID` generated in the response, later it's referred to as `{claims_mapping_policy_ID}`.

Get the service principal object ID:

1. Run the following request in Graph Explorer. Replace `{App_to_enrich_ID}` with the **appId** of *My Test Application*.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals(appId='{App_to_enrich_ID}')
    ```

Record the value of **id**.

Assign the claims mapping policy to the service principal of *My Test Application*.

1. Run the following request in Graph Explorer. You'll need the *Policy.ReadWrite.ApplicationConfiguration* and *Application.ReadWrite.All* delegated permission.

    ```http
    POST https://graph.microsoft.com/v1.0/servicePrincipals/{test_App_Service_Principal_ObjectId}/claimsMappingPolicies/$ref
    Content-type: application/json
    
    {
        "@odata.id": "https://graph.microsoft.com/v1.0/policies/claimsMappingPolicies/{claims_mapping_policy_ID}"
    }
    ```

---

## Step 4: Protect your Azure Function

Microsoft Entra custom authentication extension uses server to server flow to obtain an access token that is sent in the HTTP `Authorization` header to your Azure function. When publishing your function to Azure, especially in a production environment, you need to validate the token sent in the authorization header.

To protect your Azure function, follow these steps to integrate Microsoft Entra authentication, for validating incoming tokens with your *Azure Functions authentication events API* application registration. Choose one of the following tabs based on your tenant type.

Note

If the Azure function app is hosted in a different Azure tenant than the tenant in which your custom authentication extension is registered, choose the Open ID Connect tab.

### 4.1 Using Microsoft Entra identity provider

Use the following steps to add Microsoft Entra as an identity provider to your Azure Function app.

# [Workforce tenant](#tab/workforce-tenant)
1. In the [Azure portal](https://portal.azure.com), find and select the function app you previously published.
2. Under **Settings**, select **Authentication**.
3. Select **Add Identity provider**.
4. Select **Microsoft** as the identity provider.
5. Select **Workforce** as the tenant type.
6. Under **App registration** select **Pick an existing app registration in this directory** for the **App registration type**, and pick the *Azure Functions authentication events API* app registration you previously created when registering the custom claims provider.
7. Enter the following issuer URL, `https://login.microsoftonline.com/{tenantId}/v2.0`, where `{tenantId}` is the tenant ID of your workforce tenant.
8. Under **Client application requirement**, select **Allow requests from specific client applications** and enter `99045fe1-7639-4a75-9d4a-577b6ca3810f`.
9. Under **Tenant requirement**, select **Allow requests from specific tenants** and enter your workforce tenant ID.
10. Under **Unauthenticated requests**, select **HTTP 401 Unauthorized** as the identity provider.
11. Unselect the **Token store** option.
12. Select **Add** to add authentication to your Azure Function.

    [![Screenshot that shows how to add authentication to your function app while in a workforce tenant.](media/custom-extension-tokenissuancestart-configuration/add-identity-provider-auth-function-app-workforce.png)](media/custom-extension-tokenissuancestart-configuration/add-identity-provider-auth-function-app-workforce.png#lightbox)

# [External tenant](#tab/external-tenant)
1. In the [Azure portal](https://portal.azure.com), find and select the function app you previously published.
2. Under **Settings**, select **Authentication**.
3. Select **Add Identity provider**.
4. Select **Microsoft** as the identity provider.
5. Select **External configuration** as the tenant type.
6. Under **App registration**, select **Provide the details of an existing app registration** for the **App registration type**, and enter the `client_id` of the *Azure Functions authentication events API* app registration you previously created when registering the custom claims provider.
7. For the **Issuer URL**, enter the following URL `https://{domainName}.ciamlogin.com/{tenant_id}/v2.0`, where

    - `{domainName}` is the domain name of your external tenant, in the form `{domainName}.contoso.com`.
    - `{tenantId}` is the tenant ID of your external tenant.
8. Under **Client application requirement**, select **Allow requests from specific client applications** and enter `99045fe1-7639-4a75-9d4a-577b6ca3810f`.
9. Under **Tenant requirement**, select **Allow requests from specific tenants** and enter your external tenant ID.
10. Under **Unauthenticated requests**, select **HTTP 401 Unauthorized** as the identity provider.
11. Unselect the **Token store** option.
12. Select **Add** to add authentication to your Azure Function.

    [![Screenshot that shows how to add authentication to your function app while in an external tenant.](media/custom-extension-tokenissuancestart-configuration/add-identity-provider-auth-function-app-customer.png)](media/custom-extension-tokenissuancestart-configuration/add-identity-provider-auth-function-app-customer.png#lightbox)

---

### 4.2 Using OpenID Connect identity provider

If you configured the Microsoft identity provider, skip this step. Otherwise, if the Azure Function is hosted under a different tenant than the tenant in which your custom authentication extension is registered, follow these steps to protect your function:

#### Create a client secret

1. From the **Home** page of the Azure portal, select **Microsoft Entra ID** &gt; **App registrations**.
2. Select the *Azure Functions authentication events API* app registration you created previously.
3. Select **Certificates & secrets** &gt; **Client secrets** &gt; **New client secret**.
4. Select an expiration for the secret or specify a custom lifetime, add a description, and select **Add**.
5. Record the **secret's value** for use in your client application code. This secret value is never displayed again after you leave this page.

#### Add the OpenID Connect identity provider to your Azure Function app.

1. Find and select the function app you previously published.
2. Under **Settings**, select **Authentication**.
3. Select **Add Identity provider**.
4. Select **OpenID Connect** as the identity provider.
5. Provide a name, such as *Contoso Microsoft Entra ID*.
6. Under the **Metadata entry**, enter the following URL to the **Document URL**. Replace the `{tenantId}` with your Microsoft Entra tenant ID.

    ```http
    https://login.microsoftonline.com/{tenantId}/v2.0/.well-known/openid-configuration
    ```
7. Under the **App registration**, enter the application ID (client ID) of the *Azure Functions authentication events API* app registration you created previously.
8. Return to the Azure Function, under the **App registration**, enter the **Client secret**.
9. Unselect the **Token store** option.
10. Select **Add** to add the OpenID Connect identity provider.

## Step 5: Test the application

To test your custom claims provider, follow these steps:

# [Workforce tenant](#tab/workforce-tenant)
1. Open a new private browser and navigate and sign-in through the following URL.

    ```http
    https://login.microsoftonline.com/{tenantId}/oauth2/v2.0/authorize?client_id={App_to_enrich_ID}&response_type=id_token&redirect_uri=https://jwt.ms&scope=openid&state=12345&nonce=12345
    ```
2. Replace `{tenantId}` with your tenant ID, tenant name, or one of your verified domain names. For example, `contoso.onmicrosoft.com`.
3. Replace `{App_to_enrich_ID}` with the *My Test application* client ID.
4. After logging in, you'll be presented with your decoded token at `https://jwt.ms`. Validate that the claims from the Azure Function are presented in the decoded token, for example, `DateOfBirth`.

# [External tenant](#tab/external-tenant)
1. Open a new private browser and navigate and sign-in through the following URL.

    ```http
    https://{domainName}.ciamlogin.com/{tenantId}/oauth2/v2.0/authorize?client_id={App_to_enrich_ID}&response_type=id_token&redirect_uri=https://jwt.ms&scope=openid&state=12345&nonce=12345
    ```
2. Replace `{domainName}` with your domain name, for example, `contoso`.
3. Replace `{tenantId}` with your tenant ID, tenant name, or one of your verified domain names. For example, `contoso.onmicrosoft.com`.
4. Replace `{App_to_enrich_ID}` with the *My Test application* client ID.
5. Go through the sign in user flow that you've configured, and accept the requested permissions.
6. After logging in, you'll be presented with your decoded token at `https://jwt.ms`. Validate that the claims from the Azure Function are presented in the decoded token, for example, `DateOfBirth`.

---