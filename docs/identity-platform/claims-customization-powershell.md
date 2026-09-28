---
layout: Conceptual
title: Claims customization using PowerShell and Claims Mapping Policy - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/claims-customization-powershell
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This article describes how to customize claims in Microsoft Entra ID using PowerShell
manager: pmwongera
ms.topic: how-to
ms.date: 2023-11-02T00:00:00.0000000Z
ms.reviewer: 
ms.custom: 
locale: en-us
document_id: a3ab34da-dd04-6d50-34c1-15a6542df47b
document_version_independent_id: a3ab34da-dd04-6d50-34c1-15a6542df47b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/claims-customization-powershell.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/claims-customization-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/claims-customization-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 07439422-8496-82f5-0f39-49f22d24f4bd
---

# Claims customization using PowerShell and Claims Mapping Policy - Microsoft identity platform | Microsoft Learn

A claim is information that an identity provider states about a user inside the token they issue for that user. Claims customization is used by tenant admins to customize the claims emitted in tokens for a specific application in their tenant. You can use claims-mapping policies to:

- select which claims are included in tokens.
- create claim types that do not already exist.
- choose or change the source of data emitted in specific claims.

Claims customization supports configuring claim-mapping policies for the SAML, OAuth, and OpenID Connect protocols.

Note

Claims Mapping Policy supersedes both Custom Claims policy and the [claims customization](saml-claims-customization) offered through the Microsoft Entra admin center. Customizing claims for an application using the Claims Mapping Policy means that tokens issued for that application will ignore the configuration in Custom Claims Policy or the configuration in [claims customization](saml-claims-customization) blade in the Microsoft Entra admin center.

## Prerequisites

- Learn about [how to get a Microsoft Entra tenant](../external-id/customers/quickstart-tenant-setup).
- Download the latest [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

## Get started

In the following examples, you create, update, link, and delete policies for service principals. Claims-mapping policies can only be assigned to service principal objects.

When creating a claims-mapping policy, you can also emit a claim from a directory extension attribute in tokens. Use `ExtensionID` for the extension attribute instead of ID in the `ClaimsSchema` element. For more info on extension attributes, see [Using directory extension attributes](schema-extensions).

Note

The [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation) is required to configure claims-mapping policies.

Open a terminal and run the following command to sign in to your Microsoft Entra admin account. Run this command each time you start a new session.

```PowerShell
Import-Module Microsoft.Graph.Identity.SignIns

Connect-MgGraph -Scopes "Policy.ReadWrite.ApplicationConfiguration", "Policy.Read.All"
```

Now you can create a claims mapping policy and assign it to a service principal. Refer to the following examples for common scenarios:

- Omit the basic claims from tokens
- Include the EmployeeID and TenantCountry as claims in tokens
- Use a claims transformation in tokens

After creating a claims mapping policy, configure your application to acknowledge that tokens will contain customized claims. For more information, read [security considerations](jwt-claims-customization#security-considerations).

### Omit the basic claims from tokens

In this example, you create a policy that removes the [basic claim set](reference-claims-customization#claim-sets) from tokens issued to linked service principals.

1. Create a claims-mapping policy. This policy, linked to specific service principals, removes the basic claim set from tokens.
2. Using the terminal you have open, run the following command to create the policy:

    ```PowerShell
    New-MgPolicyClaimMappingPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims"
    ```
3. To see your new policy, and to get the policy `ObjectId`, run the following command:

    ```PowerShell
    Get-MgPolicyClaimMappingPolicy
    
    Definition                    DeletedDateTime Description DisplayName      Id
    ----------                    --------------- ----------- -----------      --
    {"ClaimsMappingPolicy":{..}}                              OmitBasicClaims  36d1aa10-f9ac...
    ```

### Include the `EmployeeID` and `TenantCountry` as claims in tokens

In this example, you create a policy that adds the `EmployeeID` and `TenantCountry` to tokens issued to linked service principals. The EmployeeID is emitted as the name claim type in both SAML tokens and JWTs. The TenantCountry is emitted as the country/region claim type in both SAML tokens and JWTs. In this example, we continue to include the basic claims set in the tokens.

1. Create a claims-mapping policy. This policy, linked to specific service principals, adds the EmployeeID and TenantCountry claims to tokens.
2. To create the policy, run the following command in your terminal:

    ```PowerShell
    New-MgPolicyClaimMappingPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/employeeid","JwtClaimType":"employeeid"},{"Source":"company","ID":"tenantcountry","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample"
    ```
3. To see your new policy, and to get the policy `ObjectId`, run the following command:

    ```PowerShell
    Get-MgPolicyClaimMappingPolicy
    ```

### Use a claims transformation in tokens

In this example, you create a policy that emits a custom claim "JoinedData" to JWTs issued to linked service principals. This claim contains a value created by joining the data stored in the extensionattribute1 attribute on the user object with "-ext". In this example, we exclude the basic claims set in the tokens.

1. Create a claims-mapping policy. This policy, linked to specific service principals, emits a custom claim `JoinedData` to tokens.
2. To create the policy, run the following command:

    ```PowerShell
    New-MgPolicyClaimMappingPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformations":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"ID":"string2","Value":"ext"},{"ID":"separator","Value":"-"}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample"
    ```
3. To see your new policy, and to get the policy `ObjectId`, run the following command:

    ```PowerShell
    Get-MgPolicyClaimMappingPolicy
    ```

## Assign the claims mapping policy to your service principal

To assign the policy to the service principal you will need the `ObjectId` of your claims mapping policy and the `objectId` of the service principal to which the policy must be assigned.

1. To see all your organization's service principals, you can [query the Microsoft Graph API](/en-us/graph/api/serviceprincipal-list) or, check them in [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. To see all the claims mapping policies in your tenant, and to get the policy `ObjectId`, run the following command:

    ```PowerShell
    Get-MgPolicyClaimMappingPolicy
    ```
3. When you have the `ObjectId` of your claims mapping policy and the service principal, run the following command:

    ```PowerShell
    New-MgServicePrincipalClaimMappingPolicyByRef -ServicePrincipalId <servicePrincipalId> -BodyParameter @{"@odata.id" = "https://graph.microsoft.com/v1.0/policies/claimsMappingPolicies/<claimsMappingPolicyId>"}
    ```