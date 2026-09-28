---
layout: Conceptual
title: Require MFA for Azure management with Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-old-require-mfa-azure-mgmt
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Create a custom Conditional Access policy to require multifactor authentication for Azure management tasks.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: 22df42c6-831d-ba42-8224-27176e8fd7d9
document_version_independent_id: 15299b18-e361-9e9f-f836-f37a466dcae0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-old-require-mfa-azure-mgmt.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-old-require-mfa-azure-mgmt
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-old-require-mfa-azure-mgmt.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 084a79d4-7c3f-29c6-68b7-3113de6cbcb4
---

# Require MFA for Azure management with Conditional Access - Microsoft Entra ID | Microsoft Learn

## Overview

Organizations use many Azure services and manage them from Azure Resource Manager based tools like:

- Azure portal
- Azure PowerShell
- Azure CLI

These tools can provide highly privileged access to resources that can make the following changes:

- Alter subscription-wide configurations
- Service settings
- Subscription billing

To protect these privileged resources, Microsoft recommends requiring multifactor authentication for any user accessing these resources. In Microsoft Entra ID, these tools are grouped together in a suite called [Windows Azure Service Management API](concept-conditional-access-cloud-apps#windows-azure-service-management-api). For Azure Government, this suite should be the Azure Government Cloud Management API app.

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Create a Conditional Access policy

The following steps help create a Conditional Access policy to require users who access the [Windows Azure Service Management API](concept-conditional-access-cloud-apps#windows-azure-service-management-api) suite do multifactor authentication.

Caution

Make sure you understand how Conditional Access works before setting up a policy to manage access to Windows Azure Service Management API. Make sure you don't create conditions that could block your own access to the portal.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include** &gt; **Select resources**, choose **Windows Azure Service Management API**, and select **Select**.
7. Under **Access controls** &gt; **Grant**, select **Grant access**, **Require multifactor authentication**, and select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.