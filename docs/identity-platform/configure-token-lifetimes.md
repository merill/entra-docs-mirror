---
layout: HowTo
title: Set token lifetimes - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/configure-token-lifetimes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure token lifetimes for access, SAML, or ID tokens issued by Microsoft identity platform. Improve security and authentication management.
manager: pmwongera
ms.date: 2026-04-08T00:00:00.0000000Z
ms.reviewer: sreyanthmora
ms.custom:
- ge-structured-content-pilot
ms.topic: how-to
locale: en-us
document_id: 7537fd89-fd10-1fa2-a721-5260896cfa8a
document_version_independent_id: 8bacaf52-5b8b-d118-2bda-7dfc3861aaba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/configure-token-lifetimes.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/configure-token-lifetimes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/configure-token-lifetimes.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 1819a7f1-a6cd-c460-8985-927755a1e8e1
---

# Set token lifetimes - Microsoft identity platform | Microsoft Learn

This article explains how to configure token lifetime policies for access, SAML, and ID tokens issued by the Microsoft identity platform. Learn how to set token lifetimes for all apps in your organization, specific apps, or multi-tenant applications to improve security and authentication management. You might want to increase the token lifetime so that a script will run for more than an hour. Many Microsoft libraries and applications, such as Microsoft Graph PowerShell SDK, proactively refresh access tokens as needed and you don't need to make changes to the access token policy. For more information, see [configurable token lifetimes](configurable-token-lifetimes). To control how frequently users are required to sign in, use [Conditional Access sign-in frequency](../identity/conditional-access/howto-conditional-access-session-lifetime) instead.

## Prerequisites

To get started, download the latest [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).

## Create a policy and assign it to an app

In the following steps, you'll create a policy that sets the lifetime of the access/ID tokens to 4 hours and assign the policy to an app.

```powershell
Install-Module Microsoft.Graph

Connect-MgGraph -Scopes  "Policy.ReadWrite.ApplicationConfiguration","Policy.Read.All","Application.ReadWrite.All"

# Create a token lifetime policy
$params = @{
  Definition = @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"04:00:00"}}') 
    DisplayName = "WebPolicyScenario"
  IsOrganizationDefault = $false
}
$tokenLifetimePolicyId=(New-MgPolicyTokenLifetimePolicy -BodyParameter $params).Id

# Display the policy
Get-MgPolicyTokenLifetimePolicy -TokenLifetimePolicyId $tokenLifetimePolicyId

# Assign the token lifetime policy to an app
$params = @{
  "@odata.id" = "https://graph.microsoft.com/v1.0/policies/tokenLifetimePolicies/$tokenLifetimePolicyId"
}

$applicationObjectId="aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"

New-MgApplicationTokenLifetimePolicyByRef -ApplicationId $applicationObjectId -BodyParameter $params

# List the token lifetime policy on the app
Get-MgApplicationTokenLifetimePolicy -ApplicationId $applicationObjectId

# Remove the policy from the app
Remove-MgApplicationTokenLifetimePolicyByRef -ApplicationId $applicationObjectId -TokenLifetimePolicyId $tokenLifetimePolicyId

# Delete the policy
Remove-MgPolicyTokenLifetimePolicy -TokenLifetimePolicyId $tokenLifetimePolicyId
```

## Create a policy and assign it to a service principal

In the following steps, you'll create a policy that sets the lifetime of the access/ID tokens to 8 hours and assign the policy to a service principal.

1. Create a token lifetime policy.

    ```http
    POST https://graph.microsoft.com/v1.0/policies/tokenLifetimePolicies
    Content-Type: application/json
    {
        "definition": [
            "{\"TokenLifetimePolicy\":{\"Version\":1,\"AccessTokenLifetime\":\"08:00:00\"}}"
        ],
        "displayName": "Contoso token lifetime policy",
        "isOrganizationDefault": false
    }
    ```
2. Assign the policy to a service principal.

    ```http
    POST https://graph.microsoft.com/v1.0/servicePrincipals/00001111-aaaa-2222-bbbb-3333cccc4444/tokenLifetimePolicies/$ref
    Content-Type: application/json
    {
      "@odata.id":"https://graph.microsoft.com/v1.0/policies/tokenLifetimePolicies/00aa00aa-bb11-cc22-dd33-44ee44ee44ee"
    }
    ```
3. List the policies on the service principal.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/00001111-aaaa-2222-bbbb-3333cccc4444/tokenLifetimePolicies
    ```
4. Remove the policy from the service principal.

    ```http
    DELETE https://graph.microsoft.com/v1.0/servicePrincipals/00001111-aaaa-2222-bbbb-3333cccc4444/tokenLifetimePolicies/00aa00aa-bb11-cc22-dd33-44ee44ee44ee/$ref
    ```

## View existing policies in a tenant

To see all policies that have been created in your organization, run the [Get-MgPolicyTokenLifetimePolicy](/en-us/powershell/module/microsoft.graph.identity.signins/get-mgpolicytokenlifetimepolicy) cmdlet. Any results that define refresh or session token properties (such as `MaxInactiveTime`, `MaxAgeSingleFactor`, `MaxAgeMultiFactor`) contain legacy settings that are no longer honored. These properties were retired on January 30, 2021. Consider updating or removing these policies to avoid confusion.

1. Run the `Get-MgPolicyTokenLifetimePolicy` to see all policies that have been created in your organization.

    ```powershell
    Get-MgPolicyTokenLifetimePolicy
    ```
2. Run [List appliesTo](/en-us/graph/api/tokenlifetimepolicy-list-appliesto) with any of your policy IDs to see which apps are linked to a specific policy that you identified.

    ```powershell
    GET https://graph.microsoft.com/v1.0/policies/tokenLifetimePolicies/4d2f137b-e8a9-46da-a5c3-cc85b2b840a4/appliesTo
    ```