---
layout: Conceptual
title: Use custom security attributes to scope a workflow - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/manage-workflow-custom-security-attribute
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to use custom security attributes to configure the scope of a workflow with lifecycle workflows.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: krbain
locale: en-us
document_id: 7ab037a5-ad7e-ae4b-2fa9-873f4d9dc696
document_version_independent_id: 7ab037a5-ad7e-ae4b-2fa9-873f4d9dc696
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/manage-workflow-custom-security-attribute.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/manage-workflow-custom-security-attribute
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/manage-workflow-custom-security-attribute.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ac87a0bc-5ffb-91fd-4c24-a957540e9256
---

# Use custom security attributes to scope a workflow - Microsoft Entra ID Governance | Microsoft Learn

Workflows created using Lifecycle workflows can be scoped based on attributes, including custom security attributes, configured for a user. You can use existing custom security attributes configured for your tenant, which contain sensitive data for a user, to further control the set of users for whom the workflow runs. For more information about custom security attributes, and their use cases, see: [What are custom security attributes in Microsoft Entra ID?](../fundamentals/custom-security-attributes-overview).

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

To scope a workflow using a custom security attribute, you must have a custom security attribute set and its definitions created in your tenant. For a guide on adding a custom security attribute set, and setting its definitions, see: [Add or deactivate custom security attribute definitions in Microsoft Entra ID](../fundamentals/custom-security-attributes-add). When you have created a custom set attribute and set its definitions, you must also assign this attribute to a user. For a guide on assigning custom security attributes to a user, see: [Assign custom security attributes to a user](../identity/users/users-custom-security-attributes#assign-custom-security-attributes-to-a-user).

Note

The [prerequisite](manage-workflow-custom-security-attribute#prerequisites) steps of creating, defining, and assigning a custom security attribute must be performed using the [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) role. The Lifecycle Workflows Administrator role alone cannot create, update, or assign custom security attributes.

## Add a custom security attribute to the scope of a workflow using the Microsoft Entra admin center

Workflows can be created with, or edited to include, a custom security attribute as a scope. The following steps walk you through editing an existing workflow to use a custom security attribute as a scope. For a guide on creating a workflow from scratch, with which you could scope a workflow using custom security attributes, see: [Create a lifecycle workflow](create-lifecycle-workflow). To edit a workflow to include a custom security attribute to its scope, you complete the following steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator) and [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. On the Workflows page, select the workflow that you want to use a custom security attribute as part of the scope for.
4. On the specific workflow page, select **Execution conditions**.
5. On the execution conditions page, select **Scope details**.
6. On the scope details page, select **Add expression**, and from the drop-down list locate your custom security attributes, and then set its value. ![Screenshot of a list of custom security attributes on the scope screen.](media/manage-workflow-custom-security-attribute/custom-attribute-list.png)

    Note

    Deactivated custom security attributes don't appear in this list.
7. After setting the value for the custom security attribute, select **Save**.

## Add a custom security attribute to the scope of the workflow using Microsoft Graph

As adding a custom security attribute to the scope of a workflow updates its execution conditions, you'd be creating a new version of the workflow. To create a new version of a workflow via API using Microsoft Graph, see: [workflow: createNewVersion](/en-us/graph/api/identitygovernance-workflow-createnewversion).

## View custom security attribute used as a scope of the workflow

After you scope a workflow using a custom security attribute, you can view this information within the workflow audit logs. To view these details, do the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Lifecycle Workflows Administrator](../identity/role-based-access-control/permissions-reference#lifecycle-workflows-administrator) and [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **ID Governance** &gt; **Lifecycle workflows** &gt; **Workflows**.
3. On the workflows page, select **Audit Logs**.

    Tip

    Custom security attribute information of a workflow is also viewable, with proper permissions, from a specific workflow's version page.
4. Select an event where a custom security attribute was used to scope a workflow during creation or added to an updated workflow, and then select **Modified properties**.
5. On the version information page, under **Configure**, you should see the custom security attribute as the rule. ![Screenshot of custom security attribute as scope.](media/manage-workflow-custom-security-attribute/custom-attribute-scope.png)
6. Your assigned roles determine whether you can see the full details of the custom security attributes being used. If you attempt to view custom security attribute information without the [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) or [Attribute Assignment Reader](../identity/role-based-access-control/permissions-reference#attribute-assignment-reader) role, the information is hidden. ![Screenshot of hidden attribute information.](media/manage-workflow-custom-security-attribute/attribute-information-hidden.png)

Note

For more information about custom security attributes being hidden, see: [Why can’t I see any custom security attributes in the Property list?](workflows-faqs#why-cant-i-see-any-custom-security-attributes-in-the-property-list).