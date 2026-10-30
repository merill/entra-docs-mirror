---
layout: Conceptual
title: Add, test, or remove protected actions in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/protected-actions-add
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Learn how to add, test, or remove protected actions in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-30T00:00:00.0000000Z
locale: en-us
document_id: d536bafd-d60e-8439-dd14-c455c1581cd7
document_version_independent_id: f2191572-40ac-e9f0-00c7-1cbc6e580ef2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/protected-actions-add.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/protected-actions-add
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/protected-actions-add.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 762cebf3-3b40-250e-2748-4b89edb6817d
---

# Add, test, or remove protected actions in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

[Protected actions](protected-actions-overview) in Microsoft Entra ID are permissions that have been assigned Conditional Access polices that are enforced when a user attempts to perform an action. This article describes how to add, test, or remove protected actions.

Note

You should perform these steps in the following sequence to ensure that protected actions are properly configured and enforced. If you don't follow this order, you might get unexpected behavior, such as getting repeated requests to reauthenticate.

## Prerequisites

To add or remove protected actions, you must have:

- Microsoft Entra ID P1 or P2 license
- [Conditional Access Administrator](permissions-reference#conditional-access-administrator) or [Security Administrator](permissions-reference#security-administrator) role

## Step 1: Configure Conditional Access policy

Protected actions use a Conditional Access authentication context, so you must configure an authentication context and add it to a Conditional Access policy. If you already have a policy with an authentication context, you can skip to the next section.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](permissions-reference#conditional-access-administrator).
2. Select **Entra ID** &gt; **Conditional Access** &gt; **Authentication context** &gt; **Authentication context**.
3. Select **New authentication context** to open the **Add authentication context** pane.
4. Enter a name and description and then select **Save**.

    [![Screenshot of Add authentication context pane to add a new authentication context.](media/protected-actions-add/authentication-context-add.png)](media/protected-actions-add/authentication-context-add.png#lightbox)
5. Select **Policies** &gt; **New policy** to create a new policy.
6. Create a new policy and select your authentication context.

    For more information, see [Conditional Access: Cloud apps, actions, and authentication context](../conditional-access/concept-conditional-access-cloud-apps#authentication-context).

    [![Screenshot of New policy page to create a new policy with an authentication context.](media/protected-actions-add/policy-authentication-context.png)](media/protected-actions-add/policy-authentication-context.png#lightbox)

## Step 2: Add protected actions

To add protection actions, assign a Conditional Access policy to one or more permissions using a Conditional Access authentication context.

1. Select **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
2. Make sure the state of the Conditional Access policy that you plan to use with your protected action is set to **On** and not **Off** or **Report-only**.
3. Select **Entra ID** &gt; **Roles & admins** &gt; **Protected actions**.

    [![Screenshot of Add protected actions page in Roles and administrators.](media/protected-actions-add/protected-actions-start.png)](media/protected-actions-add/protected-actions-start.png#lightbox)
4. Select **Add protected actions** to add a new protected action.

    If **Add protected actions** is disabled, make sure you're assigned the Conditional Access Administrator or Security Administrator role. For more information, see Troubleshoot protected actions.
5. Select a configured Conditional Access authentication context.
6. Select **Select permissions** and select the permissions to protect with Conditional Access.

    [![Screenshot of Add protected actions page with permissions selected.](media/protected-actions-add/permissions-select.png)](media/protected-actions-add/permissions-select.png#lightbox)
7. Select **Add**.
8. When finished, select **Save**.

    The new protected actions appear in the list of protected actions

## Step 3: Test protected actions

When a user performs a protected action, they'll need to satisfy Conditional Access policy requirements. This section shows the experience for a user being prompted to satisfy a policy. In this example, the user is required to authenticate with a FIDO security key before they can update Conditional Access policies.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a user that must satisfy the policy.
2. Select **Entra ID** &gt; **Conditional Access**.
3. Select a Conditional Access policy to view it.

    Policy editing is disabled because the authentication requirements haven't been satisfied. At the bottom of the page is the following note:

    Editing is protected by an additional access requirement. Click here to reauthenticate.

    [![Screenshot of a disabled Conditional Access policy with a note indicating to reauthenticate.](media/protected-actions-add/test-policy-reauthenticate.png)](media/protected-actions-add/test-policy-reauthenticate.png#lightbox)
4. Select **Click here to reauthenticate**.
5. Complete the authentication requirements when the browser is redirected to the Microsoft Entra sign-in page.

    [![Screenshot of a sign-in page to reauthenticate.](media/protected-actions-add/test-policy-reauthenticate-sign-in.png)](media/protected-actions-add/test-policy-reauthenticate-sign-in.png#lightbox)

    After completing the authentication requirements, the policy can be edited.
6. Edit the policy and save changes.

    [![Screenshot of an enabled Conditional Access policy that can be edited.](media/protected-actions-add/test-policy-edit.png)](media/protected-actions-add/test-policy-edit.png#lightbox)

## Remove protected actions

To remove protection actions, unassign Conditional Access policy requirements from a permission.

1. Select **Entra ID** &gt; **Roles & admins** &gt; **Protected actions**.
2. Find and select the permission Conditional Access policy to unassign.

    [![Screenshot of Protected actions page with permission selected to remove.](media/protected-actions-add/permissions-remove.png)](media/protected-actions-add/permissions-remove.png#lightbox)
3. On the toolbar, select **Remove**.

    After you remove the protected action, the permission won't have a Conditional Access requirement. A new Conditional Access policy can be assigned to the permission.

## Microsoft Graph

### Add protected actions

Protected actions are added by assigning an authentication context value to a permission. Authentication context values that are available in the tenant can be discovered by calling the [authenticationContextClassReference](/en-us/graph/api/resources/authenticationcontextclassreference?branch=main) API.

Authentication context can be assigned to a permission using the [unifiedRbacResourceAction](/en-us/graph/api/resources/unifiedrbacresourceaction?branch=main) API beta endpoint:

```http
https://graph.microsoft.com/beta/roleManagement/directory/resourceNamespaces/microsoft.directory/resourceActions/
```

The following example shows how to get the authentication context ID that was set on the `microsoft.directory/conditionalAccessPolicies/delete` permission.

```http
GET https://graph.microsoft.com/beta/roleManagement/directory/resourceNamespaces/microsoft.directory/resourceActions/microsoft.directory-conditionalAccessPolicies-delete-delete?$select=authenticationContextId,isAuthenticationContextSettable
```

Resource actions with the property `isAuthenticationContextSettable` set to true support authentication context. Resource actions with the value of the property `authenticationContextId` is the authentication context ID that has been assigned to the action.

To view the `isAuthenticationContextSettable` and `authenticationContextId` properties, they must be included in the select statement when making the request to the resource action API.

## Troubleshoot protected actions

### Symptom - No authentication context values can be selected

When attempting to select a Conditional Access authentication context, there are no values available to select.

[![Screenshot of Add protected actions page with no authentication context to select.](media/protected-actions-add/authentication-context-none.png)](media/protected-actions-add/authentication-context-none.png#lightbox)

**Cause**

No Conditional Access authentication context values have been enabled in the tenant.

**Solution**

Enable authentication context for the tenant by adding a new authentication context. Ensure **Publish to apps** is checked, so the value is available to be selected. For more information, see [Authentication context](../conditional-access/concept-conditional-access-cloud-apps#authentication-context).

### Symptom - Policy isn't getting triggered

In some cases, after a protected action has been added, users may not be prompted as expected. For example, if policy requires multifactor authentication, a user may not see a sign-in prompt.

**Cause 1**

The user hasn't been assigned to the Conditional Access policies used for protected action.

**Solution 1**

Use Conditional Access [What If](../conditional-access/what-if-tool) tool to check if the user has been assigned policy. When using the tool, select the user and the authentication context that was used with the protected action. Select What If and verify the expected policy is listed in the **Policies that will apply** table. If the policy doesn't apply, check the policy user assignment condition, and add the user.

**Cause 2**

The user has previously satisfied policy. For example, the completed multifactor authentication earlier in the same session.

**Solution 2**

Check the [Microsoft Entra sign-in events](../conditional-access/troubleshoot-conditional-access) to troubleshoot. The sign-in events include details about the session, including if the user has already completed multifactor authentication. When troubleshooting with the sign-in logs, it's also helpful to check the policy details page, to confirm an authentication context was requested.

### Symptom - Policy is never satisfied

When you attempt to perform the requirements for the Conditional Access policy, the policy is never satisfied and you keep getting requested to reauthenticate.

**Cause**

The Conditional Access policy wasn't created or the policy state is **Off** or **Report-only**.

**Solution**

Create the Conditional Access policy if it doesn't exist or and set the state to **On**.

If you aren't able to access the Conditional Access page because of the protected action and repeated requests to reauthenticate, use the following link to open the Conditional Access page.

- https://aka.ms/MSALProtectedActions

### Symptom - No access to add protected actions

When signed in you don't have permissions to add or remove protected actions.

**Cause**

You don't have permission to manage protected actions.

**Solution**

Make sure you're assigned the [Conditional Access Administrator](permissions-reference#conditional-access-administrator) or [Security Administrator](permissions-reference#security-administrator) role.

### Symptom - Error returned using PowerShell to perform a protected action

When using PowerShell to perform a protected action, an error is returned and there's no prompt to satisfy Conditional Access policy.

**Cause**

Microsoft Graph PowerShell supports step-up authentication, which is required to allow policy prompts. Azure PowerShell isn't supported for step-up authentication.

**Solution**

Make sure you're using Microsoft Graph PowerShell.