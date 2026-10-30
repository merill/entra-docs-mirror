---
layout: FAQ
title: Microsoft Entra ID Protection FAQ - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/id-protection-faq
summary: >
  <p>This article includes answers to frequently asked questions about Microsoft Entra ID Protection. FAQ sections include: detections, leaked credentials, remediation, licensing, and B2B users.</p>

  <p>For more information, see <a href="overview-identity-protection">Microsoft Entra ID Protection overview</a>.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Frequently asked questions around Microsoft Entra ID Protection.
ms.topic: faq
ms.date: 2026-03-17T00:00:00.0000000Z
ms.reviewer: etbasser
locale: en-us
document_id: 716c83af-0d73-2711-3ee7-ccdc9391e8d9
document_version_independent_id: 716c83af-0d73-2711-3ee7-ccdc9391e8d9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/id-protection-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/id-protection-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/id-protection-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 58e1346c-b25c-8f45-a7a9-32adde117d30
---

# Microsoft Entra ID Protection FAQ - Microsoft Entra ID Protection | Microsoft Learn

This article includes answers to frequently asked questions about Microsoft Entra ID Protection. FAQ sections include: detections, leaked credentials, remediation, licensing, and B2B users.

For more information, see [Microsoft Entra ID Protection overview](overview-identity-protection).

## Detections

### How can I simulate risk to understand why a user is getting flagged?

We have a guide for [how to simulate risk](howto-identity-protection-simulate-risk). This guide provides several options to simulating different types of risk. You can also use the [Conditional Access WhatIf](../identity/conditional-access/what-if-tool) tool to see how specific policies get applied. We also recommend turning on Conditional Access policies in **Report-Only** mode to understand how policies work in the tenant without affecting your users' ability to access the resources they need.

### I just received a high-risk alert but they aren't showing up in the "Impact analysis of risk-based policies" workbook. Why?

If the user is assigned high risk, but hasn't signed-in yet, you won't see them in this report. The report only uses sign-in logs to populate this data.

### What if incorrect credentials were used to attempt to sign-in?

ID Protection generates risk detections only when the correct credentials are used. If incorrect credentials are used on a sign-in, it doesn't represent risk of credential compromise.

### Is password hash synchronization required?

Risk detections like leaked credentials require the presence of password hashes for detection to occur. For more information about password hash synchronization, see [Implement password hash synchronization with Microsoft Entra Connect Sync](../identity/hybrid/connect/how-to-connect-password-hash-synchronization).

### Why are risk detections generated for disabled accounts?

First, it's important to know that user accounts in a disabled state can be reenabled. If the credentials of a disabled account are compromised, and the account gets re-enabled, bad actors might use those credentials to gain access. ID Protection generates risk detections for suspicious activities against these disabled accounts to alert customers about potential account compromise.

If an account is no longer in use and won't be reenabled, customers should consider deleting it to prevent compromise. No risk detections are generated for deleted accounts.

### I tried to sort the Risk detections report using the "Detection time" column, but it's not working.

Sorting by *Detection time* in the Risk detections report might not always give the correct result because of a known technical constraint. To sort by *Detection time*, open the report in the Microsoft Entra admin center and select **Download** to export the data as a CSV file and sort accordingly.

### Where does Microsoft find leaked credentials? How often are they processed?

Microsoft operates a large-scale credential scanning pipeline that continuously discovers compromised credentials across a broad range of sources, including:

- Dark web forums and underground marketplaces where stolen credentials are traded and sold.
- Breach dump repositories and public paste sites where bad actors post stolen credential sets.
- Law enforcement agencies that share credential databases seized during investigations.
- Microsoft Threat Intelligence Center (MSTIC), with research teams dedicated to tracking threat actors.
- Microsoft Digital Crimes Unit (DCU), which disrupts cybercriminal infrastructure and recovers stolen data.
- Industry partner intelligence sharing and collaboration with security researchers.

### How does the leaked credentials detection work?

When new leaked credentials are discovered from any source, they're ingested into the Microsoft leaked credentials service and processed in multiple batches per day. The service receives the actual credential pair — including password material — and validates it against your tenant's current valid password hashes. This direct credential validation is what makes the detection high fidelity. A detection is only emitted when the discovered credential is confirmed to match a user's current password. Plaintext passwords aren't stored at any point, and all discovered credential data is deleted shortly after processing.

