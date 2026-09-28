---
layout: Conceptual
title: Set up a Flexible Federated identity credential (preview) - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identities-set-up-flexible-federated-identity-credential
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Learn how to configure a flexible federated identity credential for an application or user-assigned managed identity by using the Azure portal or REST APIs.
ms.topic: how-to
ms.date: 2026-09-18T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1018
ms.reviewer: ludwignick
ai-usage: ai-assisted
locale: en-us
document_id: f7033470-bbe9-327b-6a2f-6acdffe6541f
document_version_independent_id: f7033470-bbe9-327b-6a2f-6acdffe6541f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identities-set-up-flexible-federated-identity-credential.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identities-set-up-flexible-federated-identity-credential
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identities-set-up-flexible-federated-identity-credential.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: 0c909956-7702-0893-ca8a-0af157538cdc
---

# Set up a Flexible Federated identity credential (preview) - Microsoft Entra Workload ID | Microsoft Learn

This article shows how to set up a [flexible federated identity credential](workload-identities-flexible-federated-identity-credentials) for an application or user-assigned managed identity. You can use the Azure portal, Microsoft Graph for an application, or Azure Resource Manager for a user-assigned managed identity. Before you begin, review the requirements in Prerequisites.

## Prerequisites

- An Azure account with an active subscription. If you don't already have one, [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- For an application, [create an app registration](../identity-platform/quickstart-register-app). Grant the application access to the Azure resources targeted by your external software workload.
- For a managed identity, [create a user-assigned managed identity](../identity/managed-identities-azure-resources/how-manage-user-assigned-managed-identities).

## Understand the credential properties

| **Property** | **Description** |
| --- | --- |
| **audiences** | The audience that can appear in the external token. This field is mandatory and should be set to `api://AzureADTokenExchange` for Microsoft Entra ID. It says what Microsoft identity platform should accept in the `aud` claim in the incoming token. This value represents Microsoft Entra ID in your external identity provider and has no fixed value across identity providers - you might need to create a new application registration in your IdP to serve as the audience of this token. |
| **issuer** | The URL of the external identity provider. Must match the `issuer` claim of the external token being exchanged. |
| **subject** | The identifier of the external software workload within the external identity provider. Like the audience value, it has no fixed format, as each IdP uses their own - sometimes a GUID, sometimes a colon delimited identifier, sometimes arbitrary strings. The value here must match the `sub` claim within the token presented to Microsoft Entra ID. If subject is defined, claimsMatchingExpression must be set to null. |
| **name** | A unique string to identify the credential. For applications, this property is an alternate key, and you can use it to reference the credential through a GET operation. For a user-assigned managed identity, the credential name is part of the Azure Resource Manager resource path. |
| **claimsMatchingExpression** | a new complex type containing two properties, value and languageVersion. Value is used to define the expression, and languageVersion is used to define the version of the flexible federated identity credential expression language (FFL) being used. languageVersion should always be set to 1. If claimsMatchingExpression is defined, subject must be set to null. |

## Set up a flexible federated identity credential

For GitHub, a flexible federated identity credential must match the `sub` claim and one or both of the following immutable claims:

- `repository_id` identifies the repository where the workflow runs.
- `repository_owner_id` identifies the repository owner.

These claims are required regardless of whether `sub` uses a name-based, customized, or immutable format.

When you use mutable subjects with GitLab, your flexible federated identity credential expression must match the `sub` and `project_id` claims.

# [Application - Azure portal](#tab/application-portal)
To create the credential in the Azure portal:

- Navigate to Microsoft Entra ID and select the application where you want to configure the federated identity credential.
- In the left-hand navigation pane, select **Certificates & secrets**.
- Under the **Federated credentials** tab, select **+ Add credential**.
- In the **Add a credential** window that appears, from the dropdown menu next to **Federated credential scenario**, select **Other issuer**.
- Under **Connect your account**, enter the **Issuer**URL of the external identity provider. For example:
    - GitHub: `https://token.actions.githubusercontent.com`
    - GitLab: `https://gitlab.example.com`
    - Terraform Cloud: `https://app.terraform.io`
- In **Value**, enter the claim matching expression you want to use. For example, for GitHub, enter `claims['sub'] matches 'repo:contoso/contoso-repo:ref:refs/heads/*' and claims['repository_id'] eq '456789'`.
- Select **Add** to save the credential.

# [Application - Microsoft Graph](#tab/application-graph)
To create the credential by using Microsoft Graph Explorer:

- Open the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
- In the **Request** section, enter the URL that corresponds to the application: `https://graph.microsoft.com/beta/applications/{objectId}/federatedIdentityCredentials`.
- Add the following request body:

    ```json
    {
      "audiences": [
        "api://AzureADTokenExchange"
      ],
      "issuer": "https://token.actions.githubusercontent.com",
      "name": "MyFlexibleFIC",
      "claimsMatchingExpression": {
        "value": "claims['sub'] matches 'repo:contoso/contoso-repo:ref:refs/heads/*' and claims['repository_id'] eq '456789'",
        "languageVersion": 1
      }
    }
    ```
