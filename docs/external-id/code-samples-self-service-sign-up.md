---
layout: Conceptual
title: API connector code samples for user flows - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/code-samples-self-service-sign-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Code samples for API connectors in self-service sign-up flows for Microsoft Entra External ID.
ms.topic: sample
ms.date: 2025-04-14T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
locale: en-us
document_id: 4eb6a3cc-d46c-b4ad-41a5-1b347f6d21be
document_version_independent_id: 83191b2a-86f4-6e9e-965f-1f9a6781f568
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/code-samples-self-service-sign-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/code-samples-self-service-sign-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/code-samples-self-service-sign-up.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: fda17448-52f2-2425-1bad-99469db5ab0f
---

# API connector code samples for user flows - Microsoft Entra External ID | Microsoft Learn

The following tables provide links to code samples for applying web APIs in your self-service sign-up user flows using [API connectors](api-connectors-overview).

## API connector Azure Function quickstarts

| Sample | Description |
| --- | --- |
| [.NET Core](https://github.com/Azure-Samples/active-directory-dotnet-external-identities-api-connector-azure-function-validate) | This .NET Core Azure Function sample demonstrates how to limit sign-ups to specific tenant domains and validate user-provided information. |
| [Node.js](https://github.com/Azure-Samples/active-directory-nodejs-external-identities-api-connector-azure-function-validate) | This Node.js Azure Function sample demonstrates how to limit sign-ups to specific tenant domains and validate user-provided information. |
| [Python](https://github.com/Azure-Samples/active-directory-python-external-identities-api-connector-azure-function-validate) | This Python Azure Function sample demonstrates how to limit sign-ups to specific tenant domains and validate user-provided information. |

## Custom approval workflows

| Sample | Description |
| --- | --- |
| [Manual approval workflow](https://github.com/Azure-Samples/active-directory-dotnet-external-identities-api-connectors-approvals) | This sample demonstrates an end-to-end approval workflow to manage guest user account creation in self-service sign-up |

## Identity verification

| Sample | Description |
| --- | --- |
| [IDology](https://github.com/Azure-Samples/active-directory-dotnet-external-identities-idology-identity-verification) | This sample shows how to verify a user identity as part of your self-service sign-up by using an API connector to integrate with IDology. |
| [Experian](https://github.com/Azure-Samples/active-directory-dotnet-external-identities-experian-identity-verification) | This sample shows how to verify a user identity as part of your self-service sign-up by using an API connector to integrate with Experian. |