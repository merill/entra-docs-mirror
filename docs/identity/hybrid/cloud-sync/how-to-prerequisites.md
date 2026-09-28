---
layout: Conceptual
title: Prerequisites for Microsoft Entra Cloud Sync in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-prerequisites
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the prerequisites and hardware requirements you need for cloud sync.
ms.topic: how-to
ms.date: 2026-07-27T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 88fc98f5-0c60-1f46-2f02-3dad22b6632a
document_version_independent_id: 4d2ce2cc-94dd-6073-f145-5a0694e9b542
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-prerequisites.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-prerequisites.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 51949239-d4e9-f71b-a4d1-d04af02959ff
---

# Prerequisites for Microsoft Entra Cloud Sync in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article provides guidance on using Microsoft Entra Cloud Sync as your identity solution.

## Cloud provisioning agent requirements

You need the following to use Microsoft Entra Cloud Sync:

- Domain Administrator or Enterprise Administrator credentials to create the Microsoft Entra Connect cloud sync gMSA (group managed service account) to run the agent service.
- A Hybrid Identity Administrator account for your Microsoft Entra tenant that isn't a guest user.
- Microsoft Entra Cloud Sync agent must be installed on a domain-joined server. We recommend using Windows Server 2025 or Windows Server 2022. You can also deploy Microsoft Entra Cloud Sync on older Windows Server versions that are in extended support; however, support for this configuration may require [a paid support program](/en-us/lifecycle/policies/fixed#extended-support).
- This server should be a tier 0 server based on the [Active Directory administrative tier model](/en-us/security/privileged-access-workstations/privileged-access-access-model). Installing the agent on a domain controller is supported. For more information, see Harden your Microsoft Entra provisioning agent server
- The Active Directory Schema is required to have the attribute msDS-ExternalDirectoryObjectId, which is available in Windows Server 2016 and later.
- The Windows Credential Manager service (VaultSvc) cannot be disabled as that prevents the provisioning agent from installing.
- High availability refers to the Microsoft Entra Cloud Sync's ability to operate continuously without failure for a long time. By having multiple active agents installed and running, Microsoft Entra Cloud Sync can continue to function even if one agent should fail. Microsoft recommends having 3 active agents installed for high availability.
- On-premises firewall configurations.

## Harden your Microsoft Entra provisioning agent server

We recommend that you harden your Microsoft Entra provisioning agent server to decrease the security attack surface for this critical component of your IT environment. Following these recommendations helps mitigate some security risks to your organization.

- We recommend hardening the Microsoft Entra provisioning agent server as a Control Plane (formerly Tier 0) asset by following the guidance provided in [Secure Privileged Access](/en-us/security/privileged-access-workstations/overview) and [Active Directory administrative tier model](/en-us/security/privileged-access-workstations/privileged-access-access-model).
- Restrict administrative access to the Microsoft Entra provisioning agent server to only domain administrators or other tightly controlled security groups.
- Create a [dedicated account for all personnel with privileged access](/en-us/windows-server/identity/securing-privileged-access/securing-privileged-access). Administrators shouldn't be browsing the web, checking their email, and doing day-to-day productivity tasks with highly privileged accounts.
- Follow the guidance provided in [Securing privileged access](/en-us/security/privileged-access-workstations/overview).
- Deny use of NTLM authentication with the Microsoft Entra provisioning agent server. Here are some ways to do this: [Restricting NTLM on the Microsoft Entra provisioning agent Server](/en-us/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers) and [Restricting NTLM on a domain](/en-us/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-ntlm-authentication-in-this-domain)
- Ensure every machine has a unique local administrator password. For more information, see [Local Administrator Password Solution (Windows LAPS)](/en-us/windows-server/identity/laps/laps-overview) can configure unique random passwords on each workstation and server store them in Active Directory protected by an ACL. Only eligible authorized users can read or request the reset of these local administrator account passwords. Additional guidance for operating an environment with Windows LAPS and privileged access workstations (PAWs) can be found in [Operational standards based on clean source principle](/en-us/security/privileged-access-workstations/privileged-access-access-model#operational-standards-based-on-clean-source-principle).
- Implement dedicated [privileged access workstations](https://4sysops.com/archives/understand-the-microsoft-privileged-access-workstation-paw-security-model/) for all personnel with privileged access to your organization's information systems.
- Follow these [additional guidelines](/en-us/windows-server/identity/ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface) to reduce the attack surface of your Active Directory environment.
- Follow the [Monitor changes to federation configuration](../connect/how-to-connect-monitor-federation-changes) to set up alerts to monitor changes to the trust established between your IdP and Microsoft Entra ID.
- Enable multifactor authentication (MFA) for all users that have privileged access in Microsoft Entra ID or in AD. One security issue with using Microsoft Entra provisioning agent is that if an attacker can get control over the Microsoft Entra provisioning agent server they can manipulate users in Microsoft Entra ID. To prevent an attacker from using these capabilities to take over Microsoft Entra accounts, MFA offers protections. For example, even if an attacker manages to reset a user's password using the Microsoft Entra provisioning agent, they still can't bypass the second factor.

## Group Managed Service Accounts

A group Managed Service Account is a managed domain account that provides automatic password management and simplified service principal name (SPN) management. It also offers the ability to delegate the management to other administrators and extends this functionality over multiple servers. Microsoft Entra Cloud Sync supports and uses a gMSA for running the agent. You'll be prompted for administrative credentials during setup, in order to create this account. The account appears as `domain\provAgentgMSA$`. For more information on a gMSA, see [group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

### Prerequisites for gMSA

- The Active Directory schema in the gMSA domain's forest needs to be updated to Windows Server 2012 or later.
- [PowerShell RSAT modules](/en-us/windows-server/remote/remote-server-administration-tools) on a domain controller.
- At least one domain controller in the domain must be running Windows Server 2012 or later.
- A domain-joined server that runs Windows Server 2025, Windows Server 2022, Windows Server 2019, or Windows Server 2016 for the agent installation.

### Custom gMSA account

If you're creating a custom gMSA account, you need to ensure that the account has the following permissions.

| Type | Name | Access | Applies To |
| --- | --- | --- | --- |
| Allow | gMSA Account | Read all properties | Descendant device objects |
| Allow | gMSA Account | Read all properties | Descendant InetOrgPerson objects |
| Allow | gMSA Account | Read all properties | Descendant Computer objects |
| Allow | gMSA Account | Read all properties | Descendant foreignSecurityPrincipal objects |
| Allow | gMSA Account | Full control | Descendant Group objects |
| Allow | gMSA Account | Read all properties | Descendant User objects |
| Allow | gMSA Account | Read all properties | Descendant Contact objects |
| Allow | gMSA Account | Create/delete User objects | This object and all descendant objects |

For steps on how to upgrade an existing agent to use a gMSA account see [group Managed Service Accounts](how-to-install#group-managed-service-accounts).

For more information on how to prepare your Active Directory for group Managed Service Account, see [group Managed Service Accounts Overview](/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) and [Group managed service accounts with cloud sync](gmsa-cloud-sync).

## In the Microsoft Entra admin center

1. Create a cloud-only Hybrid Identity Administrator account on your Microsoft Entra tenant. This way, you can manage the configuration of your tenant if your on-premises services fail or become unavailable. Learn about how to [add a cloud-only Hybrid Identity Administrator account](../../../fundamentals/how-to-create-delete-users). Finishing this step is critical to ensure that you don't get locked out of your tenant.
2. Add one or more [custom domain names](../../../fundamentals/add-custom-domain) to your Microsoft Entra tenant. Your users can sign in with one of these domain names.

## In your directory in Active Directory

Run the [IdFix tool](/en-us/microsoft-365/enterprise/set-up-directory-synchronization) to prepare the directory attributes for synchronization.

## In your on-premises environment

1. Identify a domain-joined host server that runs Windows Server 2025, Windows Server 2022, Windows Server 2019, or Windows Server 2016 with a minimum of 4-GB RAM and .NET 4.7.1+ runtime.
2. The PowerShell execution policy on the local server must be set to Undefined or RemoteSigned.
3. If there's a firewall between your servers and Microsoft Entra ID, see Firewall and proxy requirements.

Note

Installing the cloud provisioning agent on Windows Server Core isn't supported.

## Provision Microsoft Entra ID to Active Directory Domain Services - Prerequisites

The following prerequisites are required to implement provisioning groups to Active Directory Domain Services (AD DS).

## License requirements

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## General requirements

- Microsoft Entra account with at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) role.
- On-premises AD DS schema with the *msDS-ExternalDirectoryObjectId* attribute, which is available in Windows Server 2016 and later.
- Provisioning agent with build version [1.1.2334.0](reference-version-history#1123340) or later.

Note

The permissions to the service account are assigned during clean install only. If you're upgrading from the previous version, then permissions need to be assigned manually by using PowerShell:

```powershell
$credential = Get-Credential  

Set-AADCloudSyncPermissions -PermissionType UserGroupCreateDelete -TargetDomain "FQDN of domain" -EACredential $credential
```

If the permissions are set manually, you need to assign Read, Write, Create, and Delete all properties for all descendant Groups and User objects.

These permissions aren't applied to AdminSDHolder objects by default. For more information, see [Microsoft Entra provisioning agent gMSA PowerShell cmdlets](how-to-gmsa-cmdlets#grant-permissions-to-a-specific-domain).

- The provisioning agent must be installed on a server that runs Windows Server 2022, Windows Server 2019, or Windows Server 2016.
- The provisioning agent must be able to communicate with one or more domain controllers on ports TCP/389 (LDAP) and TCP/3268 (Global Catalog).
    - Required for Global Catalog lookup to filter out invalid membership references
- Microsoft Entra Connect Sync with build version [2.2.8.0](../connect/reference-connect-version-history#2280)
    - Required to support on-premises user membership synchronized using Microsoft Entra Connect Sync
    - Required to synchronize `AD DS:user:objectGUID` to `AAD DS:user:onPremisesObjectIdentifier`

## Scale limits for Provisioning groups to Active Directory

Group Provision to Active Directory feature's performance is impacted by the size of the tenant and the number of groups and memberships that are in scope for provisioning to Active Directory. This section provides guidance on how to determine if GPAD supports your scale requirement and how to pick the right group scoping mode to achieve quicker initial and delta sync cycles.

### What is not supported?

- Groups that are larger than 50K members aren't supported.
- The use of "All security groups" scoping without applying attribute scope filtering is not supported.

### Scale limits

| Scoping Mode | Number of in-scope groups | Number of membership links (Direct members only) | Notes |
| --- | --- | --- | --- |
| "Selected security groups" mode | Up to 10K groups. The CloudSync pane in Microsoft Entra portal only allows selecting up to 999 groups as well as displaying up to 999 groups. If you need to add more than 1000 groups into scope, see: Expanded group selection via API. | Up to 250K total members across all the groups **in scope**. | Use this scoping mode if your tenant exceeds ANY of these limits 1. Tenant has more than 200k users2. Tenant has more than 40K groups 3. Tenant has more than 1M group memberships. |
| “All Security groups” mode with at least one attribute scoping filter. | Up to 20K groups. | Up to 500K total members across all the groups **in scope**. | Use this scoping mode if your tenant satisfies ALL the below limits:1. Tenant has less than 200k users2. Tenant has less than 40K groups3. Tenant has less than 1M group memberships. |

### What to do if you exceed limits

Exceeding the recommended limits will slow initial and delta sync, possibly causing sync errors. If this happens, follow these steps:

### Too many groups or group members in ‘Selected security groups’ scoping mode:

Reduce the number of in-scope groups (target higher value groups), **or split provisioning into multiple, distinct jobs** with disjoint scopes.

### Too many groups or group members in ‘All security groups’ scoping mode:

Use **Selected security groups** scoping mode as recommended.

### Some group exceeds 50K members:

**Split membership** across multiple groups or adopt staged groups (for example, by region or business unit) to keep each group under the cap.

### Expanded group selection via API

If you need to select more than 999 groups, you must use the [Grant an appRoleAssignment for a service principal](/en-us/graph/api/serviceprincipal-post-approleassignedto) API call.

An example of the API calls is as follows:

```https
POST https://graph.microsoft.com/v1.0/servicePrincipals/{servicePrincipalID}/appRoleAssignedTo
Content-Type: application/json

{
  "principalId": "",
  "resourceId": "",
  "appRoleId": ""
}

```

where:

- **principalId**: Group object ID.
- **resourceId**: Job's service principal ID.
- **appRoleId**: Identifier of app role exposed by the resource service principal.

The following table is a list of App Role IDs for Clouds:

| Cloud | appRoleId |
| --- | --- |
| Public | 1a0abf4d-b9fa-4512-a3a2-51ee82c6fd9f |
| AzureUSGovernment | d8fa317e-0713-4930-91d8-1dbeb150978f |
| AzureUSNatCloud | 50a55e47-aae2-425c-8dcb-ed711147a39f |
| AzureUSSecCloud | 52e862b9-0b95-43fe-9340-54f51248314f |

### More information

Here are more points to consider when you provision groups to AD DS.

- Group membership written to AD DS includes only members that have an AD DS account. Those members can be on-premises synchronized users, cloud-managed users that Cloud Sync provisions to AD DS because they're in scope of user provisioning, or other cloud-created security groups. A cloud-managed user that has no AD DS account is skipped.
- On-premises synchronized users must have the *onPremisesObjectIdentifier* attribute set on their account.
- The *onPremisesObjectIdentifier* must match a corresponding *objectGUID* in the target AD DS environment.
- An on-premises user *objectGUID* attribute can be synchronized to a cloud user *onPremisesObjectIdentifier* attribute by using either sync client.
- Only global Microsoft Entra ID tenants can provision from Microsoft Entra ID to AD DS. Tenants such as B2C aren't supported.
- The provisioning job is scheduled to run every 20 minutes.

## More requirements

- Minimum [Microsoft .NET Framework 4.7.1](https://dotnet.microsoft.com/download/dotnet-framework/net471)

### TLS requirements

Note

Transport Layer Security (TLS) is a protocol that provides for secure communications. Changing the TLS settings affects the entire forest. For more information, see [Update to enable TLS 1.1 and TLS 1.2 as default secure protocols in WinHTTP in Windows](https://support.microsoft.com/help/3140245/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-wi).

The Windows server that hosts the Microsoft Entra Connect cloud provisioning agent must have TLS 1.2 enabled before you install it.

To enable TLS 1.2, follow these steps.

1. Set the following registry keys by copying the content into a *.reg* file and then run the file (right select and choose **Merge**):

    ```dos
    Windows Registry Editor Version 5.00
    
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]
    "DisabledByDefault"=dword:00000000
    "Enabled"=dword:00000001
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server]
    "DisabledByDefault"=dword:00000000
    "Enabled"=dword:00000001
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
    "SchUseStrongCrypto"=dword:00000001
    ```
2. Restart the server.

## Firewall and Proxy requirements

If there's a firewall between your servers and Microsoft Entra ID, configure the following items:

- Ensure that agents can make *outbound* requests to Microsoft Entra ID over the following ports:

    | Port number | Description |
    | --- | --- |
    | **80** | Downloads the certificate revocation lists (CRLs) while validating the TLS/SSL certificate. |
    | **443** | Handles all outbound communication with the service. |
    | **8080** (optional) | Agents report their status every 10 minutes over port 8080, if port 443 is unavailable. This status is displayed in the Microsoft Entra admin center. |
- If your firewall enforces rules according to the originating users, open these ports for traffic from Windows services that run as a network service.
- Ensure that your proxy supports at least HTTP 1.1 protocol and chunked encoding is enabled.
- If your firewall or proxy allows you to specify safe suffixes, add connections:

# [Public Cloud](#tab/public-cloud)
| URL | Description |
| --- | --- |
| `*.msappproxy.net``*.servicebus.windows.net` | The agent uses these URLs to communicate with the Microsoft Entra cloud service. |
| `*.microsoftonline.com``*.microsoft.com``*.msappproxy.com``*.windowsazure.com` | The agent uses these URLs to communicate with the Microsoft Entra cloud service. |
| `mscrl.microsoft.com:80``crl.microsoft.com:80``ocsp.msocsp.com:80``www.microsoft.com:80` | The agent uses these URLs to verify certificates. |
| `login.windows.net``login.live.com` | The agent uses these URLs during the registration process. |
| `aadcdn.msauth.net``aadcdn.msftauth.net``www.msftconnecttest.com` | The agent uses these URLs during the registration process. |

# [U.S. Government Cloud](#tab/us-government-cloud)
| URL | Description |
| --- | --- |
| `*.msappproxy.us``*.servicebus.usgovcloudapi.net` | The agent uses these URLs to communicate with the Microsoft Entra cloud service. |
| `mscrl.microsoft.us:80``crl.microsoft.us:80``ocsp.msocsp.us:80``www.microsoft.us:80` | The agent uses these URLs to verify certificates. |
| `login.windows.us``secure.aadcdn.microsoftonline-p.com``*.microsoftonline.us``*.microsoftonline-p.us``*.msauth.net``*.msauthimages.net``*.msecnd.net``*.msftauth.net``*.msftauthimages.net``*.phonefactor.net``enterpriseregistration.windows.net``management.azure.com``policykeyservice.dc.ad.msft.net``ctldl.windowsupdate.us:80``aadcdn.msftauthimages.us``*.microsoft.us``msauthimages.us``msftauthimages.us` | The agent uses these URLs during the registration process. |

- If you're unable to add connections, allow access to the [Azure datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated weekly.

---

## NTLM requirement

You shouldn't enable NTLM on the Windows Server that is running the Microsoft Entra provisioning agent and if it is enabled you should make sure you disable it.

## Known limitations

The following are known limitations:

### Delta Synchronization

- Group scope filtering for delta sync doesn't support more than 50,000 members.
- When you delete a group that's used as part of a group scoping filter, users who are members of the group, don't get deleted.
- When you rename the OU or group that's in scope, delta sync doesn't remove the users.

### Provisioning Logs

- Provisioning logs don't clearly differentiate between create and update operations. You could see a create operation for an update and an update operation for a create.

### Group renaming or OU renaming

- If you rename a group or OU in AD that's in scope for a given configuration, the cloud sync job isn't able to recognize the name change in AD. The job doesn't go into quarantine and remains healthy.

### Scoping filter

When using OU scoping filter

- The scoping configuration has a limitation of 4 MB in character length. In a standard tested environment, this translates to approximately 50 separate Organizational Units (OUs) or Security Groups, including its required metadata, for a given configuration.
- Nested OUs are supported (that is, you **can** sync an OU that has 130 nested OUs, but you **can't** sync 60 separate OUs in the same configuration).

Note

At this time, it isn't possible to check the scoping configuration size to determine if it is near to, reached, or exceeded the 4 MB character limit, which includes metadata.

### Password Hash Sync

- Using password hash sync with InetOrgPerson isn't supported.