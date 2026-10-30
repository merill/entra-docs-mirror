---
layout: Conceptual
title: Security guidance - Protect engineering systems - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/zero-trust-protect-engineering-systems
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: pmwongera
description: Improve your security posture with the Microsoft Entra Zero Trust assessment to protect engineering systems.
ms.topic: concept-article
ms.date: 2025-09-11T00:00:00.0000000Z
ms.reviewer: ramical
locale: en-us
document_id: 3c5813da-b0d7-91bd-0998-68a688c70b69
document_version_independent_id: 3c5813da-b0d7-91bd-0998-68a688c70b69
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/zero-trust-protect-engineering-systems.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/zero-trust-protect-engineering-systems
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/zero-trust-protect-engineering-systems.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 8eef49a0-839f-40dc-4567-f8f2acca4896
---

# Security guidance - Protect engineering systems - Microsoft Entra | Microsoft Learn

The [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars) pillar for protecting engineering systems was first developed to safeguard Microsoft’s own software assets and infrastructure. The practices and insights gained from this internal work are now shared with customers, enabling you to strengthen your own environments.

These recommendations focus on ensuring least privilege access to your organization's engineering systems and resources.

## Security recommendations

### Emergency access accounts are configured appropriately

Microsoft recommends that organizations have two cloud-only emergency access accounts permanently assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. These accounts are highly privileged and aren't assigned to specific individuals. The accounts are limited to emergency or "break glass" scenarios where normal accounts can't be used or all other administrators are accidentally locked out.

**Remediation action**

- Create accounts following the [emergency access account recommendations](/en-us/entra/identity/role-based-access-control/security-emergency-access).

### Global Administrator role activation triggers an approval workflow

Without approval workflows, threat actors who compromise Global Administrator credentials through phishing, credential stuffing, or other authentication bypass techniques can immediately activate the most privileged role in a tenant without any other verification or oversight. Privileged Identity Management (PIM) allows eligible role activations to become active within seconds, so compromised credentials can allow near-instant privilege escalation. Once activated, threat actors can use the Global Administrator role to use the following attack paths to gain persistent access to the tenant:

- Create new privileged accounts
- Modify Conditional Access policies to exclude those new accounts
- Establish alternate authentication methods such as certificate-based authentication or application registrations with high privileges

The Global Administrator role provides access to administrative features in Microsoft Entra ID and services that use Microsoft Entra identities, including Microsoft Defender XDR, Microsoft Purview, Exchange Online, and SharePoint Online. Without approval gates, threat actors can rapidly escalate to complete tenant takeover, exfiltrating sensitive data, compromising all user accounts, and establishing long-term backdoors through service principals or federation modifications that persist even after the initial compromise is detected.

**Remediation action**

- [Configure role settings to require approval for Global Administrator activation](/en-us/entra/id-governance/privileged-identity-management/pim-how-to-change-default-settings)
- [Set up approval workflow for privileged roles](/en-us/entra/id-governance/privileged-identity-management/pim-approval-workflow)

### Global Administrators don't have standing access to Azure subscriptions

Global Administrators with persistent access to Azure subscriptions expand the attack surface for threat actors. If a Global Administrator account is compromised, attackers can immediately enumerate resources, modify configurations, assign roles, and exfiltrate sensitive data across all subscriptions. Requiring just-in-time elevation for subscription access introduces detectable signals, slows attacker velocity, and routes high-impact operations through observable control points.

**Remediation action**

