---
layout: Conceptual
title: Verify mandatory MFA setup for Microsoft Entra users - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-mandatory-multifactor-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Verify that your users meet mandatory MFA requirements for Azure and admin portals. Check and enable MFA for Microsoft Entra ID P1, P2, and Free licenses.
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-106
ms.reviewer: nashahid, gkinasewitz
locale: en-us
document_id: 78a5a27b-848d-d358-b3ec-b17c2668b89d
document_version_independent_id: 78a5a27b-848d-d358-b3ec-b17c2668b89d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-mandatory-multifactor-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-mandatory-multifactor-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-mandatory-multifactor-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 18b85bb5-7cb9-d59e-4b44-69ffc7bd7f6f
---

# Verify mandatory MFA setup for Microsoft Entra users - Microsoft Entra ID | Microsoft Learn

This topic covers steps to verify that users in your organization are set up to meet Azure's mandatory MFA requirements. For more information about which applications and accounts are affected and how the rollout works, see [Planning for mandatory multifactor authentication for Azure and other admin portals](concept-mandatory-multifactor-authentication).

## Verify MFA for a personal account

A user might use their personal account to create a Microsoft Entra tenant for only a few users. If you used your personal account to subscribe to Azure, complete the following steps to confirm that your account is set up for MFA.

1. Sign in to your Microsoft account Security tab at https://account.microsoft.com/security.
2. Select **Manage how I sign in** ​​​​​​​to show the ways to prove who you are.
3. Under **Additional security** and **Two-step verification** choose **Turn on**.
4. Follow the instructions shown on the screen.

For more information, see [How to use two-step verification with your Microsoft account](https://support.microsoft.com/account-billing/how-to-use-two-step-verification-with-your-microsoft-account-c7910146-672f-01e9-50a0-93b4585e7eb4).

## Find users who sign in with and without MFA

Use the following resources to find users who sign in with and without MFA:

- To export a list of users and their authentication methods, use [PowerShell](https://aka.ms/AzMFA).
- If you run queries to analyze user sign-ins, use the application IDs of the [applications that require MFA](concept-mandatory-multifactor-authentication#application-ids-and-urls).

## Verify MFA enablement

All users who access [applications that require MFA](concept-mandatory-multifactor-authentication#application-ids-and-urls) must be set up to use MFA. Mandatory MFA isn't restricted to privileged roles.

Use the following steps to verify that MFA is set up for those users, or to enable it if needed.

1. Sign in to Azure portal as a Global Reader.
2. Browse to **Entra ID** &gt; **Overview**.
3. Check the license type for the tenant subscription.
4. Follow the steps for your license type to verify MFA is enabled, or enable it if needed. To complete these steps, you need to sign out as a Global Reader, and sign back in with a more privileged role.

    - Microsoft Entra ID P1 or Microsoft Entra ID P2
    - Microsoft 365 or Microsoft Entra ID Free

### Verify MFA is enabled for Microsoft Entra ID P1 or Microsoft Entra ID P2 license

If you have a Microsoft Entra ID P1 or Microsoft Entra ID P2 license, you can create a Conditional Access policy to require MFA for users who access [applications that require MFA](concept-mandatory-multifactor-authentication#application-ids-and-urls):

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
6. Under **Include**, select **All users**, or a group of users who sign in to the [applications that require MFA](concept-mandatory-multifactor-authentication#application-ids-and-urls).
7. Under **Target resources** &gt; **Cloud apps** &gt; **Include**, **Select apps**, select **Microsoft Admin Portals** and **Windows Azure Service Management API**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**, **Require authentication strength**, select **Multifactor authentication**, and select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to create to enable your policy.

    Important

    Create the CA Policy in Report-Only mode to understand impact for your tenant so you don't get locked out.

For more information, see [Common Conditional Access policy: Require multifactor authentication for admins accessing Microsoft admin portals](../conditional-access/how-to-policy-mfa-admin-portals).

You can use the Conditional Access insights and reporting workbook that contains sign-in logs to understand impact for your tenant. As a prerequisite, you need to:

- [Create a workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).
- [Integrate activity logs with Azure Monitor](/en-us/entra/identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs).

Choose the following parameters to see how mandatory MFA affects your tenant:

- Select the previously created MFA Conditional Access policy
- Select a time range to evaluate the data
- Select **Data View** to see results in terms of number of users or number of sign-ins

You can query the sign-in details or download the sign-in logs to dive deeper into the data. For more information, see [Conditional Access insights and reporting](/en-us/entra/identity/conditional-access/howto-conditional-access-insights-reporting).

### Verify MFA is enabled for Microsoft 365 or Microsoft Entra ID Free

If you have a Microsoft 365 or Microsoft Entra ID Free license, you can enable MFA by using security defaults. Users are prompted for MFA as needed, but you can't define your own rules to control the behavior.

To enable security defaults:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Properties**.
3. Select **Manage security defaults**.
4. Set **Security defaults** to **Enabled**.
5. Select **Save**.

For more information about security defaults, see [Security defaults in Microsoft Entra ID](../../fundamentals/security-defaults).

If you don't want to use security defaults, you can enable per-user MFA. When you enable users individually, they perform MFA each time they sign in. An Authentication Administrator can enable some exceptions. To enable per-user MFA:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select a user account, and click **Enable MFA**.
4. Confirm your selection in the pop-up window that opens.

After you enable users, notify them by email. Tell the users that a prompt is displayed to ask them to register the next time they sign in. For more information, see [Enable per-user Microsoft Entra multifactor authentication to secure sign-in events](howto-mfa-userstates).