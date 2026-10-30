---
layout: Conceptual
title: Troubleshoot custom security attributes in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn how to troubleshoot custom security attributes in Microsoft Entra ID.
ms.topic: troubleshooting
ms.date: 2024-11-27T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5df84e2a-b4ef-1692-b3b3-cc2bd68aacd3
document_version_independent_id: 4e97285e-6aae-4928-69b2-51803482d0e5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/custom-security-attributes-troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/custom-security-attributes-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/custom-security-attributes-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5d157f90-eaf4-68e7-83ea-6618003a43fa
---

# Troubleshoot custom security attributes in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

## Symptom - Add attribute set is disabled

When signed in to the [Microsoft Entra admin center](https://entra.microsoft.com) and you try to select the **Custom security attributes** &gt; **Add attribute set** option, it's disabled.

[![Screenshot of Add attribute set option disabled in Microsoft Entra admin center.](media/custom-security-attributes-troubleshoot/attribute-set-add-disabled.png)](media/custom-security-attributes-troubleshoot/attribute-set-add-disabled.png#lightbox)

**Cause**

You don't have permissions to add an attribute set. To add an attribute set and custom security attributes, you must be assigned the [Attribute Definition Administrator](../identity/role-based-access-control/permissions-reference#attribute-definition-administrator) role.

Important

By default, [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

**Solution**

Make sure that you're assigned the [Attribute Definition Administrator](../identity/role-based-access-control/permissions-reference#attribute-definition-administrator) role at either the tenant scope or attribute set scope. For more information, see [Manage access to custom security attributes in Microsoft Entra ID](custom-security-attributes-manage).

## Symptom - Error when you try to assign a custom security attribute

When you try to save a custom security attribute assignment, you get the message:

```
Insufficient privileges to save custom security attributes
This account does not have the necessary admin privileges to change custom security attributes
```

**Cause**

You don't have permissions to assign custom security attributes. To assign custom security attributes, you must be assigned the [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) role.

Important

By default, [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

**Solution**

Make sure that you're assigned the [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) role at either the tenant scope or attribute set scope. For more information, see [Manage access to custom security attributes in Microsoft Entra ID](custom-security-attributes-manage).

## Symptom - Can't filter custom security attributes for users or applications

**Cause 1**

You don't have permissions to filter custom security attributes. To read and filter custom security attributes for users or enterprise applications, you must be assigned the [Attribute Assignment Reader](../identity/role-based-access-control/permissions-reference#attribute-assignment-reader) or [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) role.

Important

By default, [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

**Solution 1**

Make sure that you're assigned one of the following Microsoft Entra built-in roles at either the tenant scope or attribute set scope. For more information, see [Manage access to custom security attributes in Microsoft Entra ID](custom-security-attributes-manage).

- [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator)
- [Attribute Assignment Reader](../identity/role-based-access-control/permissions-reference#attribute-assignment-reader)

**Cause 2**

You're assigned the Attribute Assignment Reader or Attribute Assignment Administrator role, but you haven't been assigned access to an attribute set.

**Solution 2**

You can delegate the management of custom security attributes at the tenant scope or at the attribute set scope. Make sure you have been assigned access to an attribute set at either the tenant scope or attribute set scope. For more information, see [Manage access to custom security attributes in Microsoft Entra ID](custom-security-attributes-manage).

**Cause 3**

There are no custom security attributes defined and assigned yet for your tenant.

**Solution 3**

Add and assign custom security attributes to users or enterprise applications. For more information, see [Add or deactivate custom security attribute definitions in Microsoft Entra ID](custom-security-attributes-add), [Assign, update, list, or remove custom security attributes for a user](../identity/users/users-custom-security-attributes), or [Assign, update, list, or remove custom security attributes for an application](../identity/enterprise-apps/custom-security-attributes-apps).

## Symptom - Custom security attributes can't be deleted

**Cause**

You can only activate and deactivate custom security attribute definitions. Deletion of custom security attributes isn't supported. Deactivated definitions don't count toward the tenant wide 500 definition limit.

**Solution**

Deactivate the custom security attributes you no longer need. For more information, see [Add or deactivate custom security attribute definitions in Microsoft Entra ID](custom-security-attributes-add).

## Symptom - Can't add a role assignment at an attribute set scope using PIM

When you try to add an eligible Microsoft Entra role assignment using [Microsoft Entra Privileged Identity Management (PIM)](../id-governance/privileged-identity-management/pim-configure), you can't set the scope to an attribute set.

**Cause**

PIM currently doesn't support adding an eligible Microsoft Entra role assignment at an attribute set scope.

## Symptom - Insufficient privileges to complete the operation

When you try to use [Graph Explorer](/en-us/graph/graph-explorer/graph-explorer-overview) to call Microsoft Graph API for custom security attributes, you see a message similar to the following:

```
Forbidden - 403. You need to consent to the permissions on the Modify permissions (Preview) tab
Authorization_RequestDenied
Insufficient privileges to complete the operation.
```

[![Screenshot of Graph Explorer displaying an insufficient privileges error message.](media/custom-security-attributes-troubleshoot/graph-explorer-insufficient-privileges.png)](media/custom-security-attributes-troubleshoot/graph-explorer-insufficient-privileges.png#lightbox)

Or when you try to use a PowerShell command, you see a message similar to the following:

```
Insufficient privileges to complete the operation.
Status: 403 (Forbidden)
ErrorCode: Authorization_RequestDenied
```

**Cause 1**

You're using Graph Explorer and you haven't consented to the required custom security attribute permissions to make the API call.

**Solution 1**

Open the Permissions panel, select the appropriate custom security attribute permission, and select **Consent**. In the Permissions requested window that appears, review the requested permissions.

[![Screenshot of Graph Explorer Permissions panel with CustomSecAttributeDefinition selected.](media/custom-security-attributes-troubleshoot/graph-explorer-permissions-consent.png)](media/custom-security-attributes-troubleshoot/graph-explorer-permissions-consent.png#lightbox)

**Cause 2**

You aren't assigned the required custom security attribute role to make the API call.

Important

By default, [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

**Solution 2**

Make sure that you're assigned the required custom security attribute role. For more information, see [Manage access to custom security attributes in Microsoft Entra ID](custom-security-attributes-manage).

**Cause 3**

You're trying to remove a single-valued custom security attribute assignment by setting it to `null` using the [Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser) or [Update-MgServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/update-mgserviceprincipal) command.

**Solution 3**

Use the [Invoke-MgGraphRequest](/en-us/powershell/microsoftgraph/authentication-commands#using-invoke-mggraphrequest) command instead. For more information, see [Remove a single-valued custom security attribute assignment from a user](../identity/users/users-custom-security-attributes#remove-a-single-valued-custom-security-attribute-assignment-from-a-user) or [Remove custom security attribute assignments from applications](../identity/enterprise-apps/custom-security-attributes-apps#remove-custom-security-attribute-assignments-from-applications-using-microsoft-graph-powershell).

## Symptom - Request\_UnsupportedQuery error

When you try to call Microsoft Graph API for custom security attributes, you see a message similar to the following:

```
Bad Request - 400
Request_UnsupportedQuery
Unsupported or invalid query filter clause specified for property '<AttributeSet>_<Attribute>' of resource 'CustomSecurityAttributeValue'.
```

**Cause**

The request isn't formatted correctly.

**Solution**

If required, add `ConsistencyLevel=eventual` in the request or the header. You might also need to include `$count=true` to ensure the request is routed correctly. For more information, see [Examples: Assign, update, list, or remove custom security attribute assignments using the Microsoft Graph API](/en-us/graph/custom-security-attributes-examples).

[![Screenshot of Graph Explorer with ConsistencyLevel header added.](media/custom-security-attributes-troubleshoot/graph-explorer-consistency-level-header.png)](media/custom-security-attributes-troubleshoot/graph-explorer-consistency-level-header.png#lightbox)