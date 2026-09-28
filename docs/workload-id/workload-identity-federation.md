---
layout: Conceptual
title: Workload Identity Federation - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identity-federation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Learn how workload identify federation enables secure access to Microsoft Entra protected resources from external software workloads without managing secrets.
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.reviewer: hosamsh
ms.custom: aaddev
locale: en-us
document_id: cf644d11-51ae-8ef0-34c8-d471a47d5cf1
document_version_independent_id: d5e3190b-f287-6542-fd2b-f8fe9066c23e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identity-federation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identity-federation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identity-federation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 11bc7bfa-32c8-ba0d-b7b6-adcfbc6fe9ea
---

# Workload Identity Federation - Microsoft Entra Workload ID | Microsoft Learn

Learn how workload identity federation enables secure access to Microsoft Entra protected resources without managing secrets. This article provides an overview of its benefits and supported scenarios.

You can use workload identity federation in scenarios such as GitHub Actions, workloads running on Kubernetes, or workloads running in compute platforms outside of Azure.

## Why use workload identity federation?

Watch this video to learn why you would use workload identity federation.

Typically, a software workload (such as an application, service, script, or container-based application) needs an identity in order to authenticate and access resources or communicate with other services. When these workloads run on Azure, you can use [managed identities](../identity/managed-identities-azure-resources/overview) and the Azure platform manages the credentials for you. For a software workload running outside of Azure, or those running in Azure but use app registrations for their identities, you need to use application credentials (a secret or certificate) to access Microsoft Entra protected resources (such as Azure, Microsoft Graph, Microsoft 365, or third-party resources). These credentials pose a security risk and have to be stored securely and rotated regularly. You also run the risk of service downtime if the credentials expire.

You use workload identity federation to configure a [user-assigned managed identity](../identity/managed-identities-azure-resources/how-manage-user-assigned-managed-identities) or [app registration](../identity-platform/app-objects-and-service-principals) in Microsoft Entra ID to trust tokens from an external identity provider (IdP), such as GitHub or Google. The user-assigned managed identity or app registration in Microsoft Entra ID becomes an identity for software workloads running, for example, in on-premises Kubernetes or GitHub Actions workflows. Once that trust relationship is created, your external software workload exchanges trusted tokens from the external IdP for access tokens from Microsoft identity platform. Your software workload uses that access token to access the Microsoft Entra protected resources to which the workload has been granted access. You eliminate the maintenance burden of manually managing credentials and eliminates the risk of leaking secrets or having certificates expire.

## Supported scenarios

The following scenarios are supported for accessing Microsoft Entra protected resources using workload identity federation:

