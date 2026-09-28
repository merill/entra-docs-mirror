---
layout: Conceptual
title: What is the Identity Secure Score? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-identity-secure-score
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to use the Identity Secure Score to improve the security posture of your Microsoft Entra tenant.
ms.topic: how-to
ms.date: 2026-02-09T00:00:00.0000000Z
ms.reviewer: jadedsouza
locale: en-us
document_id: bfcc3d22-db50-3c7a-a6b8-b9740a34920c
document_version_independent_id: d283a2fc-92fc-ab0e-5a7d-b92248213d2e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/concept-identity-secure-score.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/concept-identity-secure-score
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/concept-identity-secure-score.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8696ca4c-6433-9a0e-e1e4-6b046d7f11a1
---

# What is the Identity Secure Score? - Microsoft Entra ID | Microsoft Learn

The Identity Secure Score is shown as a percentage that functions as an indicator for how aligned you are with Microsoft's recommendations for security. Each improvement action in Identity Secure Score is tailored to your configuration. You can access the score and view individual recommendations related to your score in Microsoft Entra recommendations. You can also see how your score changes over time.

[![Screenshot of the Recommendations page with the Secure Score details highlighted.](media/concept-identity-secure-score/secure-score-overview.png)](media/concept-identity-secure-score/secure-score-overview.png#lightbox)

## Prerequisites

- Identity Secure Score is available to free and paid customers.
- Some recommendations require a paid license to view and act on. For more information, see [What are Microsoft Entra recommendations](overview-recommendations).
- To *view* the improvement action but not update, you need at least the [Service Support Administrator](../role-based-access-control/permissions-reference#service-support-administrator) role.
- To *update* the status of an improvement action, you need at least the [SharePoint Administrator](../role-based-access-control/permissions-reference#sharepoint-administrator) role.
- For a full list of roles, see [Least privileged roles by task](../role-based-access-control/delegate-by-task#monitoring-and-health---recommendations-least-privileged-roles).

## How does the Identity Secure Score benefit me?

This score helps to objectively measure your identity security posture, help you plan identity security improvements, and review the success of your improvements. By following the improvement actions in the Microsoft Entra recommendations, you can take advantage the features available to your organization as part of your identity investments.

The following recommendations are included in the Identity Secure Score:

- Configure VPN integration
- Designate more than one Global Administrator
- Do not allow users to grant consent to unreliable applications
- Do not expire passwords
- Edit misconfigured agent certificate templates
- Edit misconfigured enrollment agent certificate template
- Enable policy to block legacy authentication
- Enable password hash sync if hybrid
- Enable self-service password reset
- Ensure all users can complete MFA
- Modify unsecure Kerberos delegations to prevent impersonation
- Protect all users with a sign-in risk policy
- Protect all users with a user risk policy
- Protect and manage local admin passwords with Microsoft LAPS
- Remove dormant accounts from sensitive groups
- Remove unsafe permissions on sensitive Microsoft Entra Connect accounts
- Replace Enterprise or Domain Admin account for Microsoft Entra Connect AD DS Connector
- Require multifactor authentication (MFA) for administrative roles
- Reversible passwords found in GPOs
- Rotate password for Microsoft Entra Connect AD DS Connector account
- Stop clear text credentials exposure
- Stop weak cipher usage
- Use least privileged administrative roles

## How does it work?

Every 24 hours, we look at your security configuration and compare your settings with the recommended best practices. Based on the outcome of this evaluation, a new score is calculated for your directory. It’s possible that your security configuration isn’t fully aligned with the best practice guidance and the improvement actions are only partially met. In these scenarios, you're awarded a portion of the max score available for the control.

## How do I use the Identity Secure Score?

To access the Identity Secure Score:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Reader](../role-based-access-control/permissions-reference#global-reader).
2. Browse to **Entra ID** &gt; **Identity Secure Score** to view the dashboard or **Entra ID** &gt; **Overview** &gt; **Recommendations**. Select the **Security** filter option to see only those recommendations that are included in the Identity Secure Score.

[![Screenshot of the Entra recommendations with the Secure Score filter highlighted.](media/concept-identity-secure-score/recommendations-secure-score.png)](media/concept-identity-secure-score/recommendations-secure-score.png#lightbox)

Each recommendation is measured based on your configuration. If you're using non-Microsoft products to enable a best practice recommendation, you can indicate this configuration in the settings of an improvement action. You might set recommendations to be ignored if they don't apply to your environment. An ignored recommendation doesn't contribute to the calculation of your score.

[![Screenshot of the improvement action panel.](media/concept-identity-secure-score/identity-secure-score-ignore-or-non-microsoft-recommendations.png)](media/concept-identity-secure-score/identity-secure-score-ignore-or-non-microsoft-recommendations.png#lightbox)

- **To address** - You recognize that the improvement action is necessary and plan to address it at some point in the future. This state also applies to actions that are detected as partially, but not fully completed.
- **Risk accepted** - Security should always be balanced with usability, and not every recommendation works for everyone. When that is the case, you can choose to accept the risk, or the remaining risk, and not enact the improvement action. You aren't awarded any points, and the action isn't visible in the list of improvement actions. You can view this action in history or undo it at any time.
- **Planned** - There are concrete plans in place to complete the improvement action.
- **Resolved through third party** and **Resolved through alternate mitigation** - The improvement action was addressed by a non-Microsoft application or software, or an internal tool. You're awarded the points the action is worth, so your score better reflects your overall security posture. If a non-Microsoft or internal tool no longer covers the control, you can choose another status. Keep in mind, Microsoft has no visibility into the completeness of implementation if the improvement action is marked as either of these statuses.

## Frequently asked questions

Many factors can affect your score. Here are some frequently asked questions about the Identity Secure Score.

### How are the recommendations scored?

Recommendations can be scored in two ways. Some are scored in a binary fashion, so you get 100% of the score if you have the feature or setting configured based on our recommendation. Other scores are calculated as a percentage of the total configuration. For example, the recommendation states there's a maximum of 10.71% increase if you protect all your users with MFA. You have 5 of 100 total users protected, so you're given a partial score around 0.53% (5 protected / 100 total \* 10.71% maximum = 0.53% partial score).

### What does [Not Scored] mean?

Actions labeled as [Not Scored] are ones you can perform in your organization but aren't scored. So, you can still improve your security, but you aren't given credit for those actions right now.

### My score changed. How do I figure out why?

The [Microsoft Defender XDR portal](https://security.microsoft.com/) shows your complete Microsoft secure score. You can easily see all the changes to your secure score by reviewing the in-depth changes on the history tab.

### Does the score measure my risk of getting breached?

No, score doesn't express an absolute measure of how likely you're to get breached. It expresses the extent to which you adopted features that can *offset* risk. No service can guarantee protection, and the score shouldn't be interpreted as a guarantee in any way.

### Is there a minimum score I should aim for?

Instead of focusing on a specific score, you should focus on the high importance recommendations that are relevant to your organization. It's more beneficial to have a high score on the high importance recommendations than a high score on low importance recommendations.

### How should I interpret my score?

Your score improves for configuring recommended security features or performing security-related tasks (like reading reports). Some actions are scored for partial completion, like enabling multifactor authentication (MFA) for your users. Your secure score is directly representative of the Microsoft security services you use. Remember that security must be balanced with usability. All security controls have a user impact component. Controls with low user impact should have little to no effect on your users' day-to-day operations.

### How does the Identity Secure Score relate to the Microsoft 365 secure score?

The [Microsoft secure score](/en-us/microsoft-365/security/defender/microsoft-secure-score) contains five distinct control and score categories:

- Identity
- Data
- Devices
- Infrastructure
- Apps

The Identity Secure Score represents the identity part of the Microsoft secure score. This overlap means that your recommendations for the Identity Secure Score and the identity score in Microsoft are the same.