---
layout: Conceptual
title: Home Realm Discovery Policy for an Application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/home-realm-discovery-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to manage the Home Realm Discovery policy for Microsoft Entra authentication for federated users, including auto-acceleration and domain hints.
ms.topic: concept-article
ms.date: 2024-11-26T00:00:00.0000000Z
ms.reviewer: sreyanth, ludwignick
ms.custom: enterprise-apps, no-azure-ad-ps-ref sfi-ropc-nochange
locale: en-us
document_id: 9798ee3a-fb6f-01fc-be29-fffcad317e4a
document_version_independent_id: 5c80c0fd-c6ca-28b8-091c-b4afa31319cd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/home-realm-discovery-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/home-realm-discovery-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/home-realm-discovery-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 54468e37-16a7-ad3b-ddfa-02199f04e665
---

# Home Realm Discovery Policy for an Application - Microsoft Entra ID | Microsoft Learn

Home Realm Discovery (HRD) enables Microsoft Entra ID to identify the appropriate identity provider (IdP) for user authentication during sign-in. When users sign in to a Microsoft Entra tenant to access a resource or the common sign-in page, they enter a user principal name (UPN). Microsoft Entra ID uses this information to determine the correct sign-in location.

Users are directed to one of the following identity providers for authentication:

- The user's home tenant (which might be the same as the resource tenant).
- A Microsoft account, if the user is a guest in the resource tenant and uses a consumer account.
- An on-premises identity provider like Active Directory Federation Services (AD FS).
- Another identity provider federated with the Microsoft Entra tenant.

## Auto-acceleration

Organizations might configure domains in their Microsoft Entra tenant to federate with another IdP, such as AD FS, for user authentication. When users sign in to an application, they initially see a Microsoft Entra sign-in page. If they belong to a federated domain, they're redirected to the IdP's sign-in page for that domain. Administrators might want to bypass the initial Microsoft Entra ID page for specific applications. This process is called *sign-in auto-acceleration*.

Microsoft advises against configuring auto-acceleration because it can hinder stronger authentication methods like FIDO and collaboration. For more information, see [Enable passwordless security key sign-in](../authentication/howto-authentication-passwordless-security-key). To learn how to prevent sign-in auto-acceleration, see [Disable auto-acceleration sign-in](prevent-domain-hints-with-home-realm-discovery).

Auto-acceleration can streamline sign-in for tenants federated with another IdP. You can configure it for individual applications. To learn how to force auto-acceleration by using HRD, See [Configure auto-acceleration](configure-authentication-for-federated-users-portal).

Note

Configuring an application for auto-acceleration prevents users from using managed credentials (like FIDO) and guest users from signing in. Directing users to a federated IdP for authentication bypasses the Microsoft Entra sign-in page and prevents guest users from accessing other tenants or external IdPs, like Microsoft accounts.

You can control auto-acceleration to a federated IdP in three ways:

- Use a domain hint on authentication requests for an application.
- Configure an HRD policy to [force auto-acceleration](configure-authentication-for-federated-users-portal).
- Configure an HRD policy to [ignore domain hints](prevent-domain-hints-with-home-realm-discovery) for specific applications or domains.

## Domain confirmation dialog

As of April 2023, organizations that use auto-acceleration or smart links might encounter a domain confirmation dialog in the sign-in UI. This dialog is part of Microsoft's security hardening efforts and requires users to confirm the domain of the tenant that they're signing in to.

### What you need to do

When the domain confirmation dialog appears, check the domain. Verify that the domain name in the dialog matches the organization that you intend to sign in to.

If you recognize the domain, select **Confirm** to proceed. If you don't recognize the domain, cancel the sign-in process and contact your IT admin for assistance.

### Components of the domain confirmation dialog

The following screenshot shows an example of what the domain confirmation dialog might look like.

![Screenshot of the domain confirmation dialog that shows a sign-in identifier and a tenant domain.](media/home-realm-discovery-policy/domain-confirmation-dialog-new.png)

The identifier at the top of the dialog, `kelly@contoso.com`, represents the identifier for signing in. The dialog's heading and text show the domain of the account's home tenant.

This dialog might not appear for every instance of auto-acceleration or smart links. Frequent domain confirmation dialogs might occur if your organization clears cookies due to browser policies.

The domain confirmation dialog shouldn't cause application breakages, because Microsoft Entra ID manages the auto-acceleration sign-in flow.

## Domain hints

Domain hints are directives in authentication requests from applications that can accelerate users to their federated IdP sign-in page. Multitenant applications can use them to direct users to the branded Microsoft Entra sign-in page for their tenant.

For example, `largeapp.com` might allow access via a custom URL `contoso.largeapp.com` and include a domain hint to `contoso.com` in the authentication request.

