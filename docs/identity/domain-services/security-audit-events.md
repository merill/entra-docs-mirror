---
layout: Conceptual
title: Enable security and DNS audits for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/security-audit-events
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to enable security audits to centralize the logging of events for analysis and alerts in Microsoft Entra Domain Services
ms.assetid: 662362c3-1a5e-4e94-ae09-8e4254443697
ms.topic: how-to
ms.date: 2025-02-19T00:00:00.0000000Z
ms.custom: devx-track-azurepowershell
locale: en-us
document_id: dbe5ec6d-e6db-03df-4dcf-81cfff6246b4
document_version_independent_id: 4b56a82d-0387-adbd-2e91-3262b905b007
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/security-audit-events.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/security-audit-events
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/security-audit-events.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/9949a35d-c893-4f91-bf98-ae940fc30f5f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/21f7bb14-0703-4e59-a64b-65dd13773dd3
platformId: 60cc7653-e0e2-176d-e2bd-5f69beb7cc12
---

# Enable security and DNS audits for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Domain Services security and DNS audits let Azure stream events to targeted resources. These resources include Azure Storage, Azure Log Analytics workspaces, or Azure Event Hubs. After you enable security audit events, Domain Services sends all the audited events for the selected category to the targeted resource.

You can archive events into Azure storage and stream events into security information and event management (SIEM) software (or equivalent) using Azure Event Hubs, or do your own analysis and using Azure Log Analytics workspaces from the Microsoft Entra admin center.

## Security audit destinations

You can use Azure Storage, Azure Event Hubs, or Azure Log Analytics workspaces as a target resource for Domain Services security audits. These destinations can be combined. For example, you could use Azure Storage for archiving security audit events, but an Azure Log Analytics workspace to analyze and report on the information in the short term.

The following table outlines scenarios for each destination resource type.

Important

You need to create the target resource before you enable Domain Services security audits. You can create these resources using the Microsoft Entra admin center, Azure PowerShell, or the Azure CLI.

| Target Resource | Scenario |
| --- | --- |
| Azure Storage | This target should be used when your primary need is to store security audit events for archival purposes. Other targets can be used for archival purposes, however those targets provide capabilities beyond the primary need of archiving. Before you enable Domain Services security audit events, first [Create an Azure Storage account](/en-us/azure/storage/common/storage-account-create). |
| Azure Event Hubs | This target should be used when your primary need is to share security audit events with additional software such as data analysis software or security information & event management (SIEM) software.Before you enable Domain Services security audit events, [Create an event hub using Microsoft Entra admin center](/en-us/azure/event-hubs/event-hubs-create) |
| Azure Log Analytics Workspace | This target should be used when your primary need is to analyze and review secure audits from the Microsoft Entra admin center directly.Before you enable Domain Services security audit events, [Create a Log Analytics workspace in the Microsoft Entra admin center.](/en-us/azure/azure-monitor/logs/quick-create-workspace) |

## Enable security audit events using the Microsoft Entra admin center

To enable Domain Services security audit events using the Microsoft Entra admin center, complete the following steps.

Important

Domain Services security audits aren't retroactive. You can't retrieve or replay events from the past. Domain Services can only send events that occur after security audits are enabled.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Search for and select **Microsoft Entra Domain Services**. Choose your managed domain, such as *aaddscontoso.com*.
3. In the Domain Services window, select **Diagnostic settings** on the left-hand side.
4. No diagnostics are configured by default. To get started, select **Add diagnostic setting**.

    ![Add a diagnostic setting for Microsoft Entra Domain Services](media/security-audit-events/add-diagnostic-settings.png)
5. Enter a name for the diagnostic configuration, such as *aadds-auditing*.

    Check the box for the security or DNS audit destination you want. You can choose from a Log Analytics workspace, an Azure Storage account, an Azure event hub, or a partner solution. These destination resources must already exist in your Azure subscription. You can't create the destination resources in this wizard.

    - **Azure Log Analytic workspaces**
        - Select **Send to Log Analytics**, then choose the **Subscription** and **Log Analytics Workspace** you want to use to store audit events.
    - **Azure storage**
        - Select **Archive to a storage account**, then choose **Configure**.
        - Select the **Subscription** and the **Storage account** you want to use to archive audit events.
        - When ready, choose **OK**.
    - **Azure event hubs**
        - Select **Stream to an event hub**, then choose **Configure**.
        - Select the **Subscription** and the **Event hub namespace**. If needed, also choose an **Event hub name** and then **Event hub policy name**.
        - When ready, choose **OK**.
    - **Partner solution**
        - Select **Send to partner solution**, then choose the **Subscription** and **Destination** you want to use to store audit events.
