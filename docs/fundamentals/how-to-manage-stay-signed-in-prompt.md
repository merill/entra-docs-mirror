---
layout: HowTo
title: Manage the 'Stay signed in' prompt in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/how-to-manage-stay-signed-in-prompt
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn how the 'Stay signed in' prompt for Microsoft Entra users works and how to configure it in Microsoft Entra ID.
ms.reviewer: almars
ms.date: 2026-04-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- ge-structured-content-pilot
- sfi-ga-nochange
locale: en-us
document_id: 244f6b9a-42f2-73d1-7c8b-6fe219de24ae
document_version_independent_id: 18939379-a92e-9832-d83d-bf8c25bc182e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/how-to-manage-stay-signed-in-prompt.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/how-to-manage-stay-signed-in-prompt
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/how-to-manage-stay-signed-in-prompt.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 10a9251a-0b8d-733b-e790-ec066b723309
---

# Manage the 'Stay signed in' prompt in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

The **Stay signed in?** prompt appears after a user successfully signs in. This process is known as **Keep me signed in (KMSI)** and was previously part of the [customize branding](how-to-customize-branding) process.

This article covers how the KMSI process works, how to enable it for customers, and how to troubleshoot KMSI issues.

## Prerequisites

Configuring the 'keep me signed in' (KMSI) option requires one of the following licenses:

- Microsoft Entra ID Free
- Office 365 (for Office apps)
- Microsoft 365

You must have the **Global Administrator** role to enable the 'Stay signed in?' prompt.

## How does it work?

If a user answers **Yes** to the **'Stay signed in?'** prompt, a persistent authentication cookie is set. The cookie must be stored in session for KMSI to work. KMSI doesn't work with locally stored cookies. If KMSI isn't enabled, a non-persistent cookie is issued and lasts for 24 hours or until the browser is closed.

The following diagram shows the user sign-in flow for a managed tenant and federated tenant using the KMSI prompt. If the user is presented with the **Stay signed in?** prompt and they select 'Yes', the persistent cookie is set.

![Diagram showing the user sign-in flow for a managed vs. federated tenant.](media/how-to-manage-stay-signed-in-prompt/kmsi-workflow.png)

## Special considerations

- The 'Don't show this again' checkbox functions separately from the 'Stay signed in?' flow.
- This experience might not be applicable depending on the authentication requirements configured for your tenant. Some Conditional Access policies and authentication configurations prevent the 'Keep me signed in' flow from being displayed.
- The flow contains smart logic so that the **Stay signed in?** option isn't displayed if the machine learning system detects a high-risk sign-in or a sign-in from a shared device. This scenario is reflected in the diagram, where the 'Keep me signed in' option is removed.
- For federated tenants, the prompt shows after the user successfully authenticates with the federated identity service.
- Some features of SharePoint Online and Office 2010 depend on users being able to choose to remain signed in. If you uncheck the **Show option to remain signed in** option, your users might see other unexpected prompts during the sign-in process.

## Enable the 'Stay signed in?' prompt

The KMSI setting is managed in **User settings**.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Entra ID** &gt; **Users** &gt; **User settings**.
3. Set the **Show keep user signed in** toggle to **Yes**.

    ![Screenshot that shows the User settings page in Microsoft Entra ID with the Show keep user signed in toggle highlighted.](media/how-to-manage-stay-signed-in-prompt/user-settings-page.png)

## Troubleshoot 'Stay signed in?' issues

    If a user doesn't act on the **Stay signed in?** prompt but abandons the sign-in attempt, a sign-in log entry appears in the Microsoft Entra sign-in logs. The prompt the user sees is called an "interrupt."

    ![Screenshot of the Sample Stay signed in? prompt.](media/how-to-manage-stay-signed-in-prompt/kmsi-stay-signed-in-prompt.png)

    Details about the sign-in error are found in the **Sign-in logs**. Select the impacted user from the list and locate the following details in the **Basic info** section.

    - **Sign in error code**: 50140
    - **Failure reason**: This error occurred due to "Keep me signed in" interrupt when the user was signing in.

    You can stop users from seeing the interrupt by setting the **Show option to remain signed in** setting to **No** in the user settings. This setting disables the KMSI prompt for all users in your directory.

    You also can use the [persistent browser session controls in Conditional Access](../identity/conditional-access/howto-conditional-access-session-lifetime) to prevent users from seeing the KMSI prompt. This option allows you to disable the KMSI prompt for a select group of users without affecting sign-in behavior for everyone else in the directory.

    To ensure that the KMSI prompt is shown only when it can benefit the user, the KMSI prompt is intentionally not shown in the following scenarios:

    - User is signed in via seamless SSO and integrated Windows authentication (IWA)
    - User is signed in via Active Directory Federation Services and IWA
    - User is a guest in the tenant
    - User's risk score is high
    - Sign-in occurs during user or admin consent flow
    - Persistent browser session control is configured in a Conditional Access policy