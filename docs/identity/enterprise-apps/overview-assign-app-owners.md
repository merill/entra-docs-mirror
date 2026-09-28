---
layout: Conceptual
title: Overview of Enterprise Application Ownership - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/overview-assign-app-owners
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn about application ownership in Microsoft Entra ID, including default assignments, managing configurations, and handling ownerless apps effectively.
ms.topic: concept-article
ms.date: 2024-12-06T00:00:00.0000000Z
ms.reviewer: saibandaru
ms.custom: enterprise-apps
locale: en-us
document_id: 0d89081e-ad51-e8dc-fe38-944c7de3214d
document_version_independent_id: 6dccde7e-17a2-b0ee-4edd-45161a98f190
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/overview-assign-app-owners.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/overview-assign-app-owners
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/overview-assign-app-owners.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a873e5d5-d4db-25e7-4fe4-0e895a174ba1
---

# Overview of Enterprise Application Ownership - Microsoft Entra ID | Microsoft Learn

A user who registers an application in Microsoft Entra ID is automatically added as the application owner. Default ownership of an enterprise application is assigned only when a user without any administrator roles creates a new application registration.

When a Cloud Application Administrator assigns a user as the owner of a service principal through an enterprise application, that user is also added as an application owner for single-tenant OpenID Connect (OIDC) and Security Assertion Markup Language (SAML) applications.

In all other scenarios, ownership is not assigned by default to an enterprise application. Although users can be assigned as owners of enterprise applications, groups can't be assigned as owners.

As an owner of an enterprise application in Microsoft Entra ID, a user can manage the organization-specific configuration of the application. This configuration includes single sign-on, provisioning, and user assignment. An owner can also add or remove other owners.

Unlike application administrators, owners can manage only the enterprise applications that they own. Owners have the same permissions as application administrators, scoped to an individual application. To learn more about the permissions that an owner of an application has, see [Ownership permissions](../../fundamentals/users-default-permissions#owned-enterprise-applications).

Note

The application might have more permissions than the owner. This situation is an elevation of privilege over what the owner can access as a user. In that case, an application owner can create or update users or other objects while impersonating the application. The elevation of privilege to owners can raise a security concern in some cases, depending on the application's permissions.

Currently, due to background applications and dependencies for service principal objects' settings, application owners added through methods other than the Microsoft Entra admin center (like Microsoft Graph API or PowerShell) can't manage some enterprise application settings. These settings include attributes and claims, configured SAML certificate properties, or token encryption settings.

## FAQ

**What should I do with applications where the owner is no longer with the organization?**

If you have an ownerless application in your tenant, you can access the audit log for the application to investigate other users who might be involved in configuring the application. However, there are limitations on how long audit logs are stored. See [Microsoft Entra audit log reporting](../monitoring-health/reference-reports-data-retention).

You might also see other users who scope permissions on the application by going to the **Roles and Administrators** tab. After you find the right person to own the application, a user with a highly privileged administrative role in the organization can assign the new owner for the application. See [Assign enterprise application owners](assign-app-owners).

As a best practice, we recommend proactively monitoring applications in your environment to ensure that there are at least two owners, where possible. This monitoring can help you avoid the situation of ownerless apps.

Additionally, you should use the `serviceManagementReference` property on the application object to reference the team contact information from your enterprise service or asset management database. The `serviceManagementReference` property ensures that you have a team contact, even if an individual leaves the organization.

**How can I find enterprise applications that are ownerless or at risk of being ownerless in my organization?**

To learn how to identify ownerless enterprise apps (or apps with only one owner) by using the Microsoft Graph API, see [List ownerless applications](/en-us/graph/tutorial-applications-basics#manage-application-ownership).

**How do I add myself as an owner of an enterprise application?**

Existing owners of an application can add other users as the owners. Also, users with a privileged role, such as Application Administrator or Cloud Application Administrator, can assign owners to applications in the organization. If you aren't an administrator, work with an administrator in your organization to [assign you as the owner](assign-app-owners) of the application.

**How can I find all the applications that I own?**

1. Go to **Enterprise Applications**, and then select **All Applications**.
2. Select **Add filter**, and then use **owned by** to search for apps that you or anyone else owns.