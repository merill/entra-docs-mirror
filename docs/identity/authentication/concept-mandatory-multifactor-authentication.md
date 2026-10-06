---
layout: Conceptual
title: Plan for mandatory Microsoft Entra multifactor authentication (MFA) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mandatory-multifactor-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about mandatory multifactor authentication (MFA) enforcement for Azure, Microsoft 365, and other admin portals, and how to prepare your tenant.
ms.topic: concept-article
ms.date: 2026-04-03T00:00:00.0000000Z
ms.reviewer: shahjoy, nehakulkarni
ms.custom: sfi-ga-nochange, msecd-doc-authoring-106
locale: en-us
document_id: 40f7b11e-bf19-f28d-df27-7fc27eec36a7
document_version_independent_id: 40f7b11e-bf19-f28d-df27-7fc27eec36a7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-mandatory-multifactor-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-mandatory-multifactor-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-mandatory-multifactor-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
platformId: 4fa07fe3-2539-97d7-8126-a4d71ea5655d
---

# Plan for mandatory Microsoft Entra multifactor authentication (MFA) - Microsoft Entra ID | Microsoft Learn

At Microsoft, we're committed to providing our customers with the highest level of security. One of the most effective security measures available to them is multifactor authentication (MFA). [Research by Microsoft](https://www.microsoft.com/security/blog/2019/08/20/one-simple-action-you-can-take-to-prevent-99-9-percent-of-account-attacks) shows that MFA can block more than 99.2% of account compromise attacks.

