---
layout: Conceptual
title: Add API connectors to self-service sign-up flows - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/self-service-sign-up-add-api-connector
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Configure a web API to be used in a user flow.
ms.topic: how-to
ms.date: 2025-04-15T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: e8f1874e-2faf-a639-022f-af09bb4a18a0
document_version_independent_id: 496d4a20-dc6d-fe6e-eab9-a0491f70ff99
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/self-service-sign-up-add-api-connector.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/self-service-sign-up-add-api-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/self-service-sign-up-add-api-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9604f763-9029-7ec5-afc8-90d4424ed394
---

# Add API connectors to self-service sign-up flows - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

To use an [API connector](api-connectors-overview), you first create the API connector and then enable it in a user flow.

Important

- **As of July 12, 2021**, if Microsoft Entra B2B customers set up new Google integrations for use with self-service sign-up for their custom or line-of-business applications, authentication with Google identities won’t work until authentications are moved to system web-views. [Learn more](google-federation#deprecation-of-web-view-sign-in-support).
- **On September 30, 2021**, Google [deprecated embedded web-view sign-in support](https://developers.googleblog.com/2016/08/modernizing-oauth-interactions-in-native-apps.html). If your apps authenticate users with an embedded web-view and you're using Google federation with [Azure AD B2C](/en-us/azure/active-directory-b2c/identity-provider-google) or Microsoft Entra B2B for [external user invitations](google-federation) or [self-service sign-up](identity-providers), Google Gmail users can't authenticate. [Learn more](google-federation#deprecation-of-web-view-sign-in-support).

## Create an API connector

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Overview**.
3. Select **All API connectors**, and then select **New API connector**.

    ![Screenshot of adding a new API connector to External ID.](media/self-service-sign-up-add-api-connector/api-connector-new.png)
4. Provide a display name for the call. For example, **Check approval status**.
5. Provide the **Endpoint URL** for the API call.
6. Choose the **Authentication type** and configure the authentication information for calling your API. Learn how to [Secure your API Connector](self-service-sign-up-secure-api-connector).

    ![Screenshot of configuring an API connector.](media/self-service-sign-up-add-api-connector/api-connector-config.png)
7. Select **Save**.

## The request sent to your API

An API connector materializes as an **HTTP POST** request, sending user attributes ('claims') as key-value pairs in a JSON body. Attributes are serialized similarly to [Microsoft Graph](/en-us/graph/api/resources/user#properties) user properties.

**Example request**

```http
POST <API-endpoint>
Content-type: application/json

{
 "email": "johnsmith@fabrikam.onmicrosoft.com",
 "identities": [ // Sent for Google, Facebook, and Email One Time Passcode identity providers 
     {
     "signInType":"federated",
     "issuer":"facebook.com",
     "issuerAssignedId":"0123456789"
     }
 ],
 "displayName": "John Smith",
 "givenName":"John",
 "surname":"Smith",
 "jobTitle":"Supplier",
 "streetAddress":"1000 Microsoft Way",
 "city":"Seattle",
 "postalCode": "12345",
 "state":"Washington",
 "country":"United States",
 "extension_<extensions-app-id>_CustomAttribute1": "custom attribute value",
 "extension_<extensions-app-id>_CustomAttribute2": "custom attribute value",
 "ui_locales":"en-US"
}
```

Only user properties and custom attributes listed in the **Entra ID** &gt; **External Identities** &gt; **Overview** &gt; **Custom user attributes** experience are available to be sent in the request.

Custom attributes exist in the **extension\_&lt;extensions-app-id&gt;\_AttributeName** format in the directory. Your API should expect to receive claims in this same serialized format. For more information on custom attributes, see [define custom attributes for self-service sign-up flows](user-flow-add-custom-attributes).

Additionally, the claims are typically sent in all request:

- **UI Locales ('ui\_locales')** - An end-user's locales as configured on their device, which your API can use to return internationalized responses.

- **Email Address ('email')** or [**identities ('identities')**](/en-us/graph/api/resources/objectidentity) - these claims can be used by your API to identify the end-user that is authenticating to the application.

Important

If a claim doesn't have a value at the time the API endpoint is called, it isn't sent to the API. Your API should be designed to explicitly check and handle the case in which a claim isn't in the request.

## Enable the API connector in a user flow

Follow these steps to add an API connector to a self-service sign-up user flow.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Overview**.
3. Select **User flows**, and then select the user flow you want to add the API connector to.
4. Select **API connectors**, and then select the API endpoints you want to invoke at the following steps in the user flow:

    - **After federating with an identity provider during sign-up**
    - **Before creating the user**

    ![Selecting which API connector to use for a step in the user flow like 'Before creating the user'.](media/self-service-sign-up-add-api-connector/api-connectors-user-flow-select.png)
5. Select **Save**.

## After federating with an identity provider during sign-up

An API connector at this step in the sign-up process is invoked immediately after the user authenticates with an identity provider (like Google, Facebook, or Microsoft Entra ID). This step precedes the ***attribute collection page***, which is the form presented to the user to collect user attributes.

### Example request sent to the API at this step

```http
POST <API-endpoint>
Content-type: application/json

{
 "email": "johnsmith@fabrikam.onmicrosoft.com",
 "identities": [ // Sent for Google, Facebook, and Email One Time Passcode identity providers 
     {
     "signInType":"federated",
     "issuer":"facebook.com",
     "issuerAssignedId":"0123456789"
     }
 ],
 "displayName": "John Smith",
 "givenName":"John",
 "lastName":"Smith",
 "ui_locales":"en-US"
}
```

The exact claims sent to the API depend on which information is provided by the identity provider. 'email' is always sent.

### Expected response types from the web API at this step

When the web API receives an HTTP request from Microsoft Entra ID during a user flow, it can return these responses:

- Continuation response
- Blocking response

#### Continuation response

A continuation response indicates that the user flow should continue to the next step: the attribute collection page.

In a continuation response, the API can return a claim that:

- Prefills the input field in the attribute collection page.

See an example of a continuation response.

#### Blocking Response

A blocking response exits the user flow. The API can purposely issue a blocking response to stop the continuation of the user flow by displaying a block page to the user. The block page displays the `userMessage` provided by the API.

See an example of a blocking response.

## Before creating the user

An API connector at this step in the sign-up process is invoked after the attribute collection page, if one is included. This step is always invoked before a user account is created in Microsoft Entra ID.

### Example request sent to the API at this step

```http
POST <API-endpoint>
Content-type: application/json

{
 "email": "johnsmith@fabrikam.onmicrosoft.com",
 "identities": [ // Sent for Google, Facebook, and Email One Time Passcode identity providers 
     {
     "signInType":"federated",
     "issuer":"facebook.com",
     "issuerAssignedId":"0123456789"
     }
 ],
 "displayName": "John Smith",
 "givenName":"John",
 "surname":"Smith",
 "jobTitle":"Supplier",
 "streetAddress":"1000 Microsoft Way",
 "city":"Seattle",
 "postalCode": "12345",
 "state":"Washington",
 "country":"United States",
 "extension_<extensions-app-id>_CustomAttribute1": "custom attribute value",
 "extension_<extensions-app-id>_CustomAttribute2": "custom attribute value",
 "ui_locales":"en-US"
}
```

The exact claims sent to the API depend on which information is collected from the user or is provided by the identity provider.

### Expected response types from the web API at this step

When the web API receives an HTTP request from Microsoft Entra ID during a user flow, it can return these responses:

- Continuation response
- Blocking response
- Validation response

#### Continuation response

A continuation response indicates that the user flow should continue to the next step: create the user in the directory.

In a continuation response, the API can return a claim that:

- Overrides any value already assigned to the claim from the attribute collection page.

See an example of a continuation response.

#### Blocking Response

A blocking response exits the user flow. The API can purposely issue a blocking response to stop the continuation of the user flow by displaying a block page to the user. The block page displays the `userMessage` provided by the API.

See an example of a blocking response.

### Validation-error response

When the API responds with a validation-error response, the user flow stays on the attribute collection page, and a `userMessage` is displayed to the user. The user can then edit and resubmit the form. This type of response can be used for input validation.

See an example of a validation-error response.

## Example responses

### Example of a continuation response

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "Continue",
    "postalCode": "12349", // return claim
    "extension_<extensions-app-id>_CustomAttribute": "value" // return claim
}
```

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| version | String | Yes | The version of your API. |
| action | String | Yes | Value must be `Continue`. |
| &lt;builtInUserAttribute&gt; | &lt;attribute-type&gt; | No | Values can be stored in the directory if they selected as a **Claim to receive** in the API connector configuration and **User attributes** for a user flow. Values can be returned in the token if selected as an **Application claim**. |
| &lt;extension\_{extensions-app-id}\_CustomAttribute&gt; | &lt;attribute-type&gt; | No | The claim doesn't need to contain `_<extensions-app-id>_`, it's *optional*. Returned values can overwrite values collected from a user. |

### Example of a blocking response

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "ShowBlockPage",
    "userMessage": "There was an error with your request. Please try again or contact support.",
}

```

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| version | String | Yes | The version of your API. |
| action | String | Yes | Value must be `ShowBlockPage` |
| userMessage | String | Yes | Message to display to the user. |

**End-user experience with a blocking response**

![An example image of what the end-user experience looks like after an API returns a blocking response.](media/api-connectors-overview/blocking-page-response.png)

### Example of a validation-error response

```http
HTTP/1.1 400 Bad Request
Content-type: application/json

{
    "version": "1.0.0",
    "status": 400,
    "action": "ValidationError",
    "userMessage": "Please enter a valid Postal Code.",
}
```

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| version | String | Yes | The version of your API. |
| action | String | Yes | Value must be `ValidationError`. |
| status | Integer / String | Yes | Must be value `400`, or `"400"` for a ValidationError response. |
| userMessage | String | Yes | Message to display to the user. |

Note

HTTP status code has to be "400" in addition to the "status" value in the body of the response.

**End-user experience with a validation-error response**

![An example image of what the end-user experience looks like after an API returns a validation-error response.](media/api-connectors-overview/validation-error-postal-code.png)

## Best practices and how to troubleshoot

### Using serverless cloud functions

Serverless functions, like [HTTP triggers in Azure Functions](/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger), provide a way create API endpoints to use with the API connector. You can use the serverless cloud function to, [for example](code-samples-self-service-sign-up#api-connector-azure-function-quickstarts), perform validation logic and limit sign-ups to specific email domains. The serverless cloud function can also call and invoke other web APIs, data stores, and other cloud services for complex scenarios.

### Best practices

Ensure that:

- Your API is following the API request and response contracts as outlined earlier.
- The **Endpoint URL** of the API connector points to the correct API endpoint.
- Your API explicitly checks for null values of received claims that it depends on.
- Your API implements an authentication method outlined in [secure your API Connector](self-service-sign-up-secure-api-connector).
- Your API responds as quickly as possible to ensure a fluid user experience.
    - Microsoft Entra ID waits for a maximum of *20 seconds* to receive a response. If none is received, it makes *one more attempt (retry)* at calling your API.
    - If using a serverless function or scalable web service, use a hosting plan that keeps the API "awake" or "warm" in production. For Azure Functions, we recommended using at a minimum the [Premium plan](/en-us/azure/azure-functions/functions-scale#overview-of-plans).
- Ensure high availability of your API.
- Monitor and optimize performance of downstream APIs, databases, or other dependencies of your API.
- Your endpoints must comply with the Microsoft Entra TLS and cipher security requirements. For more information, see [TLS and cipher suite requirements](/en-us/azure/active-directory-b2c/https-cipher-tls-requirements).

### Use logging

In general, it's helpful to use the logging tools enabled by your web API service, like [Application insights](/en-us/azure/azure-functions/functions-monitoring), to monitor your API for unexpected error codes, exceptions, and poor performance.

- Monitor for HTTP status codes that aren't HTTP 200 or 400.
- A 401 or 403 HTTP status code typically indicates there's an issue with your authentication. Double-check your API's authentication layer and the corresponding configuration in the API connector.
- Use more aggressive levels of logging (for example "trace" or "debug") in development if needed.
- Monitor your API for long response times.