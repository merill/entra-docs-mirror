---
layout: Conceptual
title: How to Require Device Compliance with Conditional Access - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-device-compliance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to enforce device compliance with Conditional Access policies. Ensure secure access to resources by meeting your organization's configuration requirements.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: jodah
locale: en-us
document_id: 198421d7-d91d-3a2c-7c80-d81277721f0b
document_version_independent_id: 198421d7-d91d-3a2c-7c80-d81277721f0b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/policy-all-users-device-compliance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/policy-all-users-device-compliance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/policy-all-users-device-compliance.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f3bc5512-ca07-d8e9-ab4b-e1e6bac89583
---

# How to Require Device Compliance with Conditional Access - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Intune and Microsoft Entra work together to secure your organization through [device compliance policies](/en-us/mem/intune/protect/device-compliance-get-started) and Conditional Access. Device compliance policies ensure user devices meet minimum configuration requirements. The requirements can be enforced when users access services protected with Conditional Access policies.

Some organizations might not be ready to require device compliance for all users. These organizations might instead choose to deploy the following policies:

- [Require a compliant or Microsoft Entra hybrid joined device for administrators](policy-alt-admin-device-compliand-hybrid)
- [Require a compliant device, Microsoft Entra hybrid joined device, **OR** multifactor authentication for all users](policy-alt-all-users-compliant-hybrid-or-mfa)
- [Block unknown or unsupported device platforms](policy-all-users-device-unknown-unsupported)
- [Disable browser persistence](policy-all-users-persistent-browser)

## User exclusions

Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policies:

- **Emergency access** or **break-glass**accounts to prevent lockout due to policy misconfiguration. In the unlikely scenario where all administrators are locked out, your emergency access administrative account can be used to sign in and recover access.
    - More information can be found in the article, [Manage emergency access accounts in Microsoft Entra ID](../role-based-access-control/security-emergency-access).
- **Service accounts** and **Service principals**, such as the Microsoft Entra Connect Sync Account. Service accounts are noninteractive accounts that aren't tied to any specific user. They're typically used by backend services to allow programmatic access to applications, but they're also used to sign in to systems for administrative purposes. Calls made by service principals aren't blocked by Conditional Access policies scoped to users. Use Conditional Access for workload identities to define policies that target service principals.
    - If your organization uses these accounts in scripts or code, replace them with [managed identities](../managed-identities-azure-resources/overview).

## Template deployment

Organizations can deploy this policy by following the steps outlined below or by using the [Conditional Access templates](concept-conditional-access-policy-common).

## Create a Conditional Access policy

The following steps help create a Conditional Access policy to require devices accessing resources be marked as compliant with your organization's [Intune compliance policies](/en-us/mem/intune/protect/create-compliance-policy).

Warning

Without a compliance policy created in Microsoft Intune, this Conditional Access policy won't function as intended. Create a compliance policy first and ensure you have at least one compliant device before proceeding.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**
    2. Under **Exclude**:
        1. Select **Users and groups**
            1. Choose your organization's emergency access or break-glass accounts.
            2. If you use hybrid identity solutions like Microsoft Entra Connect or Microsoft Entra Connect Cloud Sync, select **Directory roles**, then select **Directory Synchronization Accounts**
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select **All resources (formerly 'All cloud apps')**.
7. Under **Access controls** &gt; **Grant**.
    1. Select **Require device to be marked as compliant**.
    2. Select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

Note

You can enroll your new devices to Intune even if you select **Require device to be marked as compliant** for **All users** and **All resources (formerly 'All cloud apps')** using the previous steps. The **Require device to be marked as compliant** control doesn't block Intune enrollment.

Similarly, the **Require device to be marked as compliant** doesn't block Microsoft Authenticator app access to the UserAuthenticationMethod.Read scope. Authenticator needs access to the UserAuthenticationMethod.Read scope during Authenticator registration to determine which credentials a user can configure. Authenticator needs access to UserAuthenticationMethod.ReadWrite to register credentials, which doesn't bypass the **Require device to be marked as compliant** check.

### Known behavior

On iOS, Android, macOS, and some non-Microsoft web browsers, Microsoft Entra ID identifies the device using a client certificate that is provisioned when the device is registered with Microsoft Entra ID. When a user first signs in through the browser the user is prompted to select the certificate. The end user must select this certificate before they can continue to use the browser.

### B2B scenarios

For organizations you have a relationship with and trust, you might trust their device compliance claims. To configure this setting, see the article [Manage cross-tenant access settings for B2B collaboration](../../external-id/cross-tenant-access-settings-b2b-collaboration#to-change-inbound-trust-settings-for-mfa-and-device-claims).

### Subscription activation

Organizations that use the [Subscription Activation](/en-us/windows/deployment/windows-10-subscription-activation) feature to enable users to "step-up" from one version of Windows to another, might want to exclude the Windows Store for Business, AppID 45a330b1-b1ec-4cc1-9161-9f03992aa49f from their device compliance policy.