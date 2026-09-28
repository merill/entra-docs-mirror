---
layout: Conceptual
title: Configure a custom email provider for one time passcode send events - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-extension-email-otp-get-started
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure and set up a custom email provider with the One Time Passcode Send event type.
manager: pmwongera
ms.reviewer: 
ms.date: 2025-06-25T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 030b758d-ca19-9f9f-8ff4-a1b944e4ab3e
document_version_independent_id: 030b758d-ca19-9f9f-8ff4-a1b944e4ab3e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-extension-email-otp-get-started.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-extension-email-otp-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-extension-email-otp-get-started.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/54fcef21-b24a-4ef4-9c4a-a525c23ee9a3
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ab60220-e56b-41ff-a8bf-45b8d7ab716f
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 3a531dc9-c99a-a0ff-cdcd-bbf728696ec7
---

# Configure a custom email provider for one time passcode send events - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article provides a guide on configuring and setting up a custom email provider for the One Time Passcode (OTP) Send event type. The event is triggered when an OTP email is activated, it allows you to call a REST API to use your own email provider by calling a REST API.

Watch this video to learn how to customize verification emails with Microsoft Entra custom authentication extensions, using a web API based on Azure Logic Apps. Logic App enables users to create workflows through a visual designer.

## Prerequisites

- A familiarity and understanding of the concepts covered in [custom authentication extensions](/en-us/entra/identity-platform/custom-extension-overview).
- An Azure subscription. If you don't have an existing Azure account, sign up for a [free trial](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) or use your [Visual Studio Subscription](https://visualstudio.microsoft.com/subscriptions/) benefits when you [create an account](https://account.windowsazure.com/Home/Index).
- A Microsoft Entra ID [external tenant](../external-id/customers/quickstart-tenant-setup).
- A mail relay service provider:

# [Azure Communication Services](#tab/azure-communication-services)
- An Azure Communications Services resource. If you don't have one, create one in [Quickstart: Create and manage Communication Services resources](/en-us/azure/communication-services/quickstarts/create-communication-resource?tabs=windows&amp;pivots=platform-azp) using a new or existing resource group.
    - An Azure Email Communication Services Resource created and ready with a provisioned domain. If you don't have one, refer to [Quickstart: Create and manage Email Communication Service resources](/en-us/azure/communication-services/quickstarts/email/create-email-communication-resource?pivots=platform-azp), and use the same resource group as the Azure Communication Services.
    - An active Communication Services resource connected with an Email Domain. Refer to [Quickstart: How to connect a verified email domain](/en-us/azure/communication-services/quickstarts/email/connect-email-communication-resource?branch=main&amp;pivots=azure-portal)
    - (Optional) [Send an email using Azure Communication Services](/en-us/azure/communication-services/quickstarts/email/send-email?tabs=windows%2Cconnection-string%2Csend-email-and-get-status-async%2Csync-client&amp;pivots=platform-azportal) to test sending emails to the desired recipients using Azure Communication Services, while verifying the configuration for your application to send email.

# [SendGrid](#tab/sendgrid)
- A SendGrid account. If you don't already have one, start by setting up a SendGrid account. For setup instructions, see the [Create a SendGrid Account](https://docs.sendgrid.com/for-developers/partners/microsoft-azure-2021#create-a-sendgrid-account) section of [How to send email using SendGrid with Azure](https://docs.sendgrid.com/for-developers/partners/microsoft-azure-2021#create-a-twilio-sendgrid-accountcreate-a-twilio-sendgrid-account).

---

## Step 1: Create an Azure Function app

This section shows you how to set up an Azure Function app in the Azure portal. The function API is the gateway to your email provider. You create an Azure Function app to host the HTTP trigger function and configure the settings in the function.

Tip

Steps in this article might vary slightly based on the portal you start from.