6. Select the log categories you want included for the particular target resource. If you send the audit events to an Azure Storage account, you can also configure a retention policy that defines the number of days to retain data. A default setting of *0* retains all data and doesn't rotate events after a period of time.

    You can select different log categories for each targeted resource within a single configuration. This ability lets you choose which logs categories you want to keep for Log Analytics and which logs categories you want to archive, for example.
7. When done, select **Save** to commit your changes. The target resources start to receive Domain Services audit events soon after the configuration is saved.

## Enable security and DNS audit events using Azure PowerShell

To enable Domain Services security and DNS audit events using Azure PowerShell, complete the following steps. If needed, first [install the Azure PowerShell module and connect to your Azure subscription](/en-us/powershell/azure/install-azure-powershell).

Important

Domain Services audits aren't retroactive. You can't retrieve or replay events from the past. Domain Services can only send events that occur after audits are enabled.

1. Authenticate to your Azure subscription using the [Connect-AzAccount](/en-us/powershell/module/Az.Accounts/Connect-AzAccount) cmdlet. When prompted, enter your account credentials.

    ```azurepowershell
    Connect-AzAccount
    ```
2. Create the target resource for the audit events.

    - **Azure Log Analytic workspaces** - [Create a Log Analytics workspace with Azure PowerShell](/en-us/azure/azure-monitor/logs/powershell-workspace-configuration).
    - **Azure storage** - [Create a storage account using Azure PowerShell](/en-us/azure/storage/common/storage-account-create?tabs=azure-powershell)
    - **Azure event hubs** - [Create an event hub using Azure PowerShell](/en-us/azure/event-hubs/event-hubs-quickstart-powershell). You may also need to use the [New-AzEventHubAuthorizationRule](/en-us/powershell/module/az.eventhub/new-azeventhubauthorizationrule) cmdlet to create an authorization rule that grants Domain Services permissions to the event hub *namespace*. The authorization rule must include the **Manage**, **Listen**, and **Send** rights.

        Important

        Ensure you set the authorization rule on the event hub namespace and not the event hub itself.
3. Get the resource ID for your Domain Services managed domain using the [Get-AzResource](/en-us/powershell/module/az.resources/get-azresource) cmdlet. Create a variable named *$aadds.ResourceId* to hold the value:

    ```azurepowershell
    $aadds = Get-AzResource -name aaddsDomainName
    ```
4. Configure the Azure Diagnostic settings using the [Set-AzDiagnosticSetting](/en-us/powershell/module/az.monitor/set-azdiagnosticsetting) cmdlet to use the target resource for Microsoft Entra Domain Services audit events. In the following examples, the variable *$aadds.ResourceId* is used from the previous step.

    - **Azure storage** - Replace *storageAccountId* with your storage account name:

        ```powershell
        Set-AzDiagnosticSetting `
            -ResourceId $aadds.ResourceId `
            -StorageAccountId storageAccountId `
            -Enabled $true
        ```
    - **Azure event hubs** - Replace *eventHubName* with the name of your event hub and *eventHubRuleId* with your authorization rule ID:

        ```powershell
        Set-AzDiagnosticSetting -ResourceId $aadds.ResourceId `
            -EventHubName eventHubName `
            -EventHubAuthorizationRuleId eventHubRuleId `
            -Enabled $true
        ```
    - **Azure Log Analytic workspaces** - Replace *workspaceId* with the ID of the Log Analytics workspace:

        ```powershell
        Set-AzureRmDiagnosticSetting -ResourceId $aadds.ResourceId `
            -WorkspaceID workspaceId `
            -Enabled $true
        ```

## Query and view security and DNS audit events using Azure Monitor

Log Analytic workspaces let you view and analyze the security and DNS audit events using Azure Monitor and the Kusto query language. This query language is designed for read-only use that boasts power analytic capabilities with an easy-to-read syntax. For more information to get started with Kusto query languages, see the following articles:

- [Azure Monitor documentation](/en-us/azure/azure-monitor/)
- [Get started with Log Analytics in Azure Monitor](/en-us/azure/azure-monitor/logs/log-analytics-tutorial)
- [Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries)
- [Create and share dashboards of Log Analytics data](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)

The following sample queries can be used to start analyzing audit events from Domain Services.

### Sample query 1

View all the account lockout events for the last seven days:

```Kusto
AADDomainServicesAccountManagement
| where TimeGenerated >= ago(7d)
| where OperationName has "4740"
```

### Sample query 2

