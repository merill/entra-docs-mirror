---
layout: Conceptual
title: 'Conditional Access Templates: Simplify Security - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-policy-common
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how Conditional Access templates provide preconfigured policies to secure your environment, aligned with Microsoft recommendations.
ms.topic: concept-article
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
ms.custom:
- sfi-image-nochange
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:07/22/2025
- ai-gen-description
locale: en-us
document_id: 87abc0fe-0bab-9b07-07d2-660d778d7cdb
document_version_independent_id: c6d70b80-ba25-83b9-a25f-a695cbb8b88e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-conditional-access-policy-common.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-conditional-access-policy-common
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-conditional-access-policy-common.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: ccd35a07-3ec7-29e6-fe4e-2822158b5468
---

# Conditional Access Templates: Simplify Security - Microsoft Entra ID | Microsoft Learn

## Overview

Conditional Access templates provide a convenient method to deploy new policies aligned with Microsoft recommendations. These templates are designed to provide maximum protection aligned with commonly used policies across various customer types and locations.

[![Screenshot that shows Conditional Access policies and templates in the Microsoft Entra admin center.](media/concept-conditional-access-policy-common/conditional-access-policies-azure-ad-listing.png)](media/concept-conditional-access-policy-common/conditional-access-policies-azure-ad-listing.png#lightbox)

## Template categories

Conditional Access policy templates are organized into the following categories:

# [Secure foundation](#tab/secure-foundation)
Microsoft recommends these policies as the base for all organizations. Deploy these policies as a group.

- [Require multifactor authentication for admins](policy-old-require-mfa-admin)
- [Securing security info registration](policy-all-users-security-info-registration)
- [Block legacy authentication](policy-block-legacy-authentication)
- [Require multifactor authentication for admins accessing Microsoft admin portals](policy-old-require-mfa-admin-portals)
- [Require multifactor authentication for all users](policy-all-users-mfa-strength)
- [Require multifactor authentication for Azure management](policy-old-require-mfa-azure-mgmt)
- [Require compliant or Microsoft Entra hybrid joined device or multifactor authentication for all users](policy-alt-all-users-compliant-hybrid-or-mfa)
- [Require compliant device](policy-all-users-device-compliance)

# [Zero Trust](#tab/zero-trust)
These policies help support a [Zero Trust architecture](/en-us/security/zero-trust/deploy/identity).

- [Require multifactor authentication for admins](policy-old-require-mfa-admin)
- [Securing security info registration](policy-all-users-security-info-registration)
- [Block legacy authentication](policy-block-legacy-authentication)
- [Require multifactor authentication for all users](policy-all-users-mfa-strength)
- [Require multifactor authentication for guest access](policy-old-require-mfa-guest)
- [Require multifactor authentication for Azure management](policy-old-require-mfa-azure-mgmt)
- [Require multifactor authentication for risky sign-ins](policy-risk-based-sign-in)**Requires Microsoft Entra ID P2**
- [Require password change for high-risk users](policy-risk-based-user)**Requires Microsoft Entra ID P2**
- [Block access for unknown or unsupported device platform](policy-all-users-device-unknown-unsupported)
- [No persistent browser session](policy-all-users-persistent-browser)
- [Require approved client apps or app protection policies](policy-all-users-device-compliance)
- [Require compliant or Microsoft Entra hybrid joined device or multifactor authentication for all users](policy-alt-all-users-compliant-hybrid-or-mfa)
- [Require multifactor authentication for admins accessing Microsoft admin portals](policy-old-require-mfa-admin-portals)
- [Block access for users with insider risk](policy-risk-based-insider-block)**Requires Microsoft Purview**

# [Remote work](#tab/remote-work)
These policies help secure organizations with remote workers.

- [Securing security info registration](policy-all-users-security-info-registration)
- [Block legacy authentication](policy-block-legacy-authentication)
- [Require multifactor authentication for all users](policy-all-users-mfa-strength)
- [Require multifactor authentication for guest access](policy-old-require-mfa-guest)
- [Require multifactor authentication for risky sign-ins](policy-risk-based-sign-in)**Requires Microsoft Entra ID P2**
- [Require password change for high-risk users](policy-risk-based-user)**Requires Microsoft Entra ID P2**
- [Require compliant or Microsoft Entra hybrid joined device for administrators](policy-alt-admin-device-compliand-hybrid)
- [Block access for unknown or unsupported device platform](policy-all-users-device-unknown-unsupported)
- [No persistent browser session](policy-all-users-persistent-browser)
- [Require compliant device](policy-all-users-device-compliance)
- [Require approved client apps or app protection policies](policy-all-users-device-compliance)
- [Use application enforced restrictions for unmanaged devices](policy-all-users-app-enforced-restrictions)

# [Protect administrator](#tab/protect-administrator)
These policies are for highly privileged administrators in your environment, where compromise might cause the most damage.

- [Require multifactor authentication for admins](policy-old-require-mfa-admin)
- [Block legacy authentication](policy-block-legacy-authentication)
- [Require multifactor authentication for Azure management](policy-old-require-mfa-azure-mgmt)
- [Require compliant or Microsoft Entra hybrid joined device for administrators](policy-alt-admin-device-compliand-hybrid)
- [Require compliant device](policy-all-users-device-compliance)
- [Require phishing-resistant multifactor authentication for administrators](policy-admin-phish-resistant-mfa)

# [Emerging threats](#tab/emerging-threats)
Policies in this category provide new ways to protect against compromise.

- [Require phishing-resistant multifactor authentication for administrators](policy-admin-phish-resistant-mfa)

# [AI Agents](#tab/ai-agents)
Policies in this category provide ways to control agents in your environment.

- [Block high-risk agent identities](policy-agent-block-high-risk)
- [Configure policy for autonomous agent access](policy-autonomous-agents)
- [Configure policy for on-behalf-of agent access](policy-on-behalf-of-agents)

---

Find these templates in the [Microsoft Entra admin center](https://entra.microsoft.com) &gt; **Entra ID** &gt; **Conditional Access** &gt; **Create new policy from templates**. Select **Show more** to view all policy templates in each category.

[![Screenshot that shows how to create a Conditional Access policy from a preconfigured template in the Microsoft Entra admin center.](media/concept-conditional-access-policy-common/create-policy-from-template-identity.png)](media/concept-conditional-access-policy-common/create-policy-from-template-identity.png#lightbox)

Important

Conditional Access template policies targeting users exclude only the user creating the policy from the template. If your organization needs to [exclude other accounts](../role-based-access-control/security-emergency-access), modify the policy after it's created. You can find these policies in the [Microsoft Entra admin center](https://entra.microsoft.com) &gt; **Entra ID** &gt; **Conditional Access** &gt; **Policies**. Select a policy to open the editor and modify the excluded users and groups to select accounts you want to exclude.

By default, each policy is created in [report-only mode](concept-conditional-access-report-only). Test and monitor usage to ensure the intended result before turning on each policy.

Organizations can select individual policy templates and:

- View a summary of the policy settings.
- Edit, to customize based on organizational needs.
- Export the JSON definition for use in programmatic workflows.
    - These JSON definitions can be edited and then imported on the main Conditional Access policies page using the **Upload policy file** option.

## Other common policies

- [Require multifactor authentication for device registration](policy-all-users-device-registration)
- [Block access by location](policy-block-by-location)
- [Block access except specific apps](policy-block-example)

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Migrate from classic policies

Classic Conditional Access policies are deprecated and stopped enforcing controls after July 10, 2024. They depend on the retired Azure AD Graph service and can't protect your resources. If your tenant still has classic policies, migrate their settings to modern Conditional Access policies.

Warning

After you disable a classic policy, you can't re-enable it. Document the policy's settings before you disable it.

To migrate a classic policy:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Classic policies**.
3. Select a classic policy and document its configuration settings.
4. Recreate the settings by using a template or custom policy described earlier in this article. Test the new policy in [report-only mode](concept-conditional-access-report-only) before you turn it on.
5. Return to the classic policy and select **Disable**.

The [What If tool](what-if-tool) indicates whether classic policies still exist in your environment.