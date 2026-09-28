---
layout: Conceptual
title: Frequently asked questions about the admin consent workflow - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/admin-consent-workflow-faq
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Find answers to frequently asked questions (FAQs) about the admin consent workflow.
ms.topic: faq
ms.date: 2022-05-27T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps
locale: en-us
document_id: b05e9501-9970-560d-a45c-5a705ab120bd
document_version_independent_id: a507819e-a4c0-7772-5e21-fd351bdb6028
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/admin-consent-workflow-faq.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/admin-consent-workflow-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/admin-consent-workflow-faq.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 4d8cb3f5-d9f5-0c18-89f6-28876cbccfe2
---

# Frequently asked questions about the admin consent workflow - Microsoft Entra ID | Microsoft Learn

## I enabled a workflow, but when testing the functionality, why can’t I see the new “Approval required” prompt that allows me to request access?

After enabling the feature, it may take up to 60 minutes for users to see the update, though it's usually available to all users within a few minutes.

## As a reviewer, why can’t I see all pending requests?

Reviewers can only see admin requests that are created after they're designated as a reviewer. If you've recently been added as a reviewer, you won't see requests that were created before your assignment.

## As a reviewer, why do I see multiple requests for the same application?

If an application is configured to use static and dynamic consent to request access to their user’s data, you'll see two admin consent requests. One request represents the static permissions, and the other represents the dynamic permissions.

## As a requestor, can I check the status of my request?

No, requestors are only able to receive updates using email notifications.

## As a reviewer, is it possible to approve the application, but not for everyone?

If you're concerned about granting admin consent and allowing all users in the tenant to use the application, you should deny the request. You can then manually grant admin consent by restricting access to the application. Configure the application to require user assignment, and assign users or groups to the application to restrict access. For more information, see [Methods for assigning users and groups](assign-user-or-group-access-portal).

## I have an application that requires user assignment. A user that I assigned to an application is being asked to request admin consent instead of being able to consent themselves. Why is that?

When access to an application is restricted using the "user assignment required" setting, an administrator needs to consent to all the permissions requested by the application.