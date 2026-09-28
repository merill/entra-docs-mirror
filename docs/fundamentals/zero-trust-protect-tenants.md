---
layout: Conceptual
title: Security guidance - Protect tenants and isolate production systems - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/zero-trust-protect-tenants
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: pmwongera
description: Improve your security posture with the Microsoft Entra Zero Trust assessment to protect tenants and isolate production systems.
ms.topic: concept-article
ms.date: 2025-09-11T00:00:00.0000000Z
ms.reviewer: ramical
locale: en-us
document_id: 46b60345-f79e-9619-309d-5a400467d24e
document_version_independent_id: 46b60345-f79e-9619-309d-5a400467d24e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/zero-trust-protect-tenants.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/zero-trust-protect-tenants
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/zero-trust-protect-tenants.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: bc2c7099-c877-65b6-3883-07834b5ba5ff
---

# Security guidance - Protect tenants and isolate production systems - Microsoft Entra | Microsoft Learn

Protecting your tenant and isolating production systems is about setting tenant boundaries and keeping your production systems isolated from test and pre-production environments. Lateral movement was a critical concern from the [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars).

Even smaller organizations can protect their environments by implementing stricter guest access policies and limiting who can create tenants. Larger organizations that manage several environments should take action to prevent unauthorized tenant sprawl and lateral movement. All organizations can benefit from these checks to reduce attack surface area through unmanaged tenants.

## Zero Trust security recommendations

### Permissions to create new tenants are limited to the Tenant Creator role

A threat actor or a well-intentioned but uninformed employee can create a new Microsoft Entra tenant if there are no restrictions in place. By default, the user who creates a tenant is automatically assigned the Global Administrator role. Without proper controls, this action fractures the identity perimeter by creating a tenant outside the organization's governance and visibility. It introduces risk though a shadow identity platform that can be exploited for token issuance, brand impersonation, consent phishing, or persistent staging infrastructure. Since the rogue tenant might not be tethered to the enterprise’s administrative or monitoring planes, traditional defenses are blind to its creation, activity, and potential misuse.

**Remediation action**

Enable the **Restrict non-admin users from creating tenants** setting. For users that need the ability to create tenants, assign them the Tenant Creator role. You can also review tenant creation events in the Microsoft Entra audit logs.

