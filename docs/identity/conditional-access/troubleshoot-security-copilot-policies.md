---
layout: Conceptual
title: Troubleshoot Conditional Access policies for Microsoft Security Copilot - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/troubleshoot-security-copilot-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Security Copilot Conditional Access - Learn to create, assign, and troubleshoot policies using custom security attributes for better protection.
ms.topic: troubleshooting
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: lhuangnorth
locale: en-us
document_id: 0cfef338-6c93-04e0-aed6-aed9e3c9942e
document_version_independent_id: 0cfef338-6c93-04e0-aed6-aed9e3c9942e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/troubleshoot-security-copilot-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/troubleshoot-security-copilot-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/troubleshoot-security-copilot-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: caafd8d0-d0bd-8860-77d2-d79c9d5f6df3
---

# Troubleshoot Conditional Access policies for Microsoft Security Copilot - Microsoft Entra ID | Microsoft Learn

## Overview

[Generative artificial intelligence (AI)](/en-us/ai/playbook/technology-guidance/generative-ai/) services like [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot) can bring value to your organization when used appropriately.

Apply Conditional Access policy to these generative AI services by following [our recommendation to target all resources](concept-conditional-access-cloud-apps#conditional-access-for-all-resources). These policies might include those for [all users](policy-all-users-mfa-strength), risky [users](policy-risk-based-user), [sign-ins](policy-risk-based-sign-in), [device compliance](policy-all-users-device-compliance), and users with [insider risk](policy-risk-based-insider-block).

Some organizations target these services directly by using the underlying service principals and custom security attributes in their Conditional Access policies:

- 43d7b169-1d9e-4d32-8cd8-06c5974ed90c - Security Copilot Agent Management
- bb5ffd56-39eb-458c-a53a-775ba21277da - Security Copilot Portal
- bb3d68c2-d09e-4455-94a0-e323996dbaa3 - Security Copilot API
- b0cf1501-8e0f-4fbb-b70a-52ca5ea7bda6 - Security Copilot Logic Apps Connector

In these cases, admins create, assign, and target these underlying service principals with custom security attributes.

## Required roles

Custom security attributes are security sensitive and only delegated users can manage them. Assign one or more of the following roles to the user who manages or reports on these attributes.

| Role name | Description |
| --- | --- |
| [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator) | Assign custom security attribute keys and values to supported Microsoft Entra objects. |
| [Attribute Assignment Reader](../role-based-access-control/permissions-reference#attribute-assignment-reader) | Read custom security attribute keys and values for supported Microsoft Entra objects. |
| [Attribute Definition Administrator](../role-based-access-control/permissions-reference#attribute-definition-administrator) | Define and manage the definition of custom security attributes. |
| [Attribute Definition Reader](../role-based-access-control/permissions-reference#attribute-definition-reader) | Read the definition of custom security attributes. |

Assign the appropriate role to the users who manage or report on these attributes at the directory scope. For detailed steps, see [Assign Microsoft Entra roles](../role-based-access-control/manage-roles-portal#assign-roles-with-tenant-scope).

Important

By default, [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

## Create custom security attributes

Follow the instructions in the article [Add or deactivate custom security attributes in Microsoft Entra ID](../../fundamentals/custom-security-attributes-add) to add the following **Attribute set** and **New attributes**.

- Create an **Attribute set** named *SecurityCopilotAttributeSet*.
- Create **New attributes** named *SecurityCopilotAttribute* with **Allow multiple values to be assigned** set to **No** and **Only allow predefined values to be assigned** set to **Yes**. Add the following predefined value:
    - MFARequired

Note

Conditional Access filters for applications only work with custom security attributes of type "string". Custom security attributes support creating the Boolean data type, but Conditional Access Policy only supports "string".

## Assign custom security attributes to applications

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) and [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select the apps to apply a custom security attribute to:
    1. 43d7b169-1d9e-4d32-8cd8-06c5974ed90c - Security Copilot Agent Management
    2. bb5ffd56-39eb-458c-a53a-775ba21277da - Security Copilot Portal
    3. bb3d68c2-d09e-4455-94a0-e323996dbaa3 - Security Copilot API
    4. b0cf1501-8e0f-4fbb-b70a-52ca5ea7bda6 - Security Copilot Logic Apps Connector
4. Under **Manage** &gt; **Custom security attributes**, select **Add assignment**.
5. Under **Attribute set**, select the attribute set you created.
6. Under **Attribute name**, select the attribute you created.
7. Under **Assigned values**, select **Add values**, choose the value you created from the list, then select **Done**.
8. Select **Save**.

## Targeting custom security attributes in Conditional Access policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) and [Attribute Definition Reader](../role-based-access-control/permissions-reference#attribute-definition-reader).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **New policy** or select an existing policy to update.
4. When configuring your **Target resources**, select the following options:
    1. Select what this policy applies to **Resources (formerly cloud apps)**.
    2. Include **Select resources**.
    3. Select **Edit filter**.
    4. Set **Configure** to **Yes**.
    5. Select the **Attribute** you created.
    6. Set **Operator** to **Contains**.
    7. Set **Value** to one of your custom attributes.
    8. Select **Done**.

## Which policy is causing issues?

It's sometimes hard for an admin to check which policy to update when there's an issue. Use the guidance in [Troubleshooting sign-in problems with Conditional Access](troubleshoot-conditional-access#microsoft-entra-sign-in-events) to check which policies apply, which policies don't apply, and run sign-in diagnostics to avoid ongoing issues.