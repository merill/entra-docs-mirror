---
layout: Conceptual
title: Configure How Users Consent to Applications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-user-consent
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Configure user consent settings in Microsoft Entra ID to control when and how users grant permissions to your organization's data. Secure your environment with step‑by‑step guidance.
ms.topic: how-to
ms.date: 2025-06-15T00:00:00.0000000Z
ms.reviewer: phsignor, ergreenl
ms.custom: enterprise-apps
zone_pivot_groups: enterprise-apps-minus-legacy-powershell
locale: en-us
document_id: c7a6c58c-f887-03a4-8f69-eb91a19e4fb3
document_version_independent_id: 4e53d964-7edf-5668-b976-75fcdce4638e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/configure-user-consent.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/configure-user-consent
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/configure-user-consent.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: ee05ea33-60c1-9af0-a6fc-58e491fa1c40
---

# Configure How Users Consent to Applications - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to configure user consent settings in Microsoft Entra ID to control when and how users grant permissions to applications. This guidance helps IT admins reduce security risks by restricting or disabling user consent.

Before an application can access your organization's data, a user must grant the application permissions to do so. Different permissions allow different levels of access. By default, all users are allowed to consent to applications for permissions that don't require administrator consent. For example, by default, a user can consent to allow an app to access their mailbox but can't consent to allow an app unfettered access to read and write to all files in your organization.

To reduce the risk of malicious applications attempting to trick users into granting them access to your organization's data, we recommend that you allow user consent only for applications that have been published by a [verified publisher](../../identity-platform/publisher-verification-overview).

Note

Applications that require users to be assigned to the application must have their permissions consented by an administrator, even if the user consent policies for your directory would otherwise allow a user to consent on behalf of themselves.

## Prerequisites

To configure user consent, you need:

- A user account. If you don't already have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator) role.
- A [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) role is only required when using the Microsoft Entra admin center.

## Configure user consent settings

You can configure user consent settings in Microsoft Entra ID using either the Microsoft Entra admin center, Microsoft Graph PowerShell, or Microsoft Graph API. The settings you configure apply to all users in your organization.

::: zone pivot="portal"

### Configure user consent in Microsoft Entra admin center

To configure user consent settings through the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Identity** &gt; **Applications** &gt; **Enterprise apps** &gt; **Consent and permissions** &gt; **User consent settings**.
3. Under **User consent for applications**, select which consent setting you want to configure for all users.
4. Select **Save** to save your settings.

    ![Screenshot of the User consent settings pane.](media/configure-user-consent/setting-for-all-users.png)

::: zone-end

::: zone pivot="ms-powershell"

### Understand authorization and permission grant policies in Microsoft Graph PowerShell

To configure user consent settings programmatically using Microsoft Graph PowerShell, it's important to understand the distinction between the tenant-wide **authorization policy** and individual **permission grant policies**. The `authorizationPolicy`, retrieved using [Update-MgPolicyAuthorizationPolicy](/en-us/powershell/module/microsoft.graph.identity.signins/update-mgpolicyauthorizationpolicy) governs global settings such as whether users can consent to apps and which permission grant policies are assigned to the default user role. For example, you can disable user consent while still allowing developers to manage permissions for the apps they own by assigning only `ManagePermissionGrantsForOwnedResource.DeveloperConsent` in the `permissionGrantPoliciesAssigned` collection.

On the other hand, the [permissionGrantPolicies](/en-us/powershell/module/microsoft.graph.identity.signins/get-mgpolicypermissiongrantpolicy) endpoint lists your current permission grant policies. These policies determine what permissions can be granted to applications and under what circumstances. Each policy 'includes' certain conditions, but 'excludes' others. When a user tries to consent to an application, the system checks the permission grant policies to see if any of them apply to the user's request. For example, the low-risk policy would allow users to consent to those permissions configured as 'low risk'. It includes these low-risk policies (as a GUID). In another scenario, if a user tries to consent in a context that matches the 'AdminOnly' policy, they're unable to consent.

Note

