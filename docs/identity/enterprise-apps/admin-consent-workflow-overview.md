---
layout: Conceptual
title: Overview of Admin Consent Workflow - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/admin-consent-workflow-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to manage the admin consent workflow, email notifications, and audit logs related to consent requests.
ms.topic: concept-article
ms.date: 2024-11-29T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps
locale: en-us
document_id: c5f712da-b1bd-7c90-941f-8067533e2e73
document_version_independent_id: d16848a5-f9af-3671-9abf-6556915906dc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/admin-consent-workflow-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/admin-consent-workflow-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/admin-consent-workflow-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: ec0e7d22-7882-9ad4-2913-b0e2c51c7dfe
---

# Overview of Admin Consent Workflow - Microsoft Entra ID | Microsoft Learn

In some situations, your users might need to consent to permissions for applications that they're creating or using with their work accounts. However, non-admin users aren't allowed to consent to permissions that require admin consent. Also, users can't consent to applications when [user consent](configure-user-consent) is turned off in the user's tenant.

When user consent is turned off, an admin can grant users the ability to make requests for gaining access to applications by turning on the admin consent workflow. In this article, you learn about the user and admin experience when the admin consent workflow is on versus when it's off.

When users attempt to sign in, they might see a consent prompt like the one in the following screenshot.

![Screenshot of a consent prompt when the admin consent workflow is turned off.](media/configure-admin-consent-workflow/admin-consent-workflow-off.png)

If the user doesn't know who can grant them access, they might be unable to use the application. This situation also requires administrators to create a separate workflow to track requests for applications if they're open to receiving them.

As an admin, you can use the following options to determine how users consent to applications:

- Turn off user consent. For example, a high school might want to turn off user consent so that the school IT administration has full control over all the applications in their tenant.
- Allow users to consent to the required permissions. The best practice is to keep user consent open if you have sensitive data in your tenant.
- If you still want to retain admin-only consent for certain permissions but want to assist your users in onboarding their application, you can use the admin consent workflow to evaluate and respond to admin consent requests. This way, you can have a queue of all the requests for admin consent for your tenant. You can track and respond to these requests directly through the Microsoft Entra admin center.

    To learn how to configure the admin consent workflow, see [Configure the admin consent workflow](configure-admin-consent-workflow).

## How the admin consent workflow works

When you configure the admin consent workflow, your users can request consent directly through the prompt. The users might see a consent prompt like the one in the following screenshot.

![Screenshot of consent prompt when the admin consent workflow is turned on.](media/configure-admin-consent-workflow/consent prompt-workflow-on.png)

When an administrator responds to a request, the user receives an email alert that says the request is processed.

When the user submits a consent request, the request appears in the pane for admin consent requests in the Microsoft Entra admin center. Administrators and designated reviewers sign in to [view and act on the new requests](review-admin-consent-requests).

Reviewers can view and act on all pending admin consent requests in the tenant, including requests that were created before they were designated as reviewers. Any request that's still pending remains visible to newly assigned reviewers, so they can review and take action on existing requests based on their assigned permissions.

Requests appear on the following two tabs in the pane for admin consent requests:

- **My pending**: This tab shows any active requests that have the signed-in user designated as a reviewer. Although reviewers can block or deny requests, only people with the correct role-based access control (RBAC) permissions to consent to the requested permissions can do so.
- **All (Preview)**: This tab shows all requests, active or expired, that exist in the tenant. Each request includes information about the application and the users who requested the application.

## Email notifications

If email notifications are configured, all reviewers receive the notifications when:

- A new request is created.
- A request expires.
- A request is nearing the expiration date.

Requestors receive email notifications when:

- They submit a new request for access.
- Their request expires.
- Their request is denied or blocked.
- Their request is approved.

## Audit logs

The following table outlines the scenarios and audit values available for the admin consent workflow.

| Scenario | Audit service | Audit category | Audit activity | Audit actor | Audit log limitations |
| --- | --- | --- | --- | --- | --- |
| Admin turning on the consent request workflow | Access Reviews | UserManagement | Create governance policy template | App context | Currently you can't find the user context |
| Admin turning off the consent request workflow | Access Reviews | UserManagement | Delete governance policy template | App context | Currently you can't find the user context |
| Admin updating the consent workflow configurations | Access Reviews | UserManagement | Update governance policy template | App context | Currently you can't find the user context |
| User creating an admin consent request for an app | Access Reviews | Policy | Create request | App context | Currently you can't find the user context |
| Reviewer approving an admin consent request | Access Reviews | UserManagement | Approve all requests in business flow | App context | Currently you can't find the user context or the app ID that was granted admin consent |
| Reviewer denying an admin consent request | Access Reviews | UserManagement | Approve all requests in business flow | App context | Currently you can't find the user context of the actor that denied an admin consent request |