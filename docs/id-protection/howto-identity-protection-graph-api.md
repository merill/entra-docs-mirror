---
layout: Conceptual
title: Microsoft Graph PowerShell SDK and Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/howto-identity-protection-graph-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Query Microsoft Graph risk detections and associated information from Microsoft Entra ID
ms.topic: how-to
ms.date: 2025-05-27T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
locale: en-us
document_id: 5a1b0992-84f5-43f1-6b18-b690dde9753b
document_version_independent_id: db4234aa-2047-33db-6c8a-19a7b732074b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/howto-identity-protection-graph-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/howto-identity-protection-graph-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/howto-identity-protection-graph-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/5cf46315-b33f-4e99-8224-a1592697eff9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/715d24c3-3683-4219-82c5-1e3c813fb7fc
platformId: 74a3bc2f-4c12-38fb-f00d-b4b7e6779612
---

# Microsoft Graph PowerShell SDK and Microsoft Entra ID Protection - Microsoft Entra ID Protection | Microsoft Learn

Microsoft Graph is the Microsoft unified API endpoint and the home of [Microsoft Entra ID Protection](overview-identity-protection) APIs. This article shows you how to use the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/get-started) to manage risky users with PowerShell. Organizations that want to query the Microsoft Graph APIs directly can use the article, [Tutorial: Identify and remediate risks using Microsoft Graph APIs](/en-us/graph/tutorial-riskdetection-api) to begin that journey.

## Prerequisites

To use the PowerShell commands in this article, you need the following prerequisites:

- Microsoft Graph PowerShell SDK is installed.

    - For more information, see the article [Install the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0&amp;preserve-view=true).
- [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator) role.
- `IdentityRiskEvent.Read.All` and `IdentityRiskyUser.ReadWrite.All` delegated permissions are required.

    - To set the permissions to `IdentityRiskEvent.Read.All` and `IdentityRiskyUser.ReadWrite.All`, run:

    ```powershell
    Connect-MgGraph -Scopes "IdentityRiskEvent.Read.All","IdentityRiskyUser.ReadWrite.All"
    ```
- If you use app-only authentication, see [Use app-only authentication with the Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/app-only?view=graph-powershell-1.0&amp;tabs=azure-portal&amp;preserve-view=true).

    - To register an application with the required application permissions, prepare a certificate and run:

    ```powershell
    Connect-MgGraph -ClientID YOUR_APP_ID -TenantId YOUR_TENANT_ID -CertificateName YOUR_CERT_SUBJECT ## Or -CertificateThumbprint instead of -CertificateName
    ```

## List risky detections using PowerShell

You can retrieve the risk detections by the properties of a risk detection in ID Protection.

```powershell
# List all anonymizedIPAddress risk detections
Get-MgRiskDetection -Filter "RiskType eq 'anonymizedIPAddress'" | Format-Table UserDisplayName, RiskType, RiskLevel, DetectedDateTime

# List all high risk detections for the user 'User01'
Get-MgRiskDetection -Filter "UserDisplayName eq 'User01' and RiskLevel eq 'high'" | Format-Table UserDisplayName, RiskType, RiskLevel, DetectedDateTime

```

## List risky users using PowerShell

You can retrieve the risky users and their risky histories in ID Protection.

```powershell
# List all high risk users
Get-MgRiskyUser -Filter "RiskLevel eq 'high'" | Format-Table UserDisplayName, RiskDetail, RiskLevel, RiskLastUpdatedDateTime

#  List history of a specific user with detailed risk detection
Get-MgRiskyUserHistory -RiskyUserId 00aa00aa-bb11-cc22-dd33-44ee44ee44ee | Format-Table RiskDetail, RiskLastUpdatedDateTime, @{N="RiskDetection";E={($_). Activity.RiskEventTypes}}, RiskState, UserDisplayName

```

## Confirm users compromised using PowerShell

You can confirm users compromised and flag them as high risky users in ID Protection.

```powershell
# Confirm Compromised on two users
Confirm-MgRiskyUserCompromised -UserIds "11bb11bb-cc22-dd33-ee44-55ff55ff55ff","22cc22cc-dd33-ee44-ff55-66aa66aa66aa"
```

## Dismiss risky users using PowerShell

You can bulk dismiss risky users in ID Protection.

```powershell
# Get a list of high risky users which are more than 90 days old
$riskyUsers= Get-MgRiskyUser -Filter "RiskLevel eq 'high'" | where RiskLastUpdatedDateTime -LT (Get-Date).AddDays(-90)
# bulk dismiss the risky users
Invoke-MgDismissRiskyUser -UserIds $riskyUsers.Id
```