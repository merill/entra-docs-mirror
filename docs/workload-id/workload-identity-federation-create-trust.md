---
layout: Conceptual
title: Create a trust relationship between an app and an external identity provider - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identity-federation-create-trust
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Set up a trust relationship between an app in Microsoft Entra ID and an external identity provider. This allows a software workload outside of Azure to access Microsoft Entra protected resources without using secrets or certificates.
ms.topic: how-to
ms.date: 2024-12-13T00:00:00.0000000Z
ms.reviewer: shkhalid, udayh, vakarand
zone_pivot_groups: identity-wif-apps-methods
ms.custom: aaddev, devx-track-azurecli, devx-track-azurepowershell, sfi-image-nochange
locale: en-us
document_id: 112d73f5-05dc-a709-fb3b-de4f1eee1338
document_version_independent_id: 304c98c3-8226-ce31-076c-d75b101081a5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identity-federation-create-trust.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurecli,azurepowershell
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identity-federation-create-trust
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identity-federation-create-trust.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 85c96617-fff5-9dcb-bb70-d3ce77cd5da5
---

# Create a trust relationship between an app and an external identity provider - Microsoft Entra Workload ID | Microsoft Learn

This article describes how to manage a federated identity credential on an application in Microsoft Entra ID. The federated identity credential creates a trust relationship between an application and an external identity provider (IdP).

You can then configure an external software workload to exchange a token from the external IdP for an access token from Microsoft identity platform. The external workload can access Microsoft Entra protected resources without needing to manage secrets (in supported scenarios). To learn more about the token exchange workflow, read about [workload identity federation](workload-identity-federation).

In this article, you learn how to create, list, and delete federated identity credentials on an application in Microsoft Entra ID.

## Important considerations and restrictions

