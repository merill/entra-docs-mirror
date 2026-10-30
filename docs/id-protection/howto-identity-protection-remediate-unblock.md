---
layout: Conceptual
title: Remediate risks and unblock users - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/howto-identity-protection-remediate-unblock
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn how to configure user self-remediation and manually remediate risky users in Microsoft Entra ID Protection.
ms.topic: how-to
ms.date: 2026-05-15T00:00:00.0000000Z
ms.reviewer: ebasseri
locale: en-us
document_id: bff3e81f-1107-2b97-8ae1-c85cf2314c95
document_version_independent_id: 63d5a109-a072-4442-972c-87a5f6bc35bd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/howto-identity-protection-remediate-unblock.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/howto-identity-protection-remediate-unblock
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/howto-identity-protection-remediate-unblock.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 13b33749-3a11-db48-597a-a491cbc5f073
---

# Remediate risks and unblock users - Microsoft Entra ID Protection | Microsoft Learn

After completing your [risk investigation](howto-identity-protection-investigate-risk), you need to take action to remediate risky users or unblock them. You can set up [risk-based policies](howto-identity-protection-configure-risk-policies) to enable automatic remediation or manually update the user's risk status. Microsoft recommends acting quickly because time matters when working with risks.

This article provides several options for automatically and manually remediating risks and covers scenarios when users were blocked because of user risk, so you know how to unblock them.

## Prerequisites

- The Microsoft Entra ID P2 or Microsoft Entra Suite license is required for full access to Microsoft Entra ID Protection features.
    - For a detailed list of capabilities for each license tier, see [What is Microsoft Entra ID Protection](overview-identity-protection).
