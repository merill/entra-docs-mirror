---
layout: Conceptual
title: Quickstart guide to analyze a failed sign-in attempt - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/quickstart-analyze-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: In this quickstart, you learn how you can use the sign-in log to determine the reason for a failed sign-in to Microsoft Entra ID.
ms.topic: quickstart
ms.date: 2025-02-25T00:00:00.0000000Z
ms.reviewer: besiler
locale: en-us
document_id: 49627aaa-3aae-edb5-ab40-7ed4299124bd
document_version_independent_id: 98887c1f-7d21-36af-d5c3-afc65f52a9a4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/quickstart-analyze-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/quickstart-analyze-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/quickstart-analyze-sign-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: c4710b3a-5886-a23b-d450-80123dc9c1d1
---

# Quickstart guide to analyze a failed sign-in attempt - Microsoft Entra ID | Microsoft Learn

With the information in the Microsoft Entra sign-in log, you can figure out what happened if a sign-in of a user failed. This quickstart shows how to you can locate failed sign-in using the sign-in log.

## Prerequisites

To complete the scenario in this quickstart, you need:

- An Azure subscription. If you don't have one, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant with a [Premium P1 license](../../fundamentals/get-started-premium).
- A user with the **Reports Reader**, **Security Reader**, or **Security Administrator** role for the tenant.
- **A test account called Isabella Simonsen** - If you don't know how to create a test account, see [Add cloud-based users](../../fundamentals/how-to-create-delete-users).

## Perform a failed sign-in

The goal of this step is to create a record of a failed sign-in in the Microsoft Entra sign-in log.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as Isabella Simonsen using an incorrect password.
2. Wait for 5 minutes to ensure that you can find the event in the sign-in log.

## Find the failed sign-in

This section provides you with the steps to analyze a failed sign-in. Filter the sign-in log to remove all records that aren't relevant to your analysis. For example, set a filter to display only the records of a specific user. Then you can review the error details. The log details provide helpful information. You can also look up the error using the [sign-in error lookup tool](https://login.microsoftonline.com/error). This tool might provide you with information to troubleshoot a sign-in error.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Adjust the filter to view only the records for Isabella Simonsen:

    1. Open the **Add filters**, select **User**, and then select **Apply**.

        ![Add user filter](media/quickstart-analyze-sign-in/add-filters.png)
    2. In the **User** textbox, type **Isabella Simonsen**, and then select **Apply**.
4. Select the failed sign-in attempt and view the details.
5. Copy the **Sign-in error code**.

    ![Sign-in error code](media/quickstart-analyze-sign-in/sign-in-error-code.png)
6. Paste the error code into the textbox of the [sign-in error lookup tool](https://login.microsoftonline.com/error), and then select **Submit**.

Review the outcome of the tool and determine whether it provides you with additional information.

## More tests

Now, that you know how to find an entry in the sign-in log by name, you should also try to find the record using the following filters:

- **Date** - Try to find Isabella using a **Start** and an **End**.

    ![Date filter](media/quickstart-analyze-sign-in/start-and-end-filter.png)
- **Status** - Try to find Isabella using **Status: Failure**.

    ![Status failure](media/quickstart-analyze-sign-in/status-failure.png)

## Clean up resources

When no longer needed, delete the test user. If you don't know how to delete a Microsoft Entra user, see [Delete users from Microsoft Entra ID](../../fundamentals/how-to-create-delete-users).