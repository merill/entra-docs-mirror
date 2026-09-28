---
layout: Conceptual
title: Create a custom authentication extension for attribute collection start and submit events (preview) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-extension-attribute-collection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to develop and register a Microsoft Entra custom authentication extensions REST API. The custom authentication extension allows you to add logic to attribute collection.
manager: pmwongera
ms.date: 2025-09-16T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 00b5cb48-d4b9-4baa-3aa2-0c9d096db9fb
document_version_independent_id: 00b5cb48-d4b9-4baa-3aa2-0c9d096db9fb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-extension-attribute-collection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-extension-attribute-collection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-extension-attribute-collection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 9a1484b9-6689-8bee-ba2c-89876346badb
---

# Create a custom authentication extension for attribute collection start and submit events (preview) - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article describes how to extend the user sign-up experience in Microsoft Entra External ID for customers. In customer sign-up user flows, event listeners can be used to extend the attribute collection process before attribute collection and at the time of attribute submission:

- The **OnAttributeCollectionStart** event occurs at the beginning of the attribute collection step, before the attribute collection page renders. You can add actions such as prefilling values and displaying a blocking error.
- The **OnAttributeCollectionSubmit** event occurs after the user enters and submits attributes. You can add actions such as validating or modifying the user's entries.

In addition to creating a custom authentication extension for the attribute collection start and submit events, you need to create a REST API that defines the workflow actions to take for each event. You can use any programming language, framework, and hosting environment to create and host your REST API. This article demonstrates a quick way to get started using a C# Azure Function. With Azure Functions, you run your code in a serverless environment without having to first create a virtual machine (VM) or publish a web application.

## Prerequisites

- To use Azure services, including Azure Functions, you need an Azure subscription. If you don't have an existing Azure account, you can sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) or use your [Visual Studio Subscription](https://visualstudio.microsoft.com/subscriptions/) benefits when you [create an account](https://account.windowsazure.com/Home/Index).
- A [sign-up and sign-in user flow](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers).

## Step 1: Create a custom authentication extensions REST API (Azure Function app)

In this step, you create an HTTP trigger function API using Azure Functions. The function API is the source of the business logic for your user flows. After creating your trigger function, you can configure it for either of the following events:

- OnAttributeCollectionStart
- OnAttributeCollectionSubmit

