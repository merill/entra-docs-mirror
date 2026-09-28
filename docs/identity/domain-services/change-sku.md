---
layout: Conceptual
title: Change the SKU for a Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/change-sku
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to the SKU tier for a Microsoft Entra Domain Services managed domain if your business requirements change
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 15b8dc4d-1df4-6e98-5307-517d83c1435a
document_version_independent_id: b4496233-1dfa-a1ea-97ef-15757add0213
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/change-sku.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/change-sku
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/change-sku.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 50e3225b-416c-3ed7-ed72-bc4981413ad0
---

# Change the SKU for a Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

In Microsoft Entra Domain Services, the available performance and features are based on the SKU type. These feature differences include the backup frequency or maximum number of one-way outbound forest trusts.

You select a SKU when you create the managed domain, and you can switch SKUs up or down as your business needs change after the managed domain has been deployed. Changes in business requirements could include the need for more frequent backups or to create additional forest trusts. For more information on the limits and pricing of the different SKUs, see [Domain Services SKU concepts](administration-concepts#azure-ad-ds-skus) and [Domain Services pricing](https://azure.microsoft.com/pricing/details/active-directory-ds/) pages.

This article shows you how to change the SKU for an existing Domain Services managed domain using the [Microsoft Entra admin center](https://entra.microsoft.com).

## Before you begin

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, complete the tutorial to [create and configure a managed domain](tutorial-create-instance).

## SKU change limitations

You can change SKUs up or down after the managed domain has been deployed. However, the *Premium* and *Enterprise* SKUs define a limit on the number of trusts you can create. You can't change to a SKU with a lower maximum limit than you currently have configured.

For example, if you have created seven trusts on the *Premium* SKU, you can't change down to the *Enterprise* SKU. The *Enterprise* SKU supports a maximum of five trusts.

For more information on these limits, see [Domain Services SKU features and limits](administration-concepts#azure-ad-ds-skus).

## Select a new SKU

To change the SKU for a managed domain using the [Microsoft Entra admin center](https://entra.microsoft.com), complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Microsoft Entra Domain Services**. Choose your managed domain from the list, such as *aaddscontoso.com*.
2. In the menu on the left-hand side of the Domain Services page, select **Settings &gt; SKU**.

    ![Select the SKU menu option for your Domain Services managed domain in the Microsoft Entra admin center](media/change-sku/overview-change-sku.png)
3. From the drop-down menu, select the SKU you wish for your managed domain. If you have a resource forest, you can't select *Standard* SKU as forest trusts are only available on the *Enterprise* SKU or higher.

    Choose the SKU you want from the drop-down menu, then select **Save**.

    ![Choose the required SKU from the drop-down menu in the Microsoft Entra admin center](media/change-sku/change-sku-selection.png)

It can take a minute or two to change the SKU type.