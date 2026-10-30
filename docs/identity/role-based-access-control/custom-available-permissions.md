---
layout: Conceptual
title: Custom role permissions for app registration - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/custom-available-permissions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: rolyon
ms.author: rolyon
ms.service: entra-id
ms.subservice: role-based-access-control
manager: pmwongera
description: Delegate custom administrator role permissions for managing app registrations.
ms.topic: how-to
ms.date: 2026-03-16T00:00:00.0000000Z
ms.reviewer: vincesm
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: b3cb555b-3983-1f96-146d-b7909776b191
document_version_independent_id: a76321a4-c5a5-dab2-243e-f34448ad7e39
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/role-based-access-control/custom-available-permissions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/role-based-access-control/custom-available-permissions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/role-based-access-control/custom-available-permissions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 6ee2d3ee-9241-84b6-dc94-1475ffc6c642
---

# Custom role permissions for app registration - Microsoft Entra ID | Microsoft Learn

This article outlines the app registration permissions available for custom role definitions in Microsoft Entra ID. These permissions allow administrators to manage application registrations with specific access levels, ensuring secure and efficient management of applications within the organization.

## License requirements

Using this feature requires Microsoft Entra ID P1 licenses. To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## Permissions for managing single-tenant applications

When choosing the permissions for your custom role, you can grant access to manage only single-tenant applications. Single-tenant applications are available only to users in the Microsoft Entra organization where the application is registered.

Single-tenant applications are defined as having **Supported account types** set to "Accounts in this organizational directory only." In the Graph API, single-tenant applications have the signInAudience property set to "AzureADMyOrg."

To grant access to manage only single-tenant applications, use the permissions indicated as follows with the subtype **applications.myOrganization**. For example, microsoft.directory/applications.myOrganization/basic/update.

See the [custom roles overview](custom-overview) for an explanation of the terms subtype, permission, and property set. The following information is specific to application registrations.

## Create and delete

There are two permissions available for granting the ability to create application registrations, each with different behavior:

#### microsoft.directory/applications/createAsOwner

Assigning this permission results in the creator being added as the first owner of the created app registration. The created app registration counts towards the creator's 250 created objects quota.

#### microsoft.directory/applications/create

Granting this permission prevents the creator from being added as the first owner of the app registration and excludes the app registration from the creator's 250-object quota. Use this permission carefully as there's nothing preventing the assignee from creating app registrations until the directory-level quota is reached.

If both permissions are assigned, the /create permission takes precedence. Though the /createAsOwner permission doesn't automatically add the creator as the first owner, owners can be specified during the creation of the app registration when using Graph APIs or PowerShell cmdlets.

Create permissions grant access to the **New registration** command.