1. Sign in to the [Azure portal](https://portal.azure.com) with your administrator account.
2. From the Azure portal menu or the **Home** page, select **Create a resource**.
3. Search for and select **Function App** and select **Create**.
4. On the **Basics** page, use the function app settings as specified in the following table:

    | Setting | Suggested value | Description |
    | --- | --- | --- |
    | **Subscription** | Your subscription | The subscription in which the new function app will be created. |
    | **Resource Group** | *myResourceGroup* | Select and existing resource group, or name for the new one in which you'll create your function app. |
    | **Function App name** | Globally unique name | A name that identifies the new function app. Valid characters are `a-z` (case insensitive), `0-9`, and `-`. |
    | **Publish** | Code | Option to publish code files or a Docker container. For this tutorial, select **Code**. |
    | **Runtime stack** | .NET | Your preferred programming language. For this tutorial, select **.NET**. |
    | **Version** | 6 (LTS) isolated (out-of-process) | Version of the .NET runtime. Isolated (out-of-process) signifies that you can create and run functions using the supported hosting model. |
    | **Region** | Preferred region | Select a [region](https://azure.microsoft.com/regions/) that's near you or near other services that your functions can access. |
    | **Operating System** | Windows | The operating system is preselected for you based on your runtime stack selection. |
    | **Plan type** | Consumption (Serverless) | Hosting plan that defines how resources are allocated to your function app. |
5. Select **Review + create** to review the app configuration selections and then select **Create**. Deployment takes a few minutes.
6. Once deployed, select **Go to resource** to view your new function app.

### 1.1 Create HTTP trigger functions

Now that you've created the Azure Function app, you create HTTP trigger functions for the actions you want to invoke with an HTTP request. HTTP triggers are referenced and called by your Microsoft Entra custom authentication extension.

1. Within the **Overview** page of your function app, select the **Functions** pane and select **Create function** under **Create in Azure portal**.
2. In the **Create Function** window, leave the **Development environment** property as **Develop in portal**. Under **Template**, select **HTTP trigger**.
3. Under **Template details**, enter *CustomAuthenticationExtensionsAPI* for the **New Function** property.
4. For the **Authorization level**, select **Function**.
5. Select **Create**.

### 1.2 Configure the HTTP trigger for OnAttributeCollectionStart

1. From the menu, select **Code + Test**.
2. Select the tab below for the scenario you want to implement: **Continue**, **Block**, or **SetPrefillValues**. Replace the code with the code snippet(s) provided.
3. After you replace the code, from the top menu, select **Get Function Url**, and copy the URL. You use this URL in Step 2: Create and register a custom authentication extension for **Target Url**.

# [Continue](#tab/start-continue)
Use this HTTP trigger to allow the user to continue with the sign-up flow if no further action is needed.

```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Text;

public static async Task<object> Run(HttpRequest req, ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    dynamic request = JsonConvert.DeserializeObject(requestBody);

    var actions = new List<ContinueWithDefaultBehavior>{
        new ContinueWithDefaultBehavior { type = "microsoft.graph.attributeCollectionStart.continueWithDefaultBehavior"}
    };

    var dataObject = new Data {
        type = "microsoft.graph.onAttributeCollectionStartResponseData",
        actions= actions
    };

    dynamic response = new ResponseObject {
        data = dataObject
    };

    // Send the response
    return response;
}

public class ResponseObject
{
    public Data data { get; set; }
}

[JsonObject]
public class Data {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public List<ContinueWithDefaultBehavior> actions { get; set; }
}

[JsonObject]
public class ContinueWithDefaultBehavior {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
}
```

# [Block](#tab/start-block)
Use this HTTP trigger to block the user from continuing the sign-up process. For example, you could use an identity verification service or external identity data source to verify the user's email address.

```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Text;

public static async Task<object> Run(HttpRequest req, ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    
    dynamic request = JsonConvert.DeserializeObject(requestBody);       

    var actions = new List<BlockedActions>{
        new BlockedActions { 
            type = "microsoft.graph.attributeCollectionStart.showBlockPage", 
            message = "AttributeCollectionStart Custom Extension message: Sorry, your access request has been blocked. Try reaching an admin at admin@contoso.com."
        }
    };

    var dataObject = new Data {
        type = "microsoft.graph.onAttributeCollectionStartResponseData",
        actions= actions
    };

    dynamic response = new ResponseObject {
        data = dataObject
    };

    // Send the response
    return response;
}

public class ResponseObject
{
    public Data data { get; set; }
}

[JsonObject]
public class Data {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public List<BlockedActions> actions { get; set; }
}

[JsonObject]
public class BlockedActions {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public string message { get; set; }
}
```

# [Prefill values](#tab/start-set-prefill-values)
Use this HTTP trigger to prefill the values associated with the user flow, for example from an external HR system or other data source. You can prefill values for built-in attributes (for example, address), custom user attributes (for example, loyalty number).

```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using System.Text;

public static async Task<object> Run(HttpRequest req, ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    dynamic request = JsonConvert.DeserializeObject(requestBody);

    // The form fields will load with these default values
    var inputs = new Dictionary<string, object>()
    {
        { "postalCode", "<your-prefill-value>" },
        { "streetAddress", "<your-prefill-value>" },
        { "city", "<your-prefill-value>" },
        { "extension_appId_mailingList", false },
        { "extension_appId_memberSince", 2023 }      
    };

    var actions = new List<SetPrefillValuesAction>{
        new SetPrefillValuesAction { 
            type = "microsoft.graph.attributeCollectionStart.setPrefillValues", 
            inputs = inputs }
    };

    var dataObject = new Data {
        type = "microsoft.graph.onAttributeCollectionStartResponseData",
        actions= actions
    };

    dynamic response = new ResponseObject {
        data = dataObject
    };

    // Send the response
    return response;
}

public class ResponseObject
{
    public Data data { get; set; }
}

[JsonObject]
public class Data {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public List<SetPrefillValuesAction> actions { get; set; }
}

[JsonObject]
public class SetPrefillValuesAction {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public Dictionary<string, object> inputs { get; set; }
}
```

---

### 1.3 Configure the HTTP trigger for OnAttributeCollectionSubmit

1. From the menu, select **Code + Test**.
2. Select the tab below for the scenario you want to implement: **Continue**, **Block**, **Modify values**, or **Validation error**. Replace the code with the code snippet(s) provided.
3. After you replace the code, from the top menu, select **Get Function Url**, and copy the URL. You use this URL in Step 2: Create and register a custom authentication extension for **Target Url**.

# [Continue](#tab/submit-continue)
Use this HTTP trigger to allow the user to continue with the sign-up flow if no further action is needed.

```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Text;

public static async Task<object> Run(HttpRequest req, ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    dynamic request = JsonConvert.DeserializeObject(requestBody);
    
    var actions = new List<ContinueWithDefaultBehavior>{
        new ContinueWithDefaultBehavior { type = "microsoft.graph.attributeCollectionSubmit.continueWithDefaultBehavior"}
    };					
    var dataObject = new Data {
        type = "microsoft.graph.onAttributeCollectionSubmitResponseData",
        actions= actions
    };    dynamic response = new ResponseObject {
        data = dataObject
    };

    // Send the response
    return response;
}

public class ResponseObject
{
    public Data data { get; set; }
}

[JsonObject]
public class Data {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    
    public List<ContinueWithDefaultBehavior> actions { get; set; }
}

[JsonObject]
public class ContinueWithDefaultBehavior {
    [JsonProperty("@odata.type")]public string type { get; set; }
}
```

# [Block](#tab/submit-block)
Use this HTTP trigger to block the user from continuing the sign-up process based on the attribute values they entered. For example, you can block sign-up based on a risky phone number. Or you can terminate the sign-up flow and send the user to a custom approval system for account creation.

```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Text;

public static async Task<object> Run(HttpRequest req, ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    dynamic request = JsonConvert.DeserializeObject(requestBody);
    
    var actions = new List<BlockedActions>{
        new BlockedActions { 
            type = "microsoft.graph.attributeCollectionSubmit.showBlockPage", 
            message = "AttributeCollectionSubmit Custom Extension Message: Thank you for your response. Your access request is processing. You'll be notified when your request has been approved."
        }
    };

    var dataObject = new Data {
        type = "microsoft.graph.onAttributeCollectionSubmitResponseData",
        actions= actions
    };

    dynamic response = new ResponseObject {
        data = dataObject
    };

    // Send the response
    return response;
}

public class ResponseObject
{
    public Data data { get; set; }
}

[JsonObject]
public class Data {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public List<BlockedActions> actions { get; set; }
}

[JsonObject]
public class BlockedActions {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public string message { get; set; }
}
```

# [Modify values](#tab/submit-modify-collected-values)
Use this HTTP trigger to modify attributes collection from the user. For example, you can change the format of a user-provided attribute. After attributes are modified, sign-up continues without notification to user. If notification is required, use the validate action.

```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Text;

public static async Task<object> Run(HttpRequest req, ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    // User attributes will be saved with these override values
    var attributes = new Dictionary<string, object>()
    {
        { "postalCode", "<your-override-value>" },
        { "streetAddress", "<your-override-value>" },
        { "city", "<your-override-value>" },
        { "extension_appId_mailingList", false }
        { "extension_appId_memberSince", 2010 }
    };

    var actions = new List<ModifiedAttributesAction>{
        new ModifiedAttributesAction { 
            type = "microsoft.graph.attributeCollectionSubmit.modifyAttributeValues", 
            attributes = attributes 
        }
    };

    log.LogInformation("actions: " + actions);

    var dataObject = new Data {
        type = "microsoft.graph.onAttributeCollectionSubmitResponseData",
        actions= actions
    };

    dynamic response = new ResponseObject {
        data = dataObject
    };

    // Send the response
    return response;
}

public class ResponseObject
{
    public Data data { get; set; }
}

[JsonObject]
public class Data {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public List<ModifiedAttributesAction> actions { get; set; }
}

[JsonObject]
public class ModifiedAttributesAction {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public Dictionary<string, object> attributes { get; set; }
}
```

# [Validation error](#tab/submit-show-validation-error)
Use this HTTP trigger to validate attributes entered by the user. For example, you can validate attributes against an external data store. You can validate built-in attributes (for example, country), custom user attributes (for example, loyalty number).

```csharp
#r "Newtonsoft.Json"

using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using System.Text;

public static async Task<object> Run(HttpRequest req, ILogger log)
{
    log.LogInformation($"C# HTTP trigger function processed a request.");

    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    dynamic request = JsonConvert.DeserializeObject(requestBody);

    // Parse specified attributes
    string cityValue = (JsonConvert.SerializeObject(request?.data?.userSignUpInfo?.attributes?.city?.value)).ToString();

    string postalCodeValue = (JsonConvert.SerializeObject(request?.data?.userSignUpInfo?.attributes?.postalCode?.value)).ToString();

    string streetAddressValue = (JsonConvert.SerializeObject(request?.data?.userSignUpInfo?.attributes?.streetAddress?.value)).ToString();

    // JSON convert makes the length different, so we put 7 here
    if(cityValue.Length < 7 || postalCodeValue.Length < 7 || streetAddressValue.Length < 7){
        var inputs = new Dictionary<string, string>();

        if(cityValue.Length < 7){
            inputs.Add("city", "Length of city string should be of at 5 characters at least");
        }

        if(postalCodeValue.Length < 7){
            inputs.Add("postalCode", "Length of postalCodeValue string should be of at 5 characters at least");
        }

        if(streetAddressValue.Length < 7){
            inputs.Add("streetAddress", "Length of streetAddress string should be of at 5 characters at least");
        }

        string pageMessage = "Please fix below errors to proceed";

        var actions = new List<ValidationErrorActions>{
            new ValidationErrorActions { type = "microsoft.graph.attributeCollectionSubmit.ShowValidationError", message = pageMessage, attributeErrors = inputs }
        };

        var dataObject = new Data {
            type = "microsoft.graph.onAttributeCollectionSubmitResponseData",
            actions= actions
        };

        dynamic response = new ResponseObject {
            data = dataObject
        };

        log.LogInformation($"Returning validation error");

        // Send the validation error response
        return response;

    }else{
        var actions = new List<ContinueWithDefaultBehavior>{
            new ContinueWithDefaultBehavior { type = "microsoft.graph.attributeCollectionSubmit.ContinueWithDefaultBehavior"}
            };

        var dataObject = new DataContinue {
            type = "microsoft.graph.onAttributeCollectionSubmitResponseData",
            actions= actions
            };

        dynamic response = new ResponseObjectContinue {
            data = dataObject
        };

        log.LogInformation($"Returning continue");
        
        // Send the continue response
        return response;
    }
}

public class ResponseObject
{
    public Data data { get; set; }
}

[JsonObject]
public class Data {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public List<ValidationErrorActions> actions { get; set; }
}

[JsonObject]
public class ValidationErrorActions {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public string message { get; set; }
    public Dictionary<string, string> attributeErrors {get; set;}
}

public class ResponseObjectContinue
{
    public DataContinue data { get; set; }
}

[JsonObject]
public class DataContinue {
    [JsonProperty("@odata.type")]
    public string type { get; set; }
    public List<ContinueWithDefaultBehavior> actions { get; set; }
}

[JsonObject]
public class ContinueWithDefaultBehavior {
    [JsonProperty("@odata.type")]public string type { get; set; }
}
```

---

## Step 2: Create and register a custom authentication extension

In this step, you register a custom authentication extension that is used by Microsoft Entra ID to call your Azure function. The custom authentication extension contains information about your REST API endpoint, the attribute collection start and submit actions that it parses from your REST API, and how to authenticate to your REST API.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-developer) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Custom authentication extensions**.
3. Select **Create a custom extension**.
4. In **Basics**, select the **AttributeCollectionStart** event or the **AttributeCollectionSubmit** event, and then select **Next**. Be sure that this matches the configuration in the previous step.
5. In **Endpoint Configuration**, fill in the following properties:

    - **Name** - A name for your custom authentication extension. For example, *On Attribute Collection Event*.
    - **Target Url** - The `{Function_Url}` of your Azure Function URL.
    - **Description** - A description for your custom authentication extensions.
6. Select **Next**.
7. In **API Authentication**, select the **Create new app registration** option to create an app registration that represents your *function app*.
8. Give the app a name, for example **Azure Functions authentication events API**.
9. Select **Next**.
10. Select **Create**, which creates the custom authentication extension and the associated application registration.

### 2.2 Grant admin consent

After your custom authentication extension is created, grant application consent to the registered app, which allows the custom authentication extension to authenticate to your API.

1. Browse to **Entra ID** &gt; **External Identities** &gt; **Custom authentication extensions**.
2. Select your custom authentication extension from the list.
3. On the **Overview** tab, select the **Grant permission** button to give admin consent to the registered app. The custom authentication extension uses `client_credentials` to authenticate to the Azure Function App using the `Receive custom authentication extension HTTP requests` permission. Select **Accept**.

## Step 3: Add the custom authentication extension to a user flow

Now you can associate the custom authentication extension with one or more of your user flows.

Note

If you need to create a user flow, follow the steps in [Create a sign-up and sign-in user flow for customers](../external-id/customers/how-to-user-flow-sign-up-sign-in-customers).

### 3.1 Add the custom authentication extension to an existing user flow

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-developer) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator)
2. If you have access to multiple tenants, use the **Settings** icon ![](media/custom-extension-attribute-collection/settings-icon.png) in the top menu to switch to your external tenant.
3. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
4. Select the user flow from the list.
5. Select **Custom authentication extensions**.
6. On the **Custom authentication extensions** page, you can associate your custom authentication extension with two different steps in your user flow:

    - **Before collecting information from the user** is associated with the *OnAttributeCollectionStart* event. Select the edit pencil. Only those custom extensions configured for the *OnAttributeCollectionStart* event will be displayed. Select the application you configured for the attribute collection start event, and then choose **Select**.
    - **When a user submits their information** is associated with the *OnAttributeCollectionSubmit* event. only those custom extensions configured for the *OnAttributeCollectionSubmit* event will be displayed. Select the application you configured for the attribute collection submit event, and then choose **Select**.
