---
layout: Conceptual
title: Customize claims using Microsoft Graph Custom Claims Policy (preview) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/claims-customization-custom-claims-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This article demonstrates how to customize claims in Microsoft Entra ID using the Custom Claims Policy.
manager: pmwongera
ms.topic: how-to
ms.date: 2024-06-11T00:00:00.0000000Z
ms.reviewer: 
ms.custom: 
locale: en-us
document_id: 1e2ff6fa-f9df-7a19-24ad-9511f21d82c6
document_version_independent_id: 1e2ff6fa-f9df-7a19-24ad-9511f21d82c6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/claims-customization-custom-claims-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/claims-customization-custom-claims-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/claims-customization-custom-claims-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5ca83fa4-a5e0-be0b-bfc5-da4b44947f85
---

# Customize claims using Microsoft Graph Custom Claims Policy (preview) - Microsoft identity platform | Microsoft Learn

A claim is information that an identity provider states about a user inside the token they issue for that user. Claims customization is used by tenant admins to customize the claims emitted in tokens for a specific application in their tenant. Claims customization supports configuring claims for applications using SAML, OAuth, and OpenID Connect protocols. You can use claims customization to:

- Select which claims are included in tokens.
- Create claim types that don't already exist.
- Choose or change the source of data emitted in specific claims.

In this how-to guide, we cover a few common scenarios that can help you understand how to use the [Custom Claims policy](/en-us/graph/api/resources/customclaimspolicy).

## Prerequisites

- A [Microsoft Entra tenant](../external-id/customers/quickstart-tenant-setup).
- An [Enterprise Application](/en-us/entra/identity/enterprise-apps/add-application-portal) configured in the Microsoft Entra admin center.
- For PowerShell users, download the latest [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation). This step is optional.

## Claims customization in Microsoft Entra ID

Microsoft Entra ID supports two ways to customize claims using Microsoft Graph/PowerShell for your applications:

- Using [Custom Claims Policy (Preview)](/en-us/graph/api/resources/customclaimspolicy)
- Using [Claims Mapping Policy](/en-us/graph/api/resources/claimsmappingpolicy)

In the following examples, you create, update, and replace policies for service principals. Custom claims policies are always linked to [service principal](/en-us/graph/api/resources/serviceprincipal) objects. Be sure that you've configured your Enterprise Application as part of the prerequisites before creating a Custom Claims policy for the application/service principal.

Open Microsoft Graph Explorer in your browser sign in to Microsoft Graph Explorer as at least an [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), choose one of the following scenarios.

- Omit the basic claims from tokens
- Include the EmployeeID and TenantCountry as claims in tokens
- Use a claims transformation in tokens

