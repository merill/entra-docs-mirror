---
layout: Conceptual
title: Revoke user access in an emergency in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-revoke-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: How to revoke all access for a user in Microsoft Entra ID
ms.topic: how-to
ms.reviewer: yukarppa
ms.date: 2026-06-19T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: a9b38e3c-c054-794a-70af-ce9d2ec70507
document_version_independent_id: 04653c31-670f-ebd4-da07-072ea5503483
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-revoke-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-revoke-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-revoke-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8ba07fcc-2863-79a7-b293-5177cdd8c6c4
---

# Revoke user access in an emergency in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

Scenarios that could require an administrator to revoke all access for a user include compromised accounts, employee termination, and other insider threats. Depending on the complexity of the environment, administrators can take several steps to ensure access is revoked. In some scenarios, there could be a period between the initiation of access revocation and when access is effectively revoked.

To mitigate the risks, you must understand how tokens work. There are many kinds of tokens, which fall into one of the patterns discussed in this article.

## Prerequisites

Sign in with an account that has the appropriate roles. Different steps require different roles:

- Disable user accounts: [User Administrator](../role-based-access-control/permissions-reference#user-administrator) for non-admin users, or [Privileged Authentication Administrator](../role-based-access-control/permissions-reference#privileged-authentication-administrator) for admin accounts.
- Disable devices: [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator) at minimum.

The PowerShell steps in this article also require the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0&amp;preserve-view=true). Install the required modules:

```PowerShell
Install-Module Microsoft.Graph.Users
Install-Module Microsoft.Graph.Users.Actions
Install-Module Microsoft.Graph.Identity.DirectoryManagement
```

Connect to Microsoft Graph with the required scopes:

```PowerShell
Connect-MgGraph -Scopes "User.ReadWrite.All","Directory.AccessAsUser.All"
```

## Access tokens and refresh tokens

Access tokens and refresh tokens are frequently used with thick client applications, and also used in browser-based applications such as single page apps.

- When users authenticate to Microsoft Entra ID, part of Microsoft Entra, authorization policies are evaluated to determine if the user can be granted access to a specific resource.
- After authorization, Microsoft Entra ID issues an access token and a refresh token for the resource.
- If the authentication protocol allows, the app can silently reauthenticate the user by passing the refresh token to Microsoft Entra ID when the access token expires. By default, access tokens issued by Microsoft Entra ID last for 1 hour.
- Microsoft Entra ID then reevaluates its authorization policies. If the user is still authorized, Microsoft Entra ID issues a new access token and refresh token.

Access tokens might pose a security risk if they need to be revoked within a period shorter than their typical one-hour lifespan. For this reason, Microsoft is actively working to bring [continuous access evaluation](../conditional-access/concept-continuous-access-evaluation) to Office 365 applications, which helps ensure invalidation of access tokens in near real time.

## Session tokens (cookies)

Most browser-based applications use session tokens instead of access and refresh tokens.

- When a user opens a browser and authenticates to an application via Microsoft Entra ID, the user receives two session tokens. One from Microsoft Entra ID and another from the application.
- After the application issues its own session token, the application controls access based on its authorization policies.
- The authorization policies of Microsoft Entra ID are reevaluated as often as the application sends the user back to Microsoft Entra ID. Reevaluation usually happens silently, though the frequency depends on how the application is configured. It's possible that the app might never send the user back to Microsoft Entra ID as long as the session token is valid.
- To revoke a session token, the application must revoke access based on its own authorization policies. Microsoft Entra ID can't directly revoke a session token issued by an application.

## Revoke access for a user in the hybrid environment

For a hybrid environment with on-premises Active Directory synchronized with Microsoft Entra ID, Microsoft recommends that IT admins take the following actions. If you have a **Microsoft Entra-only environment**, skip to the Microsoft Entra environment section.

### On-premises Active Directory environment

As an admin in the Active Directory, connect to your on-premises network, open PowerShell, and take the following actions:

1. Disable the user in Active Directory. Refer to [Disable-ADAccount](/en-us/powershell/module/activedirectory/disable-adaccount).

    ```PowerShell
    Disable-ADAccount -Identity johndoe  
    ```
2. Reset the user's password twice in the Active Directory. Refer to [Set-ADAccountPassword](/en-us/powershell/module/activedirectory/set-adaccountpassword).

    Note

    The reason for changing a user's password twice is to mitigate the risk of pass-the-hash, especially if there are delays in on-premises password replication. If you can safely assume this account isn't compromised, you might reset the password only once.

    Important

    Don't use the example passwords in the following cmdlets. Be sure to change the passwords to a random string.

    ```PowerShell
    Set-ADAccountPassword -Identity johndoe -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "p@ssw0rd1" -Force)
    Set-ADAccountPassword -Identity johndoe -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "p@ssw0rd2" -Force)
    ```

### Microsoft Entra environment

For an individual user, you can use the Microsoft Entra admin center to block new sign-ins and revoke refresh tokens.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with an account that has the appropriate role. For more information, see Prerequisites.
2. Browse to **Entra ID** &gt; **Users** &gt; **All users**, and then select the user.
3. Under **Account status**, select **Edit**.
4. In **Properties**, clear **Account enabled**, and then select **Save**.
5. On the user **Overview** page, select **Revoke sessions**.

