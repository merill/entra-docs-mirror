---
layout: Conceptual
title: Security guidance - Protect identities and secrets - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/zero-trust-protect-identities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: pmwongera
description: Improve your security posture with the Microsoft Entra Zero Trust assessment to protect identities and secrets.
ms.topic: concept-article
ms.date: 2025-09-11T00:00:00.0000000Z
ms.reviewer: ramical
locale: en-us
document_id: d02ac8ed-3634-31e6-a6c9-ab973e7c8a2a
document_version_independent_id: d02ac8ed-3634-31e6-a6c9-ab973e7c8a2a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/zero-trust-protect-identities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/zero-trust-protect-identities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/zero-trust-protect-identities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 6176d5cc-5892-065c-7540-8a2fb8c0d24a
---

# Security guidance - Protect identities and secrets - Microsoft Entra | Microsoft Learn

User and application authentication and authorization are the entry point into your identity and secrets infrastructure. Protecting all identities and secrets is a foundational step in your Zero Trust journey and a pillar of the [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars).

The recommendations and Zero Trust checks that are part of this pillar help reduce the risk of unauthorized access. Protecting identities and secrets represents the core of Zero Trust within Microsoft Entra. Themes include proper use of secrets and certificates, appropriate limits on privileged accounts, and modern passwordless authentication methods.

## Zero Trust security recommendations

### Applications don't have client secrets configured

Applications that use client secrets might store them in configuration files, hardcode them in scripts, or risk their exposure in other ways. The complexities of secret management make client secrets susceptible to leaks and attractive to attackers. Client secrets, when exposed, provide attackers with the ability to blend their activities with legitimate operations, making it easier to bypass security controls. If an attacker compromises an application's client secret, they can escalate their privileges within the system, leading to broader access and control, depending on the permissions of the application.

Applications and service principals that have permissions for Microsoft Graph APIs or other APIs have a higher risk because an attacker can potentially exploit these additional permissions.

**Remediation action**

- [Move applications away from shared secrets to managed identities and adopt more secure practices](/en-us/entra/identity/enterprise-apps/migrate-applications-from-secrets).
    - Use managed identities for Azure resources
    - Deploy Conditional Access policies for workload identities
    - Implement secret scanning
    - Deploy application authentication policies to enforce secure authentication practices
    - Create a least-privileged custom role to rotate application credentials
    - Ensure you have a process to triage and monitor applications

### Service principals don't have certificates or credentials associated with them

Service principals without proper authentication credentials (certificates or client secrets) create security vulnerabilities that allow threat actors to impersonate these identities. This can lead to unauthorized access, lateral movement within your environment, privilege escalation, and persistent access that's difficult to detect and remediate.

**Remediation action**

- For your organization's service principals: [Add certificates or client secrets to the app registration](/en-us/entra/identity-platform/how-to-add-credentials)
- For external service principals: Review and remove any unnecessary credentials to reduce security risk

### Applications don't have certificates with expiration longer than 180 days

Certificates, if not securely stored, can be extracted and exploited by attackers, leading to unauthorized access. Long-lived certificates are more likely to be exposed over time. Credentials, when exposed, provide attackers with the ability to blend their activities with legitimate operations, making it easier to bypass security controls. If an attacker compromises an application's certificate, they can escalate their privileges within the system, leading to broader access and control, depending on the privileges of the application.

**Remediation action**