[![Screenshot of permissions to grant access to the New Registration portal command.](media/custom-available-permissions/new-custom-role.png)](media/custom-available-permissions/new-custom-role.png#lightbox)

There are two permissions available for granting the ability to delete app registrations:

#### microsoft.directory/applications/delete

Grants the ability to delete app registrations regardless of subtype including both single-tenant and multitenant applications.

#### microsoft.directory/applications.myOrganization/delete

Grants the ability to delete app registrations restricted to those that are accessible only to accounts in your organization or single-tenant applications (myOrganization subtype).

[![Screenshot of permissions to grant access to the Delete app registration command.](media/custom-available-permissions/delete-app-registration.png)](media/custom-available-permissions/delete-app-registration.png#lightbox)

Note

When assigning a role that contains create permissions, the role assignment must be made at the directory scope. A create permission assigned at a resource scope doesn't grant the ability to create app registrations.

## Read

All member users in the organization can read app registration information by default. However, guest users and application service principals can't. If you plan to assign a role to a guest user or application, you must include the appropriate read permissions.

#### microsoft.directory/applications/allProperties/read

Grants the ability to read all properties of single-tenant and multitenant applications outside of properties that can't be read in any situation like credentials.

#### microsoft.directory/applications.myOrganization/allProperties/read

Grants the same permissions as microsoft.directory/applications/allProperties/read, but only for single-tenant applications.

#### microsoft.directory/applications/owners/read

Grants the ability to read owners property on single-tenant and multitenant applications. Grants access to all fields on the application registration owners page:

[![Screenshot of permissions to grant access to the app registration owners page.](media/custom-available-permissions/app-registration-owners.png)](media/custom-available-permissions/app-registration-owners.png#lightbox)

#### microsoft.directory/applications/standard/read

Grants access to read standard application registration properties. This includes properties across application registration pages.

#### microsoft.directory/applications.myOrganization/standard/read

Grants the same permissions as microsoft.directory/applications/standard/read, but for only single-tenant applications.

## Update

The "Update" permissions in Microsoft Entra ID allow administrators to modify various properties of application registrations. These permissions are essential for maintaining and managing both single-tenant and multitenant applications. Depending on the specific permission granted, administrators can update properties such as supported account types, authentication settings, branding details, and more. The following is a detailed list of the available update permissions and their specific capabilities.

#### microsoft.directory/applications/allProperties/update

Allows the ability to update all properties on single-tenant and multitenant applications.

#### microsoft.directory/applications.myOrganization/allProperties/update

Grants the same permissions as microsoft.directory/applications/allProperties/update, but only for single-tenant applications.

#### microsoft.directory/applications/audience/update

Allows the ability to update the supported account type (signInAudience) property on single-tenant and multitenant applications.

[![Screenshot of permission to grant access to app registration supported account type property on authentication page.](media/custom-available-permissions/supported-account-types.png)](media/custom-available-permissions/supported-account-types.png#lightbox)

#### microsoft.directory/applications.myOrganization/audience/update

Grants the same permissions as microsoft.directory/applications/audience/update, but only for single-tenant applications.

#### microsoft.directory/applications/authentication/update

Allows the ability to update the reply URL, sign-out URL, implicit flow, and publisher domain properties on single-tenant and multitenant applications. Grants access to all fields on the application registration authentication page except supported account types:

[![Screenshot of permissions to grant access to app registration authentication, but not supported account types.](media/custom-available-permissions/supported-account-types.png)](media/custom-available-permissions/supported-account-types.png#lightbox)

#### microsoft.directory/applications.myOrganization/authentication/update

Grants the same permissions as microsoft.directory/applications/authentication/update, but only for single-tenant applications.

#### microsoft.directory/applications/basic/update

Allows the ability to update the name, logo, homepage URL, terms of service URL, and privacy statement URL properties on single-tenant and multitenant applications. Grants access to all fields on the application registration branding page:

[![Screenshot of permission to grant access to the app registration branding page.](media/custom-available-permissions/app-registration-branding.png)](media/custom-available-permissions/app-registration-branding.png#lightbox)

#### microsoft.directory/applications.myOrganization/basic/update

Grants the same permissions as microsoft.directory/applications/basic/update, but only for single-tenant applications.

#### microsoft.directory/applications/credentials/update

Allows the ability to update the certificates and client secrets properties on single-tenant and multitenant applications. Grants access to all fields on the application registration certificates & secrets page:

[![Screenshot of permission to grant access to the app registration certificates &amp; secrets page.](media/custom-available-permissions/app-registration-secrets.png)](media/custom-available-permissions/app-registration-secrets.png#lightbox)

#### microsoft.directory/applications.myOrganization/credentials/update

Grants the same permissions as microsoft.directory/applications/credentials/update, but only for single-tenant applications.

#### microsoft.directory/applications/disablement/update

Allows the ability to update whether an application is enabled for users to sign in.

#### microsoft.directory/applications/owners/update

Allows the ability to update the owner property on single-tenant and multitenant. Grants access to all fields on the application registration owners page:

[![Screenshot of permissions to grant access to the app registration owners page.](media/custom-available-permissions/app-registration-owners.png)](media/custom-available-permissions/app-registration-owners.png#lightbox)

#### microsoft.directory/applications.myOrganization/owners/update

Grants the same permissions as microsoft.directory/applications/owners/update, but only for single-tenant applications.

#### microsoft.directory/applications/permissions/update

This permission allows updates to various properties on single-tenant and multitenant applications, including delegated permissions, application permissions, authorized client applications, required permissions, and consent properties. It doesn't grant the ability to perform consent. Grants access to all fields on the application registration API permissions and Expose an API pages:

[![Screenshot of permissions to grant access to the app registration API permissions page.](media/custom-available-permissions/app-registration-api-permissions.png)](media/custom-available-permissions/app-registration-api-permissions.png#lightbox)

[![Screenshot of permissions to grant access to the app registration Expose an API page.](media/custom-available-permissions/app-registration-expose-api.png)](media/custom-available-permissions/app-registration-expose-api.png#lightbox)

#### microsoft.directory/applications.myOrganization/permissions/update

Grants the same permissions as microsoft.directory/applications/permissions/update, but only for single-tenant applications.