---
layout: Conceptual
title: Migrate GitHub Actions federated credentials to immutable subjects - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identities-github-immutable-subjects
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: ahmed-mohamed-msft
ms.author: ahmed.m
ms.service: entra-workload-id
manager: dougeby
description: Learn how to migrate a Microsoft Entra federated identity credential for GitHub Actions from a mutable subject to GitHub's immutable subject format.
ms.topic: how-to
ms.custom: msecd-doc-authoring-1018
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 19056b24-a8c7-7788-0ca6-de468894d05c
document_version_independent_id: 19056b24-a8c7-7788-0ca6-de468894d05c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identities-github-immutable-subjects.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identities-github-immutable-subjects
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identities-github-immutable-subjects.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: b2f0cffb-cdfb-b6d3-4c61-fbc314a865f1
---

# Migrate GitHub Actions federated credentials to immutable subjects - Microsoft Entra Workload ID | Microsoft Learn

A Microsoft Entra federated identity credential trusts a GitHub Actions workflow by matching the subject (`sub`) claim in the OpenID Connect (OIDC) token that GitHub issues. GitHub's original subject was built from the repository and owner names, which can be renamed, transferred, or reused. A federated identity credential that trusts a name-based subject is exposed to *subject recycling*, where a different repository or owner later produces a token that matches your credential. To learn more about this risk, see [Mutable subjects in federated identity credentials](workload-identities-federated-credential-mutable-subjects).

GitHub now offers an immutable subject format that embeds the immutable repository and owner IDs. This article shows how to migrate an existing federated identity credential to that format without downtime: you create a new credential for the immutable subject, enable immutable subjects in GitHub, validate the workflow, and then remove the old credential.

## Understand the immutable subject format

GitHub's original subject is name-based. For example, a workflow running on the `main` branch of the `contoso/payments-api` repository produces this subject:

```text
repo:contoso/payments-api:ref:refs/heads/main
```

The immutable format keeps the names but appends the immutable owner ID and repository ID, separated by an `@` symbol:

```text
repo:<owner>@<owner_id>/<repo>@<repo_id>:ref:refs/heads/main
```

The owner ID and repository ID are assigned once and never reused, so renaming, transferring, or recreating the repository doesn't change them. A federated identity credential that trusts the immutable subject stays bound to the original repository.

Note

Immutable subjects apply to GitHub.com. They aren't available on GitHub Enterprise Server.

## Get the immutable repository and owner IDs

To build the immutable subject, get the numeric owner ID and repository ID from GitHub. These IDs are available through GitHub's OIDC settings and REST API.

Combine the names and IDs to form the immutable subject. For example, if the owner `contoso` has the ID `5544123` and the repository `payments-api` has the ID `821093847`, the immutable subject for the `main` branch is:

```text
repo:contoso@5544123/payments-api@821093847:ref:refs/heads/main
```

## Create a federated identity credential for the immutable subject

Create a new federated identity credential for the immutable subject alongside the existing one. Keeping both credentials in place lets the workflow keep running while you validate the change.

Save the credential body to a file, such as `credential.json`, using the immutable subject you built:

```json
{
  "name": "payments-api-main-immutable",
  "issuer": "https://token.actions.githubusercontent.com",
  "subject": "repo:contoso@5544123/payments-api@821093847:ref:refs/heads/main",
  "audiences": ["api://AzureADTokenExchange"]
}
```

Create the credential with the Azure CLI:

```azurecli
az ad app federated-credential create \
  --id <application-object-id> \
  --parameters ./credential.json
```

Replace `<application-object-id>` with the object ID of your app registration. Create one credential for each subject the workflow presents, such as a different branch or environment.

### Add required claims to a flexible federated identity credential

For GitHub, a flexible federated identity credential must match the `sub` claim and one or both of the following additional claims:

- `repository_id` identifies the repository where the workflow runs.
- `repository_owner_id` identifies the repository owner.

These additional claims are required regardless of whether `sub` uses a name-based, customized, or immutable format. Include the claims that represent the intended trust boundary.

The following credential matches an immutable subject and separately verifies the repository:

```json
{
  "name": "github-repository-immutable",
  "issuer": "https://token.actions.githubusercontent.com",
  "claimsMatchingExpression": {
    "value": "claims['sub'] matches 'repo:octo-org@123456/octo-repo@456789:*' and claims['repository_id'] eq '456789'",
    "languageVersion": 1
  },
  "audiences": ["api://AzureADTokenExchange"]
}
```

To require the repository to remain with a specific owner, also match `repository_owner_id`:

```json
{
  "name": "github-repository-owner-immutable",
  "issuer": "https://token.actions.githubusercontent.com",
  "claimsMatchingExpression": {
    "value": "claims['sub'] matches 'repo:octo-org@123456/octo-repo@456789:*' and claims['repository_id'] eq '456789' and claims['repository_owner_id'] eq '123456'",
    "languageVersion": 1
  },
  "audiences": ["api://AzureADTokenExchange"]
}
```

Replace the example values with the IDs from the GitHub OIDC token. GitHub provides `repository_id` and `repository_owner_id` as separate claims in the token.

## Enable immutable subjects in GitHub

Opt the repository into the immutable subject format from the repository or organization OIDC settings. GitHub provides both UI and API controls, and a preview endpoint that shows the subject a workflow emits, so that you can confirm the value before you rely on it. For the current steps, see the [GitHub OpenID Connect reference](https://docs.github.com/en/actions/reference/security/oidc).

After you opt in, GitHub issues tokens that use the immutable subject you configured your credential to match.

Note

Starting July 15, 2026, GitHub applies the immutable format automatically to repositories that are created, renamed, or transferred. Existing repositories keep the name-based format until you opt in. For details, see [Immutable subject claims for GitHub Actions OIDC tokens](https://github.blog/changelog/2026-04-23-immutable-subject-claims-for-github-actions-oidc-tokens/) in the GitHub Changelog.

## Validate and remove the old credential

After the new credential is in place and GitHub emits the immutable subject, confirm the workflow works and then retire the old credential:

1. Run the GitHub Actions workflow and confirm that it authenticates to Microsoft Entra with the new credential.
2. After the workflow succeeds against the immutable subject, remove the old name-based credential so that no mutable credential remains:

    ```azurecli
    az ad app federated-credential delete \
      --id <application-object-id> \
      --federated-credential-id <old-credential-id>
    ```

    Replace `<application-object-id>` with the object ID of your app registration and `<old-credential-id>` with the ID of the old name-based credential.

Removing the old credential eliminates the dangling, mutable-subject trust and completes the migration.