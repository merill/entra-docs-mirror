---
layout: Conceptual
title: Microsoft Entra hybrid join using Microsoft Entra Kerberos (preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/how-to-hybrid-join-using-microsoft-entra-kerberos
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Explains prerequisites and steps to set up Microsoft Entra hybrid join by using Microsoft Entra Kerberos.
ms.reviewer: nbeesett
ms.date: 2026-02-24T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: af837306-f9c9-73aa-ff16-7c366e04802d
document_version_independent_id: af837306-f9c9-73aa-ff16-7c366e04802d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/how-to-hybrid-join-using-microsoft-entra-kerberos.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/how-to-hybrid-join-using-microsoft-entra-kerberos
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/how-to-hybrid-join-using-microsoft-entra-kerberos.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 427ef132-4243-2167-d218-06495ab95726
---

# Microsoft Entra hybrid join using Microsoft Entra Kerberos (preview) - Microsoft Entra ID | Microsoft Learn

You can use Microsoft Entra Kerberos to perform Microsoft Entra hybrid join for a device without requiring Active Directory Federation Services (AD FS) or Microsoft Entra Connect sync. You get the Microsoft Entra hybrid join behavior instantly without the AD FS setup.

## Use cases

The following use cases are enabled for preview:

- Deploy non-persistent Virtual Desktop Infrastructure (VDI) with Microsoft Entra hybrid join in a managed environment.
- Deploy Microsoft Entra hybrid join for customers who have or want to use Microsoft Entra Cloud Sync.
- Improve provisioning experience for Azure Virtual Desktop and Windows 365 hybrid deployment.
- Deploy Microsoft Entra hybrid join for a disconnected forest setup where Microsoft Entra Connect Sync can't be used.

## Prerequisites

Make sure you have the following permissions and configuration set up to perform Microsoft Entra hybrid join using Microsoft Entra Kerberos. There are no license requirements.

- **Role requirements**: The user who creates and configures Entra Kerberos Trusted Domain Object needs the following roles:

    - A member of the Domain Admins and Enterprise Admins group in Active Directory Domain Services on-premises
    - A [Hybrid Identity Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator) in Microsoft Entra ID

    For more information, see [Create and configure Microsoft Entra Kerberos Trusted Domain Object](/en-us/azure/azure-sql/managed-instance/winauth-azuread-setup-incoming-trust-based-flow#permissions).
- **Configure the Key Distribution Center (KDC) proxy server Group Policy Object (GPO)**: This prerequisite is only required if you deployed a KDC Proxy Server GPO to your client computer. The user who configures the GPO must be a Domain Admin or be delegated permissions to configure a GPO.
- **Configure Microsoft Entra Device Registration Service Principal**: Add a Kerberos entry to the Microsoft Entra device registration service principal. The user who configures the service principal must have the [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) role.
- **Deploy a domain controller that runs Windows Server 2025**: Install at least one domain controller that runs Windows Server 2025 [build 26100.6905](https://support.microsoft.com/topic/october-23-2025-kb5070881-os-build-26100-6905-out-of-band-8e7ac742-6785-4677-87e4-b73dd8ac0122) or later in the Active Directory domain.
- **Configure client computer for Entra Kerberos based join**: You need to deploy [Windows 11 build 26100.6584](https://support.microsoft.com/topic/september-9-2025-kb5065426-os-build-26100-6584-77a41d9b-1b7c-4198-b9a5-3c4b6706dea9) or later on the client computer that you want to register with Entra as Entra hybrid join using Entra Kerberos.

    Note

    The client computer must have unimpeded network connectivity with the domain controller that runs Windows Server 2025 during join.
- **Configure Service Connection Point (SCP):** You can use Microsoft Entra Connect or write to Active Directory Domain Services (AD DS) by using PowerShell. For more information, see [Configure a service connection point](/en-us/entra/identity/devices/hybrid-join-manual#configure-a-service-connection-point).

## Create and configure Microsoft Entra Kerberos Trusted Domain Object

Follow the steps in [How to set up Windows Authentication for Microsoft Entra ID with the incoming trust-based flow](/en-us/azure/azure-sql/managed-instance/winauth-azuread-setup-incoming-trust-based-flow#create-and-configure-the-microsoft-entra-kerberos-trusted-domain-object).

## Configure the KDC proxy server GPO

Skip this section if you didn't deploy the KDC proxy server GPO on your client computers.

1. Find your [Microsoft Entra tenant ID](/en-us/azure/active-directory/fundamentals/how-to-find-tenant).
2. Deploy the following Group Policy setting to client machines using the incoming trust-based flow:
    1. Edit the **Administrative Templates\System\Kerberos\Specify KDC proxy servers for Kerberos clients** policy setting.

        - If the policy is **Not Configured**, go to step e.
        - If the policy is **Disabled**, select **Enabled**.
    2. Under **Options**, select **Show...**. This opens the **Show Contents** dialog box.

        [![Screenshot of dialog box to enable Specify KDC proxy servers for Kerberos clients.](media/how-to-hybrid-join-using-microsoft-entra-kerberos/show-contents.png)](media/how-to-hybrid-join-using-microsoft-entra-kerberos/show-contents.png#lightbox)
    3. Define the KDC proxy servers setting by using the following mapping. Replace `your_Microsoft Entra_tenant_id` with your Microsoft Entra tenant ID. **A blank space appears after https and before the closing / in the value mapping**.

        | **Value name** | **Value** |
        | --- | --- |
        | KERBEROS.MICROSOFTONLINE.COM | `https login.microsoftonline.com:443:your_Microsoft Entra_tenant_id/kerberos /` |

        [![Screenshot of the Define KDC proxy server settings dialog box.](media/how-to-hybrid-join-using-microsoft-entra-kerberos/settings.png)](media/how-to-hybrid-join-using-microsoft-entra-kerberos/settings.png#lightbox)
    4. Select **OK** to close the **Show Contents** dialog box.
    5. In the **Specify KDC proxy servers for Kerberos clients** dialog box, select **Apply**.

### Configure Microsoft Entra Device Registration Service Principal

1. Install [Microsoft Entra PowerShell](/en-us/powershell/entra-powershell/installation).
2. Open an elevated PowerShell session by choosing **Run as administrator**.
3. Run the following PowerShell command and authenticate by using a Microsoft Entra account with the [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) role.

    ```powershell
    Connect-Entra -Environment ‘Global’ -Scopes "Application.ReadWrite.All"
    ```

    Note

    Azure for US Government and Microsoft sovereign clouds require different environment names. Run `Get-EntraEnvironment` to retrieve the list of predefined environments.
4. Run the following command to check your service principal settings:

    ```powershell
    $drsSP = Get-EntraServicePrincipal -Filter "AppId eq '01cb2876-7ebd-4aa4-9cc9-d28bd4d359a9'"
    $drsSP.ServicePrincipalNames
    ```
5. Check the displayed service principal names. If `adrs/enterpriseregistration.windows.net` isn't listed, run the following command to add it:

    ```powershell
    $spns = [System.Collections.Generic.List[string]]::new($drsSP.ServicePrincipalNames)
    $kerbSpn = "adrs/enterpriseregistration.windows.net"
    $spns.Add($kerbSpn)
    Set-EntraServicePrincipal -ObjectId $drsSp.ObjectId -ServicePrincipalNames $spns
    $drsSP.ServicePrincipalNames
    ```

    Note

    Check the displayed service principal names again. The `adrs/enterpriseregistration.windows.net` service principal name should be listed. Azure for US Government and Microsoft sovereign clouds have different service principal names.
6. Run the following command to check the tags of the service principal:

    ```powershell
    $drsSP.Tags
    ```
7. Check the displayed tags. If `KerberosPolicy:ExchangeForJwt` isn't listed, run the following command to add it.

    ```powershell
    $tags = [System.Collections.Generic.List[string]]::new($drsSP.Tags)  
    $tags.Add("KerberosPolicy:ExchangeForJwt")
    Set-EntraServicePrincipal -ObjectId $drsSP.ObjectId -Tags $tags
    ```

Or you can run the following script:

```powershell
# Use specific environment for your sovereign cloud
# Run Get-EntraEnvironment to retrieve the list of predefined environments

Connect-Entra -Environment 'Global' -Scopes "Application.ReadWrite.All"

# Get the service principal

$drsSP = Get-EntraServicePrincipal -Filter "AppId eq '01cb2876-7ebd-4aa4-9cc9-d28bd4d359a9'"

# Prepare both updates

$needsUpdate = $false
$spns = [System.Collections.Generic.List[string]]::new($drsSP.ServicePrincipalNames)
$tags = [System.Collections.Generic.List[string]]::new($drsSP.Tags)

# Configure Kerberos SPN

$kerbSpn = "adrs/enterpriseregistration.windows.net"
if ($drsSP.ServicePrincipalNames -notcontains $kerbSpn) {
Write-Host "Kerberos SPN needs to be added"
$spns.Add($kerbSpn)
$needsUpdate = $true

}

# Configure Kerberos policy tag

$kerberosTag = "KerberosPolicy:ExchangeForJwt"
if ($drsSP.Tags -notcontains $kerberosTag) {
Write-Host "Kerberos policy tag needs to be added"
$tags.Add($kerberosTag)
$needsUpdate = $true

}

# Single update operation

if ($needsUpdate) {
Write-Host "Updating service principal configuration..."
Set-EntraServicePrincipal -ObjectId $drsSP.Id -ServicePrincipalNames $spns -Tags $tags
Write-Host "Service principal configuration updated successfully"
} else {
Write-Host "Service principal already configured correctly"

}

# Display final configuration

$drsSP = Get-EntraServicePrincipal -Filter "AppId eq '01cb2876-7ebd-4aa4-9cc9-d28bd4d359a9'"
Write-Host "`nFinal Configuration:"
Write-Host "SPNs:"
$drsSP.ServicePrincipalNames | ForEach-Object { Write-Host " $_" }
Write-Host "Tags:"
$drsSP.Tags | ForEach-Object { Write-Host " $_" }
```

## Deploy a domain controller that runs Windows Server 2025

Follow these [instructions](/en-us/windows-server/identity/ad-ds/deploy/upgrade-domain-controllers) to deploy a domain controller to your domain. Make sure the domain controller runs Windows Server 2025 [build 26100.6905](https://support.microsoft.com/topic/october-23-2025-kb5070881-os-build-26100-6905-out-of-band-8e7ac742-6785-4677-87e4-b73dd8ac0122) or later.

Note

You need to install a domain controller that runs Windows Server 2025 in every domain that you want to perform Microsoft Entra hybrid join using Microsoft Entra Kerberos.

### Configure the client computer for Microsoft Entra Kerberos join

1. Deploy [Windows 11 build 26100.6584](https://support.microsoft.com/topic/september-9-2025-kb5065426-os-build-26100-6584-77a41d9b-1b7c-4198-b9a5-3c4b6706dea9) or later on a client computer, or use Windows update to update your existing Windows 11 client computer.
2. Join the client computer to the Active Directory domain and restart it.

## FAQ

**Question**: Can Microsoft Entra hybrid join using Entra Kerberos fail?

**Answer**: A failure can occur if network connectivity is impeded with the domain controller that runs Windows Server 2025 during join, or if other prerequisites are incomplete.

## Troubleshooting

For help with troubleshooting errors, you can follow these articles:

- [Troubleshoot hybrid joined devices](/en-us/entra/identity/devices/troubleshoot-hybrid-join-windows-current)
- [Enable Kerberos event logging](/en-us/troubleshoot/windows-server/active-directory/enable-kerberos-event-logging)

To collect Kerberos logs, follow these steps:

1. Download and unzip the logging scripts from https://aka.ms/authscripts.
2. If you have multiple domain controllers that run Windows Server 2025, disable KDC services on all of them except one. Run the following command to stop the KDC service on a domain controller:

    ```
    net stop kdc
    ```
3. On the remaining domain controller that runs Windows Server 2025 with the KDC service running, open a PowerShell window with administrator privileges, run the following script:

    ```powershell
    start-auth.ps1
    ```
4. On your client computer, open a PowerShell window with administrator privileges, run the following script:

    ```powershell
    start-auth.ps1
    ```
5. On your client computer, open a cmd window with administrator privileges, run the following command:

    ```
    dsregcmd /join
    ```
6. On your client computer, in the PowerShell window, run the following script:

    ```powershell
    stop-auth.ps1
    ```
7. On your domain controller that runs Windows Server 2025 with the KDC service running, in the PowerShell window, run the following script:

    ```powershell
    stop-auth.ps1
    ```
8. You can restart KDC services on your extra domain controllers that run Windows Server 2025. Run the following command to start the KDC service on a domain controller:

    ```
    net start kdc
    ```

## Kerberos errors

| **Error code** | **Description** | **Reason** | **Resolution** |
| --- | --- | --- | --- |
| DSREG\_TOKEN\_MISSING\_ON\_PREM\_ID(0x801c0095) | The token doesn't contain an on-premises ID. | The Kerberos ticket from the on-premises Kerberos authority doesn't contain information required by Microsoft Entra ID. | On every domain controller that runs Windows Server 2025 within the Active Directory domain, make sure it runs [build 26100.6905](https://support.microsoft.com/topic/october-23-2025-kb5070881-os-build-26100-6905-out-of-band-8e7ac742-6785-4677-87e4-b73dd8ac0122) or later. |
| SEC\_E\_NO\_AUTHENTICATING\_AUTHORITY(0x80090311) | No authority could be contacted for authentication. | No functional domain controller that runs Windows Server 2025 can be contacted. | Install at least one domain controller that runs Windows Server 2025 [build 26100.6905](https://support.microsoft.com/topic/october-23-2025-kb5070881-os-build-26100-6905-out-of-band-8e7ac742-6785-4677-87e4-b73dd8ac0122) or later in the Active Directory domain. Make sure the KDC service is running on this domain controller, and this domain controller can be contacted by the computer trying to perform the hybrid join. Run dcdiag.exe on the domain controller and make sure it's advertising itself. |
| SEC\_E\_TARGET\_UNKNOWN (0x80090303) error code in Kerberos event log: KDC\_ERR\_S\_PRINCIPAL\_UNKNOWN (0x7) | The specified target is unknown or unreachable. |  |  |
| SEC\_E\_LOGON\_DENIED (0x8009030c) error code in Kerberos event log: KDC\_ERR\_NULL\_KEY (0x9) | The logon attempt failed. Kerberos error: `No KerberosKeyInformation Keys found.` | Kerberos key for the Microsoft Entra device registration service principal isn't found. | Add the tag **KerberosPolicy:ExchangeForJwt** to the service principal. |