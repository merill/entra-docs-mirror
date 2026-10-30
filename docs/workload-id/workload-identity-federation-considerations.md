---
layout: Conceptual
title: Workload identity federation for app considerations - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identity-federation-considerations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Important considerations and restrictions for creating a federated identity credential on an app.
ms.topic: concept-article
ms.date: 2024-02-28T00:00:00.0000000Z
ms.reviewer: shkhalid
ms.custom: aaddev, references_regions
locale: en-us
document_id: 65d09367-0e52-f540-637a-13eb1c094173
document_version_independent_id: ce84db4f-e1a1-799d-b34a-4f750ec34c14
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identity-federation-considerations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identity-federation-considerations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identity-federation-considerations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/4e834929-0ce1-4c1d-9c81-fcb14721edfb
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/75670257-a3f0-4627-9981-8046f99219e6
platformId: 9c276c74-4974-d843-ee98-de37f08fcd93
---

# Workload identity federation for app considerations - Microsoft Entra Workload ID | Microsoft Learn

This article describes important considerations, restrictions, and limitations for federated identity credentials on Microsoft Entra apps and user-assigned managed identities.

For more information on the scenarios enabled by federated identity credentials, see [workload identity federation overview](workload-identity-federation).

## General federated identity credential considerations

*Applies to: applications and user-assigned managed identities*