Before updating consent settings with a `Update-MgPolicyPermissionGrantPolicy` command, always retrieve the current `authorizationPolicy` to identify which permission grant policies are already assigned. This ensures you preserve necessary permissions—such as those enabling developers to manage consent for apps they own—and avoid unintentionally removing existing functionality.

To choose which app consent policy governs user consent for applications, use the [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/get-started?view=graph-powershell-1.0&amp;preserve-view=true) module. The cmdlets used here are included in the [Microsoft.Graph.Identity.SignIns](https://www.powershellgallery.com/packages/Microsoft.Graph.Identity.SignIns) module.

Connect to Microsoft Graph PowerShell using the least-privilege permission needed. For reading the current user consent settings, use *Policy.Read.All*. For reading and changing the user consent settings, use *Policy.ReadWrite.Authorization*. You need to sign in as a [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator).

```powershell
Connect-MgGraph -Scopes "Policy.ReadWrite.Authorization"
```

### Disable user consent using Microsoft Graph PowerShell

To disable user consent, ensure that the consent policies (`PermissionGrantPoliciesAssigned`) include other current `ManagePermissionGrantsForOwnedResource.*` policies if any while updating the collection. This way, you can maintain your current configuration for user consent settings and other resource consent settings.

```powershell
# only exclude user consent policy
$body = @{
    "permissionGrantPolicyIdsAssignedToDefaultUserRole" = @(
        "managePermissionGrantsForOwnedResource.{other-current-policies}" 
    )
}
Update-MgPolicyAuthorizationPolicy -BodyParameter $body

```

### Allow user consent subject to an app consent policy using PowerShell

To allow user consent, choose which app consent policy should govern users' authorization to grant consent to apps. Ensure that the consent policies (`PermissionGrantPoliciesAssigned`) include other current `ManagePermissionGrantsForOwnedResource.*` policies if any while updating the collection. This way, you can maintain your current configuration for user consent settings and other resource consent settings.

```powershell
$body = @{
    "permissionGrantPolicyIdsAssignedToDefaultUserRole" = @(
        "managePermissionGrantsForSelf.{consent-policy-id}",
        "managePermissionGrantsForOwnedResource.{other-current-policies}"
    )
}
Update-MgPolicyAuthorizationPolicy -BodyParameter $body
```

Replace `{consent-policy-id}` with the ID of the policy you want to apply. You can choose a [custom app consent policy](manage-app-consent-policies#create-a-custom-app-consent-policy-using-powershell) that you've created, or you can choose from the following built-in policies:

| ID | Description |
| --- | --- |
| microsoft-user-default-low | **Allow user consent for apps from verified publishers, for selected permissions** Allow limited user consent only for apps from verified publishers and apps that are registered in your tenant, and only for permissions that you classify as *low impact*. (Remember to [classify permissions](configure-permission-classifications) to select which permissions users are allowed to consent to.) |
| microsoft-user-default-legacy | **Allow user consent for apps** This option allows all users to consent to any permission that doesn't require admin consent, for any application |

For example, to enable user consent subject to the built-in policy `microsoft-user-default-low`, run the following commands:

```powershell
$body = @{
    "permissionGrantPolicyIdsAssignedToDefaultUserRole" = @(
        "managePermissionGrantsForSelf.managePermissionGrantsForSelf.microsoft-user-default-low",
        "managePermissionGrantsForOwnedResource.{other-current-policies}"
    )
}
```

::: zone-end

::: zone pivot="ms-graph"

### Understand authorization and permission grant policies in Microsoft Graph

To configure user consent settings programmatically using Microsoft Graph, it's important to understand the distinction between the tenant-wide **authorization policy** and individual **permission grant policies**. The `authorizationPolicy` (retrieved using `GET https://graph.microsoft.com/v1.0/policies/authorizationPolicy/authorizationPolicy`) governs global settings such as whether users can consent to apps and which permission grant policies are assigned to the default user role. For example, you can disable user consent while still allowing developers to manage permissions for the apps they own by assigning only `ManagePermissionGrantsForOwnedResource.DeveloperConsent` in the `permissionGrantPoliciesAssigned` collection.

On the other hand, the `permissionGrantPolicies` endpoint (`GET https://graph.microsoft.com/v1.0/policies/permissionGrantPolicies`) lists your current permission grant policies. These policies determine what permissions can be granted to applications and under what circumstances. Each policy 'includes' certain conditions, but 'excludes' others. When a user tries to consent to an application, the system checks the permission grant policies to see if any of them apply to the user's request. For example, the low-risk policy would allow users to consent to those permissions configured as 'low risk'. It includes these low-risk policies (as a GUID). In another scenario, if a user tries to consent in a context that matches the 'AdminOnly' policy, they're unable to consent.

Note

Before updating consent settings with a `PATCH` request, always retrieve the current `authorizationPolicy` to identify which permission grant policies are already assigned. This ensures you preserve necessary permissions—such as those enabling developers to manage consent for apps they own—and avoid unintentionally removing existing functionality.

Use the [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to choose which app consent policy governs user consent for applications. You need to sign in as a [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator).

### Disable user consent using Microsoft Graph

To disable user consent, ensure that the consent policies (`PermissionGrantPoliciesAssigned`) include other current `ManagePermissionGrantsForOwnedResource.*` policies if any while updating the collection. This way, you can maintain your current configuration for user consent settings and other resource consent settings.

```http
PATCH https://graph.microsoft.com/v1.0/policies/authorizationPolicy
{
   "defaultUserRolePermissions": {
       "permissionGrantPoliciesAssigned": [
           "managePermissionGrantsForOwnedResource.{other-current-policies}"
        ]
    }
}
```

### Allow user consent subject to an app consent policy using Microsoft Graph

To allow user consent, choose which app consent policy should govern users' authorization to grant consent to apps. Ensure that the consent policies (`PermissionGrantPoliciesAssigned`) include other current `ManagePermissionGrantsForOwnedResource.*` policies if any while updating the collection. This way, you can maintain your current configuration for user consent settings and other resource consent settings.

```http
PATCH https://graph.microsoft.com/v1.0/policies/authorizationPolicy

{
    "defaultUserRolePermissions": {
        "managePermissionGrantsForSelf.{consent-policy-id}",
        "managePermissionGrantsForOwnedResource.{other-current-policies}"
   }
}
```

Replace `{consent-policy-id}` with the ID of the policy you want to apply. You can choose a [custom app consent policy](manage-app-consent-policies#create-a-custom-app-consent-policy-using-microsoft-graph) that you've created, or you can choose from the following built-in policies:

| ID | Description |
| --- | --- |
| microsoft-user-default-low | **Allow user consent for apps from verified publishers, for selected permissions** Allow limited user consent only for apps from verified publishers and apps that are registered in your tenant, and only for permissions that you classify as *low impact*. (Remember to [classify permissions](configure-permission-classifications) to select which permissions users are allowed to consent to.) |
| microsoft-user-default-legacy | **Allow user consent for apps** This option allows all users to consent to any permission that doesn't require admin consent, for any application |

For example, to enable user consent subject to the built-in policy `microsoft-user-default-low`, use the following PATCH command:

```http
PATCH https://graph.microsoft.com/v1.0/policies/authorizationPolicy

{
    "defaultUserRolePermissions": {
        "permissionGrantPoliciesAssigned": [
            "managePermissionGrantsForSelf.microsoft-user-default-low",
            "managePermissionGrantsForOwnedResource.{other-current-policies}"
        ]
    }
}
```

::: zone-end

Any updates to user consent settings only affect future consent operations for applications. Existing consent grants remain unchanged, and users continue to have access based on the permissions previously granted. To learn how to revoke existing consent grants, see [Review permissions granted to enterprise applications](manage-application-permissions).

Tip

To allow users to request an administrator's review and approval of an application that the user isn't allowed to consent to, [enable the admin consent workflow](configure-admin-consent-workflow). For example, you might do this when user consent has been disabled or when an application is requesting permissions that the user isn't allowed to grant.