- The [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator) role is the least privileged role required to **reset passwords**.
- The [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator) role is the least privileged role required to **dismiss user risk**.
- The [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) role is the least privileged role required to **create or edit risk-based policies**.
- The [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role is the least privileged role required to **create or edit Conditional Access policies**.

## Password change vs. self-service password reset (SSPR)

This article distinguishes between two different password change flows:

- **Password change (risk remediation)**: The user knows their current password, authenticates with multifactor authentication (MFA), and then changes their password. This is the mechanism used by risk-based Conditional Access policies, including the **Require password change** and **Require risk remediation** grant controls. This flow doesn't use self-service password reset (SSPR).
- **Password reset (SSPR / recovery)**: The user doesn't know their password and uses self-service password reset (SSPR) or an admin-initiated reset to recover access. This flow is intended for account recovery. A password reset through SSPR also remediates user risk.

## How risk remediation works

All active risk detections contribute to the calculation of the user's risk level, which indicates the probability that the user's account is compromised. Depending on the risk level and your tenant's configuration, you might need to investigate and address the risk. You can allow users to self-remediate their sign-in and user risks by setting up [risk-based policies](howto-identity-protection-configure-risk-policies). If users pass the required access control, such as multifactor authentication or secure password change, then their risks are automatically remediated.

If a risk-based policy is applied during sign-in where the criteria aren't met, the user is blocked. This block occurs because the user can't perform the required step, so admin intervention is required to unblock the user.

Risk-based policies are configured based on risk levels and only apply if the risk level of the sign-in or user matches the configured level. Some detections might not raise risk to the level where the policy applies, so administrators need to handle those situations manually. Administrators can determine that extra measures are necessary, such as [blocking access from locations](../identity/conditional-access/policy-block-by-location) or lowering the acceptable risk in their policies.

## End user self-remediation

When risk-based Conditional Access policies are configured, remediating user risk and sign-in risk can be a self-service process for users. This self-remediation allows users to resolve their own risks without needing to contact the help desk or an administrator. As an IT administrator, you might not need to take any action to remediate risks, but you do need to know how to configure the policies that allow self-remediation and what to expect to see in the related reports. For more information, see:

- [Configure and enable risk policies](howto-identity-protection-configure-risk-policies)
- [Self-remediation experience with Microsoft Entra ID Protection and Conditional Access](concept-identity-protection-user-experience)
- [Require multifactor authentication for all users](../identity/conditional-access/policy-all-users-mfa-strength)
- [Implement password hash sync](../identity/hybrid/connect/how-to-connect-password-hash-synchronization)

### Self-remediation of sign-in risk

If a user's sign-in risk reaches the level set by your risk-based policy, the user is prompted to perform multifactor authentication (MFA) to remediate sign-in risk. If they successfully complete the MFA challenge, the sign-in risk is remediated. The risk state and risk details for the user, sign-ins, and corresponding risk detections are updated as follows:

- Risk state: "At risk" -&gt; "Remediated"
- Risk detail: "-" -&gt; "User passed multifactor authentication"

Sign-in risks that aren't remediated impact the user risk, so having risk-based policies in place allows users to self-remediate their sign-in risk, so their user risk isn't affected.

### Self-remediation of user risk

When a user risk policy with the **Require password change** grant control is configured, the user is prompted to perform a secure password change as shown in the [Microsoft Entra ID Protection user experience](concept-identity-protection-user-experience) article. The user must first complete multifactor authentication and then change their password. This process doesn't use the self-service password reset (SSPR) flow. Once the password is changed, the user risk is remediated and the user can proceed to sign in with their new password. The risk state and risk details for the user, sign-ins, and corresponding risk detections are updated as follows:

- Risk state: "At risk" -&gt; "Remediated"
- Risk detail: "-" -&gt; "User performed secured password reset"

Note

The risk detail value "User performed secured password reset" is a system-reported label. Despite the name, this value indicates the user completed a secure password change (MFA + password change), not a self-service password reset flow.

#### Considerations for cloud and hybrid users

- Both cloud and hybrid users can complete a secure password change only if they can perform MFA. For users that aren't registered, this option isn't available.
- Hybrid users can complete a password change from an on-premises or hybrid joined Windows device, when password hash synchronization and the Allow on-premises password change to reset user risk setting is enabled.

## System-based remediation

In some cases, Microsoft Entra ID Protection can also automatically dismiss a user's risk state. Both the risk detection and the corresponding risky sign-in are identified by ID Protection as no longer posing a security threat. This automatic intervention can happen if the user provides a second factor, such as multifactor authentication (MFA) or if the real-time and offline assessment determines that the sign-in is no longer risky. This automatic remediation reduces noise in risk monitoring so you can focus on the things that require your attention.

- **Risk state**: "At risk" -&gt; "Dismissed"
- **Risk detail**: "-" -&gt; "Microsoft Entra ID Protection assessed sign-in safe"

### Threat-informed remediation by Microsoft

In limited cases, Microsoft Threat Intelligence identifies accounts, sessions, or resources being actively used in attack campaigns targeting Microsoft Entra tenants. When Microsoft has high-confidence evidence of compromise that poses an active risk to your organization, Microsoft might take remediation action on your behalf to help contain the threat.

These actions are recorded in the Microsoft Entra audit logs with *Microsoft* listed as the initiator. Administrators retain full control of their tenant and can reverse any action taken through this process after completing their own investigation.

## Administrator manual remediation

Some situations require an IT administrator to manually remediate sign-in or user risk. If you don't have risk-based policies configured, if the risk level doesn't meet the criteria for self-remediation, or if time is of the essence, you might need to take one of the following actions:

- Generate a temporary password for the user.
- Require the user to change their password.
- Dismiss the user's risk.
- Confirm the user is compromised and take action to secure the account.
- Unblock the user.

### Generate a temporary password

By generating a temporary password, you can immediately bring an identity back into a safe state. This method requires contacting the affected users because they need to know what the temporary password is. Because the password is temporary, the user is prompted to change the password to something new during the next sign-in.

To generate a temporary password:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).

    - To generate a temporary password from the user's details, you need the [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator) role.
    - To generate a temporary password from ID Protection, you need both the [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator) and [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator) roles.
    - Security Operator is required to access ID Protection and User Administrator is required to reset passwords.
2. Browse to **Protection** &gt; **Identity Protection** &gt; **Risky users**, and select the affected user.

    - Alternatively, browse to **Users** &gt; **All users**, and select the affected user.