7. Make sure the applications listed next to both attribute collection steps are correct.
8. Select the **Save** icon.

## Step 4: Test the application

To get a token and test the custom authentication extension, you can use the https://jwt.ms app. It's a Microsoft-owned web application that displays the decoded contents of a token (the contents of the token never leave your browser).

Follow these steps to register the **jwt.ms** web application:

### 4.1 Register the jwt.ms web application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-developer).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select **New registration**.
4. Enter a **Name** for the application. For example, **My Test application**.
5. Under **Supported account types**, select **Accounts in this organizational directory only**.
6. In the **Select a platform** dropdown in **Redirect URI**, select **Web** and then enter `https://jwt.ms` in the URL text box.
7. Select **Register** to complete the app registration.

### 4.2 Get the application ID

In your app registration, under **Overview**, copy the **Application (client) ID**. The app ID is referred to as the `<client_id>` in later steps. In Microsoft Graph, it's referenced by the **appId** property.

### 4.3 Enable implicit flow

The **jwt.ms** test application uses the implicit flow. Enable implicit flow in your *My Test application* registration with the following steps.

Important

Microsoft recommends using the most secure authentication flow available. The authentication flow used for testing in this procedure requires a very high degree of trust in the application, and carries risks that are not present in other flows. This approach shouldn't be used for authenticating users to your production apps ([learn more](v2-oauth2-implicit-grant-flow)).

