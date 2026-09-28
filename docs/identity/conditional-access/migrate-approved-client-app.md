---
layout: Conceptual
title: Migrate approved client app to application protection policy in Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/migrate-approved-client-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: The approved client app control is going away. Migrate to App protection policies.
ms.topic: how-to
ms.date: 2026-05-29T00:00:00.0000000Z
ms.reviewer: jogro
locale: en-us
document_id: b5b96d45-d3ce-83c2-695c-5b528e32149d
document_version_independent_id: 1315e93b-f3e0-c4aa-d43a-2b9e59378a46
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/migrate-approved-client-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/migrate-approved-client-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/migrate-approved-client-app.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 747611bf-2050-16f5-4a20-4427eee35b41
---

# Migrate approved client app to application protection policy in Conditional Access - Microsoft Entra ID | Microsoft Learn

## Overview

In this article, you learn how to migrate from the "Require approved client app" Conditional Access grant control to the "Require app protection policy" grant control. App protection policies provide the same data loss and protection as approved client app policies, but with other benefits. For more information about the benefits of using app protection policies, see the article [App protection policies overview](/en-us/mem/intune/apps/app-protection-policy).

The **Require approved client app** grant retirement date is extended from March 2026 to June 30, 2026. Organizations must transition all current Conditional Access policies that use **only** the **Require approved client app** grant to **Require approved client app** **or** **Require app protection policy** by June 2026. Additionally, for any new Conditional Access policy, **only** apply the **Require app protection policy** grant.

Important

On **June 30, 2026**, the Conditional Access **Require approved client app** control in Microsoft Entra and any Conditional Access policies that include the approved client app grant control move to a read-only state. Admins can no longer create new policies or edit existing ones that use this control. Admins can still disable or delete existing policies. Existing policies continue to be enforced for end users as long as they remain enabled.

## Edit an existing Conditional Access policy

Require approved client apps or app protection policy with mobile devices

The following steps make an existing Conditional Access policy require an approved client app or an app protection policy when using an iOS/iPadOS or Android device. This policy works in tandem with an app protection policy created in Microsoft Intune.

Organizations can choose to update their policies using the following steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select a policy that uses the approved client app grant.
4. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require approved client app** and **Require app protection policy**.
    2. Under **For multiple controls**, select **Require one of the selected controls**.
5. Confirm your settings and set **Enable policy** to **Report-only**.
6. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Repeat the previous steps on all of your policies that use the approved client app grant.

Warning

Not all applications that are supported as approved applications support application protection policies. For a list of some common client apps, see [App protection policy requirement](concept-conditional-access-grant#require-app-protection-policy). If your application isn't listed there, contact the application developer.

## Create a Conditional Access policy

Require app protection policy with mobile devices

The following steps help create a Conditional Access policy requiring an approved client app or an app protection policy when using an iOS/iPadOS or Android device. This policy works in tandem with an [app protection policy created in Microsoft Intune](/en-us/mem/intune/apps/app-protection-policies).

Organizations can choose to deploy this policy using the following steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and exclude at least one account to prevent yourself from being locked out. If you don't exclude any accounts, you can't create the policy.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Conditions** &gt; **Device platforms**, set **Configure** to **Yes**.
    1. Under **Include**, **Select device platforms**.
    2. Choose **Android** and **iOS**.
    3. Select **Done**.
8. Under **Access controls** &gt; **Grant**, select **Grant access**.
    1. Select **Require approved client app** and **Require app protection policy**.
        1. Under **For multiple controls**, select **Require one of the selected controls**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Note

If an app doesn't support **Require app protection policy**, end users trying to access resources from that app are blocked.