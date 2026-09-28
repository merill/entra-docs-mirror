---
layout: Conceptual
title: Conditional Access and Microsoft Entra activity logs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/how-to-view-applied-conditional-access-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to view Conditional Access details in Microsoft Entra activity logs so that you can assess the effect of your policies.
ms.topic: how-to
ms.date: 2024-11-19T00:00:00.0000000Z
ms.reviewer: egreenberg
locale: en-us
document_id: 649454c0-8974-5662-99a1-826c71d93353
document_version_independent_id: 4ae2b83d-95d7-78a9-0583-790a2a52a504
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/how-to-view-applied-conditional-access-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/how-to-view-applied-conditional-access-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/how-to-view-applied-conditional-access-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 29a450ab-7a62-5a03-df56-2a89b1cbb64b
---

# Conditional Access and Microsoft Entra activity logs - Microsoft Entra ID | Microsoft Learn

With Conditional Access policies, you can control how your users get access to your Azure and Microsoft Entra resources. As a tenant admin, you need to be able to determine what effect your Conditional Access policies have on sign-ins to your tenant, so that you can take action if necessary. You might also need to view audit logs for recent changes to Conditional Access policies.

This article explains how to view applied Conditional Access policies in the Microsoft Entra activity logs.

## Prerequisites

To see applied Conditional Access policies in the logs, administrators must have permissions to view *both* the logs and the policies. The least privileged built-in role that grants *both* permissions is *Security Reader*. As a best practice, you should add the Security Reader role to the related administrator accounts.

The following built-in roles grant permissions to *read Conditional Access policies*:

- Security Reader
- Security Administrator
- Conditional Access Administrator

The following built-in roles grant permission to *view activity logs*:

- Reports Reader
- Security Reader
- Security Administrator

### Permissions

If you use a client app or the Microsoft Graph PowerShell module to pull logs from Microsoft Graph, your app needs permissions to receive the `appliedConditionalAccessPolicy` resource from Microsoft Graph. As a best practice, assign `Policy.Read.ConditionalAccess` because it's the least privileged permission.

The following permissions allow a client app to access the activity logs and any applied Conditional Access policies in the logs through Microsoft Graph:

- `Policy.Read.ConditionalAccess`
- `Policy.ReadWrite.ConditionalAccess`
- `Policy.Read.All`
- `AuditLog.Read.All`
- `Directory.Read.All`

To use the Microsoft Graph PowerShell module, you also need the following least privileged permissions with the necessary access:

- To consent to the necessary permissions: `Connect-MgGraph -Scopes Policy.Read.ConditionalAccess, AuditLog.Read.All, Directory.Read.All`
- To view the sign-in logs: `Get-MgAuditLogSignIn`
- To view the audit logs: `Get-MgAuditLogDirectoryAudit`

For more information, see [Get-MgAuditLogSignIn](/en-us/powershell/module/microsoft.graph.reports/get-mgauditlogsignin) and [Get-MgAuditLogDirectoryAudit](/en-us/powershell/module/microsoft.graph.reports/get-mgauditlogdirectoryaudit).

## Conditional Access and sign-in log scenarios

As a Microsoft Entra administrator, you can use the sign-in logs to:

- Troubleshoot sign-in problems.
- Check on feature performance.
- Evaluate the security of a tenant.

Some scenarios require you to get an understanding of how your Conditional Access policies were applied to a sign-in event. Common examples include:

- Helpdesk administrators who need to look at applied Conditional Access policies to understand if a policy is the root cause of a ticket that a user opened.
- Tenant administrators who need to verify that Conditional Access policies have the intended effect on the users of a tenant.

You can access the sign-in logs by using the Microsoft Entra admin center, the Azure portal, Microsoft Graph, and PowerShell.

## How to view Conditional Access policies

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
The activity details of sign-in logs contain several tabs. The **Conditional Access** tab lists the Conditional Access policies applied to that sign-in event.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Select a sign-in item from the table to view the sign-in details pane.
4. Select the **Conditional Access** tab.

If you don't see the Conditional Access policies, confirm you're using a role that provides access to both the sign-in logs and the Conditional Access policies.