To create, update, or delete a federated identity credential, the account performing the action must be the owner of the application, or have one of these Entra roles: [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator), [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator), or [Hybrid Identity Administrator](../identity/role-based-access-control/permissions-reference#hybrid-identity-administrator). The [microsoft.directory/applications/credentials/update permission](../identity/role-based-access-control/custom-available-permissions#microsoftdirectoryapplicationscredentialsupdate) is required to update a federated identity credential.

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

To learn more about supported regions, time to propagate federated credential updates, supported issuers and more, read [Important considerations and restrictions for federated identity credentials](workload-identity-federation-considerations).

::: zone pivot="identity-wif-apps-methods-azp"

## Prerequisites

- [Create an app registration](../identity-platform/quickstart-register-app) or [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) in Microsoft Entra ID. Grant your app access to the Azure resources targeted by your external software workload.
- Find the object ID of the app (not the application (client) ID), which you need in the following steps. You can find the object ID of the app in the [Microsoft Entra admin center](https://entra.microsoft.com). Go to the list of app registrations and select your app registration. In **Overview**, you can find the **Object ID**.
- Get the *subject* and *issuer* information for your external IdP and software workload, which you need in the following steps.

## Configure a federated identity credential on an app

### GitHub Actions

To add a federated identity for GitHub actions, follow these steps:

1. Find your app registration in the app registrations experience of the [Microsoft Entra admin center](https://entra.microsoft.com). Select **Certificates & secrets** in the left nav pane, select the **Federated credentials** tab, and select **Add credential**.
2. In the **Federated credential scenario** drop-down box, select **GitHub actions deploying Azure resources**.
3. Specify the **Organization** and **Repository** for your GitHub Actions workflow.
4. For **Entity type**, select **Environment**, **Branch**, **Pull request**, or **Tag** and specify the value. The values must exactly match the configuration in the [GitHub workflow](https://docs.github.com/actions/using-workflows/workflow-syntax-for-github-actions#on). Pattern matching isn't supported for branches and tags. Specify an environment if your on-push workflow runs against many branches or tags. For more info, read the examples.
5. Add a **Name** for the federated credential.
6. The **Issuer**, **Audiences**, and **Subject identifier** fields autopopulate based on the values you entered.
7. Select **Add** to configure the federated credential.

    ![Screenshot of the Add a credential window, showing sample values.](media/workload-identity-federation-create-trust/add-credential.png)

Use the following values from your Microsoft Entra application registration for your GitHub workflow:

- `AZURE_CLIENT_ID` the **Application (client) ID**
- `AZURE_TENANT_ID` the **Directory (tenant) ID**

    The following screenshot demonstrates how to copy the application ID and tenant ID.

    ![Screenshot that demonstrates how to copy the application ID and tenant ID from Microsoft Entra admin center.](media/workload-identity-federation-create-trust/copy-client-id.png)

#### Entity type examples

##### Branch example

For a workflow triggered by a push or pull request event on the main branch:

```yml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
```

Specify an **Entity type** of **Branch** and a **GitHub branch name** of "main".

##### Environment example

For Jobs tied to an environment named "production":

```yml
on:
  push:
    branches:
      - main

jobs:
  deployment:
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: deploy
        # ...deployment-specific steps
```

Specify an **Entity type** of **Environment** and a **GitHub environment name** of "production".

##### Tag example

For example, for a workflow triggered by a push to the tag named "v2":

```yml
on:
  push:
    # Sequence of patterns matched against refs/heads
    branches:
      - main
      - 'mona/octocat'
      - 'releases/**'
    # Sequence of patterns matched against refs/tags
    tags:
      - v2
      - v1.*
```

Specify an **Entity type** of **Tag** and a **GitHub tag name** of "v2".

##### Pull request example

For a workflow triggered by a pull request event, specify an **Entity type** of **Pull request**

### Kubernetes

Find your app registration in the app registrations experience of the [Microsoft Entra admin center](https://entra.microsoft.com). Select **Certificates & secrets** in the left nav pane, select the **Federated credentials** tab, and select **Add credential**.

Select the **Kubernetes accessing Azure resources** scenario from the dropdown menu.

Fill in the **Cluster issuer URL**, **Namespace**, **Service account name**, and **Name** fields:

- **Cluster issuer URL** is the [OIDC issuer URL](/en-us/azure/aks/use-oidc-issuer) for the managed cluster or the [OIDC Issuer URL](https://azure.github.io/azure-workload-identity/docs/installation/self-managed-clusters/oidc-issuer.html) for a self-managed cluster.
- **Service account name** is the name of the Kubernetes service account, which provides an identity for processes that run in a Pod.
- **Namespace** is the service account namespace.
- **Name** is the name of the federated credential, which can't be changed later.

### Other identity providers

Find your app registration in the app registrations experience of the [Microsoft Entra admin center](https://entra.microsoft.com). Select **Certificates & secrets** in the left nav pane, select the **Federated credentials** tab, and select **Add credential**.

Select the **Other issuer** scenario from the dropdown menu.

Specify the following fields (using a software workload running in Google Cloud as an example):

- **Name** is the name of the federated credential, which can't be changed later.
- **Subject identifier**: must match the `sub` claim in the token issued by the external identity provider. In this example using Google Cloud, *subject* is the Unique ID of the service account you plan to use.
- **Issuer**: must match the `iss` claim in the token issued by the external identity provider. A URL that complies with the OIDC Discovery spec. Microsoft Entra ID uses this issuer URL to fetch the keys that are necessary to validate the token. For Google Cloud, the *issuer* is `https://accounts.google.com`.

## List federated identity credentials on an app

Find your app registration in the app registrations experience of the [Microsoft Entra admin center](https://entra.microsoft.com). Select **Certificates & secrets** in the left nav pane and select the **Federated credentials** tab. The federated credentials that are configured on your app are listed.

## Delete a federated identity credential from an app

Find your app registration in the app registrations experience of the [Microsoft Entra admin center](https://entra.microsoft.com). Select **Certificates & secrets** in the left nav pane and select the **Federated credentials** tab. The federated credentials that are configured on your app are listed.

To delete a federated identity credential, select the **Delete** icon for the credential.

## Set up a Flexible Federated identity credential (preview)

1. Navigate to Microsoft Entra ID and select the application where you want to configure the federated identity credential.
2. In the left-hand navigation pane, select **Certificates & secrets**.
3. Under the **Federated credentials** tab, select **+ Add credential**.
4. In the **Add a credential** window that appears, from the dropdown menu next to **Federated credential scenario**, select **Other issuer**.
5. In **Value** enter the claim matching expression you want to use.

::: zone-end

::: zone pivot="identity-wif-apps-methods-azcli"

## Prerequisites

- If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you continue.

- Use the Bash environment in [Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see [Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).

    [![](../reusable-content/azure-cli/media/hdi-launch-cloud-shell.png)](https://shell.azure.com)
- If you prefer to run CLI reference commands locally, [install](/en-us/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).

    - If you're using a local installation, sign in to the Azure CLI by using the [az login](/en-us/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).
    - When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see [Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).
    - Run [az version](/en-us/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).

- [Create an app registration](../identity-platform/quickstart-register-app) in Microsoft Entra ID. Grant your app access to the Azure resources targeted by your external software workload.
- Find the object ID, app (client) ID, or identifier URI of the app, which you need in the following steps. You can find these values in the [Microsoft Entra admin center](https://entra.microsoft.com). Go to the list of registered applications and select your app registration. In **Overview**-&gt;**Essentials**, get the **Object ID**, **Application (client) ID**, or **Application ID URI** value, which you need in the following steps.
- Get the *subject* and *issuer* information for your external IdP and software workload, which you need in the following steps.

## Configure a federated identity credential on an app

Run the [az ad app federated-credential create](/en-us/cli/azure/ad/app/federated-credential) command to create a new federated identity credential on your app.

The `id` parameter specifies the identifier URI, application ID, or object ID of the application. The `parameters` parameter specifies the parameters, in JSON format, for creating the federated identity credential.

### GitHub Actions example

The *name* specifies the name of your federated identity credential.

The *issuer* identifies the path to the GitHub OIDC provider: `https://token.actions.githubusercontent.com/`. This issuer becomes trusted by your Azure application.

The *subject* identifies the GitHub organization, repo, and environment for your GitHub Actions workflow. When the GitHub Actions workflow requests Microsoft identity platform to exchange a GitHub token for an access token, the values in the federated identity credential are checked against the provided GitHub token. Before Azure grants an access token, the request must match the conditions defined here.

- For Jobs tied to an environment: `repo:< Organization/Repository >:environment:< Name >`
- For Jobs not tied to an environment, include the ref path for branch/tag based on the ref path used for triggering the workflow: `repo:< Organization/Repository >:ref:< ref path>`. For example, `repo:n-username/ node_express:ref:refs/heads/my-branch` or `repo:n-username/ node_express:ref:refs/tags/my-tag`.
- For workflows triggered by a pull request event: `repo:< Organization/Repository >:pull-request`.

```azurecli
az ad app federated-credential create --id 00001111-aaaa-2222-bbbb-3333cccc4444 --parameters credential.json
("credential.json" contains the following content)
{
    "name": "Testing",
    "issuer": "https://token.actions.githubusercontent.com",
    "subject": "repo:octo-org/octo-repo:environment:Production",
    "description": "Testing",
    "audiences": [
        "api://AzureADTokenExchange"
    ]
}
```

### Kubernetes example

The *issuer* is your service account issuer URL (the [OIDC issuer URL](/en-us/azure/aks/use-oidc-issuer) for the managed cluster or the [OIDC Issuer URL](https://azure.github.io/azure-workload-identity/docs/installation/self-managed-clusters/oidc-issuer.html) for a self-managed cluster).

The *subject* is the subject name in the tokens issued to the service account. Kubernetes uses the following format for subject names: `system:serviceaccount:<SERVICE_ACCOUNT_NAMESPACE>:<SERVICE_ACCOUNT_NAME>`.

The *name* is the name of the federated credential, which can't be changed later.

The *audiences* lists the audiences that can appear in the external token. This field is mandatory. The recommended value is `api://AzureADTokenExchange`.

```azurecli
az ad app federated-credential create --id 00001111-aaaa-2222-bbbb-3333cccc4444 --parameters credential.json
("credential.json" contains the following content)
{
    "name": "Kubernetes-federated-credential",
    "issuer": "https://aksoicwesteurope.blob.core.windows.net/aaaabbbb-0000-cccc-1111-dddd2222eeee/",
    "subject": "system:serviceaccount:erp8asle:pod-identity-sa",
    "description": "Kubernetes service account federated credential",
    "audiences": [
        "api://AzureADTokenExchange"
    ]
}
```

### Other identity providers example

You can configure a federated identity credential on an app and create a trust relationship with other external identity providers. The following example uses a software workload running in Google Cloud as an example:

- `name` is the name of the federated credential, which can't be changed later.
- `id`: the object ID, application (client) ID, or identifier URI of the app.
- `subject`: must match the `sub` claim in the token issued by the external identity provider. In this example using Google Cloud, *subject* is the Unique ID of the service account you plan to use.
- `issuer`: must match the `iss` claim in the token issued by the external identity provider. A URL that complies with the OIDC Discovery spec. Microsoft Entra ID uses this issuer URL to fetch the keys that are necessary to validate the token. For Google Cloud, the *issuer* is `https://accounts.google.com`.
- `audiences`: lists the audiences that can appear in the external token. This field is mandatory. The recommended value is "api://AzureADTokenExchange".

```azurecli
az ad app federated-credential create --id 00001111-aaaa-2222-bbbb-3333cccc4444 --parameters credential.json
("credential.json" contains the following content)
{
    "name": "GcpFederation",
    "issuer": "https://accounts.google.com",
    "subject": "112633961854638529490",
    "description": "Test GCP federation",
    "audiences": [
        "api://AzureADTokenExchange"
    ]
}
```

## List federated identity credentials on an app

Run the [az ad app federated-credential list](/en-us/cli/azure/ad/app/federated-credential) command to list the federated identity credentials on your app.

The `id` parameter specifies the identifier URI, application ID, or object ID of the application.

```azurecli
az ad app federated-credential list --id 00001111-aaaa-2222-bbbb-3333cccc4444
```

## Get a federated identity credential on an app

Run the [az ad app federated-credential show](/en-us/cli/azure/ad/app/federated-credential) command to get a federated identity credential on your app.

The `id` parameter specifies the identifier URI, application ID, or object ID of the application.

The `federated-credential-id` specifies the ID or name of the federated identity credential.

```azurecli
az ad app federated-credential show --id 00001111-aaaa-2222-bbbb-3333cccc4444 --federated-credential-id c79f8feb-a9db-4090-85f9-90d820caa0eb
```

## Delete a federated identity credential from an app

Run the [az ad app federated-credential delete](/en-us/cli/azure/ad/app/federated-credential) command to remove a federated identity credential from your app.

The `id` parameter specifies the identifier URI, application ID, or object ID of the application.

The `federated-credential-id` specifies the ID or name of the federated identity credential.

```azurecli
az ad app federated-credential delete --id 00001111-aaaa-2222-bbbb-3333cccc4444 --federated-credential-id c79f8feb-a9db-4090-85f9-90d820caa0eb
```

::: zone-end

::: zone pivot="identity-wif-apps-methods-powershell"

## Prerequisites

- To run the example scripts, you have two options:
    - Use [Azure Cloud Shell](/en-us/azure/cloud-shell/overview), which you can open by using the **Try It** button in the upper-right corner of code blocks.
    - Run scripts locally with Azure PowerShell, as described in the next section.
- [Create an app registration](../identity-platform/quickstart-register-app) in Microsoft Entra ID. Grant your app access to the Azure resources targeted by your external software workload.
- Find the object ID of the app (not the application (client) ID), which you need in the following steps. You can find the object ID of the app in the [Microsoft Entra admin center](https://entra.microsoft.com). Go to the list of registered applications and select your app registration. In **Overview**-&gt;**Essentials**, find the **Object ID**.
- Get the *subject* and *issuer* information for your external IdP and software workload, which you need in the following steps.

### Configure Azure PowerShell locally

To use Azure PowerShell locally for this article instead of using Cloud Shell:

1. Install [the latest version of Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) if you haven't already.
2. Sign in to Azure.

    ```azurepowershell
    Connect-AzAccount
    ```
3. Install the [latest version of PowerShellGet](/en-us/powershell/gallery/powershellget/install-powershellget).

    ```azurepowershell
    Install-Module -Name PowerShellGet -AllowPrerelease
    ```

    You might need to `Exit` out of the current PowerShell session after you run this command for the next step.
4. Install the prerelease version of the `Az.Resources` module to perform the federated identity credential operations in this article.

    ```azurepowershell
    Install-Module -Name Az.Resources -AllowPrerelease
    ```

## Configure a federated identity credential on an app

Run the [New-AzADAppFederatedCredential](/en-us/powershell/module/az.resources/new-azadappfederatedcredential) cmdlet to create a new federated identity credential on an application.

### GitHub Actions example

- *ApplicationObjectId*: the object ID of the app (not the application (client) ID) you previously registered in Microsoft Entra ID.
- *Issuer* identifies GitHub as the external token issuer.
- *Subject*identifies the GitHub organization, repo, and environment for your GitHub Actions workflow. When the GitHub Actions workflow requests Microsoft identity platform to exchange a GitHub token for an access token, the values in the federated identity credential are checked against the provided GitHub token.
    - For Jobs tied to an environment: `repo:< Organization/Repository >:environment:< Name >`
    - For Jobs not tied to an environment, include the ref path for branch/tag based on the ref path used for triggering the workflow: `repo:< Organization/Repository >:ref:< ref path>`. For example, `repo:n-username/ node_express:ref:refs/heads/my-branch` or `repo:n-username/ node_express:ref:refs/tags/my-tag`.
    - For workflows triggered by a pull request event: `repo:< Organization/Repository >:pull-request`.
- *Name* is the name of the federated credential, which can't be changed later.
- *Audience* lists the audiences that can appear in the external token. This field is mandatory. The recommended value is `api://AzureADTokenExchange`.

```azurepowershell
New-AzADAppFederatedCredential -ApplicationObjectId $appObjectId -Audience api://AzureADTokenExchange -Issuer 'https://token.actions.githubusercontent.com/' -Name 'GitHub-Actions-Test' -Subject 'repo:octo-org/octo-repo:environment:Production'
```

### Kubernetes example

- *ApplicationObjectId*: the object ID of the app (not the application (client) ID) you previously registered in Microsoft Entra ID.
- *Issuer* is your service account issuer URL (the [OIDC issuer URL](/en-us/azure/aks/use-oidc-issuer) for the managed cluster or the [OIDC Issuer URL](https://azure.github.io/azure-workload-identity/docs/installation/self-managed-clusters/oidc-issuer.html) for a self-managed cluster).
- *Subject* is the subject name in the tokens issued to the service account. Kubernetes uses the following format for subject names: `system:serviceaccount:<SERVICE_ACCOUNT_NAMESPACE>:<SERVICE_ACCOUNT_NAME>`.
- *Name* is the name of the federated credential, which can't be changed later.
- *Audience* lists the audiences that can appear in the `aud` claim of the external token.

```azurepowershell
New-AzADAppFederatedCredential -ApplicationObjectId $appObjectId -Audience api://AzureADTokenExchange -Issuer 'https://aksoicwesteurope.blob.core.windows.net/aaaabbbb-0000-cccc-1111-dddd2222eeee/' -Name 'Kubernetes-federated-credential' -Subject 'system:serviceaccount:erp8asle:pod-identity-sa'
```

### Other identity providers example

Specify the following parameters (using a software workload running in Google Cloud as an example):

- *ObjectID*: the object ID of the app (not the application (client) ID) you previously registered in Microsoft Entra ID.
- *Name* is the name of the federated credential, which can't be changed later.
- *Subject*: must match the `sub` claim in the token issued by the external identity provider. In this example using Google Cloud, *subject* is the Unique ID of the service account you plan to use.
- *Issuer*: must match the `iss` claim in the token issued by the external identity provider. A URL that complies with the OIDC Discovery spec. Microsoft Entra ID uses this issuer URL to fetch the keys that are necessary to validate the token. For Google Cloud, the *issuer* is `https://accounts.google.com`.
- *Audiences*: must match the `aud` claim in the external token. For security reasons, you should pick a value that is unique for tokens meant for Microsoft Entra ID. The recommended value is "api://AzureADTokenExchange".

```azurepowershell
New-AzADAppFederatedCredential -ApplicationObjectId $appObjectId -Audience api://AzureADTokenExchange -Issuer 'https://accounts.google.com' -Name 'GcpFederation' -Subject '112633961854638529490'
```

## List federated identity credentials on an app

Run the [Get-AzADAppFederatedCredential](/en-us/powershell/module/az.resources/get-azadappfederatedcredential) cmdlet to list the federated identity credentials for an application.

```azurepowershell
Get-AzADApplication -ObjectId $app | Get-AzADAppFederatedCredential
```

## Get a federated identity credential on an app

Run the [Get-AzADAppFederatedCredential](/en-us/powershell/module/az.resources/get-azadappfederatedcredential) cmdlet to get the federated identity credential by ID from an application.

```azurepowershell
Get-AzADAppFederatedCredential -ApplicationObjectId $appObjectId -FederatedCredentialId $credentialId
```

## Delete a federated identity credential from an app

Run the [Remove-AzADAppFederatedCredential](/en-us/powershell/module/az.resources/remove-azadappfederatedcredential) cmdlet to delete a federated identity credential from an application.

```azurepowershell
Remove-AzADAppFederatedCredential -ApplicationObjectId $appObjectId -FederatedCredentialId $credentialId
```

::: zone-end

::: zone pivot="identity-wif-apps-methods-rest"

## Prerequisites

[Create an app registration](../identity-platform/quickstart-register-app) in Microsoft Entra ID. Grant your app access to the Azure resources targeted by your external software workload.

Find the object ID of the app (not the application (client) ID), which you need in the following steps. You can find the object ID of the app in the [Microsoft Entra admin center](https://entra.microsoft.com). Go to the list of registered applications and select your app registration. In **Overview**-&gt;**Essentials**, find the **Object ID**.

Get the *subject* and *issuer* information for your external IdP and software workload, which you need in the following steps.

The Microsoft Graph endpoint (`https://graph.microsoft.com`) exposes REST APIs to create, update, delete [federatedIdentityCredentials](/en-us/graph/api/resources/federatedidentitycredential) on applications. Launch [Azure Cloud Shell](https://portal.azure.com/#cloudshell/) and sign in to your tenant to run Microsoft Graph commands from AZ CLI.

## Configure a federated identity credential on an app

### GitHub Actions

Run the following method to [create a new federated identity credential](/en-us/graph/api/application-post-federatedidentitycredentials) on your app (specified by the object ID of the app). The `issuer` identifies GitHub as the external token issuer. `subject` identifies the GitHub organization, repo, and environment for your GitHub Actions workflow. When the GitHub Actions workflow requests Microsoft identity platform to exchange a GitHub token for an access token, the values in the federated identity credential are checked against the provided GitHub token.

```azurecli
az rest --method POST --uri 'https://graph.microsoft.com/applications/00001111-aaaa-2222-bbbb-3333cccc4444/federatedIdentityCredentials' --body '{"name":"Testing","issuer":"https://token.actions.githubusercontent.com","subject":"repo:octo-org/octo-repo:environment:Production","description":"Testing","audiences":["api://AzureADTokenExchange"]}'
```

And you get the response:

```azurecli
{
  "@odata.context": "https://graph.microsoft.com/$metadata#applications('00001111-aaaa-2222-bbbb-3333cccc4444')/federatedIdentityCredentials/$entity",
  "audiences": [
    "api://AzureADTokenExchange"
  ],
  "description": "Testing",
  "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
  "issuer": "https://token.actions.githubusercontent.com",
  "name": "Testing",
  "subject": "repo:octo-org/octo-repo:environment:Production"
}
```

In the snippet, the parameters are as follows:

- `name`: The name of your Azure application.
- `issuer`: The path to the GitHub OIDC provider: `https://token.actions.githubusercontent.com`. This issuer becomes trusted by your Azure application.
- `subject`: Before Azure grants an access token, the request must match the conditions defined here.
    - For Jobs tied to an environment: `repo:< Organization/Repository >:environment:< Name >`
    - For Jobs not tied to an environment, include the ref path for branch/tag based on the ref path used for triggering the workflow: `repo:< Organization/Repository >:ref:< ref path>`. For example, `repo:n-username/ node_express:ref:refs/heads/my-branch` or `repo:n-username/ node_express:ref:refs/tags/my-tag`.
    - For workflows triggered by a pull request event: `repo:< Organization/Repository >:pull-request`.
- `audiences` lists the audiences that can appear in the external token. This field is mandatory. The recommended value is "api://AzureADTokenExchange".

### Kubernetes example

Run the following method to configure a federated identity credential on an app and create a trust relationship with a Kubernetes service account. Specify the following parameters:

- `issuer` is your service account issuer URL (the [OIDC issuer URL](/en-us/azure/aks/use-oidc-issuer) for the managed cluster or the [OIDC Issuer URL](https://azure.github.io/azure-workload-identity/docs/installation/self-managed-clusters/oidc-issuer.html) for a self-managed cluster).
- `subject` is the subject name in the tokens issued to the service account. Kubernetes uses the following format for subject names: `system:serviceaccount:<SERVICE_ACCOUNT_NAMESPACE>:<SERVICE_ACCOUNT_NAME>`.
- `name` is the name of the federated credential, which can't be changed later.
- `audiences` lists the audiences that can appear in the external token. This field is mandatory. The recommended value is "api://AzureADTokenExchange".

```azurecli
az rest --method POST --uri 'https://graph.microsoft.com/applications/00001111-aaaa-2222-bbbb-3333cccc4444/federatedIdentityCredentials' --body '{"name":"Kubernetes-federated-credential","issuer":"https://aksoicwesteurope.blob.core.windows.net/aaaabbbb-0000-cccc-1111-dddd2222eeee/","subject":"system:serviceaccount:erp8asle:pod-identity-sa","description":"Kubernetes service account federated credential","audiences":["api://AzureADTokenExchange"]}'
```

And you get the response:

```azurecli
{
  "@odata.context": "https://graph.microsoft.com/$metadata#applications('00001111-aaaa-2222-bbbb-3333cccc4444')/federatedIdentityCredentials/$entity",
  "audiences": [
    "api://AzureADTokenExchange"
  ],
  "description": "Kubernetes service account federated credential",
  "id": "51ecf9c3-35fc-4519-a28a-8c27c6178bca",
  "issuer": "https://aksoicwesteurope.blob.core.windows.net/aaaabbbb-0000-cccc-1111-dddd2222eeee/",
  "name": "Kubernetes-federated-credential",
  "subject": "system:serviceaccount:erp8asle:pod-identity-sa"
}
```

### Other identity providers example

Run the following method to configure a federated identity credential on an app and create a trust relationship with an external identity provider. Specify the following parameters (using a software workload running in Google Cloud as an example):

- *name* is the name of the federated credential, which can't be changed later.
- *ObjectID*: the object ID of the app (not the application (client) ID) you previously registered in Microsoft Entra ID.
- *subject*: must match the `sub` claim in the token issued by the external identity provider. In this example using Google Cloud, *subject* is the Unique ID of the service account you plan to use.
- *issuer*: must match the `iss` claim in the token issued by the external identity provider. A URL that complies with the OIDC Discovery spec. Microsoft Entra ID uses this issuer URL to fetch the keys that are necessary to validate the token. For Google Cloud, the *issuer* is "https://accounts.google.com".
- *audiences* lists the audiences that can appear in the external token. This field is mandatory. The recommended value is "api://AzureADTokenExchange".

```azurecli
az rest --method POST --uri 'https://graph.microsoft.com/applications/<ObjectID>/federatedIdentityCredentials' --body '{"name":"GcpFederation","issuer":"https://accounts.google.com","subject":"112633961854638529490","description":"Testing","audiences":["api://AzureADTokenExchange"]}'
```

And you get the response:

```azurecli
{
  "@odata.context": "https://graph.microsoft.com/$metadata#applications('00001111-aaaa-2222-bbbb-3333cccc4444')/federatedIdentityCredentials/$entity",
  "audiences": [
    "api://AzureADTokenExchange"
  ],
  "description": "Testing",
  "id": "51ecf9c3-35fc-4519-a28a-8c27c6178bca",
  "issuer": "https://accounts.google.com"",
  "name": "GcpFederation",
  "subject": "112633961854638529490"
}
```

## List federated identity credentials on an app

Run the following method to [list the federated identity credentials](/en-us/graph/api/application-list-federatedidentitycredentials) for an app (specified by the object ID of the app):

```azurecli
az rest -m GET -u 'https://graph.microsoft.com/applications/00001111-aaaa-2222-bbbb-3333cccc4444/federatedIdentityCredentials'
```

And you get a response similar to:

```azurecli
{
  "@odata.context": "https://graph.microsoft.com/$metadata#applications('00001111-aaaa-2222-bbbb-3333cccc4444')/federatedIdentityCredentials",
  "value": [
    {
      "audiences": [
        "api://AzureADTokenExchange"
      ],
      "description": "Testing",
      "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
      "issuer": "https://token.actions.githubusercontent.com/",
      "name": "Testing",
      "subject": "repo:octo-org/octo-repo:environment:Production"
    }
  ]
}
```

## Get a federated identity credential on an app

Run the following method to [get a federated identity credential](/en-us/graph/api/federatedidentitycredential-get) for an app (specified by the object ID of the app):

```azurecli
az rest -m GET -u 'https://graph.microsoft.com/applications/00001111-aaaa-2222-bbbb-3333cccc4444//federatedIdentityCredentials/00aa00aa-bb11-cc22-dd33-44ee44ee44ee'
```

And you get a response similar to:

```azurecli
{
  "@odata.context": "https://graph.microsoft.com/$metadata#applications('00001111-aaaa-2222-bbbb-3333cccc4444')/federatedIdentityCredentials",
  "value": {
      "@odata.context": "https://graph.microsoft.com/$metadata#applications('00001111-aaaa-2222-bbbb-3333cccc4444')/federatedIdentityCredentials/$entity",
      "@odata.id": "https://graph.microsoft.com/v2/3d1e2be9-a10a-4a0c-8380-7ce190f98ed9/directoryObjects/$/Microsoft.DirectoryServices.Application('00001111-aaaa-2222-bbbb-3333cccc4444')/federatedIdentityCredentials('00001111-aaaa-2222-bbbb-3333cccc4444')/00001111-aaaa-2222-bbbb-3333cccc4444",
    "audiences": [
        "api://AzureADTokenExchange"
      ],
      "description": "Testing",
      "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
      "issuer": "https://token.actions.githubusercontent.com/",
      "name": "Testing",
      "subject": "repo:octo-org/octo-repo:environment:Production"
    }
}
```

## Delete a federated identity credential from an app

Run the following method to [delete a federated identity credential](/en-us/graph/api/federatedidentitycredential-delete) from an app (specified by the object ID of the app):

```azurecli
az rest -m DELETE  -u 'https://graph.microsoft.com/applications/00001111-aaaa-2222-bbbb-3333cccc4444/federatedIdentityCredentials/00aa00aa-bb11-cc22-dd33-44ee44ee44ee'
```

::: zone-end