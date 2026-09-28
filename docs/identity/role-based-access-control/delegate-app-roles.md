---
layout: Conceptual
title: Delegate application management administrator permissions - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/delegate-app-roles
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Grant permissions for application access management in Microsoft Entra ID
ms.topic: how-to
ms.date: 2024-11-17T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 467ee93c-4df9-24b9-021b-a48aafdf3bc5
document_version_independent_id: 5aba9f59-9d9d-1bfb-821c-22cabe0d04a4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/delegate-app-roles.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/delegate-app-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/delegate-app-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 44af96b3-d751-2500-cfa2-82be70b7a122
---

# Delegate application management administrator permissions - Microsoft Entra ID | Microsoft Learn

This article describes how to use permissions granted by custom roles in Microsoft Entra ID to address your application management needs. In Microsoft Entra ID, you can delegate Application creation and management permissions in the following ways:

- Restricting who can create applications and manage the applications they create. By default in Microsoft Entra ID, all users can register applications and manage all aspects of applications they create. This can be restricted to only allow selected people that permission.
- Assigning one or more owners to an application. This is a simple way to grant someone the ability to manage all aspects of Microsoft Entra configuration for a specific application.
- Assigning a built-in administrative role that grants access to manage configuration in Microsoft Entra ID for all applications. This is the recommended way to grant IT experts access to manage broad application configuration permissions without granting access to manage other parts of Microsoft Entra not related to application configuration.
- Creating a custom role defining very specific permissions and assigning it to someone either to the scope of a single application as a limited owner, or at the directory scope (all applications) as a limited administrator.

It's important to consider granting access using one of the above methods for two reasons. First, delegating the ability to perform administrative tasks reduces highly-privileged administrator overhead. Second, using limited permissions improves your security posture and reduces the potential for unauthorized access. For guidelines about role security planning, see [Securing privileged access for hybrid and cloud deployments in Microsoft Entra ID](security-planning).

## Restrict who can create applications

By default in Microsoft Entra ID, all users can register applications and manage all aspects of applications they create. Everyone also has the ability to consent to apps accessing company data on their behalf. You can choose to selectively grant those permissions by setting the global switches to 'No' and adding the selected users to the Application Developer role.

### To disable the default ability to create application registrations or consent to applications

To disable the default ability to create application registrations or consent to applications, follow these steps to set one or both of these settings for your organization.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Users** &gt; **User settings**.
3. Set the **Users can register applications** setting to **No**.

    This will disable the default ability for users to create application registrations.
4. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Consent and permissions**.
5. Select the **Do not allow user consent** option.

    This will disable the default ability for users to consent to applications accessing company data on their behalf.

### Grant individual permissions to create and consent to applications when the default ability is disabled

Assign the [Application Developer role](permissions-reference#application-developer) to grant the ability to create application registrations when the **Users can register applications** setting is set to No. This role also grants permission to consent on one's own behalf when the **Users can consent to apps accessing company data on their behalf** setting is set to No.

## Assign application owners

Assigning owners is a simple way to grant the ability to manage all aspects of Microsoft Entra configuration for a specific application registration or enterprise application. For more information, see [Assign enterprise application owners](../enterprise-apps/assign-app-owners).

## Assign built-in Application Administrator roles

Microsoft Entra ID has a set of built-in admin roles for granting access to manage configuration in Microsoft Entra ID for all applications. These roles are the recommended way to grant IT experts access to manage broad application configuration permissions without granting access to manage other parts of Microsoft Entra not related to application configuration.

- Application Administrator: Users in this role can create and manage all aspects of enterprise applications, application registrations, and application proxy settings. This role also grants the ability to consent to delegated permissions, and application permissions excluding Microsoft Graph. Users assigned to this role are not added as owners when creating new application registrations or enterprise applications.
- Cloud Application Administrator: Users in this role have the same permissions as the Application Administrator role, excluding the ability to manage application proxy. Users assigned to this role are not added as owners when creating new application registrations or enterprise applications.

For more information and to view the description for these roles, see [Microsoft Entra built-in roles](permissions-reference).

Follow the instructions in the [Assign roles to users with Microsoft Entra ID](../../fundamentals/how-subscriptions-associated-directory) how-to guide to assign the Application Administrator or Cloud Application Administrator roles.

Important

Application Administrators and Cloud Application Administrators can add credentials to an application and use those credentials to impersonate the application’s identity. The application may have permissions that are an elevation of privilege over the admin role's permissions. An admin in this role could potentially create or update users or other objects while impersonating the application, depending on the application's permissions. Neither role grants the ability to manage Conditional Access settings.

## Create and assign a custom role (preview)

Creating custom roles and assigning custom roles are separate steps:

- [Create a custom *role definition*](custom-create) and [add permissions to it from a preset list](custom-available-permissions). These are the same permissions used in the built-in roles.
- [Create a *role assignment*](manage-roles-portal) to assign the custom role.

This separation allows you to create a single role definition and then assign it many times at different *scopes*. A custom role can be assigned at organization-wide scope, or it can be assigned at the scope of a single Microsoft Entra object. An example of an object scope is a single app registration. Using different scopes, the same role definition can be assigned to Sally over all app registrations in the organization and then to Naveen over only the Contoso Expense Reports app registration.

Tips when creating and using custom roles for delegating application management:

- Custom roles only grant access in the most current app registration blades of the Microsoft Entra admin center. They do not grant access in the legacy app registrations blades.
- Custom roles do not grant access to the Microsoft Entra admin center when the [Restrict access to Microsoft Entra administration portal](../../fundamentals/users-default-permissions) user setting is set to **Yes**.
- App registrations the user has access to using role assignments only show up in the ‘All applications’ tab on the App registration page. They do not show up in the ‘Owned applications’ tab.

For more information on the basics of custom roles, see the [custom roles overview](custom-overview), as well as how to [create a custom role](custom-create) and how to [assign a role](manage-roles-portal).

## Troubleshoot

### Symptom - Access denied when you try to register an application

When you try to register an application in Microsoft Entra ID, you get a message similar to the following:

```
Access denied
You do not have access
You don't have permission to register applications in the <directoryName> directory. To request access, contact your administrator.
```

[![Screenshot of access denied message when trying to create a new app registration.](media/delegate-app-roles/app-registrations-access-denied.png)](media/delegate-app-roles/app-registrations-access-denied.png#lightbox)

**Cause**

You can't register the application in the directory because your directory administrator has restricted who can create applications.

**Solution**

Contact your administrator to do one of the following:

- Grant you permissions to create and consent to applications by assigning you the Application Developer role.
- Create the application registration for you and assign you as the application owner.