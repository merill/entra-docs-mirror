---
layout: Conceptual
title: Guest lifecycle policies in Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/guest-lifecycle-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to configure guest lifecycle policies in Lifecycle Workflows to govern external collaboration.
ms.subservice: lifecycle-workflows
ms.topic: how-to
ms.date: 2026-03-13T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6ad26d32-feb3-10fb-2046-0c623f5d7929
document_version_independent_id: 6ad26d32-feb3-10fb-2046-0c623f5d7929
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/guest-lifecycle-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/guest-lifecycle-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/guest-lifecycle-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 69680105-aeba-ffa5-93d7-1acd707b79d4
---

# Guest lifecycle policies in Lifecycle Workflows - Microsoft Entra ID Governance | Microsoft Learn

Important

Guest lifecycle policies are currently in preview. Preview features are provided without a service-level agreement and aren't recommended for production workloads. Certain features might not be supported or might have limited capabilities. This preview is available in the public cloud.

Guest lifecycle policies in Lifecycle Workflows help you govern external collaboration at scale. You can define which Microsoft Entra guest users are covered, configure rules that evaluate guest lifecycle signals, notify sponsors or guests, and automatically disable or delete accounts that no longer meet policy requirements.

With guest lifecycle policies, you can focus on business rules that apply at scale instead of building and maintaining individual workflows.

## Key benefits

- **Reduce stale guest access:** Regular attestation and inactivity controls help remove external accounts that no longer need access.
- **Apply consistent governance:** Tenant-wide defaults, attribute and group scoping, exclusions, and policy precedence provide predictable enforcement.
- **Automate guest enforcement:** Choose deletion, disablement, or disablement followed by deletion after a grace period.
- **Improve sponsor accountability:** Notify sponsors before enforcement actions.
- **Support gradual adoption:** Use multiple policies and targeted scopes to introduce controls to selected populations.
- **Increase operational visibility:** Review processing status, users in scope, compliance state, and the policy enforced for a guest.

## Before you begin

### License requirements

To configure guest lifecycle policies, your tenant must have:

- A Microsoft Entra ID Governance license.
- A connected Azure subscription for the guest add-on meter.

Important

Guest lifecycle policies use the Microsoft Entra ID Governance monthly active users (MAU) billing model for guest users. For information about billable actions and licensing requirements, see [Microsoft Entra ID Governance licensing for guest users](microsoft-entra-id-governance-licensing-for-guest-users).

### Roles and permissions

You need one of the following roles to manage guest lifecycle policies:

- Lifecycle Workflows Administrator
- Global Administrator
- Global Reader (read-only)

### Supported guest users and data

- Policies apply to users whose Microsoft Entra `userType` property is set to `Guest`, regardless of how the guest account was created or invited.
- Creation-date scope uses the guest object's `createdDateTime` property and can include guests created through first-party applications or other invitation sources.
- Attribute-based rules can use supported standard user properties, on-premises extension attributes 1 through 15, directory extensions, and custom security attributes, subject to the attributes exposed in the preview experience.
- Group inclusion and exclusion use direct membership. Nested groups aren't evaluated.
- Access-based conditions depend on access package assignment data.

### Policy concepts

| Term | Description |
| --- | --- |
| **Policy** | A set of guest scoping criteria, policy rules, policy actions, and notifications. |
| **Rules** | Lifecycle signals that a guest must satisfy, such as sponsor attestation, recent activity, access package assignment, minimum sponsor count, or redemption state. |
| **Scope** | The guests to which a policy applies, including tenant-wide coverage, creation date, attributes, groups, or exclusions. |
| **Precedence** | The priority order used to resolve conflicts when more than one policy matches a guest. |
| **Action** | The automated enforcement action taken when a guest doesn't meet policy requirements. |

The following procedure explains how to create a guest lifecycle policy, define its scope and rules, choose an enforcement action, and set its precedence. Validate the configuration with a limited guest population before you enable broad enforcement.

## Create a guest lifecycle policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with a role that can manage guest lifecycle policies.
2. Browse to **ID Governance** &gt; **Lifecycle Workflows** &gt; **Lifecycle Policies** &gt; **Guest Lifecycle Policies** &gt; **Create policy**.
3. Enter a unique policy name and a description that identifies the intended guest population and purpose.
4. Configure the policy scope and rules.
5. Choose the policy action and, if desired, the grace period.
6. Review the notification behavior.
7. Set the policy priority if other guest lifecycle policies exist.
8. Review the configuration, create the policy, and enable it when you're ready for evaluation and enforcement.

After you save the policy, Lifecycle Workflows periodically evaluates it, identifies guests who violate the policy rules, and starts the enforcement cycle according to the policy configuration.

## Define the policy scope

You can start broadly with **All guests** or narrow the policy to a selected population. If you select **All guests**, the policy includes existing guest users in the tenant regardless of invitation source.

Scoping options include:

- All guests, including existing guests.
- Guests that match specific conditions based on supported attributes.
- Guests that are direct members of specified groups.
- All guests except direct members of specified groups. If you select multiple exclusion groups, a direct member of any selected group is excluded.

Note

Use exclusions carefully. A guest who is excluded from one policy might still match another policy, depending on the other policy's scope and precedence.

## Configure policy rules

A policy can contain multiple rules. A rule determines whether a guest remains compliant or becomes eligible for enforcement. Confirm the final rule-combination behavior in a test environment before you enable the policy in production.