View all the account lockout events (*4740*) between June 3, 2020 at 9 a.m. and June 10, 2020 midnight, sorted ascending by the date and time:

```Kusto
AADDomainServicesAccountManagement
| where TimeGenerated >= datetime(2020-06-03 09:00) and TimeGenerated <= datetime(2020-06-10)
| where OperationName has "4740"
| sort by TimeGenerated asc
```

### Sample query 3

View account sign-in events seven days ago (from now) for the account named user:

```Kusto
AADDomainServicesAccountLogon
| where TimeGenerated >= ago(7d)
| where "user" == tolower(extract("Logon Account:\t(.+[0-9A-Za-z])",1,tostring(ResultDescription)))
```

### Sample query 4

View account sign-in events seven days ago from now for the account named user that attempted to sign in using a bad password (*0xC0000006a*):

```Kusto
AADDomainServicesAccountLogon
| where TimeGenerated >= ago(7d)
| where "user" == tolower(extract("Logon Account:\t(.+[0-9A-Za-z])",1,tostring(ResultDescription)))
| where "0xc000006a" == tolower(extract("Error Code:\t(.+[0-9A-Fa-f])",1,tostring(ResultDescription)))
```

### Sample query 5

View account sign-in events seven days ago from now for the account named user that attempted to sign in while the account was locked out (*0xC0000234*):

```Kusto
AADDomainServicesAccountLogon
| where TimeGenerated >= ago(7d)
| where "user" == tolower(extract("Logon Account:\t(.+[0-9A-Za-z])",1,tostring(ResultDescription)))
| where "0xc0000234" == tolower(extract("Error Code:\t(.+[0-9A-Fa-f])",1,tostring(ResultDescription)))
```

### Sample query 6

View the number of account sign-in events seven days ago from now for all sign-in attempts that occurred for all locked out users:

```Kusto
AADDomainServicesAccountLogon
| where TimeGenerated >= ago(7d)
| where "0xc0000234" == tolower(extract("Error Code:\t(.+[0-9A-Fa-f])",1,tostring(ResultDescription)))
| summarize count()
```

### Sample query 7

View all Kerberos ticket-granting (event ID 4768) and service ticket (event ID 4769) events that used RC4 encryption in the last seven days, to identify workloads and service accounts that still rely on RC4:

```Kusto
let EncryptionTypeFromHex = (hex_value: int) {
    case(
        hex_value == 0x1, "DES-CRC",
        hex_value == 0x3, "DES-MD5",
        hex_value == 0x11, "AES128-SHA96",
        hex_value == 0x12, "AES256-SHA96",
        hex_value == 0x13, "AES128-SHA256",
        hex_value == 0x14, "AES256-SHA384",
        hex_value == 0x17, "RC4",
        "Unknown"
    )
};
AADDomainServicesAccountLogon
| where TimeGenerated >= ago(7d)
| where OperationName has "4768" or OperationName has "4769"
| parse ResultDescription with * "Ticket Encryption Type:\t" EncryptionType "\n" *
| where EncryptionType has "0x17"
| parse ResultDescription with * "Account Name:\t\t" AccountName "\n" *
| parse ResultDescription with * "Service Name:\t\t" ServiceName "\n" *
| extend EncryptionTypeName = EncryptionTypeFromHex(toint(EncryptionType))
| project TimeGenerated, OperationName, AccountName, ServiceName, EncryptionType, EncryptionTypeName
| summarize Count = count() by AccountName, ServiceName, EncryptionType, EncryptionTypeName
| order by Count desc
```

Tip

Encryption type `0x17` indicates RC4-HMAC. Use this query to identify RC4 dependencies before disabling RC4 in your managed domain's [security settings](secure-your-domain). For more information about the RC4 deprecation timeline, see [CVE-2026-20833](https://www.cve.org/CVERecord?id=CVE-2026-20833).

## Audit security and DNS event categories

Domain Services security and DNS audits align with traditional auditing for traditional AD DS domain controllers. In hybrid environments, you can reuse existing audit patterns so the same logic may be used when analyzing the events. Depending on the scenario you need to troubleshoot or analyze, the different audit event categories need to be targeted.

The following audit event categories are available:

