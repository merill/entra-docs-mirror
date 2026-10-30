---
layout: Conceptual
title: Find and address gaps in strong authentication coverage for your administrators in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-authentication-find-coverage-gaps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to find and address gaps in strong authentication coverage for your administrators in Microsoft Entra ID
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: inbarc
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: 4180415d-70f5-1ab2-408f-1f850c678829
document_version_independent_id: d868ad2e-b8fd-bd12-f843-be7a3be80aba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-authentication-find-coverage-gaps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-authentication-find-coverage-gaps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-authentication-find-coverage-gaps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 56792c2a-d919-4475-450a-0ac2d1c66a15
---

# Find and address gaps in strong authentication coverage for your administrators in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Requiring multifactor authentication (MFA) for the administrators in your tenant is one of the first steps you can take to increase the security of your tenant. In this article, we'll cover how to ensure all of your administrators are covered by multifactor authentication.

## Detect current usage for Microsoft Entra Built-in administrator roles

The [Microsoft Entra ID Secure Score](../monitoring-health/concept-identity-secure-score) provides a score for **Require MFA for administrative roles** in your tenant. This improvement action tracks the MFA usage of those with [administrator roles](../role-based-access-control/permissions-reference).

There are different ways to check if your admins are covered by an MFA policy.

- To troubleshoot sign-in for a specific administrator, you can use the sign-in logs. The sign-in logs let you filter **Authentication requirement** for specific users. Any sign-in where **Authentication requirement** is **Single-factor authentication** means there was no multifactor authentication policy that was required for the sign-in.

    ![Screenshot of the sign-in log.](media/how-to-authentication-find-coverage-gaps/auth-requirement.png)

    When viewing the details of a specific sign-in, select the **Authentication details** tab for details about the MFA requirements. For more information, see [Sign-in log activity details](../monitoring-health/concept-sign-in-log-activity-details).

    ![Screenshot of the authentication activity details.](media/how-to-authentication-find-coverage-gaps/details.png)
- To choose which policy to enable based on your user licenses, we have a new MFA enablement wizard to help you [compare MFA policies](concept-mfa-licensing#compare-multi-factor-authentication-policies) and see which steps are right for your organization. The wizard shows administrators who were protected by MFA in the last 30 days.

    ![Screenshot of the multifactor authentication enablement wizard.](media/how-to-authentication-find-coverage-gaps/wizard.png)
- You can run [this script](https://github.com/microsoft/AzureADToolkit/blob/main/src/Find-AADToolkitUnprotectedUsersWithAdminRoles.ps1) to programmatically generate a report of all users with directory role assignments who have signed in with or without MFA in the last 30 days. This script will enumerate all active built-in and custom role assignments, all eligible built-in and custom role assignments, and groups with roles assigned.

## Enforce multifactor authentication on your administrators

If you find administrators who aren't protected by multifactor authentication, you can protect them in one of the following ways:

- If your administrators are licensed for Microsoft Entra ID P1 or P2, you can [create a Conditional Access policy](tutorial-enable-azure-mfa) to enforce MFA for administrators. You can also update this policy to require MFA from users who are in custom roles.
- Run the [MFA enablement wizard](https://aka.ms/MFASetupGuide) to choose your MFA policy.
- If you assign custom or built-in admin roles in [Privileged Identity Management](../../id-governance/privileged-identity-management/pim-configure), require multifactor authentication upon role activation.

## Use Passwordless and phishing resistant authentication methods for your administrators

After your admins are enforced for multifactor authentication and have been using it for a while, it's time to increase authentication strength and use Passwordless and phishing resistant authentication methods:

- [Phone Sign-in (with Microsoft Authenticator)](concept-authentication-authenticator-app)
- [FIDO2](concept-authentication-passkeys-fido2)
- [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/)

You can read more about these authentication methods and their security considerations in [Microsoft Entra authentication methods](overview-authentication).