---
layout: Conceptual
title: Migrate Conditional Access policies to a policy plan (preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/how-to-migrate-conditional-access-policy-plan
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: ebasseri
ms.author: etbasser
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to consolidate existing Conditional Access policies into a policy plan and validate the new rules before enforcement.
ms.topic: how-to
ms.date: 2026-10-21T00:00:00.0000000Z
ms.reviewer: celested
ai-usage: ai-assisted
locale: en-us
document_id: ffc25855-d323-059d-3f66-5d66cdb4ff94
document_version_independent_id: ffc25855-d323-059d-3f66-5d66cdb4ff94
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/how-to-migrate-conditional-access-policy-plan.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/how-to-migrate-conditional-access-policy-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/how-to-migrate-conditional-access-policy-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 905256db-0156-a753-eba4-22b5c19b5d49
---

# Migrate Conditional Access policies to a policy plan (preview) - Microsoft Entra ID | Microsoft Learn

This article shows you how to consolidate existing Conditional Access policies into a policy plan by using the built-in migration experience. The migration tool analyzes your selected policies, identifies shared conditions, and proposes a plan structure for you to review before committing. Your original policies aren't changed during this process.

Important

Conditional Access policy plans are in preview. Preview features are available under the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) and might not have all the capabilities of generally available features.

## Prerequisites

To migrate Conditional Access policies, sign in with the Conditional Access Administrator role.

For license requirements, see [Conditional Access license requirements](overview#license-requirements).

Before you begin, read [What are Conditional Access policy plans?](concept-conditional-access-policy-plans) to understand how shared conditions and rules interact, and how plan rules evaluate alongside existing policies.

## Before you begin

The migration experience works best when you select policies that share a common intent. For example, select policies that protect the same set of applications but apply different controls to different user types, risk levels, or device states.

When you plan your migration:

- **Group by protected resource.** Policies that protect the same applications or services are natural candidates for a single plan.
- **Group by persona.** If multiple policies apply to the same set of users with different grant controls, they can be consolidated into one plan. Shared user targeting lives at the plan level, and each grant control becomes a rule.
- **Group by condition.** Separate policies that already share a common condition, such as a sign-in risk level, device platform, or network location, are candidates for a plan. Configure the shared condition at the plan level and the scenario-specific settings in each rule.
- **Migrate incrementally.** You don't need to migrate all policies at once. Starting with a small, well-understood group of related policies reduces risk during validation.

## Migrate policies to a plan

After you identify a related set of policies, use the migration experience to review and create a proposed plan:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. On the **Policies** page, locate the **Migrate to Conditional Access Policy plans (Preview)** banner, and then select **Get started**.
4. Select the existing policies that you want to consolidate into a single plan. Choose policies that share a common intent. You can search for specific policies or filter on policy attributes.
5. Select **Merge policies into a plan**.
6. The migration tool analyzes the selected policies and identifies any **shared conditions**. Update the policy plan name if needed.
7. Review the plan preview. Settings that the selected policies have in common become **shared conditions**.
8. Review the proposed **Rules**. Each selected policy is mapped to a rule. Identities, resources, locations, grant controls, session controls, and other settings that are unique to a policy remain in its corresponding rule. Note that the initial **State** for all rules generated during migration is **Off** to prevent unintended impact to your organization.
9. Select **Create policy plan**.
10. Select **Edit plan** to update the plan's name, description, tags, and owners to record accountability and organizational context.
11. Select a rule to edit its details as needed.
12. Update each rule's **State** to **Report-only** when you are ready.

Note

Your original policies aren't changed by the migration. They remain in their previous state, whether on, off, or report-only, and continue to evaluate independently. Original policies that are set to **On** continue to enforce access. New plan rules that are set to **Report-only** record their results in sign-in logs without enforcing controls.

## Validate the plan

After you configure the rules to **Report-only**, use the built-in policy impact metrics or sign-in logs to confirm that the rules produce the expected results before you enable enforcement.

1. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
2. Review sign-in events to confirm that each rule in the plan matches the expected users, applications, and conditions.
3. Compare the plan rule behavior against the original policy behavior. The results should be equivalent.
4. When you're satisfied with the results, return to **Entra ID** &gt; **Conditional Access** &gt; **Policy plans (Preview)**, open the plan, and set each rule's **State** to **On**.

For more information about validating policy behavior before enforcement, see [Analyze Conditional Access policy impact](concept-conditional-access-report-only).

## Decommission the original policies

After you enable and validate the plan rules, disable the original policies. Delete them only after the validation period and when your organization's change-management and retention requirements allow it.

Important

During sign-in evaluation, existing policies and policy plan rules evaluate independently. Every applicable policy and every applicable rule must be satisfied for access to be granted. Disable the original policies only after you're confident that the plan covers your intended security posture.

1. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
2. For each policy that was migrated to the plan, open the policy and set its state to **Off**.
3. Confirm that sign-in behavior remains consistent after the original policies are disabled.
4. After the validation period, delete the original policies if your organization's change-management and retention requirements allow it.

## Maintain the migrated plan

When a new scenario supports the same security objective, add it as a rule in the existing plan instead of creating another standalone policy. Update shared conditions when a change should apply to every rule in the plan.