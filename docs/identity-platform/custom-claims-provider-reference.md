---
layout: Conceptual
title: Custom claims provider reference - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-claims-provider-reference
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Reference documentation for custom claims providers
manager: pmwongera
ms.custom: 
ms.date: 2025-05-25T00:00:00.0000000Z
ms.reviewer: jasuri
ms.topic: how-to
locale: en-us
document_id: fe819e4f-33cb-8ab0-a5f1-f197e9fbe499
document_version_independent_id: f1818b00-ab24-133a-2ca0-6a268c842614
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-claims-provider-reference.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-claims-provider-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-claims-provider-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 05cb7535-66ed-9559-9b7c-b9d3639f4e31
---

# Custom claims provider reference - Microsoft identity platform | Microsoft Learn

In this how-to guide, you can learn about the REST API schema and claims mapping policy structure for custom claim provider events.

## Token issuance start event

The custom claims provider token issuance event allows you to enrich or customize application tokens with information from external systems. This information that can't be stored as part of the user profile in Microsoft Entra directory.

### Component overview

To set up and, integrate a custom extension with your application requires multiple components to be connected. The following diagram shows a high level view of the configuration points, and relationships that are created to implement a custom extension.

[![Screenshot that shows the components to configure in Microsoft Entra ID to set up and integrate a custom claims provider.](media/custom-extension-tokenissuancestart-configuration/token-issuance-start-config.png)](media/custom-extension-tokenissuancestart-configuration/token-issuance-start-config.png#lightbox)

- You should have a **REST API endpoint** publicly available. In this diagram, it represented by Azure Function. The REST API generates and returns custom claims to the custom extension. It's associated with a Microsoft Entra application registration.
- You require to configure a **custom extension** in Microsoft Entra ID, which is configured to connect to your API.
- You require an **application** that receives the customized tokens. For example https://jwt.ms a Microsoft-owned web application that displays the decoded contents of a token.
- The application, such as the https://jwt.ms must be registered into Microsoft Entra ID using **app registration**.
- You must create an association between your application and your custom extension.
- You can optionally secure the Azure Function with an authentication provider, in this article we use your Microsoft Entra ID.

### REST API

Your REST API endpoint is responsible for interfacing with downstream services. For example, databases, other REST APIs, LDAP directories, or any other stores that contain the attributes you'd like to add to the token configuration.

The REST API returns an HTTP response to Microsoft Entra ID containing the attributes. Attributes that return by your REST API aren't automatically added into a token. Instead, an application's claims mapping policy must be configured for any attribute to be included in the token. In Microsoft Entra ID, a claims mapping policy modifies the claims emitted in tokens issued for specific applications.

### Request to the REST API

To develop your own REST API for the token issuance start event, use the following REST API data contract. The schema describes the contract to design the request and response handler.

Your custom extension in Microsoft Entra ID makes an HTTP call to your REST API with a JSON payload. The JSON payload contains user profile data, authentication context attributes, and information about the application the user wants to sign-in. The `id` value in the following JSON is a Microsoft application that represents the Microsoft Entra authentication events service. The JSON attributes can be used to perform extra logic by your API.

The following HTTP request demonstrates how Microsoft Entra invokes your REST API. This HTTP request can be used to debug your REST API by simulating a request from Microsoft Entra.

```http
POST https://your-api.com/endpoint

Content-Type: application/json

[Request payload]
```

The following JSON document provides an example of a request payload:

```json
{
    "type": "microsoft.graph.authenticationEvent.tokenIssuanceStart",
    "source": "/tenants/<Your tenant GUID>/applications/<Your Test Application App Id>",
    "data": {
        "@odata.type": "microsoft.graph.onTokenIssuanceStartCalloutData",
        "tenantId": "<Your tenant GUID>",
        "authenticationEventListenerId": "<GUID>",
        "customAuthenticationExtensionId": "<Your custom extension ID>",
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
            },
            "user": {
                "companyName": "Casey Jensen",
                "createdDateTime": "2016-03-01T15:23:40Z",
                "displayName": "Casey Jensen",
                "givenName": "Casey",
                "id": "90847c2a-e29d-4d2f-9f54-c5b4d3f26471", 
                "mail": "casey@contoso.com",
                "onPremisesSamAccountName": "caseyjensen",
                "onPremisesSecurityIdentifier": "<Enter Security Identifier>",
                "onPremisesUserPrincipalName": "Casey Jensen",
                "preferredLanguage": "en-us",
                "surname": "Jensen",
                "userPrincipalName": "casey@contoso.com",
                "userType": "Member"
            }
        }
    }
}
```

When a B2B user from Fabrikam organization authenticates to Contoso's organization, the request payload sent to the REST API has the `user` element in the following format:

```json
"user": {
    "companyName": "Fabrikam",
    "createdDateTime": "2022-07-15T00:00:00Z",
    "displayName": "John Wright",
    "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
    "mail": "johnwright@fabrikam.com",
    "preferredDataLocation": "EUR",
    "userPrincipalName": "johnwright_fabrikam.com#EXT#@contoso.onmicrosoft.com",
    "userType": "Guest"
}
```

### Response from the REST API

Microsoft Entra ID expects a REST API response in the following HTTP.

```http
HTTP/1.1 200 OK

Content-Type: application/json

[JSON document]
```

In the HTTP response, provide the following JSON document, where the claims `DateOfBirth` and `CustomRoles` are returned to Microsoft Entra:

```json
{
    "data": {
        "@odata.type": "microsoft.graph.onTokenIssuanceStartResponseData",
        "actions": [
            {
                "@odata.type": "microsoft.graph.tokenIssuanceStart.provideClaimsForToken",
                "claims": {
                    "DateOfBirth": "01/01/2000",
                    "CustomRoles": [
                        "Writer",
                        "Editor"
                    ]
                }
            }
        ]
    }
}
```

If no additional claim have to be returned, provide an empty `claims` object:

```json
{
    "data": {
        "@odata.type": "microsoft.graph.onTokenIssuanceStartResponseData",
        "actions": [
            {
                "@odata.type": "microsoft.graph.tokenIssuanceStart.provideClaimsForToken",
                "claims": {
                }
            }
        ]
    }
}
```

### Supported data types

The following table shows the data types supported by Custom claims providers for the token issuance start event:

| Data type | Supported |
| --- | --- |
| String | True |
| String array | True |
| Boolean | False |
| JSON | False |

### Claim size limitations

The maximum claim size that a claims provider can return is limited to 3KB. This is the sum of all the key and value pairs returned by the REST API.

### Claims mapping policy

In Microsoft Entra ID, a claims mapping policy modifies the claims emitted in tokens issued for specific applications. It includes claims from your custom claims provider, and issuing them into the token.

```json
{
    "ClaimsMappingPolicy": {
        "Version": 1,
        "IncludeBasicClaimSet": "true",
        "ClaimsSchema": [{
            "Source": "CustomClaimsProvider",
            "ID": "dateOfBirth",
            "JwtClaimType": "birthdate"
        },
        {
            "Source": "CustomClaimsProvider",
            "ID": "customRoles",
            "JwtClaimType": "my_roles"
        },
        {
            "Source": "CustomClaimsProvider",
            "ID": "correlationId",
            "JwtClaimType": "correlation_Id"
        },
        {
            "Source": "CustomClaimsProvider",
            "ID": "apiVersion",
            "JwtClaimType": "apiVersion"
        },
        {
            "Value": "tokenaug_V2",
            "JwtClaimType": "policy_version"
        }]
    }
}
```

The `ClaimsSchema` element contains the list of claims to be mapped with the following attributes:

- **Source** describes the source of the attribute, the `CustomClaimsProvider`. Note, the last element contains a fixed value with the policy version, for testing purposes. Thus, the `source` attribute is omitted.
- **ID** is the name of the claims at it returns from the Azure Function you created.

    Important

    The ID attribute's value is case sensitive. Make sure you type the claim name exactly as it returned by the Azure Function.
- **JwtClaimType** is an optional name of claim in the emitted token for OpenID Connect app. It allows you to provide a different name that returns in the JWT token. For example, if the API response has an `ID` value of `dateOfBirth`, it can be emitted as `birthdate` in the token.

Once you create your claims mapping policy, the next step is to upload it to your Microsoft Entra tenant. Use the following [claimsMappingPolicy](/en-us/graph/api/claimsmappingpolicy-post-claimsmappingpolicies) Graph API in your tenant.

Important

The **definition** element should be an array with a single string value. The string should be the stringified and escaped version of your claims mapping policy. You can use tools like https://jsontostring.com/ to stringify your claims mapping policy.