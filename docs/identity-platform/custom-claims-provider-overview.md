---
layout: Conceptual
title: Custom claims provider overview - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-claims-provider-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Conceptual article describing the custom claims provider as part of the custom authentication extension framework.
manager: pmwongera
ms.custom: 
ms.date: 2025-09-16T00:00:00.0000000Z
ms.reviewer: jasuri
ms.topic: concept-article
locale: en-us
document_id: 3ad29896-92bf-88dc-6d3e-77cb8ae930f1
document_version_independent_id: 32146ffc-fcbe-1e66-434d-d24bf8427b9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-claims-provider-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-claims-provider-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-claims-provider-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: d0975b3e-72a1-8e78-548a-e4249b0575a3
---

# Custom claims provider overview - Microsoft identity platform | Microsoft Learn

This article provides an overview to the Microsoft Entra custom claims provider.

When a user authenticates to an application, a custom claims provider can be used to add claims into the token. A custom claims provider is made up of a custom authentication extension that calls an external REST API, to fetch claims from external systems. A custom claims provider can be assigned to one or many applications in your directory.

Key data about a user is often stored in systems external to Microsoft Entra ID. For example, secondary email, billing tier, or sensitive information. Some applications may rely on these attributes for the application to function as designed. For example, the application may block access to certain features based on a claim in the token.

The following video provides an excellent overview of the Microsoft Entra custom authentication extensions and custom claims providers:

Use a custom claims provider for the following scenarios:

- **Migration of legacy systems** - You may have legacy identity systems such as Active Directory Federation Services (AD FS) or data stores (such as LDAP directory) that hold information about users. You'd like to migrate these applications, but can't fully migrate the identity data into Microsoft Entra ID. Your apps may depend on certain information on the token, and can't be rearchitected.
- **Integration with other data stores that can't be synced to the directory** - You may have third-party systems, or your own systems that store user data. Ideally this information could be consolidated, either through [synchronization](../identity/hybrid/cloud-sync/what-is-cloud-sync) or direct migration, in the Microsoft Entra directory. However, that isn't always feasible. The restriction may be because of data residency, regulations, or other requirements.

Note

A custom claims provider isn't the only way to add custom claims to a token. You can also [customize claims issued in the JSON web token (JWT) for enterprise applications](jwt-claims-customization).

## Token issuance start event listener

An event listener is a procedure that waits for an event to occur. The custom authentication extension uses the **token issuance start** event listener. The event is triggered when a token is about to be issued to your application. When the event is triggered the custom authentication extension REST API is called to fetch attributes from external systems.

To set up a custom claims provider, you'll need to [create a REST API with a token issuance start event](custom-extension-tokenissuancestart-setup), then [configure a custom claim provider for a token issuance event](custom-extension-tokenissuancestart-configuration).

## Authentication events trigger for Azure Functions client library for .NET

The authentication events trigger for Azure Functions allows you to implement a custom extension to handle Microsoft Entra ID authentication events. The authentication events trigger handles all the backend processing for incoming HTTP requests for authentication events.

- Token validation for securing the API call
- Object model, typing and IDE intellisense
- Inbound and outbound validation of the API request and response schemas