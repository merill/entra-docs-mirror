---
layout: Conceptual
title: Troubleshoot Conditional Access Authentication Strengths - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/troubleshoot-authentication-strengths
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to resolve errors when you're using Microsoft Entra Conditional Access authentication strengths.
ms.topic: troubleshooting
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: inbarc
ms.custom: sfi-image-nochange
locale: en-us
document_id: 82cb6ce4-502f-f506-322a-be23fe19ac6f
document_version_independent_id: 8587c54e-e07c-6fe8-4697-8911e5dfa531
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/troubleshoot-authentication-strengths.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/troubleshoot-authentication-strengths
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/troubleshoot-authentication-strengths.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: aba40ae9-e4f3-5012-3b0d-d518c8226e4f
---

# Troubleshoot Conditional Access Authentication Strengths - Microsoft Entra ID | Microsoft Learn

This article describes how to resolve problems that might happen when you use Microsoft Entra Conditional Access authentication strengths.

## A user is asked to sign in with another method, but an expected method doesn't appear

For sign-in, the authentication method needs to be:

- Registered for the user.
- Enabled by the policy for authentication methods.

For more information, see [How Conditional Access authentication strengths work](concept-authentication-strength-how-it-works).

To verify that you can use a method:

1. Check which authentication strength is required. Select **Security** &gt; **Authentication methods** &gt; **Authentication strengths**.
2. Check the policy for authentication methods to see if the user is enabled for any method that the authentication strength requires. Select **Security** &gt; **Authentication methods** &gt; **Policies**.
3. As needed, check if the tenant is enabled for any method that the authentication strength requires. Select **Security** &gt; **Multifactor Authentication** &gt; **Additional cloud-based multifactor authentication settings**.
4. Check which authentication methods are registered for the user in the policy for authentication methods. Select **Users and groups** &gt; *username* &gt; **Authentication methods**.

If the user is registered for an enabled method that meets the authentication strength, the user might need to use another method that isn't available after primary authentication, such as Windows Hello for Business. For more information, see [Authentication methods in Microsoft Entra ID](overview-authentication). The user needs to restart the session, select **Sign-in options**, and then select a method that the authentication strength requires.

![Screenshot of the dialog for choosing another sign-in method.](media/troubleshoot-authentication-strengths/choose-another-method.png)

## A user can't access a resource

If an authentication strength requires a method that a user can't use, the user is blocked from signing in. To check which method an authentication strength requires, and which method the user is registered and enabled to use, follow the steps in the previous section.

## You need to check which authentication strength was enforced during sign-in

Use the **Sign-ins** log to find more information about the sign-in:

- On the **Authentication Details** tab, the **Requirement** column shows the name of the authentication strength policy.

    ![Screenshot that shows authentication strengths in a sign-in log.](media/troubleshoot-authentication-strengths/sign-in-logs-authentication-details.png)
- On the **Conditional Access** tab, you can see which Conditional Access policy was applied. Select the name of the policy, and look for **Grant Controls** to see the authentication strength that was enforced.

    ![Screenshot that shows an authentication strength under Conditional Access policy details in a sign-in log.](media/troubleshoot-authentication-strengths/sign-in-logs-control.png)

## A user can't register a new method during sign-in

Some methods can't be registered during sign-in, or they need more setup beyond the combined registration. For more information, see [Register passwordless authentication methods](concept-authentication-strength-how-it-works#registration-of-passwordless-authentication-methods).

![Screenshot of a sign-in error when a user can't register a method.](media/troubleshoot-authentication-strengths/register.png)