Anyone with permissions to create an app registration and add a secret or certificate can add a federated identity credential to an app. If the **Users can register applications** switch is set to **No** in the **Users-&gt;User Settings** blade in the [Microsoft Entra admin center](https://entra.microsoft.com), however, you won't be able to create an app registration or configure the federated identity credential. Find an admin to configure the federated identity credential on your behalf, someone in the Application Administrator or Application Owner roles.

Federated identity credentials don't consume the Microsoft Entra tenant service principal object quota.

A maximum of 20 federated identity credentials can be added to an application or user-assigned managed identity.

When you configure a federated identity credential, there are several important pieces of information to provide:

- *issuer* and *subject* are the key pieces of information needed to set up the trust relationship. The combination of `issuer` and `subject` must be unique on the app. When the external software workload requests Microsoft identity platform to exchange the external token for an access token, the *issuer* and *subject* values of the federated identity credential are checked against the `issuer` and `subject` claims provided in the external token. If that validation check passes, Microsoft identity platform issues an access token to the external software workload.
- *issuer* is the URL of the external identity provider and must match the `issuer` claim of the external token being exchanged. Required. If the `issuer` claim has leading or trailing whitespace in the value, the token exchange is blocked. This field has a character limit of 600 characters.
- *subject* is the identifier of the external software workload and must match the `sub` (`subject`) claim of the external token being exchanged. *subject* has no fixed format, as each IdP uses their own - sometimes a GUID, sometimes a colon delimited identifier, sometimes arbitrary strings. This field has a character limit of 600 characters.

    Important

    The *subject* setting values must exactly match the configuration on the GitHub workflow configuration. Otherwise, Microsoft identity platform will look at the incoming external token and reject the exchange for an access token. You won't get an error, the exchange fails without error.

    Important

    If you accidentally add the incorrect external workload information in the *subject* setting the federated identity credential is created successfully without error. The error does not become apparent until the token exchange fails.
- *audiences* lists the audiences that can appear in the external token. Required. You must add a single audience value, which has a limit of 600 characters. The recommended value is "api://AzureADTokenExchange". It says what Microsoft identity platform must accept in the `aud` claim in the incoming token.
- *name* is the unique identifier for the federated identity credential. Required. This field has a character limit of 3-120 characters and must be URL friendly. Alphanumeric, dash, or underscore characters are supported, the first character must be alphanumeric only. It's immutable once created.
- *description* is the user-provided description of the federated identity credential. Optional. The description isn't validated or checked by Microsoft Entra ID. This field has a limit of 600 characters.

Wildcard characters aren't supported in any federated identity credential property value.

## Unsupported regions (user-assigned managed identities)

*Applies to: user-assigned managed identities*

Creation of federated identity credentials is currently **not supported** on user-assigned managed identities created in the following regions:

- Malaysia South

Support for creating federated identity credentials on user assigned identities in these regions will be gradually rolled out. Resources in this region which need to use federated identity credentials, can do so by leveraging a user assigned managed identity created in a supported region.

## Supported signing algorithms and issuers

*Applies to: applications and user-assigned managed identities*

Only issuers that provide tokens signed using the RS256 algorithm are supported for token exchange using workload identity federation. Exchanging tokens signed with other algorithms may work, but haven't been tested.

## Time for federated credential changes to propagate

*Applies to: applications and user-assigned managed identities*

It takes time for the federated identity credential to be propagated throughout a region after being initially configured. A token request made several minutes after configuring the federated identity credential may fail because the cache is populated in the directory with old data. During this time window, an authorization request might fail with error message: `AADSTS70021: No matching federated identity record found for presented assertion.`

To avoid this issue, wait a short time after adding the federated identity credential before requesting a token to ensure replication completes across all nodes of the authorization service. We also recommend adding retry logic for token requests. Retries should be done for every request even after a token was successfully obtained. Eventually after the data is fully replicated the percentage of failures will drop.

## Concurrent updates aren't supported (user-assigned managed identities)

*Applies to: user-assigned managed identities*

Creating multiple federated identity credentials under the same user-assigned managed identity concurrently triggers concurrency detection logic, which causes requests to fail with 409-conflict HTTP status code.

[Terraform Provider for Azure (Resource Manager)](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs) version 3.40.0 introduces an [update](https://github.com/hashicorp/terraform-provider-azurerm/pull/20003) which creates multiple federated identity credentials sequentially instead of concurrently. Versions earlier than 3.40.0 can cause failures in pipelines when multiple federated identities are created. We recommend you use [Terraform Provider for Azure (Resource Manager) v3.40.0](https://github.com/hashicorp/terraform-provider-azurerm/tree/main) or later so that multiple federated identity credentials are created sequentially.

When you use automation or Azure Resource Manager templates (ARM templates) to create federated identity credentials under the same parent identity, create the federated credentials sequentially. Federated identity credentials under different managed identities can be created in parallel without any restrictions.

If federated identity credentials are provisioned in a loop, you can [provision them serially](/en-us/azure/azure-resource-manager/templates/copy-resources#serial-or-parallel) by setting *"mode": "serial"*.

You can also provision multiple new federated identity credentials sequentially using the *dependsOn* property. The following Azure Resource Manager template (ARM template) example creates three new federated identity credentials sequentially on a user-assigned managed identity by using the *dependsOn* property:

```json
{ 
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", 
    "contentVersion": "1.0.0.0", 
    "parameters": { 
        "userAssignedIdentities_parent_uami_name": { 
            "defaultValue": "parent_uami", 
            "type": "String" 
        } 
    }, 
    "variables": {}, 
    "resources": [ 
        { 
            "type": "Microsoft.ManagedIdentity/userAssignedIdentities", 
            "apiVersion": "2022-01-31-preview", 
            "name": "[parameters('userAssignedIdentities_parent_uami_name')]", 
            "location": "eastus" 
        }, 
        { 
            "type": "Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials", 
            "apiVersion": "2022-01-31-preview", 
            "name": "[concat(parameters('userAssignedIdentities_parent_uami_name'), '/fic01')]", 
            "dependsOn": [ 
                "[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', parameters('userAssignedIdentities_parent_uami_name'))]" 
            ], 
            "properties": { 
                "issuer": "https://kubernetes-oauth.azure.com", 
                "subject": "fic01", 
                "audiences": [ 
                    "api://AzureADTokenExchange" 
                ] 
            } 
        }, 
        { 
            "type": "Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials", 
            "apiVersion": "2022-01-31-preview", 
            "name": "[concat(parameters('userAssignedIdentities_parent_uami_name'), '/fic02')]", 
            "dependsOn": [ 
                "[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', parameters('userAssignedIdentities_parent_uami_name'))]", 
                "[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials', parameters('userAssignedIdentities_parent_uami_name'), 'fic01')]" 
            ], 
            "properties": { 
                "issuer": "https://kubernetes-oauth.azure.com", 
                "subject": "fic02", 
                "audiences": [ 
                    "api://AzureADTokenExchange" 
                ] 
            } 
        }, 
        { 
            "type": "Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials", 
            "apiVersion": "2022-01-31-preview", 
            "name": "[concat(parameters('userAssignedIdentities_parent_uami_name'), '/fic03')]", 
            "dependsOn": [ 
                "[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', parameters('userAssignedIdentities_parent_uami_name'))]", 
                "[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials', parameters('userAssignedIdentities_parent_uami_name'), 'fic02')]" 
            ], 
            "properties": { 
                "issuer": "https://kubernetes-oauth.azure.com", 
                "subject": "fic03", 
                "audiences": [ 
                    "api://AzureADTokenExchange" 
                ] 
            } 
        } 
    ] 
} 
```

## Azure policy

*Applies to: applications and user-assigned managed identities*

It's possible to use a deny [Azure Policy](/en-us/azure/governance/policy/overview) as in the following ARM template example:

```json
{ 
"policyRule": { 
            "if": { 
                "field": "type", 
                "equals": "Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials" 
            }, 
            "then": { 
                "effect": "deny" 
            } 
        } 
}
```

## Throttling limits

*Applies to: user-assigned managed identities*

The following table describes limits on requests to the user-assigned managed identities REST APIS. If you exceed a throttling limit, you receive an HTTP 429 error.

| Operation | Requests-per-second per Microsoft Entra tenant | Requests-per-second per subscription | Requests-per-second per resource |
| --- | --- | --- | --- |
| [Create or update](/en-us/rest/api/managedidentity/2022-01-31-preview/user-assigned-identities/create-or-update) requests | 10 | 2 | 0.25 |
| [Get](/en-us/rest/api/managedidentity/2022-01-31-preview/user-assigned-identities/get) requests | 30 | 10 | 0.5 |
| [List by resource group](/en-us/rest/api/managedidentity/2022-01-31-preview/user-assigned-identities/list-by-resource-group) or [List by subscription](/en-us/rest/api/managedidentity/2022-01-31-preview/user-assigned-identities/list-by-subscription) requests | 15 | 5 | 0.25 |
| [Delete](/en-us/rest/api/managedidentity/2022-01-31-preview/user-assigned-identities/delete) requests | 10 | 2 | 0.25 |

## Errors

*Applies to: applications and user-assigned managed identities*

The following error codes may be returned when creating, updating, getting, listing, or deleting federated identity credentials.

| HTTP code | Error message | Comments |
| --- | --- | --- |
| 405 | The request format was unexpected: Support for federated identity credentials not enabled. | Federated identity credentials aren't enabled in this region. Refer to “Currently Supported regions”. |
| 400 | Federated identity credentials must have exactly one audience. | Currently, federated identity credentials support a single audience “api://AzureADTokenExchange”. |
| 400 | Federated Identity Credential from HTTP body has empty properties | All federated identity credential properties are mandatory. |
| 400 | Federated Identity Credential name '{ficName}' is invalid. | Alphanumeric, dash, underscore, no more than 3-120 symbols. First symbol is alphanumeric. |
| 404 | The parent user-assigned identity doesn't exist. | Check user assigned identity name in federated identity credentials resource path. |
| 400 | Issuer and subject combination already exists for this Managed Identity. | This is a constraint. List all federated identity credentials associated with the user-assigned identity to find existing federated identity credential. |
| 409 | Conflict | Concurrent write request to federated identity credential resources under the same user-assigned identity has been denied. |