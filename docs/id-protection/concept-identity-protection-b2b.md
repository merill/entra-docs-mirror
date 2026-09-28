---
layout: Conceptual
title: Microsoft Entra ID Protection for B2B Users - Microsoft Entra ID Protection | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-protection/concept-identity-protection-b2b
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: shlipsey3
ms.author: sarahlipsey
ms.service: entra-id-protection
manager: dougeby
description: Learn how to use Microsoft Entra ID Protection for B2B users to secure your organization. Discover benefits and steps to unblock accounts.
ms.topic: concept-article
ms.date: 2025-08-06T00:00:00.0000000Z
ms.reviewer: chuqiaoshi
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6e0625bb-7367-0bb3-7380-55ac91bde11f
document_version_independent_id: efa6711d-73b0-c30f-2e13-97f29beebedb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-protection/concept-identity-protection-b2b.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-protection/concept-identity-protection-b2b
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-protection/concept-identity-protection-b2b.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/079cf7bf-da09-4bd3-ab74-bd5a5da031d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b606cead-f1a2-4925-9a71-5fbd7a0d9b81
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 48b56437-e482-4252-e36c-30b283387b49
---

# Microsoft Entra ID Protection for B2B Users - Microsoft Entra ID Protection | Microsoft Learn

You can use your organizational credentials to sign in to another organization as a guest. This process is referred to [business-to-business or B2B collaboration](../external-id/what-is-b2b). Organizations can configure Conditional Access policies to block users from signing in if their credentials are considered [at risk](concept-identity-protection-risks). Microsoft Entra ID Protection detects compromised credentials for Microsoft Entra users, including B2B users. If your credential is detected as compromised, it means that someone else might have your password and is using it illegitimately. To prevent further risk to your account, it's important to securely reset your password so that the bad actor can no longer use your compromised password.

If your account is at risk and you're blocked from signing in to another organization as a guest, you might be able to self-remediate your account using the steps in this article.

## Unblock your account

If you're attempting to sign in to another organization as a guest and are blocked due to risk, you see the following block message: "Your account is blocked. We've detected suspicious activity on your account."

![Screenshot of error message showing guest account blocked, contact your organization's administrator.](media/concept-identity-protection-b2b/risky-guest-user-blocked.png)

If your organization enables it, you can use self-service password reset to unblock your account and get your credentials back to a safe state.

1. Go to the [Password reset portal](https://passwordreset.microsoftonline.com/) and initiate the password reset. If self-service password reset isn't enabled for your account and you can't proceed, reach out to your IT administrator with the following information.
2. If self-service password reset is enabled for your account, you're prompted to verify your identity using security methods before changing your password. For assistance, see the [Reset your work or school password](https://support.microsoft.com/account-billing/reset-your-work-or-school-password-using-security-info-23dde81f-08bb-4776-ba72-e6b72b9dda9e) article.
3. Once you have successfully and securely reset your password, your user risk is remediated. You can now try again to sign in as a guest user.

If after resetting your password you're still blocked as a guest due to risk, reach out to your organization's IT administrator.

## How to remediate a user's risk as an administrator

ID Protection automatically detects risky users for Microsoft Entra tenants. If you haven't checked the ID Protection reports before, there might be a large number of users with risk. Since resource tenants can apply user risk policies to guest users, your users can be blocked due to risk even if they were previously unaware of their risky state. If your user reports they're blocked as a guest user in another tenant due to risk, it's important to remediate the user to protect their account and enable collaboration.

### Reset the user's password

From the [Risky users report](https://portal.azure.com/#blade/Microsoft_AAD_IAM/SecurityMenuBlade/RiskyUsers) in Microsoft Entra ID Protection, search for the impacted user with the 'User' filter. Select the impacted user in the report and select **Reset password** in the top toolbar. The user will be assigned a temporary password that must be changed on the next sign-in. This process remediates their user risk and brings their credentials back to a safe state.

### Manually dismiss user's risk

If password reset isn't an option for you, you can choose to manually dismiss user risk. Dismissing user risk doesn't have any effect on the user's existing password, but this process changes the user's **Risk State** from **At Risk** to **Dismissed**. It's important that you change the user's password using whatever means are available to you in order to bring the identity back to a safe state.

To dismiss user risk, go to the [Risky users report](https://portal.azure.com/#blade/Microsoft_AAD_IAM/SecurityMenuBlade/RiskyUsers) in the Microsoft Entra Security menu. Search for the impacted user using the 'User' filter and select the user. Select the **Dismiss user risk** option from the toolbar. This action might take a few minutes to complete and update the user risk state in the report.

To learn more about Microsoft Entra ID Protection, see [What is ID Protection](overview-identity-protection).

## How does ID Protection work for B2B users?

The user risk for B2B collaboration users is evaluated at their home directory. The real-time sign-in risk for these users is evaluated at the resource directory when they try to access the resource. With Microsoft Entra B2B collaboration, organizations can enforce risk-based policies for B2B users using ID Protection. These policies be configured in two ways:

- Administrators can configure their Conditional Access policies, using sign-in risk as a condition, and includes guest users.
- Administrators can configure the built-in ID Protection risk-based policies, that apply to all apps, and include guest users.

## Limitations of ID Protection for B2B collaboration users

There are limitations in the implementation of ID Protection for B2B collaboration users in a resource directory, due to their identity existing in their home directory. The main limitations include:

- If a guest user triggers the ID Protection user risk policy to force password reset, **they will be blocked**. This block is due to the inability to reset passwords in the resource directory.
- **Guest users do not appear in the risky users report**. This limitation is due to the risk evaluation occurring in the B2B user's home directory.
- Administrators **cannot dismiss or remediate a risky B2B collaboration user** in their resource directory. This limitation is due to administrators in the resource directory not having access to the B2B user's home directory.