---
layout: Conceptual
title: Block workload identity federation using Azure Policy - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identity-federation-block-using-azure-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Learn how to use a built-in Azure Policy to block workload identity federation on user-assigned managed identities. Govern the use of federated identity credentials on managed identities so that no one can access Microsoft Entra protected resources from external workloads.
ms.topic: how-to
ms.date: 2023-03-09T00:00:00.0000000Z
ms.custom: aaddev
ms.reviewer: cbrooks, udayh, vakarand
locale: en-us
document_id: f68f8755-ccf8-bf3d-0390-2fe083aeaedf
document_version_independent_id: 4150a1af-003b-1d07-7c63-bceb7b6ef4e4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identity-federation-block-using-azure-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identity-federation-block-using-azure-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identity-federation-block-using-azure-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: dea33688-90d7-8225-1bc4-6cde70873538
---

# Block workload identity federation using Azure Policy - Microsoft Entra Workload ID | Microsoft Learn

This article describes how to block the creation of federated identity credentials on user-assigned managed identities by using Azure Policy. By blocking the creation of federated identity credentials, you can block everyone from using [workload identity federation](workload-identity-federation) to access Microsoft Entra protected resources. [Azure Policy](/en-us/azure/governance/policy/overview) helps enforce certain business rules on your Azure resources and assess compliance of those resources.

The Not allowed resource types built-in policy can be used to block the creation of federated identity credentials on user-assigned managed identities.

## Create a policy assignment

To create a policy assignment for the Not allowed resource types that blocks the creation of federated identity credentials in a subscription or resource group:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Navigate to **Policy** in the Azure portal.
3. Go to the **Definitions** pane.
4. In the **Search** box, search for "Not allowed resource types" and select the *Not allowed resource types* policy in the list of returned items. ![Screenshot showing search results in the Azure Policy Definitions pane.](media/workload-identity-federation-block-using-azure-policy/azure-policy-search.png)
5. After selecting the policy, you can now see the **Definition** tab.
6. Click the **Assign** button to create an Assignment. ![Screenshot showing Policy Definition pane.](media/workload-identity-federation-block-using-azure-policy/azure-policy-assign.png)
7. In the **Basics** tab, fill out **Scope** by setting the **Subscription** and optionally set the **Resource Group**.
8. In the **Parameters** tab, select **userAssignedIdentities/federatedIdentityCredentials** from the **Not allowed resource types** list. Select **Review and create**. ![Screenshot showing Parameters tab.](media/workload-identity-federation-block-using-azure-policy/azure-policy-assign-parameters.png)
9. Apply the Assignment by selecting **Create**.
10. View your assignment in the **Assignments** tab next to **Definition**.