3. Select **Reset password**.

    [![Screenshot of the Risky User Details panel with reset password highlighted.](media/howto-identity-protection-remediate-unblock/risky-user-details.png)](media/howto-identity-protection-remediate-unblock/risky-user-details.png#lightbox)
4. Review the message and select **Reset password** again.

    [![Screenshot of the second reset password button.](media/howto-identity-protection-remediate-unblock/reset-password.png)](media/howto-identity-protection-remediate-unblock/reset-password.png#lightbox)
5. Provide the temporary password to the user. The user must change their password the next time they sign-in.

The risk state and risk details for the user, sign-ins, and corresponding risk detections are updated as follows:

- Risk state: "At risk" -&gt; "Remediated"
- Risk detail: "-" -&gt; "Admin generated temporary password for user"

#### Considerations for cloud and hybrid users

Pay attention to the following considerations when generating a temporary password for cloud and hybrid users:

- You can generate passwords for cloud and hybrid users in the Microsoft Entra admin center.
- You can generate passwords for hybrid users from your on-premises directory if the following settings are in place:
    - Enable password hash synchronization, including the PowerShell script in the [Synchronizing temporary passwords](../identity/hybrid/connect/how-to-connect-password-hash-synchronization) section.
    - Enable the Allow on-premises password change to reset user risk setting in Microsoft Entra ID Protection.
    - Enable [Self-service password reset](../identity/authentication/tutorial-enable-sspr).
    - In Active Directory, only select the option **User must change password at next logon** after you enable everything in the previous bullets.

### Require a password change

You can require risky users to change their password to remediate their risk. Because these users aren't prompted to change their password through a risk-based policy, you must contact them to change their password. How the password is changed depends on the type of user:

- **Cloud users and hybrid users with Microsoft Entra-joined devices**: Perform a secure password change after a successful MFA sign-in. Users must already be registered for MFA.
- **Hybrid users with on-premises or hybrid-joined Windows devices**: Perform a secure password change through the Ctrl-Alt-Delete screen on their Windows device.
    - The Allow on-premises password change to reset user risk setting must be enabled.
    - If the **User must change password at next logon** setting is enabled in Active Directory, the user is prompted to change their password the next time they sign in. This option is available only if the settings in the Considerations for cloud and hybrid users section are in place.

The risk state and risk details for the user, sign-ins, and corresponding risk detections are updated as follows:

- Risk state: "At risk" -&gt; "Remediated"
- Risk detail: "-" -&gt; "User performed secure password change"

### Dismiss risk

If after investigation, you confirm the sign-in or user account isn't at risk of being compromised, you can dismiss the risk.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator).
2. Browse to **Protection** &gt; **Identity Protection** &gt; **Risky sign-ins** or **Risky users**, and select the risky activity.
3. Select **Dismiss risky sign-in(s)** or **Dismiss user risk**.

Because this method doesn't change the user's existing password, it doesn't bring their identity back into a safe state. You might still need to contact the user to inform them of the risk and advise them to change their password.

The risk state and risk details for the user, sign-ins, and corresponding risk detections are updated as follows:

- Risk state: "At risk" -&gt; "Dismissed"
- Risk detail: "-" -&gt; "Admin dismissed risk for sign-in" or "Admin dismissed all risk for user"

### Confirm a user to be compromised

If after investigation, you confirm that the sign-in or user *is* at risk, you can manually confirm an account is compromised:

1. Select the event or user in the **Risky sign-ins** or **Risky users** reports and choose **Confirm compromised**.
2. If a risk-based policy wasn't triggered, and the risk wasn't self-remediated using one of the methods described in this article, then take one or more of the following actions:
    1. Request a password change.
    2. Block the user if you suspect the attacker can reset the password or do multifactor authentication for the user.
    3. [Revoke refresh tokens](/en-us/entra/identity/users/users-revoke-access).
    4. [Disable any devices](../identity/devices/manage-device-identities) that are considered compromised.
    5. If using [continuous access evaluation](../identity/conditional-access/concept-continuous-access-evaluation), revoke all access tokens.

The risk state and risk details for the user, sign-ins, and corresponding risk detections are updated as follows:

- Risk state: "At risk" -&gt; "Confirmed compromised"
- Risk detail: "-" -&gt; "Admin confirmed user compromised"

For more information about what happens when confirming compromise, see [How to give feedback on risks](howto-identity-protection-risk-feedback#how-to-give-risk-feedback-in-microsoft-entra-id-protection).

### Unblock users

Risk-based policies can be used to block accounts to protect your organization from compromised accounts. You should investigate these scenarios to determine how to unblock the user and then determine why the user was blocked.

#### Sign in from a familiar location or device

Sign-ins are often blocked as suspicious if the sign-in attempt appears to come from an unfamiliar location or device. Your users can sign-in from a familiar location or device to try and unblock the sign-in. If the sign-in is successful, Microsoft ID Protection automatically remediates the sign-in risk.

- Risk state: "At risk" -&gt; "Dismissed"
- Risk detail: "-" -&gt; "Microsoft Entra ID Protection assessed sign-in safe"

#### Exclude the user from policy

If you think the current configuration of your sign-in or user risk policy is causing issues for *specific* users, you can exclude the users from the policy. You need to confirm that it's safe to grant access to these users without applying this policy to them. For more information, see [How To: Configure and enable risk policies](howto-identity-protection-configure-risk-policies#policy-exclusions).

You might need to manually dismiss the risk or user so they can sign in.

#### Disable the policy

If you think that your policy configuration is causing issues for *all* users, you can disable the policy. For more information, see [How To: Configure and enable risk policies](howto-identity-protection-configure-risk-policies).

You might need to manually dismiss the risk or user so they can sign in before addressing the policy.

#### Automatic blocking due to high confidence risk

Microsoft Entra ID Protection automatically blocks sign-ins that have a very high confidence of being risky. This block most commonly occurs on sign-ins performed using legacy authentication protocols or displaying properties of a malicious attempt. When a user is blocked for either scenario, they receive a 50053 authentication error. The sign-in logs display the following block reason: "Sign-in was blocked by built-in protections due to high confidence of risk."

To unblock an account based on high confidence sign-in risk, you have the following options:

- **Add the IPs being used to sign in to the Trusted location settings**: If the sign-in is performed from a known location for your company, you can add the IP to the trusted list. For more information, see [Conditional Access: Network assignment](../identity/conditional-access/concept-assignment-network#trusted-locations).
- **Use a modern authentication protocol**: If the sign-in is performed using a legacy protocol, switching to a modern method unblocks the attempt.

## Allow on-premises password reset to remediate user risks

If your organization has a hybrid environment, you can allow on-premises password changes to reset user risks with [password hash synchronization](../identity/hybrid/connect/whatis-phs). You must enable password hash synchronization *before* users can self-remediate in those scenarios.

- Risky hybrid users can self-remediate without administrator intervention. When the user changes their password on-premises, user risk is automatically remediated within Microsoft Entra ID Protection, resetting the current user risk state.
- Organizations can proactively deploy [user risk policies that require password changes](howto-identity-protection-configure-risk-policies#user-risk-policy-in-conditional-access) to protect their hybrid users. This option strengthens your organization's security posture and simplifies security management by ensuring that user risks are promptly addressed, even in complex hybrid environments.

Note

Allowing on-premises password change to remediate user risk is an opt-in only feature. Customers should evaluate this feature before enabling it in production environments. We recommend customers secure the on-premises password change process. For example, require multifactor authentication before allowing users to change their password on-premises using a tool like [Microsoft Identity Manager's Self-Service Password Reset Portal](/en-us/microsoft-identity-manager/working-with-self-service-password-reset).

To configure this setting:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Operator](../identity/role-based-access-control/permissions-reference#security-operator).
2. Browse to **Protection** &gt; **Identity Protection** &gt; **Settings**.
3. Check the box to **Allow on-premises password change to reset user risk** and select **Save**.

[![Screenshot showing the location of the Allow on-premises password change to reset user risk checkbox.](media/howto-identity-protection-remediate-unblock/allow-on-premises-password-reset-user-risk.png)](media/howto-identity-protection-remediate-unblock/allow-on-premises-password-reset-user-risk.png#lightbox)

## Deleted users

If a user was deleted from the directory that had a risk present, that user still appears in the risk report even though the account was deleted. Administrators can't dismiss risk for users who were deleted from the directory. To remove deleted users, open a Microsoft support case.

## Token theft related detections

With a recent update to our detection architecture, we no longer autoremediate sessions with MFA claims when a token theft related or the Verified threat actor IP detection triggers during sign-in.

The following ID Protection detections that identify suspicious token activity or the Verified threat actor IP detection are no longer auto-remediated:

- Microsoft Entra threat intelligence
- Anomalous token
- Attacker in the Middle
- Verified threat actor IP
- Token issuer anomaly

ID Protection now surfaces session details in the Risk Detection Details pane for detections that emit sign-in data. This change ensures we don't close sessions containing detections where there's MFA-related risk. Providing session details with user-level risk details provides valuable information to assist with investigation. This information includes:

- Token Issuer type
- Sign-in time
- IP address
- Sign-in location
- Sign-in client
- Sign-in request ID
- Sign-in correlation ID

If you have user risk-based Conditional Access policies configured and one of these detections that denotes suspicious token activity is fired on a user, the end user is required to perform secure password change and reauthenticate their account with multifactor authentication to clear the risk.

## PowerShell preview

Using the Microsoft Graph PowerShell SDK Preview module, organizations can manage risk using PowerShell. The preview modules and sample code can be found in the [Microsoft Entra GitHub repo](https://github.com/AzureAD/IdentityProtectionTools).

The `Invoke-AzureADIPDismissRiskyUser.ps1` script included in the repository allows organizations to dismiss all risky users in their directory.