1. Sign in to the [Azure portal](https://portal.azure.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-developer) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator).
2. From the Azure portal menu or the **Home** page, select **Create a resource**.
3. Search for and select **Function App** and select **Create**.
4. On the **Create Function App** page, select **Consumption**, then **Select**.
5. On the **Create Function App (Consumption)** page, in the **Basics** tab, create a function app using the settings as specified in the following table:

    | Setting | Suggested value | Description |
    | --- | --- | --- |
    | **Subscription** | Your subscription | The subscription under which the new function app is created. |
    | **[Resource Group](/en-us/azure/azure-resource-manager/management/overview)** | *myResourceGroup* | Select the resource group used to set up the [Azure Communications Service](/en-us/azure/communication-services/quickstarts/create-communication-resource?tabs=windows&amp;pivots=platform-azp) and [Email Communication Service](/en-us/azure/communication-services/quickstarts/email/create-email-communication-resource?pivots=platform-azp) resources as part of the prerequisites |
    | **Function App name** | Globally unique name | A name that identifies the new function app. Valid characters are `a-z` (case insensitive), `0-9`, and `-`. |
    | **Deploy code or container image** | Code | Option to publish code files or a Docker container. For this tutorial, select **Code**. |
    | **Runtime stack** | .NET | Your preferred programming language. For this tutorial, select **.NET**. |
    | **Version** | 8 (LTS) In-process | Version of the .NET runtime. In-process signifies that you can create and modify functions in the portal, which is recommended for this guide |
    | **Region** | Preferred region | Select a [region](https://azure.microsoft.com/regions/) that's near you or near other services that your functions can access. |
    | **Operating System** | Windows | The operating system is preselected for you based on your runtime stack selection. |
6. Select **Review + create** to review the app configuration selections and then select **Create**. Deployment takes a few minutes.
7. Once deployed, select **Go to resource** to view your new function app.

### 1.1 Create an HTTP trigger function

After the Azure Function app is created, create an HTTP trigger function. The HTTP trigger lets you invoke a function with an HTTP request. Your Microsoft Entra custom authentication extension links to this HTTP trigger function.

1. Within your **Function App**, from the menu select **Functions**.
2. Select **Create function**.
3. In the **Create Function** window, under **Select a template**, search for and select the **HTTP trigger** template. Select **Next**.
4. Under **Template details**, enter *CustomAuthenticationExtensionsAPI* for the **Function Name** property.
5. For the **Authorization level**, select **Function**.
6. Select **Create**.

### 1.2 Edit the function

The code starts with reading the incoming JSON object. Microsoft Entra ID sends the [JSON object](/en-us/entra/identity-platform/custom-claims-provider-reference) to your API. In this example, it reads the email address (identifier) and the OTP. Then, the code sends the details to the communications service to send the email using a [dynamic template](https://sendgrid.com/en-us/solutions/email-api/dynamic-email-templates).

This how-to guide demonstrates the OTP send event using Azure Communication Services and SendGrid. Use the tabs to select your implementation.

# [Azure Communication Services](#tab/azure-communication-services)
1. From the menu, select **Code + Test**.
2. Replace the entire code with the following code snippet.

    ```csharp
    using System.Dynamic;
    using System.Text.Json;
    using System.Text.Json.Nodes;
    using System.Text.Json.Serialization;
    using Azure.Communication.Email;
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Http.HttpResults;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.Functions.Worker;
    using Microsoft.Extensions.Logging;
    
    namespace Company.AuthEvents.OnOtpSend.CustomEmailACS
    {
        public class CustomEmailACS
        {
            private readonly ILogger<CustomEmailACS> _logger;
    
            public CustomEmailACS(ILogger<CustomEmailACS> logger)
            {
                _logger = logger;
            }
    
            [Function("OnOtpSend_CustomEmailACS")]
            public async Task<IActionResult> RunAsync([HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequest req)
            {
                _logger.LogInformation("C# HTTP trigger function processed a request.");
    
                // Get the request body
                string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
                JsonNode jsonPayload = JsonNode.Parse(requestBody)!;
    
                // Get OTP and mail to
                string emailTo = jsonPayload["data"]!["otpContext"]!["identifier"]!.ToString();
                string otp = jsonPayload["data"]!["otpContext"]!["onetimecode"]!.ToString();
    
                // Send email
                await SendEmailAsync(emailTo, otp);
    
                // Prepare response
                ResponseObject responseData = new ResponseObject("microsoft.graph.OnOtpSendResponseData");
                responseData.Data.Actions = new List<ResponseAction>() { new ResponseAction(
                    "microsoft.graph.OtpSend.continueWithDefaultBehavior") };
    
                return new OkObjectResult(responseData);
            }
    
            private async Task SendEmailAsync(string emailTo, string code)
            {
                // Get app settings
                var connectionString = Environment.GetEnvironmentVariable("mail_connectionString");
                var sender = Environment.GetEnvironmentVariable("mail_sender");
                var subject = Environment.GetEnvironmentVariable("mail_subject");
    
                try
                {
                    if (!string.IsNullOrEmpty(connectionString))
                    {
                        var emailClient = new EmailClient(connectionString);
                        var body = EmailTemplate.GenerateBody(code);
    
                        _logger.LogInformation($"Sending OTP to {emailTo}");
    
                        EmailSendOperation emailSendOperation = await emailClient.SendAsync(
                        Azure.WaitUntil.Started,
                        sender,
                        emailTo,
                        subject,
                        body);
                    }
                }
                catch (System.Exception ex)
                {
                    _logger.LogError(ex.Message);
                }
            }
        }
    
        public class ResponseObject
        {
            [JsonPropertyName("data")]
            public Data Data { get; set; }
    
            public ResponseObject(string dataType)
            {
                Data = new Data(dataType);
            }
        }
    
        public class Data
        {
            [JsonPropertyName("@odata.type")]
            public string DataType { get; set; }
            [JsonPropertyName("actions")]
            public List<ResponseAction> Actions { get; set; }
    
            public Data(string dataType)
            {
                DataType = dataType;
            }
        }
    
        public class ResponseAction
        {
            [JsonPropertyName("@odata.type")]
            public string DataType { get; set; }
    
            public ResponseAction(string dataType)
            {
                DataType = dataType;
            }
        }
    
        public class EmailTemplate
        {
            public static string GenerateBody(string oneTimeCode)
            {
                return @$"<html><body>
                <div style='background-color: #1F6402!important; padding: 15px'>
                    <table>
                    <tbody>
                        <tr>
                            <td colspan='2' style='padding: 0px;font-family: "Segoe UI Semibold", "Segoe UI Bold", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif;font-size: 17px;color: white;'>Woodgrove Groceries live demo</td>
                        </tr>
                        <tr>
                            <td colspan='2' style='padding: 15px 0px 0px;font-family: "Segoe UI Light", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif;font-size: 35px;color: white;'>Your Woodgrove verification code</td>
                        </tr>
                        <tr>
                            <td colspan='2' style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'> To access <span style='font-family: "Segoe UI Bold", "Segoe UI Semibold", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif; font-size: 14px; font-weight: bold; color: white;'>Woodgrove Groceries</span>'s app, please copy and enter the code below into the sign-up or sign-in page. This code is valid for 30 minutes. </td>
                        </tr>
                        <tr>
                            <td colspan='2' style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'>Your account verification code:</td>
                        </tr>
                        <tr>
                            <td style='padding: 0px;font-family: "Segoe UI Bold", "Segoe UI Semibold", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif;font-size: 25px;font-weight: bold;color: white;padding-top: 5px;'>
                            {oneTimeCode}</td>
                            <td rowspan='3' style='text-align: center;'>
                                <img src='https://woodgrovedemo.com/custom-email/shopping.png' style='border-radius: 50%; width: 100px'>
                            </td>
                        </tr>
                        <tr>
                            <td style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'> If you didn't request a code, you can ignore this email. </td>
                        </tr>
                        <tr>
                            <td style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'> Best regards, </td>
                        </tr>
                        <tr>
                            <td>
                                <img src='https://woodgrovedemo.com/Company-branding/headerlogo.png' height='20'>
                            </td>
                            <td style='font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white; text-align: center;'>
                                <a href='https://woodgrovedemo.com/Privacy' style='color: white; text-decoration: none;'>Privacy Statement</a>
                            </td>
                        </tr>
                    </tbody>
                    </table>
                </div>
                </body></html>";
            }
        }
    }
    ```
3. Select **Get Function Url**, and copy the **Function key** URL, which is henceforth used and referred to as `{Function_Url}`. Close the function.

# [SendGrid](#tab/sendgrid)
1. From the menu, select **Code + Test**.
2. Replace the entire code with the following code snippet.

    ```csharp
    using System.Dynamic;
    using System.Text.Json;
    using System.Text.Json.Nodes;
    using System.Text.Json.Serialization;
    using Azure.Communication.Email;
    using Microsoft.AspNetCore.Http;
    using Microsoft.AspNetCore.Http.HttpResults;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.Functions.Worker;
    using Microsoft.Extensions.Logging;
    
    namespace Company.AuthEvents.OnOtpSend.CustomEmailSendGrid
    {
        public class CustomEmailSendGrid
        {
            private readonly ILogger<CustomEmailSendGrid> _logger;
    
            public CustomEmailSendGrid(ILogger<CustomEmailSendGrid> logger)
            {
                _logger = logger;
            }
    
            [Function("OnOtpSend_CustomEmailSendGrid")]
            public async Task<IActionResult> RunAsync([HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequest req)
            {
                _logger.LogInformation("C# HTTP trigger function processed a request.");
    
                // Get the request body
                string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
                JsonNode jsonPayload = JsonNode.Parse(requestBody)!;
    
                // Get OTP and mail to
                string emailTo = jsonPayload["data"]!["otpContext"]!["identifier"]!.ToString();
                string otp = jsonPayload["data"]!["otpContext"]!["onetimecode"]!.ToString();
    
                // Send email
                await SendEmailAsync(emailTo, otp);
    
                // Prepare response
                ResponseObject responseData = new ResponseObject("microsoft.graph.OnOtpSendResponseData");
                responseData.Data.Actions = new List<ResponseAction>() { new ResponseAction(
                    "microsoft.graph.OtpSend.continueWithDefaultBehavior") };
    
                return new OkObjectResult(responseData);
            }
    
            private async Task SendEmailAsync(string emailTo, string code)
            {
                // Get app settings
                var apiKey = Environment.GetEnvironmentVariable("mail_sendgridKey");
                var sender = Environment.GetEnvironmentVariable("mail_sender");
                var senderName = Environment.GetEnvironmentVariable("mail_senderName");
                var template = Environment.GetEnvironmentVariable("mail_template");
    
                _logger.LogInformation($"Sending OTP to {emailTo}");
    
                try
                {
                    if (!string.IsNullOrEmpty(apiKey))
                    {
                        var client = new HttpClient();
                        var request = new HttpRequestMessage(HttpMethod.Post, "https://api.sendgrid.com/v3/mail/send");
                        request.Headers.Add("Authorization", $"Bearer {apiKey}");
    
                        SendGridMessage msg = new SendGridMessage()
                        {
                            template_id = template,
                            from = new Person { email = sender, name = senderName },
                            personalizations = new List<Personalization> {
    
                    new Personalization(emailTo, code)
                    }
                        };
    
                        request.Content = new StringContent(msg.ToString(), null, "application/json");
    
                        var response = await client.SendAsync(request);
                        _logger.LogInformation($"Sendgrid response: {response.StatusCode}");
                        response.EnsureSuccessStatusCode();
                        _logger.LogInformation(await response.Content.ReadAsStringAsync());
                    }
                }
                catch (System.Exception ex)
                {
                    _logger.LogError(ex.Message);
                }
            }
        }
    
        public class ResponseObject
        {
            [JsonPropertyName("data")]
            public Data Data { get; set; }
    
            public ResponseObject(string dataType)
            {
                Data = new Data(dataType);
            }
        }
    
        public class Data
        {
            [JsonPropertyName("@odata.type")]
            public string DataType { get; set; }
            [JsonPropertyName("actions")]
            public List<ResponseAction> Actions { get; set; }
    
            public Data(string dataType)
            {
                DataType = dataType;
            }
        }
    
        public class ResponseAction
        {
            [JsonPropertyName("@odata.type")]
            public string DataType { get; set; }
    
            public ResponseAction(string dataType)
            {
                DataType = dataType;
            }
        }
    
        public class EmailTemplate
        {
            public static string GenerateBody(string oneTimeCode)
            {
                return @$"<html><body>
                <div style='background-color: #1F6402!important; padding: 15px'>
                    <table>
                    <tbody>
                        <tr>
                            <td colspan='2' style='padding: 0px;font-family: "Segoe UI Semibold", "Segoe UI Bold", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif;font-size: 17px;color: white;'>Woodgrove Groceries live demo</td>
                        </tr>
                        <tr>
                            <td colspan='2' style='padding: 15px 0px 0px;font-family: "Segoe UI Light", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif;font-size: 35px;color: white;'>Your Woodgrove verification code</td>
                        </tr>
                        <tr>
                            <td colspan='2' style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'> To access <span style='font-family: "Segoe UI Bold", "Segoe UI Semibold", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif; font-size: 14px; font-weight: bold; color: white;'>Woodgrove Groceries</span>'s app, please copy and enter the code below into the sign-up or sign-in page. This code is valid for 30 minutes. </td>
                        </tr>
                        <tr>
                            <td colspan='2' style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'>Your account verification code:</td>
                        </tr>
                        <tr>
                            <td style='padding: 0px;font-family: "Segoe UI Bold", "Segoe UI Semibold", "Segoe UI", "Helvetica Neue Medium", Arial, sans-serif;font-size: 25px;font-weight: bold;color: white;padding-top: 5px;'>
                            {oneTimeCode}</td>
                            <td rowspan='3' style='text-align: center;'>
                                <img src='https://woodgrovedemo.com/custom-email/shopping.png' style='border-radius: 50%; width: 100px'>
                            </td>
                        </tr>
                        <tr>
                            <td style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'> If you didn't request a code, you can ignore this email. </td>
                        </tr>
                        <tr>
                            <td style='padding: 25px 0px 0px;font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white;'> Best regards, </td>
                        </tr>
                        <tr>
                            <td>
                                <img src='https://woodgrovedemo.com/Company-branding/headerlogo.png' height='20'>
                            </td>
                            <td style='font-family: "Segoe UI", Tahoma, Verdana, Arial, sans-serif;font-size: 14px;color: white; text-align: center;'>
                                <a href='https://woodgrovedemo.com/Privacy' style='color: white; text-decoration: none;'>Privacy Statement</a>
                            </td>
                        </tr>
                    </tbody>
                    </table>
                </div>
                </body></html>";
            }
        }
    
        /********* SendGrid data ********/
        public class SendGridMessage
        {
            public List<Personalization> personalizations { get; set; }
            public string template_id { get; set; }
            public Person from { get; set; }
    
            public override string ToString()
            {
                return JsonSerializer.Serialize(this, new JsonSerializerOptions { WriteIndented = true });
            }
        }
    
        public class Personalization
        {
            public Personalization(string to, string otp)
            {
                this.to = new List<Person>() { new Person() { email = to } };
                this.dynamic_template_data = new DynamicTemplateData() { otp = otp };
            }
    
            public List<Person> to { get; set; }
            public DynamicTemplateData dynamic_template_data { get; set; }
        }
    
        public class DynamicTemplateData
        {
            public string otp { get; set; }
        }
    
        public class Person
        {
            public string email { get; set; }
    
            [JsonIgnore(Condition = JsonIgnoreCondition.WhenWritingNull)]
            public string name { get; set; }
        }
    
        public class OTPCodeTemplateData
        {
            [JsonPropertyName("otp")]
            public string OTPCode { get; set; }
    
        }
    }
    ```
3. Select **Get Function Url**, and copy the **Function key** URL, which is henceforth used and referred to as `{Function_Url}`. Close the function.

---

## Step 2: Add connection strings to the Azure Function

Connection strings enable your function app to connect and authenticate to the mail relay service. For both Azure Communication Services and SendGrid, add these connection strings to your Azure Function app as environment variables.

# [Azure Communication Services](#tab/azure-communication-services)
### 2.1: Extract the connection strings and service endpoints from your Azure Communication Services resource

You can access your Communication Services connection strings and service endpoints from the Azure portal or programmatically with Azure Resource Manager APIs.

1. From the **Home** page in the [Azure portal](https://portal.azure.com/#home), open the portal menu, search for and select **All resources**.
2. Search for and select the **Azure Communications Service** created as part of the Prerequisites to this article.
3. In the left pane, select the **Settings** dropdown, then select **Keys**.
4. Copy the **Endpoint**, and from **Primary key** copy the values for **Key** and **Connection string**.

    [![Screenshot of the Azure Communications Service Keys page showing the endpoint and key locations.](media/custom-extension-email-otp-get-started/extract-communications-service-keys.png)](media/custom-extension-email-otp-get-started/extract-communications-service-keys.png#lightbox)

### 2.2: Add the connection strings to the Azure Function

1. Navigate back to the Azure Function you created in Create an Azure Function app.
2. From **Overview** page of your function app, in the left menu, select **Settings** &gt; **Environment variables** add the following App settings. Once all the settings are added, select **Apply**, then **Confirm**.

    | Setting | Value (Example) | Description |
    | --- | --- | --- |
    | **mail\_connectionString** | `https://ciamotpcommsrvc.unitedstates.communication.azure.com/:accesskey=` | The Azure Communication Services endpoint |
    | **mail\_sender** | from.email@myemailprovider.com | The from email address. |
    | **mail\_subject** | Your account verification code | The subject of the email. |

# [SendGrid](#tab/sendgrid)
### 2.1: Add the connection strings to the Azure Function

1. Navigate back to the Azure Function you created in Create an Azure Function app.
2. From **Overview** page of your function app, in the left menu, select **Settings** &gt; **Environment variables** add the following App settings. Once all the settings are added, select **Apply**, then **Confirm**.

    | Setting | Value (Example) | Description |
    | --- | --- | --- |
    | **mail\_sendgridKey** | SG.12a3456789... | The SendGrid API Key. |
    | **mail\_sender** | from.email@myemailprovider.com | The from email address. |
    | **mail\_senderName** | Contoso | The name of the From Email. |
    | **mail\_template** | d-01234567.... | The SendGrid dynamic template ID. |

---

## Step 3: Register a custom authentication extension

In this step, you configure a custom authentication extension, which Microsoft Entra ID uses to call your Azure Function. The custom authentication extension contains information about your REST API endpoint, the claims that it parses from your REST API, and how to authenticate to your REST API. Use either the Azure portal or Microsoft Graph to register an application to authenticate your custom authentication extension to your Azure Function.

# [Azure portal](#tab/azure-portal)
### Register a custom authentication extension

1. Sign in to the [Azure portal](https://portal.azure.com) as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-developer) and [Authentication Administrator](../identity/role-based-access-control/permissions-reference#authentication-administrator).
2. Search for and select **Microsoft Entra ID** and select **Enterprise applications**.
3. Select **Custom authentication extensions**, and then select **Create a custom extension**.
4. In **Basics**, select the **EmailOtpSend** event type and select **Next**.

    [![Screenshot of the Azure portal highlighting the email OTP send event.](media/custom-extension-email-otp-get-started/select-email-otp-send-event.png)](media/custom-extension-email-otp-get-started/select-email-otp-send-event.png#lightbox)
5. In the **Endpoint Configuration** tab, fill in the following properties, then select **Next** to continue.

    - **Name** - A name for your custom authentication extension. For example, *Email OTP Send*.
    - **Target Url** - The `{Function_Url}` of your Azure Function URL. Navigate to the **Overview** page of your Azure Function app, then select the function you created. In the function **Overview** page, select **Get Function Url** and use the copy icon to copy the **customauthenticationextension\_extension (System key)** URL.
    - **Description** - A description for your custom authentication extensions.
6. In the **API Authentication** tab, select the **Create new app registration** option to create an app registration that represents your *function app*.
7. Give the app a name, for example **Azure Functions authentication events API**, and select **Next**.
8. In the **Applications** tab, select the application to associate with the custom authentication extension. Select **Next**. You have the option to apply it across the whole tenant by checking the box. Select **Next** to continue.
9. In the **Review** tab, check that the details are correct for the custom authentication extension. Note the **App ID** under **API Authentication**, which is needed to [configure authentication for your Azure Function](custom-extension-tokenissuancestart-setup#configure-authentication-for-your-azure-function) in your Azure Function app. Select **Create**.

# [Microsoft Graph](#tab/microsoft-graph)
### 3.1 Register an application in Graph Explorer

1. Sign in to [Graph Explorer](https://aka.ms/ge) using an account whose home tenant is the tenant you wish to manage your custom authentication extension in. The account must have the privileges to create and manage an application registration in the tenant.
2. Run the following request.

    ```http
    POST https://graph.microsoft.com/v1.0/applications
    Content-type: application/json
    
    {
        "displayName": "authenticationeventsAPI"
    }
    ```
3. From the response, record the value of **id** and **appId** of the newly created app registration. These values are referenced in this article as `{authenticationeventsAPI_ObjectId}` and `{authenticationeventsAPI_AppId}` respectively.
4. Create a service principal in the tenant for the **authenticationeventsAPI** app registration.
5. Run the following request in Graph Explorer. Replace `{authenticationeventsAPI_AppId}` with the value of **appId** that you recorded from the previous step.

    ```http
    POST https://graph.microsoft.com/v1.0/servicePrincipals
    Content-type: application/json
    
    {
        "appId": "{authenticationeventsAPI_AppId}"
    }
    ```

### 3.2 Set the App ID URI, access token version, and required resource access

Update the newly created application to set the application ID URI value, the access token version, and the required resource access.

1. In Graph Explorer, run the following request.

- Set the application ID URI value in the *identifierUris* property. Replace `{Function_Url_Hostname}` with the hostname of the `{Function_Url}` you recorded earlier.
- Set the `{authenticationeventsAPI_AppId}` value with the **appId** that you recorded earlier.
- An example value is `api://authenticationeventsAPI.azurewebsites.net/00001111-aaaa-2222-bbbb-3333cccc4444`. Take note of this value. You will need it later in this article in place of `{functionApp_IdentifierUri}`.

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

### 3.3 Register a custom authentication extension

Next, you register the custom authentication extension and associating it with the app registration for the Azure Function, and your Azure Function endpoint `{Function_Url}`.

1. In Graph Explorer, run the following request. Replace `{Function_Url}` with the hostname of your Azure Function app. Replace `{functionApp_IdentifierUri}` with the identifierUri used in the previous step.

    - You need the *CustomAuthenticationExtension.ReadWrite.All* delegated permission.

    ```http
    POST https://graph.microsoft.com/beta/identity/customAuthenticationExtensions
    Content-type: application/json
    
    {
        "@odata.type": "#microsoft.graph.OnOtpSendCustomExtension",
        "displayName": "onEmailOtpSendCustomExtension",
        "description": "Use an external Email provider to send OTP Codes.",
        "authenticationConfiguration": {
            "@odata.type": "#microsoft.graph.azureAdTokenAuthentication",
            "resourceId": "{functionApp_IdentifierUri}"
        },
        "endpointConfiguration": {
            "@odata.type": "#microsoft.graph.httpRequestEndpoint",
            "targetUrl": "{Function_Url}"
        }
    }
    ```
2. Record the **id** value of the created custom email OTP provider object, which is used later in this article in place of `{customExtensionObjectId}`.

### 3.4 Assign a custom email provider to your app

To use the custom emails, you must assign a custom email provider to your application. The custom email provider relies on the custom authentication extension configured with the **OTP send** event listener.

Follow these steps to connect the *My Test application* with your custom authentication extension:

1. Sign in to [Graph Explorer](https://aka.ms/ge) using an account whose home tenant is the tenant you wish to manage your custom authentication extension in.
2. Run the following request. Replace `{App_to_sendotp_ID}` with the app ID of *My Test application* recorded earlier. Replace `{customExtensionObjectId}` with the custom authentication extension ID recorded earlier.

    - You need the *EventListener.ReadWrite.All* delegated permission.

    ```json
    POST https://graph.microsoft.com/beta/identity/authenticationEventListeners
    Content-type: application/json
    
    {
        "@odata.type": "#microsoft.graph.onEmailOtpSendListener",
        "conditions": {
            "applications": {
                "includeAllApplications": false,
                "includeApplications": [
                    {
                        "appId": "{App_to_sendotp_ID}"
                    }
                ]
            }
        },
        "priority": 500,
        "handler": {
            "@odata.type": "#microsoft.graph.onOtpSendCustomExtensionHandler",
            "customExtension": {
                "id": "{customExtensionObjectId}"
            }
        }
    }
    ```
3. Record the **id** value of the created listener object, which is used later in this article in place of `{customListenerObjectId}`.

---

### Grant admin consent

After your custom authentication extension is created, open the application from the portal under **App registrations** and select **API permissions**.

From the **API permissions** page, select the **Grant admin consent for "YourTenant"** button to give admin consent to the registered app, which allows the custom authentication extension to authenticate to your API. The custom authentication extension uses `client_credentials` to authenticate to the Azure Function App using the `Receive custom authentication extension HTTP requests` permission.

The following screenshot shows how to grant permissions.

[![Screenshot of Azure portal and how to grant admin consent.](media/custom-extension-email-otp-get-started/application-grant-consent.png)](media/custom-extension-email-otp-get-started/application-grant-consent.png#lightbox)

## Step 4: Configure an OpenID Connect app to test with

To get a token and test the custom authentication extension, you can use the https://jwt.ms app. It's a Microsoft-owned web application that displays the decoded contents of a token (the contents of the token never leave your browser).

Follow these steps to register the **jwt.ms** web application:

### 4.1 Register a test web application

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-developer).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select **New registration**.
4. Enter a **Name** for the application. For example, **My Test application**.
5. Under **Supported account types**, select **Accounts in this organizational directory only**.
6. In the **Select a platform** dropdown in **Redirect URI**, select **Web**, and then enter `https://jwt.ms` in the URL text box.
7. Select **Register** to complete the app registration.
8. In your app registration, under **Overview**, copy the **Application (client) ID**, which is used later and referred to as the `{App_to_sendotp_ID}`. In Microsoft Graph, it's referenced by the **appId** property.

The following screenshot shows how to register the *My Test application*.

[![Screenshot that shows how to select the supported account type and redirect URI.](media/custom-extension-email-otp-get-started/register-test-web-application.png)](media/custom-extension-email-otp-get-started/register-test-web-application.png#lightbox)

### 4.1 Get the application ID

In your app registration, under **Overview**, copy the **Application (client) ID**. The app ID is referred to as the `{App_to_sendotp_ID}` in later steps. In Microsoft Graph, it's referenced by the **appId** property.

### 4.2 Enable implicit flow

The **jwt.ms** test application uses the implicit flow. Enable implicit flow in *My Test application* registration:

Important

Microsoft recommends using the most secure authentication flow available. The authentication flow used for testing in this procedure requires a high degree of trust in the application, and carries risks that aren't present in other flows. This approach shouldn't be used for authenticating users to your production apps ([learn more](v2-oauth2-implicit-grant-flow)).

1. Under **Manage**, select **Authentication**.
2. Under **Implicit grant and hybrid flows**, select the **ID tokens (used for implicit and hybrid flows)** checkbox.
3. Select **Save**.

## Step 5: Protect your Azure Function

Microsoft Entra custom authentication extension uses server to server flow to obtain an access token that is sent in the HTTP `Authorization` header to your Azure function. When publishing your function to Azure, especially in a production environment, you need to validate the token sent in the authorization header.

To protect your Azure function, follow these steps to integrate Microsoft Entra authentication, for validating incoming tokens with your *Azure Functions authentication events API* application registration.

Note

If the Azure function app is hosted in a different Azure tenant than the tenant in which your custom authentication extension is registered, skip to using OpenID Connect identity provider step.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate and select the function app you previously published.
3. Select **Authentication** in the menu on the left.
4. Select **Add Identity provider**.
5. From the dropdown menu, select **Microsoft** as the identity provider.
6. Under **App registration**-&gt;**App registration type**, select **Pick an existing app registration in this directory** and pick the *Azure Functions authentication events API* app registration you previously created when registering the custom email provider.
7. Add the **Client secret** expiration for the app.
8. Under **Unauthenticated requests**, select **HTTP 401 Unauthorized** as the identity provider.
9. Unselect the **Token store** option.
10. Select **Add** to add authentication to your Azure Function.

[![Screenshot that shows how to add authentication to your function app.](media/custom-extension-email-otp-get-started/configure-auth-function-app.png)](media/custom-extension-email-otp-get-started/configure-auth-function-app.png#lightbox)

### 5.1 Using OpenID Connect identity provider

If you configured the Microsoft identity provider, skip this step. Otherwise, if the Azure Function is hosted under a different tenant than the tenant in which your custom authentication extension is registered, follow these steps to protect your function:

1. Sign in to the [Azure portal](https://portal.azure.com), then navigate and select the function app you previously published.
2. Select **Authentication** in the left pane.
3. Select **Add Identity provider**.
4. Select **OpenID Connect** as the identity provider.
5. Provide a name, such as *Contoso Microsoft Entra ID*.
6. Under the **Metadata entry**, enter the following URL to the **Document URL**. Replace the `{tenantId}` with your Microsoft Entra tenant ID, and `{tenantname}` with the name of your tenant without the 'onmicrosoft.com'.

    ```http
    https://{tenantname}.ciamlogin.com/{tenantId}/v2.0/.well-known/openid-configuration
    ```
7. Under the **App registration**, enter the application ID (client ID) of the *Azure Functions authentication events API* app registration you created previously.
8. In the Microsoft Entra admin center:

    1. Select the *Azure Functions authentication events API* app registration you created previously.
    2. Select **Certificates & secrets** &gt; **Client secrets** &gt; **New client secret**.
    3. Add a description for your client secret.
    4. Select an expiration for the secret or specify a custom lifetime.
    5. Select **Add**.
    6. Record the **secret's value** for use in your client application code. This secret value is never displayed again after you leave this page.
9. Back to the Azure Function, under the **App registration**, enter the **Client secret**.
10. Unselect the **Token store** option.
11. Select **Add** to add the OpenID Connect identity provider.

## Step 6: Test the application

To test your custom email provider, follow these steps:

1. Open a new private browser and navigate and sign-in through the following URL.

    ```http
    https://{tenantname}.ciamlogin.com/{tenant-id}/oauth2/v2.0/authorize?client_id={App_to_sendotp_ID}&response_type=id_token&redirect_uri=https://jwt.ms&scope=openid&state=12345&nonce=12345
    ```
2. Replace `{tenant-id}` with your tenant ID, tenant name, or one of your verified domain names. For example, `contoso.onmicrosoft.com`.
3. Replace `{tenantname}` with the name of your tenant without the 'onmicrosoft.com'.
4. Replace `{App_to_sendotp_ID}` with the My Test application registration ID.
5. Ensure you sign in using an [Email One Time Passcode account](/en-us/entra/external-id/one-time-passcode). Then select **Send Code**. Ensure that the code sent to the registered email addresses uses the custom provider registered above.

## Step 7: Fall back to Microsoft Provider

If an error occurs within your extension API, by default Entra ID does not send an OTP to the user. You can instead set the behavior on error to fall back to the Microsoft Provider.

To enable this, run the following request. Replace `{customListenerObjectId}` with the custom authentication listener ID recorded earlier.

- You need the *EventListener.ReadWrite.All* delegated permission.

```json
PATCH https://graph.microsoft.com/beta/identity/authenticationEventListeners/{customListenerOjectId}

{
    "@odata.type": "#microsoft.graph.onEmailOtpSendListener",
    "handler": {
        "@odata.type": "#microsoft.graph.onOtpSendCustomExtensionHandler",
        "configuration": {
            "behaviorOnError": {
                "@odata.type": "#microsoft.graph.fallbackToMicrosoftProviderOnError"
            }
        }
    }
}
```