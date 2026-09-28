---
layout: Conceptual
title: Create a custom authentication extension for account recovery claim validation - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-custom-authentication-extension-account-recovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to set up a custom authentication extension that validates Verified ID claims during Microsoft Entra account recovery using an Azure Function and REST API.
ms.date: 2026-04-22T00:00:00.0000000Z
ms.reviewer: rohulati
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: 985e7c12-6b38-c743-730f-0d91ee4725e7
document_version_independent_id: 985e7c12-6b38-c743-730f-0d91ee4725e7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-custom-authentication-extension-account-recovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-custom-authentication-extension-account-recovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-custom-authentication-extension-account-recovery.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: ed419f3c-189b-5bd5-6157-489d8a6a718b
---

# Create a custom authentication extension for account recovery claim validation - Microsoft identity platform | Microsoft Learn

This article describes how to set up a custom authentication extension that validates Verified ID claims during Microsoft Entra account recovery. In the account recovery flow, event listeners can be used to extend the claim validation process:

- The **OnVerifiedIdClaimValidation** event occurs when a user initiates account recovery and presents Verified ID claims. You can add actions such as validating claims against an authoritative data source (such as an HR system, application database, or any employee records system) and returning a pass or fail decision.

In addition to creating a custom authentication extension, you need to create a REST API that defines the workflow actions to take for the event. This article demonstrates a quick way to get started using a C# Azure Function deployed from a sample repository. With Azure Functions, you run your code in a serverless environment without having to first create a virtual machine (VM) or publish a web application.

## Prerequisites

- An Azure subscription. If you don't have an existing Azure account, sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra ID tenant with [account recovery enabled](../identity/authentication/how-to-account-recovery-enable).
- At least the [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator) roles.

## How it works

During account recovery, a user who has lost all authentication methods must re-establish their identity. The custom authentication extension adds a claim validation step into this flow:

