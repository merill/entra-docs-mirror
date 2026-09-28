---
layout: Conceptual
title: Investigate risk with Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/howto-identity-protection-investigate-risk
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn how to investigate risky users, detections, and sign-ins in Microsoft Entra ID Protection.
ms.topic: how-to
ms.date: 2026-05-27T00:00:00.0000000Z
ms.reviewer: lvandenende
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5779b726-83b3-3242-297a-17410b372ab5
document_version_independent_id: ff902d75-e5b4-25db-4d31-80d28808efff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/howto-identity-protection-investigate-risk.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/howto-identity-protection-investigate-risk
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/howto-identity-protection-investigate-risk.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ebdf2cf4-fc1c-981c-3951-eae31f9c828d
---

# Investigate risk with Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn

Microsoft Entra ID Protection provides several [risk reports](concept-risk-reports) that can be used to investigate identity risks in your environment. Investigation of events is key to better understanding and identifying any weak points in your security strategy. ID Protection reports can be archived for storage or integrated with Security Information and Event Management (SIEM) tools for further analysis. Organizations can also take advantage of Microsoft Defender, Microsoft Sentinel, and Microsoft Graph API integrations to aggregate data with other sources.

There are many ways to investigate risk in your environment and even more details to consider during your investigation. This article provides a framework to help you get started and outlines some of the most common scenarios and recommended actions.

## Prerequisites

