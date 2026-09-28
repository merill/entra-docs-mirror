---
layout: Conceptual
title: Sign-in to Microsoft Entra ID with email as an alternate login ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-authentication-use-email-signin
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to enable users to sign in to Microsoft Entra ID with their email as an alternate login ID
ms.custom: no-azure-ad-ps-ref, sfi-image-nochange
ms.topic: how-to
ms.date: 2025-04-17T00:00:00.0000000Z
ms.reviewer: rahulnagraj
locale: en-us
document_id: 1a2d44d9-f737-c619-a0b9-cf48755cd2ca
document_version_independent_id: 2b6d043e-52fd-d066-d599-3eff99c47756
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-authentication-use-email-signin.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-authentication-use-email-signin
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-authentication-use-email-signin.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a26a3800-275b-7d27-0b06-e4828acc712e
---

# Sign-in to Microsoft Entra ID with email as an alternate login ID - Microsoft Entra ID | Microsoft Learn

Note

Sign-in to Microsoft Entra ID with email as an alternate login ID is a public preview feature of Microsoft Entra ID. For more information about previews, see [Supplemental Terms of Use for Microsoft Azure Previews](https://aka.ms/EntraPreviewsTermsOfUse).

Many organizations want to let users sign in to Microsoft Entra ID using the same credentials as their on-premises directory environment. With this approach, known as hybrid authentication, users only need to remember one set of credentials.

Some organizations haven't moved to hybrid authentication for the following reasons:

- By default, the Microsoft Entra user Principal Name (UPN) is set to the same value as the on-premises UPN.
- Changing the Microsoft Entra UPN creates a mismatch between on-premises and Microsoft Entra environments that could cause problems with certain applications and services.
- Due to business or compliance reasons, the organization doesn't want to use the on-premises UPN to sign in to Microsoft Entra ID.

To move toward hybrid authentication, you can configure Microsoft Entra ID to let users sign in with their email as an alternate login ID. For example, if *Contoso* rebranded to *Fabrikam*, rather than continuing to sign in with the legacy `ana@contoso.com` UPN, email as an alternate login ID can be used. To access an application or service, users would sign in to Microsoft Entra ID using their non-UPN email, such as `ana@fabrikam.com`.

![Diagram of email as an alternate login ID.](media/howto-authentication-use-email-signin/email-alternate-login-id.png)

This article shows you how to enable and use email as an alternate login ID.

## Before you begin

Here's what you need to know about email as an alternate login ID:

- The feature is available in Microsoft Entra ID Free edition and higher.
- The feature enables sign-in with *ProxyAddresses*, in addition to UPN, for cloud-authenticated Microsoft Entra users. More on how this applies to Microsoft Entra business-to-business (B2B) collaboration in the B2B section.
- When a user signs in with a non-UPN email, the `unique_name` and `preferred_username` claims (if present) in the [ID token](../../identity-platform/id-tokens)will return the non-UPN email.
    - If the non-UPN email in use becomes stale (no longer belongs to the user), these claims will return the UPN instead.
- The feature supports managed authentication with Password Hash Sync (PHS) or Pass-Through Authentication (PTA).
- There are two options for configuring the feature:
    - Home Realm Discovery (HRD) policy - Use this option to enable the feature for the entire tenant. At least the [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) role is required.
    - Staged rollout policy - Use this option to test the feature with specific Microsoft Entra groups. When you first add a security group for staged rollout, you're limited to 200 users to avoid a UX time-out. After you've added the group, you can add more users directly to it, as required.

## Preview limitations

In the current preview state, the following limitations apply to email as an alternate login ID:

- **User experience** - Users may see their UPN, even when they signed-in with their non-UPN email. The following example behavior may be seen:

    - User is prompted to sign in with UPN when directed to Microsoft Entra sign-in with `login_hint=<non-UPN email>`.
    - When a user signs-in with a non-UPN email and enters an incorrect password, the *"Enter your password"* page changes to display the UPN.
    - On some Microsoft sites and apps, such as Microsoft Office, the *Account Manager* control typically displayed in the upper right may display the user's UPN instead of the non-UPN email used to sign in.
- **Unsupported flows** - Some flows are currently not compatible with non-UPN emails, such as the following:

    - Microsoft Entra ID Protection doesn't match non-UPN emails with *Leaked Credentials* risk detection. This risk detection uses the UPN to match credentials that have been leaked. For more information, see [How To: Investigate risk](../../id-protection/howto-identity-protection-investigate-risk).
    - When a user is signed-in with a non-UPN email, they cannot change their password. Microsoft Entra self-service password reset (SSPR) should work as expected. During SSPR, the user may see their UPN if they verify their identity using a non-UPN email.
- **Unsupported scenarios** - The following scenarios are not supported. Sign-in with non-UPN email for:

    - [Microsoft Entra hybrid joined devices](../devices/concept-hybrid-join)
    - [Microsoft Entra joined devices](../devices/concept-directory-join)
    - [Microsoft Entra registered devices](../devices/concept-device-registration)
    - [Single Sign-On and App Protection Policies on Mobile Platform](../../identity-platform/mobile-sso-support-overview)
    - Legacy authentication such as POP3 and SMTP
- **Unsupported apps** - Some third-party applications may not work as expected if they assume that the `unique_name` or `preferred_username` claims are immutable or will always match a specific user attribute, such as UPN.
- **Logging** - Changes made to the feature's configuration in HRD policy are not explicitly shown in the audit logs.
- **Staged rollout policy** - The following limitations apply only when the feature is enabled using staged rollout policy:

    - The feature does not work as expected for users that are included in other staged rollout policies.
    - Staged rollout policy supports a maximum of 10 groups per feature.
    - Staged rollout policy does not support nested groups.
    - Staged rollout policy does not support dynamic membership groups.
    - Contact objects inside the group will block the group from being added to a staged rollout policy.
- **Duplicate values** - Within a tenant, a cloud-only user's UPN can be the same value as another user's proxy address synced from the on-premises directory. In this scenario, with the feature enabled, the cloud-only user will not be able to sign in with their UPN. More on this issue in the Troubleshoot section.

## Overview of alternate login ID options

To sign in to Microsoft Entra ID, users enter a value that uniquely identifies their account. Historically, you could only use the Microsoft Entra UPN as the sign-in identifier.

For organizations where the on-premises UPN is the user's preferred sign-in email, this approach was great. Those organizations would set the Microsoft Entra UPN to the exact same value as the on-premises UPN, and users would have a consistent sign-in experience.

### Alternate Login ID for AD FS

However, in some organizations the on-premises UPN isn't used as a sign-in identifier. In the on-premises environments, you would configure the local AD DS to allow sign-in with an alternate login ID. Setting the Microsoft Entra UPN to the same value as the on-premises UPN isn't an option as Microsoft Entra ID would then require users to sign in with that value.

### Alternate Login ID in Microsoft Entra Connect

The typical workaround to this issue was to set the Microsoft Entra UPN to the email address the user expects to sign in with. This approach works, though results in different UPNs between the on-premises AD and Microsoft Entra ID, and this configuration isn't compatible with all Microsoft 365 workloads.

### Email as an Alternate Login ID

A different approach is to synchronize the Microsoft Entra ID and on-premises UPNs to the same value and then configure Microsoft Entra ID to allow users to sign in to Microsoft Entra ID with a verified email. To provide this ability, you define one or more email addresses in the user's *ProxyAddresses* attribute in the on-premises directory. *ProxyAddresses* are then synchronized to Microsoft Entra ID automatically using Microsoft Entra Connect.

| Option | Description |
| --- | --- |
| [Alternate Login ID for AD FS](/en-us/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) | Enable sign-in with an alternate attribute (such as Mail) for AD FS users. |
| [Alternate Login ID in Microsoft Entra Connect](../hybrid/connect/plan-connect-userprincipalname#alternate-login-id) | Synchronize an alternate attribute (such as Mail) as the Microsoft Entra UPN. |
| Email as an Alternate Login ID | Enable sign-in with verified domain *ProxyAddresses* for Microsoft Entra users. |

## Synchronize sign-in email addresses to Microsoft Entra ID

Traditional Active Directory Domain Services (AD DS) or Active Directory Federation Services (AD FS) authentication happens directly on your network and is handled by your AD DS infrastructure. With hybrid authentication, users can instead sign in directly to Microsoft Entra ID.

To support this hybrid authentication approach, you synchronize your on-premises AD DS environment to Microsoft Entra ID using [Microsoft Entra Connect](../hybrid/connect/whatis-azure-ad-connect) and configure it to use PHS or PTA. For more information, see [Choose the right authentication method for your Microsoft Entra hybrid identity solution](../hybrid/connect/choose-ad-authn).

In both configuration options, the user submits their username and password to Microsoft Entra ID, which validates the credentials and issues a ticket. When users sign in to Microsoft Entra ID, it removes the need for your organization to host and manage an AD FS infrastructure.

One of the user attributes that's automatically synchronized by Microsoft Entra Connect is *ProxyAddresses*. If users have an email address defined in the on-premises AD DS environment as part of the *ProxyAddresses* attribute, it's automatically synchronized to Microsoft Entra ID. This email address can then be used directly in the Microsoft Entra sign-in process as an alternate login ID.

Important

Only emails in verified domains for the tenant are synchronized to Microsoft Entra ID. Each Microsoft Entra tenant has one or more verified domains, for which you have proven ownership, and are uniquely bound to your tenant.

For more information, see [Add and verify a custom domain name in Microsoft Entra ID](../../fundamentals/add-custom-domain).

## B2B guest user sign-in with an email address

![Diagram of email as an alternate login ID for B 2 B guest user sign-in.](media/howto-authentication-use-email-signin/email-alternate-login-id-b2b.png)

Email as an alternate login ID applies to [Microsoft Entra B2B collaboration](../../external-id/what-is-b2b) under a "bring your own sign-in identifiers" model. When email as an alternate login ID is enabled in the home tenant, Microsoft Entra users can perform guest sign in with non-UPN email on the resource tenant endpoint. No action is required from the resource tenant to enable this functionality.

Note

When an alternate login ID is used on a resource tenant endpoint that does not have the functionality enabled, the sign-in process will work seamlessly, but SSO will be interrupted.

## Enable user sign-in with an email address

Note

This configuration option uses HRD policy. For more information, see [homeRealmDiscoveryPolicy resource type](/en-us/graph/api/resources/homerealmdiscoverypolicy).

Once users with the *ProxyAddresses* attribute applied are synchronized to Microsoft Entra ID using Microsoft Entra Connect, you need to enable the feature for users to sign in with email as an alternate login ID for your tenant. This feature tells the Microsoft Entra login servers to not only check the sign-in identifier against UPN values, but also against *ProxyAddresses* values for the email address.

You can use either Microsoft Entra admin center or Graph PowerShell to set up the feature.

### Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Connect Sync**
3. Select Email as alternate login ID\*\*.

    ![Screenshot of email as alternate login ID option in the Microsoft Entra admin center.](media/howto-authentication-use-email-signin/azure-ad-connect-screen.png)
4. Click the checkbox next to *Email as an alternate login ID*.
5. Click **Save**.

    ![Screenshot of email as alternate login ID blade in the Microsoft Entra admin center.](media/howto-authentication-use-email-signin/email-alternate-login-id-screen.png)

With the policy applied, it can take up to one hour to propagate and for users to be able to sign in using their alternate login ID.

### PowerShell

Note

This configuration option uses HRD policy. For more information, see [homeRealmDiscoveryPolicy resource type](/en-us/graph/api/resources/homeRealmDiscoveryPolicy?view=graph-rest-1.0&amp;preserve-view=true).

Once users with the *ProxyAddresses* attribute applied are synchronized to Microsoft Entra ID using Microsoft Entra Connect, you need to enable the feature for users to sign-in with email as an alternate login ID for your tenant. This feature tells the Microsoft Entra login servers to not only check the sign-in identifier against UPN values, but also against *ProxyAddresses* values for the email address.

1. Open a PowerShell session as an administrator, then install the *Microsoft.Graph* module using the `Install-Module` cmdlet:

    ```powershell
    Install-Module Microsoft.Graph
    ```

    For more information on installation, see [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation).
2. Sign-in to your Microsoft Entra tenant using the `Connect-MgGraph` cmdlet:

    ```powershell
    Connect-MgGraph -Scopes "Policy.ReadWrite.ApplicationConfiguration" -TenantId organizations
    ```

    The command will ask you to authenticate using a web browser.
3. Check if a *HomeRealmDiscoveryPolicy* already exists in your tenant using the `Get-MgPolicyHomeRealmDiscoveryPolicy` cmdlet as follows:

    ```powershell
    Get-MgPolicyHomeRealmDiscoveryPolicy
    ```
4. If there's no policy currently configured, the command returns nothing. If a policy is returned, skip this step and move on to the next step to update an existing policy.

    To add the *HomeRealmDiscoveryPolicy* to the tenant, use the `New-MgPolicyHomeRealmDiscoveryPolicy` cmdlet and set the *AlternateIdLogin* attribute to *"Enabled": true* as shown in the following example:

    ```powershell
    $AzureADPolicyDefinition = @(
      @{
         "HomeRealmDiscoveryPolicy" = @{
            "AlternateIdLogin" = @{
               "Enabled" = $true
            }
         }
      } | ConvertTo-JSON -Compress
    )
    
    $AzureADPolicyParameters = @{
      Definition            = $AzureADPolicyDefinition
      DisplayName           = "BasicAutoAccelerationPolicy"
      AdditionalProperties  = @{ IsOrganizationDefault = $true }
    }
    
    New-MgPolicyHomeRealmDiscoveryPolicy @AzureADPolicyParameters
    ```

    When the policy has been successfully created, the command returns the policy ID, as shown in the following example output:

    ```powershell
    Definition                                                           DeletedDateTime Description DisplayName                 Id            IsOrganizationDefault
    ----------                                                           --------------- ----------- -----------                 --            ---------------------
    {{"HomeRealmDiscoveryPolicy":{"AlternateIdLogin":{"Enabled":true}}}}                             BasicAutoAccelerationPolicy HRD_POLICY_ID True
    ```
5. If there's already a configured policy, check if the *AlternateIdLogin* attribute is enabled, as shown in the following example policy output:

    ```powershell
    Definition                                                           DeletedDateTime Description DisplayName                 Id            IsOrganizationDefault
    ----------                                                           --------------- ----------- -----------                 --            ---------------------
    {{"HomeRealmDiscoveryPolicy":{"AlternateIdLogin":{"Enabled":true}}}}                             BasicAutoAccelerationPolicy HRD_POLICY_ID True
    ```

    If the policy exists but the *AlternateIdLogin* attribute that isn't present or enabled, or if other attributes exist on the policy you wish to preserve, update the existing policy using the `Update-MgPolicyHomeRealmDiscoveryPolicy` cmdlet.

    Important

    When you update the policy, make sure you include any old settings and the new *AlternateIdLogin* attribute.

    The following example adds the *AlternateIdLogin* attribute and preserves the *AllowCloudPasswordValidation* attribute that was previously set:

    ```powershell
    $AzureADPolicyDefinition = @(
      @{
         "HomeRealmDiscoveryPolicy" = @{
            "AllowCloudPasswordValidation" = $true
            "AlternateIdLogin" = @{
               "Enabled" = $true
            }
         }
      } | ConvertTo-JSON -Compress
    )
    
    $AzureADPolicyParameters = @{
      HomeRealmDiscoveryPolicyId = "HRD_POLICY_ID"
      Definition                 = $AzureADPolicyDefinition
      DisplayName                = "BasicAutoAccelerationPolicy"
      AdditionalProperties       = @{ "IsOrganizationDefault" = $true }
    }
    
    Update-MgPolicyHomeRealmDiscoveryPolicy @AzureADPolicyParameters
    ```

    Confirm that the updated policy shows your changes and that the *AlternateIdLogin* attribute is now enabled:

    ```powershell
    Get-MgPolicyHomeRealmDiscoveryPolicy
    ```

Note

With the policy applied, it can take up to an hour to propagate and for users to be able to sign-in using email as an alternate login ID.

### Removing policies

To remove an HRD policy, use the `Remove-MgPolicyHomeRealmDiscoveryPolicy` cmdlet:

```powershell
Remove-MgPolicyHomeRealmDiscoveryPolicy -HomeRealmDiscoveryPolicyId "HRD_POLICY_ID"
```

## Enable staged rollout to test user sign-in with an email address

Note

This configuration option uses staged rollout policy. For more information, see [featureRolloutPolicy resource type](/en-us/graph/api/resources/featurerolloutpolicy).

Staged rollout policy allows tenant administrators to enable features for specific Microsoft Entra groups. It is recommended that tenant administrators use staged rollout to test user sign-in with an email address. When administrators are ready to deploy this feature to their entire tenant, they should use HRD policy.

1. Open a PowerShell session as an administrator, then install the *Microsoft.Graph.Beta* module using the [Install-Module](/en-us/powershell/module/powershellget/install-module) cmdlet:

    ```powershell
    Install-Module Microsoft.Graph.Beta
    ```

    If prompted, select **Y** to install NuGet or to install from an untrusted repository.
2. Sign in to your Microsoft Entra tenant using the [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands#using-connect-mggraph) cmdlet:

    ```powershell
    Connect-MgGraph -Scopes "Directory.ReadWrite.All"
    ```

    The command returns information about your account, environment, and tenant ID.
3. List all existing staged rollout policies using the following cmdlet:

    ```powershell
    Get-MgBetaPolicyFeatureRolloutPolicy
    ```
4. If there are no existing staged rollout policies for this feature, create a new staged rollout policy and take note of the policy ID:

    ```powershell
    $MgPolicyFeatureRolloutPolicy = @{
    Feature    = "EmailAsAlternateId"
    DisplayName = "EmailAsAlternateId Rollout Policy"
    IsEnabled   = $true
    }
    New-MgBetaPolicyFeatureRolloutPolicy @MgPolicyFeatureRolloutPolicy
    ```
5. Find the directoryObject ID for the group to be added to the staged rollout policy. Note the value returned for the *Id* parameter, because it will be used in the next step.

    ```powershell
    Get-MgBetaGroup -Filter "DisplayName eq 'Name of group to be added to the staged rollout policy'"
    ```
6. Add the group to the staged rollout policy as shown in the following example. Replace the value in the *-FeatureRolloutPolicyId* parameter with the value returned for the policy ID in step 4 and replace the value in the *-OdataId* parameter with the *Id* noted in step 5. It may take up to 1 hour before users in the group can sign in to Microsoft Entra ID with email as an alternate login ID.

    ```powershell
    New-MgBetaDirectoryFeatureRolloutPolicyApplyToByRef `
       -FeatureRolloutPolicyId "ROLLOUT_POLICY_ID" `
       -OdataId "https://graph.microsoft.com/v1.0/directoryObjects/{GROUP_OBJECT_ID}"
    ```

For new members added to the group, it may take up to 24 hours before they can sign in to Microsoft Entra ID with email as an alternate login ID.

### Removing groups

To remove a group from a staged rollout policy, run the following command:

```powershell
Remove-MgBetaPolicyFeatureRolloutPolicyApplyToByRef -FeatureRolloutPolicyId "ROLLOUT_POLICY_ID" -DirectoryObjectId "GROUP_OBJECT_ID"
```

### Removing policies

To remove a staged rollout policy, first disable the policy then remove it from the system:

```powershell
Update-MgBetaPolicyFeatureRolloutPolicy -FeatureRolloutPolicyId "ROLLOUT_POLICY_ID" -IsEnabled:$false 
Remove-MgBetaPolicyFeatureRolloutPolicy -FeatureRolloutPolicyId "ROLLOUT_POLICY_ID"
```

## Test user sign-in with an email address

To test that users can sign in with email, go to https://myprofile.microsoft.com and sign in with a non-UPN email, such as `balas@fabrikam.com`. The sign-in experience should look and feel the same as signing-in with the UPN.

## Troubleshoot

If users have trouble signing in with their email address, review the following troubleshooting steps:

1. Make sure it's been at least 1 hour since email as an alternate login ID was enabled. If the user was recently added to a group for staged rollout policy, make sure it's been at least 24 hours since they were added to the group.
2. If using HRD policy, confirm that the Microsoft Entra ID *HomeRealmDiscoveryPolicy* has the *AlternateIdLogin* definition property set to *"Enabled": true* and the *IsOrganizationDefault* property set to *True*:

    ```powershell
    Get-MgBetaPolicyHomeRealmDiscoveryPolicy | Format-List *
    ```

    If using staged rollout policy, confirm that the Microsoft Entra ID *FeatureRolloutPolicy* has the *IsEnabled* property set to *True*:

    ```powershell
    Get-MgBetaPolicyFeatureRolloutPolicy
    ```
3. Make sure the user account has their email address set in the *ProxyAddresses* attribute in Microsoft Entra ID.

### Sign-in logs

![Screenshot of Microsoft Entra sign-in logs showing email as alternate login ID activity.](media/howto-authentication-use-email-signin/email-alternate-login-id-logs.png)

You can review the [sign-in logs in Microsoft Entra ID](../monitoring-health/concept-sign-ins) for more information. Sign-ins with email as an alternate login ID will emit `proxyAddress` in the *Sign-in identifier type* field and the inputted username in the *Sign-in identifier* field.

### Conflicting values between cloud-only and synced users

Within a tenant, a cloud-only user's UPN may take on the same value as another user's proxy address synced from the on-premises directory. In this scenario, with the feature enabled, the cloud-only user will not be able to sign in with their UPN. Here are the steps for detecting instances of this issue.

1. Open a PowerShell session as an administrator, then install Microsoft Graph by using the [Install-Module](/en-us/powershell/module/powershellget/install-module) cmdlet:

    ```powershell
    Install-Module Microsoft.Graph.Authentication
    ```

    If prompted, select **Y** to install NuGet or to install from an untrusted repository.
2. Connect to Microsoft Graph:

    ```powershell
    Connect-MgGraph -Scopes "User.Read.All"
    ```
3. Get affected users.

    ```powershell
    # Get all users
    $allUsers = Get-MgUser -All
    
    # Get list of proxy addresses from all synced users
    $syncedProxyAddresses = $allUsers |
        Where-Object {$_.ImmutableId} |
        Select-Object -ExpandProperty ProxyAddresses |
        ForEach-Object {$_ -Replace "smtp:", ""}
    
    # Get list of user principal names from all cloud-only users
    $cloudOnlyUserPrincipalNames = $allUsers |
        Where-Object {!$_.ImmutableId} |
        Select-Object -ExpandProperty UserPrincipalName
    
    # Get intersection of two lists
    $duplicateValues = $syncedProxyAddresses |
        Where-Object {$cloudOnlyUserPrincipalNames -Contains $_}
    ```
4. To output affected users:

    ```powershell
    # Output affected synced users
    $allUsers |
        Where-Object {$_.ImmutableId -And ($_.ProxyAddresses | Where-Object {($duplicateValues | ForEach-Object {"smtp:$_"}) -Contains $_}).Length -GT 0} |
        Select-Object ObjectId, DisplayName, UserPrincipalName, ProxyAddresses, ImmutableId, UserType
    
    # Output affected cloud-only users
    $allUsers |
        Where-Object {!$_.ImmutableId -And $duplicateValues -Contains $_.UserPrincipalName} |
        Select-Object ObjectId, DisplayName, UserPrincipalName, ProxyAddresses, ImmutableId, UserType
    ```
5. To output affected users to CSV:

    ```powershell
    # Output affected users to CSV
    $allUsers |
        Where-Object {
            ($_.ImmutableId -And ($_.ProxyAddresses | Where-Object {($duplicateValues | ForEach-Object {"smtp:$_"}) -Contains $_}).Length -GT 0) -Or
            (!$_.ImmutableId -And $duplicateValues -Contains $_.UserPrincipalName)
        } |
        Select-Object ObjectId, DisplayName, UserPrincipalName, @{n="ProxyAddresses"; e={$_.ProxyAddresses -Join ','}}, @{n="IsSyncedUser"; e={$_.ImmutableId.Length -GT 0}}, UserType |
        Export-Csv -Path .\AffectedUsers.csv -NoTypeInformation
    ```