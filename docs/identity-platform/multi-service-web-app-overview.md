---
layout: Conceptual
title: Tutorial - Build a secure web app on Azure App Service - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/multi-service-web-app-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this tutorial, you learn how to build a web app by using Azure App Service, sign in users to the web app, call Azure Storage, and call Microsoft Graph.
manager: pmwongera
ms.custom: 
ms.date: 2024-02-07T00:00:00.0000000Z
ms.reviewer: stsoneff
ms.subservice: 
ms.topic: tutorial
locale: en-us
document_id: 7ae0b903-d102-d8e2-0d1c-4d30552dba69
document_version_independent_id: f3b6f62a-e423-fbba-a665-1b61495fc9e5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/multi-service-web-app-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/multi-service-web-app-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/multi-service-web-app-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 5946a240-62e1-9ef6-a89e-11da753a97a9
---

# Tutorial - Build a secure web app on Azure App Service - Microsoft identity platform | Microsoft Learn

This tutorial describes a common application scenario: an internal employee dashboard web application. Your web app is hosted in Azure App Service and needs to connect to Microsoft Graph and Azure Storage in order to get data to visualize in the dashboard. In some cases, the web app needs to get data that only the signed-in user can access. In other cases, the web app needs to access data under the identity of the app itself, and not the signed-in user. Access to the web application needs to be restricted to users in your organization.

The goal of this tutorial *isn't* to show how to build the dashboard itself or visualize data. Rather, the tutorial focuses on the identity-related aspects of the described scenario. Learn how to:

- [Configure authentication for a web app](multi-service-web-app-authentication-app-service) and limit access to users in your organization​. See A in the diagram.
- [Securely access Azure Storage](multi-service-web-app-access-storage) from the web application using managed identities​. See B in the diagram.
- Access data in Microsoft Graph from the web application (See C in the diagram):
    - [as the signed-in user​](multi-service-web-app-access-microsoft-graph-as-user)
    - [as the web application](multi-service-web-app-access-microsoft-graph-as-app) using managed identities​
- [Clean up the resources](multi-service-web-app-clean-up-resources) you created for this tutorial.

![Diagram that shows application scenarios in Microsoft identity platform.](media/multi-service-web-app-overview/web-app.svg)