- Workloads running on any Kubernetes cluster (Azure Kubernetes Service (AKS), Amazon Web Services EKS, Google Kubernetes Engine (GKE), or on-premises). Establish a trust relationship between your user-assigned managed identity or app in Microsoft Entra ID and a Kubernetes workload (described in the [workload identity overview](/en-us/azure/aks/workload-identity-overview)).
- GitHub Actions. First, configure a trust relationship between your [user-assigned managed identity](workload-identity-federation-create-trust-user-assigned-managed-identity) or [application](workload-identity-federation-create-trust) in Microsoft Entra ID and a GitHub repo in the [Microsoft Entra admin center](https://entra.microsoft.com) or using Microsoft Graph. Then [configure a GitHub Actions workflow](/en-us/azure/developer/github/connect-from-azure) to get an access token from Microsoft identity provider and access Azure resources.
- Workloads running on Azure compute platforms using app identities. First assign a user-assigned managed identity to your Azure VM or App Service. Then, [configure a trust relationship between your app and the user-assigned identity](workload-identity-federation-config-app-trust-managed-identity).
- Google Cloud. First, configure a trust relationship between your user-assigned managed identity or app in Microsoft Entra ID and an identity in Google Cloud. Then configure your software workload running in Google Cloud to get an access token from Microsoft identity provider and access Microsoft Entra protected resources. See [Tutorial: Federate a Google Cloud workload identity with Microsoft Entra ID](workload-identity-federation-google-cloud).
- Workloads running in Amazon Web Services (AWS). First, configure a trust relationship between your user-assigned managed identity or app in Microsoft Entra ID and your AWS account using [IAM Outbound Identity Federation.](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_outbound_getting_started.html) Then configure your software workload running in AWS first get a JWT from IAM Outbound Identity Federation, then request an access token from Microsoft identity provider using the JWT from [IAM Outbound Identity Federation as a federated credential](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_outbound_getting_started.html), then finally access Microsoft Entra protected resources using the Microsoft issued access token.
- Other workloads running in compute platforms outside of Azure. Configure a trust relationship between your [user-assigned managed identity](workload-identity-federation-create-trust-user-assigned-managed-identity) or [application](workload-identity-federation-create-trust) in Microsoft Entra ID and the external IdP for your compute platform. You can use tokens issued by that platform to authenticate with Microsoft identity platform and call APIs in the Microsoft ecosystem. Use the [client credentials flow](../identity-platform/v2-oauth2-client-creds-grant-flow#third-case-access-token-request-with-a-federated-credential) to get an access token from Microsoft identity platform, passing in the identity provider's JWT instead of creating one yourself using a stored certificate.
- SPIFFE and SPIRE are a set of platform agnostic, open-source standards for providing identities to your software workloads deployed across platforms and cloud vendors. First, configure a trust relationship between your user-assigned managed identity or app in Microsoft Entra ID and a SPIFFE ID for an external workload. Then configure your external software workload to get an access token from Microsoft identity provider and access Microsoft Entra protected resources. See [Tutorial: Federate a SPIFFE/SPIRE workload identity with Microsoft Entra ID](workload-identity-federation-spiffe-spire).
- Create a service connection in Azure Pipelines. [Create an Azure Resource Manager service connection](/en-us/azure/devops/pipelines/library/connect-to-azure#create-an-azure-resource-manager-service-connection-using-workload-identity-federation) using workload identity federation.

Note

Microsoft Entra ID issued tokens may not be used for federated identity flows. The federated identity credentials flow does not support tokens issued by Microsoft Entra ID.

## How it works

Create a trust relationship between the external IdP and a [user-assigned managed identity](workload-identity-federation-create-trust-user-assigned-managed-identity) or [application](workload-identity-federation-create-trust) in Microsoft Entra ID. The federated identity credential is used to indicate which token from the external IdP should be trusted by your application or managed identity. You configure a federated identity either:

- On a user-assigned managed identity through the [Microsoft Entra admin center](https://entra.microsoft.com), Azure CLI, Azure PowerShell, Azure SDK, and Azure Resource Manager (ARM) templates. The external workload uses the access token to access Microsoft Entra protected resources without needing to manage secrets (in supported scenarios). The [steps for configuring the trust relationship](workload-identity-federation-create-trust-user-assigned-managed-identity) differs, depending on the scenario and external IdP.
- On an app registration in the [Microsoft Entra admin center](https://entra.microsoft.com) or through Microsoft Graph. This configuration allows you to get an access token for your application without needing to manage secrets outside Azure. For more information, learn how to [configure an app to trust an external identity provider](workload-identity-federation-create-trust) and how to configure trust between an app and a [user-assigned managed identity](workload-identity-federation-config-app-trust-managed-identity).

Note

The Federated Identity Credential `issuer`, `subject`, and `audience` values must case-sensitively match the corresponding `issuer`, `subject` and `audience` values contained in the token being sent to Microsoft Entra ID by the external IdP in order for the scenario to be authorized. For more information surrounding this change, please visit [What's new for Authentication](../identity-platform/reference-breaking-changes).

The workflow for exchanging an external token for an access token is the same, however, for all scenarios. The following diagram shows the general workflow of a workload exchanging an external token for an access token and then accessing Microsoft Entra protected resources.

![Diagram showing an external token exchanged for an access token and accessing Azure](media/workload-identity-federation/workflow.svg)

1. The external workload (such as a GitHub Actions workflow) requests a token from the external IdP (such as GitHub).
2. The external IdP issues a token to the external workload.
3. The external workload (the sign in action in a GitHub workflow, for example) [sends the token to Microsoft identity platform](../identity-platform/v2-oauth2-client-creds-grant-flow#third-case-access-token-request-with-a-federated-credential) and requests an access token.
4. Microsoft identity platform checks the trust relationship on the [user-assigned managed identity](workload-identity-federation-create-trust-user-assigned-managed-identity) or [app registration](workload-identity-federation-create-trust) and validates the external token against the OpenID Connect (OIDC) issuer URL on the external IdP.
5. When the checks are satisfied, Microsoft identity platform issues an access token to the external workload.
6. The external workload accesses Microsoft Entra protected resources using the access token from Microsoft identity platform. A GitHub Actions workflow, for example, uses the access token to publish a web app to Azure App Service.

The Microsoft identity platform stores only the first 100 signing keys when they're downloaded from the external IdP's OIDC endpoint. If the external IdP exposes more than 100 signing keys, you may experience errors when using workload identity federation.