After creating a Custom Claims policy, you should configure your application to acknowledge that the tokens contain the customized claims. For more information, refer to [Security considerations](jwt-claims-customization#security-considerations).

### Omit the basic claims from tokens

In this example, you create a custom claims policy that removes the [basic claim set](reference-claims-customization#claim-sets) from tokens issued to the linked service principal.

1. In Microsoft Graph Explorer, identify the application you want to configure the custom claims policy for using the [service principal API](/en-us/graph/api/resources/serviceprincipal).
2. Create the Custom Claims policy by running the following API. This policy, linked to a service principal, omits the basic claims from the tokens.

    ```http
    PUT https://graph.microsoft.com/beta/servicePrincipals/<servicePrincipal-id>/claimsPolicy
    ```

    Request Body:

    ```json
    {
        "includeBasicClaimSet": false
    }
    ```
3. To see your new policy, run the following command

    ```http
    GET https://graph.microsoft.com/beta/servicePrincipals/<servicePrincipal-id>/claimsPolicy
    ```

    Response:

    ```json
    HTTP/1.1 200 OK
    Content-type: application/json
    
    {
        "@odata.context": "…",
        "id": "aaaaaaaa-bbbb-cccc-1111-222222222222.",
        "includeBasicClaimSet": false,
        "includeApplicationIdInIssuer": false,
        "audienceOverride": null,
        "groupFilter": null,
        "claims": []
    }
    ```

### Include the `EmployeeID` and `TenantCountry` as claims in tokens

In this example, you create a customization to the claims that adds the `EmployeeID` and `TenantCountry` to tokens. In this example, we also include the basic claims set in the tokens.

1. In Microsoft Graph Explorer, identify the application you want to configure the custom claims policy for using the [service principal API](/en-us/graph/api/resources/serviceprincipal).
2. Create the Custom Claims policy by running the following API. This policy, linked to a service principal, adds the EmployeeID and TenantCountry claims to tokens.

    ```http
    PUT https://graph.microsoft.com/beta/servicePrincipals/<servicePrincipal-id>/claimsPolicy
    ```

    Request Body:

    ```json
    {
        "includeBasicClaimSet": true,
        "claims": [
            {
                "@odata.type": "#microsoft.graph.customClaim",
                "name": "employeeId",
                "namespace": null,
                "tokenFormat": [
                    "jwt"
                ],
                "samlAttributeNameFormat": null,
                "configurations": [
                    {
                        "condition": null,
                        "attribute": {
                            "@odata.type": "#microsoft.graph.sourcedAttribute",
                            "id": " employeeId",
                            "source": "user",
                            "isExtensionAttribute": false
                        },
                        "transformations": []
                    }
                ]
            },
            {
                "@odata.type": "#microsoft.graph.customClaim",
                "name": "country",
                "namespace": null,
                "tokenFormat": [
                    "jwt"
                ],
                "samlAttributeNameFormat": null,
                "configurations": [
                    {
                        "condition": null,
                        "attribute": {
                            "@odata.type": "#microsoft.graph.sourcedAttribute",
                            "id": " tenantcountry",
                            "source": "user",
                            "isExtensionAttribute": false
                        },
                        "transformations": []
                    }
                ]
            }
        ]
    }
    ```
3. To see your new policy, run the following command:

    ```http
    GET https://graph.microsoft.com/beta/servicePrincipals/<servicePrincipal-id>/claimsPolicy
    ```

    Response:

    ```json
    {
        "@odata.context": "…",
        "id": "aaaaaaaa-bbbb-cccc-1111-222222222222",
        "includeBasicClaimSet": true,
        "includeApplicationIdInIssuer": false,
        "audienceOverride": null,
        "groupFilter": null,
        "claims": [...]
    }
    ```

### Use a claims transformation in tokens

In this example, you update a policy to emit a custom claim "JoinedData" to JWTs issued to linked service principals. This claim contains a value created by joining the data stored in the extensionattribute1 attribute on the user object with "-ext". In this example, we exclude the basic claims set in the tokens.

1. In Microsoft Graph Explorer, identify the application you want to configure the custom claims policy for using the [service principal API](/en-us/graph/api/resources/serviceprincipal).
2. Create the custom claims policy by running the following API. This policy emits a custom claim `JoinedData` to tokens.

    ```http
    PATCH https://graph.microsoft.com/beta/servicePrincipals/<servicePrincipal-id>/claimsPolicy
    ```

    Request Body:

    ```json
    {
        "includeBasicClaimSet": true,
        "claims": 
        [
            {
                "@odata.type": "#microsoft.graph.customClaim",
                "name": "JoinedData",
                "namespace": null,
                "tokenFormat": [
                    "jwt"
                ],
                "samlAttributeNameFormat": null,
                "configurations": 
                [
                    {
                        "condition": null,
                        "attribute": null,
                        "transformations": 
                        [
                            {
                                "@odata.type": "#microsoft.graph.joinTransformation",
                                "separator": "-",
                                "input": 
                                {
                                    "treatAsMultiValue": false,
                                    "attribute": 
                                    {
                                        "@odata.type": "#microsoft.graph.sourcedAttribute",
                                        "id": "extensionattribute1",
                                        "source": "user",
                                        "isExtensionAttribute": false
                                    }
                                },
                                "input2": 
                                {
                                    "treatAsMultiValue": false,
                                    "attribute": 
                                    {
                                        "@odata.type":"#microsoft.graph.valueBasedAttribute",
                                        "value": "ext"
                                     }
                                }
                            }
                        ]
                    }
                ]
            }
        ]
    }
    ```

    Note

    Custom Claims Policy is a strongly typed policy and each transformation uses a different `@odata.type` value.
3. To see your new policy, and to get the policy `ObjectId`, run the following command:

    ```http
    GET https://graph.microsoft.com/beta/servicePrincipals/<servicePrincipal-id>/claimsPolicy
    ```

    Response:

    ```json
    {
        "@odata.context": "…",
        "id": "aaaaaaaa-bbbb-cccc-1111-222222222222",
        "includeBasicClaimSet": true,
        "includeApplicationIdInIssuer": false,
        "audienceOverride": null,
        "groupFilter": null,
        "claims": [...]
    }
    ```