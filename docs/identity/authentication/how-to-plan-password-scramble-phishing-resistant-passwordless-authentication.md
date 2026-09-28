---
layout: Conceptual
title: Remove Passwords from Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-plan-password-scramble-phishing-resistant-passwordless-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Removing password usage from Entra through Password scrambling to deploy passwordless and phishing-resistant authentication for organizations that use Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-01-28T00:00:00.0000000Z
ms.reviewer: sipower
ms.collection: M365-identity-device-management
locale: en-us
document_id: fd833575-6ab8-4526-a3c6-949fdb072fa3
document_version_independent_id: fd833575-6ab8-4526-a3c6-949fdb072fa3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-plan-password-scramble-phishing-resistant-passwordless-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-plan-password-scramble-phishing-resistant-passwordless-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-plan-password-scramble-phishing-resistant-passwordless-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e1e53da8-0f7d-73cf-171b-aac66a28e548
---

# Remove Passwords from Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Passwords are one of the least secure authentication methods available. They are vulnerable to a wide range of threats—including phishing, credential stuffing, brute-force attacks, and social engineering. To realize the benefits of passwordless authentication in Microsoft Entra ID, you must ensure passwords are no longer available as a sign-in option in your tenant.

Password scrambling ensures that users can't authenticate by using passwords. It forces them to use more secure phishing-resistant passwordless credentials, like Windows Hello for Business, FIDO2 security keys, or passkey in Microsoft Authenticator. Because there's no known reference of the password after scrambling, it reduces the attack surface for bad actors.

This article provides guidance about how to scramble passwords for both hybrid users who are synced from on-premises Active Directory Domain Services (AD DS) and cloud-only users in Microsoft Entra ID.

## Prerequisites

- Microsoft Entra Connect sync [version 2.4.18.0 or later](../hybrid/connect/how-to-connect-password-hash-synchronization#password-hash-synchronization-and-smart-card-authentication)

## Scramble passwords for hybrid user accounts synced from on-premises AD DS

Organizations with users synced from on-premises AD DS to Microsoft Entra ID should scramble user passwords in the on-premises environment, as on-premises is the source of authority for synced user accounts and their passwords. If your organization uses [cloud authentication](../hybrid/connect/choose-ad-authn) and syncs password hashes to Microsoft Entra ID, then these scrambled passwords are also synced to the cloud. The sync process ensures that users aren't aware of their passwords in either on-premises or the cloud, preventing their use and driving users towards using more secure phishing-resistant passwordless credentials.

## Scramble on-premises user passwords with a scripted random value

In Active Directory, it is not possible to remove a password attribute from a user account. Therefore to prevent usage of the password you can scramble the password periodically.

If you have legacy applications that still require a password for authentication, users can continue to use self-service password reset (SSPR) to set their password to a known state to access these apps for a period of time, until their password is scrambled again.

You can use the following script to routinely scramble any passwords that users reset back to a known state.

The script allows you to scramble a user's password in your AD DS domain. It generates a random password of 64 characters and sets it for the user specified in the variable name $samAccountName. You must modify the $samAccountName variable in the script to target the appropriate user. Use the credentials of an admin account with appropriate permissions in on-premises AD DS.

Caution

Execute the script only from a secure and trusted environment, and ensure that the script isn't logged. Treat the host where the script is executed as a privileged host, with the same level of security as a domain controller.

```PowerShell
$samAccountName = <sAMAccountName of the user>

Import-Module ActiveDirectory

function Generate-RandomPassword{
    [CmdletBinding()]
    param (
      [int]$Length = 64
    )
  $chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()-_=+[]{};:,.<>/?\|`~"
  $random = New-Object System.Random
  $password = ""
  for ($i = 0; $i -lt $Length; $i++) {
    $index = $random.Next(0, $chars.Length)
    $password += $chars[$index]
  }
  return $password
}

Import-Module ActiveDirectory

$NewPassword = ConvertTo-SecureString -String (Generate-RandomPassword) -AsPlainText -Force

Set-ADAccountPassword -Identity $samAccountName -NewPassword $NewPassword -Reset
```

Note

If your password scrambling script runs less frequently than your current password age policy, then you should consider increasing password age to be greater than this frequency, or setting password age to 0, which disables password expiration.

## Randomize passwords for cloud user accounts in Microsoft Entra ID

Cloud-based passwordless users should have their password set to a random value. Randomizing the password prevents the user from knowing the password and using it to authenticate. Optionally, organizations can allow end users to reset their password if they encounter an application where they need the password. Run the script routinely to scramble any passwords that users have reset back to a known state.

The following sample PowerShell script generates a random password of 64 characters and sets it for the user specified in the variable name **$userId** against Microsoft Entra ID. Modify the **$userId** variable of the script to match your environment, and then run it in a PowerShell session. When prompted to authenticate to Microsoft Entra ID, use the credentials of an account with a role that can reset passwords.

```PowerShell
$userId = "<UPN of the user>"

function Generate-RandomPassword{
    [CmdletBinding()]  
    param (  
      [int]$Length = 64  
    )  
  $chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()-_=+[]{};:,.<>/? \|`~"  
  $rng = [System.Security.Cryptography.RandomNumberGenerator]::Create()  
  $bytes = New-Object byte[] $Length  
  $rng.GetBytes($bytes)  
  $password = -join ($bytes | ForEach-Object { $chars[$_ % $chars.Length] })  
  $rng.Dispose()  
  return $password  
}

Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
Install-Module Microsoft.Graph -Scope CurrentUser
Import-Module Microsoft.Graph.Users.Actions
Connect-MgGraph -Scopes "UserAuthenticationMethod.ReadWrite.All" -NoWelcome

$passwordParams = @{
 UserId = $userId
 AuthenticationMethodId = "28c10230-6103-485e-b985-444c60001490"
 NewPassword = Generate-RandomPassword
}

Reset-MgUserAuthenticationMethodPassword @passwordParams
```

Caution

Execute the script only from a secure and trusted environment, and ensure that the script isn't logged. Treat the host where the script is executed as a privileged host, with the same level of security as a domain controller.

## More considerations for organizations that completely enforce phishing-resistant authentication

If your organization no longer needs passwords whatsoever, because all applications and scenarios are compatible with passwordless credentials, then you may no longer need to provide users with self-service password recovery options. Consider disabling tools that let users override the scrambled passwords and gain access to their password again.

- Disable self-service password reset (SSPR) tools, including [Microsoft Entra self-service password reset](tutorial-enable-sspr-writeback#clean-up-resources).
- Disable password writeback from [Microsoft Entra to on-premises Active Directory](tutorial-enable-sspr-writeback#clean-up-resources).
- Set your Microsoft Entra password policy to have [no expiry](concept-sspr-policy).