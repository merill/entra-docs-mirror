---
layout: Conceptual
title: Enable Compliant Network Check with Conditional Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-compliant-network
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to require known compliant network locations to connect to your secured resources with Conditional Access.
ms.topic: how-to
ms.date: 2026-04-03T00:00:00.0000000Z
ms.reviewer: dhruvinrshah
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3704f909-64fc-7558-b9c9-0577bde73757
document_version_independent_id: 7d95c30a-86d2-395a-b673-6f971ab6b788
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-compliant-network.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-compliant-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-compliant-network.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 527ed885-052b-6844-76ce-d549a1bbbf5b
---

# Enable Compliant Network Check with Conditional Access - Global Secure Access | Microsoft Learn

Organizations that use Conditional Access along with Global Secure Access can prevent malicious access to Microsoft apps, third-party SaaS apps, and private line-of-business (LoB) apps by using multiple conditions to provide defense-in-depth. These conditions might include strong factor authentication, device compliance, location, and others. Enabling these conditions protects your organization against user identity compromise or token theft. Global Secure Access introduces the concept of a compliant network within Microsoft Entra ID Conditional Access. This compliant network check ensures users connect through the Global Secure Access service for their specific tenant and are compliant with security policies enforced by administrators.

By using the Global Secure Access client installed on devices or users behind configured remote networks, administrators can secure resources behind a compliant network by using advanced Conditional Access controls. This compliant network feature makes it easier for administrators to manage access policies without having to maintain a list of egress IP addresses. It also removes the requirement to hairpin traffic through your organization's VPN to maintain source IP anchoring and apply IP-based Conditional Access policies. For more information, see [What is Conditional Access?](../identity/conditional-access/overview)

## Compliant network check enforcement

Compliant network enforcement reduces the risk of token theft and replay attacks. Microsoft Entra ID performs authentication plane enforcement at the time of user authentication. If an adversary steals a session token and attempts to replay it from a device that isn't connected to your organization's compliant network (for example, by requesting an access token with a stolen refresh token), Microsoft Entra ID immediately denies the request and blocks further access. Data plane enforcement works with services integrated with Global Secure Access that support Continuous Access Evaluation (CAE), such as Microsoft Graph. By using apps that support CAE, stolen access tokens that are replayed outside your tenant's compliant network are rejected by the application in near-real time. Without CAE, a stolen access token remains valid for its full lifetime (default is between 60 and 90 minutes).

This compliant network check is specific to the tenant in which you configure it. For example, if you define a Conditional Access policy requiring compliant network in contoso.com, only users with Global Secure Access or with the Remote Network configuration can pass this control. A user from fabrikam.com can't pass contoso.com's compliant network policy.

The compliant network is different from [IPv4, IPv6, or geographic locations](../identity/conditional-access/concept-assignment-network) you might configure in Microsoft Entra. Administrators don't need to review and maintain compliant network IP addresses or ranges, which strengthens the security posture and minimizes the administrative overhead.

## Prerequisites

- Administrators who interact with **Global Secure Access**features must have one or more of the following role assignments depending on the tasks they're performing:
    - The [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference) role to manage the Global Secure Access features.
    - The [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role to enable Global Secure Access signaling for Conditional Access, and to create and interact with Conditional Access policies and named locations.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Enable Global Secure Access signaling for Conditional Access

To enable the setting that allows the compliant network check, an administrator must take the following steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with an account that has the [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) and [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) roles activated.
2. Browse to **Global Secure Access** &gt; **Settings** &gt; **Session management** &gt; **Adaptive access**.
3. Select the toggle to **Enable Conditional Access Signaling for Microsoft Entra ID**.

    [![Screenshot showing the toggle to enable Conditional Access Signaling for Microsoft Entra ID.](media/how-to-compliant-network/enable-conditional-access-signaling.png)](media/how-to-compliant-network/enable-conditional-access-signaling.png#lightbox)
4. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Named locations**.

    1. Confirm you have a location called **All Compliant Network locations** with location type **Network Access**. You can optionally mark this location as trusted.

Caution

If your organization has active Conditional Access policies based on compliant network check, and you later disable Global Secure Access signaling in Conditional Access, you might unintentionally block targeted end users from accessing the resources. If you must disable this feature, first delete any corresponding Conditional Access policies.

## Protect your resources behind the compliant network

Use the compliant network Conditional Access policy to protect your Microsoft and third-party applications that use Microsoft Entra ID single sign-on. A typical policy blocks all network locations except compliant networks. The following example shows how to configure this policy type:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **Create new policy**.
4. Enter a name for your policy. Create a meaningful standard for the names of your policies for your organization.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
    1. If your organization enrolls devices into Microsoft Intune, exclude the applications **Microsoft Intune Enrollment** and **Microsoft Intune** from your Conditional Access policy to avoid a circular dependency.
7. Under **Network**:
    1. Set **Configure** to **Yes**.
    2. Under **Include**, select **Any location**.
    3. Under **Exclude**, select the **All Compliant Network locations** location.
8. Under **Access controls**:
    1. **Grant**, select **Block Access**, and select **Select**.
9. Confirm your settings and set **Enable policy** to **On**.
10. Select **Create** to enable your policy.

Note

Use Global Secure Access along with Conditional Access policies that require a Compliant Network for *All Resources*.

Global Secure Access resources are automatically excluded from the Conditional Access policy when *Compliant Network* is enabled in the policy. There's no explicit resource exclusion required. These automatic exclusions are required to ensure the Global Secure Access client isn't blocked from accessing the resources it needs. The resources Global Secure Access needs are:

- Global Secure Access Traffic Profiles
- Global Secure Access Policy Service (internal service)

Sign-in events for authentication of excluded Global Secure Access resources appear in the Microsoft Entra ID sign-in logs as:

- Internet resources with Global Secure Access
- Microsoft apps with Global Secure Access
- All private resources with Global Secure Access
- ZTNA Policy Service

### Mobile app support

The Global Secure Access mobile app is part of the Defender app. You need to add exclusions to make sure the Defender client can access the resources it needs. To exclude Defender resources from Conditional Access policies, see [Microsoft Defender mobile app exclusion from Conditional Access policies](/en-us/defender-endpoint/mobile-resources-defender-endpoint#microsoft-defender-mobile-app-exclusion-from-conditional-access-ca-policies).

For more information, see [Mobile resources for Microsoft Defender for Endpoint](/en-us/defender-endpoint/mobile-resources-defender-endpoint).

### User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../identity/role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../identity/managed-identities-azure-resources/overview).

## Try your compliant network policy

1. On an end-user device with the [Global Secure Access client installed and running](how-to-install-windows-client), browse to https://myapps.microsoft.com or any other application that uses Microsoft Entra ID single sign-on in your tenant.
2. Pause the Global Secure Access client by right-clicking the application in the Windows tray and selecting **Disable**.
3. After disabling the Global Secure Access client, access another application integrated with Microsoft Entra ID single sign-on. For example, you can try signing in to the Azure portal. Microsoft Entra ID Conditional Access blocks your access.

Note

If you're already signed in to an application, access isn't interrupted. Microsoft Entra ID evaluates the Compliant Network condition. If you're already signed in, you might have an existing session with the application. In this scenario, Microsoft Entra ID reevaluates the Compliant Network check the next time sign-in is required, when your application session expires.

![Screenshot showing error message in browser window You can't access this right now.](media/how-to-compliant-network/you-cannot-access-this-right-now-error.png)