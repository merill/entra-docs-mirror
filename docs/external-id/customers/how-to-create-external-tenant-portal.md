---
layout: Conceptual
title: Create an External Tenant - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-create-external-tenant-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Create an external tenant to get started with Microsoft Entra External ID as your customer identity and access management (CIAM) service.
ms.topic: how-to
ms.date: 2025-11-06T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024, sfi-image-nochange
locale: en-us
document_id: 84478bfd-7512-e74e-7052-822dc1b0ef3d
document_version_independent_id: 84478bfd-7512-e74e-7052-822dc1b0ef3d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-create-external-tenant-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-create-external-tenant-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-create-external-tenant-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5cc1296e-8400-7022-dc81-780e057d4ac7
---

# Create an External Tenant - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra External ID offers a customer identity access management (CIAM) solution that lets you create secure, customized sign-in experiences for your apps and services. With these built-in CIAM features, Microsoft Entra External ID can serve as the identity provider and access management service for your customer scenarios. You'll need to create an external tenant in the Microsoft Entra admin center to get started. Once the external tenant is created, you can access it in both the Microsoft Entra admin center and the Azure portal.

In this article, you learn how to:

- Create an external tenant
- Switch to the directory containing your external tenant
- Find your external tenant name and ID in the Microsoft Entra admin center

## Prerequisites

- An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- An Azure account that's been assigned at least the [Tenant Creator](/en-us/entra/identity/role-based-access-control/permissions-reference#tenant-creator) role scoped to the subscription or to a resource group within the subscription.

## Create a new external tenant

1. Sign in to your organization's [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Tenant Creator](/en-us/entra/identity/role-based-access-control/permissions-reference#tenant-creator).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Manage tenants**.
3. Select **Create**.

    ![Screenshot of the create tenant option.](media/how-to-create-external-tenant-portal/create-tenant.png)
4. Select **External**, and then **Continue**.

    ![Screenshot of the select tenant type screen.](media/how-to-create-external-tenant-portal/select-tenant-type.png)
5. If you're creating an external tenant for the first time, you have the option to create a trial tenant that doesn't require an Azure subscription. Otherwise, use the Azure Subscription option to continue to the next step.
6. If you choose the 30-day free trial, an Azure subscription isn't required.
7. If you choose **Use Azure Subscription** option, then the admin center displays the tenant creation page. On the **Basics** tab, in the **Create a tenant for customers** page, enter the following information:

    ![Screenshot of the Basics tab.](media/how-to-create-external-tenant-portal/add-basics-to-external-tenant.png)

    - Type your desired **Tenant Name** (for example *Contoso Customers*).
    - Type your desired **Domain Name** (for example *Contosocustomers*).
8. Select your desired **Country/Region**. This selection can't be changed later.

    If you select a country/region that supports the Go-Local add-on, such as Australia or Japan, a **Go-Local data residency** option appears. You can elect to have your Microsoft Entra ID Core Store data and Microsoft Entra ID components and service data stored in the selected location. For more information, see [Go-Local add-on](../../fundamentals/data-residency#go-local-add-on).

    ![Screenshot of the Basics tab and the Go-Local data residency option.](media/how-to-create-external-tenant-portal/go-local-add-on-option.png)
9. Select **Next: Add a subscription**.
10. On the **Add a subscription** tab, enter the following information:

    - Next to **Subscription**, select your subscription from the menu.
    - Next to **Resource group**, select a resource group from the menu. If there are no available resource groups, select **Create new**, type a **Name**, and then select **OK**.
    - If **Resource group location** appears, select the geographic location of the resource group from the menu.

    ![Screenshot that shows the subscription settings.](media/how-to-create-external-tenant-portal/add-subscription.png)
11. Select **Next: Review + Create**. If the information that you entered is correct, select **Create**. The tenant creation process can take up to 30 minutes. You can monitor the progress of the tenant creation process in the **Notifications** pane. Once the external tenant is created, you can access it in both the Microsoft Entra admin center and the Azure portal.

    ![Screenshot that shows the link to the new external tenant.](media/how-to-create-external-tenant-portal/tenant-successfully-created.png)

Note

You can also use the [Microsoft Entra External ID extension for Visual Studio Code](https://aka.ms/ciamvscode/quickstarts/marketplace) to set up a trial or paid external tenant directly within Visual Studio Code ([learn more](https://aka.ms/ciamvscode/quickstartguide)).

## Get the external tenant details

If you're not sure which directory contains your external tenant, you can find the tenant name and ID both in the Microsoft Entra admin center and in the Azure portal.

1. If you have access to multiple tenants, select the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant from the **Directories + subscriptions** menu.

    ![Screenshot of the Directories + subscriptions icon.](media/how-to-create-external-tenant-portal/directories-subscription.png)
2. On the **Portal settings | Directories + subscriptions** page, find your external tenant in the **Directory name** list, and then select **Switch**. This step brings you to the tenant's home page.
3. Select **Tenant overview** under **Quick navigation**. You can find the tenant **Name**, **Tenant ID** and **Primary domain** under the **Overview** tab.

    ![Screenshot of the tenant details.](media/how-to-create-external-tenant-portal/tenant-overview.png)

You can find the same details if you go to **Microsoft Entra ID** in the Azure portal. On the **Microsoft Entra ID** page, you can find the tenant **Name**, **Tenant ID** and **Primary domain** under **Overview** &gt; **Basic information**.