# [Microsoft Graph API](#tab/microsoft-graph-api)
Follow these instructions to view Conditional Access policies and log details using the Microsoft Graph API in [Graph Explorer](https://aka.ms/ge).

1. Sign in to the [Graph Explorer](https://aka.ms/ge).
2. Select **GET** as the HTTP method from the dropdown.
3. Select the API version to **v1.0**.
4. To get sign-in attempts where Conditional Access failed during a specific time frame, add the following query and select **Run query**.

    ```http
    GET https://graph.microsoft.com/v1.0/auditLogs/signIns?$filter=(createdDateTime ge 2024-11-01T14:13:32Z and createdDateTime le 2024-11-10T17:43:26Z) and conditionalAccessStatus eq 'failure'
    ```
5. To view a specific Conditional Access policy, add the policy ID.

    ```http
    GET https://graph.microsoft.com/v1.0/identity/conditionalAccess/policies/{id}
    ```

For more information, review the following resources:

- [conditionalAccessPolicy resource type](/en-us/graph/api/resources/conditionalaccesspolicy)
- [signIn resource type](/en-us/graph/api/resources/signin)

# [Microsoft Graph PowerShell](#tab/microsoft-graph-powershell)
Follow these steps to list Microsoft Entra roles using PowerShell.

1. Open a PowerShell window. If necessary, use [Install-Module](/en-us/powershell/module/powershellget/install-module) to install Microsoft Graph PowerShell. For more information, see [Prerequisites to use PowerShell or Graph Explorer](../role-based-access-control/prerequisites).

    ```powershell
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```
2. In a PowerShell window, use [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands#using-connect-mggraph) to sign in to your tenant.

    ```powershell
    Connect-MgGraph -Scopes "Policy.Read.All", "Policy.Read.ConditionalAccess"
    ```
3. Use [Get-MgIdentityConditionalAccessPolicy](/en-us/powershell/module/microsoft.graph.identity.signins/get-mgidentityconditionalaccesspolicy) to get all Conditional Access policies.

    ```powershell
    Get-MgIdentityConditionalAccessPolicy
    ```
4. To format the results as a list, use the following command:

    ```powershell
    Get-MgIdentityConditionalAccessPolicy |Format-List
    ```

The following command can be used to export sign-in logs to a CSV file, formatted to highlight Conditional Access related details.

1. Define the output CSV file path.

    ```powershell
    $PathCsv = "C:\\temp\\ConditionalAccessSignInLogs.csv"
    ```
2. Retrieve the logs, filtered from a specified date, and export them to the CSV file.

    ```powershell
    $SignInLogs = Get-MgAuditLogSignIn -Filter "createdDateTime gt 2024-11-10T05:30:00.0Z" | Select-Object `
    @{Name="ResourceName";Expression={$_.ResourceDisplayName}}, `
    @{Name="User";Expression={$_.UserDisplayName}}, `
    @{Name="IPv4";Expression={$_.IPAddress}}, `
    @{Name="Location";Expression={$_.Location.City}}, `
    @{Name="NamedLocation";Expression={$_.ConditionalAccessLocations}}, `
    @{Name="Success/Failure/ReportOnly";Expression={$_.ConditionalAccessStatus}}, `
    @{Name="FailureReason";Expression={$_.FailureReason}}, `
    @{Name="Details";Expression={$_.ConditionalAccessDetails}}, `
    @{Name="DeviceName";Expression={$_.DeviceDetail.DeviceDisplayName}}, `
    @{Name="ClientApp";Expression={$_.ClientAppUsed}} | 
    Export-Csv -Path $PathCsv -NoTypeInformation
    
    Write-Host "Conditional Access SignInLogs exported to $PathCsv"
    ```

---

## Conditional Access and audit log scenarios

The Microsoft Entra audit logs contain information about changes to Conditional Access policies. You can use the audit logs to find out when a policy was created, updated, or deleted.

To see when an existing Conditional Access policy was updated:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**.
3. Set **Service** filter to **Conditional Access**.
4. Set the **Category** filter to **Policy**.
5. Set the **Activity** filter to **Update Conditional Access policy**.

You might need to adjust the date to see the changes you're looking for. The **Target** column shows the name of the Conditional Access policy that was updated.

To compare the current policy with the previous policy, select the audit log entry and then select the **Modified properties** tab.