- [Get started with a phishing-resistant passwordless authentication deployment](/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)
- [Ensure that privileged accounts register and use phishing resistant methods](/en-us/entra/identity/authentication/concept-authentication-strengths#authentication-strengths.md)
- [Deploy Conditional Access policy to target privileged accounts and require phishing resistant credentials using authentication strengths](/en-us/entra/identity/conditional-access/policy-admin-phish-resistant-mfa)
- [Monitor authentication method activity](/en-us/entra/identity/monitoring-health/concept-usage-insights-report#authentication-methods-activity.md)

### Creating new applications and service principals is restricted to privileged users

If nonprivileged users can create applications and service principals, these accounts might be misconfigured or be granted more permissions than necessary, creating new vectors for attackers to gain initial access. Attackers can exploit these accounts to establish valid credentials in the environment and bypass some security controls.

If these nonprivileged accounts are mistakenly granted elevated application owner permissions, attackers can use them to move from a lower level of access to a more privileged level of access. Attackers who compromise nonprivileged accounts might add their own credentials or change the permissions associated with the applications created by the nonprivileged users to ensure they can continue to access the environment undetected.

Attackers can use service principals to blend in with legitimate system processes and activities. Because service principals often perform automated tasks, malicious activities carried out under these accounts might not be flagged as suspicious.

**Remediation action**

- [Block nonprivileged users from creating apps](/en-us/entra/identity/role-based-access-control/delegate-app-roles)

### Inactive applications don't have highly privileged Microsoft Graph API permissions

Attackers might exploit valid but inactive applications that still have elevated privileges. These applications can be used to gain initial access without raising alarm because they’re legitimate applications. From there, attackers can use the application privileges to plan or execute other attacks. Attackers might also maintain access by manipulating the inactive application, such as by adding credentials. This persistence ensures that even if their primary access method is detected, they can regain access later.

**Remediation action**

- [Disable privileged service principals](/en-us/graph/api/serviceprincipal-update)
- Investigate if the application has legitimate use cases
- [If service principal doesn't have legitimate use cases, delete it](/en-us/graph/api/serviceprincipal-delete)

### Inactive applications don't have highly privileged built-in roles

Attackers might exploit valid but inactive applications that still have elevated privileges. These applications can be used to gain initial access without raising alarm because they're legitimate applications. From there, attackers can use the application privileges to plan or execute other attacks. Attackers might also maintain access by manipulating the inactive application, such as by adding credentials. This persistence ensures that even if their primary access method is detected, they can regain access later.

**Remediation action**

- [Disable inactive privileged service principals](/en-us/graph/api/serviceprincipal-update)
- Investigate if the application has legitimate use cases. If so, [analyze if a OAuth2 permission is a better fit](/en-us/entra/identity-platform/v2-app-types)
- [If service principal doesn't have legitimate use cases, delete it](/en-us/graph/api/serviceprincipal-delete)

### App registrations use safe redirect URIs

OAuth applications configured with URLs that include wildcards, or URL shorteners increase the attack surface for threat actors. Insecure redirect URIs (reply URLs) might allow adversaries to manipulate authentication requests, hijack authorization codes, and intercept tokens by directing users to attacker-controlled endpoints. Wildcard entries expand the risk by permitting unintended domains to process authentication responses, while shortener URLs might facilitate phishing and token theft in uncontrolled environments.

Without strict validation of redirect URIs, attackers can bypass security controls, impersonate legitimate applications, and escalate their privileges. This misconfiguration enables persistence, unauthorized access, and lateral movement, as adversaries exploit weak OAuth enforcement to infiltrate protected resources undetected.

**Remediation action**

- [Check the redirect URIs for your application registrations.](/en-us/entra/identity-platform/reply-url) Make sure the redirect URIs don't have \*.azurewebsites.net, wildcards, or URL shorteners.

### Service principals use safe redirect URIs

Non-Microsoft and multitenant applications configured with URLs that include wildcards, localhost, or URL shorteners increase the attack surface for threat actors. These insecure redirect URIs (reply URLs) might allow adversaries to manipulate authentication requests, hijack authorization codes, and intercept tokens by directing users to attacker-controlled endpoints. Wildcard entries expand the risk by permitting unintended domains to process authentication responses, while localhost and shortener URLs might facilitate phishing and token theft in uncontrolled environments.

Without strict validation of redirect URIs, attackers can bypass security controls, impersonate legitimate applications, and escalate their privileges. This misconfiguration enables persistence, unauthorized access, and lateral movement, as adversaries exploit weak OAuth enforcement to infiltrate protected resources undetected.

**Remediation action**

- [Check the redirect URIs for your application registrations.](/en-us/entra/identity-platform/reply-url) Make sure the redirect URIs don't have localhost, \*.azurewebsites.net, wildcards, or URL shorteners.

### App registrations must not have dangling or abandoned domain redirect URIs

Unmaintained or orphaned redirect URIs in app registrations create significant security vulnerabilities when they reference domains that no longer point to active resources. Threat actors can exploit these "dangling" DNS entries by provisioning resources at abandoned domains, effectively taking control of redirect endpoints. This vulnerability enables attackers to intercept authentication tokens and credentials during OAuth 2.0 flows, which can lead to unauthorized access, session hijacking, and potential broader organizational compromise.

**Remediation action**

- [Redirect URI (reply URL) outline and restrictions](/en-us/entra/identity-platform/reply-url)

### Resource-specific consent is restricted

If you let group owners consent to applications in Microsoft Entra ID, you create a lateral escalation path that bad actors can use to persist and steal data without admin credentials. If an attacker compromises a group owner account, they can register or use a malicious application and consent to high-privilege Graph API permissions scoped to the group. Attackers can potentially read all Teams messages, access SharePoint files, or manage group membership. This consent action creates a long-lived application identity with delegated or application permissions. The attacker maintains persistence with OAuth tokens, steals sensitive data from team channels and files, and impersonates users through messaging or email permissions. Without centralized enforcement of app consent policies, security teams lose visibility, and malicious applications spread under the radar, enabling multistage attacks across collaboration platforms.

**Remediation action**

Set your organization's Resource-Specific Consent (RSC) configuration to `EnabledForPreApprovedAppsOnly` and create preapproval policies for each app that requires RSC permissions. Don't use the default `ManagedByMicrosoft` state.

- [Enable RSC for a specific set of apps only](/en-us/microsoftteams/platform/graph-api/rsc/preapproval-instruction-docs#enable-rsc-for-a-specific-set-of-apps-only)

### Workload Identities are not assigned privileged roles

If administrators assign privileged roles to workload identities, such as service principals or managed identities, the tenant can be exposed to significant risk if those identities are compromised. Threat actors who gain access to a privileged workload identity can perform reconnaissance to enumerate resources, escalate privileges, and manipulate or exfiltrate sensitive data. The attack chain typically begins with credential theft or abuse of a vulnerable application. Next step is privilege escalation through the assigned role, lateral movement across cloud resources, and finally persistence via other role assignments or credential updates. Workload identities are often used in automation and might not be monitored as closely as user accounts. Compromise can then go undetected, allowing threat actors to maintain access and control over critical resources. Workload identities aren't subject to user-centric protections like MFA, making least-privilege assignment and regular review essential.

**Remediation action**

- [Review and remove privileged roles assignments](/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-assign-roles#update-or-remove-an-existing-role-assignment).
- [Follow the best practices for workload identities](/en-us/entra/workload-id/workload-identities-overview#key-scenarios).
- [Learn about privileged roles and permissions in Microsoft Entra ID](/en-us/entra/identity/role-based-access-control/privileged-roles-permissions)

### Enterprise applications must require explicit assignment or scoped provisioning

When enterprise applications lack both explicit assignment requirements AND scoped provisioning controls, threat actors can exploit this dual weakness to gain unauthorized access to sensitive applications and data. The highest risk occurs when applications are configured with the default setting: "Assignment required" is set to "No" *and* provisioning isn't required or scoped. This dangerous combination allows threat actors who compromise any user account within the tenant to immediately access applications with broad user bases, expanding their attack surface and potential for lateral movement within the organization.

While an application with open assignment but proper provisioning scoping (such as department-based filters or group membership requirements) maintains security controls through the provisioning layer, applications lacking both controls create unrestricted access pathways that threat actors can exploit. When applications provision accounts for all users without assignment restrictions, threat actors can abuse compromised accounts to conduct reconnaissance activities, enumerate sensitive data across multiple systems, or use the applications as staging points for further attacks against connected resources. This unrestricted access model is dangerous for applications that have elevated permissions or are connected to critical business systems. Threat actors can use any compromised user account to access sensitive information, modify data, or perform unauthorized actions that the application's permissions allow. The absence of both assignment controls and provisioning scoping also prevents organizations from implementing proper access governance. Without proper governance, it's difficult to track who has access to which applications, when access was granted, and whether access should be revoked based on role changes or employment status. Furthermore, applications with broad provisioning scopes can create cascading security risks where a single compromised account provides access to an entire ecosystem of connected applications and services.

**Remediation action**

- Evaluate business requirements to determine appropriate access control method. [Restrict a Microsoft Entra app to a set of users](/en-us/entra/identity-platform/howto-restrict-your-app-to-a-set-of-users).
- Configure enterprise applications to require assignment for sensitive applications. [Learn about the "Assignment required" enterprise application property](/en-us/entra/identity/enterprise-apps/application-properties#assignment-required).
- Implement scoped provisioning based on groups, departments, or attributes. [Create scoping filters](/en-us/entra/identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts#create-scoping-filters).

### Enterprise applications have owners

Enterprise applications without owners become orphaned assets that threat actors can exploit. These applications often retain elevated permissions and access to sensitive resources while lacking proper oversight and security governance.

Applications without owners create blind spots in security monitoring where attackers can establish persistence by leveraging existing application permissions to access data or create backdoor accounts. The absence of ownership also prevents proper access reviews and permission audits, allowing applications with excessive permissions or outdated configurations to remain unmanaged.

Assigning owners enables effective application lifecycle management and ensures proper security oversight.

**Remediation action**

- [Assign enterprise application owners](/en-us/entra/identity/enterprise-apps/assign-app-owners)

### Limit the maximum number of devices per user to 10

Controlling device proliferation is important. Set a reasonable limit on the number of devices each user can register in your Microsoft Entra ID tenant. Limiting device registration maintains security while allowing business flexibility. Microsoft Entra ID lets users register up to 50 devices by default. Reducing this number to 10 minimizes the attack surface and simplifies device management.

**Remediation action**

- Learn how to [limit the maximum number of devices per user](/en-us/entra/identity/devices/manage-device-identities#configure-device-settings).

### Conditional Access policies for Privileged Access Workstations are configured

If privileged role activations aren't restricted to dedicated Privileged Access Workstations (PAWs), threat actors can exploit compromised endpoint devices to perform privileged escalation attacks from unmanaged or noncompliant workstations. Standard productivity workstations often contain attack vectors such as unrestricted web browsing, email clients vulnerable to phishing, and locally installed applications with potential vulnerabilities. When administrators activated privileged roles from these workstations, threat actors who gain initial access through malware, browser exploits, or social engineering can then use the locally cached privileged credentials or hijack existing authenticated sessions to escalate their privileges. Privileged role activations grant extensive administrative rights across Microsoft Entra ID and connected services, so attackers can create new administrative accounts, modify security policies, access sensitive data across all organizational resources, and deploy malware or backdoors throughout the environment to establish persistent access. This lateral movement from a compromised endpoint to privileged cloud resources represents a critical attack path that bypasses many traditional security controls. The privileged access appears legitimate when originating from an authenticated administrator's session.

If this check passes, your tenant has a Conditional Access policy that restricts privileged role access to PAW devices, but it isn't the only control required to fully enable a PAW solution. You also need to configure an Intune device configuration and compliance policy and a device filter.

**Remediation action**

- [Deploy a privileged access workstation solution](/en-us/security/privileged-access-workstations/privileged-access-deployment)
    - Provides guidance for configuring the Conditional Access and Intune device configuration and compliance policies.
- [Configure device filters in Conditional Access to restrict privileged access](/en-us/entra/identity/conditional-access/concept-condition-filters-for-devices)