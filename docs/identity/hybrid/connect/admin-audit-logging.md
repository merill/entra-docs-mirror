---
layout: Conceptual
title: Audit Administrator Events in Microsoft Entra Connect Sync - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/admin-audit-logging
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes security improvements to Microsoft Entra Connect Sync and how to enable logging of administrator activities.
ms.topic: how-to
ms.date: 2025-09-25T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: d828370a-68bd-c4bd-f789-3eaf369f980d
document_version_independent_id: d828370a-68bd-c4bd-f789-3eaf369f980d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/admin-audit-logging.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/admin-audit-logging
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/admin-audit-logging.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 48bab101-824b-26ba-4b45-abc12e1d099b
---

# Audit Administrator Events in Microsoft Entra Connect Sync - Microsoft Entra ID | Microsoft Learn

Starting from version [(2.4.129.0)](reference-connect-version-history#241290) of Microsoft Entra Connect Sync, a new admin audit logging feature is available and enabled by default. This feature allows organizations to monitor changes made to Microsoft Entra Connect Sync configurations by Global Administrators, Hybrid Administrators and local server administrators.

Admin actions performed through the Microsoft Entra Connect Sync Wizard, PowerShell, or the Synchronization Rules Editor—such as updates to synchronization rules, authentication settings, and federation settings are captured and logged in Windows Event Viewer Application's event log under a dedicated event source called **Entra Connect Admin Actions**. This provides improved visibility into identity infrastructure changes and supports troubleshooting, operational accountability, and regulatory compliance.

This article outlines the list of events logged by this feature and explains how to disable it, if needed.

## List of logged events

The following table is a list of events that are logged with the new auditing feature. To view the events, use the Event Viewer and view the Application log.

[![Screenshot that shows the Event Viewer.](media/admin-audit-logging/logging-2.png)](media/admin-audit-logging/logging-2.png#lightbox)

Note

We recommend that you increase the application events log size, as the Windows default size of 20MB is relatively small and can be quickly overwritten. A minimum size of 250MB-500MB is suggested.

| Event ID | Event name | Description |
| --- | --- | --- |
| 2603 | Add/Update/Delete directories. | Provides the name of the affected directory. |
| 2604 | Enable Express settings mode. | This event is logged after the administrator selects **Express Setup**. |
| 2605 | Enable/Disable domains and organizational units (OUs) for sync. | Shows a list of all domains connected to Microsoft Entra Connect Sync. |
| 2606 | Enable/Disable password hash synchronization (PHS). | Shows that PHS is enabled or disabled. |
| 2607 | Enable/Disable sync start after installation. | Event is logged when sync is enabled or disabled after the installation is finished. |
| 2608 | Create Active Directory Domain Services (AD DS) account. | Shows the created account needed to connect to the new directory added. |
| 2609 | Use existing AD DS account. | Shows the name of the account used to connect to the directory. |
| 2610 | Create/Update/Delete sync rule. | Shows the name of the sync rule that changed along with information on what changed. |
| 2611 | Enable/Disable domain-based filtering. | Shows that domain filtering is selected and lists selected domains. |
| 2612 | Enable/Disable OU-based filtering. | Shows that OU-based filtering is selected and lists selected OUs. |
| 2613 | User sign-in method changed. | Shows the old sign-in method and the new one. |
| 2614 | Configure new Active Directory Federation Services (AD FS) farm. | Shows the federation services name. |
| 2615 | Enable/Disable single sign-on. | Shows single sign-on change. |
| 2616 | Install web application proxy server. | Shows selected AD FS servers and the domain admin username. |
| 2617 | Set permissions. | Shows the specific ADSync permission that changed. |
| 2618 | Change AD DS Connector credential. | Shows the AD DS Connector credential that changed. |
| 2619 | Reinitialize Microsoft Entra ID Connector account password. | Shows that the ADSync account password was reset. |
| 2620 | Install AD FS server. | Shows the selected server. |
| 2621 | Set AD FS service account. | Specifies if group managed or a domain user. Includes the administrator username. |
| 2622 | `ConfigureEntraApplicationAuthentication` | Specifies that configuring application authentication to Microsoft Entra ID was attempted. It provides the status of the operation along with relevant details like application (client) ID. |
| 2623 | `RotateEntraApplicationCertificate` | Specifies that rotation of the application certificate used for authentication to Microsoft Entra ID was attempted along with the status of the operation. |
| 2624 | `DeleteEntraConnectorAccount` | Specifies that deletion of the Microsoft Entra ID synchronization account was attempted. It provides the status of the operation along with the name of the account. |
| 2625 | `DeleteEntraApplication` | Specifies that deletion of the Microsoft Entra Connect Sync application used for synchronizing with Microsoft Entra ID was attempted. It provides the application (client) ID along with the status of the operation. |
| 2626 | `DeleteApplicationCertificate` | Specifies that deletion of the Microsoft Entra Connect Sync application certificate was attempted. It provides the application (client) ID and the certificate ID along with the status of the operation. |

## Disable auditing of administrator events

### Use the Registry Editor

To disable auditing of administrator events, follow these steps:

1. Open the Registry Editor. Select **Win+R** to open the **run** dialog.
2. Enter **regedit** and select **Enter** to open the Registry Editor. Confirm any security prompts to proceed.
3. Go to **HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Azure AD Connect**.
4. Right-click the **Azure AD Connect** key to modify or create the **AuditEventLogging** value. Select **New** and select the **DWORD (32-bit)** value if the **AuditEventLogging** value doesn't already exist.
5. Name the new **DWORD** as **AuditEventLogging**.
6. Double-click the **AuditEventLogging** entry and enter **0** to disable the audit event logging. Enter **1** to reenable it.

[![Screenshot that shows the new AuditEventLogging registry key.](media/admin-audit-logging/logging-1.png)](media/admin-audit-logging/logging-1.png#lightbox)

### Use PowerShell

You can also use PowerShell to disable audit logging of administrator events. Use the following script:

```powershell
#Declare variables
$registryPath = 'HKLM:\SOFTWARE\Microsoft\Azure AD Connect'
$valueName = 'AuditEventLogging'
$newValue = '0'

#Create the AuditEventLogging key if it doesn't exist
if (!(Test-Path $registryPath)) {New-Item -Path $registryPath -Force}

#Set the value of the new AuditEventLogging key
Set-ItemProperty -Path $registryPath -Name $valueName -Value $newValue
```