- [Microsoft Entra ID P2 or Microsoft Entra Suite license](overview-identity-protection) is required for full access to Microsoft Entra ID Protection features.
- [Global Reader](../identity/role-based-access-control/permissions-reference#global-reader) is the least privileged role required to **view the risk reports**.
- [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader) is the least privileged role required to **view the sign-in and audit logs**.

## Initial triage

When starting the initial triage, we recommend the following actions:

1. Review the [ID Protection dashboard](id-protection-dashboard) to visualize number of attacks, number of high risk users, and other important metrics based on detections in your environment.
2. Review the [risk reports](concept-risk-reports) to examine the details of any recent risky users, sign-ins, or detections.
3. Review the [Impact analysis workbook](workbook-risk-based-policy-impact) to understand the scenarios where risk is evident in your environment and what risk-based access policies should be enabled to manage high-risk users and sign-ins.
4. Review the [sign-in logs](../identity/monitoring-health/concept-sign-ins) to identify similar activities with the same characteristics. This activity could be an indication of more compromised accounts.

    1. If there are common characteristics, like IP address, geography, success/failure, etc., consider blocking them with a Conditional Access policy.
    2. Review which resources might be compromised, including potential data downloads or administrative modifications.
    3. Enable [self-remediation policies through Conditional Access](howto-identity-protection-configure-risk-policies).
5. With [Insider Risk Management through Microsoft Purview](/en-us/purview/insider-risk-management), you can check to see if the user performed other risky activities, such as downloading a large volume of files from a new location. This behavior is a strong indication of a possible compromise.

If you suspect an attacker can impersonate the user, you should require the user to reset their password and perform MFA or block the user and revoke all refresh and access tokens.

## Investigation and risk remediation framework

Organizations can use the following framework to investigate suspicious activity. When risk is detected, the recommended first step is self-remediation, if it's an option. Self-remediation can take place through self-service password reset or through remediation flow of a [risk-based Conditional Access policy](howto-identity-protection-configure-risk-policies).

If self-remediation isn't an option, an administrator needs to remediate the risk. Remediation is done by invoking a password reset, requiring user to reregister for MFA, blocking the user, or revoking user sessions. The following flow chart shows the recommended flow once a risk is detected:

[![Diagram showing the risk remediation flow.](media/howto-identity-protection-investigate-risk/risk-remediation-flow.png)](media/howto-identity-protection-investigate-risk/risk-remediation-flow.png#lightbox)

Once the risk is contained, more investigation might be required to mark the risk as safe, compromised, or to dismiss it.

1. Check the sign-in logs and validate whether the activity is normal for the given user.

    1. Look at the user's past activities including the following properties to see if they're normal for the given user.
        - Application - Is the app commonly used by the user?
        - Device - Is the device registered or compliant?
        - Location - Is the user traveling to a different location or accessing devices from multiple locations?
        - IP address
        - **User agent string**
2. Investigate using other security tools, where available.

    - If you have [Microsoft Sentinel](/en-us/azure/sentinel/overview), check for corresponding alerts that might indicate a larger issue.
    - If you have [Microsoft Defender XDR](/en-us/defender-for-identity/understanding-security-alerts), you can follow a user risk event through other related alerts and incidents.
    - The MITRE ATT&CK chain through Microsoft Sentinel in Microsoft Defender XDR might also provide insights. In the [Microsoft Defender portal](https://security.microsoft.com), browse to **Incidents & alerts** &gt; **Alerts** &gt; and set the **Product name** filter to **AAD Identity Protection** to find alerts from Microsoft Entra ID Protection.
3. Contact the user to confirm if they recognize the sign-in; however, keep in mind that email or Teams might be compromised.

    1. Confirm the information you have such as:
        - Timestamp
        - Application
        - Device
        - Location
        - IP address
4. Depending on the results of the investigation, mark the user or sign-in as confirmed compromised, confirmed safe, or dismiss the risk. You can confirm compromise in the Microsoft Entra admin center or [programmatically using Microsoft Graph](howto-identity-protection-simulate-risk#confirm-compromise-using-microsoft-graph).
5. [Set up risk-based Conditional Access policies](howto-identity-protection-configure-risk-policies#enable-policies) to prevent similar attacks or to address any gaps in coverage.

## Investigate specific detections

Certain risk detections require specific investigation steps. The following sections outline some of the most common risk detections and recommended actions.

### Microsoft Entra threat intelligence

To investigate a Microsoft Entra threat intelligence risk detection, follow these steps based on the information provided in the "additional info" field of the Risk Detection Details pane:

- If the sign-in was from a suspicious IP Address:

    1. Confirm if the IP address shows suspicious behavior in your environment.
    2. Does the IP generate a high number of failures for a user or set of users in your directory?
    3. Is the traffic of the IP coming from an unexpected protocol or application, for example Exchange legacy protocols?
    4. If the IP address corresponds to a cloud service provider, rule out that there are no legitimate enterprise applications running from the same IP.
- Account was the victim of a password spray attack

    1. Validate that no other users in your directory are targets of the same attack.
    2. Determine if other users have sign-ins with similar atypical patterns seen in the detected sign-in within the same time frame. Password spray attacks might display unusual patterns in:
        - User agent string
        - Application
        - Protocol
        - Ranges of IPs/ASNs
        - Time and frequency of sign-ins
- Detection was triggered by a real-time rule

    1. Validate that no other users in your directory are targets of the same attack. This information can be found using the TI\_RI\_#### number assigned to the rule.
    2. Real-time rules protect against novel attacks identified by Microsoft's threat intelligence research. If multiple users in your directory were targets of the same attack, investigate unusual patterns in other attributes of the sign in.

### Atypical travel detections

- If you confirm the activity was *not*performed by a legitimate user:
    1. Mark the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.
    2. Block the user if attacker has access to reset password or perform MFA and reset password.
- If a user is known to use the IP address in the scope of their duties, confirm sign-in as safe.
- If you confirm that the user recently traveled to the destination mentioned detailed in the alert, confirm sign-in as safe.
- If you confirm that the IP address range is from a sanctioned VPN, confirm sign-in as safe and add the VPN IP address range to named locations in Microsoft Entra ID and Microsoft Defender for Cloud Apps.

### Anomalous token and token issuer anomaly detections

- If you confirm that the activity was *not* performed by a legitimate user using a combination of risk alert, location, application, IP address, User Agent, or other characteristics that are unexpected for the user:

    1. Mark the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.
    2. Block the user if an attacker has access to reset password or perform.
    3. [Set up risk-based Conditional Access policies](howto-identity-protection-configure-risk-policies#enable-policies) to require password reset, perform MFA, or block access for all high-risk sign-ins.
- If you confirm location, application, IP address, User Agent, or other characteristics are expected for the user and there aren't other indications of compromise, allow the user to self-remediate with a risk-based Conditional Access policy or have an admin confirm sign-in as safe.

For further investigation of token based detections, see the blog post [Token tactics: How to prevent, detect, and respond to cloud token theft](https://www.microsoft.com/security/blog/2022/11/16/token-tactics-how-to-prevent-detect-and-respond-to-cloud-token-theft) the [Token theft investigation playbook](/en-us/security/operations/token-theft-playbook).

### Suspicious browser detections

This detection indicates the user doesn't commonly use the browser or activity within the browser doesn't match the user's normal behavior.

- Confirm the sign-in as compromised, and invoke a password reset if not already performed by self-remediation. Block the user if an attacker has access to reset password or perform MFA.
- [Set up risk-based Conditional Access policies](howto-identity-protection-configure-risk-policies#enable-policies) to require password reset, perform MFA, or block access for all high-risk sign-ins.

### Malicious IP address detections

- If you confirm that the activity was *not* performed by a legitimate user:

    1. Confirm the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.
    2. Block the user if an attacker has access to reset password or perform MFA and reset password and revoke all tokens.
    3. [Set up risk-based Conditional Access policies](howto-identity-protection-configure-risk-policies#enable-policies) to require password reset or perform MFA for all high-risk sign-ins.
- If you confirm the user *does* use the IP address in the scope of their duties, confirm the sign-in as safe.

### Password spray detections

A password spray detection means Microsoft observed an attacker conducting a spray attack and achieving a successful credential validation against a user in your tenant. The spray attack might have targeted users across many tenants — the detection fires only in tenants where a successful password match was confirmed. Unsuccessful spray attempts don't generate a detection.

- If you confirm that the activity was *not* performed by a legitimate user:

    1. Mark the sign-in as compromised, and invoke a password reset if not already performed by self-remediation.
    2. Block the user if an attacker has access to reset password or perform MFA and reset password and revoke all tokens.
- If you confirm the user *does* use the IP address in the scope of their duties, confirm the sign-in as safe.
- If you confirm that the account isn't compromised and see no brute force or password spray indicators against the account:

    1. Allow the user to self-remediate with a risk-based Conditional Access policy or have an admin confirm sign-in as safe.
    2. Ensure you have [Microsoft Entra smart lockout](../identity/authentication/howto-password-smart-lockout) configured appropriately to avoid unnecessary account lockouts.

For further investigation of password spray risk detections, see the article [Password spray investigation](/en-us/security/operations/incident-response-playbook-password-spray).

### Leaked credentials detections

Leaked credentials detections are always high risk because they represent confirmed credential exposure. When this detection fires, investigate right away.

If this detection identified a leaked credential for a user:

1. **Assess the scope of exposure.** Review the user's risk history and sign-in logs to determine if the leaked credential was used for unauthorized access. Look for correlated sign-in risk events such as sign-ins from unfamiliar locations, anonymous IP addresses, or atypical travel.
2. **Check if the password was already changed.** Verify whether the user changed their password after the date the leak was detected. A cloud-based password reset triggered by a [Microsoft Entra Conditional Access policy](howto-identity-protection-configure-risk-policies#user-risk-policy-in-conditional-access) fully remediates the user risk for this detection. If the password was changed, the risk might already be self-remediated. If not, confirm the user as compromised and initiate a password reset.
3. **Block access if an attacker is active.** If sign-in logs show unauthorized access, or if an attacker has the ability to reset the password or perform MFA, block the user, reset the password, and revoke all refresh tokens. Revoking sessions is critical when there's evidence of active compromise.
4. **Review for lateral movement.** Check the user's recent activity for signs of privilege escalation, new app registrations, mailbox rule changes, or access to sensitive resources that might indicate post-compromise activity.
5. **Verify connected accounts.** If the user reuses passwords across services, consider the credential compromised beyond your tenant. Advise the user to change passwords on other services where they use the same credential.

## Mitigate future risks

- Add corporate VPNs and IP address ranges to [named locations](../identity/conditional-access/concept-assignment-network) in your Conditional Access policies to reduce false positives.
- Consider creating a known traveler database for updated organizational travel reporting and use it to cross-reference travel activity.
- [Provide feedback in ID Protection](howto-identity-protection-risk-feedback) to improve detection accuracy and reduce false positives.