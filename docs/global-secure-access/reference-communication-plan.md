---
layout: Conceptual
title: Global Secure Access change communication plan template - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/reference-communication-plan
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Use this template to plan how you communicate Global Secure Access changes to stakeholders, support teams, and users.
ms.topic: reference
ms.date: 2026-05-04T00:00:00.0000000Z
ms.reviewer: tdetzner
ai-usage: ai-assisted
locale: en-us
document_id: 43b7b40c-c555-83fe-aecd-2970e17ba0b8
document_version_independent_id: 43b7b40c-c555-83fe-aecd-2970e17ba0b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/reference-communication-plan.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/reference-communication-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/reference-communication-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: ce1d6841-6f04-4375-509f-5ed060dc64c2
---

# Global Secure Access change communication plan template - Global Secure Access | Microsoft Learn

Use this template for **normal** and **major** changes that have user-visible impact. Adapt the communication channels and timing to your organization's practices.

## Communication plan details

| Field | Value |
| --- | --- |
| **Change ID** | *(match the change request template)* |
| **Change summary** | *(one-sentence description)* |
| **Change date and time** |  |
| **Expected duration** |  |
| **Expected user impact** | *(for example, brief reconnection, temporary access loss, new client version required)* |

## Stakeholder notification matrix

| Audience | When to notify | Channel | Owner | Sent? |
| --- | --- | --- | --- | --- |
| **Operations team** | Five business days before change | Team meeting or Teams channel | Service owner | [ ] |
| **IT support / help desk** | Three business days before change | Email and knowledge base article update | Network security engineer | [ ] |
| **Affected users** | Two business days before change | Email or company portal announcement | Service owner | [ ] |
| **Security / SOC team** | Two business days before change | Email or security information and event management (SIEM) notification | Network security engineer | [ ] |
| **Management / leadership** | Two business days before major changes | Email summary | Service owner | [ ] |
| **All stakeholders** | Immediately after change completion | Email or Teams channel update | Service owner | [ ] |

## Prechange notification template

**Subject:** Planned Global Secure Access maintenance—*date and time*

**What is happening:**

*Briefly describe the change. Keep it nontechnical for users.*

**When:**

*Date of the change, start time, expected end time, and time zone.*

**Who is affected:**

*Describe the affected user groups, sites, or applications.*

**Expected impact:**

Describe what users experience. Be specific. Examples:

- "You might be briefly disconnected and need to reconnect."
- "Access to *application* is temporarily unavailable."
- "No user impact expected. We're notifying you as a precaution."

**What you need to do:**

If users must take action, list it here. If no action is needed, say so. Examples:

- "No action required on your part."
- "Restart the Global Secure Access client after *time*."
- "Save your work before *time* as a precaution."

**Questions?**

Contact *help desk email or Teams channel* if you have questions or experience issues after the maintenance window.

## Post-change notification template

**Subject:** Global Secure Access maintenance completed—*date*

**The planned maintenance on *date* is complete.**

**What was changed:***Brief summary*

**Impact:***Confirm whether the maintenance completed within the expected window and whether any unexpected impact occurred.*

**If you experience issues:** Contact *help desk email or Teams channel*. Reference ticket *Change ID*.

## Communication checklist

- Prechange notification drafted and reviewed
- Help desk briefed and knowledge base updated with expected issues and responses
- Prechange notification sent to all audiences in the stakeholder notification matrix
- Day-of reminder sent (for major changes affecting many users)
- Post-change notification sent after the change completes
- Help desk debriefed on any unexpected issues reported during the change

## Escalation during change

If unexpected issues arise during the change, use this escalation path:

| Severity | Escalation action | Contact |
| --- | --- | --- |
| Minor (cosmetic, &lt; 5 users affected) | Notify operations team; continue monitoring | *Team channel or on-call engineer* |
| Moderate (&gt; 5 users affected, workaround available) | Notify service owner; decide whether to continue or roll back | *Service owner name and contact* |
| Major (widespread outage, no workaround) | Roll back immediately; notify all stakeholders; open incident | *Incident management process or bridge call number* |

**Notes:**