[![Architecture diagram showing the account recovery flow: user starts recovery, Microsoft Entra ID triggers event listener, custom authentication extension calls REST API endpoint (Logic Apps or Azure Functions), which validates against external system, then response is processed and TAP code is presented.](media/custom-extension-account-recovery/account-recovery-flow.png)](media/custom-extension-account-recovery/account-recovery-flow.png#lightbox)

The `OnVerifiedIdClaimValidation` event is the pre-proofing hook in the recovery pipeline. It lets you plug in custom validation logic — HR lookups, external database checks, or partner trust verification — before Microsoft Entra ID proceeds with recovery.

## Step 1: Create a custom authentication extensions REST API (Azure Function app)

In this step, you deploy an Azure Function app that serves as the REST API for your custom authentication extension. The function receives Verified ID claims from Microsoft Entra ID during account recovery and validates them against an authoritative data source.

The sample function is available as a one-click deployment. It deploys an Azure Function App (.NET 10, isolated worker model) on the Consumption plan with Application Insights and a storage account.

### 1.1 Deploy the Azure Function

1. Select the **Deploy to Azure** button:
2. Fill in the deployment parameters:

    | Parameter | Description |
    | --- | --- |
    | **Function App Name** | A globally unique name for the Function App (for example, `contoso-recovery-claims`). |
    | **Repo URL** | Pre-filled with the GitHub repository URL. |
    | **Branch** | `main` |
    | **Storage Account Type** | `Standard_LRS` (default). |
    | **Location** | Select an Azure region close to your users. |

    Leave the optional parameters blank for now — you configure them in the next steps.
3. Select **Review + create**, then **Create**.
4. Wait for the deployment to finish (typically 2–3 minutes).

Note

The ARM template deploys the Function App on the **Consumption plan** (Y1/Dynamic tier). Scaling is fully automatic — Azure adds and removes instances based on incoming request volume. For testing or development, you might want to switch to the **Premium plan** (EP1 or higher) to avoid cold starts. To change plans, go to your Function App &gt; **App Service plan** &gt; **Change App Service plan** &gt; select or create a plan with the desired tier.

### 1.2 Get the function URL

1. Once deployed, go to the Function App resource.
2. Select **Functions** &gt; **CustomClaimMatching** &gt; **Get Function URL**.
3. Copy the URL. It looks like: `https://<your-function-app>.azurewebsites.net/api/CustomClaimMatching`

### 1.3 Configure the test data source

For testing, the function supports an Excel file hosted on any web server with read access as a data source. In production, you can switch to the HR API provider (see Switch to production: use the HR API provider).

1. Download the sample Excel file from the [SampleData folder](https://github.com/Azure-Samples/active-directory-verifiable-credentials-dotnet/tree/main/7-AccountRecovery-ClaimsMatching/SampleData) in the repo, or create your own with these columns:

    | EmployeeId | UPN | firstName | lastName | fullName | dateOfBirth | documentType | documentId | documentExpiryDate |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | E001 | user@contoso.com | John | Doe | John Doe | 1990-01-15 | Passport | AB123456 | 2028-01-15 |

    Tip

    To add a new claim, add a column with the claim name as the header. The function matches claim keys from the request against column headers dynamically — no code changes required.

    Note

    By default, the function app only validates the **document number** (`documentId`) claim. To match additional claims such as `firstName`, `dateOfBirth`, or `employeeId`, update the validation logic in the Azure Function code.
2. Upload the file to a web server, file share, or cloud storage service (for example, Azure Blob Storage, SharePoint, or any HTTP-accessible location).
3. Get a direct download URL for the file. The URL must be accessible without interactive sign-in.
4. In the Azure portal, go to your Function App &gt; **Settings** &gt; **Environment variables**. The deployment template pre-creates these variables with default values. Verify and update the following:

    | Name | Action | Value |
    | --- | --- | --- |
    | `ClaimsValidator__Provider` | **Verify** (pre-created as `excel`) | `excel` |
    | `Excel__ShareUrl` | **Update** (pre-created but empty) | The direct download URL for your Excel file. |
    | `Excel__SheetName` | **Verify** (pre-created as `Sheet1`) | `Sheet1` (or your worksheet name). |
5. Select **Apply**, then **Confirm**.

## Step 2: Create and register a custom authentication extension

In this step, you register a custom authentication extension that Microsoft Entra ID uses to call your Azure Function. The custom authentication extension contains information about your REST API endpoint, the claim validation action that it parses from your REST API, and how to authenticate to your REST API.

Note

You can have a maximum of 100 custom extension policies. However, only **one** custom authentication extension per tenant is allowed for the **OnVerifiedIdClaimValidation** event type.

# [Azure portal](#tab/azure-portal)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Custom authentication extensions**.
3. Select **Create a custom extension**.
4. In **Basics**, select the **OnVerifiedIdClaimValidation** event, and then select **Next**.
5. In **Endpoint Configuration**, fill in the following properties:

    - **Name:** A name for your custom authentication extension. For example, `Account Recovery Claims Validation`.
    - **Target URL:** The function URL of your Azure Function. For example: `https://<your-function-app>.azurewebsites.net/api/CustomClaimMatching`
    - **Description:** A description for the extension. For example, `Validates VID claims against HR data during account recovery`.
6. Select **Next**.
7. In **API Authentication**, select the **Create new app registration** option to create an app registration that represents your function app.
8. Give the app a name, for example `Azure Functions authentication events API`.
9. Select **Next**.
10. Select **Create**, which creates the custom authentication extension and the associated application registration.

# [Microsoft Graph](#tab/microsoft-graph)
### Register an application

1. Sign in to [Graph Explorer](https://aka.ms/ge) using an account whose home tenant is the tenant you want to manage your custom authentication extension in. The account must have privileges to create and manage an application registration in the tenant.
2. Run the following request.

    ```http
    POST https://graph.microsoft.com/v1.0/applications
    Content-type: application/json
    
    {
        "displayName": "authenticationeventsAPI"
    }
    ```
3. From the response, record the values of **id** and **appId**. These values are referenced later in this article as `{authenticationeventsAPI_ObjectId}` and `{authenticationeventsAPI_AppId}` respectively.

### Create a service principal for the authenticationeventsAPI app registration

While in Graph Explorer, run the following request. Replace `{authenticationeventsAPI_AppId}` with the **appId** value you recorded from the previous step.

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

- Set the application ID URI value in the `identifierUris` property. Replace `{Function_Url_Hostname}` with the hostname of your Azure Function URL (for example, `contoso-recovery-claims.azurewebsites.net`).
- Replace `{authenticationeventsAPI_AppId}` with the **appId** you recorded earlier.
- Replace `{authenticationeventsAPI_ObjectId}` with the **id** you recorded earlier.

An example `identifierUris` value is `api://contoso-recovery-claims.azurewebsites.net/aaaabbbb-0000-cccc-1111-dddd2222eeee`. Take note of this value as you use it later in this article in place of `{functionApp_IdentifierUri}`.

```http
PATCH https://graph.microsoft.com/v1.0/applications/{authenticationeventsAPI_ObjectId}
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
                    "id": "214e810f-fda8-4fd7-a475-29461495eb00",
                    "type": "Role"
                }
            ]
        }
    ]
}
```

### Register the custom authentication extension

Next, register the custom authentication extension. You associate it with the app registration for the Azure Function, and your Azure Function endpoint `{Function_Url}`.

1. In Graph Explorer, run the following request. Replace `{Function_Url}` with the URL of your Azure Function app (for example, `https://contoso-recovery-claims.azurewebsites.net/api/CustomClaimMatching`). Replace `{functionApp_IdentifierUri}` with the `identifierUris` value set in the previous step.

    - You need the `CustomAuthenticationExtension.ReadWrite.All` delegated permission.

    ```http
    POST https://graph.microsoft.com/v1.0/identity/customAuthenticationExtensions
    Content-type: application/json
    
    {
        "@odata.type": "#microsoft.graph.onVerifiedIdClaimValidationCustomExtension",
        "displayName": "Account Recovery Claims Validation",
        "description": "Validates VID claims against HR data during account recovery",
        "endpointConfiguration": {
            "@odata.type": "#microsoft.graph.httpRequestEndpoint",
            "targetUrl": "{Function_Url}"
        },
        "authenticationConfiguration": {
            "@odata.type": "#microsoft.graph.azureAdTokenAuthentication",
            "resourceId": "{functionApp_IdentifierUri}"
        },
        "clientConfiguration": {
            "timeoutInMilliseconds": 2000,
            "maximumRetries": 1
        }
    }
    ```
2. Record the **id** value of the created custom authentication extension. You use it later in this article as `{customExtensionObjectId}`.

---

### 2.1 Grant admin consent

After your custom authentication extension is created, grant application consent to the registered app, which allows the custom authentication extension to authenticate to your API.

1. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Custom authentication extensions**.
2. Select your custom authentication extension from the list.
3. On the **Overview** tab, select the **Grant permission** button to give admin consent to the registered app. The custom authentication extension uses `client_credentials` to authenticate to the Azure Function App using the `Receive custom authentication extension HTTP requests` permission. Select **Accept**.

## Step 3: Add the custom authentication extension to the account recovery policy

Now you associate the custom authentication extension with the identity verification profile's account validation settings so it's invoked during the recovery flow.

# [Azure portal](#tab/azure-portal)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator).
2. Browse to **Entra ID** &gt; **Account Recovery** &gt; **Identity verification profiles**.
3. Select the identity verification profile you want to update (or create a new one).
4. On the **Account validation** step, under **Additional claim validations**, toggle **Enable** to **On**.
5. In the **Selected extension** dropdown, select the custom authentication extension you created in Step 2 (`Account Recovery Claims Validation`).

    [![Screenshot showing the identity verification profile with the custom authentication extension selected.](media/custom-extension-account-recovery/account-recovery-identity-verification-profile.png)](media/custom-extension-account-recovery/account-recovery-identity-verification-profile.png#lightbox)
6. Select **Review and finalize**, then **Save**.

# [Microsoft Graph](#tab/microsoft-graph)
Create an authentication event listener to bind the custom authentication extension to the account recovery flow.

1. Sign in to [Graph Explorer](https://aka.ms/ge) using an account whose home tenant is the tenant you want to manage your custom authentication extension in.
2. Run the following request. Replace `{customExtensionObjectId}` with the **id** of the custom authentication extension you recorded in Step 2.

    - You need the `EventListener.ReadWrite.All` delegated permission.

    ```http
    POST https://graph.microsoft.com/v1.0/identity/authenticationEventListeners
    Content-type: application/json
    
    {
        "@odata.type": "#microsoft.graph.onVerifiedIdClaimValidationListener",
        "handler": {
            "@odata.type": "#microsoft.graph.onVerifiedIdClaimValidationCustomExtensionHandler",
            "customExtension": {
                "id": "{customExtensionObjectId}"
            }
        }
    }
    ```
3. Record the **id** value from the response. This is the `{eventListenerId}` for the account recovery event listener.

---

## Step 4: Test the function (before adding authentication)

Before configuring authentication (Step 5), verify the function's claims matching logic works by calling it directly. At this point, the function should have no authentication configured — no EasyAuth identity provider and `EntraId__TenantId` / `EntraId__ClientId` environment variables should be empty.

### 4.1 Test the function directly

Warning

This step tests the function with no authentication configured. This is for development and testing only. Don't expose your function without authentication in production. Complete Step 5 to configure authentication before deploying to production.

Note

Even with no authentication identity provider configured, Azure Functions still requires an `Authorization: Bearer` header. You can pass any value (for example, `Bearer test`) during local testing. In production, Microsoft Entra ID provides a valid token automatically.

1. Open a terminal and run:

    ```powershell
    $body = @'
    {
        "type": "microsoft.graph.authenticationEvent.verifiedIdClaimValidation",
        "source": "/tenants/<tenant-guid>/applications/<app-id>",
        "data": {
            "@odata.type": "microsoft.graph.onVerifiedIdClaimValidationCalloutData",
            "tenantId": "<tenant-guid>",
            "authenticationContext": {
                "correlationId": "00000000-0000-0000-0000-000000000001",
                "user": {
                    "userPrincipalName": "user@contoso.com"
                }
            },
            "verifiedIdClaimsContext": {
                "additionalInfo": {
                    "employeeId": "E001"
                },
                "claims": {
                    "firstName": "John",
                    "lastName": "Doe",
                    "dateOfBirth": "1990-01-15"
                }
            }
        }
    }
    '@
    
    (Invoke-WebRequest -Method Post `
      -Uri "https://<your-function-app>.azurewebsites.net/api/CustomClaimMatching" `
      -ContentType "application/json" `
      -Headers @{ Authorization = "Bearer test" } `
      -Body $body).Content
    ```
2. Verify the response:

    **Successful match:**

    ```json
    {
        "data": {
            "@odata.type": "microsoft.graph.onVerifiedIdClaimValidationResponseData",
            "actions": [
                {
                    "@odata.type": "microsoft.graph.verifiedIdClaimValidation.pass"
                }
            ]
        }
    }
    ```

    **Failed match** (returns which claims didn't match):

    ```json
    {
        "data": {
            "@odata.type": "microsoft.graph.onVerifiedIdClaimValidationResponseData",
            "actions": [
                {
                    "@odata.type": "microsoft.graph.verifiedIdClaimValidation.failed",
                    "failedClaims": ["dateOfBirth"]
                }
            ]
        }
    }
    ```

## Step 5: Protect your Azure Function

Microsoft Entra custom authentication extensions use server-to-server flow to obtain an access token that is sent in the HTTP `Authorization` header to your Azure Function. When publishing your function to Azure, especially in a production environment, you need to validate the token sent in the authorization header.

To protect your Azure Function, follow these steps to integrate Microsoft Entra authentication for validating incoming tokens with your *Azure Functions authentication events API* application registration.

### 5.1 Add an identity provider to your Azure Function

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to and select the Function App you previously deployed.
3. Select **Authentication** in the menu on the left.
4. Select **Add Identity provider**.
5. Select **Microsoft** as the identity provider.
6. Under **Choose a tenant**, select **Workforce configuration (current tenant)**.
7. Under **App registration**, select **Pick an existing app registration in this directory** and select the *Azure Functions authentication events API* app registration created in Step 2.
8. Under **Client secret expiration**, select an expiration period.
9. Under **Supported account types**, select **Current tenant - Single tenant**.
10. Under **Additional checks**:
    - **Client application requirement:** Select **Allow requests from specific client applications** and add `99045fe1-7639-4a75-9d4a-577b6ca3810f` (this is the Microsoft Entra custom authentication extensions first-party app ID).
    - **Identity requirement:** Select **Allow requests from any identity**.
    - **Tenant requirement:** Select **Allow requests from specific tenants** and enter your workforce tenant ID.
11. Under **Unauthenticated requests**, select **HTTP 401 Unauthorized: recommended for APIs**.
12. For the **Issuer URL**, enter `https://login.microsoftonline.com/{tenantId}/v2.0`, where `{tenantId}` is the tenant ID of your Microsoft Entra tenant.
13. Unselect the **Token store** option.
14. Select **Add** to add authentication to your Azure Function.

### 5.2 Use OpenID Connect identity provider

If the Azure Function is hosted in a different tenant than the tenant where your custom authentication extension is registered, follow these steps instead:

1. Sign in to the [Azure portal](https://portal.azure.com), then navigate to the Function App.
2. Select **Authentication** in the menu on the left.
3. Select **Add Identity provider**.
4. Select **OpenID Connect** as the identity provider.
5. Provide a name, such as `Contoso Microsoft Entra ID`.
6. Under the **Metadata entry**, enter the following URL to the **Document URL**, replacing `{tenantId}` with your Microsoft Entra tenant ID: 

    ```
    https://login.microsoftonline.com/{tenantId}/v2.0/.well-known/openid-configuration
    ```
7. Under **App registration**, enter the application ID (client ID) of the *Azure Functions authentication events API* app registration created in Step 2.
8. In the Microsoft Entra admin center, go to the *Azure Functions authentication events API* app registration &gt; **Certificates & secrets** &gt; **Client secrets** &gt; **New client secret**. Copy the secret value.
9. Back in the Azure Function, enter the **Client secret**.
10. Unselect the **Token store** option.
11. Select **Add** to add the OpenID Connect identity provider.

## Step 6: Test the end-to-end recovery flow

1. Sign in to the Microsoft Entra admin center and confirm the custom authentication extension is active and assigned to the identity verification profile (Step 3).
2. In a private browser window, go to https://myaccount.microsoft.com and initiate an account recovery.
3. Complete the identity proofing steps (face check, Verified ID presentation).
4. The `OnVerifiedIdClaimValidation` event fires and calls your Azure Function. The function validates the claims against your data source and returns pass or fail.
5. Verify in **Application Insights** &gt; **Logs** that the function was called and the claims were validated:

    ```kusto
    traces
    | where message has "claims" or message has "validation"
    | order by timestamp desc
    | take 20
    ```

## Switch to production: use the HR API provider

For production, switch from the Excel provider to the HR API provider, which calls your organization's HR REST endpoint.

1. In the Function App's **Environment variables**, update:

    | Name | Value |
    | --- | --- |
    | `ClaimsValidator__Provider` | `hrapi` |
    | `HrApi__BaseUrl` | Your HR API base URL (for example, `https://hr.contoso.com/api`). |
    | `HrApi__AuthMode` | `apikey` or `oauth`. |
    | `HrApi__ApiKey` | Your API key (if using `apikey` auth mode). |
    | `HrApi__OAuthScope` | OAuth scope (if using `oauth` auth mode, for example, `api://hr-api-app-id/.default`). |
2. When using `oauth` auth mode, the function uses the Function App's system-assigned managed identity. Grant the managed identity the appropriate app role on your HR API's app registration.
3. Your HR API must implement this contract:

    **Request:**`POST {BaseUrl}/validate`

    ```json
    {
        "upn": "user@contoso.com",
        "employeeId": "E001",
        "claims": {
            "firstName": "John",
            "lastName": "Doe",
            "dateOfBirth": "1990-01-15"
        }
    }
    ```

    **Response (pass):**

    ```json
    {
        "result": "pass"
    }
    ```

    **Response (fail):**

    ```json
    {
        "result": "fail",
        "failedClaims": ["dateOfBirth"]
    }
    ```

## Troubleshoot

| Symptom | Cause | Resolution |
| --- | --- | --- |
| Function returns `401` | Bearer token validation failed or identity provider not configured. | Verify the identity provider is added in Function App Authentication (Step 5), and the client ID matches the app registration. |
| Function returns `200` but recovery flow fails | Response schema mismatch. | Check the function returns the correct `@odata.type` values in the response. |
| Claims always fail validation | Data source doesn't match. | Verify the Excel column headers or HR API response match the claim keys exactly (case-insensitive). |
| Function not called during recovery | Event listener not configured. | Confirm the custom authentication extension is assigned to the account recovery policy (Step 3). |
| Excel data not loading | Share URL invalid or expired. | Re-share the Excel file and update `Excel__ShareUrl` in Environment variables. |
| Admin consent not granted | Permission error on extension call. | Go to the custom authentication extension &gt; **Overview** &gt; **Grant permission** &gt; **Accept**. |

For more troubleshooting guidance, see [Troubleshoot your custom authentication extensions API](custom-extension-troubleshoot).