- [Define certificate based application configuration](https://devblogs.microsoft.com/identity/app-management-policy/)
- [Define trusted certificate authorities for apps and service principals in the tenant](/en-us/graph/api/resources/certificatebasedapplicationconfiguration)
- [Define application management policies](/en-us/graph/api/resources/applicationauthenticationmethodpolicy)
- [Enforce secret and certificate standards](/en-us/entra/identity/enterprise-apps/tutorial-enforce-secret-standards)
- [Create a least-privileged custom role to rotate application credentials](/en-us/entra/identity/role-based-access-control/custom-create)

### Application certificates must be rotated on a regular basis

If certificates aren't rotated regularly, they can give threat actors an extended window to extract and exploit them, leading to unauthorized access. When credentials like these are exposed, attackers can blend their malicious activities with legitimate operations, making it easier to bypass security controls. If an attacker compromises an application’s certificate, they can escalate their privileges within the system, leading to broader access and control, depending on the application's privileges.

Query all of your service principals and application registrations that have certificate credentials. Make sure the certificate start date is less than 180 days.

**Remediation action**

- [Define an application management policy to manage certificate lifetimes](/en-us/graph/api/resources/applicationauthenticationmethodpolicy)
- [Define a trusted certificate chain of trust](/en-us/graph/api/resources/certificatebasedapplicationconfiguration)
- [Create a least privileged custom role to rotate application credentials](/en-us/entra/identity/role-based-access-control/custom-create)
- [Learn more about app management policies to manage certificate based credentials](https://devblogs.microsoft.com/identity/app-management-policy/)

### Enforce standards for app secrets and certificates

Without proper application management policies, threat actors can exploit weak or misconfigured application credentials to get unauthorized access to organizational resources. Applications using long-lived password secrets or certificates create extended attack windows where compromised credentials stay valid for extended periods. If an application uses client secrets that are hardcoded in configuration files or have weak password requirements, threat actors can extract these credentials through different means, including source code repositories, configuration dumps, or memory analysis. If threat actors get these credentials, they can perform lateral movement within the environment, escalate privileges if the application has elevated permissions, establish persistence by creating more backdoor credentials, modify application configuration, or exfiltrate data. The lack of credential lifecycle management lets compromised credentials remain active indefinitely, giving threat actors sustained access to organizational assets and the ability to conduct data exfiltration, system manipulation, or deploy more malicious tools without detection.

Configuring appropriate app management policies helps organizations stay ahead of these threats.

**Remediation action**

- [Learn how to enforce secret and certificate standards using application management policies](/en-us/entra/identity/enterprise-apps/tutorial-enforce-secret-standards)

### Microsoft services applications don't have credentials configured

Microsoft services applications that operate in your tenant are identified as service principals with the owner organization ID "f8cdef31-a31e-4b4a-93e4-5f571e91255a." When these service principals have credentials configured in your tenant, they might create potential attack vectors that threat actors can exploit. If an administrator added the credentials and they're no longer needed, they can become a target for attackers. Although less likely when proper preventive and detective controls are in place on privileged activities, threat actors can also maliciously add credentials. In either case, threat actors can use these credentials to authenticate as the service principal, gaining the same permissions and access rights as the Microsoft service application. This initial access can lead to privilege escalation if the application has high-level permissions, allowing lateral movement across the tenant. Attackers can then proceed to data exfiltration or persistence establishment through creating other backdoor credentials.

When credentials (like client secrets or certificates) are configured for these service principals in your tenant, it means someone - either an administrator or a malicious actor - enabled them to authenticate independently within your environment. These credentials should be investigated to determine their legitimacy and necessity. If they're no longer needed, they should be removed to reduce the risk.

If this check doesn't pass, the recommendation is to "investigate" because you need to identify and review any applications with unused credentials configured.

**Remediation action**

- Confirm if the credentials added are still valid use cases. If not, remove credentials from Microsoft service applications to reduce security risk.
    - In the Microsoft Entra admin center, browse to **Entra ID** &gt; **App registrations** and select the affected application.
    - Go to the **Certificates & secrets** section and remove any credentials that are no longer needed.

### User consent settings are restricted

Without restricted user consent settings, threat actors can exploit permissive application consent configurations to gain unauthorized access to sensitive organizational data. When user consent is unrestricted, attackers can:

- Use social engineering and illicit consent grant attacks to trick users into approving malicious applications.
- Impersonate legitimate services to request broad permissions, such as access to email, files, calendars, and other critical business data.
- Obtain legitimate OAuth tokens that bypass perimeter security controls, making access appear normal to security monitoring systems.
- Establish persistent access to organizational resources, conduct reconnaissance across Microsoft 365 services, move laterally through connected systems, and potentially escalate privileges.

Unrestricted user consent also limits an organization's ability to enforce centralized governance over application access, making it difficult to maintain visibility into which non-Microsoft applications have access to sensitive data. This gap creates compliance risks where unauthorized applications might violate data protection regulations or organizational security policies.

**Remediation action**

- [Configure restricted user consent settings](/en-us/entra/identity/enterprise-apps/configure-user-consent) to prevent illicit consent grants by disabling user consent or limiting it to verified publishers with low-risk permissions only.

### Admin consent workflow is enabled

Enabling the admin consent workflow in a Microsoft Entra tenant ensures that users who need access to an application that requires admin consent can submit a request for review rather than being blocked outright. Without the workflow, users who can't consent to an app on their own may resort to shadow IT workarounds, such as using personal accounts or unsanctioned alternatives—that are harder to monitor and secure. When the workflow is enabled, consent requests go through a logged, auditable process where designated reviewers are notified and evaluate each request before consent is granted. This improves observability into which applications users are requesting access to, and ensures that elevated permissions are reviewed and explicitly approved rather than silently blocked or granted without oversight.

**Remediation action**

For admin consent requests, set the **Users can request admin consent to apps they are unable to consent to** setting to **Yes**. Specify other settings, such as who can review requests.

- [Enable the admin consent workflow](/en-us/entra/identity/enterprise-apps/configure-admin-consent-workflow#enable-the-admin-consent-workflow)
- Or use the [Update adminConsentRequestPolicy](/en-us/graph/api/adminconsentrequestpolicy-update) API to set the `isEnabled` property to true and other settings

### High Global Administrator to privileged user ratio

When organizations maintain a disproportionately high ratio of Global Administrators relative to their total privileged user population, they expose themselves to significant security risks that threat actors might exploit through various attack vectors. Excessive Global Administrator assignments create multiple high-value targets for threat actors who might leverage initial access through credential compromise, phishing attacks, or insider threats to gain unrestricted access to the entire Microsoft Entra ID tenant and connected Microsoft 365 services.

**Remediation action**

- [Minimize the number of Global Administrator role assignments](/en-us/entra/identity/role-based-access-control/best-practices#5-limit-the-number-of-global-administrators-to-less-than-5)

### Administrative privileges are tightly limited to prevent compromise

Excessive assignment of roles like Global Administrator and Global Secure Access Administrator create a path for threat actors to compromise these identities. With these roles an attacker can authenticate, manipulate security policies, create or elevate accounts, disable monitoring, access all corporate data, and more. Limit access to these roles to a small set of administrators, and enable monitoring of assignments and activation for groups, guests, service principals, and disabled accounts to reduce the attack surface and enforce least privilege.

**Remediation action**

- [Emergency access accounts are configured appropriately](/en-us/entra/fundamentals/zero-trust-protect-engineering-systems#emergency-access-accounts-are-configured-appropriately)
- [Limit Global Administrator and Global Secure Access Administrator role assignments to a small set of administrators.](/en-us/entra/fundamentals/zero-trust-protect-identities#high-global-administrator-to-privileged-user-ratio)
- [Configure role settings to require approval for Global Administrator activation](/en-us/entra/id-governance/privileged-identity-management/pim-how-to-change-default-settings)

### Application admin rights are constrained to specific Private Access apps

An Application Administrator role scoped at the tenant level can manage every app registration and enterprise application. If a threat actor compromises an Application Administrator with tenant-wide scope, they can add credentials to any service principal, consent to malicious APIs, modify or create applications that enable data exfiltration, and disable or tamper with Private Access apps. Scoping the role to only required Private Access enterprise apps enforces least privilege and limits the blast radius.

If you don't scope Application Administrator assignments to specific apps:

- A compromised Application Administrator can manage every app registration and enterprise application in your tenant.
- Threat actors can add credentials to any service principal, enabling persistence and lateral movement.
- There's no blast radius containment; a single compromised identity can affect all applications.

**Remediation action**

- [Assign Application Administrator roles scoped to specific app registrations](/en-us/entra/identity/role-based-access-control/custom-enterprise-app-permissions) instead of tenant-wide.
- [Assign Microsoft Entra roles](/en-us/entra/identity/role-based-access-control/manage-roles-portal) with the least privilege necessary to perform required tasks.
- [Use Privileged Identity Management to manage just-in-time role activation](/en-us/entra/id-governance/privileged-identity-management/pim-configure).
- [Manage Microsoft Entra role assignments in the admin center](/en-us/entra/identity/role-based-access-control/manage-roles-portal).

### Privileged accounts are cloud native identities

If an on-premises account is compromised and is synchronized to Microsoft Entra, the attacker might gain access to the tenant as well. This risk increases because on-premises environments typically have more attack surfaces due to older infrastructure and limited security controls. Attackers might also target the infrastructure and tools used to enable connectivity between on-premises environments and Microsoft Entra. These targets might include tools like Microsoft Entra Connect or Active Directory Federation Services, where they could impersonate or otherwise manipulate other on-premises user accounts.

If privileged cloud accounts are synchronized with on-premises accounts, an attacker who acquires credentials for on-premises can use those same credentials to access cloud resources and move laterally to the cloud environment.

**Remediation action**

- [Protecting Microsoft 365 from on-premises attacks](/en-us/entra/architecture/protect-m365-from-on-premises-attacks#specific-security-recommendations)

For each role with high privileges (assigned permanently or eligible through Microsoft Entra Privileged Identity Management), you should do the following actions:

- Review the users that have onPremisesImmutableId and onPremisesSyncEnabled set. See [Microsoft Graph API user resource type](/en-us/graph/api/resources/user).
- Create cloud-only user accounts for those individuals and remove their hybrid identity from privileged roles.

### All privileged role assignments are activated just in time and not permanently active

Threat actors target privileged accounts because they have access to the data and resources they want. This might include more access to your Microsoft Entra tenant, data in Microsoft SharePoint, or the ability to establish long-term persistence. Without a just-in-time (JIT) activation model, administrative privileges remain continuously exposed, providing attackers with an extended window to operate undetected. Just-in-time access mitigates risk by enforcing time-limited privilege activation with extra controls such as approvals, justification, and Conditional Access policy, ensuring that high-risk permissions are granted only when needed and for a limited duration. This restriction minimizes the attack surface, disrupts lateral movement, and forces adversaries to trigger actions that can be specially monitored and denied when not expected. Without just-in-time access, compromised admin accounts grant indefinite control, letting attackers disable security controls, erase logs, and maintain stealth, amplifying the impact of a compromise.

Use Microsoft Entra Privileged Identity Management (PIM) to provide time-bound just-in-time access to privileged role assignments. Use access reviews in Microsoft Entra ID Governance to regularly review privileged access to ensure continued need.

**Remediation action**

- [Start using Privileged Identity Management](/en-us/entra/id-governance/privileged-identity-management/pim-getting-started)
- [Create an access review of Azure resource and Microsoft Entra roles in PIM](/en-us/entra/id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review)

### All Microsoft Entra privileged role assignments are managed with PIM

Threat actors who compromise permanently assigned privileged accounts gain continuous access to high-impact directory operations. This extended access allows attackers to establish persistent backdoors, modify security configurations, and disable monitoring systems. Without time-limited access controls, compromised privileged accounts provide indefinite tenant control.

Requiring eligible role assignments to be activated just-in-time, reduces the attack surface and limits attacker dwell time.

**Remediation action**

- [Use Privileged Identity Management to manage privileged Microsoft Entra roles](/en-us/entra/id-governance/privileged-identity-management/pim-getting-started)

### Passkey authentication method enabled

When passkey authentication isn't enabled in Microsoft Entra ID, organizations rely on password-based authentication methods that are vulnerable to phishing, credential theft, and replay attacks. Attackers can use stolen passwords to gain initial access, bypass traditional multifactor authentication through Adversary-in-the-Middle (AiTM) attacks, and establish persistent access through token theft.

Passkeys provide phishing-resistant authentication using cryptographic proof that attackers can't phish, intercept, or replay. Enabling passkeys eliminates the foundational vulnerability that enables credential-based attack chains.

**Remediation action**

- Learn how to [enable the passkey authentication method](/en-us/entra/identity/authentication/how-to-enable-passkey-fido2#enable-passkey-fido2-authentication-method).
- Learn how to [plan a phishing-resistant passwordless authentication deployment](/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication).

### Security key attestation is enforced

When security key attestation isn't enforced, threat actors can exploit weak or compromised authentication hardware to establish persistent presence within organizational environments. Without attestation validation, malicious actors can register unauthorized or counterfeit FIDO2 security keys that bypass hardware-backed security controls, enabling them to perform credential stuffing attacks using fabricated authenticators that mimic legitimate security keys. This initial access lets threat actors escalate privileges by using the trusted nature of hardware authentication methods, then move laterally through the environment by registering more compromised security keys on high-privilege accounts. The lack of attestation enforcement creates a pathway for threat actors to establish command and control through persistent hardware-based authentication methods, ultimately leading to data exfiltration or system compromise while maintaining the appearance of legitimate hardware-secured authentication throughout the attack chain.

**Remediation action**

- [Enable attestation enforcement through the Authentication methods policy configuration](/en-us/entra/identity/authentication/how-to-enable-passkey-fido2#enable-passkey-fido2-authentication-method).
- [Configure approved list of security keys by Authenticator Attestation Globally Unique Identifier (AAGUID)](/en-us/entra/identity/authentication/concept-fido2-hardware-vendor).

### Privileged accounts have phishing-resistant methods registered

When passkey authentication isn't enabled in Microsoft Entra ID, organizations rely on password-based authentication methods that are vulnerable to phishing, credential theft, and replay attacks. Attackers can use stolen passwords to gain initial access, bypass traditional multifactor authentication through Adversary-in-the-Middle (AiTM) attacks, and establish persistent access through token theft.

Passkeys provide phishing-resistant authentication using cryptographic proof that attackers can't phish, intercept, or replay. Enabling passkeys eliminates the foundational vulnerability that enables credential-based attack chains.

**Remediation action**

- Learn how to [enable the passkey authentication method](/en-us/entra/identity/authentication/how-to-enable-passkey-fido2#enable-passkey-fido2-authentication-method).
- Learn how to [plan a phishing-resistant passwordless authentication deployment](/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication).

### Privileged Microsoft Entra built-in roles are targeted with Conditional Access policies to enforce phishing-resistant methods

Without phishing-resistant authentication methods, privileged users are more vulnerable to phishing attacks. These types of attacks trick users into revealing their credentials to grant unauthorized access to attackers. If non-phishing-resistant authentication methods are used, attackers might intercept credentials and tokens, through methods like adversary-in-the-middle attacks, undermining the security of the privileged account.

Once a privileged account or session is compromised due to weak authentication methods, attackers might manipulate the account to maintain long-term access, create other backdoors, or modify user permissions. Attackers can also use the compromised privileged account to escalate their access even further, potentially gaining control over more sensitive systems.

**Remediation action**

- [Get started with a phishing-resistant passwordless authentication deployment](/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)
- [Ensure that privileged accounts register and use phishing resistant methods](/en-us/entra/identity/authentication/concept-authentication-strengths#authentication-strengths)
- [Deploy a Conditional Access policy to target privileged accounts and require phishing resistant credentials](/en-us/entra/identity/conditional-access/policy-admin-phish-resistant-mfa)
- [Monitor authentication method activity](/en-us/entra/identity/monitoring-health/concept-usage-insights-report#authentication-methods-activity)

### Conditional Access policies enforce strong authentication for private apps

When Conditional Access policies don't protect Private Access applications by requiring strong authentication, threat actors can use phishing attacks, credential stuffing, or password spraying to get user credentials and sign in to private applications with just a compromised password.

Without strong authentication:

- Threat actors gain initial access to internal resources that should be protected by stronger controls.
- If multifactor authentication is missing or phishable methods like SMS or voice are used, adversary-in-the-middle attacks can happen where threat actors intercept authentication tokens and session cookies.
- Threat actors can move laterally from the initially compromised private application to other internal resources.

Microsoft recommends enforcing phishing-resistant authentication methods such as FIDO2 security keys, Windows Hello for Business, or certificate-based authentication for access to private applications, with multifactor authentication as the minimum acceptable baseline.

**Remediation action**

- [Configure Conditional Access policies to require phishing-resistant authentication](/en-us/entra/identity/conditional-access/policy-all-users-mfa-strength).

### Application Proxy applications require preauthentication to block anonymous access

Without Microsoft Entra preauthentication configured on Application Proxy applications, threat actors can directly reach the internal URL of published on-premises applications without first proving their identity. When you use passthrough authentication, Application Proxy forwards traffic without validating the requestor, and all authentication responsibility falls to the internal application.

If you don't configure preauthentication on Application Proxy applications:

- Threat actors can access internal application endpoints without identity verification, enabling reconnaissance and exploitation of backend vulnerabilities.
- Conditional Access policies can't be enforced, so you can't require multifactor authentication, evaluate sign-in risk, or apply location-based restrictions.
- You can't integrate with Microsoft Defender for Cloud Apps for real-time session monitoring and control.

**Remediation action**

- [Configure Microsoft Entra preauthentication for Application Proxy applications](/en-us/entra/identity/app-proxy/application-proxy-add-on-premises-application#add-an-on-premises-app-to-microsoft-entra-id) by changing the Pre-Authentication method from **Passthrough** to **Microsoft Entra ID**.
- [Use Microsoft Graph API to programmatically update Application Proxy settings](/en-us/graph/application-proxy-configure-api).

### Require password reset notifications for administrator roles

Configuring password reset notifications for administrator roles in Microsoft Entra ID enhances security by notifying privileged administrators when another administrator resets their password. This visibility helps detect unauthorized or suspicious activity that could indicate credential compromise or insider threats. Without these notifications, malicious actors could exploit elevated privileges to establish persistence, escalate access, or extract sensitive data. Proactive notifications support quick action, preserve privileged access integrity, and strengthen the overall security posture.

**Remediation action**

- [Notify all admins when other admins reset their passwords](/en-us/entra/identity/authentication/concept-sspr-howitworks#notify-all-admins-when-other-admins-reset-their-passwords)

### Block legacy authentication policy is configured

Legacy authentication protocols such as basic authentication for SMTP and IMAP don't support modern security features like multifactor authentication (MFA), which is crucial for protecting against unauthorized access. This lack of protection makes accounts using these protocols vulnerable to password-based attacks, and provides attackers with a means to gain initial access using stolen or guessed credentials.

When an attacker successfully gains unauthorized access to credentials, they can use them to access linked services, using the weak authentication method as an entry point. Attackers who gain access through legacy authentication might make changes to Microsoft Exchange, such as configuring mail forwarding rules or changing other settings, allowing them to maintain continued access to sensitive communications.

Legacy authentication also provides attackers with a consistent method to reenter a system using compromised credentials without triggering security alerts or requiring reauthentication.

From there, attackers can use legacy protocols to access other systems that are accessible via the compromised account, facilitating lateral movement. Attackers using legacy protocols can blend in with legitimate user activities, making it difficult for security teams to distinguish between normal usage and malicious behavior.

**Remediation action**

- [Deploy a Conditional Access policy to Block legacy authentication](/en-us/entra/identity/conditional-access/policy-block-legacy-authentication)

### Temporary access pass is enabled

Without Temporary Access Pass (TAP) enabled, organizations face significant challenges in securely bootstrapping user credentials, creating a vulnerability where users rely on weaker authentication mechanisms during their initial setup. When users cannot register phishing-resistant credentials like FIDO2 security keys or Windows Hello for Business due to lack of existing strong authentication methods, they remain exposed to credential-based attacks including phishing, password spray, or similar attacks. Threat actors can exploit this registration gap by targeting users during their most vulnerable state, when they have limited authentication options available and must rely on traditional username + password combinations. This exposure enables threat actors to compromise user accounts during the critical bootstrapping phase, allowing them to intercept or manipulate the registration process for stronger authentication methods, ultimately gaining persistent access to organizational resources and potentially escalating privileges before security controls are fully established.

Enable TAP and use it with security info registration to secure this potential gap in your defenses.

**Remediation action**

- [Learn how to enable Temporary Access Pass in the Authentication methods policy](/en-us/entra/identity/authentication/howto-authentication-temporary-access-pass#enable-the-temporary-access-pass-policy)
- [Learn how to update authentication strength policies to include Temporary Access Pass](/en-us/entra/identity/authentication/concept-authentication-strength-advanced-options)
- [Learn how to create a Conditional Access policy for security info registration with authentication strength enforcement](/en-us/entra/identity/conditional-access/policy-all-users-security-info-registration)

### Restrict Temporary Access Pass to Single Use

When Temporary Access Pass (TAP) is configured to allow multiple uses, threat actors who compromise the credential can reuse it repeatedly during its validity period, extending their unauthorized access window beyond the intended single bootstrapping event. This situation creates an extended opportunity for threat actors to establish persistence by registering additional strong authentication methods under the compromised account during the credential lifetime. A reusable TAP that falls into the wrong hands lets threat actors conduct reconnaissance activities across multiple sessions, gradually mapping the environment and identifying high-value targets while maintaining legitimate-looking access patterns. The compromised TAP can also serve as a reliable backdoor mechanism, allowing threat actors to maintain access even if other compromised credentials are detected and revoked, since the TAP appears as a legitimate administrative tool in security logs.

**Remediation action**

- [Configure Temporary Access Pass for one-time use in authentication methods policy](/en-us/entra/identity/authentication/howto-authentication-temporary-access-pass#enable-the-temporary-access-pass-policy)

### Migrate from legacy MFA and SSPR policies

Legacy multifactor authentication (MFA) and self-service password reset (SSPR) policies in Microsoft Entra ID manage authentication methods separately, leading to fragmented configurations and suboptimal user experience. Moreover, managing these policies independently increases administrative overhead and the risk of misconfiguration.

Migrating to the combined Authentication Methods policy consolidates the management of MFA, SSPR, and passwordless authentication methods into a single policy framework. This unification allows for more granular control, enabling administrators to target specific authentication methods to user groups and enforce consistent security measures across the organization. Additionally, the unified policy supports modern authentication methods, such as FIDO2 security keys and Windows Hello for Business, enhancing the organization's security posture.

Microsoft announced the deprecation of legacy MFA and SSPR policies, with a retirement date set for September 30, 2025. Organizations are advised to complete the migration to the Authentication Methods policy before this date to avoid potential disruptions and to benefit from the enhanced security and management capabilities of the unified policy.

**Remediation action**

- [Enable combined security information registration](/en-us/entra/identity/authentication/howto-registration-mfa-sspr-combined)
- [How to migrate MFA and SSPR policy settings to the Authentication methods policy for Microsoft Entra ID](/en-us/entra/identity/authentication/how-to-authentication-methods-manage)

### Block administrators from using SSPR

Self-Service Password Reset (SSPR) for administrators allows password changes to happen without strong secondary authentication factors or administrative oversight. Threat actors who compromise administrative credentials can use this capability to bypass other security controls and maintain persistent access to the environment.

Once compromised, attackers can immediately reset the password to lock out legitimate administrators. They can then establish persistence, escalate privileges, and deploy malicious payloads undetected.

**Remediation action**

- [Disable SSPR for administrators by updating the authorization policy](/en-us/entra/identity/authentication/concept-sspr-policy#administrator-reset-policy-differences)

### Self-service password reset doesn't use security questions

Allowing security questions as a self-service password reset (SSPR) method weakens the password reset process because answers are frequently guessable, reused across sites, or discoverable through open-source intelligence (OSINT). Threat actors enumerate or phish users, derive likely responses (family names, schools, and locations), and then trigger password reset flows to bypass stronger methods by exploiting the weaker knowledge-based gate. After they successfully reset a password on an account that isn't protected by multifactor authentication they can: gain valid primary credentials, establish session tokens, and laterally expand by registering more durable authentication methods, add forwarding rules, or exfiltrate sensitive data.

Eliminating this method removes a weak link in the password reset process. Some organizations might have specific business reasons for leaving security questions enabled, but this isn't recommended.

**Remediation action**

- [Disable security questions in SSPR policy](/en-us/entra/identity/authentication/concept-authentication-security-questions)
- [Select authentication methods and registration options](/en-us/entra/identity/authentication/tutorial-enable-sspr#select-authentication-methods-and-registration-options)

### SMS and Voice Call authentication methods are disabled

When weak authentication methods like SMS and voice calls remain enabled in Microsoft Entra ID, threat actors can exploit these vulnerabilities through multiple attack vectors. Initially, attackers often conduct reconnaissance to identify organizations using these weaker authentication methods through social engineering or technical scanning. Then they can execute initial access through credential stuffing attacks, password spraying, or phishing campaigns targeting user credentials.

Once basic credentials are compromised, threat actors use these weaknesses in SMS and voice-based authentication. SMS messages can be intercepted through SIM swapping attacks, SS7 network vulnerabilities, or malware on mobile devices, while voice calls are susceptible to voice phishing (vishing) and call forwarding manipulation. With these weak second factors bypassed, attackers achieve persistence by registering their own authentication methods. Compromised accounts can be used to target higher-privileged users through internal phishing or social engineering, allowing attackers to escalate privileges within the organization. Finally, threat actors achieve their objectives through data exfiltration, lateral movement to critical systems, or deployment of other malicious tools, all while maintaining stealth by using legitimate authentication pathways that appear normal in security logs.

**Remediation action**

- [Deploy authentication method registration campaigns to encourage stronger methods](/en-us/graph/api/authenticationmethodspolicy-update?view=graph-rest-beta&amp;preserve-view=true)
- [Disable authentication methods](/en-us/entra/identity/authentication/concept-authentication-methods-manage)
- [Disable phone-based methods in legacy MFA settings](/en-us/entra/identity/authentication/howto-mfa-mfasettings)
- [Deploy Conditional Access policies using authentication strength](/en-us/entra/identity/authentication/concept-authentication-strength-how-it-works)

### Turn off Seamless SSO if there is no usage

Microsoft Entra seamless single sign-on (Seamless SSO) is a legacy authentication feature designed to provide passwordless access for domain-joined devices that are not hybrid Microsoft Entra ID joined. Seamless SSO relies on Kerberos authentication and is primarily beneficial for older operating systems like Windows 7 and Windows 8.1, which do not support Primary Refresh Tokens (PRT). If these legacy systems are no longer present in the environment, continuing to use Seamless SSO introduces unnecessary complexity and potential security exposure. Threat actors could exploit misconfigured or stale Kerberos tickets, or compromise the `AZUREADSSOACC` computer account in Active Directory, which holds the Kerberos decryption key used by Microsoft Entra ID. Once compromised, attackers could impersonate users, bypass modern authentication controls, and gain unauthorized access to cloud resources. Disabling Seamless SSO in environments where it is no longer needed reduces the attack surface and enforces the use of modern, token-based authentication mechanisms that offer stronger protections.

**Remediation action**

- [Review how Seamless SSO works](/en-us/entra/identity/hybrid/connect/how-to-connect-sso-how-it-works)
- [Disable Seamless SSO](/en-us/entra/identity/hybrid/connect/how-to-connect-sso-faq#how-can-i-disable-seamless-sso-)
- [Clean up stale devices in Microsoft Entra ID](/en-us/entra/identity/devices/manage-stale-devices)

### Secure the MFA registration (My Security Info) page

Without Conditional Access policies protecting security information registration, threat actors can exploit unprotected registration flows to compromise authentication methods. When users register multifactor authentication and self-service password reset methods without proper controls, threat actors can intercept these registration sessions through adversary-in-the-middle attacks or exploit unmanaged devices accessing registration from untrusted locations. Once threat actors gain access to an unprotected registration flow, they can register their own authentication methods, effectively hijacking the target's authentication profile. The threat actors can bypass security controls and potentially escalate privileges throughout the environment because they can maintain persistent access by controlling the MFA methods. The compromised authentication methods then become the foundation for lateral movement as threat actors can authenticate as the legitimate user across multiple services and applications.

**Remediation action**

- [Deploy a Conditional Access policy for security info registration](/en-us/entra/identity/conditional-access/policy-all-users-security-info-registration)
- [Configure known network locations](/en-us/entra/identity/conditional-access/concept-assignment-network)
- [Enable combined security info registration](/en-us/entra/identity/authentication/howto-registration-mfa-sspr-combined)

### Use cloud authentication

An on-premises federation server introduces a critical attack surface by serving as a central authentication point for cloud applications. Threat actors often gain a foothold by compromising a privileged user such as a help desk representative or an operations engineer through attacks like phishing, credential stuffing, or exploiting weak passwords. They might also target unpatched vulnerabilities in infrastructure, use remote code execution exploits, attack the Kerberos protocol, or use pass-the-hash attacks to escalate privileges. Misconfigured remote access tools like remote desktop protocol (RDP), virtual private network (VPN), or jump servers provide other entry points, while supply chain compromises or malicious insiders further increase exposure. Once inside, threat actors can manipulate authentication flows, forge security tokens to impersonate any user, and pivot into cloud environments. Establishing persistence, they can disable security logs, evade detection, and exfiltrate sensitive data.

**Remediation action**

- [Migrate from federation to cloud authentication like Microsoft Entra Password hash synchronization (PHS)](/en-us/entra/identity/hybrid/connect/migrate-from-federation-to-cloud-authentication).

### All users are required to register for MFA

Require multifactor authentication (MFA) registration for all users. Based on studies, your account is more than 99% less likely to be compromised if you're using MFA. Even if you don't require MFA all the time, this policy ensures your users are ready when it's needed.

**Remediation action**

- [Configure the multifactor authentication registration policy](/en-us/entra/id-protection/howto-identity-protection-configure-mfa-policy)

### Users have strong authentication methods configured

Attackers might gain access if multifactor authentication (MFA) isn't universally enforced or if there are exceptions in place. Attackers might gain access by exploiting vulnerabilities of weaker MFA methods like SMS and phone calls through social engineering techniques. These techniques might include SIM swapping or phishing, to intercept authentication codes.

Attackers might use these accounts as entry points into the tenant. By using intercepted user sessions, attackers can disguise their activities as legitimate user actions, evade detection, and continue their attack without raising suspicion. From there, they might attempt to manipulate MFA settings to establish persistence, plan, and execute further attacks based on the privileges of compromised accounts.

**Remediation action**

- [Deploy multifactor authentication](/en-us/entra/identity/authentication/howto-mfa-getstarted)
- [Get started with a phishing-resistant passwordless authentication deployment](/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)
- [Deploy a Conditional Access policy to require phishing-resistant MFA for all users](/en-us/entra/identity/conditional-access/policy-all-users-mfa-strength)
- [Review authentication methods activity](/en-us/entra/identity/monitoring-health/concept-usage-insights-report?tabs=microsoft-entra-admin-center#authentication-methods-activity)

### Reduce the user-visible password surface area

Organizations with extensive user-facing password surfaces expose multiple entry points for credential-based attacks. Threat actors often begin with credential stuffing using compromised credentials from data breaches, followed by password spraying to test common passwords across multiple accounts. Once initial access is gained, they conduct credential discovery by examining browser password stores, cached credentials in memory, and credential managers to harvest additional authentication materials. These stolen credentials enable lateral movement to more systems and applications, often escalating privileges by targeting administrative accounts that still rely on password authentication.

Without passwordless methods like Windows Hello for Business, FIDO2 security keys, and Microsoft Authenticator deployed broadly, every password prompt is an opportunity for interception and exploitation. Reducing the password surface area limits these attack vectors and reduces the overall exposure to credential-based threats.

**Remediation action**

- [Plan a phishing-resistant passwordless authentication deployment](/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication).
- [Enable passkeys (FIDO2)](/en-us/entra/identity/authentication/how-to-enable-passkey-fido2).
- [Configure Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/).

### User sign-in activity uses token protection

A threat actor can intercept or extract authentication tokens from memory, local storage on a legitimate device, or by inspecting network traffic. The attacker might replay those tokens to bypass authentication controls on users and devices, get unauthorized access to sensitive data, or run further attacks. Because these tokens are valid and time bound, traditional anomaly detection often fails to flag the activity, which might allow sustained access until the token expires or is revoked.

Token protection, also called token binding, helps prevent token theft by making sure a token is usable only from the intended device. Token protection uses cryptography so that without the client device key, no one can use the token.

**Remediation action**

- [Deploy a Conditional Access policy to require token protection](/en-us/entra/identity/conditional-access/concept-token-protection)

### Token protection policies are configured

Without the Token Protection Conditional Access policy, threat actors who steal sign-in session tokens can replay them from any device to gain unauthorized access to resources. Token theft allows attackers to bypass authentication entirely because the stolen token is already a valid proof of identity. This access vector enables lateral movement, privilege escalation, and data exfiltration without triggering reauthentication challenges.

Token protection in Microsoft Entra ID binds sign-in session tokens to the device where they were originally issued, rendering stolen tokens unusable on attacker-controlled devices. Configuring the Conditional Access Token Protection policy for Windows and Apple platforms ensures that sign-in session tokens for critical services like SharePoint Online and Exchange Online can't be replayed from unauthorized endpoints.

**Remediation action**

- [Configure token protection in Conditional Access](/en-us/entra/identity/conditional-access/concept-token-protection#create-a-conditional-access-policy).

### All user sign-in activity uses phishing-resistant authentication methods

Phishing-resistant authentication methods like passkeys and FIDO2 security keys provide the strongest protection against credential theft and sophisticated phishing attacks. Traditional MFA methods remain vulnerable to adversary-in-the-middle attacks and social engineering. Enforcing phishing-resistant methods for all users through Conditional Access policies helps prevent unauthorized access even when attackers attempt to intercept authentication flows.

**Remediation action**

- [Configure Conditional Access for all users with MFA strength](/en-us/entra/identity/conditional-access/policy-all-users-mfa-strength)
- [Deploy phishing-resistant passwordless authentication](/en-us/entra/identity/authentication/how-to-deploy-phishing-resistant-passwordless-authentication)

### All sign-in activity comes from managed devices

Requiring sign-ins from managed devices ensures that users access organizational resources only from devices that meet your security and compliance requirements. Unmanaged devices lack organizational security controls and endpoint protection, creating potential entry points for attackers. Using Conditional Access to require compliant or Microsoft Entra hybrid joined devices helps protect against credential theft and unauthorized access from untrusted endpoints.

**Remediation action**

- [Require compliant or hybrid joined devices with Conditional Access](/en-us/entra/identity/conditional-access/policy-all-users-device-compliance)
- [Configure device compliance policies in Microsoft Intune](/en-us/mem/intune/protect/device-compliance-get-started)

### Security key authentication method enabled

FIDO2 security keys provide hardware-backed, phishing-resistant authentication that protects against credential theft and unauthorized access. Security keys use cryptographic proof of identity bound to a specific device, making credentials impossible to replicate or phish. Enabling this authentication method allows users to register security keys for strong passwordless authentication.

**Remediation action**

- [Enable FIDO2 security key authentication method](/en-us/entra/identity/authentication/how-to-enable-passkey-fido2#enable-passkey-fido2-authentication-method)
- [Manage authentication methods](/en-us/entra/identity/authentication/concept-authentication-methods-manage)

### Privileged roles aren't assigned to stale identities

Privileged roles should not remain assigned to identities that show no recent sign-in activity. Stale accounts with administrative privileges are attractive targets for attackers because they can be compromised without triggering behavioral analytics alerts. Regularly reviewing and removing privileged role assignments from inactive identities reduces the risk of credential-based attacks and helps maintain least-privilege access.

**Remediation action**

- [Review privileged role assignments using access reviews](/en-us/entra/id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review)
- [Remove privileged role assignments from inactive identities](/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-assign-roles#update-or-remove-an-existing-role-assignment)
- [Configure automated access reviews for privileged roles](/en-us/entra/id-governance/access-reviews-overview)

### Restrict device code flow

Device code flow is a cross-device authentication flow designed for input-constrained devices. It can be exploited in phishing attacks, where an attacker initiates the flow and tricks a user into completing it on their device, thereby sending the user's tokens to the attacker. Given the security risks and the infrequent legitimate use of device code flow, you should enable a Conditional Access policy to block this flow by default.

**Remediation action**

- [Deploy a Conditional Access policy to block device code flow](/en-us/entra/identity/conditional-access/policy-block-authentication-flows#device-code-flow-policies).

### Authentication transfer is blocked

Blocking authentication transfer in Microsoft Entra ID is a critical security control. It helps protect against token theft and replay attacks by preventing the use of device tokens to silently authenticate on other devices or browsers. When authentication transfer is enabled, a threat actor who gains access to one device can access resources to nonapproved devices, bypassing standard authentication and device compliance checks. When administrators block this flow, organizations can ensure that each authentication request must originate from the original device, maintaining the integrity of the device compliance and user session context.

**Remediation action**

- [Deploy a Conditional Access policy to block authentication transfer](/en-us/entra/identity/conditional-access/policy-block-authentication-flows#authentication-transfer-policies)

### Microsoft Authenticator app shows sign-in context

Without sign-in context, threat actors can exploit authentication fatigue by flooding users with push notifications, increasing the chance that a user accidentally approves a malicious request. When users get generic push notifications without the application name or geographic location, they don't have the information they need to make informed approval decisions. This lack of context makes users vulnerable to social engineering attacks, especially when threat actors time their requests during periods of legitimate user activity. This vulnerability is especially dangerous when threat actors gain initial access through credential harvesting or password spraying attacks and then try to establish persistence by approving multifactor authentication (MFA) requests from unexpected applications or locations. Without contextual information, users can't detect unusual sign-in attempts, allowing threat actors to maintain access and escalate privileges by moving laterally through systems after bypassing the initial authentication barrier. Without application and location context, security teams also lose valuable telemetry for detecting suspicious authentication patterns that can indicate ongoing compromise or reconnaissance activities.

**Remediation action** Give users the context they need to make informed approval decisions. Configure Microsoft Authenticator notifications by setting the Authentication methods policy to include the application name and geographic location.

- [Use additional context in Authenticator notifications - Authentication methods policy](/en-us/entra/identity/authentication/how-to-mfa-additional-context)

### Microsoft Authenticator app report suspicious activity setting is enabled

Threat actors increasingly rely on prompt bombing and real-time phishing proxies to coerce or trick users into approving fraudulent multifactor authentication (MFA) challenges. Without the Microsoft Authenticator app's **Report suspicious activity** capability enabled, an attacker can iterate until a fatigued user accepts. This type of attack can lead to privilege escalation, persistence, lateral movement into sensitive workloads, data exfiltration, or destructive actions.

When reporting is enabled for all users, any unexpected push or phone prompt can be actively flagged, immediately elevating the user to high user risk and generating a high-fidelity user risk detection (userReportedSuspiciousActivity) that risk-based Conditional Access policies or other response automation can use to block or require secure remediation.

**Remediation action**

- [Enable the report suspicious activity setting in the Microsoft Authenticator app](/en-us/entra/identity/authentication/howto-mfa-mfasettings#report-suspicious-activity)

### Password expiration is disabled

When password expiration policies remain enabled, threat actors can exploit the predictable password rotation patterns that users typically follow when forced to change passwords regularly. Users frequently create weaker passwords by making minimal modifications to existing ones, such as incrementing numbers or adding sequential characters. Threat actors can easily anticipate and exploit these types of changes through credential stuffing attacks or targeted password spraying campaigns. These predictable patterns enable threat actors to establish persistence through:

- Compromised credentials
- Escalated privileges by targeting administrative accounts with weak rotated passwords
- Maintaining long-term access by predicting future password variations

Research shows that users create weaker, more predictable passwords when they are forced to expire. These predictable passwords are easier for experienced attackers to crack, as they often make simple modifications to existing passwords rather than creating entirely new, strong passwords. Additionally, when users are required to frequently change passwords, they might resort to insecure practices such as writing down passwords or storing them in easily accessible locations, creating more attack vectors for threat actors to exploit during physical reconnaissance or social engineering campaigns.

**Remediation action**

- [Set the password expiration policy for your organization](/en-us/microsoft-365/admin/manage/set-password-expiration-policy).
    - Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com/). Go to **Settings** &gt; **Org Settings** &gt;\*\* Security & Privacy\*\* &gt; **Password expiration policy**. Ensure the **Set passwords to never expire** setting is checked.
- [Disable password expiration using Microsoft Graph](/en-us/graph/api/domain-update?view=graph-rest-1.0&amp;preserve-view=true).
- [Set individual user passwords to never expire using Microsoft Graph PowerShell](/en-us/microsoft-365/admin/add-users/set-password-to-never-expire)
    - `Update-MgUser -UserId <UserID> -PasswordPolicies DisablePasswordExpiration`

### Smart lockout threshold set to 10 or less

When the smart lockout threshold is set to more than 10, threat actors can exploit the configuration to conduct reconnaissance, identify valid user accounts without triggering lockout protections, and establish initial access without detection. Once attackers gain initial access, they can move laterally through the environment by using the compromised account to access resources and escalate privileges.

Smart lockout helps lock out bad actors who try to guess your users' passwords or use brute force methods to get in. Smart lockout recognizes sign-ins that come from valid users and treats them differently than ones of attackers and other unknown sources. A threshold of more than 10 provides insufficient protection against automated password spray attacks, making it easier for threat actors to compromise accounts while evading detection mechanisms.

**Remediation action**

- [Set Microsoft Entra smart lockout threshold to 10 or less](/en-us/entra/identity/authentication/howto-password-smart-lockout).

### Smart lockout duration is set to a minimum of 60

When Smart Lockout duration is configured below the default 60 seconds, threat actors can exploit shortened lockout periods to conduct password spray and credential stuffing attacks more effectively. Reduced lockout windows allow attackers to resume authentication attempts more rapidly, increasing their success probability while potentially evading detection systems that rely on longer observation periods.

**Remediation action**

- [Set Smart Lockout duration to 60 seconds or higher](/en-us/entra/identity/authentication/howto-password-smart-lockout#manage-microsoft-entra-smart-lockout-values)

### Add organizational terms to the banned password list

Organizations that don't populate and enforce the custom banned password list expose themselves to a systematic attack chain where threat actors exploit predictable organizational password patterns. These threat actors typically start with reconnaissance phases, where they gather open-source intelligence (OSINT) from websites, social media, and public records to identify likely password components. With this knowledge, they launch password spray attacks that test organization-specific password variations across multiple user accounts, staying under lockout thresholds to avoid detection. Without the protection the custom banned password list offers, employees often add familiar organizational terms to their passwords, like locations, product names, and industry terms, creating consistent attack vectors.

The custom banned password list helps organizations plug this critical gap to prevent easily guessed passwords that could lead to initial access and subsequent lateral movement within the environment.

**Remediation action**

- [Learn how to enable custom banned password protection and add organizational terms](/en-us/entra/identity/authentication/tutorial-configure-custom-password-protection)

### Require multifactor authentication for device join and device registration using user action

Threat actors can exploit the lack of multifactor authentication during new device registration. Once authenticated, they can register rogue devices, establish persistence, and circumvent security controls tied to trusted endpoints. This foothold enables attackers to exfiltrate sensitive data, deploy malicious applications, or move laterally, depending on the permissions of the accounts being used by the attacker. Without MFA enforcement, risk escalates as adversaries can continuously reauthenticate, evade detection, and execute objectives.

**Remediation action**

- [Deploy a Conditional Access policy to require multifactor authentication for device registration](/en-us/entra/identity/conditional-access/policy-all-users-device-registration).

### Local Admin Password Solution is deployed

Without Local Admin Password Solution (LAPS) deployed, threat actors exploit static local administrator passwords to establish initial access. After threat actors compromise a single device with a shared local administrator credential, they can move laterally across the environment and authenticate to other systems sharing the same password. Compromised local administrator access gives threat actors system-level privileges, which lets them accomplish a wide range of malicious activities, including:

- Disable security controls
- Install persistent backdoors
- Exfiltrate sensitive data
- Establish command and control channels

The automated password rotation and centralized management of LAPS closes this security gap and adds controls to help manage who has access to these critical accounts. Without solutions like LAPS, you can't detect or respond to unauthorized use of local administrator accounts, giving threat actors extended dwell time to achieve their objectives while remaining undetected.

**Remediation action**

- [Configure Windows Local Administrator Password Solution](/en-us/entra/identity/devices/howto-manage-local-admin-passwords).

### Entra Connect Sync is configured with Service Principal Credentials

Microsoft Entra Connect Sync using user accounts instead of service principals creates security vulnerabilities. Legacy user account authentication with passwords is more susceptible to credential theft and password attacks than service principal authentication with certificates. Compromised connector accounts allow threat actors to manipulate identity synchronization, create backdoor accounts, escalate privileges, or disrupt hybrid identity infrastructure.

**Remediation action**

- [Configure service principal authentication for Entra Connect](/en-us/entra/identity/hybrid/connect/authenticate-application-id?tabs=default#onboard-to-application-based-authentication)
- [Remove legacy Directory Synchronization Accounts](/en-us/entra/identity/hybrid/connect/authenticate-application-id?tabs=default#remove-a-legacy-service-account)

### Directory sync account is locked down to specific named location

Directory synchronization accounts are highly privileged service accounts that facilitate identity synchronization between on-premises Active Directory and Microsoft Entra ID. Without location-based access controls, threat actors who compromise these accounts can synchronize malicious changes from any location, including unauthorized networks or geographic regions.

Once a directory sync account is compromised, threat actors can:

- Manipulate identity synchronization processes
- Create unauthorized user accounts
- Escalate privileges of existing accounts
- Persist access by modifying synchronization rules

Unrestricted network access allows threat actors to operate remotely from compromised infrastructure, making detection harder while maintaining long-term access to the hybrid identity environment. Restricting these accounts to trusted named locations through Conditional Access policies limits the attack surface by ensuring synchronization operations only occur from authorized network locations.

**Remediation action**

- [Block access by location with Conditional Access](/en-us/entra/identity/conditional-access/policy-block-by-location).

### No usage of ADAL in the tenant

Microsoft ended support and security fixes for ADAL on June 30, 2023. Continued ADAL usage bypasses modern security protections available only in MSAL, including Conditional Access enforcement, Continuous Access Evaluation (CAE), and advanced token protection. ADAL applications create security vulnerabilities by using weaker legacy authentication patterns, often calling deprecated Azure AD Graph endpoints, and preventing adoption of hardened authentication flows that could mitigate future security advisories.

**Remediation action**

- [Migrate applications to the Microsoft Authentication Library (MSAL)](/en-us/entra/identity-platform/msal-migration)

### Block legacy Azure AD PowerShell module

Threat actors frequently target legacy management interfaces such as the Azure AD PowerShell module (AzureAD and AzureADPreview), which don't support modern authentication, Conditional Access enforcement, or advanced audit logging. Continued use of these modules exposes the environment to risks including weak authentication, bypass of security controls, and incomplete visibility into administrative actions. Attackers can exploit these weaknesses to gain unauthorized access, escalate privileges, and perform malicious changes.

Block the Azure AD PowerShell module (appID: 00001111-aaaa-2222-bbbb-3333cccc4444) and enforce the use of Microsoft Graph PowerShell or Microsoft Entra PowerShell to ensure that only secure, supported, and auditable management channels are available, which closes critical gaps in the attack chain.

**Remediation action**

- [Disable user sign-in for application](/en-us/entra/identity/enterprise-apps/disable-user-sign-in-portal)

### Enable Microsoft Entra ID security defaults for free tenants

Enabling security defaults in Microsoft Entra is essential for organizations with Microsoft Entra Free licenses to protect against identity-related attacks. These attacks can lead to unauthorized access, financial loss, and reputational damage. Security defaults require all users to register for multifactor authentication (MFA), ensure administrators use MFA, and block legacy authentication protocols. This significantly reduces the risk of successful attacks, as more than 99% of common identity-related attacks are stopped by using MFA and blocking legacy authentication. Security defaults offer baseline protection at no extra cost, making them accessible for all organizations.

**Remediation action**

- [Enable security defaults in Microsoft Entra ID](/en-us/entra/fundamentals/security-defaults#enabling-security-defaults)