---
layout: Conceptual
title: External Tenant Quickstart - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/quickstart-tenant-setup
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: In this quickstart, learn how to create an external tenant for customer identity and access management (CIAM). Customize a sign-in experience and try it out with a sample app.
ms.topic: quickstart
ms.date: 2025-04-08T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024
locale: en-us
document_id: 91b93213-dce1-7c6e-1611-36fd9708cf1f
document_version_independent_id: 8491a338-9cd7-1e40-7289-fe40eb3e0552
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/quickstart-tenant-setup.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/quickstart-tenant-setup
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/quickstart-tenant-setup.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 0def326f-c3a4-14b2-5b16-4ad2482db279
---

# External Tenant Quickstart - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra External ID offers a customer identity access management (CIAM) solution that lets you create secure, customized sign-in experiences for your apps and services. You'll need to create a tenant with external configurations in the Microsoft Entra admin center to get started. Once the tenant with external configurations is created, you can access it in both the Microsoft Entra admin center and the Azure portal.

In this quickstart, you'll learn how to create a tenant with external configurations if you already have an Azure subscription.

## Prerequisites

- An Azure subscription.
- An Azure account that's been assigned at least the [Tenant Creator](/en-us/entra/identity/role-based-access-control/permissions-reference#tenant-creator) role scoped to the subscription.

## Create a new tenant with external configurations

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Manage tenants**.
3. Select **Create**.

    ![Screenshot of the create tenant option.](media/how-to-create-external-tenant-portal/create-tenant.png)
4. Select **External**, and then select **Continue**.

    ![Screenshot of the select tenant type screen.](media/how-to-create-external-tenant-portal/select-tenant-type.png)
5. On the **Basics** tab, in the **Create a tenant** page, enter the following information:

    ![Screenshot of the Basics tab.](media/how-to-create-external-tenant-portal/add-basics-to-external-tenant.png)

    - Type your desired **Tenant Name** (for example *Contoso Customers*).
    - Type your desired **Domain Name** (for example *Contosocustomers*).
    - Select your desired **Location**. This selection can't be changed later.
6. Select **Next: Add a subscription**.
7. On the **Add a subscription** tab, enter the following information:

    - Next to **Subscription**, select your subscription from the menu.
    - Next to **Resource group**, select a resource group from the menu. If there are no available resource groups, select **Create new**, add a name, and then select **OK**.
    - If **Resource group location** appears, select the geographic location of the resource group from the menu.

    ![Screenshot that shows the subscription settings.](media/how-to-create-external-tenant-portal/add-subscription.png)
8. Select **Next: Review + create**. If the information that you entered is correct, select **Create**. The tenant creation process can take up to 30 minutes. You can monitor the progress of the tenant creation process in the **Notifications** pane. Once the tenant is created, you can access it in both the Microsoft Entra admin center and the Azure portal.

    ![Screenshot that shows the link to the new tenant.](media/how-to-create-external-tenant-portal/tenant-successfully-created.png)

## Customize your tenant with a guide

Our guide will walk you through the process of setting up a user and configuring a sample app in just a few minutes. This means that you can quickly and easily test out different sign-in and sign-up options and set up a sample app to see what works best for you. This guide is available in any external tenant.

Note

The guide won’t run automatically in external tenants that you created with the steps above. If you want to run the guide, follow the steps below.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Home** &gt; **Tenant overview**.
4. On the Get started tab, select **Start the guide**.

    ![Screenshot that shows how to start the guide.](media/how-to-create-external-tenant-portal/guide-link.png)

This link will take you to the [guide](quickstart-get-started-guide), where you can customize your tenant in three easy steps.

Note

You can also set up and customize your external tenant directly within Visual Studio Code using the [Microsoft Entra External ID extension for Visual Studio Code](https://aka.ms/ciamvscode/quickstarts/marketplace). For more information, see our [quickstart guide](https://aka.ms/ciamvscode/quickstartguide).