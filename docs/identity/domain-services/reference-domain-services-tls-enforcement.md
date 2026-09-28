---
layout: Conceptual
title: How to migrate to Transport Layer Security (TLS) 1.2 enforcement for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/reference-domain-services-tls-enforcement
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to enforce TLS 1.2 for a Microsoft Entra Domain Services managed domain.
ms.assetid: 6b4665b5-4324-42ab-82c5-d36c01192c2a
ms.topic: how-to
ms.date: 2025-09-03T00:00:00.0000000Z
ms.reviewer: bochingwa
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
locale: en-us
document_id: d49b4e30-3cd6-05fc-358b-e571d0ab3144
document_version_independent_id: d49b4e30-3cd6-05fc-358b-e571d0ab3144
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/reference-domain-services-tls-enforcement.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/reference-domain-services-tls-enforcement
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/reference-domain-services-tls-enforcement.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: ced8d4d8-50bd-51f6-5369-779b8a3eda75
---

# How to migrate to Transport Layer Security (TLS) 1.2 enforcement for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

Microsoft is enhancing security by disabling TLS versions 1.0 and 1.1 as communicated on November 10, 2023. While the Microsoft implementation of TLS 1.0 and TLS 1.1 versions isn't known to have vulnerabilities, TLS 1.2 or later versions provide improved security features, including perfect forward secrecy and stronger cipher suites. This change helps protect customer data and ensures compliance with industry standards.

Microsoft Entra Domain Services supports TLS versions 1.0 and 1.1, but they're disabled by default. Domain Services has removed the ability to disable **TLS 1.2 Only Mode**. Customers who disable **TLS 1.2 Only Mode** can enable it.

You can use the Azure portal or PowerShell to enable **TLS 1.2 Only Mode**.

## Prerequisites

You need the [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) and [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator) roles in Microsoft Entra ID to change security settings such as **TLS 1.2 Only Mode**.

## Identify applications that use deprecated TLS versions

Before you enable **TLS 1.2 Only Mode**, it's important to identify applications that still use TLS 1.0 or 1.1, and update them or replace them with alternatives that support TLS 1.2. For more information about apps that are expected to be impacted, see [TLS 1.0 and TLS 1.1 deprecation in Windows](/en-us/windows/win32/secauthn/tls-10-11-deprecation-in-windows).

# [Azure portal](#tab/portal)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) and a [Groups Administrator](../role-based-access-control/permissions-reference#groups-administrator).
2. Search for **Domain Services**, and select your Domain Services instance.
3. Select **Security Settings**.
4. If **TLS 1.2 Only Mode** is set to **Disable**, the instance enables TLS versions 1.0 and 1.1. Set **TLS 1.2 Only Mode** to **Enable**, and then click **Save**.

    This change may take about 10 minutes to complete as domain security updates are enforced.

    ![Screenshot that shows how to enable TLS 1.2 Only Mode for Domain Services.](media/reference-domain-services-tls-enforcement/enable.png)

Note

Until June 30, 2026, you can select **Disable** to temporarily allow legacy TLS traffic while you update or replace apps that might fail. Select **Enable** again to remain compliant.

# [PowerShell](#tab/powershell)
1. Install the Az.ADDomainServices module:

    ```powershell
    Install-Module -Name Az.ADDomainServices
    ```
2. Connect to the Azure subscription:

    ```powershell
    Connect-AzAccount -Subscription aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e
    ```
3. Update the value of **TLS 1.2 Only Mode** by executing these two commands:

    ```powershell
    $domainService = Get-AzADDomainService
    ```

    ```powershell
    Update-AzADDomainService -Name $domainService.Name -ResourceGroupName $domainService.ResourceGroupName -DomainSecuritySettingTlsV1 Disabled
    ```

    This command may take about 10 minutes to complete as domain security updates are enforced.

## Troubleshooting

- Some apps provide logs or error messages when TLS handshakes fail. Use application-level diagnostics to look for errors related to unsupported protocols.
- Until June 30, 2026, you can modify the following PowerShell example to temporarily allow legacy TLS traffic while you update or replace apps:

    ```powershell
    Update-AzADDomainService -Name $domainService.Name -ResourceGroupName $domainService.ResourceGroupName -DomainSecuritySettingTlsV1 Enabled
    ```
- For more troubleshooting help, you can [create an Azure support request](/en-us/entra/fundamentals/how-to-get-support).

---