For repeatable response actions, bulk response, or disabling the user's registered devices, open PowerShell, connect to Microsoft Graph with the required scopes (see Prerequisites), and take the following actions:

1. Disable the user in Microsoft Entra ID. Refer to [Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser).

    ```PowerShell
    $User = Get-MgUser -Search UserPrincipalName:'johndoe@contoso.com' -ConsistencyLevel eventual
    Update-MgUser -UserId $User.Id -AccountEnabled:$false
    ```
2. Revoke the user's Microsoft Entra ID refresh tokens. Refer to [Revoke-MgUserSignInSession](/en-us/powershell/module/microsoft.graph.users.actions/revoke-mgusersigninsession).

    ```PowerShell
    Revoke-MgUserSignInSession -UserId $User.Id
    ```
3. Disable the user's devices. Refer to [Get-MgUserRegisteredDevice](/en-us/powershell/module/microsoft.graph.users/get-mguserregistereddevice).

    ```PowerShell
    Get-MgUserRegisteredDevice -UserId $User.Id -All | ForEach-Object {
        Update-MgDevice -DeviceId $_.Id -AccountEnabled:$false
    }
    ```

Note

For information on specific roles that can perform these steps review [Microsoft Entra built-in roles](../role-based-access-control/permissions-reference)

Note

Azure AD and MSOnline PowerShell modules are deprecated as of March 30, 2024. To learn more, read the [deprecation update](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270). After this date, support for these modules are limited to migration assistance to Microsoft Graph PowerShell SDK and security fixes. The deprecated modules will continue to function through March, 30 2025.

We recommend migrating to [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) to interact with Microsoft Entra ID (formerly Azure AD). For common migration questions, refer to the [Migration FAQ](/en-us/powershell/azure/active-directory/migration-faq). *Note:* Versions 1.0.x of MSOnline may experience disruption after June 30, 2024.

## When access is revoked

After admins take the above steps, the user can't gain new tokens for any application tied to Microsoft Entra ID. The elapsed time between revocation and the user losing their access depends on how the application is granting access:

- For **applications using access tokens**, the user loses access when the access token expires.
- For **applications that use session tokens**, the existing sessions end as soon as the token expires. If the disabled state of the user is synchronized to the application, the application can automatically revoke the user's existing sessions if it's configured to do so. The time it takes depends on the frequency of synchronization between the application and Microsoft Entra ID.

## Best practices

- Deploy an automated provisioning and deprovisioning solution. Deprovisioning users from applications is an effective way of revoking access, especially for applications that use sessions tokens or allow users to sign in directly without a Microsoft Entra or Windows Server AD token. Develop a process to also deprovision users to apps that don't support automatic provisioning and deprovisioning. Ensure applications revoke their own session tokens and stop accepting Microsoft Entra access tokens even if they're still valid.

    - Use [Microsoft Entra app provisioning](../app-provisioning/user-provisioning). Microsoft Entra app provisioning typically runs automatically every 20-40 minutes. [Configure Microsoft Entra provisioning](../saas-apps/tutorial-list) to deprovision or deactivate users in SaaS and on-premises applications. If you were using [Microsoft Identity Manager](/en-us/microsoft-identity-manager/mim-how-provision-users-adds) to automate the deprovisioning of users from on-premises applications, you can use Microsoft Entra app provisioning to reach on-premises applications with a [SQL database](../app-provisioning/on-premises-sql-connector-configure), [non-AD directory server](../app-provisioning/on-premises-ldap-connector-configure) or [other connectors](../app-provisioning/on-premises-custom-connector).
    - For on-premises applications using Windows Server AD, you can configure Microsoft Entra Lifecycle Workflows to [update users in AD (preview)](../../id-governance/lifecycle-workflow-on-premises) when employees leave.
    - Identify and develop a process for applications that require manual deprovisioning. For example, the [automated ServiceNow ticket creation with Microsoft Entra Entitlement Management](../../id-governance/entitlement-management-ticketed-provisioning) can open a ticket when employees lose access. Ensure admins and application owners can quickly run the required manual tasks to deprovision the user from these apps when needed.
- [Manage your devices and applications with Microsoft Intune](/en-us/mem/intune/remote-actions/device-management). Intune-managed [devices can be reset to factory settings](/en-us/mem/intune/remote-actions/devices-wipe). If the device is unmanaged, you can [wipe the corporate data from managed apps](/en-us/mem/intune/apps/apps-selective-wipe). These processes are effective for removing potentially sensitive data from end users' devices. However, for either process to be triggered, the device must be connected to the internet. If the device is offline, it still has access to any locally stored data.

Note

Data on the device can't be recovered after a wipe.

- Use [Microsoft Defender for Cloud Apps to block data download](/en-us/defender-cloud-apps/use-case-proxy-block-session-aad) when appropriate. If the data can only be accessed online, organizations can monitor sessions and achieve real-time policy enforcement.
- Use [Continuous Access Evaluation (CAE) in Microsoft Entra ID](../conditional-access/concept-continuous-access-evaluation). CAE allows admins to revoke the session tokens and access tokens for applications that are CAE capable.