- [Restrict member users' default permissions](/en-us/entra/fundamentals/users-default-permissions#restrict-member-users-default-permissions)
- [Assign the Tenant Creator role](/en-us/entra/identity/role-based-access-control/permissions-reference#tenant-creator)
- [Review tenant creation events](/en-us/entra/identity/monitoring-health/reference-audit-activities#core-directory). Look for OperationName=="Create Company", Category == "DirectoryManagement".

### Protected actions are enabled for high-impact management tasks

Threat actors who gain privileged access to a tenant can manipulate identity, access, and security configurations. This type of attack can result in environment-wide compromise and loss of control over organizational assets. Take action to protect high-impact management tasks associated with Conditional Access policies, cross-tenant access settings, hard deletions, and network locations that are critical to maintaining security.

Protected actions let administrators secure these tasks with extra security controls, such as stronger authentication methods (passwordless MFA or phishing-resistant MFA), the use of Privileged Access Workstation (PAW) devices, or shorter session timeouts.

**Remediation action**

- [Add, test, or remove protected actions in Microsoft Entra ID](/en-us/entra/identity/role-based-access-control/protected-actions-add)

### Enable protected actions to secure Conditional Access policy creation and changes

Threat actors who gain privileged access to a tenant can manipulate Conditional Access policies, potentially disabling critical security controls and enabling persistent access or lateral movement. This type of attack can result in environment-wide compromise by bypassing authentication and authorization barriers.

Protected actions let administrators secure Conditional Access policy creation and modification with extra security controls, such as stronger authentication methods (passwordless MFA or phishing-resistant MFA), the use of Privileged Access Workstation (PAW) devices, or shorter session timeouts.

**Remediation action**

- [Add, test, or remove protected actions in Microsoft Entra ID](/en-us/entra/identity/role-based-access-control/protected-actions-add)

### Guest access is limited to approved tenants

Limiting guest access to a known and approved list of tenants helps to prevent threat actors from exploiting unrestricted guest access to establish initial access through compromised external accounts or by creating accounts in untrusted tenants. Threat actors who gain access through an unrestricted domain can discover internal resources, users, and applications to perform additional attacks.

Organizations should take inventory and configure an allowlist or blocklist to control B2B collaboration invitations from specific organizations. Without these controls, threat actors might use social engineering techniques to obtain invitations from legitimate internal users.

**Remediation action**

- Learn how to [set up a list of approved domains](/en-us/entra/external-id/allow-deny-list#add-an-allowlist).

### Guests are not assigned high privileged directory roles

When guest users are assigned highly privileged directory roles such as Global Administrator or Privileged Role Administrator, organizations create significant security vulnerabilities that threat actors can exploit for initial access through compromised external accounts or business partner environments. Since guest users originate from external organizations without direct control of security policies, threat actors who compromise these external identities can gain privileged access to the target organization's Microsoft Entra tenant.

When threat actors obtain access through compromised guest accounts with elevated privileges, they can escalate their own privilege to create other backdoor accounts, modify security policies, or assign themselves permanent roles within the organization. The compromised privileged guest accounts enable threat actors to establish persistence and then make all the changes they need to remain undetected. For example they could create cloud-only accounts, bypass Conditional Access policies applied to internal users, and maintain access even after the guest's home organization detects the compromise. Threat actors can then conduct lateral movement using administrative privileges to access sensitive resources, modify audit settings, or disable security monitoring across the entire tenant. Threat actors can reach complete compromise of the organization's identity infrastructure while maintaining plausible deniability through the external guest account origin.

**Remediation action**

- [Remove Guest users from privileged roles](/en-us/entra/identity/role-based-access-control/best-practices)

### Guests can't invite other guests

External user accounts are often used to provide access to business partners who belong to organizations that have a business relationship with your enterprise. If these accounts are compromised in their organization, attackers can use the valid credentials to gain initial access to your environment, often bypassing traditional defenses due to their legitimacy.

Allowing external users to onboard other external users increases the risk of unauthorized access. If an attacker compromises an external user's account, they can use it to create more external accounts, multiplying their access points and making it harder to detect the intrusion.

**Remediation action**

- [Restrict who can invite guests to only users assigned to specific admin roles](/en-us/entra/external-id/external-collaboration-settings-configure#to-configure-guest-invite-settings)

### Guests have restricted access to directory objects

External user accounts are often used to provide access to business partners who belong to organizations that have a business relationship with your enterprise. If these accounts are compromised in their organization, attackers can use the valid credentials to gain initial access to your environment, often bypassing traditional defenses due to their legitimacy.

External accounts with permissions to read directory object permissions provide attackers with broader initial access if compromised. These accounts allow attackers to gather additional information from the directory for reconnaissance.

**Remediation action**

- [Restrict guest access to their own directory objects](/en-us/entra/external-id/external-collaboration-settings-configure#to-configure-guest-user-access)

### App instance property lock is configured for all multitenant applications

App instance property lock prevents changes to sensitive properties of a multitenant application after the application is provisioned in another tenant. Without a lock, critical properties such as application credentials can be maliciously or unintentionally modified, causing disruptions, increased risk, unauthorized access, or privilege escalations.

**Remediation action** Enable the app instance property lock for all multitenant applications and specify the properties to lock.

- [Configure an app instance lock](/en-us/entra/identity-platform/howto-configure-app-instance-property-locks#configure-an-app-instance-lock)

### Guests don't have long lived sign-in sessions

Guest accounts with extended sign-in sessions increase the risk surface area that threat actors can exploit. When guest sessions persist beyond necessary timeframes, threat actors often attempt to gain initial access through credential stuffing, password spraying, or social engineering attacks. Once they gain access, they can maintain unauthorized access for extended periods without reauthentication challenges. These compromised and extended sessions:

- Allow unauthorized access to Microsoft Entra artifacts, enabling threat actors to identify sensitive resources and map organizational structures.
- Allow threat actors to persist within the network by using legitimate authentication tokens, making detection more challenging as the activity appears as typical user behavior.
- Provides threat actors with a longer window of time to escalate privileges through techniques like accessing shared resources, discovering more credentials, or exploiting trust relationships between systems.

Without proper session controls, threat actors can achieve lateral movement across the organization's infrastructure, accessing critical data and systems that extend far beyond the original guest account's intended scope of access.

**Remediation action**

- [Configure adaptive session lifetime policies](/en-us/entra/identity/conditional-access/howto-conditional-access-session-lifetime) so sign-in frequency policies have shorter live sign-in sessions.

### Guest access is protected by strong authentication methods

External user accounts are often used to provide access to business partners who belong to organizations that have a business relationship with your organization. If these accounts are compromised in their organization, attackers can use the valid credentials to gain initial access to your environment, often bypassing traditional defenses due to their legitimacy.

Attackers might gain access with external user accounts, if multifactor authentication (MFA) isn't universally enforced or if there are exceptions in place. They might also gain access by exploiting the vulnerabilities of weaker MFA methods like SMS and phone calls using social engineering techniques, such as SIM swapping or phishing, to intercept the authentication codes.

Once an attacker gains access to an account without MFA or a session with weak MFA methods, they might attempt to manipulate MFA settings (for example, registering attacker controlled methods) to establish persistence to plan and execute further attacks based on the privileges of the compromised accounts.

**Remediation action**

- [Deploy a Conditional Access policy to enforce authentication strength for guests](/en-us/entra/identity/conditional-access/policy-guests-mfa-strength).
- For organizations with a closer business relationship and vetting on their MFA practices, consider deploying cross-tenant access settings to accept the MFA claim.
    - [Configure B2B collaboration cross-tenant access settings](/en-us/entra/external-id/cross-tenant-access-settings-b2b-collaboration#to-change-inbound-trust-settings-for-mfa-and-device-claims)

### Guest self-service sign-up via user flow is disabled

When guest self-service sign-up is enabled, threat actors can exploit it to establish unauthorized access by creating legitimate guest accounts without requiring approval from authorized personnel. These accounts can be scoped to specific services to reduce detection and effectively bypass invitation-based controls that validate external user legitimacy.

Once created, self-provisioned guest accounts provide persistent access to organizational resources and applications. Threat actors can use them to conduct reconnaissance activities to map internal systems, identify sensitive data repositories, and plan further attack vectors. This persistence allows adversaries to maintain access across restarts, credential changes, and other interruptions, while the guest account itself offers a seemingly legitimate identity that might evade security monitoring focused on external threats.

Additionally, compromised guest identities can be used to establish credential persistence and potentially escalate privileges. Attackers can exploit trust relationships between guest accounts and internal resources, or use the guest account as a staging ground for lateral movement toward more privileged organizational assets.

**Remediation action**

- [Configure guest self-service sign-up With Microsoft Entra External ID](/en-us/entra/external-id/external-collaboration-settings-configure#to-configure-guest-self-service-sign-up)

### Outbound cross-tenant access settings are configured

Allowing unrestricted external collaboration with unverified organizations can increase the risk surface area of the tenant because it allows guest accounts that might not have proper security controls. Threat actors can attempt to gain access by compromising identities in these loosely governed external tenants. Once granted guest access, they can then use legitimate collaboration pathways to infiltrate resources in your tenant and attempt to gain sensitive information. Threat actors can also exploit misconfigured permissions to escalate privileges and try different types of attacks.

Without vetting the security of organizations you collaborate with, malicious external accounts can persist undetected, exfiltrate confidential data, and inject malicious payloads. This type of exposure can weaken organizational control and enable cross-tenant attacks that bypass traditional perimeter defenses and undermine both data integrity and operational resilience. Cross-tenant settings for outbound access in Microsoft Entra provide the ability to block collaboration with unknown organizations by default, reducing the attack surface.

**Remediation action**

- [Cross-tenant access overview](/en-us/entra/external-id/cross-tenant-access-overview)
- [Configure cross-tenant access settings](/en-us/entra/external-id/cross-tenant-access-settings-b2b-collaboration#configure-default-settings)
- [Modify outbound access settings](/en-us/entra/external-id/cross-tenant-access-settings-b2b-collaboration)

### Guests don't own apps in the tenant

Without restrictions preventing guest users from registering and owning applications, threat actors can exploit external user accounts to establish persistent backdoor access to organizational resources through application registrations that might evade traditional security monitoring. When guest users own applications, compromised guest accounts can be used to exploit guest-owned applications that might have broad permissions. This vulnerability enables threat actors to request access to sensitive organizational data such as emails, files, and user information without the same level of scrutiny for internal user-owned applications.

This attack vector is dangerous because guest-owned applications can be configured to request high-privilege permissions and, once granted consent, provide threat actors with legitimate OAuth tokens. Furthermore, guest-owned applications can serve as command and control infrastructure, so threat actors can maintain access even after the compromised guest account is detected and remediated. Application credentials and permissions might persist independently of the original guest user account, so threat actors can retain access. Guest-owned applications also complicate security auditing and governance efforts, as organizations might have limited visibility into the purpose and security posture of applications registered by external users. These hidden weaknesses in the application lifecycle management make it difficult to assess the true scope of data access granted to non-Microsoft entities through seemingly legitimate application registrations.

**Remediation action**

- Remove guest users as owners from applications and service principals, and implement controls to prevent future guest user application ownership.
- [Restrict guest user access permissions](/en-us/entra/identity/users/users-restrict-guest-permissions)

### All guests have a sponsor

Inviting external guests is beneficial for organizational collaboration. However, in the absence of an assigned internal sponsor for each guest, these accounts might persist within the directory without clear accountability. This oversight creates a risk: threat actors could potentially compromise an unused or unmonitored guest account, and then establish an initial foothold within the tenant. Once granted access as an apparent "legitimate" user, an attacker might explore accessible resources and attempt privilege escalation, which could ultimately expose sensitive information or critical systems. An unmonitored guest account might therefore become the vector for unauthorized data access or a significant security breach. A typical attack sequence might use the following pattern, all achieved under the guise of a standard external collaborator:

1. Initial access gained through compromised guest credentials
2. Persistence due to a lack of oversight.
3. Further escalation or lateral movement if the guest account possesses group memberships or elevated permissions.
4. Execution of malicious objectives.

Mandating that every guest account is assigned to a sponsor directly mitigates this risk. Such a requirement ensures that each external user is linked to a responsible internal party who is expected to regularly monitor and attest to the guest's ongoing need for access. The sponsor feature within Microsoft Entra ID supports accountability by tracking the inviter and preventing the proliferation of "orphaned" guest accounts. When a sponsor manages the guest account lifecycle, such as removing access when collaboration concludes, the opportunity for threat actors to exploit neglected accounts is substantially reduced. This best practice is consistent with Microsoft’s guidance to require sponsorship for business guests as part of an effective guest access governance strategy. It strikes a balance between enabling collaboration and enforcing security, as it guarantees that each guest user's presence and permissions remain under ongoing internal oversight.

**Remediation action**

- For each guest user that has no sponsor, assign a sponsor in Microsoft Entra ID.
    - [Add a sponsor to a guest user in the Microsoft Entra admin center](/en-us/entra/external-id/b2b-sponsors)
    - [Add a sponsor to a guest user using Microsoft Graph](/en-us/graph/api/user-post-sponsors?view=graph-rest-1.0&amp;preserve-view=true)

### Inactive guest identities are disabled or removed from the tenant

When guest identities remain active but unused for extended periods, threat actors can exploit these dormant accounts as entry vectors into the organization. Inactive guest accounts represent a significant attack surface because they often maintain persistent access permissions to resources, applications, and data while remaining unmonitored by security teams. Threat actors frequently target these accounts through credential stuffing, password spraying, or by compromising the guest's home organization to gain lateral access. Once an inactive guest account is compromised, attackers can utilize existing access grants to:

- Move laterally within the tenant
- Escalate privileges through group memberships or application permissions
- Establish persistence through techniques like creating more service principals or modifying existing permissions

The prolonged dormancy of these accounts provides attackers with extended dwell time to conduct reconnaissance, exfiltrate sensitive data, and establish backdoors without detection, as organizations typically focus monitoring efforts on active internal users rather than external guest accounts.

**Remediation action**

- [Monitor and clean up stale guest accounts](/en-us/entra/identity/users/clean-up-stale-guest-accounts)

### All entitlement management policies have an expiration date

Entitlement management policies without expiration dates create persistent access that threat actors can exploit. When user assignments lack time bounds, compromised credentials maintain indefinite access, enabling attackers to establish persistence, escalate privileges through additional access packages, and conduct long-term malicious activities while remaining undetected.

**Remediation action**

- [Configure expiration settings for access packages](/en-us/entra/id-governance/entitlement-management-access-package-lifecycle-policy#specify-a-lifecycle)

### All entitlement management assignment policies that apply to external users require connected organizations

Access packages configured to allow "All users" instead of specific connected organizations expose your organization to uncontrolled external access. Threat actors can exploit this by requesting access through compromised external accounts from unauthorized organizations, bypassing the principle of least privilege. This enables initial access, reconnaissance, privilege escalation, and lateral movement within your environment.

**Remediation action**

- [Define trusted organizations as connected organizations](/en-us/entra/id-governance/entitlement-management-organization#view-the-list-of-connected-organizations)
- [Configure access packages to only allow specific connected organizations](/en-us/entra/id-governance/entitlement-management-access-package-create#allow-users-not-in-your-directory-to-request-the-access-package)

### All entitlement management assignment policies that apply to external users require approval

Access package assignment policies that allow external users to request access should require approval. Without an approval gate, external users can self-provision access to organizational resources without oversight. Requiring approval ensures that a designated approver reviews each request, providing an opportunity to validate the requestor's identity and business justification before granting access.

**Remediation action**

- [Configure approval for access package assignment policies](/en-us/entra/id-governance/entitlement-management-access-package-approval-policy)
- [Review access package policies for external users](/en-us/entra/id-governance/entitlement-management-access-package-request-policy)

### All entitlement management packages that apply to guests have expirations or access reviews configured in their assignment policies

Access packages for guest users without expiration dates or access reviews allow indefinite access to organizational resources. Compromised or stale guest accounts enable threat actors to maintain persistent, undetected access for lateral movement, privilege escalation, and data exfiltration. Without periodic validation, organizations cannot identify when business relationships change or when guest access is no longer needed.

**Remediation action**

- [Configure lifecycle settings](/en-us/entra/id-governance/entitlement-management-access-package-lifecycle-policy)
- [Configure access reviews](/en-us/entra/id-governance/entitlement-management-access-reviews-create)

### Manage the local administrators on Microsoft Entra joined devices

When local administrators on Microsoft Entra joined devices aren't properly managed, threat actors with compromised credentials can execute device takeover attacks by removing organizational administrators and disabling the device's connection to Microsoft Entra. This lack of control results in complete loss of organizational control, creating orphaned assets that can't be managed or recovered.

**Remediation action**

- [Manage the local administrators on Microsoft Entra joined devices](/en-us/entra/identity/devices/assign-local-admin#manage-the-microsoft-entra-joined-device-local-administrator-role)

### Restrict nonadministrator users from recovering the BitLocker keys for their owned devices

When non-administrator users can access their own BitLocker keys, threat actors who compromise user credentials can gain direct access to encryption keys without requiring privilege escalation. Once attackers obtain BitLocker keys, they can decrypt sensitive data stored on the device, including cached credentials, local databases, and confidential files.

Without proper restrictions, a single compromised user account provides immediate access to all encrypted data on that device, negating the primary security benefit of disk encryption and creating a pathway for lateral movement.

**Remediation action**

- [Restrict non-admin users from recovering the BitLocker key(s) for their owned devices](/en-us/entra/identity/devices/manage-device-identities#configure-device-settings)