Domain hint syntax varies by protocol:

- **WS-Federation**: `whr` query string parameter; for example, `whr=contoso.com`.
- **SAML**: SAML authentication request with a domain hint or `whr=contoso.com`.
- **OpenID Connect**: `domain_hint` query string parameter; for example, `domain_hint=contoso.com`.

Microsoft Entra ID redirects sign-in to the configured IdP for a domain if *both* of the following cases are true:

- A domain hint is included in the authentication request.
- The tenant is federated with that domain.

If the domain hint doesn't refer to a verified federated domain, it can be ignored.

Note

A domain hint in an authentication request overrides auto-acceleration set for the application in an HRD policy.

### HRD policy for auto-acceleration

Some applications don't allow configuration of authentication requests. In such cases, it's not possible to use domain hints to control auto-acceleration. Use a [Home Realm Discovery](configure-authentication-for-federated-users-portal) policy to configure auto-acceleration.

### HRD policy to prevent auto-acceleration

Some Microsoft and software as a service (SaaS) applications automatically include domain hints, which can disrupt managed credential rollouts like FIDO. Use a [Home Realm Discovery policy to ignore domain hints](prevent-domain-hints-with-home-realm-discovery) from certain apps or domains during managed credential rollouts.

## Direct ROPC authentication of federated users for legacy applications

The best practice is for applications to use Microsoft Entra libraries and interactive sign-in for user authentication. Legacy applications that use Resource Owner Password Credentials (ROPC) grants might submit credentials directly to Microsoft Entra ID without understanding federation. They don't perform HRD or interact with the correct federated endpoint. You can use a [Home Realm Discovery policy to enable specific legacy applications](configure-authentication-for-federated-users-portal) to authenticate directly with Microsoft Entra ID. This option works if password hash synchronization is enabled.

Important

Enable direct authentication only if password hash synchronization is active and if authenticating the application without on-premises IdP policies is acceptable. If password hash synchronization or directory synchronization with Microsoft Entra Connect is disabled, remove this policy to prevent direct authentication with stale password hashes.

## Steps for setting an HRD policy

To set an HRD policy on an application for federated sign-in auto-acceleration or direct cloud-based applications:

1. Create an HRD policy.
2. Locate the service principal to attach the policy.
3. Attach the policy to the service principal.

Policies take effect for a specific application when they're attached to a service principal. Only one HRD policy can be active on a service principal at a time. Use [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) cmdlets to create and manage the HRD policy.

Here's an example HRD policy definition:

```json
{  
  "HomeRealmDiscoveryPolicy": {  
    "AccelerateToFederatedDomain": true,  
    "PreferredDomain": "federated.example.edu",  
    "AllowCloudPasswordValidation": false  
  }  
}  
```

- `AccelerateToFederatedDomain`: Optional. If the value is `false`, the policy doesn't affect auto-acceleration. If the value is `true` and there's one verified federated domain, users are directed to the federated IdP. If multiple domains exist, specify `PreferredDomain`.
- `PreferredDomain`: Optional. Indicates a domain for acceleration. Omit it if only one federated domain exists. If it's omitted with multiple domains, the policy has no effect.
- `AllowCloudPasswordValidation`: Optional. If the value is `true`, this setting allows federated user authentication via username/password credentials directly to a Microsoft Entra token endpoint, and it requires password hash synchronization.

Additional tenant-level HRD options are:

- `AlternateIdLogin`: Optional. Enables [AlternateLoginID](../authentication/howto-authentication-use-email-signin) for email sign-in instead of UPN at the Microsoft Entra sign-in page. Relies on users not being auto-accelerated to a federated IDP.
- `DomainHintPolicy`: Optional complex object that [prevents domain hints from auto-accelerating users](prevent-domain-hints-with-home-realm-discovery) to federated domains. Ensures that applications that send domain hints don't prevent cloud-managed credential sign-ins.

### Priority and evaluation of HRD policies

You can assign HRD policies to organizations and service principals so that multiple policies can apply to an application. Microsoft Entra ID determines precedence by using these rules:

- If a domain hint is present, the tenant's HRD policy checks if domain hints should be ignored. If domain hints are allowed, Microsoft Entra ID uses the domain hint behavior.
- If a policy is explicitly assigned to the service principal, Microsoft Entra ID enforces it.
- If no domain hint or service principal policy exists, Microsoft Entra ID enforces a policy assigned to the parent organization.
- If no domain hint or policies are assigned, default HRD behavior applies.

Note

HRD policies don't work with brokered authentication on mobile platforms and macOS. This restriction includes using the Microsoft Authenticator app on mobile platforms or the Company Portal app on Mac. If auto-acceleration is necessary in these cases, a domain hint must be passed in the authentication request of the calling app.