| Audit Category Name | Description |
| --- | --- |
| Account Logon | Audits attempts to authenticate account data on a domain controller or on a local Security Accounts Manager (SAM).-Logon and Logoff policy settings and events track attempts to access a particular computer. Settings and events in this category focus on the account database that is used. This category includes the following subcategories:-[Audit Credential Validation](/en-us/windows/security/threat-protection/auditing/audit-credential-validation)-[Audit Kerberos Authentication Service](/en-us/windows/security/threat-protection/auditing/audit-kerberos-authentication-service)-[Audit Kerberos Service Ticket Operations](/en-us/windows/security/threat-protection/auditing/audit-kerberos-service-ticket-operations)-[Audit Other Logon/Logoff Events](/en-us/windows/security/threat-protection/auditing/audit-other-logonlogoff-events) |
| Account Management | Audits changes to user and computer accounts and groups. This category includes the following subcategories:-[Audit Application Group Management](/en-us/windows/security/threat-protection/auditing/audit-application-group-management)-[Audit Computer Account Management](/en-us/windows/security/threat-protection/auditing/audit-computer-account-management)-[Audit Distribution Group Management](/en-us/windows/security/threat-protection/auditing/audit-distribution-group-management)-[Audit Other Account Management](/en-us/windows/security/threat-protection/auditing/audit-other-account-management-events)-[Audit Security Group Management](/en-us/windows/security/threat-protection/auditing/audit-security-group-management)-[Audit User Account Management](/en-us/windows/security/threat-protection/auditing/audit-user-account-management) |
| DNS Server | Audits changes to DNS environments. This category includes the following subcategories: - [DNSServerAuditsDynamicUpdates (preview)](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn800669%28v=ws.11%29#audit-and-analytic-event-logging)- [DNSServerAuditsGeneral (preview)](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn800669%28v=ws.11%29#audit-and-analytic-event-logging) |
| Detail Tracking | Audits activities of individual applications and users on that computer, and to understand how a computer is being used. This category includes the following subcategories:-[Audit DPAPI Activity](/en-us/windows/security/threat-protection/auditing/audit-dpapi-activity)-[Audit PNP activity](/en-us/windows/security/threat-protection/auditing/audit-pnp-activity)-[Audit Process Creation](/en-us/windows/security/threat-protection/auditing/audit-process-creation)-[Audit Process Termination](/en-us/windows/security/threat-protection/auditing/audit-process-termination)-[Audit RPC Events](/en-us/windows/security/threat-protection/auditing/audit-rpc-events) |
| Directory Services Access | Audits attempts to access and modify objects in Active Directory Domain Services (AD DS). These audit events are logged only on domain controllers. This category includes the following subcategories:-[Audit Detailed Directory Service Replication](/en-us/windows/security/threat-protection/auditing/audit-detailed-directory-service-replication)-[Audit Directory Service Access](/en-us/windows/security/threat-protection/auditing/audit-directory-service-access)-[Audit Directory Service Changes](/en-us/windows/security/threat-protection/auditing/audit-directory-service-changes)-[Audit Directory Service Replication](/en-us/windows/security/threat-protection/auditing/audit-directory-service-replication) |
| Logon-Logoff | Audits attempts to log on to a computer interactively or over a network. These events are useful for tracking user activity and identifying potential attacks on network resources. This category includes the following subcategories:-[Audit Account Lockout](/en-us/windows/security/threat-protection/auditing/audit-account-lockout)-[Audit User/Device Claims](/en-us/windows/security/threat-protection/auditing/audit-user-device-claims)-[Audit IPsec Extended Mode](/en-us/windows/security/threat-protection/auditing/audit-ipsec-extended-mode)-[Audit Group Membership](/en-us/windows/security/threat-protection/auditing/audit-group-membership)-[Audit IPsec Main Mode](/en-us/windows/security/threat-protection/auditing/audit-ipsec-main-mode)-[Audit IPsec Quick Mode](/en-us/windows/security/threat-protection/auditing/audit-ipsec-quick-mode)-[Audit Logoff](/en-us/windows/security/threat-protection/auditing/audit-logoff)-[Audit Logon](/en-us/windows/security/threat-protection/auditing/audit-logon)-[Audit Network Policy Server](/en-us/windows/security/threat-protection/auditing/audit-network-policy-server)-[Audit Other Logon/Logoff Events](/en-us/windows/security/threat-protection/auditing/audit-other-logonlogoff-events)-[Audit Special Logon](/en-us/windows/security/threat-protection/auditing/audit-special-logon) |
| Object Access | Audits attempts to access specific objects or types of objects on a network or computer. This category includes the following subcategories:-[Audit Application Generated](/en-us/windows/security/threat-protection/auditing/audit-application-generated)-[Audit Certification Services](/en-us/windows/security/threat-protection/auditing/audit-certification-services)-[Audit Detailed File Share](/en-us/windows/security/threat-protection/auditing/audit-detailed-file-share)-[Audit File Share](/en-us/windows/security/threat-protection/auditing/audit-file-share)-[Audit File System](/en-us/windows/security/threat-protection/auditing/audit-file-system)-[Audit Filtering Platform Connection](/en-us/windows/security/threat-protection/auditing/audit-filtering-platform-connection)-[Audit Filtering Platform Packet Drop](/en-us/windows/security/threat-protection/auditing/audit-filtering-platform-packet-drop)-[Audit Handle Manipulation](/en-us/windows/security/threat-protection/auditing/audit-handle-manipulation)-[Audit Kernel Object](/en-us/windows/security/threat-protection/auditing/audit-kernel-object)-[Audit Other Object Access Events](/en-us/windows/security/threat-protection/auditing/audit-other-object-access-events)-[Audit Registry](/en-us/windows/security/threat-protection/auditing/audit-registry)-[Audit Removable Storage](/en-us/windows/security/threat-protection/auditing/audit-removable-storage)-[Audit SAM](/en-us/windows/security/threat-protection/auditing/audit-sam)-[Audit Central Access Policy Staging](/en-us/windows/security/threat-protection/auditing/audit-central-access-policy-staging) |
| Policy Change | Audits changes to important security policies on a local system or network. Policies are typically established by administrators to help secure network resources. Monitoring changes or attempts to change these policies can be an important aspect of security management for a network. This category includes the following subcategories:-[Audit Audit Policy Change](/en-us/windows/security/threat-protection/auditing/audit-audit-policy-change)-[Audit Authentication Policy Change](/en-us/windows/security/threat-protection/auditing/audit-authentication-policy-change)-[Audit Authorization Policy Change](/en-us/windows/security/threat-protection/auditing/audit-authorization-policy-change)-[Audit Filtering Platform Policy Change](/en-us/windows/security/threat-protection/auditing/audit-filtering-platform-policy-change)-[Audit MPSSVC Rule-Level Policy Change](/en-us/windows/security/threat-protection/auditing/audit-mpssvc-rule-level-policy-change)-[Audit Other Policy Change](/en-us/windows/security/threat-protection/auditing/audit-other-policy-change-events) |
| Privilege Use | Audits the use of certain permissions on one or more systems. This category includes the following subcategories:-[Audit Non-Sensitive Privilege Use](/en-us/windows/security/threat-protection/auditing/audit-non-sensitive-privilege-use)-[Audit Sensitive Privilege Use](/en-us/windows/security/threat-protection/auditing/audit-sensitive-privilege-use)-[Audit Other Privilege Use Events](/en-us/windows/security/threat-protection/auditing/audit-other-privilege-use-events) |
| System | Audits system-level changes to a computer not included in other categories and that have potential security implications. This category includes the following subcategories:-[Audit IPsec Driver](/en-us/windows/security/threat-protection/auditing/audit-ipsec-driver)-[Audit Other System Events](/en-us/windows/security/threat-protection/auditing/audit-other-system-events)-[Audit Security State Change](/en-us/windows/security/threat-protection/auditing/audit-security-state-change)-[Audit Security System Extension](/en-us/windows/security/threat-protection/auditing/audit-security-system-extension)-[Audit System Integrity](/en-us/windows/security/threat-protection/auditing/audit-system-integrity) |

## Event IDs per category

Domain Services security and DNS audits record the following event IDs when the specific action triggers an auditable event:

| Event Category Name | Event IDs |
| --- | --- |
| Account Logon security | 4767, 4774, 4775, 4776, 4777 |
| Kerberos Tickets | 4768, 4769 |
| Account Management security | 4720, 4722, 4723, 4724, 4725, 4726, 4727, 4728, 4729, 4730, 4731, 4732, 4733, 4734, 4735, 4737, 4738, 4740, 4741, 4742, 4743, 4754, 4755, 4756, 4757, 4758, 4764, 4765, 4766, 4780, 4781, 4782, 4793, 4798, 4799, 5376, 5377 |
| Detail Tracking security | None |
| DNS Server | 513-523, 525-531, 533-537, 540-582 |
| DS Access security | 5136, 5137, 5138, 5139, 5141 |
| Logon-Logoff security | 4624, 4625, 4634, 4647, 4648, 4672, 4675, 4964 |
| Object Access security | None |
| Policy Change security | 4670, 4703, 4704, 4705, 4706, 4707, 4713, 4715, 4716, 4717, 4718, 4719, 4739, 4864, 4865, 4866, 4867, 4904, 4906, 4911, 4912 |
| Privilege Use security | 4985 |
| System security | 4612, 4621 |