That's why, starting in 2024, we'll enforce mandatory MFA for all Azure sign-in attempts. For more background about this requirement, see our blog posts [Azure mandatory multifactor authentication: Phase 2 starting in October 2025](https://azure.microsoft.com/blog/azure-mandatory-multifactor-authentication-phase-2-starting-in-october-2025/) and [Announcing mandatory multifactor authentication for Azure sign-in](https://aka.ms/azuremfablogpost). This topic covers which applications and accounts are affected, how enforcement gets rolled out to tenants, and other common questions and answers.

There's no change for users if your organization already enforces MFA for them, or if they sign in with stronger methods like passwordless or passkey (FIDO2). To verify that MFA is enabled, see [How to verify that users are set up for mandatory MFA](how-to-mandatory-multifactor-authentication).

## Scope of enforcement

The scope of enforcement covers enforcement timing, affected applications, and account requirements.

### Enforcement phases

Note

The date of enforcement for Phase 2 has changed to October 1, 2025.

The enforcement of MFA for applications rolls out in two phases.

#### Phase 1 applications

Starting in October 2024, MFA is required for accounts that sign in to the Azure portal, Microsoft Entra admin center, and Microsoft Intune admin center to perform any Create, Read, Update, or Delete (CRUD) operation. The enforcement will gradually roll out to all tenants worldwide. Starting in February 2025, MFA enforcement gradually begins for sign in to Microsoft 365 admin center. Phase 1 won't impact other Azure clients such as Azure CLI, Azure PowerShell, Azure mobile app, or IaC tools.

#### Phase 2 applications

Starting October 1, 2025, MFA enforcement will gradually begin for accounts that sign in to Azure CLI, Azure PowerShell, Azure mobile app, IaC tools, and REST API endpoints to perform any Create, Update, or Delete operation. Read operations won't require MFA.

Some customers may use a user account in Microsoft Entra ID as a service account. It's recommended to migrate these user-based service accounts to [secure cloud-based service accounts](/en-us/entra/architecture/secure-service-accounts) with [workload identities](../../workload-id/workload-identities-overview).

### Application IDs and URLs

The following table lists affected apps, app IDs, and URLs for Azure.

| Application Name | App ID | Enforcement starts |
| --- | --- | --- |
| [Azure portal](/en-us/azure/azure-portal/) | c44b4083-3bb0-49c1-b47d-974e53cbdf3c | Second half of 2024 |
| [Microsoft Entra admin center](https://aka.ms/MSEntraPortal) | c44b4083-3bb0-49c1-b47d-974e53cbdf3c | Second half of 2024 |
| [Microsoft Intune admin center](https://aka.ms/IntunePortal) | c44b4083-3bb0-49c1-b47d-974e53cbdf3c | Second half of 2024 |
| [Azure command-line interface (Azure CLI)](/en-us/cli/azure/) | 04b07795-8ddb-461a-bbee-02f9e1bf7b46 | October 1, 2025 |
| [Azure PowerShell](/en-us/powershell/azure/) | 1950a258-227b-4e31-a9cf-717495945fc2 | October 1, 2025 |
| [Azure mobile app](/en-us/azure/azure-portal/mobile-app/overview) | 0c1307d4-29d6-4389-a11c-5cbe7f65d7fa | October 1, 2025 |
| [Infrastructure as Code (IaC) tools](/en-us/devops/deliver/what-is-infrastructure-as-code) | Use Azure CLI or Azure PowerShell IDs | October 1, 2025 |
| [REST API (Control Plane)](/en-us/azure/azure-resource-manager/management/control-plane-and-data-plane#control-plane) | N/A | October 1, 2025 |
| [Azure SDK](/en-us/azure/developer/intro/azure-developer-create-resources#azure-sdk-and-rest-apis) | N/A | October 1, 2025 |

The following table lists affected apps and URLs for Microsoft 365.

| Application Name | URL | Enforcement starts |
| --- | --- | --- |
| Microsoft 365 admin center | `https://portal.office.com/adminportal/home` | February 2025 |
| Microsoft 365 admin center | `https://admin.cloud.microsoft` | February 2025 |
| Microsoft 365 admin center | `https://admin.microsoft.com` | February 2025 |

### Accounts

All accounts that sign in to perform operations cited in the applications section must complete MFA when the enforcement begins. Users aren't required to use MFA if they access other applications, websites, or services hosted on Azure. Each application, website, or service owner listed earlier controls the authentication requirements for users.

[Break glass or emergency access accounts](/en-us/entra/identity/role-based-access-control/security-emergency-access) are also required to sign in with MFA once enforcement begins. We recommend that you update these accounts to use [passkey (FIDO2)](how-to-authentication-passkeys-fido2) or configure [certificate-based authentication](how-to-certificate-based-authentication) for MFA. Both methods satisfy the MFA requirement.

Workload identities, such as managed identities and service principals, aren't impacted by either phase of this MFA enforcement. If user identities are used to sign in as a service account to run automation (including scripts or other automated tasks), those user identities need to sign in with MFA once enforcement begins. User identities aren't recommended for automation. You should migrate those user identities to [workload identities](../../workload-id/workload-identities-overview).

### Client libraries

The OAuth 2.0 Resource Owner Password Credentials (ROPC) token grant flow is incompatible with MFA. After MFA is enabled in your Microsoft Entra tenant, ROPC-based APIs used in your applications throw exceptions. For more information about how to migrate from ROPC-based APIs in [Microsoft Authentication Libraries (MSAL)](/en-us/entra/msal/), see [How to migrate away from ROPC](/en-us/entra/identity-platform/v2-oauth-ropc#how-to-migrate-away-from-ropc). For language-specific MSAL guidance, see the following tabs.

# [.NET](#tab/dotnet)
Changes are required if you use the [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) package and one of the following APIs in your application. The public client API is **deprecated**[as of the 4.74.0 release](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet/blob/main/CHANGELOG.md):

- [IByUsernameAndPassword.AcquireTokenByUsernamePassword](/en-us/dotnet/api/microsoft.identity.client.ibyusernameandpassword.acquiretokenbyusernamepassword) (confidential client API)
- [PublicClientApplication.AcquireTokenByUsernamePassword](/en-us/dotnet/api/microsoft.identity.client.publicclientapplication.acquiretokenbyusernamepassword) (public client API) [deprecated]

# [Go](#tab/go)
Changes are required if you use the [microsoft-authentication-library-for-go](https://pkg.go.dev/github.com/AzureAD/microsoft-authentication-library-for-go) module and one of the following APIs in your application:

- [Client.AcquireTokenByUsernamePassword](https://pkg.go.dev/github.com/AzureAD/microsoft-authentication-library-for-go@v1.4.0/apps/confidential#Client.AcquireTokenByUsernamePassword) (confidential client API)
- [Client.AcquireTokenByUsernamePassword](https://pkg.go.dev/github.com/AzureAD/microsoft-authentication-library-for-go@v1.4.0/apps/public#Client.AcquireTokenByUsernamePassword) (public client API) [**deprecated** as of the `1.6.0` release]

# [Java](#tab/java)
Changes are required if you use the [msal4j](https://central.sonatype.com/artifact/com.microsoft.azure/msal4j) package and the following API in your application:

[PublicClientApplication.acquireToken(UserNamePasswordParameters parameters)](/en-us/java/api/com.microsoft.aad.msal4j.publicclientapplication#com-microsoft-aad-msal4j-publicclientapplication-acquiretoken%28com-microsoft-aad-msal4j-usernamepasswordparameters%29) [**deprecated** as of the `1.24.0` release]

# [Node.js](#tab/js)
Changes are required if you use the [@azure/msal-node](https://www.npmjs.com/package/@azure/msal-node) package and one of the following APIs in your application. These APIs are [**deprecated** as of the `3.2.3` release](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/CHANGELOG.md#323-1).

- [ClientApplication.acquireTokenByUsernamePassword](/en-us/javascript/api/@azure/msal-node/confidentialclientapplication#@azure-msal-node-confidentialclientapplication-acquiretokenbyusernamepassword)
- [IConfidentialClientApplication.acquireTokenByUsernamePassword](/en-us/javascript/api/@azure/msal-node/iconfidentialclientapplication#@azure-msal-node-iconfidentialclientapplication-acquiretokenbyusernamepassword)
- [IPublicClientApplication.acquireTokenByUsernamePassword](/en-us/javascript/api/@azure/msal-node/ipublicclientapplication#@azure-msal-node-ipublicclientapplication-acquiretokenbyusernamepassword)

# [Python](#tab/python)
Changes are required if you use the [msal](https://pypi.org/project/msal/) package and the following API in your application:

[ClientApplication.acquire_token_by_username_password](/en-us/python/api/msal/msal.application.clientapplication#msal-application-clientapplication-acquire-token-by-username-password) [**deprecated** for the public client flow as of `1.35.0` release]

---

The same general MSAL guidance applies to the Azure Identity libraries. The `UsernamePasswordCredential` class provided in those libraries uses MSAL ROPC-based APIs. For language-specific guidance, see the following tabs.

# [.NET](#tab/dotnet)
Changes are required if you use the [Azure.Identity](https://www.nuget.org/packages/Azure.Identity) package and do one of the following things in your application:

- Use [DefaultAzureCredential](/en-us/dotnet/api/azure.identity.defaultazurecredential) or [EnvironmentCredential](/en-us/dotnet/api/azure.identity.environmentcredential)with the following two environment variables set:
    - `AZURE_USERNAME`
    - `AZURE_PASSWORD`
- Using `UsernamePasswordCredential` ([**deprecated** as of the `1.14.0-beta.2` release](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/identity/Azure.Identity/CHANGELOG.md#1140-beta2-2025-03-11))

# [Go](#tab/go)
Changes are required if you use the [azidentity](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity) module and do one of the following things in your application:

- Use [DefaultAzureCredential](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity#DefaultAzureCredential) or [EnvironmentCredential](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity#EnvironmentCredential)with the following two environment variables set:
    - `AZURE_USERNAME`
    - `AZURE_PASSWORD`
- Using [UsernamePasswordCredential](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity#UsernamePasswordCredential) ([**deprecated** as of the `1.9.0` release](https://github.com/Azure/azure-sdk-for-go/blob/main/sdk/azidentity/CHANGELOG.md#190-2025-04-08))

# [Java](#tab/java)
Changes are required if you use the [azure-identity](https://central.sonatype.com/artifact/com.azure/azure-identity) package and do one of the following things in your application:

- Use [DefaultAzureCredential](/en-us/java/api/com.azure.identity.defaultazurecredential) or [EnvironmentCredential](/en-us/java/api/com.azure.identity.environmentcredential)with the following two environment variables set:
    - `AZURE_USERNAME`
    - `AZURE_PASSWORD`
- Using [UsernamePasswordCredential](/en-us/java/api/com.azure.identity.usernamepasswordcredential) ([**deprecated** as of the `1.16.0-beta.1` release](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/identity/azure-identity/CHANGELOG.md#1160-beta1-2025-03-13))

# [Node.js](#tab/js)
Changes are required if you use the [@azure/identity](https://www.npmjs.com/package/@azure/identity) package and do one of the following things in your application:

- Use [DefaultAzureCredential](/en-us/javascript/api/@azure/identity/defaultazurecredential) or [EnvironmentCredential](/en-us/javascript/api/@azure/identity/environmentcredential)with the following two environment variables set:
    - `AZURE_USERNAME`
    - `AZURE_PASSWORD`
- Using [UsernamePasswordCredential](/en-us/javascript/api/@azure/identity/usernamepasswordcredential) ([**deprecated** as of the `4.8.0` release](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/identity/identity/CHANGELOG.md#480-2025-03-11))

# [Python](#tab/python)
Changes are required if you use the [azure-identity](https://pypi.org/project/azure-identity) package and do one of the following things in your application:

- Use [DefaultAzureCredential](/en-us/python/api/azure-identity/azure.identity.defaultazurecredential) or [EnvironmentCredential](/en-us/python/api/azure-identity/azure.identity.environmentcredential)with the following two environment variables set:
    - `AZURE_USERNAME`
    - `AZURE_PASSWORD`
- Using [UsernamePasswordCredential](/en-us/python/api/azure-identity/azure.identity.usernamepasswordcredential) ([**deprecated** as of the `1.21.0` release](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/identity/azure-identity/CHANGELOG.md#1210-2025-03-11))

---

### Migrate user-based service accounts to workload identities

We recommend that customers discover user accounts that are used as service accounts and begin to migrate them to workload identities. Migration often requires updating scripts and automation processes to use workload identities.

Review [How to verify that users are set up for mandatory MFA](how-to-mandatory-multifactor-authentication) to identify all user accounts, including user accounts being used as service accounts, that sign in to the applications.

For more information about how to migrate from user-based service accounts to workload identities for authentication with these applications, see:

- [Sign in to Azure with a managed identity using the Azure CLI](/en-us/cli/azure/authenticate-azure-cli-managed-identity)
- [Sign in to Azure with a service principal using the Azure CLI](/en-us/cli/azure/authenticate-azure-cli-service-principal)
- [Sign in to Azure PowerShell non-interactively for automation scenarios](/en-us/powershell/azure/authenticate-noninteractive) includes guidance for both managed identity and service principal use cases

Some customers apply Conditional Access policies to user-based service accounts. You can reclaim the user-based license, and add a [workload identities](../../workload-id/workload-identities-overview) license to apply [Conditional Access for workload identities](../conditional-access/workload-identity).

## Migrate federated Identity Provider to external MFA

Support for external MFA solutions is available with [external MFA](https://aka.ms/EAMAdminDocs), and can be used to meet the MFA requirement. The legacy Conditional Access custom controls preview doesn't satisfy the MFA requirement. You should migrate to external MFA to use an external solution with Microsoft Entra ID.

If you're using a federated Identity Provider (IdP), such as Active Directory Federation Services, and your MFA provider is integrated directly with this federated IdP, the federated IdP must be configured to send an MFA claim. For more information, see [Expected inbound assertions for Microsoft Entra MFA](how-to-mfa-expected-inbound-assertions).

## Prepare for mandatory MFA enforcement

To prepare for MFA enforcement, configure a [Conditional Access policy](how-to-mandatory-multifactor-authentication#verify-mfa-is-enabled-for-microsoft-entra-id-p1-or-microsoft-entra-id-p2-license) that requires users to sign in with MFA. If you configured exceptions or exclusions in the policy, they no longer apply. If you have more restrictive Conditional Access policies that target Azure and require stronger authentication, such as phishing-resistant MFA, they remain enforced.

Conditional Access requires a Microsoft Entra ID P1 or P2 license. If you can't use Conditional Access, enable [security defaults](../../fundamentals/security-defaults).

You can self-enforce MFA by using built-in definitions in Azure Policy. To learn more and follow a step-by-step overview to apply these policy assignments in your environment, see [Tutorial: Apply MFA self-enforcement through Azure Policy](/en-us/azure/governance/policy/tutorials/mfa-enforcement). Azure Policy supports both the `Audit` effect (which reports noncompliance in policy compliance results) and the `Deny` effect, which blocks noncompliant requests.

For the best compatibility experience, ensure users in your tenant are using Azure CLI version 2.76 and Azure PowerShell version 14.3 or later. Otherwise, you can expect to see error messages as explained in these topics:

- [Troubleshoot MFA errors in Azure PowerShell](/en-us/powershell/azure/troubleshooting#troubleshooting-multifactor-authentication-mfa)
- [Troubleshoot MFA errors in Azure CLI](/en-us/cli/azure/use-azure-cli-successfully-troubleshooting#troubleshooting-multifactor-authentication-mfa)

Note

Users who sign in without MFA can use a Phase 2 application. But if they try to create, update, or delete a resource, the app returns an error that says they need to sign in with MFA and a claims challenge. Some clients use the claims challenge to prompt the user to step up and perform MFA. Other clients return only the error without an MFA prompt. A Conditional Access policy or security defaults are recommended to help users satisfy MFA before they see an error.

## Request more time to prepare for Phase 1 MFA enforcement

We understand that some customers may need more time to prepare for this MFA requirement. Microsoft allows customers with complex environments or technical barriers to postpone the enforcement of Phase 1 for their tenants until September 30, 2025.

For each tenant where they want to postpone the start date of enforcement, a Global Administrator can go to the https://aka.ms/managemfaforazure to select a start date.

Caution

By postponing the start date of enforcement, you take extra risk because accounts that access Microsoft services like the Azure portal are highly valuable targets for threat actors. We recommend all tenants set up MFA now to secure cloud resources.

## Request more time to prepare for Phase 2 MFA enforcement

Microsoft allows customers with complex environments or technical barriers to postpone the enforcement of Phase 2 for their tenants until July 1st, 2026. You can request more time to prepare for Phase 2 MFA enforcement at https://aka.ms/postponePhase2MFA. Choose another start date, and select **Apply**. After Phase 2 enforcement begins, you can submit a request to Microsoft Help and Support to temporarily lift enforcement. The request must be done by a Global Administrator due to the security implications.

Note

If you postponed the start of Phase 1, the start of Phase 2 is also postponed to the same date. You can choose a later start date for Phase 2.

![Screenshot of how to postpone mandatory MFA for phase two.](media/concept-mandatory-multifactor-authentication/postpone-phase-two.png)

## Confirm mandatory MFA enforcement

### Confirm Phase 1 enforcement

To confirm that Phase 1 mandatory MFA is enforced for your tenant:

1. Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Browse to https://aka.ms/managemfaforazure.
3. Verify that the **Multifactor authentication (Phase 1)** page shows a banner that confirms enforcement began for your tenant.

    ![Screenshot of the Multifactor authentication Phase 1 page in the Azure portal, showing that MFA is enforced for all users in the directory.](media/concept-mandatory-multifactor-authentication/phase-1-confirm.png)

### Confirm Phase 2 enforcement

To confirm that Phase 2 mandatory MFA is enforced for your tenant:

1. Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Browse to https://aka.ms/postponePhase2MFA.
3. Verify that the **Multifactor authentication (Phase 2)** page shows a banner that confirms enforcement began for your tenant.

    ![Screenshot of the Multifactor authentication Phase 2 page in the Azure portal, showing that MFA enforcement began on or after February 20, 2026.](media/concept-mandatory-multifactor-authentication/phase-2-confirm.png)

Microsoft Entra ID [sign-in logs](../monitoring-health/concept-sign-ins) show the application that enforced MFA as the source of the MFA requirement.

## FAQs

**Question**: Which accounts are affected by Phase 2 MFA enforcement?

**Answer**: Azure Phase 2 enforcement applies to all user accounts that make Azure resource management actions through any Azure client, including PowerShell, CLI, SDKs, or even REST APIs. This enforcement is on the Azure Resource Manager server side, so any requests that target `https://management.azure.com` are under scope of enforcement. Automation accounts are not in scope as long as they use a managed identity or service principal. Any automation accounts that are set up as user identities will be enforced upon.

**Question**: How can I understand the impact of MFA enforcement without Conditional Access?

**Answer**: If your Microsoft Entra ID license doesn't include Conditional Access, you can use Azure Policy to understand how MFA enforcement impacts your tenant. During system enforcement, Microsoft deploys the [Azure Policy](/en-us/azure/governance/policy/tutorials/mfa-enforcement) to your tenant. You can follow those steps to deploy the same Azure policy yourself at any time. You can deploy the policy in Audit mode, and then convert to Enforcement mode. You can choose the date to apply this policy in your tenant while you are in Enforcement mode. Then when Microsoft enforces MFA, there's no further impact to your tenant.

**Question**: Are there any exceptions for specific accounts?

**Answer**: The system enforcement applies to all user accounts, regardless if they are a student account, break-glass account, an administrator account with activated or eligible roles, or any [user exclusions](../conditional-access/policy-all-users-mfa-strength#user-exclusions) that are enabled for them. Each of these account types can perform resource management actions in Azure, posing the same security risk if they are compromised.

**Question**: Are Microsoft Graph APIs under the scope for Phase 2 enforcement?

**Answer**: Generally, Microsoft Graph APIs aren't in scope for Azure MFA enforcement. Only requests sent to `https://management.azure.com/` are under scope of enforcement.

**Question**: If the tenant is only used for testing, is MFA required?

**Answer**: Yes, every Azure tenant will require MFA, with no exception for test environments.

**Question**: How does this requirement impact the Microsoft 365 admin center?

**Answer**: Mandatory MFA will roll out to the Microsoft 365 admin center starting in February 2025. Learn more about the mandatory MFA requirement for the Microsoft 365 admin center on the blog post [Announcing mandatory multifactor authentication for the Microsoft 365 admin center](https://techcommunity.microsoft.com/t5/microsoft-365-blog/microsoft-will-require-mfa-to-access-the-microsoft-365-admin/ba-p/4232568).

**Question**: Do I need to complete MFA if I choose the option to **Stay signed in**?

**Answer**: Yes, even if you choose **Stay signed in**, you're required to complete MFA before you can sign in to these applications.

**Question**: Does the enforcement apply to B2B guest accounts?

**Answer**: Yes, MFA has to be adhered to either from the partner resource tenant, or the user's home tenant if it's set up properly to send MFA claims to the resource tenant by using cross-tenant access.

**Question**: Does the enforcement apply to Azure for US Government or Azure sovereign clouds?

**Answer**: Microsoft enforces mandatory MFA only in the public Azure cloud. Microsoft doesn't currently enforce MFA in Azure for US Government or other Azure sovereign clouds.

**Question**: How can we comply if we enforce MFA by using another identity provider or MFA solution, and we don't enforce by using Microsoft Entra MFA?

**Answer**: Third-party MFA can be integrated directly with Microsoft Entra ID. For more information, see [Microsoft Entra multifactor authentication external method provider reference](concept-authentication-external-method-provider). Microsoft Entra ID can be optionally configured with a federated identity provider. If so, the identity provider solution needs to be configured properly to send the `multipleauthn` claim to Microsoft Entra ID. For more information, see [Satisfy Microsoft Entra ID multifactor authentication (MFA) controls with MFA claims from a federated IdP](how-to-mfa-expected-inbound-assertions).

**Question**: Will mandatory MFA impact my ability to sync with Microsoft Entra Connect or Microsoft Entra Cloud Sync?

**Answer**: No. The synchronization service account isn't affected by the mandatory MFA requirement. Only applications listed earlier require MFA for sign in.

**Question**: Will I be able to opt out?

**Answer**: There's no way to opt out. This security motion is critical to the safety and security of the Azure platform and is being repeated across cloud vendors. For example, see [Secure by Design: AWS to enhance MFA requirements in 2024](https://aws.amazon.com/blogs/security/security-by-design-aws-to-enhance-mfa-requirements-in-2024/).

An option to postpone the enforcement start date is available for customers. Global Administrators can go to the [Azure portal](https://aka.ms/managemfaforazure) to postpone the start date of enforcement for their tenant. Global Administrators must have [elevated access](https://aka.ms/enableelevatedaccess) before they postpone the start date of MFA enforcement on this page. They must perform this action for each tenant that needs postponement.

**Question**: Can I test MFA before Azure enforces the policy to ensure nothing breaks?

**Answer**: Yes, you can [test your MFA](tutorial-enable-azure-mfa#test-microsoft-entra-multifactor-authentication) through the manual setup process for MFA. We encourage you to set this up and test. If you use Conditional Access to enforce MFA, you can use Conditional Access templates to test your policy. For more information, see [Require multifactor authentication for admins accessing Microsoft admin portals](../conditional-access/policy-old-require-mfa-admin-portals). If you run a free edition of Microsoft Entra ID, you can enable [security defaults](../../fundamentals/security-defaults).

**Question**: What if I already have MFA enabled, what happens next?

**Answer**: Customers that already require MFA for their users who access the applications listed earlier don't see any change. If you only require MFA for a subset of users, then any users not already using MFA will now need to use MFA when they sign in to the applications.

**Question**: How can I review MFA activity in Microsoft Entra ID?

**Answer**: To review details about when a user is prompted to sign in with MFA, use the Microsoft Entra sign-in logs. For more information, see [Sign-in event details for Microsoft Entra multifactor authentication](howto-mfa-reporting).

**Question**: What if I have a "break glass" scenario?

**Answer**: We recommend updating these accounts to use [passkey (FIDO2)](how-to-authentication-passkeys-fido2) or configure [certificate-based authentication](how-to-certificate-based-authentication) for MFA. Both methods satisfy the MFA requirement.

**Question**: What if I don't receive an email about enabling MFA before it was enforced, and then I get locked-out. How should I resolve it?

**Answer**: Users shouldn't be locked out, but they may get a message that prompts them to enable MFA once enforcement for their tenant has started. If the user is locked out, there may be other issues. For more information, see [Account has been locked](https://support.microsoft.com/account-billing/account-has-been-locked-805e8b0d-4141-29b2-7b65-df6ff6c9ce27).