1. Under **Manage**, select **Authentication**.
2. Under **Implicit grant and hybrid flows**, select the **ID tokens (used for implicit and hybrid flows)** checkbox.
3. Select **Save**.

## Step 5: Protect your Azure Function

Microsoft Entra custom authentication extension uses server to server flow to obtain an access token that is sent in the HTTP `Authorization` header to your Azure function. When publishing your function to Azure, especially in a production environment, you need to validate the token sent in the authorization header.

To protect your Azure function, follow these steps to integrate Microsoft Entra authentication, for validating incoming tokens with your *Azure Functions authentication events API* application registration.

Note

If the Azure function app is hosted in a different Azure tenant than the tenant in which your custom authentication extension is registered, skip to 5.1 Using OpenID Connect identity provider step.

### 5.1 Add an identity provider to your Azure Function

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate and select the function app you previously published.
3. Select **Authentication** in the menu on the left.
4. Select **Add Identity provider**.
5. Select **Microsoft** as the identity provider.
6. Select **Customer** as the tenant type.
7. Under **App registration**, enter the `client_id` of the *Azure Functions authentication events API* app registration you previously created when registering the custom claims provider.
8. For the **Issuer URL**, enter the following URL `https://{domainName}.ciamlogin.com/{tenant_id}/v2.0`, where

    - `{domainName}` is the domain name of your external tenant.
    - `{tenantId}` is the tenant ID of your external tenant. Your custom authentication extension should be registered here.
