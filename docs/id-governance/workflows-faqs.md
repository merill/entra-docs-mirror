---
layout: Conceptual
title: Lifecycle workflows FAQs - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/workflows-faqs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Frequently asked questions about Lifecycle workflows.
ms.subservice: lifecycle-workflows
ms.topic: faq
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
ms.custom: template-tutorial
locale: en-us
document_id: 7cf7c478-1bf3-72b7-48f1-9310b82863a1
document_version_independent_id: 3fca36d0-9f83-6520-2882-34cea6559d5c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/workflows-faqs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/workflows-faqs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/workflows-faqs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1df9589a-6276-c934-c496-21c6eb2dbb1e
---

# Lifecycle workflows FAQs - Microsoft Entra ID Governance | Microsoft Learn

In this article, you find answers to commonly asked questions about [Lifecycle Workflows](what-are-lifecycle-workflows). Check back to this page frequently as changes happen often, and answers are continually being added.

## Frequently asked questions

### Can I create custom workflows for guests?

Yes, custom workflows can be configured for members or guests in your tenant. Workflows can run for all types of external guests, external members, internal guests, and internal members.

### Why do I see "Lifecycle Management" instead of "Lifecycle Workflows"?

For a small portion of our customers, Lifecycle Workflows could still be listed under the former name Lifecycle Management in the audit logs and enterprise applications.

### Do I need to map employeeHireDate in provisioning apps like WorkDay?

Yes, key user properties like employeeHireDate are supported for user provisioning from HR apps like WorkDay. To use these properties in Lifecycle workflows, you need to map them in the provisioning process to ensure the values are set. The following screenshot is an example of the mapping:

![Screenshot showing an example of how mapping is done in a Lifecycle Workflow.](media/workflows-faqs/workflows-mapping.png)

For more information on syncing employee attributes in Lifecycle Workflows, see: [How to synchronize attributes for Lifecycle workflows](how-to-lifecycle-workflow-sync-attributes)

### How do I see more details and parameters of tasks and the attributes that are being updated?

Some tasks do update existing attributes; however, we don’t currently share those specific details. As these tasks are updating attributes related to other Microsoft Entra features, so you can find that info in those docs. For temporary access pass, we're writing to the appropriate attributes listed [here](/en-us/graph/api/resources/temporaryaccesspassauthenticationmethod).

### Is it possible for me to create new tasks and how? For example, triggering other graph APIs/web hooks?

We currently don’t support the ability to create new tasks outside of the set of tasks supported in the task templates. As an alternative, you can accomplish this by setting up a logic app and then creating a logic apps task in Lifecycle Workflows with the URL. For more information, see [Trigger Logic Apps based on custom task extensions](trigger-custom-task).

### Why can’t I see any custom security attributes in the Property list?

Make sure you have active custom security attributes in your tenant as deactivated custom security attributes won't appear in the list. You also need the [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) or [Attribute Assignment Reader](../identity/role-based-access-control/permissions-reference#attribute-assignment-reader) roles in order for custom security attributes to be visible.

### What does it mean when it says “This rule contains invalid properties.” and there’s a red x icon on the rule expression for an existing workflow?

The red icon indicates that this custom security attribute is no longer active, so the rule is invalid. As the rule is invalid, the workflow won't be processed. You should remove the deactivated custom security attribute expression from the workflow's rule.

### My user is assigned a custom security attribute that’s part of the workflow trigger, why didn’t the workflow run for this user?

Lifecycle workflows checks that the user is assigned the custom security attribute that matches the specified value, including case-sensitivity. So check that the custom security attribute value matches exactly.

### How does Lifecycle workflows handle custom security attributes with multiple values?

If a user is assigned a custom security attribute that has multiple values, and one of the values matches the value specified in rule expressions, the user matches the scope.

### Why can’t I see the custom attributes listed in the attributes change trigger?

To see the expected attributes in the drop down list, you need to ensure the following:

- The attributes must be configured and active
- For custom security attributes, you have the appropriate permissions

### Do workflows using custom attribute triggers always take 4 hours to process changes?

No, the change processing time can vary depending on tenant change activity, timing and volume, with 4 hours expected to be the upper limit. We are working to optimize the timing as much as possible in hopes of reducing the time it takes.

### What happens if I have multiple workflows using custom attributes as triggers?

If multiple workflows are using the same custom attribute as trigger, when that change is processed, those workflows will be processed at the same time. If multiple workflows are using different custom attributes as trigger, but the custom attributes updates occurred at the same time, then those workflows will be processed at the same time. If the attribute updates occur at different times, then the workflows processing may be different.