---
layout: Conceptual
title: Create a Microsoft Entra tenant - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-create-new-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how to create a Microsoft Entra tenant for use in developing applications that use the Microsoft identity platform for authentication and authorization.
manager: pmwongera
ms.custom: 
ms.date: 2025-04-16T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: how-to
locale: en-us
document_id: 14ab965b-dc45-f450-1302-5ffe491ca129
document_version_independent_id: 0d96d50d-a349-3408-3b93-d8b084e1cbd1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/quickstart-create-new-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/quickstart-create-new-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/quickstart-create-new-tenant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f8e7af5d-f6c5-2e39-e688-fb28d450707a
---

# Create a Microsoft Entra tenant - Microsoft identity platform | Microsoft Learn

To build apps that use the Microsoft identity platform for identity and access management, you need access to a Microsoft Entra *tenant*. It's in the Microsoft Entra tenant that you register and manage your apps, configure their access to data in Microsoft 365 and other web APIs, and enable features like Conditional Access.

A tenant represents an organization. It's a dedicated instance of Microsoft Entra ID that an organization or app developer receives at the beginning of a relationship with Microsoft. That relationship could start with signing up for Azure, Microsoft Intune, or Microsoft 365, for example.

Each Microsoft Entra tenant is distinct and separate from other Microsoft Entra tenants. It has its own representation of work and school identities, consumer identities (if it's an Azure AD B2C tenant), and app registrations. An app registration inside your tenant can allow authentications only from accounts within your tenant or all tenants.

## Prerequisites

An Azure account that has an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Determining the type of users you'll create apps for

You can create a tenant with two different configurations: workforce or customer. The environment depends solely on the types of users your app will authenticate.

This quickstart addresses two scenarios for the type of app you want to build:

- Workforce-facing apps and services for work and school accounts (Microsoft Entra ID) or Microsoft accounts (such as Outlook.com and Live.com)
- Customer-facing apps and services for social and local accounts

## Work and school accounts, or personal Microsoft accounts

To build an environment for either work and school accounts or personal Microsoft accounts (MSA), you can use an existing Microsoft Entra tenant or create a new one. 

### Use an existing Microsoft Entra tenant

Many developers already have tenants through services or subscriptions that are tied to Microsoft Entra tenants, such as Microsoft 365 or Azure subscriptions.

To check the tenant:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Tenant Creator](../identity/role-based-access-control/permissions-reference#tenant-creator).
2. Check the upper-right corner. If you have a tenant, you'll automatically be signed in. You see the tenant name directly under your account name.
    - Hover over your account name to see your name, email address, directory or tenant ID (a GUID), and domain.
    - If your account is associated with multiple tenants, you can select your account name to open a menu where you can switch between tenants. Each tenant has its own tenant ID.

Tip

To find the tenant ID, you can:

- Hover over your account name to get the directory or tenant ID.
- Browse to **Entra ID** &gt; **Overview** &gt; **Properties** and look for **Tenant ID**.

If you don't have a tenant associated with your account, you'll see a GUID under your account name. You won't be able to do actions like registering apps until you create a Microsoft Entra tenant.

### Create a new Microsoft Entra tenant

If you don't already have a Microsoft Entra tenant or if you want to create a new one for development, see [Create a new tenant in Microsoft Entra ID](../fundamentals/create-new-tenant). If you want to create a tenant for app testing, see [build a test environment](test-setup-environment).

You'll provide the following information to create your new tenant:

- **Tenant type** - Choose between a Microsoft Entra tenant and an Azure AD B2C tenant
- **Organization name**
- **Initial domain** - Initial domain `<domainname>.onmicrosoft.com` can't be edited or deleted. You can add a customized domain name later.
- **Country or region**

Note

When naming your tenant, use alphanumeric characters. Special characters aren't allowed. The name must not exceed 256 characters.

## Social and local accounts

To begin building external facing applications that sign in social and local accounts, create a tenant with external configurations. To begin, see [Create a tenant with external configuration](../external-id/customers/quickstart-tenant-setup).