9. Under **Unauthenticated requests**, select **HTTP 401 Unauthorized** as the identity provider.
10. Unselect the **Token store** option.
11. Select **Add** to add authentication to your Azure Function.

    [![Screenshot that shows how to add authentication to your function app while in a external tenant.](media/custom-extension-attribute-collection/add-identity-provider-auth-function-app-customer.png)](media/custom-extension-attribute-collection/add-identity-provider-auth-function-app-customer.png#lightbox)

### 5.2 Using OpenID Connect identity provider

If you configured Step 5: Protect your Azure Function, skip this step. Otherwise, if the Azure Function is hosted under a different tenant than the tenant in which your custom authentication extension is registered, follow these steps to protect your function:

1. Sign in to the [Azure portal](https://portal.azure.com), then navigate and select the function app you previously published.
2. Select **Authentication** in the menu on the left.
3. Select **Add Identity provider**.
4. Select **OpenID Connect** as the identity provider.
5. Provide a name, such as *Contoso Microsoft Entra ID*.
6. Under the **Metadata entry**, enter the following URL to the **Document URL**. Replace the `{tenantId}` with your Microsoft Entra tenant ID.

    ```http
    https://login.microsoftonline.com/{tenantId}/v2.0/.well-known/openid-configuration
    ```
7. Under the **App registration**, enter the application ID (client ID) of the *Azure Functions authentication events API* app registration you previously created.
8. In the Microsoft Entra admin center:

    1. Select the *Azure Functions authentication events API* app registration you previously created.
    2. Select **Certificates & secrets** &gt; **Client secrets** &gt; **New client secret**.
    3. Add a description for your client secret.
    4. Select an expiration for the secret or specify a custom lifetime.
    5. Select **Add**.
    6. Record the **secret's value** for use in your client application code. This secret value is never displayed again after you leave this page.
9. Back to the Azure Function, under the **App registration**, enter the **Client secret**.
10. Unselect the **Token store** option.
11. Select **Add** to add the OpenID Connect identity provider.

## Step 6: Test the application

To test your custom authentication extension, follow these steps:

1. Open a new private browser and navigate to the following URL:

    ```http
    https://<domainName>.ciamlogin.com/<tenant_id>/oauth2/v2.0/authorize?client_id=<client_id>&response_type=code+id_token&redirect_uri=https://jwt.ms&scope=openid&state=12345&nonce=12345
    ```

    - Replace `<domainName>` with your external tenant name, and replace `<tenant-id>` with your external tenant ID.
    - Replace `<client_id>` with the ID for the application you added to the user flow.
2. After signing in, you'll be presented with your decoded token at `https://jwt.ms`.