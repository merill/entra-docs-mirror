---
layout: Conceptual
title: External ID Pricing - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/external-identities-pricing
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about the pricing and billing structure for Microsoft Entra External ID, along with steps for linking an external tenant to an Azure subscription.
ms.topic: concept-article
ms.date: 2026-06-22T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
locale: en-us
document_id: d48108c5-3850-af59-ed14-84238bca37f7
document_version_independent_id: cca4148e-8754-87a7-42a3-ea368fcb0285
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/external-identities-pricing.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/external-identities-pricing
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/external-identities-pricing.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1ca9184c-2ee4-07bc-75e4-325bc8fb8104
---

# External ID Pricing - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article outlines the pricing and billing structure for Microsoft Entra External ID. External ID uses a basic monthly active users (MAU) billing model with optional premium add-ons for advanced scenarios. It also describes how to link your tenant to an Azure subscription to ensure correct billing and feature access.

For the latest pricing details, see [External ID pricing](https://aka.ms/ExternalIDPricing).

## External ID billing model

The basic External ID billing model is based on monthly active users (MAU), which is the count of unique external users who authenticate to your tenants within a calendar month. To determine the total number of MAUs, we combine MAUs from all workforce and external tenants that are linked to a subscription.

MAU billing helps reduce your costs by offering a free tier and flexible, predictable pricing. You can get started for free and pay for only what you use as your business grows.

The MAU billing model for External ID applies to all guest users. Guest users include:

- External guests for B2B collaboration in Microsoft Entra [workforce tenants](tenant-configurations#workforce-tenants). These users sign in with *external* credentials. Their `UserType` property is set to `Guest`.

    Note

    If you own and operate multiple tenants, your member users can authenticate across your tenants without being counted in the MAU total. For B2B collaboration, the MAU billing model applies only to external users who have a `UserType` value of `Guest`. It doesn't apply to users who originate from within the organization and have a `UserType` value of `Member`.
- Internal guests in Microsoft Entra. These users sign in with `internal` credentials. Their `UserType` property is set to `Guest`.
- External users in Microsoft Entra [external tenants](tenant-configurations#external-tenants):

    - Consumers and business guests (users without directory roles)
    - Admins (users with directory roles)

    MAU billing applies to all users in an external tenant regardless of their `UserType` setting.

For more info about the differences between internal and external guests, see [Understand and manage the properties of B2B guest users](user-properties).

## Premium add-ons

In addition to the basic MAU billing, External ID provides premium add-ons that extend functionality for advanced scenarios. Each add-on has its own billing model. The following table summarizes the available add-ons.

| Add-on | Tenant configuration | Billing model | Description |
| --- | --- | --- | --- |
| **M2M Authentication** | External | Transaction-based | Authentication using OAuth 2.0 client credentials flows for machine-to-machine (M2M) authentication scenarios without user interaction. Charges are based on the number of authentication transactions. |
| **SMS Phone Authentication** | Workforce, External | Transaction-based | Additional charges for each SMS-based authentication event (text only; voice isn't supported). For more information, see [Features and licenses for Microsoft Entra multifactor authentication](../identity/authentication/concept-mfa-licensing). |
| **Go-Local** | External | MAU-based | Store external identity data in a specific geographic region to meet data residency requirements. Currently available only in Australia and Japan. |
| **ID Governance** | Workforce | MAU-based | Govern guest users with premium features in Microsoft Entra ID Governance. For more information, see [Microsoft Entra ID Governance licensing for guest users](../id-governance/microsoft-entra-id-governance-licensing-for-guest-users). |
| **GSA for Guests** | Workforce | MAU-based | Global Secure Access (GSA) coverage for guest users in workforce tenants. |

Note

Premium add-on charges are in addition to the basic MAU billing. For the latest information about add-on pricing, see [External ID pricing](https://aka.ms/ExternalIDPricing).

## Billing scenarios

The following examples illustrate how basic MAU billing and premium add-ons work together. Each scenario indicates the tenant configurations it applies to (workforce or external). For more information, see [Tenant configurations](tenant-configurations). These scenarios are conceptual and don't include specific prices. For current pricing, see [External ID pricing](https://aka.ms/ExternalIDPricing).

### Scenario 1: Consumer app with basic sign-in (external tenant)

A consumer-facing app registered in an external tenant has 10,000 users who sign in using email and password or social identity providers. No premium add-ons are enabled.

- **Tenant configuration**: External
- **Applicable add-on SKU**: None
- **Meter type**: MAU
- **MAU count**: 10,000
- **Result**: No cost if MAU usage is within free limits.

### Scenario 2: M2M Authentication (external tenant)

A background service, such as a console app, runs continuously and authenticates with Microsoft Entra External ID using client credentials. The app calls an API on its own behalf without any user interaction and refreshes its access token hourly.

- **Tenant configuration**: External
- **Applicable add-on SKU**: M2M Authentication
- **Meter type**: Transaction (M2M Authentication)
- **MAU count**: 0 (M2M authentication doesn't involve user sign-ins, so no MAU charges apply)
- **Description**: Transaction charges based on the number of client credential authentication requests; for example, one token refresh per hour produces approximately 720 transactions per month.
- **Result**: Only M2M Authentication add-on charges apply. For current transaction pricing, see [External ID pricing](https://aka.ms/ExternalIDPricing).

### Scenario 3: Consumer app with interactive users and M2M calls (external tenant)

A consumer app in an external tenant has 5,000 users who sign in interactively. The app also uses M2M Authentication (client credentials) for background processing tasks, such as syncing data and sending notifications.

- **Tenant configuration**: External
- **Applicable add-on SKU**: M2M Authentication
- **Meter type**: MAU and transaction (M2M Authentication)
- **MAU count**: 5,000 (interactive users only; M2M Authentication calls don't count toward MAU)
- **Description**: Transaction charges based on the number of client credential authentication requests.
- **Result**: Microsoft Entra External ID Basic MAU charges for interactive users, plus M2M Authentication add-on charges for background processing.

### Scenario 4: B2B collaboration with ID Governance (workforce tenant)

An organization invites 2,000 external business partners as B2B collaboration guests in their workforce tenant. The organization uses ID Governance to manage machine learning assisted access reviews for guest users.

- **Tenant configuration**: Workforce
- **Applicable add-on SKU**: ID Governance
- **Meter type**: MAU
- **MAU count**: 2,000
- **Description**: Charges for guests who trigger governance actions during the month, such as machine learning assisted access reviews; for more information, see [Microsoft Entra ID Governance licensing for guest users](../id-governance/microsoft-entra-id-governance-licensing-for-guest-users).
- **Result**: Microsoft Entra External ID Basic MAU charges plus ID Governance add-on charges.

### Scenario 5: Consumer app with data residency (external tenant)

A consumer app in an external tenant has 8,000 users who sign in interactively. The organization enables the Go-Local add-on to store external identity data in a specific geographic region to meet data residency requirements. The Go-Local add-on is currently available only in Australia and Japan.

- **Tenant configuration**: External
- **Applicable add-on SKU**: Go-Local
- **Meter type**: MAU
- **MAU count**: 8,000
- **Description**: MAU-based charges for storing external identity data in the selected region, in addition to the basic MAU charges.
- **Result**: Microsoft Entra External ID Basic MAU charges plus Go-Local add-on charges.

## Subscription requirements

External ID requires an Azure subscription for billing. The following sections describe how to link a workforce or external tenant to a subscription. For pricing details, see [External ID pricing](https://aka.ms/ExternalIDPricing).

Note

If you previously subscribed to B2B collaboration under an Azure AD External Identities P1/P2 SKU, see the [External ID pricing](https://aka.ms/ExternalIDPricing) page for information about current pricing options and any available upgrade paths.

## Link a workforce tenant to a subscription

Microsoft Entra workforce tenants must be linked to an Azure subscription for proper billing and access to features. To link your tenant to a subscription:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/). Use an account that has at least the Contributor role within the subscription or a resource group within the subscription.
2. Select the directory that you want to link:

    1. On the toolbar, select the **Settings** icon.
    2. On the **Directories + subscriptions** pane, find your workforce tenant in the **Directory name** list. Then select **Switch**.
3. Go to **Entra ID** &gt; **External Identities** &gt; **Overview**.
4. Under **Subscriptions**, select **Linked subscriptions**.
5. In the tenant list, select the checkbox next to the tenant, and then select **Link subscription**.

    ![Screenshot of actions for linking a subscription.](media/external-identities-pricing/linked-subscriptions.png)
6. On the **Link a subscription** pane, select a subscription and a resource group. Then select **Apply**. (If no subscriptions are listed, see What if I can't find a subscription? later in this article.)

    ![Screenshot of boxes for selecting a subscription and a resource group.](media/external-identities-pricing/link-subscription-resource.png)

After you complete these steps, your Azure subscription is billed based on your Azure direct or Enterprise Agreement details, if applicable.

### What if I can't find a subscription?

If no subscriptions are available on the **Link a subscription** pane, here are some possible reasons:

- You're trying link a workforce tenant to a subscription, but you're currently signed in to an external tenant. Switch to the workforce tenant:

    1. On the Microsoft Entra admin center toolbar, select **Settings**.
    2. On the **Directories + subscriptions** pane, find your workforce tenant in the list. Then select **Switch**.
- You don't have the appropriate permissions. Be sure to sign in by using an Azure account that has at least the Contributor role within the subscription or a resource group within the subscription.
- A subscription exists, but it isn't associated with your directory yet. You can [associate an existing subscription with your tenant](../fundamentals/how-subscriptions-associated-directory) and then repeat the steps for linking it to your tenant.
- No subscription exists. On the **Link a subscription** pane, you can create a subscription by selecting the link **If you don't already have a subscription you may create one here**.

    After you create a new subscription, you need to [create a resource group](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal) in the new subscription. Then, repeat the steps for linking it to your tenant.

## Link an external tenant to a subscription

Depending on how you created your external tenant, it might already be linked to a subscription. To find out, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Make sure your external tenant is selected:

    1. On the toolbar, select the **Settings** icon.
    2. On the **Directories + subscriptions** pane, find your external tenant in the **Directory name** list. Then select **Switch**.
3. Select **Home** and find the **Billing** section. Then take one of these actions:

    - If your tenant is linked to a subscription, the subscription ID appears in this section. You can select the ID to view subscription details.

        ![Screenshot that shows an example external tenant linked to a subscription.](media/external-identities-pricing/billing-section-subscription.png)
    - If your tenant isn't yet linked to a subscription, in the **Billing** section, select the **Click here to upgrade** link. Then select the **Add Subscription** button.

        ![Screenshot that shows an example external tenant that has no subscriptions.](media/external-identities-pricing/billing-section-no-subscription.png)

## Change the subscription that your external tenant is linked to

You can move an external tenant to another subscription, as long as the subscription that you want to use is in the same Microsoft Entra workforce tenant as the current subscription. Moving to a subscription in a *different* Microsoft Entra workforce tenant isn't currently supported.

To move your external tenant resources to the new subscription, use Azure Resource Manager as described in [Move Azure resources to a new resource group or subscription](/en-us/azure/azure-resource-manager/management/move-resource-group-and-subscription). Before you start, read the article to fully understand the limitations and requirements. The article also contains other critical information, such as a pre-move checklist and steps for validating the move operation.

## Can I change the ownership of a subscription?

You can't change the ownership of a subscription to a Microsoft Entra external tenant. External tenants don't have subscription management capabilities. External tenants must be linked to subscriptions that Microsoft Entra workforce tenants own.