- Select **Run query** to create the federated identity credential.

# [Managed identity - Azure portal](#tab/managed-identity-portal)
To create the credential for a user-assigned managed identity in the Azure portal:

- In the [Azure portal](https://portal.azure.com), open the user-assigned managed identity where you want to configure the credential.
- Under **Settings**, select **Federated credentials**.
- Select **Add credential**.
- For **Federated credential scenario**, select **Other issuer**.
- Enter the **Issuer**URL of the external identity provider. For example:
    - GitHub: `https://token.actions.githubusercontent.com`
    - GitLab: `https://gitlab.example.com`
    - Terraform Cloud: `https://app.terraform.io`
- In **Value**, enter the claims matching expression. For example, enter `claims['sub'] matches 'repo:contoso/contoso-repo:ref:refs/heads/*' and claims['repository_id'] eq '456789'`.
- Select **Add** to save the credential.

# [Managed identity - ARM REST](#tab/managed-identity-rest)
Create the credential under the user-assigned managed identity's `Microsoft.ManagedIdentity/userAssignedIdentities/federatedIdentityCredentials` resource.

```http
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ManagedIdentity/userAssignedIdentities/{identityName}/federatedIdentityCredentials/{credentialName}?api-version=2025-01-31-preview
Content-Type: application/json

{
  "properties": {
    "issuer": "https://token.actions.githubusercontent.com",
    "audiences": [
      "api://AzureADTokenExchange"
    ],
    "claimsMatchingExpression": {
      "value": "claims['sub'] matches 'repo:contoso/contoso-repo:ref:refs/heads/*' and claims['repository_id'] eq '456789'",
      "languageVersion": 1
    }
  }
}
```

The request must contain either `subject` or `claimsMatchingExpression`, but not both.

---

## More examples of Flexible Federated identity credentials

Flexible federated identity credentials can use different issuers, such as GitHub, GitLab, and Terraform Cloud. Use the following tabs to set up a flexible federated identity credential for each of these issuers.

# [GitHub](#tab/github)
This example shows how to set up a flexible federated identity credential for GitHub with an expression for the `job_workflow_ref` claim. Get the numeric `repository_id` and `repository_owner_id` values from the GitHub OpenID Connect (OIDC) token. Use `repository_id` to bind the credential to a repository.

```json
{
  "audiences": [
    "api://AzureADTokenExchange"
  ],
  "name": "MyGitHubFlexibleFIC",
  "issuer": "https://token.actions.githubusercontent.com",
  "claimsMatchingExpression": {
    "value": "claims['sub'] matches 'repo:contoso/contoso-repo:ref:refs/heads/*' and claims['repository_id'] eq '456789' and claims['job_workflow_ref'] matches 'contoso/contoso-prod/.github/workflows/*.yml@refs/heads/main'",
    "languageVersion": 1
  }
}
```

To require the repository to remain with a specific owner, also match `repository_owner_id`:

```json
{
  "audiences": [
    "api://AzureADTokenExchange"
  ],
  "name": "MyGitHubOwnerFlexibleFIC",
  "issuer": "https://token.actions.githubusercontent.com",
  "claimsMatchingExpression": {
    "value": "claims['sub'] matches 'repo:contoso/contoso-repo:ref:refs/heads/*' and claims['repository_id'] eq '456789' and claims['repository_owner_id'] eq '123456' and claims['job_workflow_ref'] matches 'contoso/contoso-prod/.github/workflows/*.yml@refs/heads/main'",
    "languageVersion": 1
  }
}
```

# [GitLab](#tab/gitlab)
Get the numeric `project_id` value from the GitLab ID token. Include this immutable claim when the `sub` claim uses the mutable `project_path` format.

```json
{
  "audiences": [
    "api://AzureADTokenExchange"
  ],
  "name": "MyGitLabFlexibleFIC",
  "issuer": "https://gitlab.example.com",
  "claimsMatchingExpression": {
    "value": "claims['sub'] matches 'project_path:contoso/contoso-project:ref_type:branch:ref:main' and claims['project_id'] eq '57382910'",
    "languageVersion": 1
  }
}
```

# [Terraform Cloud](#tab/terraform-cloud)
The following example matches Terraform Cloud runs for any run phase in the specified workspace:

```json
{
  "audiences": [
    "api://AzureADTokenExchange"
  ],
  "name": "MyTfcFlexibleFIC",
  "issuer": "https://app.terraform.io",
  "claimsMatchingExpression": {
    "value": "claims['sub'] matches 'organization:contoso:project:contoso-proj:workspace:wrk-1:run_phase:*'",
    "languageVersion": 1
  }
}
```

---