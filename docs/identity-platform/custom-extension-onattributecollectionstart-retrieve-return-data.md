---
layout: Conceptual
title: Retrieve and return data from an OnAttributeCollectionStart event - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-extension-onattributecollectionstart-retrieve-return-data
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Reference documentation for a custom authentication extension that invokes the OnAttributeCollectionStart event for External ID customer configurations.
manager: pmwongera
ms.date: 2025-09-16T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: 5766eb46-a404-0f6f-d9a6-1a721fca6e7a
document_version_independent_id: 5766eb46-a404-0f6f-d9a6-1a721fca6e7a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-extension-onattributecollectionstart-retrieve-return-data.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-extension-onattributecollectionstart-retrieve-return-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-extension-onattributecollectionstart-retrieve-return-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 6472d1b6-a1e0-c269-ff99-dd4750552b8c
---

# Retrieve and return data from an OnAttributeCollectionStart event - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

To modify the sign-up experience for your customer self-service sign-up user flows, you can create a custom authentication extension and invoke it at specific points in the user flow. The OnAttributeCollectionStart event occurs at the beginning of the attribute collection step, before the attribute collection page renders. This event allows you to define actions before attributes are collected from the user. For example, you can block a user from continuing the sign-up flow based on their federated identity or email, or prefill attributes with specified values. The following actions can be configured:

- **continueWithDefaultBehavior** - Render the attribute collection page as usual.
- **setPreFillValues** - Prefill attributes in the sign-up form.
- **showBlockPage** - Show an error message and block the user from signing up.

This article describes the REST API schema for the OnAttributeCollectionStart event. (See also the related article [Custom Extension for OnAttributeCollectionSubmit event](custom-extension-onattributecollectionsubmit-reference).)

## REST API schema

To develop your own REST API for the attribute collection start event, use the following REST API data contract. The schema describes the contract to design the request and response handler.

Your custom authentication extension in Microsoft Entra ID makes an HTTP call to your REST API with a JSON payload. The JSON payload contains user profile data, authentication context attributes, and information about the application the user wants to sign in to. The JSON attributes can be used to perform extra logic by your API.

### Request to the external REST API

The request to your REST API is in the format shown below. In this example, the request includes user identities information along with built-in attributes (givenName and companyName) and custom attributes (universityGroups, graduationYear, and onMailingList).

The request contains the user attributes that are selected in the user flow for collection during self-service sign-up, including built-in attributes (for example, givenName and companyName) and [custom attributes that have already been defined](../external-id/customers/how-to-define-custom-attributes) (for example, universityGroups, graduationYear, and onMailingList). Your REST API can't add new attributes.

The request also contains user identities, including the user's email if it was used as a verified credential to sign up. The password isn't sent.

Attributes in the start request contain their default values. For attributes with multiple values, the values are sent as a comma-delimited string. Because attributes haven't been collected from the user yet, most attributes won't have values assigned. The following HTTP request demonstrates how Microsoft Entra invokes your REST API.

```http
POST https://example.azureWebsites.net/api/functionName

Content-Type: application/json

[Request payload]
```

The following JSON document provides an example of a request payload:

```json
{
  "type": "microsoft.graph.authenticationEvent.attributeCollectionStart",
  "source": "/tenants/aaaabbbb-0000-cccc-1111-dddd2222eeee/applications/<resourceAppguid>",
  "data": {
    "@odata.type": "microsoft.graph.onAttributeCollectionStartCalloutData",
    "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
    "authenticationEventListenerId": "00001111-aaaa-2222-bbbb-3333cccc4444",
    "customAuthenticationExtensionId": "11112222-bbbb-3333-cccc-4444dddd5555",
    "authenticationContext": {
        "correlationId": "<GUID>",
        "client": {
            "ip": "30.51.176.110",
            "locale": "en-us",
            "market": "en-us"
        },
        "protocol": "OAUTH2.0",
        "clientServicePrincipal": {
            "id": "<Your Test Applications servicePrincipal objectId>",
            "appId": "<Your Test Application App Id>",
            "appDisplayName": "My Test application",
            "displayName": "My Test application"
        },
        "resourceServicePrincipal": {
            "id": "<Your Test Applications servicePrincipal objectId>",
            "appId": "<Your Test Application App Id>",
            "appDisplayName": "My Test application",
            "displayName": "My Test application"
        }
    },
    "userSignUpInfo": {
      "attributes": {
        "givenName": {
          "@odata.type": "microsoft.graph.stringDirectoryAttributeValue",
          "value": "Larissa Price",
          "attributeType": "builtIn"
        },
        "companyName": {
          "@odata.type": "microsoft.graph.stringDirectoryAttributeValue",
          "value": "Contoso University",
          "attributeType": "builtIn"
        },
        "extension_<appid>_universityGroups": {
          "@odata.Type": "microsoft.graph.stringDirectoryAttributeValue",
          "value": "Alumni,Faculty",
          "attributeType": "directorySchemaExtension"
        },
        "extension_<appid>_graduationYear": {
          "@odata.type": "microsoft.graph.int64DirectoryAttributeValue",
          "value": 2010,
          "attributeType": "directorySchemaExtension"
        },
        "extension_<appid>_onMailingList": {
          "@odata.type": "microsoft.graph.booleanDirectoryAttributeValue",
          "value": false,
          "attributeType": "directorySchemaExtension"
        }
      },
      "identities": [
        {
          "signInType": "email",
          "issuer": "contoso.onmicrosoft.com",
          "issuerAssignedId": "larissa.price@contoso.onmicrosoft.com"
        }
      ]
    }
  }
}
```

### Response from the external REST API

The response value types match the request value types, for example:

- If the request contains an attribute `graduationYear` with an `@odata.type` of `int64DirectoryAttributeValue`, the response should include a `graduationYear` attribute with an integer value, such as `2010`.
- If the request contains an attribute with multiple values specified as a comma-delimited string, the response should contain the values in a comma-delimited string.

Microsoft Entra ID expects a REST API response in the following format.

```http
HTTP/1.1 200 OK

Content-Type: application/json

[JSON document]
```

In the HTTP response, provide one of following JSON documents. The **continueWithDefaultBehavior** action specifies that your external REST API is returning a continuation response.

```json
{
  "data": {
    "@odata.type": "microsoft.graph.onAttributeCollectionStartResponseData",
    "actions": [
      {
        "@odata.type": "microsoft.graph.attributeCollectionStart.continueWithDefaultBehavior"
      }
    ]
  }
}
```

The **setPrefillValues** action specifies that the external REST API is returning a response to prefill attributes with default values. Your REST API can't add new attributes. Any extra attributes that are returned but that aren't part of the attribute collection are ignored.

```json
{
  "data": {
    "@odata.type": "microsoft.graph.onAttributeCollectionStartResponseData",
    "actions": [
      {
        "@odata.type": "microsoft.graph.attributeCollectionStart.setPrefillValues",
        "inputs": {
          "key1": "value1,value2,value3",
          "key2": true
        }
      }
    ]
  }
}
```

The **showBlockPage** action specifies that your external REST API is returning a blocking response.

```json
{
  "data": {
    "@odata.type": "microsoft.graph.onAttributeCollectionStartResponseData",
    "actions": [
      {
        "@odata.type": "microsoft.graph.attributeCollectionStart.showBlockPage",
        "title": "Hold tight...",
        "message": "Your access request is already processing. You'll be notified when your request has been approved."
      }
    ]
  }
}
```