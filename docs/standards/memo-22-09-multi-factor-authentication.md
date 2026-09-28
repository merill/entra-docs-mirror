---
layout: Conceptual
title: Memo 22-09 multifactor authentication requirements overview - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/standards/memo-22-09-multi-factor-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
manager: martinco
description: Get guidance on meeting multifactor authentication requirements outlined in the Office of Management and Budget memorandum 22-09.
ms.service: entra
ms.subservice: standards
ms.topic: how-to
author: janicericketts
ms.author: jricketts
ms.reviewer: martinco, gasinh
ms.date: 2025-02-10T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 5a73d324-5e4b-4f6e-36ae-4ff352a8060a
document_version_independent_id: 2deac1ec-8746-30ff-ee65-68caffef6470
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/standards/memo-22-09-multi-factor-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: standards/memo-22-09-multi-factor-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/standards/memo-22-09-multi-factor-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 57caf4df-4afa-8e18-d160-5ecc2b7ea013
---

# Memo 22-09 multifactor authentication requirements overview - Microsoft Entra | Microsoft Learn

Learn about using Microsoft Entra ID as the centralized identity management system when implementing Zero Trust principles. See, US Office of Management and Budget (OMB) [M 22-09 Memorandum for the Heads of Executive Departments and Agencies](https://bidenwhitehouse.archives.gov/wp-content/uploads/2022/01/M-22-09.pdf).

The memo requirements are that employees use enterprise-managed identities to access applications, and that multifactor authentication protects employees from sophisticated online attacks, such as phishing. This attack method attempts to obtain and compromise credentials, with links to inauthentic sites.

Multifactor authentication prevents unauthorized access to accounts and data. The memo requirements cite multifactor authentication with phishing-resistant methods: authentication processes designed to detect and prevent disclosure of authentication secrets and outputs to a website or application masquerading as a legitimate system. Therefore, establish what multifactor authentication methods qualify as phishing-resistant.

## Phishing-resistant methods

Some federal agencies deployed modern credentials such as FIDO2 security keys or Windows Hello for Business. Many are evaluating Microsoft Entra authentication with certificates.

Learn more:

- [FIDO2 security keys](../identity/authentication/concept-authentication-passkeys-fido2)
- [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-overview)
- [Overview of Microsoft Entra certificate-based authentication](../identity/authentication/concept-certificate-based-authentication)

Some agencies are modernizing their authentication credentials. There are multiple options for meeting phishing-resistant multifactor authentication requirements with Microsoft Entra ID. Microsoft recommends adopting phishing-resistant multifactor authentication method that matches the agency capabilities. Consider what's possible now for phishing-resistance multifactor authentication to improve the overall cybersecurity posture. Implement modern credentials. However, if the quickest path isn't a modern approach, take the step to begin the journey toward modern approaches.

![Diagram of Microsoft Entra phishing-resistant multifactor authentication methods.](media/memo-22-09/azure-entra-pr-methods.png)

### Modern approaches

- **FIDO2 security keys**are, according to the Cybersecurity & Infrastructure Security Agency (CISA) the gold standard of multifactor authentication
    - See, [Passwordless authentication options for Microsoft Entra ID, FIDO2 security keys](../identity/authentication/concept-authentication-passkeys-fido2)
    - Go to cisa.gov for [More than a Password](https://www.cisa.gov/mfa)
- **Microsoft Entra certificate authentication**without dependency on a federated identity provider.
    - This solution includes smart card implementations: Common Access Card (CAC), Personal Identity Verification (PIV), and derived PIV credentials for mobile devices or security keys
    - See, [Overview of Microsoft Entra certificate-based authentication](../identity/authentication/concept-certificate-based-authentication)
- **Windows Hello for Business**has phishing-resistant multifactor authentication
    - See, [Windows Hello for Business Deployment Overview](/en-us/windows/security/identity-protection/hello-for-business/hello-deployment-guide)
    - See, [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/)

### Protection from external phishing

Microsoft Authenticator and Conditional Access policies enforce managed devices: Microsoft Entra hybrid joined devices or devices marked as compliant. Install Microsoft Authenticator on devices accessing applications protected by Microsoft Entra ID.

Learn more: [Authentication methods in Microsoft Entra ID - Microsoft Authenticator app](../identity/authentication/concept-authentication-authenticator-app)

Important

To meet the phishing-resistant requirement: Manage only the devices accessing the protected application. Users allowed to use Microsoft Authenticator are in scope for Conditional Access policy requiring managed devices for access. A Conditional Access policy blocks access to the Microsoft Intune Enrollment Cloud App. Users allowed to use Microsoft Authenticator are in scope for this Conditional Access policy. Use the same group(s) to allow Microsoft Authenticator authentication in Conditional Access policies to ensure that users enabled for the authentication method are in scope for both policies. This Conditional Access policy prevents the most significant vector of phishing threats from malicious external actors. It also prevents malicious actor from phishing Microsoft Authenticator to register a credential, or join a device and enroll it in Intune to mark it as compliant.

Learn more:

- [Plan your Microsoft Entra hybrid join implementation](../identity/devices/hybrid-join-plan), or
- [How to: Plan your Microsoft Entra join implementation](../identity/devices/device-join-plan)
- See also, [Common Conditional Access policy: Require a compliant device, Microsoft Entra hybrid joined device, or multifactor authentication for all users](../identity/conditional-access/policy-alt-all-users-compliant-hybrid-or-mfa)

Note

Microsoft Authenticator isn't phishing-resistant. Configure Conditional Access policy to require that managed devices get protection from external phishing threats.

### Legacy

Federated identity providers (IdPs) such as Active Directory Federation Services (AD FS) configured with phishing-resistant method(s). While agencies achieve phishing resistance with federated IdP, it adds cost, complexity, and risk. Microsoft encourages the security benefits of Microsoft Entra ID an IdP, removing the associated risk of a federated IdP

Learn more:

- [Protecting Microsoft 365 from on-premises attacks](../architecture/protect-m365-from-on-premises-attacks)
- [Deploying AD Federation Services in Azure](/en-us/windows-server/identity/ad-fs/deployment/how-to-connect-fed-azure-adfs)
- [Configuring AD FS for user certificate authentication](/en-us/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication)

### Phishing-resistant method considerations

Your current device capabilities, user personas, and other requirements might dictate multi-factor methods. For example, FIDO2 security keys with USB-C support require devices with USB-C ports. Consider the following information when evaluating phishing-resistant multifactor authentication:

- **Device types and capabilities you can support**: kiosks, laptops, mobile phones, biometric readers, USB, Bluetooth, and near-field communication devices
- **Organizational user personas**: frontline workers, remote workers with and without company-owned hardware, administrators with privileged access workstations, and business-to-business guest users
- **Logistics**: distribute, configure, and register multifactor authentication methods such as FIDO2 security keys, smart cards, government-furnished equipment, or Windows devices with TPM chips
- **Federal Information Processing Standards (FIPS) 140 validation at an authenticator assurance level**: some FIDO security keys are FIPS 140 validated at levels for AAL3 set by NIST SP 800-63B
    - See, [Authenticator assurance levels](nist-about-authenticator-assurance-levels)
    - See, [NIST authenticator assurance level 3 by using Microsoft Entra ID](nist-authenticator-assurance-level-3)
    - Go to nist.gov for [NIST Special Publication 800-63B, Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html)

## Implementation considerations for phishing-resistant multifactor authentication

See the following sections for support of implementing phishing-resistant methods for application and virtual device sign-in.

### Application sign-in scenarios from various clients

The following table details the availability of phishing-resistant multifactor authentication scenarios, based on the device type that's used to sign in to the applications:

| Device | AD FS as a federated IdP with certificate authentication | Microsoft Entra certificate authentication | FIDO2 security keys | Windows Hello for Business | Microsoft Authenticator with Conditional Access policies enforcing Microsoft Entra hybrid join or compliant devices |
| --- | --- | --- | --- | --- | --- |
| Windows device | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | ![Checkmark with solid fill](media/memo-22-09/check.jpg) |
| iOS mobile device | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | Not applicable | Not applicable | ![Checkmark with solid fill](media/memo-22-09/check.jpg) |
| Android mobile device | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | Not applicable | Not applicable | ![Checkmark with solid fill](media/memo-22-09/check.jpg) |
| macOS device | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | ![Checkmark with solid fill](media/memo-22-09/check.jpg) | Edge/Chrome | Not applicable | ![Checkmark with solid fill](media/memo-22-09/check.jpg) |

Learn more: [Browser support for FIDO2 passwordless authentication](../identity/authentication/fido2-compatibility)

### Virtual device sign-in scenarios that require integration

To enforce phishing-resistant multifactor authentication, integration might be necessary. Enforce multifactor authentication for users accessing applications and devices. For the five phishing-resistant multifactor authentication types, use the same features to access the following device types:

| Target system | Integration actions |
| --- | --- |
| Azure Linux virtual machine (VM) | Enable the [Linux VM for Microsoft Entra sign-in](../identity/devices/howto-vm-sign-in-azure-ad-linux) |
| Azure Windows VM | Enable the [Windows VM for Microsoft Entra sign-in](../identity/devices/howto-vm-sign-in-azure-ad-windows) |
| Azure Virtual Desktop | Enable [Azure Virtual Desktop for Microsoft Entra sign-in](/en-us/azure/architecture/example-scenario/wvd/azure-virtual-desktop-azure-active-directory-join) |
| VMs hosted on-premises or in other clouds | Enable [Azure Arc](/en-us/azure/azure-arc/overview) on the VM and then enable Microsoft Entra sign-in. Currently in private preview for Linux. Support for Windows VMs hosted in these environments is on our roadmap. |
| Non-Microsoft virtual desktop solution | Integrate the virtual desktop solution as an app in Microsoft Entra ID |

### Enforcing phishing-resistant multifactor authentication

Use Conditional Access to enforce multifactor authentication for users in your tenant. With the addition of cross-tenant access policies, you can enforce it on external users.

Learn more: [Overview: Cross-tenant access with Microsoft Entra External ID](../external-id/cross-tenant-access-overview)

#### Enforcement across agencies

Use Microsoft Entra B2B collaboration to meet requirements that facilitate integration:

- Limit what other Microsoft tenants your users access
- Allow access to users you don't have to manage in your tenant, but enforce multifactor authentication and other access requirements

Learn more: [B2B collaboration overview](../external-id/what-is-b2b)

Enforce multifactor authentication for partners and external users who access organizational resources. This action is common in inter-agency collaboration scenarios. Use Microsoft Entra cross-tenant access policies to configure multifactor authentication for external users who access applications and resources.

Configure trust settings in cross-tenant access policies to trust the multifactor authentication method the guest user tenant uses. Avoid having users register a multifactor authentication method with your tenant. Enable these policies on a per-organization basis. You can determine the multifactor authentication methods in the user home tenant and decide if they meet phishing resistance requirements.

## Password policies

The memo requires organizations to change ineffective password policies, such as complex, rotated passwords. Enforcement includes removing the requirement for special characters and numbers, with time-based password rotation policies. Instead, consider the following options:

- **Password protection**to enforce a common list of weak passwords that Microsoft maintains
    - In addition, include custom banned passwords
    - See, [Eliminate bad passwords using Microsoft Entra Password Protection](../identity/authentication/concept-password-ban-bad)
- **Self-service password reset**to enable users to reset passwords, for instance after account recovery
    - [Tutorial: Enable users to unlock their account or reset passwords using Microsoft Entra self-service password reset](../identity/authentication/tutorial-enable-sspr)
- **Microsoft Entra ID Protection** for alerts about compromised credentials
- [What is risk?](../id-protection/concept-identity-protection-risks)

Although the memo isn't specific about policies to use with passwords, consider the standard from NIST 800-63B.

See, [NIST Special Publication 800-63B, Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html).