---
layout: Conceptual
title: Quickstart - Access and create new tenant - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/create-new-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Instructions about how to find Microsoft Entra ID and how to create a new tenant for your organization.
ms.topic: quickstart
ms.date: 2026-07-29T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: it-pro, fasttrack-edit, mode-other, sfi-image-nochange, msecd-doc-authoring-1018
ms.collection: M365-identity-device-management
locale: en-us
document_id: 4fb61215-dbe7-bd17-91c1-c1af722b65cc
document_version_independent_id: 40da65bb-b522-4b6f-8954-bb2b8ad17706
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/create-new-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/create-new-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/create-new-tenant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: db5c43ef-0556-c565-1aa3-2fb7547613b1
---

# Quickstart - Access and create new tenant - Microsoft Entra | Microsoft Learn

## Overview

You can perform all of your administrative tasks using the Microsoft Entra admin center, including creating a new tenant for your organization.

In this quickstart article, you learn how to create a basic tenant for your organization.

Note

Only paid customers can create a new Workforce tenant in Microsoft Entra ID. Customers using a free tenant, or a trial subscription won't be able to create additional tenants from the Microsoft Entra admin center. Customers facing this scenario who need a new tenant can sign up for a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create a new tenant for your organization

After you sign in to the [Azure portal](https://portal.azure.com), you can create a new tenant for your organization. Your new tenant represents your organization and helps you to manage a specific instance of Microsoft Cloud services for your internal and external users.

Note

- If you're unable to create a Microsoft Entra ID or Azure AD B2C tenant, review your user settings page to ensure that tenant creation isn't switched off. If it isn't enabled you must be assigned at least the [Tenant Creator](../identity/role-based-access-control/permissions-reference#tenant-creator) role.
- This article doesn't cover creating an *external* tenant configuration for consumer-facing apps; learn more about using [Microsoft Entra External ID](../external-id/customers/overview-customers-ciam) for your customer identity and access management (CIAM) scenarios.
- If you're unable to create a Governed Workforce tenant, verify that you have either an [Enterprise Agreement (EA)](/en-us/azure/cost-management-billing/manage/understand-ea-roles) or [Pay-As-You-Go](https://azure.microsoft.com/pricing/offers/ms-azr-0003p?cid=msft_learn) subscription. Both [Microsoft Online Subscription Agreement (MOSA)](/en-us/azure/cost-management-billing/manage/view-all-accounts#microsoft-online-services-program) and [Microsoft Customer Agreement (MCA)](/en-us/azure/cost-management-billing/manage/view-all-accounts#microsoft-customer-agreement) billing accounts are supported. You also need the required Azure Resource Manager (ARM) permissions for the selected subscription through the Tenant Contributor or Subscription Owner/Creator role. To identify your billing account type, see [View your billing accounts in the Azure portal](/en-us/azure/cost-management-billing/manage/view-all-accounts).

### To create a new tenant

# [Workforce / B2C](#tab/workforce)
1. Sign in to the [Azure portal](https://portal.azure.com).
2. From the Azure portal menu, select **Microsoft Entra ID**.
3. Navigate to **Entra ID** &gt; **Overview** &gt; **Manage tenants**.
4. Select **Create**.

    ![Screenshot of Microsoft Entra ID - Overview page - Create a tenant.](media/create-new-tenant/portal.png)
5. On the Basics tab, select the type of tenant you want to create, either **Microsoft Entra ID** or **Microsoft Entra ID (B2C)**.

    Choose **Microsoft Entra ID** to create a workforce tenant for your organization's users and resources. Choose **Microsoft Entra ID (B2C)** only if you need an Azure AD B2C tenant. If **Microsoft Entra ID** is unavailable, review the prerequisites in the previous note, including paid customer requirements, tenant creation settings, and the Tenant Creator role.
6. Select **Next: Configuration** to move to the Configuration tab.
7. On the Configuration tab, enter the following information:

    ![Screenshot of Microsoft Entra ID - Create a tenant page - configuration tab.](media/create-new-tenant/create-new-tenant.png)

    - Type your desired Organization name (for example *Contoso Organization*) into the **Organization name** box.
    - Type your desired Initial domain name (for example *Contosoorg*) into the **Initial domain name** box.
    - Select your desired Country/Region or leave the *United States* option in the **Country or region** box.
8. Select **Next: Review + Create**. Review the information you entered and if the information is correct, select **Create** in the lower left corner.

Your new tenant is created with the domain contoso.onmicrosoft.com.

# [Secure add-on tenant creation](#tab/governed-workforce)
Use the secure add-on tenant creation flow to create a new Governed Workforce tenant. This process creates the tenant and automatically establishes a [governance relationship](../id-governance/tenant-governance/governance-relationships) with your home tenant.

### Define the default governance policy template

In order to automatically establish governance relationships with add-on tenants, you first need to define the default governance policy template.

1. Sign in to the governing tenant as an administrator.
2. Navigate to Templates.
3. Select the default policy template and configure the following options as needed:

    - **Delegated administration**: Select one or more Microsoft Entra built-in roles and assign them to a role assignable security group in the governing tenant. Members of this group can use their governing tenant credentials to sign in to the governed tenant without needing an account in the governed tenant. Each group can have multiple role assignments, and each policy template can have multiple groups defined.
    - **Multitenant application management**: Select a custom, multitenant application. The governed tenant creates a service principal with the same permissions when you establish the relationship.

### Create the tenant

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Manage tenants**.
3. Select **Create**.
4. On the Basics tab, select **Governed Workforce** to access the secure add-on tenant creation feature.
5. Select **Next: Configuration** to move to the Configuration tab.
6. On the Configuration tab, enter the following information:

    - Type your desired Organization name (for example *Contoso Organization*) into the **Organization name** box.
    - Type your desired Initial domain name (for example *Contosoorg*) into the **Initial domain name** box.
    - Select your desired Country/Region or leave the *United States* option in the **Country or region** box.
    - Select your desired cloud subscription and resource group for storing the Microsoft Entra ID Free billing asset for your new tenant.

    Note

    Use either an [Enterprise Agreement (EA)](/en-us/azure/cost-management-billing/manage/understand-ea-roles) or [Pay-As-You-Go](https://azure.microsoft.com/pricing/offers/ms-azr-0003p?cid=msft_learn) subscription. Both [Microsoft Online Subscription Agreement (MOSA)](/en-us/azure/cost-management-billing/manage/view-all-accounts#microsoft-online-services-program) and [Microsoft Customer Agreement (MCA)](/en-us/azure/cost-management-billing/manage/view-all-accounts#microsoft-customer-agreement) billing accounts are supported. You also need the required Azure Resource Manager (ARM) permissions for the selected subscription through the Tenant Contributor or Subscription Owner/Creator role. To identify your billing account type, see [View your billing accounts in the Azure portal](/en-us/azure/cost-management-billing/manage/view-all-accounts).
7. Select **Next: Review + Create**. Review the information you entered and if the information is correct, select **Create** in the lower left corner.

Your new tenant is created with the domain contoso.onmicrosoft.com. If you defined a governance policy template, a tenant governance relationship is automatically formed between your home tenant and your newly created tenant. Your billing account now shows a Microsoft Entra ID Free billing asset linked to your newly created tenant under the selected subscription and resource group.

To learn more about governance relationships and policy templates, see [Governance relationships](../id-governance/tenant-governance/governance-relationships) and [Governance policy templates](../id-governance/tenant-governance/governance-policy-templates).

---

## Your user account in the new tenant

By default, the user who creates a Microsoft Entra tenant is automatically assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role.

By default, you're also listed as the [technical contact](/en-us/microsoft-365/admin/manage/change-address-contact-and-more#what-do-these-fields-mean) for the tenant. Technical contact information is something you can change in [**Properties**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Properties).

Microsoft recommends that organizations have two cloud-only emergency access accounts permanently assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. These accounts are highly privileged and aren't assigned to specific individuals. The accounts are limited to emergency or "break glass" scenarios where normal accounts can't be used or all other administrators are accidentally locked out. These accounts should be created following the [emergency access account recommendations](/en-us/entra/identity/role-based-access-control/security-emergency-access).

## Clean up resources

If you're not going to continue to use this tenant, you can delete the tenant using the following steps:

- Ensure that you're signed in to the directory that you want to delete through the **Directory + subscription** filter in the Azure portal. Switch to the target directory if needed.
- Select **Microsoft Entra ID**, and then on the **Contoso - Overview** page, select **Delete directory**.

    The tenant and its associated information are deleted.

    ![Screenshot of Overview page, with highlighted Delete directory button.](media/create-new-tenant/delete-new-tenant.png)