---
layout: Conceptual
title: Add and manage app credentials in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-add-credentials
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn to configure certificates, client secrets, and federated credentials in Microsoft Entra for secure app authentication.
manager: pmwongera
ms.custom: 
ms.date: 2025-03-26T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: c7db32c2-89ae-ce2c-f0da-9b4181f41af2
document_version_independent_id: c7db32c2-89ae-ce2c-f0da-9b4181f41af2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-add-credentials.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-add-credentials
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-add-credentials.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5d69211f-5106-cef4-4a6e-c3d04ebac455
---

# Add and manage app credentials in Microsoft Entra ID - Microsoft identity platform | Microsoft Learn

When building confidential client applications, managing credentials effectively is critical. This article explains how to add client certificates, federated identity credentials, or client secrets to your app registration in Microsoft Entra. These credentials enable your application to authenticate itself securely and access web APIs without user interaction.

## Prerequisites

[Quickstart: Register an app in Microsoft Entra ID](quickstart-register-app).

## Add a credential to your application

When you create credentials for a confidential client application:

- Microsoft recommends that you use a certificate instead of a client secret before moving the application to a production environment. For more information on how to use a certificate, see instructions in [Microsoft identity platform application authentication certificate credentials](certificate-credentials).
- For testing purposes, you can create a self-signed certificate and configure your apps to authenticate with it. However, **in production**, you should purchase a certificate signed by a well-known certificate authority, then use [Azure Key Vault](/en-us/azure/key-vault/general/overview) to manage certificate access and lifetime.

To learn more about client secret vulnerabilities, refer to [Migrate applications away from secret-based authentication](/en-us/entra/identity/enterprise-apps/migrate-applications-from-secrets).

# [Add a certificate](#tab/certificate)
Sometimes called a *public key*, a certificate is the recommended credential type because they're considered more secure than client secrets.

1. In the Microsoft Entra admin center, in **App registrations**, select your application.
2. Select **Certificates & secrets** &gt; **Certificates** &gt; **Upload certificate**.
3. Select the file you want to upload. It must be one of the following file types: *.cer*, *.pem*, *.crt*.
4. Select **Add**.
5. Record the certificate **Thumbprint** for use in your client application code.

    [![Screenshot of the Microsoft Entra admin center, showing the Certificates tab in the Certificates and secrets pane in an app registration.](media/quickstart-register-app/add-client-certificate.png)](media/quickstart-register-app/add-client-certificate.png#lightbox)

# [Add a client secret](#tab/client-secret)
Sometimes called an *application password*, a client secret is a string value your app can use in place of a certificate to identify itself.

Client secrets are less secure than certificate or federated credentials and therefore should **not be used** in production environments. While they may be convenient for local app development, it's imperative to use certificate or federated credentials for any applications running in production to ensure higher security.

1. In the Microsoft Entra admin center, in **App registrations**, select your application.
2. Select **Certificates & secrets** &gt; **Client secrets** &gt; **New client secret**.
3. Add a description for your client secret.
4. Select an expiration for the secret or specify a custom lifetime.

    - Client secret lifetime is limited to two years (24 months) or less. You can't specify a custom lifetime longer than 24 months.
    - Microsoft recommends that you set an expiration value of less than 12 months.
5. Select **Add**.
6. Record the client secret **Value** for use in your client application code. This secret value is *never displayed again* after you leave this page.

    [![Screenshot of the Microsoft Entra admin center, showing the Client secrets tab in the Certificates and secrets pane in an app registration.](media/quickstart-register-app/add-client-secret.png)](media/quickstart-register-app/add-client-secret.png#lightbox)

Note

If you're using an Azure DevOps service connection that automatically creates a service principal, you need to update the client secret from the Azure DevOps portal site instead of directly updating the client secret. Refer to this document on how to update the client secret from the Azure DevOps portal site: [Troubleshoot Azure Resource Manager service connections](/en-us/azure/devops/pipelines/release/azure-rm-endpoint#service-principals-token-expired).

# [Add a federated credential](#tab/federated-credential)
Federated identity credentials are a type of credential that allows workloads, such as GitHub Actions, workloads running on Kubernetes, or workloads running in compute platforms outside of Azure access Microsoft Entra protected resources without needing to manage secrets using [workload identity federation](../workload-id/workload-identity-federation).

To add a federated credential, follow these steps:

1. In the Microsoft Entra admin center, in **App registrations**, select your application.
2. Select **Certificates & secrets** &gt; **Federated credentials** &gt; **Add credential**.

    [![Screenshot of the Microsoft Entra admin center, showing the Certificates and secrets pane in an app registration.](media/quickstart-register-app/add-federated-credential.png)](media/quickstart-register-app/add-federated-credential.png#lightbox)
3. In the **Federated credential scenario** drop-down box, select one of the supported scenarios, and follow the corresponding guidance to complete the configuration.

    - **Customer managed keys** for encrypting data in your tenant using Azure Key Vault in another tenant.
    - **GitHub actions deploying Azure resources** to [configure a GitHub workflow](../workload-id/workload-identity-federation-create-trust#github-actions) to get tokens for your application and deploy assets to Azure.
    - **Kubernetes accessing Azure resources** to configure a [Kubernetes service account](../workload-id/workload-identity-federation-create-trust#kubernetes) to get tokens for your application and access Azure resources.
    - **Other issuer** to configure the application to [trust a managed identity](../workload-id/workload-identity-federation-config-app-trust-managed-identity) or an identity managed by an external [OpenID Connect provider](../workload-id/workload-identity-federation-create-trust#other-identity-providers) to get tokens for your application and access Azure resources.

For more information on how to get an access token with a federated credential, see [Microsoft identity platform and the OAuth 2.0 client credentials flow](v2-oauth2-client-creds-grant-flow#third-case-access-token-request-with-a-federated-credential).

---