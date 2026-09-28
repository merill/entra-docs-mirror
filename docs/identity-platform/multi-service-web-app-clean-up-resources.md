---
layout: Conceptual
title: Tutorial - Clean up resources - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/multi-service-web-app-clean-up-resources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this tutorial, you learn how to clean up the Azure resources allocated while creating the web app.
manager: pmwongera
ms.date: 2024-02-17T00:00:00.0000000Z
ms.reviewer: stsoneff
ms.subservice: 
ms.topic: tutorial
ms.custom: sfi-image-nochange
locale: en-us
document_id: 69f325f2-b3c3-e81b-892b-43e0e1076e84
document_version_independent_id: d78bbb67-d91b-523c-54e4-56a2c6602f73
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/multi-service-web-app-clean-up-resources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/multi-service-web-app-clean-up-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/multi-service-web-app-clean-up-resources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 99cfe3cb-15d1-ed1f-b137-eb1c0593995a
---

# Tutorial - Clean up resources - Microsoft identity platform | Microsoft Learn

If you completed all the steps in this multipart tutorial, you created an app service, app service hosting plan, and a storage account in a resource group. You also created an app registration in Microsoft Entra ID. When no longer needed, delete these resources and app registration so that you don't continue to accrue charges.

In this tutorial, you:

- Delete the Azure resources created while following the tutorial.

## Delete the resource group

In the [Azure portal](https://portal.azure.com), select **Resource groups** from the portal menu and select the resource group that contains your app service and app service plan.

Select **Delete resource group** to delete the resource group and all the resources.

![Screenshot that shows deleting the resource group.](media/multi-service-web-app-clean-up-resources/delete-resource-group.png)

This command might take several minutes to run.

## Delete the app registration

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select the application you created.
4. In the app registration overview, select **Delete**.