When a match is confirmed, ID Protection flags the affected user with **high** risk because the detection represents verified credential exposure, not a heuristic or probabilistic signal. Risk-based Conditional Access policies can then automatically require a secure password change before the compromised credential can be exploited. A cloud-based password reset through Microsoft Entra fully remediates the user risk for this detection. Microsoft Defender for Identity now also surfaces leaked credentials detections for on-premises passwords. For more information, see [Accounts security posture assessments](/en-us/defender-for-identity/security-posture-assessments/accounts#change-password-for-on-premises-account-with-potentially-leaked-credentials-preview).

The leaked credentials detection requires [password hash synchronization](../identity/hybrid/connect/how-to-connect-password-hash-synchronization) to be enabled for hybrid users. Only credentials discovered **after** PHS is enabled are matched against your tenant. Previously found credential pairs aren't retroactively checked.

### Why am I not seeing any leaked credentials?

Leaked credentials are processed anytime Microsoft finds a new, publicly available batch. Because of the sensitive nature, the leaked credentials are deleted shortly after processing. Only new leaked credentials found **after** you enable password hash synchronization (PHS) are processed against your tenant. Verifying against previously found credential pairs isn't done.

To see how leaked credentials could appear in ID Protection for your tenant, try simulating leaked credentials in GitHub for Workload Identities. For more information, see [Simulate risk detections in Microsoft Entra ID Protection](howto-identity-protection-simulate-risk#leaked-credentials-for-workload-identities).

If you don't see any leaked credential risk events, it is because of the following reasons:

- You don't have password hash sync enabled for your tenant.
- Microsoft didn't find any leaked credential pairs that match your users.

## Remediation

### When does ID Protection autoremediate sign-in risk without a risk-based policy in place?

ID Protection autoremediates sign-in risk when the user immediately provides a second factor, such as multifactor authentication (MFA) following their risky sign-in. Providing this second factor composes a strong authentication.

ID Protection also operates two models for risk assessment on sign-ins. The first is the real-time model that uses limited information to make a fast determination during the sign-in. Second is an offline model that uses other sign-in data once the sign-in is complete. The offline model can close risk when it reassesses the risk score as safe. This assessment applies to real-time and offline detections of any risk level.

### When does ID Protection autoremediate user risk without a risk-based policy in place?

ID Protection autoresolves users with low user risk after six months without elevation of user risk. Risky users with medium or high risk aren't autoresolved without a risk policy or admin dismissal.

### What if I use a non-Microsoft provider for multifactor authentication?

If you don't use Microsoft Entra multifactor authentication, you might still see sign-in risk remediated in your environment if you use a non-Microsoft MFA provider. [External authentication methods](/en-us/entra/identity/authentication/how-to-authentication-external-method-manage) make it possible to remediate risk when using a non-Microsoft MFA provider.

### What if I use federation authentication?

Even if you configure federation authentication, risk-based Conditional Access operates at the authorization layer and remains effective. If you use Microsoft Entra ID for multifactor authentication, the remediation action of MFA is triggered as usual by Microsoft Entra ID. If MFA is configured on the authentication provider side of the federation, you can use the **Federated multifactor** factor of [authentication strengths](../identity/authentication/concept-authentication-strengths) as a remediation action.

### What if I haven't rolled out multifactor authentication to end users yet?

We strongly recommend rolling out MFA as a first step. If MFA can't be implemented immediately, apply controls to [block high-risk users](howto-identity-protection-configure-risk-policies) as a mitigation measure.

### What are the best Conditional Access controls for accounts that are passwordless?

Check out our guidance on deploying phishing-resistant passwordless authentication: [Get started with a phishing-resistant passwordless authentication deployment](../identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)

### Should we add "Enforce sign-in frequency - Every time" to our Conditional Access policies for high risk?

This setting depends on your organization's risk tolerance. Some organizations might choose to block high risk. Enforcing sign-in every time can lead to sign-in or MFA fatigue, which can increase the chance of a phishing attack.

We also recommend turning on Conditional Access policies in **Report-Only** mode to understand how policies work in the tenant without affecting your users' ability to access the resources they need. You can also check the [**Impact analysis of risk-based policies** workbook](workbook-risk-based-policy-impact) in ID Protection.

### What if I am in a hybrid environment?

User risk can be self-remediated using a secure password change (MFA + password change). This flow doesn't require self-service password reset (SSPR) to be enabled; however, for hybrid users with on-premises or hybrid-joined Windows devices, password hash synchronization must be enabled. Consider enabling [allow on-premises password change to reset user risk](howto-identity-protection-remediate-unblock#allow-on-premises-password-reset-to-remediate-user-risks) so that on-premises password changes also remediate user risk.

For more information, see [How to remediate risk and unblock users](howto-identity-protection-remediate-unblock#considerations-for-cloud-and-hybrid-users).

### If I deploy a risk policy, will the system autoremediate users differently or do I need to redo past remediations?

The system relies on the grant controls specified in the Conditional Access policy for all remediation. This policy-driven approach gives you more control over access to resources. If the user risk policy requires a block, Conditional Access enforces that. If the sign-in risk policy requires MFA, Conditional Access enforces a new MFA challenge (when there's no MFA claim on an existing token). So, if Alice always had her risky sign-ins autoremediated thanks to another MFA policy, nothing changes in her user experience when you deploy a risk policy that requires MFA.

## Licensing

### What license do I need to use Microsoft Entra ID Protection?

There are several capabilities in Microsoft Entra ID Protection that require different licenses. For example, you can get limited information in the risky sign-ins report with the Microsoft Entra ID Free license, but you get full access to these reports with the Microsoft Entra ID P2 or the Microsoft Entra Suite license. For more information, see [Microsoft Entra ID Protection license requirements](overview-identity-protection#license-requirements).

Microsoft Entra ID Protection also uses signals from Microsoft Defender products that are licensed separately. For more information, see [What is Microsoft Entra ID Protection?](overview-identity-protection#microsoft-defender).

## B2B users

### Why can't I remediate risky B2B collaboration users in my directory?

The risk evaluation and remediation for B2B users occurs in their home directory, so the guest users don't appear in the risky users report in the resource directory. Admins in the resource directory can't force a secure password change for these users.

### What do I do if a B2B collaboration user was blocked due to a risk-based policy in my organization?

If a risky B2B user in your directory is blocked by your risk-based policy, the user needs to remediate that risk in their home directory. Users can remediate their risk by performing a secure password change (MFA + password change) in their home directory. This flow doesn't require self-service password reset (SSPR) to be enabled. If the user can't complete a secure password change, they need to contact their own organization's IT Staff to have an administrator manually dismiss their risk or change their password. For more information, see [Remediate user risk](howto-identity-protection-remediate-unblock).

### How do I prevent risk-based policies from affecting B2B collaboration users?

Excluding B2B users from your organization's risk-based Conditional Access policies prevents B2B users from being affected by risk evaluation. To exclude these B2B users, create a group in Microsoft Entra ID that contains all of your organization's guest users. Then, add this group as an exclusion for your built-in ID Protection user risk and sign-in risk policies, and any Conditional Access policies that use sign-in risk as a condition.