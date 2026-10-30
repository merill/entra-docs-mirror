---
layout: Conceptual
title: Analyze a sign-in with the Microsoft Graph API - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/quickstart-access-log-with-graph-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to access the sign-in log and analyze a single sign-in attempt using the Microsoft Graph API.
ms.topic: quickstart
ms.date: 2024-11-13T00:00:00.0000000Z
ms.reviewer: besiler
ms.custom: sfi-image-nochange
locale: en-us
document_id: 25fde9b1-ab81-50a8-aba7-74ed025aa4ab
document_version_independent_id: a8288b89-c88e-f89a-5df7-cb24bc57f468
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/quickstart-access-log-with-graph-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/quickstart-access-log-with-graph-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/quickstart-access-log-with-graph-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: d2d55d5d-bbd8-2330-3530-70a00b5af27d
---

# Analyze a sign-in with the Microsoft Graph API - Microsoft Entra ID | Microsoft Learn

In this Quickstart, you'll use the information in the Microsoft Entra sign-in logs to figure out what happened if a sign-in of a user failed. This quickstart shows you how to access the sign-in log using the Microsoft Graph API.

## Prerequisites

To complete the scenario in this quickstart, you need:

- **Access to a Microsoft Entra tenant**: If you don't have access to a Microsoft Entra tenant, see [Create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- **A test account called Isabella Simonsen**: If you don't know how to create a test account, see [Add cloud-based users](../../fundamentals/how-to-create-delete-users).
- **Access to the Microsoft Graph API**: If you don't have access yet, see [Microsoft Graph authentication and authorization basics](/en-us/graph/auth/auth-concepts).

## Perform a failed sign-in

The goal of this step is to create a record of a failed sign-in in the Microsoft Entra sign-in log.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as Isabella Simonsen using an incorrect password.
2. Wait for 5 minutes to ensure that you can find a record of the sign-in entry in the logs.

## Find the failed sign-in

This section provides the steps to locate the failed sign-in attempt using the Microsoft Graph API.

1. Sign in to [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) as a user with permissions to run a query.
2. Select **Modify permissions** to ensure you have the correct permissions.
3. Select **GET** as the HTTP method from the dropdown.
4. Set the API version to **beta**.
5. Enter the following query and select **Run query**: `https://graph.microsoft.com/beta/auditLogs/signIns?$top=10&$filter=userDisplayName eq 'Isabella Simonsen'`
6. Review the query response and locate the **status** section of the response.

![Screenshot of the query response with the error status section highlighted.](media/quickstart-access-log-with-graph-api/graph-sign-in-error-sample.png)

## Clean up resources

When no longer needed, delete the test user. If you don't know how to delete a Microsoft Entra user, see [Delete users from Microsoft Entra ID](../../fundamentals/how-to-create-delete-users).