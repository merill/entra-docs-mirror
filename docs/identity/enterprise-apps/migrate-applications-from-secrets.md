---
layout: Conceptual
title: Migrate applications away from secret-based authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-applications-from-secrets
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Migrate applications away from secret-based authentication to improve security and user experience.
ms.topic: concept-article
ms.date: 2025-03-19T00:00:00.0000000Z
locale: en-us
document_id: 11c868ce-c95f-8140-8ce5-8fc51b1b43dc
document_version_independent_id: 11c868ce-c95f-8140-8ce5-8fc51b1b43dc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migrate-applications-from-secrets.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migrate-applications-from-secrets
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migrate-applications-from-secrets.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
platformId: 36218970-d2c3-a0ec-0ed8-7296adedec9a
---

# Migrate applications away from secret-based authentication - Microsoft Entra ID | Microsoft Learn

Applications that use client secrets might store them in configuration files, hardcode them in scripts, or risk their exposure in other ways. Secret management complexities make secrets susceptible to leaks and attractive to attackers. Client secrets, when exposed, provide attackers with legitimate credentials to blend their activities with legitimate operations, making it easier to bypass security controls. If an attacker compromises an application’s client secret, they can escalate their privileges within the system, leading to broader access and control, depending on the permissions of the application. Replacing a compromised certificate can be incredibly time-consuming and disruptive. For these reasons, Microsoft recommends that all of our customers move away from password or certificate-based authentication to token-based authentication.

In this article, we highlight resources and best practices to help you migrate your applications away from secret-based authentication to more secure and user-friendly authentication methods.

## Why migrate applications away from secret-based authentication?

Migrating applications away from secret-based authentication offers several benefits:

- **Improved security**: Secret-based authentication is susceptible to leaks and attacks. Migrating to more secure authentication methods, such as managed identities, improves security.
- **Reduced complexity**: Managing secrets can be complex and error-prone. Migrating to more secure authentication methods reduces complexity and improves security.
- **Scalability**: Migrating to more secure authentication methods helps you scale your applications securely.
- **Compliance**: Migrating to more secure authentication methods helps you meet compliance requirements and security best practices.

## Best practices for migrating applications away from secret-based authentication

To migrate applications away from secret-based authentication, consider the following best practices:

### Use managed identities for Azure resources

Managed identities are a secure way to authenticate applications to cloud services without the need to manage credentials or to have credentials in your code. Azure services use this identity to authenticate to services that support Microsoft Entra authentication. To learn more, see [Assign a managed identity access to an application role](../managed-identities-azure-resources/how-to-assign-app-role-managed-identity).

For applications that can't be migrated in the short term, rotate the secret and ensure they use secure practices such as using Azure Key Vault. Azure Key Vault helps you safeguard cryptographic keys and secrets used by cloud applications and services. Keys, secrets, and certificates are protected without you having to write the code yourself, and you can easily use them from your applications. To learn more, see [Azure Key Vault](/en-us/azure/key-vault/general/developers-guide).

### Deploy Conditional Access policies for workload identities

Conditional Access for workload identities enables you to block service principals from outside of known public IP ranges, based on risk detected by Microsoft Entra Protection or in combination with authentication contexts. To learn more, see [Conditional Access for workload identities](../conditional-access/workload-identity).

Important

Workload Identities Premium licenses are required to create or modify Conditional Access policies scoped to service principals. In directories without appropriate licenses, existing Conditional Access policies for workload identities continue to function, but can't be modified. For more information, see [Microsoft Entra Workload ID](https://www.microsoft.com/security/business/identity-access/microsoft-entra-workload-identities#office-StandaloneSKU-k3hubfz). 

### Implement secret scanning

Secret scanning for your repository checks for any secrets that might already exist in your source code across history and push protection prevents any new secrets from being exposed in source code. To learn more, see [Secret scanning](/en-us/azure/devops/repos/security/github-advanced-security-secret-scanning).

### Deploy application authentication policies to enforce secure authentication practices

Application management policies allow IT admins to enforce best practices for how apps in their organizations should be configured. For example, an admin might configure a policy to block the use or limit the lifetime of password secrets. To learn more, see [Tutorial: Enforce secret and certificate standards using application management policies](tutorial-enforce-secret-standards) and [Microsoft Entra application management policies API overview](/en-us/graph/api/resources/applicationauthenticationmethodpolicy).

Important

Premium licenses are required to implement application authentication policy management, for more information, see [Microsoft Entra licensing](../../fundamentals/licensing). 

### Use federated identity for service accounts

Identity federation allows you to access Microsoft Entra protected resources without needing to manage secrets (for supported scenarios) by creating a trust relationship between an external identity provider (IdP) and an app in Microsoft Entra ID by configuring a federated identity credential. To learn more, see [Overview of federated identity credentials in Microsoft Entra ID](/en-us/graph/api/resources/federatedidentitycredentials-overview).

### Create a least-privileged custom role to rotate application credentials

Microsoft Entra roles allow you to grant granular permissions to your admins, abiding by the principle of least privilege. A custom role can be created to rotate application credentials, ensuring that only the necessary permissions are granted to complete the task. To learn more, see [Create a custom role in Microsoft Entra ID](../role-based-access-control/custom-create).

### Ensure you have a process to triage and monitor applications

This process should include regular security assessments, vulnerability scanning, and incident response procedures. Awareness of the security posture of your applications is essential to maintaining a secure environment.