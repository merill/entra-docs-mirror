---
layout: Conceptual
title: Migrate from federation to Microsoft Entra CBA - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-certificate-based-authentication-migration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to migrate from Federated server to Microsoft Entra ID
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: vimrang
ms.custom: has-adal-ref
locale: en-us
document_id: a06ab480-6afe-5820-3691-28dc4277a1b7
document_version_independent_id: a9e6aa53-52d1-e57c-92c0-fe8485254608
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-certificate-based-authentication-migration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-certificate-based-authentication-migration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-certificate-based-authentication-migration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: ec42b34b-1955-eff4-c01f-46ca3d8a2bf5
---

# Migrate from federation to Microsoft Entra CBA - Microsoft Entra ID | Microsoft Learn

This article explains how to migrate from running federated servers such as Active Directory Federation Services (AD FS) on-premises to cloud authentication using Microsoft Entra certificate-based authentication (CBA).

## Staged Rollout

A tenant admin could cut the federated domain fully over to Microsoft Entra CBA without pilot testing. This is done by enabling the CBA auth method in Microsoft Entra ID and converting the entire domain to managed authentication. However, if customer wants to test a small batch of users authenticate against Microsoft Entra CBA before the full domain cutover to managed, they can make use of staged rollout feature.

[Staged Rollout](../hybrid/connect/how-to-connect-staged-rollout) for Certificate-based Authentication (CBA) helps customers transition from performing CBA at a federated IdP to Microsoft Entra ID by selectively moving small set of users to use CBA at Microsoft Entra ID (no longer being redirected to the federated IdP) with selected groups of users before then converting the domain configuration in Microsoft Entra ID from federated to managed. Staged rollout isn't designed for the domain to remain federated for long periods of time or for large amounts of users.

Watch this quick video demonstrating the migration from ADFS certificate-based authentication to Microsoft Entra CBA

Note

When Staged rollout is enabled for a user, the user is considered a managed user and all authentication happens at Microsoft Entra ID. For a federated Tenant, if CBA is enabled on Staged Rollout, password authentication only works if PHS is enabled too. Otherwise, password authentication fails.

## Enable Staged Rollout for certificate-based authentication on your tenant

To configure Staged Rollout, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Search for and select **Microsoft Entra Connect**.
3. On the Microsoft Entra Connect page, under the Staged Rollout of cloud authentication, select **Enable Staged Rollout for managed user sign-in**.
4. On the **Enable Staged Rollout** feature page, select **On** for the option [Certificate-based authentication](certificate-based-authentication-federation-get-started)
5. Select **Manage groups** and add groups you want to be part of cloud authentication. To avoid a time-out, ensure that the security groups contain no more than 200 members initially.

Note

Microsoft recommends using separate groups to manage staged rollout for Entra certificate-based authentication and the certificate-based authentication method policy

For more information, see [Staged Rollout](../hybrid/connect/how-to-connect-staged-rollout).

## Use Microsoft Entra Connect to update certificateUserIds attribute

An AD FS admin can use **Synchronization Rules Editor** to create rules to sync the values of attributes from AD FS to Microsoft Entra user objects. For more information, see [Sync rules for certificateUserIds](concept-certificate-based-authentication-certificateuserids#update-certificate-user-ids-using-azure-ad-connect).

Microsoft Entra Connect requires a special role named **Hybrid Identity Administrator**, which grants the necessary permissions. You need this role for permission to write to the new cloud attribute.

Note

If a user is using synchronized attributes, such as the onPremisesUserPrincipalName attribute in the user object for username binding, then any user that has administrative access to the Microsoft Entra Connect server can change the synchronized attribute mapping, and change the value of the synchronized attribute. The user doesn't need to be a cloud admin. The AD FS admin should make sure the administrative access to the Microsoft Entra Connect server should be limited, and privileged accounts should be cloud-only accounts.

## Frequently asked questions about migrating from AD FS to Microsoft Entra ID

### Can we have privileged accounts with a federated AD FS server?

Although it's possible, Microsoft recommends privileged accounts be cloud-only accounts. Using cloud-only accounts for privileged access limits exposure in Microsoft Entra ID from a compromised on-premises environment. For more information, see [Protecting Microsoft 365 from on-premises attacks](../../architecture/protect-m365-from-on-premises-attacks).

### If an organization is a hybrid running both AD FS and Azure CBA, are they still vulnerable to the AD FS compromise?

Microsoft recommends privileged accounts be cloud-only accounts. This practice limits the exposure in Microsoft Entra ID from a compromised on-premises environment. Maintaining privileged accounts a cloud-only is foundational to this goal.

For synchronized accounts:

- If they're in a managed domain (not federated), there's no risk from the federated IdP.
- If they're in a federated domain, but a subset of accounts is being moved to Microsoft Entra CBA by Staged Rollout, they're subject to risks related to the federated Idp until the federated domain is fully switched to cloud authentication.

### Should organizations eliminate federated servers like AD FS to prevent the capability to pivot from AD FS to Azure?

With federation, an attacker could impersonate anyone, such as a CIO, even if they can't obtain a cloud-only role like a highly privileged administrator account.

When a domain is federated in Microsoft Entra ID, a high level of trust is being placed on the Federated IdP. AD FS is one example, but the notion holds true for *any* federated IdP. Many organizations deploy a federated IdP such as AD FS exclusively to accomplish certificate based authentication. Microsoft Entra CBA completely removes the AD FS dependency in this case. With Microsoft Entra CBA, customers can move their application estate to Microsoft Entra ID to modernize their IAM infrastructure and reduce costs with increased security.

From a security perspective, there's no change to the credential, including the X.509 certificate, CACs, PIVs, and so on, or to the PKI being used. The PKI owners retain complete control of the certificate issuance and revocation lifecycle and policy. The revocation check and the authentication happen at Microsoft Entra ID instead of federated Idp. These checks enable passwordless, phishing-resistant authentication directly to Microsoft Entra ID for all users.

### How does authentication work with Federated AD FS and Microsoft Entra cloud authentication with Windows?

Microsoft Entra CBA requires the user or application to supply the Microsoft Entra UPN of the user who signs in.

In the browser example, the user most often types in their Microsoft Entra UPN. The Microsoft Entra UPN is used for realm and user discovery. The certificate used then must match this user by using one of the configured username bindings in the policy.

In Windows sign-in, the match depends on if the device is hybrid or Microsoft Entra joined. But in both cases, if username hint is provided, Windows sends the hint as a Microsoft Entra UPN. The certificate used then must match this user by using one of the configured username bindings in the policy.