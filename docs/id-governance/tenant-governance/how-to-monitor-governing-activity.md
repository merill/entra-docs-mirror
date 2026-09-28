---
layout: Conceptual
title: Monitor governing tenant admin activity in a governed tenant - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/how-to-monitor-governing-activity
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to monitor and audit governing tenant administrator activity in your governed tenant using sign-in and audit logs
ms.topic: how-to
ms.date: 2026-03-10T00:00:00.0000000Z
locale: en-us
document_id: 648bfc41-570b-62d8-1e72-e7a71a46c44d
document_version_independent_id: 648bfc41-570b-62d8-1e72-e7a71a46c44d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/how-to-monitor-governing-activity.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/how-to-monitor-governing-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/how-to-monitor-governing-activity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: c52d5db2-2110-30fd-1e61-74c6e37d7c38
---

# Monitor governing tenant admin activity in a governed tenant - Microsoft Entra ID Governance | Microsoft Learn

After you establish a governance relationship between a governing tenant and a governed tenant, administrators from the governing tenant can sign in to the governed tenant using their governing tenant credentials through granular delegated admin privileges (GDAP). As a governed tenant admin, monitor these activities through sign-in logs and audit logs. This monitoring helps maintain security visibility and ensures that governing tenant admins operate within their authorized scope.

This article describes how to identify, review, and monitor the activities that governing tenant administrators perform in your governed tenant.

## Prerequisites

- An active governance relationship between the governing tenant and your governed tenant.
- One of these roles assigned in the governed tenant:

    - [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader)
    - [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader)
    - [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)
    - [Global Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#global-reader)
    - [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator)
- Access to the [Microsoft Entra admin center](https://entra.microsoft.com).

## Identify governing tenant administrators in logs

Governing tenant administrators who sign in to the governed tenant through GDAP appear differently from regular users in your logs. Understanding how to identify them is the first step in monitoring their activity.

When a governing tenant admin signs in to your governed tenant:

- **User display name** in sign-in logs and audit logs appears as: **"{Governing tenant name} Technician"**. For example, if the governing tenant is named "Contoso IT," the display name shows as "Contoso IT Technician."
- **Username** appears in the format: **user\_{user object ID in the governing tenant without dashes}**. For example, `user_a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4`.

## Review sign-in logs for governing tenant admin activity

Use sign-in logs to monitor when and how governing tenant administrators sign in to your governed tenant.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../../identity/role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Identity** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. To filter for governing tenant admin sign-ins, select **Add filters**.
4. Select the **User** filter, and enter **Technician** as the search term to find entries matching the "{Governing tenant name} Technician" display name format.
5. Select **Apply** to view the filtered results.
6. Select a sign-in entry to view details, including:

    - **Date and time** of the sign-in.
    - **Application** the admin accessed.
    - **Status** indicating whether the sign-in succeeded or failed.
    - **Conditional Access** policies that Microsoft Entra evaluated or applied.

## Review audit logs for governing tenant admin actions

Use audit logs to track the specific actions and changes that governing tenant administrators make in your governed tenant.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../../identity/role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Identity** &gt; **Monitoring & health** &gt; **Audit logs**.
3. To filter for actions performed by governing tenant admins, select **Add filters**.
4. Select the **Initiated by (actor)** filter. This filter uses a `startsWith` match. Enter the governing tenant's name (for example, **Contoso IT**) to find entries where the actor starts with the governing tenant name and matches the "{Governing tenant name} Technician" display name format.
5. Select **Apply** to view the filtered results.
6. Review the audit entries, which include:

    - **Activity** describing the action the admin performed (for example, "Update user," "Add member to role").
    - **Date and time** the action occurred.
    - **Target resource(s)** that the admin modified.
    - **Result** indicating whether the action succeeded or failed.
7. Select an individual entry to view the full details, including which properties changed and their old and new values.