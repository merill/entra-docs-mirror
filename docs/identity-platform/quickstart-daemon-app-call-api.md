---
layout: Conceptual
title: Quickstart - Call a web API in a sample daemon app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-daemon-app-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: A daemon app code sample quickstart that shows how to acquire an access token to call a protected web API by using Microsoft identity platform
manager: dougeby
ms.topic: quickstart
ms.date: 2024-11-20T00:00:00.0000000Z
zone_pivot_groups: entra-tenants
locale: en-us
document_id: e0622245-a028-3c5f-a551-d8136da96e56
document_version_independent_id: e0622245-a028-3c5f-a551-d8136da96e56
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-daemon-app-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-daemon-app-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-daemon-app-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: bb68a0f4-b056-4eb8-fbbc-5c378bb81410
---

# Quickstart - Call a web API in a sample daemon app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this quickstart, you use a sample daemon application to acquire an access token and call a protected web API by using the [Microsoft Authentication Library (MSAL)](msal-overview).

Before you begin, use the **Choose a tenant type** selector at the top of this page to select tenant type. Microsoft Entra ID provides two tenant configurations, [workforce](../external-id/tenant-configurations#workforce-tenants) and [external](../external-id/tenant-configurations#external-tenants). A workforce tenant configuration is for your employees, internal apps, and other organizational resources. An external tenant is for your customer-facing apps.

::: zone pivot="workforce"

The sample app you use in this quickstart acquires an access token to call Microsoft Graph API.

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- This Azure account must have permissions to manage applications. Any of the following Microsoft Entra roles include the required permissions:
    - Application Administrator
    - Application Developer
    - Cloud Application Administrator
- A workforce tenant. You can use your Default Directory or [set up a new tenant](quickstart-create-new-tenant).
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add a client secret to your app registration. **Do not** use client secrets in production apps. Use certificates or federated credentials instead. For more information, see [add credentials to your application](how-to-add-credentials?tabs=client-secret).

# [.NET](#tab/asp-dot-net-core-workforce)
- A minimum requirement of [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet).
- [Visual Studio 2022](https://visualstudio.microsoft.com/vs/) or [Visual Studio Code](https://code.visualstudio.com/).

# [Node](#tab/node-workforce)
- [Node.js](https://nodejs.org/en/download/package-manager).
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.

# [Python](#tab/python-workforce)
- [Python 3+](https://www.python.org/downloads/release/python-364/).
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.

# [Java](#tab/java-workforce)
- [Java Development Kit (JDK)](https://openjdk.java.net/) 8 or later.
- [Maven](https://maven.apache.org/).
- A suitable code editor.

---

## Grant API permissions to the daemon app

For daemon app to access data in Microsoft Graph API, you grant it the permissions it needs. The daemon app needs application type permissions. Users can't interact with a daemon application, so the tenant administrator must consent to these permissions. Use the following steps to grant and consent to the permissions:

# [.NET](#tab/asp-dot-net-core-workforce)
For the .NET daemon app, you don't need to grant and consent to any permission. This daemon app reads its own app registration information, so it can do so without being granted any application permissions.

# [Node](#tab/node-workforce)
1. From the **App registrations** page, select the application that you created, such as *ciam-client-app*.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Under **Microsoft APIs** tab, select the **Microsoft Graph &gt;&gt; Application permissions**. We select the **Application permissions** option as the app signs in as itself, but not on behalf of a user.
5. In the **Select permissions** list, search for then select **User.Read.All**. We grant this permission so the app wants can read all users' full profiles.
6. Select the **Add permissions** button.
7. At this point, you've assigned the permissions correctly. However, since the daemon app doesn't allow users to interact with it, the users themselves can't consent to these permissions. You as the tenant administrator must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both permissions.

# [Python](#tab/python-workforce)
1. From the **App registrations** page, select the application that you created, such as *ciam-client-app*.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Under **Microsoft APIs** tab, select the **Microsoft Graph &gt;&gt; Application permissions**. We select the **Application permissions** option as the app signs in as itself, but not on behalf of a user.
5. In the **Select permissions** list, search for then select **User.Read.All**. We grant this permission so the app wants can read all users' full profiles.
6. Select the **Add permissions** button.
7. At this point, you've assigned the permissions correctly. However, since the daemon app doesn't allow users to interact with it, the users themselves can't consent to these permissions. You as the tenant administrator must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both permissions.

# [Java](#tab/java-workforce)
1. From the **App registrations** page, select the application that you created, such as *ciam-client-app*.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Under **Microsoft APIs** tab, select the **Microsoft Graph &gt;&gt; Application permissions**. We select the **Application permissions** option as the app signs in as itself, but not on behalf of a user.
5. In the **Select permissions** list, search for then select **User.Read.All**. We grant this permission so the app wants can read all users' full profiles.
6. Select the **Add permissions** button.
7. At this point, you've assigned the permissions correctly. However, since the daemon app doesn't allow users to interact with it, the users themselves can't consent to these permissions. You as the tenant administrator must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both permissions.

---

## Clone or download the sample application

To obtain the sample application, you can either clone it from GitHub or download it as a *.zip* file.

- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

# [.NET](#tab/asp-dot-net-core-workforce)
```console
git clone https://github.com/Azure-Samples/ms-identity-docs-code-dotnet.git
```

- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-docs-code-dotnet/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

# [Node](#tab/node-workforce)
```console
git clone https://github.com/azure-samples/ms-identity-javascript-nodejs-console.git 
```

- [Download the .zip file](https://github.com/azure-samples/ms-identity-javascript-nodejs-console/archive/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

# [Python](#tab/python-workforce)
```console
git clone https://github.com/Azure-Samples/ms-identity-python-daemon.git 
```

- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-python-daemon/archive/master.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

# [Java](#tab/java-workforce)
```console
git clone https://github.com/Azure-Samples/ms-identity-java-daemon.git
```

- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-java-daemon/archive/master.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

---

## Configure the project

To use your app registration details in the client daemon app sample, use the following steps:

# [.NET](#tab/asp-dot-net-core-workforce)
1. Open a console window then navigate to the *ms-identity-docs-code-dotnet/console-daemon* directory:

    ```console
    cd ms-identity-docs-code-dotnet/console-daemon
    ```
2. Open *Program.cs* and replace the file contents with the following snippet;

    ```csharp
     // Full directory URL, in the form of https://login.microsoftonline.com/<tenant_id>
     Authority = " https://login.microsoftonline.com/Enter_the_tenant_ID_obtained_from_the_Microsoft_Entra_admin_center",
     // 'Enter the client ID obtained from the Microsoft Entra admin center
     ClientId = "Enter the client ID obtained from the Microsoft Entra admin center",
     // Client secret 'Value' (not its ID) from 'Client secrets' in the Microsoft Entra admin center
     ClientSecret = "Enter the client secret value obtained from the Microsoft Entra admin center",
     // Client 'Object ID' of app registration in Microsoft Entra admin center - this value is a GUID
     ClientObjectId = "Enter the client Object ID obtained from the Microsoft Entra admin center"
    ```

    - `Authority` - The authority is a URL that indicates a directory that MSAL can request tokens from. Replace *Enter\_the\_tenant\_ID\_obtained\_from\_the\_Microsoft\_Entra\_admin\_center* with the **Directory (tenant) ID** value that was recorded earlier.
    - `ClientId` - The identifier of the application, also referred to as the client. Replace the text in quotes with the `Application (client) ID` value that was recorded earlier from the overview page of the registered application.
    - `ClientSecret` - The client secret created for the application in the Microsoft Entra admin center. Enter the **value** of the client secret.
    - `ClientObjectId` - The object ID of the client application. Replace the text in quotes with the `Object ID` value that you recorded earlier from the overview page of the registered application.

# [Node](#tab/node-workforce)
In your editor, open the *.env* file, then replace the placeholders:

- `Enter_the_Application_Id_Here` with the application (client) ID of the application you registered earlier.
- `Enter_the_Tenant_Id_Here` with the Tenant ID of your workforce tenant.
- `Enter_the_Client_Secret_Here` with the client secret you created earlier.
- `Enter_the_Cloud_Instance_Id_Here` with `https://login.microsoftonline.com`.
- `Enter_the_Graph_Endpoint_Here` with `https://graph.microsoft.com/`.

# [Python](#tab/python-workforce)
1. Navigate to the *1-Call-MsGraph-WithSecret* directory.
2. In your editor, open the **parameters.json** file and replace the placeholders:

    - `Enter_the_Application_Id_Here` with the application (client) ID of the application you registered earlier.
    - `Enter_the_Tenant_Id_Here` with the Tenant ID of your workforce tenant.
    - `Enter_the_Client_Secret_Here` with the client secret you created earlier.

# [Java](#tab/java-workforce)
1. Navigate to the `msal-client-credential-secret` directory.
2. In your editor, open the `src\main\resources\application.properties` file and replace the placeholders:

    - `Enter_the_Application_Id_Here` with the application (client) ID of the application you registered earlier.
    - `Enter_the_Tenant_Id_Here` with the Tenant ID of your workforce tenant.
    - `Enter_the_Client_Secret_Here` with the client secret you created earlier.

---

## Run and test the application

You've configured your sample app. You can proceed to run and test it.

# [.NET](#tab/asp-dot-net-core-workforce)
From your console window, run the following command to build and run the application:

```console
dotnet run
```

Once the application runs successfully, it displays a response similar to the following snippet (shortened for brevity):

```console
{
"@odata.context": "https://graph.microsoft.com/v1.0/$metadata#applications/$entity",
"id": "00001111-aaaa-2222-bbbb-3333cccc4444",
"deletedDateTime": null,
"appId": "00001111-aaaa-2222-bbbb-3333cccc4444",
"applicationTemplateId": null,
"disabledByMicrosoftStatus": null,
"createdDateTime": "2021-01-17T15:30:55Z",
"displayName": "identity-dotnet-console-app",
"description": null,
"groupMembershipClaims": null,
...
}
```

### How it works

A daemon application acquires a token on behalf of itself (not on behalf of a user). Users can't interact with a daemon application because it requires its own identity. This type of application requests an access token by using its application identity by presenting its application ID, credential (secret or certificate), and an application ID URI. The daemon application uses the standard [OAuth 2.0 client credentials grant flow](v2-oauth2-client-creds-grant-flow) to acquire an access token.

The app acquires an access token from Microsoft identity platform. The access token is scoped for the Microsoft Graph API. The app then uses the access token to request its own application registration details from Microsoft Graph API. The app can request any resource from Microsoft Graph API as long as the access token has the right permissions.

The sample demonstrates how an unattended job or Windows service can run with an application identity, instead of a user's identity.

# [Node](#tab/node-workforce)
1. To install dependencies, run the following command:

    ```console
    npm install
    ```
2. Use the following command to run the application:

    ```console
    node . --op getUsers
    ```

If the app runs successfully, you should see a JSON formatted output representing a list of all users from your workforce tenant. It looks similar to the following snippet:

```json
{
  '@odata.context': 'https://graph.microsoft.com/v1.0/$metadata#users',
  value: [
    {
      businessPhones: [],
      displayName: 'Casey Jensen',
      givenName: 'Jense',
      jobTitle: null,
      mail: null,
      mobilePhone: null,
      officeLocation: null,
      preferredLanguage: null,
      surname: 'Casey',
      userPrincipalName: 'jensen@contoso.onmicrosoft.com',
      id: 'aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb'
    },
    ...
  ]
}

```

### How it works

A daemon application acquires a token on behalf of itself (not on behalf of a user). Users can't interact with a daemon application because it requires its own identity. This type of application requests an access token by using its application identity by presenting its application ID, credential (secret or certificate), and an application ID URI. The daemon application uses the standard [OAuth 2.0 client credentials grant flow](v2-oauth2-client-creds-grant-flow) to acquire an access token.

The app acquires an access token from Microsoft identity platform. The access token is scoped for the Microsoft Graph API. The app then uses the access token to read all users in the tenant from Microsoft Graph API. The app can request any resource from Microsoft Graph API as long as the access token has the right permissions. In this case, we granted the app **User.Read.All** app permission so that it read all users' full profiles.

The sample demonstrates how an unattended job or Windows service can run with an application identity, instead of a user's identity.

# [Python](#tab/python-workforce)
1. To install dependencies, run the following command:

    ```console
    pip install -r requirements.txt
    ```
2. To run the application, use the following command:

    ```console
    python confidential_client_secret_sample.py parameters.json
    ```

If the app runs successfully, you should see a JSON formatted output representing a list of all users from your workforce tenant. It looks similar to the following snippet:

```json
{
  '@odata.context': 'https://graph.microsoft.com/v1.0/$metadata#users',
  value: [
    {
      businessPhones: [],
      displayName: 'Casey Jensen',
      givenName: 'Jense',
      jobTitle: null,
      mail: null,
      mobilePhone: null,
      officeLocation: null,
      preferredLanguage: null,
      surname: 'Casey',
      userPrincipalName: 'jensen@contoso.onmicrosoft.com',
      id: 'aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb'
    },
    ...
  ]
}

```

### How it works

A daemon application acquires a token on behalf of itself (not on behalf of a user). Users can't interact with a daemon application because it requires its own identity. This type of application requests an access token by using its application identity by presenting its application ID, credential (secret or certificate), and an application ID URI. The daemon application uses the standard [OAuth 2.0 client credentials grant flow](v2-oauth2-client-creds-grant-flow) to acquire an access token.

The app acquires an access token from Microsoft identity platform. The access token is scoped for the Microsoft Graph API. The app then uses the access token to read all users in the tenant from Microsoft Graph API. The app can request any resource from Microsoft Graph API as long as the access token has the right permissions. In this case, we granted the app **User.Read.All** app permission so that it read all users' full profiles.

The sample demonstrates how an unattended job or Windows service can run with an application identity, instead of a user's identity.

# [Java](#tab/java-workforce)
You can test the sample app by running the main method of *ClientCredentialGrant.java* from your IDE or

1. From your console, run the following command:

    ```
    $ mvn clean compile assembly:single
    ```

    This command generates a *msal-client-credential-secret-1.0.0.jar* file in your */targets* directory.
2. Navigate to the */targets* directory, then run your Java executable file using the following command:

    ```
    $ java -jar msal-client-credential-secret-1.0.0.jar
    ```

If the app runs successfully, you should see a JSON formatted output representing a list of all users from your workforce tenant. It looks similar to the following snippet:

```json
{
  '@odata.context': 'https://graph.microsoft.com/v1.0/$metadata#users',
  value: [
    {
      businessPhones: [],
      displayName: 'Casey Jensen',
      givenName: 'Jense',
      jobTitle: null,
      mail: null,
      mobilePhone: null,
      officeLocation: null,
      preferredLanguage: null,
      surname: 'Casey',
      userPrincipalName: 'jensen@contoso.onmicrosoft.com',
      id: 'aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb'
    },
    ...
  ]
}

```

### How it works

A daemon application acquires a token on behalf of itself (not on behalf of a user). Users can't interact with a daemon application because it requires its own identity. This type of application requests an access token by using its application identity by presenting its application ID, credential (secret or certificate), and an application ID URI. The daemon application uses the standard [OAuth 2.0 client credentials grant flow](v2-oauth2-client-creds-grant-flow) to acquire an access token.

The app acquires an access token from Microsoft identity platform. The access token is scoped for the Microsoft Graph API. The app then uses the access token to read all users in the tenant from Microsoft Graph API. The app can request any resource from Microsoft Graph API as long as the access token has the right permissions. In this case, we granted the app **User.Read.All** app permission so that it read all users' full profiles.

The sample demonstrates how an unattended job or Windows service can run with an application identity, instead of a user's identity.

---

::: zone-end

::: zone pivot="external"

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- This Azure account must have permissions to manage applications. Any of the following Microsoft Entra roles include the required permissions:
    - Application Administrator
    - Application Developer
    - Cloud Application Administrator
- An external tenant. To create one, choose from the following methods:
    - (Recommended) Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/samples/marketplace) to set up an external tenant directly in Visual Studio Code.
    - [Create a new external tenant](../external-id/customers/how-to-create-external-tenant-portal) in the Microsoft Entra admin center.
- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com) with the following configuration. For more information, see [Register an application](quickstart-register-app).
    - **Name**: *ciam-daemon-app*
    - **Supported account types**: *Accounts in this organizational directory only (Single tenant)*
- [Visual Studio Code](https://code.visualstudio.com/download) or another code editor.
- [.NET 7.0](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/install) or later.
- [Node.js](https://nodejs.org) (for Node implementation only)

## Create a client secret

Create a client secret for the registered application. The application uses the client secret to prove its identity when it requests for tokens:

1. From the **App registrations** page, select the application that you created (such as *web app client secret*) to open its **Overview** page.
2. Under **Manage**, select **Certificates & secrets** &gt; **Client secrets** &gt; **New client secret**.
3. In the **Description** box, enter a description for the client secret (for example, *web app client secret*).
4. Under **Expires**, select a duration for which the secret is valid (per your organizations security rules), and then select **Add**.
5. Record the secret's **Value**. You use this value for configuration in a later step. The secret value won't be displayed again, and isn't retrievable by any means, after you navigate away from the **Certificates and secrets**. Make sure you record it.

When you create credentials for a confidential client application:

- Microsoft recommends that you use a certificate instead of a client secret before moving the application to a production environment. For more information on how to use a certificate, see instructions in [Microsoft identity platform application authentication certificate credentials](certificate-credentials).
- For testing purposes, you can create a self-signed certificate and configure your apps to authenticate with it. However, **in production**, you should purchase a certificate signed by a well-known certificate authority, then use [Azure Key Vault](/en-us/azure/key-vault/general/overview) to manage certificate access and lifetime.

## Grant API permissions to the daemon app

1. From the **App registrations** page, select the application that you created, such as *ciam-client-app*.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Select the **APIs my organization uses** tab.
5. In the list of APIs, select the API such as *ciam-ToDoList-api*.
6. Select **Application permissions** option. We select this option as the app signs in as itself, but not on behalf of a user.
7. From the permissions list, select **TodoList.Read.All, ToDoList.ReadWrite.All** (use the search box if necessary).
8. Select the **Add permissions** button.
9. At this point, you've assigned the permissions correctly. However, since the daemon app doesn't allow users to interact with it, the users themselves can't consent to these permissions. To address this problem, you as the admin must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both permissions.

## Configure app roles

An API needs to publish a minimum of one app role for applications, also called [Application permission](permissions-consent-overview), for the client apps to obtain an access token as themselves. Application permissions are the type of permissions that APIs should publish when they want to enable client applications to successfully authenticate as themselves and not need to sign-in users. To publish an application permission, follow these steps:

1. From the **App registrations** page, select the application that you created (such as *ciam-ToDoList-api*) to open its **Overview** page.
2. Under **Manage**, select **App roles**.
3. Select **Create app role**, then enter the following values, then select **Apply** to save your changes:

    | Property | Value |
    | --- | --- |
    | Display name | *ToDoList.Read.All* |
    | Allowed member types | **Applications** |
    | Value | *ToDoList.Read.All* |
    | Description | *Allow the app to read every user's ToDo list using the 'TodoListApi'* |
    | Do you want to enable this app role? | Keep it checked |
4. Select **Create app role** again, then enter the following values for the second app role, then select **Apply** to save your changes:

    | Property | Value |
    | --- | --- |
    | Display name | *ToDoList.ReadWrite.All* |
    | Allowed member types | **Applications** |
    | Value | *ToDoList.ReadWrite.All* |
    | Description | *Allow the app to read and write every user's ToDo list using the 'ToDoListApi'* |
    | Do you want to enable this app role? | Keep it checked |

## Configure optional claims

You can add the **idtyp** optional claim to help the web API to determine whether a token is an **app** token or an **app + user** token. Although you can use a combination of **scp** and **roles** claims for the same purpose, using the **idtyp** claim is the easiest way to tell an app token and an app + user token apart. For example, the value of this claim is *app* when the token is an app-only token.

## Clone or download sample daemon application and web API

To obtain the sample application, you can either clone it from GitHub or download it as a .zip file.

# [Node](#tab/node-external)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial.git
    ```
- Alternatively, [download the samples .zip file](https://github.com/Azure-Samples/ms-identity-ciam-javascript-tutorial/archive/refs/heads/main.zip), then extract it to a file path where the length of the name is fewer than 260 characters.

### Install project dependencies

1. Open a console window, and change to the directory that contains the Node.js sample app:

    ```console
    cd 2-Authorization\3-call-api-node-daemon\App
    ```
2. Run the following commands to install app dependencies:

    ```console
    npm install && npm update
    ```

# [.NET](#tab/asp-dot-net-core-external)
- To clone the sample, open a command prompt and navigate to where you wish to create the project, and enter the following command:

    ```console
    git clone https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial.git
    ```
- [Download the .zip file](https://github.com/Azure-Samples/ms-identity-ciam-dotnet-tutorial/archive/refs/heads/main.zip). Extract it to a file path where the length of the name is fewer than 260 characters.

---

## Configure the sample daemon app and API

To use your app registration details in the client web app sample, use the following steps:

# [Node](#tab/node-external)
1. In your code editor, open `App\authConfig.js` file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the daemon app you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    - `Enter_the_Client_Secret_Here` and replace it with the daemon app secret value you copied earlier.
    - `Enter_the_Web_Api_Application_Id_Here` and replace it with the Application (client) ID of the web API you copied earlier.

To use your app registration in the web API sample:

1. In your code editor, open `API\ToDoListAPI\appsettings.json` file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the web API you copied.
    - `Enter_the_Tenant_Id_Here` and replace it with the Directory (tenant) ID you copied earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

# [.NET](#tab/asp-dot-net-core-external)
1. In your code editor, open *ms-identity-ciam-dotnet-tutorial/2-Authorization/3-call-own-api-dotnet-core-daemon/ToDoListClient/appsettings.json* file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the daemon application you registered earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).
    - `Enter_the_Client_Secret_Here` and replace it with the daemon application secret value you copied earlier.
    - `Enter_the_Web_Api_Application_Id_Here` and replace it with the Application (client) ID of the web API you copied earlier.

To use your app registration in the web API sample:

1. In your code editor, open *ms-identity-ciam-dotnet-tutorial/2-Authorization/3-call-own-api-dotnet-core-daemon/ToDoListAPI/appsettings.json* file.
2. Find the placeholder:

    - `Enter_the_Application_Id_Here` and replace it with the Application (client) ID of the web API you copied.
    - `Enter_the_Tenant_Id_Here` and replace it with the Directory (tenant) ID you copied earlier.
    - `Enter_the_Tenant_Subdomain_Here` and replace it with the Directory (tenant) subdomain. For example, if your tenant primary domain is `contoso.onmicrosoft.com`, use `contoso`. If you don't have your tenant name, learn how to [read your tenant details](../external-id/customers/how-to-create-external-tenant-portal#get-the-external-tenant-details).

---

## Run and test sample daemon app and API

You've configured your sample app. You can proceed to run and test it.

# [Node](#tab/node-external)
1. Open a console window, then run the web API by using the following commands:

    ```console
    cd 2-Authorization\3-call-api-node-daemon\API\ToDoListAPI
    dotnet run
    ```
2. Run the web app client by using the following commands:

    ```console
    2-Authorization\3-call-api-node-daemon\App
    node . --op getToDos
    ```

If your daemon app and web API successfully run, you should see something similar to the following JSON array in your console window

```json
{
    "id": 1,
    "owner": "3e8....-db63-43a2-a767-5d7db...",
    "description": "Pick up grocery"
},
{
    "id": 2,
    "owner": "c3cc....-c4ec-4531-a197-cb919ed.....",
    "description": "Finish invoice report"
},
{
    "id": 3,
    "owner": "a35e....-3b8a-4632-8c4f-ffb840d.....",
    "description": "Water plants"
}
```

### How it works

The Node.js app uses the [OAuth 2.0 client credentials grant flow](v2-oauth2-client-creds-grant-flow) to acquire an access token for itself and not for the user. The access token that the app requests contains the permissions represented as roles. The client credential flow uses this set of permissions in place of user scopes for application tokens. You exposed these application permissions in the web API earlier, then granted them to the daemon app.

On the API side, a sample .NET web API, the API must verify that the access token has the required permissions (application permissions). The web API can't accept an access token that doesn't have the required permissions.

### Access to data

A Web API endpoint should be prepared to accept calls from both users and applications. Therefore, it should have a way to respond to each request accordingly. For example, a call from a user via delegated permissions/scopes receives the user's data to-do list. On the other hand, a call from an application via application permissions/roles may receive the entire to-do list. However, in this article, we're only making an application call, so we didn't need to configure delegated permissions/scopes.

# [.NET](#tab/asp-dot-net-core-external)
1. Open a console window, then run the web API by using the following commands:

    ```console
    cd 2-Authorization\3-call-own-api-dotnet-core-daemon\ToDoListAPI
    dotnet run
    ```
2. Run the daemon client by using the following commands:

    ```console
    cd 2-Authorization\3-call-own-api-dotnet-core-daemon\ToDoListClient
    dotnet run
    ```

    If your daemon application and web API successfully run, you should see something similar to the following JSON array in your console window:

    ```bash
    Posting a to-do...
    Retrieving to-do's from server...
    To-do data:
    ID: 1
    User ID: 00aa00aa-bb11-cc22-dd33-44ee44ee44ee
    Message: Bake bread
    Posting a second to-do...
    Retrieving to-do's from server...
    To-do data:
    ID: 1
    User ID: 00aa00aa-bb11-cc22-dd33-44ee44ee44ee
    Message: Bake bread
    ID: 2
    User ID: 00aa00aa-bb11-cc22-dd33-44ee44ee44ee
    Message: Butter bread
    Deleting a to-do...
    Retrieving to-do's from server...
    To-do data:
    ID: 2
    User ID: 00aa00aa-bb11-cc22-dd33-44ee44ee44ee
    Message: Butter bread
    Editing a to-do...
    Retrieving to-do's from server...
    To-do data:
    ID: 2
    User ID: 00aa00aa-bb11-cc22-dd33-44ee44ee44ee
    Message: Eat bread
    Deleting remaining to-do...
    Retrieving to-do's from server...
    There are no to-do's in server
    ```

## How it works

The daemon application uses the [OAuth 2.0 client credentials grant flow](v2-oauth2-client-creds-grant-flow) to acquire an access token for itself and not for the user. The access token that the app requests contains the permissions represented as roles. The client credential flow uses this set of permissions in place of user scopes for application tokens. You exposed these application permissions in the web API earlier, then granted them to the daemon app. The daemon app in this article uses [Microsoft Authentication Library for .NET](/en-us/entra/msal/dotnet/) to simplify the process of acquiring a token.

On the API side, a sample .NET web API, the API must verify that the access token has the required permissions (application permissions). The web API rejects access tokens that don't have the required permissions.

---

## Related content

# [Node](#tab/node-external)
- [Acquire an access token, then call a web API in your own Node.js daemon app](/en-us/entra/external-id/customers/tutorial-daemon-node-call-api-prepare-tenant).
- [Use a client certificate instead of a secret for authentication in your Node.js confidential app](/en-us/entra/external-id/customers/how-to-web-app-node-use-certificate).

# [.NET](#tab/asp-dot-net-core-external)
- [Use our multi-part tutorial series to build this .NET daemon app from scratch](/en-us/entra/external-id/customers/tutorial-daemon-dotnet-call-api-prepare-tenant)

---

::: zone-end