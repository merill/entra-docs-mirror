---
layout: Conceptual
title: Microsoft Entra multifactor authentication providers - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-mfa-authprovider
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: When should you use an authentication provider with Microsoft Entra multifactor authentication (MFA)?
ms.topic: concept-article
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: jpettere
locale: en-us
document_id: 02d89c71-7566-2cd4-6a97-8c54bbdfae88
document_version_independent_id: 0c1251e2-52f5-34d7-4815-169d6bd8d873
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-mfa-authprovider.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-mfa-authprovider
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-mfa-authprovider.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a900ff45-2cb6-d248-422c-b5d4a5e63d5b
---

# Microsoft Entra multifactor authentication providers - Microsoft Entra ID | Microsoft Learn

Important

Effective September 1, 2018 new auth providers may no longer be created. Existing auth providers may continue to be used and updated, but migration is no longer possible. Multifactor authentication continues to be available as a feature in Microsoft Entra ID P1 or P2 licenses.

Two-step verification is available by default for administrators in Microsoft Entra ID, and Microsoft 365 users. However, if you wish to take advantage of [advanced features](howto-mfa-mfasettings) then you should enable Microsoft Entra multifactor authentication by using Conditional Access. For more information, see [Common Conditional Access policy: Require MFA for all users](../conditional-access/howto-conditional-access-policy-all-users-mfa).

A Microsoft Entra multifactor authentication provider is used to take advantage of features provided by Microsoft Entra multifactor authentication for users who **don't have licenses**.

## Caveats related to the Microsoft Entra multifactor authentication SDK

Note the SDK is deprecated and calls to the SDK fail after November 14, 2018

## What is an MFA provider?

There are two types of Auth providers, and the distinction is around how your Azure subscription is charged. The per-authentication option calculates the number of authentications performed against your tenant in a month. This option is best if some accounts authenticate only occasionally. The per-user option calculates the number of accounts that are eligible to perform MFA, which is all accounts in Microsoft Entra ID, and all enabled accounts in MFA Server. This option is best if some users have licenses but you need to extend MFA to more users beyond your licensing limits.

## Manage your MFA provider

You can't change the usage model (per enabled user or per authentication) after an MFA provider is created.

If you purchased enough licenses to cover all users that are enabled for MFA, you can delete the MFA provider altogether.

If your MFA provider isn't linked to a Microsoft Entra tenant, or you link the new MFA provider to a different Microsoft Entra tenant, user settings and configuration options aren't transferred. Also, existing Microsoft Entra multifactor authentication Servers need to be reactivated using activation credentials generated through the MFA Provider.

### Removing an authentication provider

Caution

There's no confirmation when deleting an authentication provider. Selecting **Delete** is a permanent process.

Authentication providers can be found in the [Microsoft Entra admin center](https://entra.microsoft.com). Sign in as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator). Browse to **Entra ID** &gt; **Multifactor authentication** &gt; **Providers**. Click the listed providers to see details and configurations associated with that provider.

Before removing an authentication provider, take note of any customized settings configured in your provider. Decide what settings need to be migrated to general MFA settings from your provider and complete the migration of those settings.

Microsoft Entra multifactor authentication Servers linked to providers need to be reactivated using credentials generated under **Server settings**. Before reactivating, the following files must be deleted from the `\Program Files\Multi-Factor Authentication Server\Data\` directory on Microsoft Entra multifactor authentication Servers in your environment:

- caCert
- cert
- groupCACert
- groupKey
- groupName
- licenseKey
- pkey

![Delete an authentication provider](media/concept-mfa-authprovider/authentication-provider-removal.png)

After you confirm that all settings are migrated, browse to **Providers** and select the ellipses **...** and select **Delete**.

Warning

Deleting an authentication provider deletes any reporting information associated with that provider. You may want to save activity reports before deleting your provider.

Note

Users with older versions of the Microsoft Authenticator app and Microsoft Entra multifactor authentication Server may need to re-register their app.