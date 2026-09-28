---
layout: Conceptual
title: Microsoft Entra External ID deployment guide for customer authentication experience - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/deployment-external-customer-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra-external-id
manager: martinco
description: Learn about implementing self-service flows, native user experience, and more in Microsoft Entra External ID.
ms.topic: concept-article
ms.date: 2025-05-22T00:00:00.0000000Z
ms.reviewer: gasinh
locale: en-us
document_id: cbb7fcc3-409b-d69f-a75c-a0beed71ccbf
document_version_independent_id: cbb7fcc3-409b-d69f-a75c-a0beed71ccbf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/deployment-external-customer-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/deployment-external-customer-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/deployment-external-customer-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 04ffe273-9dd4-58ce-bb55-5b4c89413f00
---

# Microsoft Entra External ID deployment guide for customer authentication experience - Microsoft Entra | Microsoft Learn

Customer interface and seamless application integration are a highly visible aspect of a customer identity management solution. Applications integrate the identity experiences with a browser redirect, or you can integrate the user experience by calling the identity APIs.

There are three **self-service user flows**:

- Web browser redirect-based authentication
- Embedded or native authentication
- Microsoft Graph API experience

## Web browser redirect

A web redirect user experience occurs in a browser window. A defined user flow in Microsoft Entra External ID is processed in a browser so users can authenticate.

When users attempt to authenticate at an application, they're redirected to a Microsoft Entra External ID user flow for authentication, or identity related functions, such as password reset.

After users complete the flow, a token, an authorization code, or an error goes to the application via a browser redirect. The flow appears in the following diagram.

[![Diagram of a browser redirect flow.](media/deployment-external/user-flow-browser-redirect.png)](media/deployment-external/user-flow-browser-redirect-expanded.png#lightbox)

## Native user experience

A native experience enables the user flow user in application UI. Developers can use Microsoft Entra native authentication to host app user interface in the client application, instead of delegating authentication to browsers. This scenario can result in a natively integrated authentication experience. Experience the control over the look and feel of the sign-in and sign-up interfaces.

Use the [native authentication](../external-id/customers/concept-native-authentication) SDK to build native user experiences for iOS and Android mobile applications.

Microsoft implementation of these authentication APIs is based on the draft standard [OAuth 2.0 Direct Interaction Grants](https://drafts.aaronpk.com/oauth-direct-interaction-grant/draft-parecki-oauth-direct-interaction-grant.html). See a flow in the following diagram.

[![Diagram of native authentication.](media/deployment-external/native-authentication.png)](media/deployment-external/native-authentication-expanded.png#lightbox)

The client direct interactions pattern enables the client to manage and render the user interface, offering a native application experience. This approach uses native authentication APIs for authentication tasks.

Native authentication APIs are available for platform native iOS and Android clients and has user interface customization capabilities. Use APIs for sign-up, sign in, password reset, and profile edits. Profile edits are done with user tokens against Microsoft Graph API.

Note

Microsoft has a goal to add support for single-page applications (SPAs).

## Microsoft Graph API experience

Enable Microsoft Graph API to create, read, update, and delete objects in the Microsoft Entra External ID user directory. For user-facing portals, an application token, or a delegated token (application + user) processes data using the Microsoft Graph API.

Learn more about [delegated access](../identity-platform/delegated-access-primer).

See the following example profile edit in the diagram.

[![Diagram illustrating a profile edit.](media/deployment-external/profile-edit.png)](media/deployment-external/profile-edit-expanded.png#lightbox)

Learn more about setting up a Node.js web application for profile editing.

Learn how to [edit a user profile](../external-id/customers/how-to-web-app-node-edit-profile-prepare-app). Discover how profile edit applications work with middleware API for additional security. The following diagram illustrates middleware API and MFA.

[![Diagram of a profile edit.](media/deployment-external/middleware-api.png)](media/deployment-external/middleware-api-expanded.png#lightbox)