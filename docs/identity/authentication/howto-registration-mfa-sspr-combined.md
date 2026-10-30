---
layout: Conceptual
title: Combined Security Information Registration - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-registration-mfa-sspr-combined
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to simplify the user experience with combined Microsoft Entra multifactor authentication and self-service password reset registration.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: tilarso
locale: en-us
document_id: 12802c79-252a-3284-d0dc-e805a9516ae7
document_version_independent_id: 89652951-8794-7124-e684-273b3f501e1f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-registration-mfa-sspr-combined.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-registration-mfa-sspr-combined
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-registration-mfa-sspr-combined.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3b1c0c9b-439e-28dd-4c72-b881a0dc4e3c
---

# Combined Security Information Registration - Microsoft Entra ID | Microsoft Learn

Before combined registration was introduced, users registered authentication methods for Microsoft Entra multifactor authentication (MFA) and self-service password reset (SSPR) separately. Users were confused that similar methods were used for Microsoft Entra MFA and SSPR, but they had to register for both features. Now, with combined registration, users can register once and get the benefits of both Microsoft Entra MFA and SSPR.

To help you understand the functionality and effects of the new experience, see [Combined security information registration concepts](concept-registration-mfa-sspr-combined).

![Screenshot that shows the combined security information registration enhanced experience.](media/howto-registration-mfa-sspr-combined/combined-security-info-more-required.png)

## Conditional Access policies for combined registration

To secure when and how users register for Microsoft Entra MFA and SSPR, you can use user actions in a Microsoft Entra Conditional Access policy. Organizations can enable this functionality so that users can register for Microsoft Entra MFA and SSPR from a central location. For example, users can use a trusted network location that they access during human resources onboarding.

Note

This policy applies only when a user accesses a combined registration page. This policy doesn't enforce MFA enrollment when a user accesses other applications.

To create an MFA registration policy, see [Microsoft Entra ID Protection: Configure MFA policy](../../id-protection/howto-identity-protection-configure-mfa-policy).

For more information about how to create trusted locations in Conditional Access, see [What is the location condition in Microsoft Entra Conditional Access?](../conditional-access/concept-assignment-network#trusted-locations).

### Create a policy to require registration from a trusted location

In the following procedure, you create a policy that applies to all selected users who attempt to register by using the combined registration experience. Users connected on a nontrusted network must either perform MFA or sign in by using a temporary access pass to register for MFA or reset their password by using SSPR.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **+ New policy**.
4. Enter a name for this policy, such as **Combined Security Info Registration on Trusted Networks**.
5. Under **Assignments**, select **Users**. Choose the users and groups that must use this policy.

    Warning

    Users must be enabled for combined registration.
6. Under **Cloud apps or actions**, select **User actions**. Select the **Register security information** checkbox, and then select **Done**.

    ![Screenshot that shows creating a Conditional Access policy to control security information registration.](media/howto-registration-mfa-sspr-combined/require-registration-from-trusted-location.png)
7. Under **Conditions** &gt; **Locations**, configure the following options:

    1. Configure **Yes**.
    2. Include **Any location**.
    3. Exclude **All trusted locations**.
8. Under **Access controls** &gt; **Grant**, select **Require multifactor authentication**, and then choose **Select**.
9. Set **Enable policy** to **On**.
10. To finalize the policy, select **Create**.