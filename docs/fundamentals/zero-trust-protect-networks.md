---
layout: Conceptual
title: Security guidance - Protect networks - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/zero-trust-protect-networks
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: pmwongera
description: Improve your security posture with the Microsoft Entra Zero Trust assessment to protect networks.
ms.topic: concept-article
ms.date: 2026-04-30T00:00:00.0000000Z
ms.reviewer: ramical
locale: en-us
document_id: 73b4fe1c-e018-0adc-cc62-45592f2bc1e2
document_version_independent_id: 73b4fe1c-e018-0adc-cc62-45592f2bc1e2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/zero-trust-protect-networks.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/zero-trust-protect-networks
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/zero-trust-protect-networks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: 84cccd0b-1447-8b0f-9be5-31dfa9e49965
---

# Security guidance - Protect networks - Microsoft Entra | Microsoft Learn

The "Protect networks" pillar of the [Secure Future Initiative](https://www.microsoft.com/trust-center/security/secure-future-initiative?msockid=2bad2df65a416adb0e5838355b3e6b95#SFI-pillars) emphasizes the critical importance of securing network access and implementing network-based controls to prevent unauthorized access to organizational resources. The best practices in this pillar focus on actions such as establishing network boundaries, controlling traffic flows, and implementing location-based access policies that verify the trustworthiness of network connections before granting access.

## Zero Trust security recommendations

### Named locations are configured

Without named locations configured in Microsoft Entra ID, threat actors can exploit the absence of location intelligence to conduct attacks without triggering location-based risk detections or security controls. When organizations fail to define named locations for trusted networks, branch offices, and known geographic regions, Microsoft Entra ID Protection can't assess location-based risk signals. Not having these policies in place can lead to increased false positives that create alert fatigue and potentially mask genuine threats. This configuration gap prevents the system from distinguishing between legitimate and illegitimate locations. For example, legitimate sign-ins from corporate networks and suspicious authentication attempts from high-risk locations (anonymous proxy networks, Tor exit nodes, or regions where the organization has no business presence). Threat actors can use this uncertainty to conduct credential stuffing attacks, password spray campaigns, and initial access attempts from malicious infrastructure without triggering location-based detections that would normally flag such activity as suspicious. Organizations can also lose the ability to implement adaptive security policies that could automatically apply stricter authentication requirements or block access entirely from untrusted geographic regions. Threat actors can maintain persistence and conduct lateral movement from any global location without encountering location-based security barriers, which should serve as an extra layer of defense against unauthorized access attempts.

**Remediation action**

- [Configure named locations to define trusted IP ranges and geographic regions for enhanced location-based risk detection and Conditional Access policy enforcement](/en-us/entra/identity/conditional-access/concept-assignment-network)

### Tenant restrictions v2 policy is configured

Tenant Restrictions v2 (TRv2) allows organizations to enforce policies that restrict access to specified Microsoft Entra tenants, preventing unauthorized exfiltration of corporate data to external tenants using local accounts. Without TRv2, threat actors can exploit this vulnerability, which leads to potential data exfiltration and compliance violations, followed by credential harvesting if those external tenants have weaker controls. Once credentials are obtained, threat actors can gain initial access to these external tenants. TRv2 provides the mechanism to prevent users from authenticating to unauthorized tenants. Otherwise, threat actors can move laterally, escalate privileges, and potentially exfiltrate sensitive data, all while appearing as legitimate user activity that bypasses traditional data loss prevention controls focused on internal tenant monitoring.

Implementing TRv2 enforces policies that restrict access to specified tenants, mitigating these risks by ensuring that authentication and data access are confined to authorized tenants only.

If this check passes, your tenant has a TRv2 policy configured but more steps are required to validate the scenario end-to-end.

**Remediation action**

- [Set up Tenant Restrictions v2](/en-us/entra/external-id/tenant-restrictions-v2)

### Network validation is configured through Universal Continuous Access Evaluation

Universal Continuous Access Evaluation (Universal CAE) validates network access tokens every time a connection is established through Global Secure Access tunnels. Without Universal CAE, tokens remain valid for 60 to 90 minutes regardless of changes to user state.

Without this protection:

- A threat actor who obtains a token through theft or replay can continue accessing all Global Secure Access-protected resources even after the user's account is disabled or password is reset.
- Critical events like session revocation or high user risk detection don't prompt immediate reauthentication.
- Departing employees or malicious insiders maintain network-level access to private corporate resources for up to 90 minutes after remediation action is taken.
- Token replay attacks from different IP addresses aren't blocked without Strict Enforcement mode.

**Remediation action**

- Review the [Universal CAE](/en-us/entra/global-secure-access/concept-universal-continuous-access-evaluation) capabilities for Global Secure Access.
- Remove or modify Conditional Access policies that disable CAE for Global Secure Access workloads. For more information, see [Continuous access evaluation](/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation).
- Configure Universal CAE to use Strict Enforcement mode for enhanced token replay protection. For more information, see [Universal Continuous Access Evaluation](/en-us/entra/global-secure-access/concept-universal-continuous-access-evaluation#strict-enforcement-mode).

### Global Secure Access client is deployed on all managed endpoints

Comprehensive deployment of the Global Secure Access client is foundational to achieving Zero Trust network security. If you don't deploy the Global Secure Access client to managed endpoints, those devices operate outside the organization's Security Service Edge controls. Threat actors can exploit unprotected endpoints to establish initial access, move laterally, or exfiltrate data without triggering network-level security policies.

Without the Global Secure Access client:

- Devices can't benefit from compliant network checks in Conditional Access policies, source IP restoration, or tenant restrictions.
- Credential theft and token replay attacks are more difficult to detect when traffic bypasses the security perimeter.
- Managed endpoints can't access private applications through Microsoft Entra Private Access.

**Remediation action**

- Install the Global Secure Access client:
    - [Windows client](/en-us/entra/global-secure-access/how-to-install-windows-client)
    - [macOS client](/en-us/entra/global-secure-access/how-to-install-macos-client)
    - [iOS client](/en-us/entra/global-secure-access/how-to-install-ios-client)
    - [Android client](/en-us/entra/global-secure-access/how-to-install-android-client)
- Monitor the Global Secure Access client health and connection status by using the [Global Secure Access dashboard](/en-us/entra/global-secure-access/concept-traffic-dashboard).

### Global Secure Access licenses are available in the tenant and assigned to users

Global Secure Access requires specific Microsoft Entra licenses to function, including Microsoft Entra Internet Access and Microsoft Entra Private Access, both of which require Microsoft Entra ID P1 as a prerequisite. Without valid licenses provisioned in the tenant, administrators can't configure traffic forwarding profiles, security policies, or remote network connections. If you don't assign licenses to users, their traffic doesn't route through Global Secure Access, and remains unprotected by security controls.

Without this protection:

- Threat actors can bypass web content filtering, threat protection, and Conditional Access policies.
- Expired or suspended subscriptions can halt the Global Secure Access service, creating security gaps where previously protected traffic flows go unmonitored.

**Remediation action**

- Review Global Secure Access licensing requirements and purchase appropriate licenses. For more information, see [Licensing overview](/en-us/entra/global-secure-access/overview-what-is-global-secure-access#licensing-overview).
- Assign licenses to users through the Microsoft 365 admin center. For more information, see [Assign or unassign licenses for users in the Microsoft 365 admin center](/en-us/microsoft-365/admin/manage/assign-licenses-to-users?view=o365-worldwide&amp;preserve-view=true).
- Use group-based licensing for easier management at scale. For more information, see [Assign or unassign licenses to a group in the Microsoft 365 admin center](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true).
- Monitor license utilization through Microsoft 365 admin center. For more information, see [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home#/licenses).
- Review Microsoft Entra Suite as an alternative that includes both Internet Access and Private Access. For more information, see [What's new in Microsoft Entra](/en-us/entra/fundamentals/whats-new#microsoft-entra-suite).

### Internet Access forwarding profile is enabled

When the Internet Access forwarding profile isn't enabled, users can access internet resources without routing traffic through the Secure Web Gateway. This gap allows threat actors to bypass security controls that block threats, malicious content, and unsafe destinations.

Without this protection:

- Organizations lose visibility into traffic patterns. They can't detect data exfiltration, connections to malicious domains, or unauthorized external access.
- Threat actors can deliver malware, establish command and control connections, or exfiltrate data through unmonitored channels.
- Threat actors can use compromised credentials or social engineering to gain initial access, download tools, establish persistence, or communicate with external infrastructure.
- Threat actors can use compromised accounts to blend with typical user behavior and access external resources without triggering security alerts based on user context, device compliance, or location.

**Remediation action**

- Enable the Internet Access forwarding profile to route traffic through the Secure Web Gateway. For more information, see [How to manage the Internet Access traffic forwarding profile](/en-us/entra/global-secure-access/how-to-manage-internet-access-profile).
- Assign users and groups to the Internet Access profile to limit traffic forwarding to specific users. For more information, see [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding).

### Web content filtering policies are configured

Web content filtering policies are the foundation of internet access control in Global Secure Access. Without any configured policies, users have unrestricted access to all internet destinations, exposing the organization to malware, phishing sites, and inappropriate content. Create filtering policies to block dangerous website categories and establish baseline internet access controls.

**Remediation action**

- [Configure web content filtering policies](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering)

### Web content filtering uses category-based rules

Category-based filtering provides broader protection than URL-specific rules. Blocking entire website categories like malware, phishing, hacking, and criminal activity prevents access to thousands of malicious sites at once. Filtering policies that only target specific URLs or domains require constant maintenance and leave gaps as threat actors register new malicious domains daily.

**Remediation action**

- [Review available web content filtering categories](/en-us/entra/global-secure-access/reference-web-content-filtering-categories)
- [Configure category-based filtering rules](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering)

### Web content filtering policies are linked to security profiles

Creating filtering policies without linking them to a security profile or the baseline profile leaves them unenforced. Policies must be associated with either the baseline profile (applies to all internet traffic) or a security profile (applies through Conditional Access) to take effect. Unlinked policies provide no protection and create false confidence in your security posture.

**Remediation action**

- [Create security profiles and link filtering policies](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile)

### Web content filtering integrates with Conditional Access

The baseline profile applies the same filtering rules to all users and sessions. Conditional Access integration enables identity-aware filtering that adapts based on user risk, device compliance, location, or group membership. Apply stricter filtering to risky sessions while allowing standard access for verified users on compliant devices, preventing compromised accounts from bypassing security controls.

**Remediation action**

- [Link security profiles to Conditional Access policies](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering#create-and-link-conditional-access-policy)

### Web content filtering blocks high-risk categories

When you don't block high-risk web content filtering categories like criminal activity, hacking, and illegal software, users who connect through Global Secure Access stay exposed to dangerous attack vectors and liability risks. These high-risk sites can distribute exploit code, malware-embedded software, and guidance on committing illegal acts that threat actors can use to compromise your environment.

Without this protection:

- Users can access sites that provide tools, scripts, and tutorials for unauthorized access, enabling threat actors to escalate their capabilities within the network.
- Pirated software and license key generators downloaded from illegal software sites frequently contain embedded malware that establishes persistence and enables lateral movement.
- The organization faces both security vulnerabilities and legal liability from uncontrolled access to high-risk content categories.

**Remediation action**

- [Configure web content filtering](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering) to block high-risk web content categories **Criminal activity**, **Hacking**, and **Illegal software**.
- Review all available [Global Secure Access web content filtering categories](/en-us/entra/global-secure-access/reference-web-content-filtering-categories).
- [Create security profiles](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile) to group filtering policies for Conditional Access enforcement.
- [Enable the Internet Access traffic forwarding profile](/en-us/entra/global-secure-access/how-to-manage-internet-access-profile) to route traffic through Global Secure Access for web content filtering to apply.
- [Link security profiles to Conditional Access](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering#create-and-link-conditional-access-policy) to enforce web content filtering for targeted users and groups.

### TLS inspection is enabled and correctly configured for outbound traffic

TLS inspection decrypts and inspects HTTPS traffic, enabling visibility into encrypted sessions. Without it, many Microsoft Entra Internet Access features can't function, including URL filtering and advanced threat detection. Most internet traffic is encrypted, so TLS inspection is essential for applying security policies to most user activity.

**Remediation action**

- [Configure Transport Layer Security Inspection Policies](/en-us/entra/global-secure-access/how-to-transport-layer-security)

### TLS inspection bypass rules are regularly reviewed

Transport Layer Security (TLS) inspection bypass rules create exceptions where encrypted traffic skips deep packet inspection. Without regular review, bypass rules accumulate as temporary exceptions become permanent, applications are decommissioned while their rules remain, or initial justifications become obsolete. Threat actors target uninspected traffic channels. They know that malware command-and-control communications, data exfiltration, and credential theft over HTTPS evade detection when traffic bypasses TLS inspection. Policies not modified in over 90 days might contain stale bypass rules that create blind spots in your network security posture.

**Remediation action**

- Establish a quarterly review process for TLS inspection bypass rules, document a business justification for each bypass rule, and remove rules that are no longer necessary.
- [Review and manage TLS inspection policies](/en-us/graph/api/resources/networkaccess-tlsinspectionpolicy) in the Microsoft Entra admin center under **Global Secure Access** &gt; **Secure** &gt; **TLS inspection**.
- Review the steps in [Configure Transport Layer Security inspection policies](/en-us/entra/global-secure-access/how-to-transport-layer-security) to understand how to modify or remove bypass rules as part of the review process.

### TLS inspection certificates have a sufficient validity period

TLS inspection uses an intermediate certificate authority to dynamically create leaf certificates for decrypting and inspecting encrypted traffic. When this certificate expires, the service can't perform TLS termination. This expiration immediately disables all TLS inspection capabilities, including URL filtering, threat detection, and data loss prevention on HTTPS traffic. Threat actors know that security controls often lapse during certificate expiration and they time attacks to coincide with these gaps.

If a certificate expires:

- The organization loses visibility into encrypted traffic.
- Threat actors can bypass TLS inspection to deliver encrypted malware, access command-and-control communications, and exfiltrate data.

**Remediation action**

- Maintain a 90-day buffer before certificate expiration to provide time to complete the renewal process. Microsoft recommends that signed certificates remain valid for at least six months.
- Follow the steps in [Configure Transport Layer Security inspection settings](/en-us/entra/global-secure-access/how-to-transport-layer-security-settings)to:
    - Create a new Certificate Signing Request (CSR) and upload a renewed certificate in the Microsoft Entra admin center.
    - Sign the CSR by using your organization's PKI infrastructure with a validity period of at least six months (Microsoft recommendation).
- Use [Active Directory Certificate Services (ADCS)](/en-us/entra/global-secure-access/scripts/powershell-active-directory-certificate-service) or [OpenSSL](/en-us/entra/global-secure-access/scripts/powershell-open-secure-sockets-layer) to sign the CSR.

### TLS inspection failure rate is below 1%

By using Transport Layer Security (TLS) inspection, Global Secure Access can decrypt encrypted HTTPS traffic and check it for threats, malicious content, and policy violations. If TLS inspection fails for a connection, that traffic bypasses security controls. Inspection failures can let potential malware delivery, command-and-control communications, or data exfiltration go undetected.

Failure rates above 1% point to systemic problems. These problems include certificate trust issues on endpoints, incompatible applications that use certificate pinning without proper bypass rules, or certificate authority configuration errors. Threat actors can also intentionally create connections that cause TLS inspection failures.

**Remediation action**

- [Configure diagnostic settings to export traffic logs](/en-us/entra/global-secure-access/how-to-view-traffic-logs#configure-diagnostic-settings-to-export-logs) to a Log Analytics workspace. Use these logs to monitor TLS inspection success rates and investigate the root causes of failures.
- Follow the steps in [Troubleshoot Global Secure Access Transport Layer Security inspection errors](/en-us/entra/global-secure-access/troubleshoot-transport-layer-security) to resolve common inspection failures.
- For destinations with certificate pinning, [add TLS bypass rules](/en-us/entra/global-secure-access/how-to-transport-layer-security) to reduce failure rates while keeping inspection for other traffic.

### TLS inspection custom bypass rules don't duplicate system bypass destinations

Global Secure Access maintains a system bypass list of destinations that are automatically excluded from Transport Layer Security (TLS) inspection. These bypass destinations represent known incompatibilities such as certificate pinning, mutual TLS requirements, or other technical constraints. Custom bypass rules that duplicate destinations in the system bypass list are redundant and serve no functional purpose.

Redundant rules consume policy capacity, create administrative overhead, and can cause confusion about which rules are necessary. TLS inspection supports up to 1,000 rules and 8,000 destinations per tenant. Maintaining a clean policy configuration with only necessary custom bypass rules improves manageability, simplifies security audits, and ensures that policy capacity is available for legitimate business requirements.

**Remediation action**

- Review and remove redundant custom TLS inspection bypass rules in the Microsoft Entra admin center. Navigate to **Global Secure Access** &gt; **Secure** &gt; **TLS inspection policies**.
- Review [the destinations included in the system bypass list](/en-us/entra/global-secure-access/faq-transport-layer-security#what-destinations-are-included-in-the-system-bypass).

### Threat intelligence filtering protects internet traffic

If you don't enable threat intelligence filtering in Global Secure Access, internet traffic from users and devices stays unprotected against connections to malicious destinations. Threat actors can use this gap to access phishing sites, deliver malware payloads, or communicate with command-and-control infrastructure.

Without this protection:

- Compromised endpoints can reach command-and-control servers to receive instructions, download tools, or exfiltrate sensitive data.
- Threat actors maintain unrestricted network communication paths, enabling persistence mechanisms and lateral movement.
- The organization can't block traffic to domains and URLs associated with active malware distribution, phishing campaigns, and other high-confidence threat indicators.

The baseline security profile provides tenant-wide protection without requiring Conditional Access policy configuration, while custom security profiles enable context-aware enforcement through Conditional Access integration.

**Remediation action**

Follow the steps in [How to configure Global Secure Access threat intelligence](/en-us/entra/global-secure-access/how-to-configure-threat-intelligence) to:

- Configure threat intelligence filtering in Global Secure Access to block connections to destinations on the threat intelligence feed.
- Create a security profile and link filtering policies, including threat intelligence.
- Link a security profile to a Conditional Access policy using the Global Secure Access session control.
- Configure the baseline profile for tenant-wide protection without Conditional Access.

### File transfer policies are configured to prevent data exfiltration

Without network content filtering policies configured in Global Secure Access, threat actors can exfiltrate data to unsanctioned destinations through browsers, applications, and APIs. File sharing services, cloud storage providers, and peer-to-peer transfer sites remain unrestricted when you don't implement network content filtering policies.

Without this protection:

- Threat actors can upload files containing intellectual property, credentials, or customer data to external services without detection.
- Unmanaged cloud applications and generative AI tools become exfiltration channels for sensitive information.
- The network layer lacks real-time data protection enforcement, allowing threat actors to bypass endpoint-based controls.
- Threat actors can disguise malicious payloads or sensitive data within common file formats and transfer them across the network perimeter undetected.

**Remediation action**

- [Configure Global Secure Access web content filtering](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering), including file policies to monitor and control file transfers.
- [Enable and manage the Microsoft traffic forwarding profile](/en-us/entra/global-secure-access/how-to-manage-microsoft-profile) that group filtering policies for enforcement through Conditional Access.
- [Link security profiles to Conditional Access policies](/en-us/entra/identity/conditional-access/concept-conditional-access-session) for user-aware and context-aware enforcement of network security policies.
- [Install the Global Secure Access client](/en-us/entra/global-secure-access/how-to-install-windows-client) on end-user devices to enable traffic acquisition and policy enforcement.

### AI Gateway protects enterprise generative AI applications from prompt injection attacks

If organizations don't use Prompt Shield protection, threat actors can exploit prompt injection vulnerabilities to compromise AI-powered workflows. Malicious users can craft adversarial inputs that manipulate large language models into ignoring system instructions, disclosing confidential data, or executing unintended actions like generating phishing content.

Without network-level prompt filtering:

- Direct prompt injection attacks can bypass application-layer safety mechanisms through sophisticated jailbreak techniques.
- Indirect prompt injection occurs when threat actors embed malicious instructions in external content that the AI processes.
- Each AI application must independently implement protection, creating inconsistent security postures and inadequate safeguards against new or custom AI deployments.

**Remediation action**

- [Enable the Internet Access traffic forwarding profile to route internet traffic through Global Secure Access](/en-us/entra/global-secure-access/how-to-manage-internet-access-profile).
- [Configure TLS inspection settings and deploy the CA certificate to allow inspection of encrypted AI application traffic](/en-us/entra/global-secure-access/how-to-transport-layer-security-settings).
- Follow the steps in [Protect enterprise generative AI applications with Prompt Shield](/en-us/entra/global-secure-access/how-to-ai-prompt-shield)to:
    - Create prompt policies to scan and block malicious prompts targeting generative AI applications.
    - Link prompt policies to security profiles to organize them for Conditional Access targeting.
    - Create Conditional Access policies to apply security profiles with prompt policies to users accessing internet resources.
- [Install the Global Secure Access client on user devices to enable traffic acquisition](/en-us/entra/global-secure-access/how-to-install-windows-client).

### Global Secure Access cloud firewall protects branch office internet traffic

When you connect remote networks to Global Secure Access through IPsec tunnels but don't set up cloud firewall policies, all internet-bound traffic from branch offices goes through the Security Service Edge without egress filtering controls. If a threat actor gains access to a branch office workstation, they can make outbound connections to command-and-control infrastructure, exfiltrate data over standard ports, or download malicious payloads without network-layer inspection.

Without Global Secure Access cloud firewall:

- You can't enforce a deny-by-default posture or restrict outbound communications from branch networks to unauthorized internet destinations.
- Threat actors can stage data for exfiltration, pivot to cloud resources, or move laterally without detection.
- Traditional perimeter defenses might assume all egress is legitimate, resulting in gaps in security coverage.

Cloud firewall policies linked to the baseline profile provide centralized egress control for all remote network traffic. Administrators can use these policies to define granular filtering rules that restrict unauthorized outbound communications.

**Remediation action**

- As a prerequisite for cloud firewall, [configure remote networks for internet access](/en-us/entra/global-secure-access/how-to-create-remote-networks).
- Follow the steps in [Configure Global Secure Access cloud firewall](/en-us/entra/global-secure-access/how-to-configure-cloud-firewall)to:
    - Create a cloud firewall policy with appropriate filtering rules.
    - Add or update firewall rules based on source IP, destination IP, ports, and protocols.
    - Link the cloud firewall policy to the baseline profile for remote networks.

### Internet traffic is inspected across all Secure Web Gateway defense layers

The Global Secure Access Secure Web Gateway (SWG) implements defense-in-depth through five security layers that together create a comprehensive inspection chain for internet-bound traffic. Each layer serves a distinct protective function:

- **Layer 1: Context-aware network security** This outermost layer routes internet traffic through the SWG and applies identity- and context-aware policy enforcement. Without this layer, traffic bypasses all downstream inspection.
- **Layer 2: TLS inspection, web content, and threat intelligence filtering** TLS inspection decrypts encrypted traffic so that all downstream web content filtering and DLP inspection operates on plaintext payloads. Web content filtering blocks access to malicious, inappropriate, or policy-violating destinations. Threat intelligence filtering blocks connections to known-malicious infrastructure.
- **Layer 3: AI Gateway, content filtering, and network DLP** AI Gateway controls govern user interactions with generative AI services to prevent prompt injection and data leakage. Content filtering and network DLP inspect file transfers and payloads to prevent sensitive data exfiltration.
- **Layer 4: Cloud firewall** This layer applies network-level firewall rules that protect branch office internet traffic routed through remote networks.
- **Layer 5: Advanced threat protection** This innermost layer is reserved for future capabilities including anti-malware scanning, intrusion detection and prevention (IDPS), and anomaly detection. No active checks are configured in this layer yet.

When any layer is missing, threat actors can exploit the gap to download tools, exfiltrate data, or maintain persistent command-and-control channels.

**Remediation action**

Follow the remediation steps in the order shown to align with configuration dependencies across layers.

1. [Enable the Internet Access traffic forwarding profile](/en-us/entra/global-secure-access/how-to-manage-internet-access-profile) to route traffic through the Secure Web Gateway.
2. [Configure TLS inspection](/en-us/entra/global-secure-access/how-to-transport-layer-security) to enable decryption and plaintext analysis of encrypted traffic.
3. [Configure web content filtering policies](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering) to block access to malicious and policy-violating destinations.
4. [Link filtering policies to security profiles](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering#create-a-security-profile) to bind policies for enforcement.
5. [Link security profiles to Conditional Access policies](/en-us/entra/global-secure-access/how-to-configure-web-content-filtering#create-and-link-conditional-access-policy) to enforce identity-aware policy application.
6. [Configure threat intelligence filtering](/en-us/entra/global-secure-access/how-to-configure-threat-intelligence) to block connections to known-malicious infrastructure.
7. [Configure AI Gateway](/en-us/entra/global-secure-access/how-to-ai-prompt-shield) prompt protection policies for generative AI services.
8. [Configure network content filtering policies](/en-us/entra/global-secure-access/how-to-network-content-filtering) to prevent data exfiltration through file transfers.
9. [Configure cloud firewall rules](/en-us/entra/global-secure-access/how-to-configure-cloud-firewall) for branch office internet traffic routed through remote networks.

### Microsoft 365 traffic is actively flowing through Global Secure Access

When Microsoft 365 traffic bypasses Global Secure Access, organizations lose visibility and control over their most critical productivity workloads. Threat actors who exploit unmonitored Microsoft 365 connections can exfiltrate sensitive data through SharePoint, OneDrive, or Exchange without triggering security policies or generating actionable telemetry. Token theft and replay attacks become more difficult to detect when traffic doesn't flow through the Security Service Edge because source IP correlation with sign-in logs and Conditional Access evaluation can't be applied consistently.

Organizations with significant bypassed traffic, whether due to incomplete client deployment, misconfigured forwarding profiles, or users on unmanaged devices, create blind spots where adversary-in-the-middle attacks, credential harvesting, and unauthorized data transfers can proceed undetected. Traffic that bypasses Global Secure Access also can't benefit from compliant network checks in Conditional Access policies, tenant restrictions, or source IP restoration, leaving significant security controls ineffective.

**Remediation action**

- Enable and configure the Microsoft traffic profile. For more information, see [Enable Microsoft traffic profile](/en-us/entra/global-secure-access/how-to-manage-microsoft-profile).
- Deploy the Global Secure Access client to all managed devices. For more information, see [Deploy Global Secure Access client](/en-us/entra/global-secure-access/how-to-install-windows-client).
- Review and configure traffic forwarding rules appropriately. For more information, see [Review traffic forwarding rules](/en-us/entra/global-secure-access/concept-microsoft-traffic-profile).

### Universal tenant restrictions block unauthorized external tenant access

Without universal tenant restrictions configured, users on corporate devices and networks can authenticate to unauthorized external Microsoft Entra tenants and access cloud applications by using external identities. This vulnerability makes it possible for a threat actor to use compromised user credentials or established persistence on a corporate device to authenticate to a tenant they control. They can bypass traditional network security controls that can't inspect encrypted authentication traffic to Microsoft identity endpoints.

Once authenticated to an external tenant, a threat actor can access Microsoft Graph APIs and cloud services. This access enables data exfiltration through OneDrive, SharePoint, Teams, or any Microsoft Entra-integrated application in the external tenant. This attack path exploits the inherent trust that corporate networks and devices have with Microsoft identity services. Universal tenant restrictions address this vulnerability by injecting tenant identity headers into authentication plane traffic through Global Secure Access. Microsoft Entra ID uses these headers to enforce tenant restrictions v2 policies that block authentication attempts to unauthorized external tenants.

**Remediation action**

- [Set up tenant restrictions v2](/en-us/entra/external-id/tenant-restrictions-v2) policies to block all external tenants by default.
- [Turn on universal tenant restrictions](/en-us/entra/global-secure-access/how-to-universal-tenant-restrictions) signaling in Global Secure Access.
- [Deploy Global Secure Access client](/en-us/entra/global-secure-access/concept-clients) on devices.
- [Enable the Microsoft traffic profile](/en-us/entra/global-secure-access/how-to-manage-microsoft-profile).

### Conditional Access policies use compliant network controls

Without compliant network controls in Conditional Access policies, organizations can't enforce that users connect to corporate resources through the Global Secure Access service. This limitation leaves authentication traffic vulnerable to interception and replay attacks from arbitrary network locations.

A threat actor who obtains valid user credentials through phishing or credential theft can authenticate from any internet location, bypassing Global Secure Access network controls. Once authenticated, the threat actor can access Microsoft Entra ID-integrated applications and services, exfiltrate data, or establish persistence by creating additional credentials or modifying user permissions.

The compliant network check reduces this risk by requiring that authentication traffic originates from the Global Secure Access service, which tags authentication requests with tenant-specific network identity signals. This requirement enables Microsoft Entra ID Conditional Access to verify that users connect through the organization's secured network path before granting access.

**Remediation action**

- Enable Global Secure Access signaling for Conditional Access. For more information, see [Enable compliant network check with Conditional Access](/en-us/entra/global-secure-access/how-to-compliant-network#enable-global-secure-access-signaling-for-conditional-access).
- Create a Conditional Access policy that requires compliant network for access. For more information, see [Protect your resources behind the compliant network](/en-us/entra/global-secure-access/how-to-compliant-network#protect-your-resources-behind-the-compliant-network).
- Deploy Global Secure Access clients on devices. For more information, see [Global Secure Access clients overview](/en-us/entra/global-secure-access/concept-clients).
- Understand compliant network enforcement. For more information, see [Compliant network check enforcement](/en-us/entra/global-secure-access/how-to-compliant-network#compliant-network-check-enforcement).

### Global Secure Access signaling for Conditional Access is enabled

When Global Secure Access routes user traffic through Microsoft's Security Service Edge, it replaces the original source IP with the proxy egress IP. If you don't enable Global Secure Access signaling for Conditional Access, Microsoft Entra ID receives the proxy IP instead of the user's actual IP address. Conditional Access policies that rely on named locations or trusted IP ranges evaluate the proxy IP instead of the user's actual IP, reducing the effectiveness of location-based controls.

If you don't enable Global Secure Access signaling for Conditional Access:

- Microsoft Entra ID Protection risk detections that depend on source IP, such as impossible travel and unfamiliar sign-in properties, are less reliable.
- Sign-in logs record the proxy IP, which prevents security operations teams from correlating sign-in events to user locations during incident response.

**Remediation action**

- [Enable Global Secure Access signaling for Conditional Access](/en-us/entra/global-secure-access/how-to-source-ip-restoration#enable-global-secure-access-signaling-for-conditional-access).
- [Enable compliant network check with Conditional Access](/en-us/entra/global-secure-access/how-to-compliant-network) to require users to connect through Global Secure Access.
- [Understand how Universal Conditional Access works with Global Secure Access traffic profiles](/en-us/entra/global-secure-access/concept-universal-conditional-access).

### Network traffic is routed through Global Secure Access for security policy enforcement

Traffic forwarding profiles are the foundational mechanism through which Global Secure Access captures and routes network traffic to Microsoft's Security Service Edge infrastructure. If you don't enable the appropriate traffic forwarding profiles, network traffic bypasses the Global Secure Access service entirely, and users don't get these network access protections.

There are three distinct profiles:

- **Microsoft traffic profile**: Captures Microsoft Entra ID, Microsoft Graph, SharePoint Online, Exchange Online, and other Microsoft 365 workloads.
- **Private access profile**: Captures traffic destined for internal corporate resources.
- **Internet access profile**: Captures traffic to the public internet including non-Microsoft SaaS applications.

If you don't enable these profiles:

- You can't enforce security policies, web content filtering, threat protection, or Universal Continuous Access Evaluation.
- Threat actors who compromise user credentials can access corporate resources without the security controls that Global Secure Access would otherwise apply.

**Remediation action**

- Enable the Microsoft traffic forwarding profile. For more information, see [Manage the Microsoft traffic profile](/en-us/entra/global-secure-access/how-to-manage-microsoft-profile).
- Enable the Private Access traffic forwarding profile. For more information, see [Manage the Private Access traffic forwarding profile](/en-us/entra/global-secure-access/how-to-manage-private-access-profile).
- Enable the Internet Access traffic forwarding profile. For more information, see [Manage the Internet Access traffic forwarding profile](/en-us/entra/global-secure-access/how-to-manage-internet-access-profile).

### Traffic forwarding profiles are scoped to appropriate users and groups for controlled deployment

Without proper scoping of traffic forwarding profiles, organizations risk either exposing all users to security controls before infrastructure readiness is validated or inadvertently excluding users who should be protected.

Risks of improper scoping:

- **Too broad**: When profiles are assigned to "all users" without deliberate planning, a misconfiguration could disrupt network connectivity for the entire organization simultaneously.
- **Too narrow**: If profiles are scoped too narrowly or assignments are incomplete, a subset of users operates outside the security perimeter, creating gaps that threat actors can exploit.
- **Unmonitored access**: Attackers who compromise devices belonging to unassigned users can access resources without traffic being inspected, logged, or subject to security policies.

Proper scoping ensures controlled rollout—starting with pilot groups to validate functionality, then expanding to broader populations—while maintaining visibility into which users are protected.

**Remediation action**

- Assign users and groups to traffic forwarding profiles. For more information, see [Manage users and groups assignment](/en-us/entra/global-secure-access/how-to-manage-users-groups-assignment).

### Private network connectors are active and healthy to maintain Zero Trust access to internal resources

When Microsoft Entra private network connectors are inactive or unhealthy, organizations might resort to using less secure access methods. This condition creates opportunities where threat actors can target externally exposed services or use compromised credentials.

Without functional connectors:

- Token-based authentication and authorization for all Microsoft Entra Private Access scenarios is eliminated.
- Threat actors can bypass intended security boundaries to access resources beyond their authorization scope.
- The service can't route requests properly, directly disrupting network access controls.

**Remediation action**

- [Configure connectors for high availability](/en-us/entra/global-secure-access/how-to-configure-connectors).
- Monitor connector health in the Microsoft Entra admin center under Global Secure Access &gt; Connect &gt; Connectors.
- [Troubleshoot connector installation and connectivity issues](/en-us/entra/global-secure-access/troubleshoot-connectors).

### Private network connectors are running the latest version

The private network connector is a key component of Microsoft Entra Private Access and Application Proxy. To maintain security, stability, and performance, all connector machines must run the latest software version.

If your connectors don't run the latest version:

- They might be missing critical security patches, which leaves connectors vulnerable to known exploits.
- You don't get the latest performance improvements and bug fixes, which can affect reliability.
- Compatibility problems might arise with the Global Secure Access service as it evolves.

**Remediation action**

- [Configure private network connectors for Microsoft Entra Private Access and Microsoft Entra application proxy](/en-us/entra/global-secure-access/how-to-configure-connectors).
- Verify that all your connectors are up to date and install the latest [connector updates](/en-us/entra/global-secure-access/concept-connectors#connector-updates).

### At least two Private Access connectors are active and healthy per connector group

Microsoft Entra Private Access uses private network connectors to broker connections from on-premises or cloud-hosted networks to the Global Secure Access service. Each connector group serves as the only access path for the private applications assigned to it. If you deploy only one connector in a group, any failure of that host immediately removes all private application access for users who rely on that group.

Without this protection:

- A single connector failure causes a complete loss of private resource access for all users who rely on that connector group until you manually restore the connector.
- A threat actor who terminates the connector Windows service or blocks its outbound Transport Layer Security (TLS) communication can silently deny access to private applications without triggering identity-layer alerts.
- Automatic updates that target one connector at a time might cause downtime when only one connector exists in a group.
- You can't apply Conditional Access policies when the connector is unreachable, and users are denied access rather than routed through an alternative enforcement point.

**Remediation action**

- [Install and register an additional private network connector](/en-us/entra/global-secure-access/how-to-configure-connectors) on a Windows Server in the affected region.
- [Learn about connector group high-availability requirements](/en-us/entra/global-secure-access/concept-connectors#connector-groups) and best practices.
- [Review sizing and resiliency guidance](/en-us/entra/global-secure-access/concept-connectors#specifications-and-sizing-requirements) for Microsoft Entra private network connectors, including the minimum two-connector recommendation.
- [Review high-availability load-balancing best practices](/en-us/entra/identity/app-proxy/application-proxy-high-availability-load-balancing#best-practices-for-high-availability-of-connectors) applicable to Private Access connector groups.
- [Troubleshoot inactive or malfunctioning private network connectors](/en-us/entra/global-secure-access/troubleshoot-connectors).

### Private DNS is configured for internal name resolution

Without private DNS configuration, remote users can't resolve internal domain names through Microsoft Entra Private Access and must rely on public DNS servers. Threat actors can exploit this gap through DNS spoofing attacks that redirect users to malicious sites, enabling credential harvesting and data exfiltration. Organizations also lose visibility into DNS queries and can't enforce consistent security policies.

**Remediation action**

- [Configure private DNS for internal name resolution](/en-us/entra/global-secure-access/how-to-configure-quick-access#add-private-dns-suffixes)

### DNS traffic for internal domains is routed through Private Access

When you enable the Private Access profile in Global Secure Access but don't publish port 53 (UDP/TCP) in application segments or configure private DNS suffixes, the Global Secure Access client can't route DNS queries for internal domain names through the tunnel. As a result, DNS queries for internal FQDNs go to the local resolver on the device, which has no knowledge of internal zones.

Without this configuration:

- FQDN-based application segments fail to match traffic because the client can't resolve internal host names to IP addresses.
- Threat actors operating on the same local network as the remote user can observe unencrypted DNS queries, map internal resource names, and identify targets for later stages of an attack.
- The client might fall back to direct connections that bypass Conditional Access and security profile enforcement applied through Global Secure Access.

**Remediation action**

- [Configure private DNS suffixes for Quick Access or per-app access](/en-us/entra/global-secure-access/how-to-configure-quick-access) so DNS queries for internal domains go through Global Secure Access.
- [Configure per-app access with application segments](/en-us/entra/global-secure-access/how-to-configure-per-app-access) that include port 53 (UDP/TCP) to an internal DNS server.
- [Learn about Microsoft Entra Private Access](/en-us/entra/global-secure-access/concept-private-access) in Global Secure Access.

### Intelligent Local Access is enabled and configured

Intelligent Local Access (ILA) routes Microsoft Entra Private Access traffic locally instead of through the cloud, improving performance while maintaining policy enforcement. Without ILA, users might disable the Global Secure Access client to improve performance and bypass Conditional Access policies. Configure private networks for your user sites to ensure local routing while preserving security controls.

**Remediation action**

- [Enable Intelligent Local Network](/en-us/entra/global-secure-access/enable-intelligent-local-access)

### Quick Access is enabled and bound to a connector

When you don't configure Quick Access or bind it to a connector group with active connectors, users can access private network resources through paths that bypass Global Secure Access controls. Threat actors who compromise user credentials can reach internal FQDNs and IP ranges without Conditional Access evaluation, because traffic doesn't route through the Global Secure Access service.

Without connector-mediated traffic brokering:

- There's no enforcement point between the user and the private resource, so Conditional Access policies targeting the Quick Access enterprise application don't apply.
- Threat actors can use stolen credentials to authenticate, move between internal systems, and exfiltrate data.
- The organization loses visibility through Global Secure Access traffic logs.

If you bind Quick Access to a connector group with active connectors, you ensure that private network traffic routes through Global Secure Access, where Conditional Access policies, user assignments, and traffic logging apply.

**Remediation action**

- [Configure Quick Access for Global Secure Access](/en-us/entra/global-secure-access/how-to-configure-quick-access).
- [Configure private network connectors for Global Secure Access](/en-us/entra/global-secure-access/how-to-configure-connectors).
- [Enable the Private Access traffic forwarding profile](/en-us/entra/global-secure-access/how-to-manage-private-access-profile).
- [Review Microsoft Entra Private Access concepts](/en-us/entra/global-secure-access/concept-private-access).

### Quick Access is bound to a Conditional Access policy

When you configure Quick Access in Microsoft Entra Private Access without Conditional Access policies, threat actors who compromise user credentials gain unrestricted access to private resources. The Quick Access application serves as a container for private resources including FQDNs and IP addresses.

Without policy enforcement:

- Compromised accounts provide a direct pathway to internal systems.
- Threat actors operating from unmanaged devices or anomalous locations can access private resources indistinguishably from authorized users.
- Lateral movement across the internal network and data exfiltration from private applications become possible.
- Multifactor authentication requirements and device health checks can't be enforced.

**Remediation action**

- [Apply Conditional Access Policies to Microsoft Entra Private Access Apps](/en-us/entra/global-secure-access/how-to-target-resource-private-access-apps).

### Entra Private Access Application segments are defined to enforce least-privilege access

When organizations configure Microsoft Entra Private Access with broad application segments, such as wide IP ranges, multiple protocols, or Quick Access configurations, they effectively replicate the over-permissive access model of traditional VPNs. This approach contradicts the Zero Trust principle of least privilege, where users should only reach the specific resources required for their role.

Risks of broad segmentation:

- Threat actors who compromise a user's credentials or device can use broad network permissions to perform reconnaissance, identifying other systems and services within the permitted range.
- Lateral movement becomes easier as attackers can access multiple systems through a single compromised credential.
- Incident response is complicated because security teams can't quickly determine which specific resources a compromised identity could access.

Configuring per-application segmentation with tightly scoped destination hosts, specific ports, and Custom Security Attributes enables dynamic Conditional Access enforcement. This approach requires stronger authentication or device compliance for high-risk applications while streamlining access to lower-risk resources.

**Remediation action**

- [Review and refine application segments](/en-us/entra/global-secure-access/how-to-configure-per-app-access) to use specific FQDNs, IP addresses, and specific port ranges that match application requirements rather than wide port ranges.

### Domain controller RDP access is protected by phishing-resistant authentication through Global Secure Access

When administrators use Microsoft Entra Private Access to reach domain controllers through Remote Desktop Protocol (RDP), they authenticate through Microsoft Entra ID before the Global Secure Access client tunnels their connection to the on-premises network. Domain controllers hold the cryptographic keys to the entire Active Directory forest. Compromising one domain controller offers a way to compromise every identity and resource in the organization.

Without phishing-resistant authentication:

- Threat actors can intercept credentials during phishing campaigns or adversary-in-the-middle attacks.
- Stolen session tokens can be replayed to establish RDP connections to domain controllers.
- Once connected, threat actors can execute DCSync attacks to harvest all password hashes in the domain.
- Attackers can create golden tickets for indefinite domain persistence.
- Group Policy Objects can be modified to deploy ransomware or backdoors across all domain-joined machines.

By requiring phishing-resistant authentication, organizations ensure that even if users are successfully phished, threat actors can't replay credentials because these methods require cryptographic proof of possession.

**Remediation action**

- [Deploy phishing-resistant authentication methods to domain controller administrators](/en-us/entra/identity/authentication/how-to-deploy-phishing-resistant-passwordless-authentication).
- [Require phishing-resistant authentication for administrators accessing domain controllers via RDP](/en-us/entra/global-secure-access/how-to-configure-domain-controllers).

### Private Access sensors are enforcing strong authentication policies on domain controllers

If you don't deploy Microsoft Entra Private Access sensors to domain controllers, threat actors can exploit Kerberos authentication requests from any device on the network, including unmanaged or compromised endpoints. They can use this vulnerability to get service tickets for on-premises resources without multifactor authentication or device compliance validation.

If you don't deploy Private Access sensors to domain controllers:

- Threat actors can request Kerberos tickets for privileged resources such as file shares, database servers, and remote desktop services. This vulnerability enables lateral movement across the on-premises environment.
- Conditional Access policies don't apply to Kerberos authentication, because it operates within a perimeter-based trust model where any authenticated user can request tickets regardless of authentication strength or device posture.
- Compromised user credentials obtained through phishing or credential theft can be immediately used to access domain-authenticated resources without triggering multifactor authentication requirements.

**Remediation action**

- [Configure Microsoft Entra Private Access for Active Directory domain controllers](/en-us/entra/global-secure-access/how-to-configure-domain-controllers).

### Quick Access has user or group assignments

When Quick Access lacks user or group assignments, the service prevents connections to fully qualified domain names (FQDNs) and IP addresses that you configure in the application segments. This restriction disrupts access to internal resources like file shares, web applications, and databases. When users can't reach resources through the Global Secure Access client, they might seek alternative access methods that bypass security controls such as Conditional Access policies and multifactor authentication.

If you don't assign users to Quick Access:

- Authorized users can't reach internal resources through Private Access, creating gaps in business continuity.
- Administrators might implement temporary workarounds that weaken the organization's security posture.

**Remediation action**

- [Assign users and groups to Quick Access](/en-us/entra/global-secure-access/how-to-configure-quick-access) to enable Private Access connectivity to configured application segments.

### All Private Access apps have user or group assignments

When Microsoft Entra Private Access applications lack user or group assignments, users can't establish tunnels through the application to reach the configured fully qualified domain names (FQDNs) and IP addresses. This restriction prevents access to protected internal resources. Without assignments, organizations can't enforce Conditional Access policies because these policies require explicit user-to-application relationships to evaluate risk signals, device compliance, and authentication strength requirements.

Without user assignments on Private Access applications:

- Organizations lose the ability to enforce least privilege access controls where users get access only to the specific resources they need.
- Organizations can't apply risk-based access policies that block or challenge authentication based on sign-in risk, user risk, or device compliance.
- Identity protection signals that detect credential compromise, impossible travel, or anonymous IP addresses can't protect private resources.

**Remediation action**

- [Assign users and groups to Private Access applications](/en-us/entra/global-secure-access/how-to-configure-per-app-access#assign-users-and-groups) to enable Zero Trust access controls and Conditional Access enforcement.