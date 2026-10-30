---
layout: Conceptual
title: Enable automatic user provisioning for multitenant applications in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/isv-automatic-provisioning-multi-tenant-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: A guide for independent software vendors for enabling automated provisioning in Microsoft Entra ID
ms.topic: reference
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: zhchia, arvinh
ai-usage: ai-assisted
locale: en-us
document_id: df52b4ac-5d15-a13c-d5c0-73201172fdd5
document_version_independent_id: fb187a98-3ea2-9f83-3e25-cbb52018a580
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/isv-automatic-provisioning-multi-tenant-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/isv-automatic-provisioning-multi-tenant-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/isv-automatic-provisioning-multi-tenant-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: ce90fdb6-e50b-aa90-9825-01dd4aaca4b1
---

# Enable automatic user provisioning for multitenant applications in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Automatic user provisioning is the process of automating the creation, maintenance, and removal of user identities in target systems like your software-as-a-service applications.

## Why enable automatic user provisioning?

Applications that require that a user record is present in the application before a user’s first sign in require user provisioning. There are benefits to you as a service provider, and benefits to your customers.

### Benefits to you as the service provider

- Increase the security of your application by using the Microsoft identity platform.
- Reduce actual and perceived customer effort to adopt your application.
- Reduce your costs in integrating with multiple identity providers (IdPs) for automatic user provisioning by using System for Cross-Domain Identity Management (SCIM)-based provisioning.
- Reduce support costs by providing rich logs to help customers troubleshoot user provisioning issues.
- Increase the visibility of your application in the [Microsoft Entra app gallery](https://azuremarketplace.microsoft.com/marketplace/apps).
- Get a prioritized listing in the App Tutorials page.

### Benefits to your customers

- Increase security by automatically removing access to your application for users who change roles or leave the organization to your application.
- Simplify user management for your application by avoiding human error and repetitive work associated with manual provisioning.
- Reduce the costs of hosting and maintaining custom-developed provisioning solutions.

## Choose a provisioning method

Microsoft Entra ID provides several integration paths to enable automatic user provisioning for your application.

- The [Microsoft Entra provisioning service](user-provisioning) manages the provisioning and deprovisioning of users from Microsoft Entra ID to your application (outbound provisioning) and from your application to Microsoft Entra ID (inbound provisioning). The service connects to the System for Cross-Domain Identity Management (SCIM) user management API endpoints provided by your application.
- When using the [Microsoft Graph](/en-us/graph/), your application manages inbound and outbound provisioning of users and groups from Microsoft Entra ID to your application by querying the Microsoft Graph API.
- The Security Assertion Markup Language Just in Time (SAML JIT) user provisioning can be enabled if your application is using SAML for federation. It uses claims information sent in the SAML token to provision users.

To help determine which integration option to use for your application, refer to the high-level comparison table, and then see the more detailed information on each option.

| Capabilities enabled or enhanced by Automatic Provisioning | Microsoft Entra provisioning service (SCIM 2.0) | Microsoft Graph API (OData v4.0) | SAML JIT |
| --- | --- | --- | --- |
| User and group management in Microsoft Entra ID | √ | √ | User only |
| Manage users and groups synced from on-premises Active Directory | √\* | √\* | User only\* |
| Access data beyond users and groups during provisioning Access to Microsoft 365 data (Teams, SharePoint, Email, Calendar, Documents, and so on) | X+ | √ | X |
| Create, read, and update users based on business rules | √ | √ | √ |
| Delete users based on business rules | √ | √ | X |
| Manage automatic user provisioning for all applications from the Microsoft Entra admin center | √ | X | √ |
| Support multiple identity providers | √ | X | √ |
| Support guest accounts (B2B) | √ | √ | √ |
| Support non-enterprise accounts (B2C) | X | √ | √ |

^\*^ – Microsoft Entra Connect setup is required to sync users from AD to Microsoft Entra ID.^+^– Using SCIM for provisioning does not preclude you from integrating your application with Microsoft Graph for other purposes.

## Microsoft Entra provisioning service (SCIM)

The Microsoft Entra provisioning service uses [SCIM](https://aka.ms/SCIMOverview), an industry standard for provisioning supported by many identity providers (IdPs) as well as applications (such as Slack, G Suite, Dropbox). We recommend you use the Microsoft Entra provisioning service if you want to support IdPs in addition to Microsoft Entra ID, as any SCIM-compliant IdP can connect to your SCIM endpoint. Building a simple /User endpoint, you can enable provisioning without having to maintain your own sync engine.

You can also use SCIM in [external tenants](/en-us/entra/external-id/customers/overview-customers-ciam) to automatically provision users from Microsoft Entra External ID to supported apps. This keeps user information up to date without any manual work. The service uses differential queries, so only changes since the last update are synced, which helps improve performance and reduce system load.

For more information on how the Microsoft Entra provisioning service users SCIM, see:

- [Learn more about the SCIM standard](https://aka.ms/SCIMOverview)
- [Using System for Cross-Domain Identity Management (SCIM) to automatically provision users and groups from Microsoft Entra ID to applications](use-scim-to-provision-users-and-groups)
- [Understand the Microsoft Entra SCIM implementation](use-scim-to-provision-users-and-groups)

## Microsoft Graph for Provisioning

When you use Microsoft Graph for provisioning, you have access to all the rich user data available in Graph. In addition to the details of users and groups, you can also fetch additional information like the user’s roles, manager and direct reports, owned and registered devices, and hundreds of other data pieces available in the [Microsoft Graph](/en-us/graph/api/overview).

More than 15 million organizations, and 90% of fortune 500 companies use Microsoft Entra ID while subscribing to Microsoft cloud services like Microsoft 365, Microsoft Azure, or Enterprise Mobility Suite. You can use Microsoft Graph to integrate your app with administrative workflows, such as employee onboarding (and termination), profile maintenance, and more.

Learn more about using Microsoft Graph for provisioning:

- [Microsoft Graph Home page](https://developer.microsoft.com/graph)
- [Overview of Microsoft Graph](/en-us/graph/overview)
- [Microsoft Graph Auth Overview](/en-us/graph/auth/)
- [Getting started with Microsoft Graph](https://developer.microsoft.com/graph/rest-api/)

## Using SAML JIT for provisioning

If you want to provision users only upon first sign in to your application, and do not need to automatically deprovision users, SAML JIT is an option. Your application must support SAML 2.0 as a federation protocol to use SAML JIT.

SAML JIT uses the claims information in the SAML token to create and update user information in the application. Customers can configure these required claims in the Microsoft Entra application as needed. Sometimes the JIT provisioning needs to be enabled from the application side so that customer can use this feature. SAML JIT is useful for creating and updating users, but it can't delete or deactivate the users in the application.