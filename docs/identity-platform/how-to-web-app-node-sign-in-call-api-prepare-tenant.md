---
layout: Conceptual
title: Prepare external tenant to call an API in a Node.js web app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-web-app-node-sign-in-call-api-prepare-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to prepare your external tenant to sign in users and call an API in your Node.js web application.
manager: dougeby
ms.topic: how-to
ms.date: 2025-03-16T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 7d72b048-e80d-cf7e-4abf-d56da0c13037
document_version_independent_id: 7d72b048-e80d-cf7e-4abf-d56da0c13037
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-web-app-node-sign-in-call-api-prepare-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-web-app-node-sign-in-call-api-prepare-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-web-app-node-sign-in-call-api-prepare-tenant.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 10cdd227-3357-77f9-1138-244a50d57323
---

# Prepare external tenant to call an API in a Node.js web app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this article, you prepare your external tenant for authorization. This article is the first part of a four-part guide.

## Prerequisite

- Complete the steps in [Tutorial: Set up a Node.js web app to sign in users by using Microsoft identity platform](tutorial-web-app-node-sign-in-prepare-app).
- Complete the steps in [Tutorial: Secure an ASP.NET web API registered in an external tenant](/en-us/entra/external-id/customers/tutorial-protect-web-api-dotnet-core-build-app). After you complete this tutorial, you register a web API in your customer's tenant, which exposes API permissions and publishes application roles. You also have a secured web API. You call this web API from the client web application.

## Configure idtyp token claim [optional]

You can add the **idtyp** optional claim to help the web API to determine whether a token is an **app** token or an **app + user** token. Although you can use a combination of **scp** and **roles** claims for the same purpose, using the **idtyp** claim is the easiest way to tell an app token and an app + user token apart. For example, the value of this claim is *app* when the token is an app-only token.

Use the steps in [Configure optional claims](optional-claims?tabs=appui) article to add idtyp claim to the access token:

- For the **Token type** select **Access**.
- From the optional claims list, select **idtyp**.

### Grant API permissions to the web app

From the prerequisites, you registered a client app in your customer's tenant. You also registered a web API app in your customers. Now, you need to grant API permissions to your client app:

1. From the **App registrations** page, select the application that you created (such as *ciam-client-app*) to open its **Overview** page.
2. Under **Manage**, select **API permissions**.
3. Under **Configured permissions**, select **Add a permission**.
4. Select the **APIs my organization uses** tab.
5. In the list of APIs, select the API such as *ciam-ToDoList-api*.
6. Select **Delegated permissions** option.
7. From the permissions list, select **ToDoList.Read, ToDoList.ReadWrite** (use the search box if necessary).
8. Select the **Add permissions** button.
9. At this point, you've assigned the permissions correctly. However, since the tenant is a customer's tenant, the consumer users themselves can't consent to these permissions. To address this, you as the admin must consent to these permissions on behalf of all the users in the tenant:

    1. Select **Grant admin consent for &lt;your tenant name&gt;**, then select **Yes**.
    2. Select **Refresh**, then verify that **Granted for &lt;your tenant name&gt;** appears under **Status** for both permissions.
10. From the **Configured permissions** list, select the **ToDoList.Read** and **ToDoList.ReadWrite** permissions, one at a time, and then copy the permission's full URI for later use. The full permission URI looks something similar to `api://{clientId}/{ToDoList.Read}` or `api://{clientId}/{ToDoList.ReadWrite}`.