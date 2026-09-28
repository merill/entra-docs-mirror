---
layout: Conceptual
title: Restrict password usage on Microsoft Entra apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/block-password-addition
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Block the addition of passwords on Microsoft Entra apps to improve security
ms.reviewer: arcrowe
ms.date: 2025-08-19T00:00:00.0000000Z
ms.topic: how-to
ms.localizationpriority: medium
ms.collection: RestrictedMode
audience: admin
ROBOTS: NOINDEX, NOFOLLOW
locale: en-us
document_id: 68d9feaa-f12a-f8ed-d6b4-ef28c8dec2e2
document_version_independent_id: 68d9feaa-f12a-f8ed-d6b4-ef28c8dec2e2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/block-password-addition.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/block-password-addition
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/block-password-addition.md
platformId: 0569b23b-8bc3-37f9-0f6d-1fa6bfd10ed5
---

# Restrict password usage on Microsoft Entra apps - Microsoft Entra ID | Microsoft Learn

Passwords are one of the weakest methods of service authentication and are vulnerable to compromise by bad actors. Microsoft recommends that organizations switch applications in their tenant to a [more secure credential method](/en-us/entra/identity-platform/security-best-practices-for-app-registration#credentials-including-certificates-and-secrets). This improves security and reduces management overhead.

Tenant administrators can block the addition of new passwords to applications in their tenant. This should eventually deprecate password usage in their organization as apps modernize their credential methods and existing passwords expire. Administrators can also speed up this process by identifying apps with existing passwords and removing them.

## Block password addition

New password addition can be blocked in the Microsoft 365 admin center.

1. Go to the admin center and select Org settings.
2. Select Restricted Mode, find the **Block addition of new password credentials to apps** setting, and switch the toggle to **On**.

Password addition can also be blocked using the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). For more information, see the [app management policy usage documentation](https://aka.ms/app-mgmt-policy-ux-docs).

Enabling this setting blocks the addition of passwords to both new and existing apps. You can gauge the impact of enabling this setting by identifying recent password addition activity. From the Microsoft 365 admin center:

1. Go to the admin center and select Org settings.
2. Select Restricted Mode, find the **Block addition of new password credentials to apps** setting.
3. Select **download report** to view password additions in your organization in the last 30 days.

## Remove existing passwords

Blocking addition of new passwords doesn't affect existing passwords. Existing apps using passwords can be identified using the Microsoft 365 admin center.

1. Go to the admin center and select Org settings.
2. Select Restricted Mode, find the **Block addition of new password credentials to apps** setting.
3. Select **download report** to view existing apps with passwords.

Apps using passwords should be modernized before their existing passwords are removed. Developers should follow the [credential guidance](/en-us/entra/identity-platform/security-best-practices-for-app-registration#credentials-including-certificates-and-secrets) to modernize the apps they own. Passwords on existing applications can be removed using the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade/quickStartType%7E/null/sourceType/Microsoft_AAD_IAM), [Microsoft Graph PowerShell](/en-us/powershell/module/microsoft.graph.applications/remove-mgapplicationpassword), or the [Microsoft Graph API](/en-us/graph/api/application-removepassword?tabs=http).