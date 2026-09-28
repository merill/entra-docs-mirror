---
layout: Conceptual
title: Client libraries for managed identity authentication - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/reference-managed-identity-libraries
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: dougeby
description: Get to know the client libraries that you can use to authenticate your apps using managed identities for Azure resources.
ms.topic: reference
ms.date: 2024-11-11T00:00:00.0000000Z
locale: en-us
document_id: 82664149-a942-8048-d78c-5696a033a269
document_version_independent_id: 82664149-a942-8048-d78c-5696a033a269
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/reference-managed-identity-libraries.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/reference-managed-identity-libraries
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/reference-managed-identity-libraries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: dca4bef7-bce6-594c-edce-7aa6a1f650e2
---

# Client libraries for managed identity authentication - Managed identities for Azure resources | Microsoft Learn

This document provides an overview of the client libraries available for authenticating your applications using managed identities for Azure resources. These libraries include the Azure Identity libraries and Microsoft Authentication Libraries (MSAL).

Some Azure services built client libraries on top of these libraries. For example, the `Microsoft.Data.SqlClient` package can be used to authenticate to an Azure SQL database using managed identities. Behind the scenes, the Azure Identity library for .NET is being used.

## Choosing the right library

MSAL libraries offer lower-level abstractions than libraries like Azure Identity. Both MSAL and Azure Identity libraries allow you to acquire tokens via managed identity. Internally, Azure Identity libraries use MSAL and provide higher-level APIs such as `DefaultAzureCredential` that remove the need to implement manual switches between identity types when developing and deploying your application.

- If your application already uses one of the libraries, continue using the same library.
- If you're developing a new application and plan to call other Azure resources, use an Azure Identity library. This library provides an improved developer experience by allowing the app to authenticate on local developer machines where managed identities are not available.
- If you need to call other downstream web APIs like Microsoft Graph or your own web API, use MSAL. For .NET applications, use the *Microsoft.Identity.Web* library, which is built on top of MSAL.

In cases where an Azure service built a client library on top of these libraries, consider using the service-specific client library. For example, for Azure SQL, use the [`Microsoft.Data.SqlClient`](/en-us/sql/connect/ado-net/sql/azure-active-directory-authentication#using-managed-identity-authentication) package.

## Language-specific API references

| Language | Azure Identity | MSAL |
| --- | --- | --- |
| .NET | [Azure Identity client library for .NET](/en-us/dotnet/api/overview/azure/identity-readme#managed-identity-support) | [MSAL .NET](/en-us/dotnet/api/microsoft.identity.client.managedidentityapplication) |
| C++ | [Azure Identity client library for C++](https://azure.github.io/azure-sdk-for-cpp/identity.html) |  |
| Java | [Azure Identity client library for Java](/en-us/java/api/overview/azure/identity-readme#managed-identity-support) | [MSAL Java](/en-us/java/api/com.microsoft.aad.msal4j.managedidentityapplication) |
| JavaScript | [Azure Identity client library for JavaScript](/en-us/javascript/api/overview/azure/identity-readme#managed-identity-support) | [MSAL JavaScript](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/managed-identity.md) |
| Python | [Azure Identity client library for Python](/en-us/python/api/overview/azure/identity-readme#managed-identity-support) | [MSAL Python](/en-us/python/api/msal/msal.managed_identity) |
| Go | [Azure Identity client library for Go](https://pkg.go.dev/github.com/Azure/azure-sdk-for-go/sdk/azidentity) | [MSAL Go](https://pkg.go.dev/github.com/AzureAD/microsoft-authentication-library-for-go) |