| Policy rule | Default | Configuration range | Purpose |
| --- | --- | --- | --- |
| **Sponsor attestation** | 90 days | 30–365 days | Requires a sponsor to periodically confirm that the guest still needs access. Sponsors complete the attestation in My Access under **Sponsored guests**. |
| **Activity requirement** | 90 days | 30–730 days | Requires guests to be active within the configured period. Activity that the service recognizes, including signing in to the tenant, satisfies this requirement. |
| **Access package assignment expiration** | N/A | Enable or disable | Begins guest disablement or deletion after a guest loses their last access package assignment. This rule applies to all guest users, not only users marked as governed in entitlement management. For more information, see [Configure the lifecycle of external users in entitlement management](entitlement-management-access-package-manage-lifecycle). |
| **Minimum sponsor count** | 1 | 1–5 sponsors | Requires the guest to have at least the configured number of sponsors. A group-valued sponsor counts as one sponsor. |
| **Guest redemption** | 30 days | 1–30 days | Begins deletion for invited guests whose `externalUserState` property is set to `PendingAcceptance`. |

## Configure enforcement

### Policy actions

Choose the action to take when a guest doesn't satisfy the policy by the enforcement deadline:

- **Delete:** Delete the guest account.
- **Disable:** Disable the guest account.
- **Disable, then delete:** Immediately disable the account, and then automatically delete it after a grace period from 7 through 90 days. The default is 30 days.
- **Grace period:** If a guest becomes noncompliant with any policy rule, delay the policy action by configuring a grace period of at least one day. The default is seven days.

### Notifications

Lifecycle Workflows can send up to three notifications during enforcement. The notification events depend on the selected policy action and whether a grace period is configured.

- **Pre-action notification:** When a guest becomes noncompliant and a grace period is configured, Lifecycle Workflows notifies the guest and sponsor before enforcement.
- **Disable notification:** Lifecycle Workflows immediately notifies the sponsor when the guest account is disabled and access is revoked.
- **Delete notification:** Lifecycle Workflows immediately notifies the sponsor when the guest account is deleted and access is revoked.

### Multiple policies and precedence

You can configure multiple guest lifecycle policies with different scopes and settings. You can view, enable, disable, delete, and reorder policies. When more than one policy matches a guest, the configured priority determines which policy is enforced.

Important

A guest can be assigned to only one policy at a time. If a guest matches multiple policies, the policy with the highest precedence applies. Policies with lower precedence aren't evaluated.

Before you enable multiple policies, place the most specific or most important policies higher in the precedence order.

A tenant can have up to 20 guest lifecycle policies.

## Monitor and manage policies

### View policy processing and scope

For each policy, you can view:

- The number of guests in scope.
- The list of guests in scope.
- Each guest's compliance state, such as **Compliant**, **Noncompliant**, or **Not evaluated**.
- The policy being enforced for a selected guest.

### Delete and restore a policy

Deleted policies are soft-deleted and can be restored. A restored policy is disabled regardless of its previous state and is placed at the lowest priority. Review its scope, rules, notifications, action, and precedence before you enable it again.

## How guest lifecycle policy enforcement works

1. **Scope evaluation:** Lifecycle Workflows identifies guest users who match the policy's inclusion rules and don't match its exclusions.
2. **Condition evaluation:** Lifecycle Workflows evaluates the policy rules for each guest to determine whether the guest is compliant or noncompliant.
3. **Enforcement:** If the guest is noncompliant, Lifecycle Workflows performs the configured action. If a grace period is enabled, enforcement occurs when the grace period ends.
4. **Notification:** Lifecycle Workflows sends the applicable notifications to the sponsor and guest.
5. **Status update:** Lifecycle Workflows updates policy processing and guest compliance information in the management experience.

Lifecycle Workflows evaluates enabled guest lifecycle policies once per day.

## Guest lifecycle policy recommendations

Use the following practices when you deploy guest lifecycle policies:

- Start with a limited guest population, and confirm the policy scope and behavior before broader implementation.
- Use disablement followed by deletion when your organization requires a recovery period before permanent deletion.
- Ensure that guests have sponsors so that reminders reach the intended recipients.
- Place narrowly targeted policies above broader policies, and review overlapping scopes whenever you change precedence.
- Monitor processing status, enforcement errors, and guest compliance after each policy change.
- Document exclusions, and review them periodically so that exceptions don't become permanent unmanaged access.

## Troubleshooting

| Issue | What to check |
| --- | --- |
| Guest isn't in scope | Confirm that the object has `userType` set to `Guest`. Review creation-date, attribute, and direct group rules. Check explicit user and group exclusions, and inspect higher-priority policies. |
| Policy hasn't started | Confirm that the policy is enabled, the tenant meets licensing and guest-meter requirements, and the Lifecycle Workflows managed schedule has had time to run. |
| Unexpected policy is enforced | Review all matching policies and their precedence order. Move the intended policy higher only after you assess the effect on overlapping populations. |
| Sponsor didn't receive email | Confirm that a sponsor is assigned and has a usable mail attribute. If there's no sponsor, verify that the guest can receive mail. Review delivery errors and additional-recipient settings. |
| Restored policy isn't running | Restored policies are disabled and placed at the lowest priority. Review and explicitly enable the policy. |