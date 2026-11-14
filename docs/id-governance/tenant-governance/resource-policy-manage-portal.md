---
layout: Conceptual
title: Create and manage Microsoft Entra resource policies in the admin center (preview) - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tenant-governance/resource-policy-manage-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Manage resource policy definitions, assignments, versions, deleted items, and privileged-read configuration in the Microsoft Entra admin center.
ms.topic: how-to
ms.date: 2026-11-11T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 36d56ff9-bb14-50f3-79b2-334e7673bc3b
document_version_independent_id: 36d56ff9-bb14-50f3-79b2-334e7673bc3b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tenant-governance/resource-policy-manage-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tenant-governance/resource-policy-manage-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tenant-governance/resource-policy-manage-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: 19cd0209-568c-6b75-ccd5-8abe0dfbbf5b
---

# Create and manage Microsoft Entra resource policies in the admin center (preview) - Microsoft Entra ID Governance | Microsoft Learn

Use the [Microsoft Entra admin center](https://entra.microsoft.com/) to find built-in policies, manage custom definitions and assignments, and configure privileged policy reads.

## Prerequisites

- A tenant where resource policy preview is available.
- A Microsoft Entra ID Governance service plan for operations that require a license. See [licensing requirements and exceptions](licensing#resource-policy-preview).
- A work or school account with an active [Resource Policy Administrator](resource-policy-concepts#roles-and-api-permissions) role in the intended tenant. Use this account in the [Microsoft Entra admin center](https://entra.microsoft.com/) for policy, assignment, and configuration management. If the role is eligible through Privileged Identity Management, activate it before performing management tasks.
- To set or replace the privileged-read application, an application prepared by following [Configure the application](resource-policy-privileged-read-app#configure-the-application), including its federated identity credential and consented Microsoft Graph application permissions.

For read-only access, use the [Resource Policy Reader](resource-policy-concepts#roles-and-api-permissions) role. A read-only role doesn't grant policy management access. These portal procedures don't require you to grant permissions to Graph Explorer.

If management actions are unavailable because your role couldn't be verified, confirm it's active and select **Retry role check**. Operations that don't require a license still require management authorization.

## Find resource policies

1. Sign in to the Microsoft Entra admin center and confirm that you're in the intended tenant.
2. Go to **Tenant governance**.

Under **Resource policies**, choose the page for your task:

| Page | Use it to |
| --- | --- |
| **Definitions** | Find policies and open their properties, assignments, and versions. |
| **Assignments** | Review and manage assignments across the tenant. |
| **Deleted items** | Review, restore, or permanently delete deleted definitions and assignments. |

The tenant-wide **Assignments** page is separate from the **Assignments** tab on an individual policy definition.

You can also use the resource policy shortcuts under **Overview** &gt; **Get started** &gt; **Prevent non-compliant resources** to open **Definitions** or **Assignments**.

For tenant-wide configuration, open **Tenant governance settings** under **Settings**, then select **Resource policies**. See Manage resource policy configuration.

## Select a built-in policy

Built-in policies let you apply a policy without writing Rego. Review a policy's requirements and supported resources before assigning it.

1. In **Tenant governance**, select **Definitions**.
2. On the **Built in** tab, find and select a policy. For example, select **Require a department prefix for application names**.
3. On **Properties**, review the description and **Resource**.
4. Note the **Unique name** and **Latest version** for the assignment.

The example policy requires application names to start with an allowed department prefix and contain no banned words.

Built-in definition properties and Rego content are read-only. Use the definition's **Assignments** tab to review its assignments and **Versions** tab to review version information.

For the first-run workflow, see [Quickstart: Assign a built-in resource policy](resource-policy-quickstart-portal).

## Create a custom definition

Prepare and test the Rego before creating a custom definition. Creating a definition alone doesn't enable enforcement.

1. Prepare a nonempty `.rego` file that follows the [required policy structure](resource-policy-rego#required-policy-structure). Include the policy name and version in the package declaration, and descriptive information, applicability, and any parameter schema in `__metadata__`.
2. In **Tenant governance**, select **Definitions** and the **Custom** tab.
3. Select **New definition**.
4. In **Create resource policy definition**, select **Choose file** under **Rego policy file**, and select your `.rego` file.
5. Confirm the selected file. Use **Replace file** or **Remove file** if you selected the wrong one.
6. Select **Create**. Correct any validation or publication error before retrying.
7. After the success message, return to **Definitions** &gt; **Custom** and open the definition. Confirm its **Unique name**, **Latest version**, description, resource, and Rego content.

Upload a complete `.rego` file; there's no inline editor. The policy source supplies the definition's name, description, and version.

For policies that use `fetchAsPolicy()`, configure the privileged-read application before uploading. See [Author resource policies with Rego](resource-policy-rego) and [Test and troubleshoot a resource policy](resource-policy-test-troubleshoot).

## Create or update an assignment

Before changing an assignment, review its settings and follow [safe assignment deployment](resource-policy-safe-deployment).

| Setting | Review |
| --- | --- |
| Assignment identifier | Identify the assignment you intend to change. |
| **Version** | Confirm the policy version referenced by the assignment. |
| **Status** | **On** enables evaluation. **Off** assignments aren't evaluated, regardless of enforcement mode. |
| **Enforcement** | **Report-only** evaluates and records results without blocking requests. **Enforce** applies the deny effect and blocks noncompliant requests. |
| **Parameters** | Review the values required by the selected policy version. A policy without configurable parameters doesn't require parameter entry. |

Status and enforcement are independent. To assess a policy without blocking requests, use **Status** set to **On** and **Enforcement** set to **Report-only**.

An existing assignment's identifier, policy definition, and version are read-only in **Edit**. To use a different policy version, create another assignment for that version; don't try to repoint the existing assignment.

### Create an assignment

You can start from the tenant-wide **Assignments** page or from a policy definition.

1. In **Tenant governance**, select **Assignments** &gt; **Create assignment**. Alternatively, open a definition and select **Add assignment** to use that definition.
2. On **Settings**, enter an **Assignment identifier**, such as `contoso_application_naming`. Use a unique identifier that follows the [assignment naming rules](resource-policy-rego#required-policy-structure).
3. If you started from the tenant-wide page, select **Select definition**, choose the intended policy in **Select policy definition**, and select **Select**.
4. Confirm the **Version**. If multiple versions are available, choose the one you tested. A single available version can appear as read-only text.
5. Set **Status** to **On** and **Enforcement** to **Report-only** for an initial deployment.
6. Select **Next**. On **Parameters**, enter the values required by that version. For lists, use the list parameter editor.
7. Correct any validation errors, then select **Next**.
8. On **Review**, confirm the policy, version, identifier, status, enforcement, and parameter values.
9. Select **Add assignment**. Wait for **Resource policy assignment saved.**
10. Open the saved assignment and confirm its settings.

Assignments created in this workflow are tenant-wide (`/`); there's no scope selector.

Each definition version can have only one live assignment, including an **Off** assignment. Already assigned versions and versions with unsupported parameter settings aren't available. If a version becomes unavailable while you're creating an assignment, select another version or review the existing assignment.

If **Add assignment** can't check version availability, select **Retry checking available policy versions**. After the check succeeds, select **Add assignment** again.

For an example configuration, see [Quickstart: Assign a built-in resource policy](resource-policy-quickstart-portal#1-select-a-built-in-policy-and-assign-it-in-your-tenant).

### Edit an existing assignment

Open an assignment from its policy definition to review or change its settings.

1. In **Tenant governance**, select **Definitions** and open the policy.
2. On **Assignments**, open the assignment.
3. On **Assignment details**, review the version, status, enforcement, and parameters, then select **Edit**.
4. On **Settings**, choose the **Status** and **Enforcement** values you need.
5. Select **Next**.
6. On **Parameters**, review and change the values you need. Strings and numbers use input fields; Boolean parameters use **True** or **False**. Optional Boolean parameters can be **Not configured**. Lists use a separate editor.
7. Correct validation errors, then select **Next**.
8. On **Review**, confirm the settings and parameter values, then select **Save**.
9. Wait for **Resource policy assignment saved.**
10. Reopen **Assignment details** and confirm the status, enforcement, version, and parameter values.

If another administrator changes the assignment before you save, select **Refresh latest saved values**. Compare them with your draft on **Review**, select **I reviewed the latest saved values**, and save only if the settings are correct. Resolve any verification errors before resubmitting.

Saved changes aren't necessarily effective on resource requests immediately. Allow for [assignment propagation](resource-policy-evaluation#assignment-propagation) and verify request behavior separately.

### Edit a list parameter

Some policies use lists of values. For example, **Require a department prefix for application names** uses `allowed_departments` for case-sensitive name prefixes.

1. On **Parameters**, select **Edit allowed\_departments**.
2. In **Edit allowed\_departments**, enter one value per row. Use **Add row** for another value, or **Remove** for a row you don't need.
3. Correct any validation errors, then select **Apply** to update the assignment draft. To discard the list edits, select **Cancel**.
4. Back on **Parameters**, select **Next**, review the assignment, and select **Save** for an existing assignment or **Add assignment** for a new one.

For this example, optional `banned_word_list` and `client_appid_exclusion_list` lists can remain empty. Review each parameter's description before changing its values.

**Apply** doesn't save the assignment to the service. Required lists can't be empty, and each value must match the type declared by the policy. For parameter semantics and defaults, see [Resource policy parameters](resource-policy-parameters).

### Turn off an assignment

Turn off an assignment when you want to stop evaluation without deleting its settings.

1. Open **Assignment details** and select **Turn off**.
2. Wait for **Resource policy assignment turned off.**
3. Reopen the assignment and confirm **Status** is **Off**.

You can also select **Edit**, set **Status** to **Off** on **Settings**, and complete **Parameters** &gt; **Review** &gt; **Save**. **Turn off** from assignment details saves directly; it doesn't use the edit wizard.

If the portal reports that turning off succeeded but the saved status couldn't be verified, select **Check assignment status again**. This checks the saved state without repeating the change.

An **Off** assignment still counts as that version's live assignment. To enable it again, use **Edit**, set **Status** to **On**, confirm the enforcement mode and parameters, and save. Allow for [assignment propagation](resource-policy-evaluation#assignment-propagation).

## Delete an assignment

Delete an assignment when you no longer want it to apply the policy. Removing an assignment doesn't require deleting the built-in policy definition.

1. In **Tenant governance**, select **Assignments** to open **Resource policy assignments**.
2. Select the checkbox for the assignment you want to delete. Confirm that only the intended assignment is selected, including any selections hidden by the current filter.
3. Select **Delete**.
4. In **Remove assignment?**, confirm **Selected items: 1.**, then select **Delete**.
5. Confirm the status message: **Delete assignments: 1 succeeded; 0 failed.**

The assignment moves to **Deleted items** and can be restored for 30 days. Allow for [assignment propagation](resource-policy-evaluation#assignment-propagation) before expecting resource requests to reflect the deletion.

## Manage policy versions

Custom policy versions and assignments have distinct lifecycles. Publishing a new custom version doesn't automatically move an assignment to it.

### Review and download a version

1. In **Definitions**, open the policy.
2. Select **Versions** to review the current and previous versions.
3. Select **Refresh** to reload the definition and its version history when you need the latest saved information.
4. Select a version number to open its read-only policy source.
5. Use **Download Rego** for the version you want to save.

Use the assignment's version, not just the definition's **Latest version**, when investigating behavior or planning a rollback.

If a download fails, retry **Download Rego** for the intended version.

### Publish a new custom version

You can't publish changes to Microsoft-managed built-in definitions.

1. Save a copy of the current Rego and assignment settings.
2. Revise and test the `.rego` file. Keep the definition's unique name and increase the package version as described in [Publish a new custom policy version](resource-policy-lifecycle#publish-a-new-custom-policy-version).
3. In **Definitions** &gt; **Custom**, open the definition.
4. On **Properties**, select **Upload new version**.
5. In **Upload policy version**, select **Choose file** and choose the revised `.rego` file.
6. Confirm the file and select **Publish**. Correct any publication error before retrying.
7. After the success message, reopen the definition and confirm **Latest version**, the uploaded policy source, and the previous version in **Versions**.

Uploading identical content doesn't publish another version. If publication succeeds but you can't view the saved definition, refresh and check its version and source before uploading again.

Create a separate assignment to test the new version in report-only mode. Keep existing protection in place during rollout. For rollout and rollback steps, see [Update and retire resource policies](resource-policy-lifecycle).

## Delete a custom definition

Save the Rego and assignment settings you might need for recovery before deleting a custom policy. Built-in definitions can't be deleted.

1. Open the custom definition's **Assignments** tab and delete every live assignment that references it, including assignments whose status is **Off**.
2. Return to **Definitions** &gt; **Custom**.
3. Select the checkbox for the intended definition, then select **Delete**.
4. In **Delete this custom definition?**, review the selection and select **Delete**.
5. Confirm the operation's status and check **Deleted items** &gt; **Definitions**.

Deleted custom definitions can be restored for 30 days unless permanently deleted first.

## Restore deleted items

Review the deleted item's settings before restoring it. Restoring an assignment can resume policy evaluation and enforcement with its saved settings.

1. In **Tenant governance**, select **Deleted items**.
2. If the custom definition was deleted, select the **Definitions** tab. Open the intended item's details to confirm its identity, then select its checkbox in the list and select **Restore**.
3. If you restored a custom definition, return to **Definitions** &gt; **Custom** and confirm that the required version is available.
4. In **Deleted items** &gt; **Assignments**, open the intended assignment's details. Review its definition, version, status, enforcement, and parameters.
5. Confirm that no other live assignment, including an **Off** assignment, already uses that definition version.
6. Select the deleted assignment's checkbox and select **Restore**.
7. Return to **Assignments**, open the restored assignment, and confirm its saved settings.

Restore a deleted definition before its assignments. Allow the restored settings to take effect, then verify request behavior and [evaluation audit events](resource-policy-logs). For reserved names and recovery requirements, see [Update and retire resource policies](resource-policy-lifecycle#restore-a-deleted-policy-or-assignment).

## Permanently delete deleted items

Warning

Permanent deletion can't be undone. You can't restore a permanently deleted definition or assignment.

1. In **Tenant governance**, select **Deleted items**.
2. Select **Assignments** or **Definitions** for the item type.
3. Select only the intended items, then select **Permanently delete**.
4. In **Permanently delete selected items?**, confirm the selected-item count and select **Permanently delete**.
5. Review the result and confirm that the items no longer appear in the deleted-items list.

For operations on multiple items, review both the succeeded and failed counts. Partial success doesn't mean every selected item changed. Review the per-item errors and retry only the failed items.

## Manage resource policy configuration

The **Resource policies** tab in **Tenant governance settings** manages the tenant-wide resource policy configuration. Under **Privileged reads**, you can set, replace, or clear the application used by policies that call `fetchAsPolicy()`.

### Set or replace the privileged-read application

Prepare the application before saving its ID. This settings page doesn't register an application, create its federated identity credential, or grant Microsoft Graph permissions.

1. Follow [Configure the application](resource-policy-privileged-read-app#configure-the-application) to prepare a customer-owned application, its federated identity credential, and consent for the required read permissions. Record its application (client) ID, not its application object ID or service principal object ID.
2. In **Tenant governance**, under **Settings**, open **Tenant governance settings**.
3. Select **Resource policies** and find **Privileged reads**.
4. In **Privileged-read application (client) ID**, enter the application's client ID as a GUID. For a replacement, replace the existing value with the prepared application's client ID.
5. Select **Save** and wait for **Privileged-read application settings were saved.**
6. Reopen the **Resource policies** tab and confirm the intended client ID is saved. Resolve any saved-state verification warning before making another change.
7. [Validate a live privileged read](resource-policy-privileged-read-app#validate-a-live-privileged-read) before relying on policies that use this application.

For first-time setup, have one administrator configure this tenant-wide setting at a time.

**Cancel** discards unsaved edits and returns the field to its loaded value. Saving the application ID doesn't prove that the application has all the read permissions your policies require.

### Clear the privileged-read application

Warning

Clearing this setting disables privileged reads tenant-wide and affects every policy that uses `fetchAsPolicy()`. Review dependent policies and how they handle failed reads before proceeding.

1. Open **Tenant governance settings** &gt; **Resource policies**.
2. Clear **Privileged-read application (client) ID** so the field is blank, then select **Save**.
3. Reopen the tab and confirm the field is blank.

Clearing the field doesn't delete the application or its credentials.

### Recover from configuration errors

Follow the message for the failed operation rather than repeatedly selecting **Save**.

| Message or situation | Action |
| --- | --- |
| Settings couldn't be loaded. | Select **Retry loading settings**. |
| Settings changed elsewhere. | Select **Refresh saved settings**. Compare **Current saved application ID** with your retained draft, then select **Save** only if you intend to replace the saved value. |
| The saved settings or their version couldn't be verified. | Select **Refresh saved settings**. Don't submit another change until verification succeeds. |

## Review evaluation results

Use Graph Explorer for [simulated evaluations in the quickstart](resource-policy-quickstart-portal#2-validate-without-performing-a-write); these actions aren't available in the admin center. For real requests and enforcement tests, follow the [observe-and-enforce tutorial](resource-policy-tutorial-portal).

To inspect real request outcomes and assess assignment impact, see [Analyze resource policy evaluation audit logs](resource-policy-logs).