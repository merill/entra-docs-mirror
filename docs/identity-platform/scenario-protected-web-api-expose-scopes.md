---
layout: Conceptual
title: Expose scopes in a protected web API - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-protected-web-api-expose-scopes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to expose scopes in a protected web API.
manager: pmwongera
ms.custom: 
ms.date: 2024-05-28T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: caaa6d31-5644-e962-305e-cbfbcc907da8
document_version_independent_id: caaa6d31-5644-e962-305e-cbfbcc907da8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-protected-web-api-expose-scopes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-protected-web-api-expose-scopes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-protected-web-api-expose-scopes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 44c428d1-c267-4119-6290-11e44c5804fa
---

# Expose scopes in a protected web API - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article explains how to add scopes to an application for a protected web API.

## Prerequisites

- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID

## Scopes and the Application ID URI

Scopes usually have the form `resourceURI/scopeName`. For Microsoft Graph, the scopes have shortcuts. For example, `User.Read` is a shortcut for `https://graph.microsoft.com/user.read`.

During app registration, define these parameters:

- The resource URI
- One or more scopes
- One or more app roles

By default, the application registration portal recommends that you use the resource URI `api://{clientId}`. This URI is unique but not human readable. If you change the URI, make sure the new value is unique. The application registration portal ensures that you use a [configured publisher domain](howto-configure-publisher-domain).

To client applications, scopes show up as *delegated permissions* and app roles show up as *application permissions* for your web API.

Scopes also appear on the consent window that's presented to users of your app. Therefore, provide the corresponding strings that describe the scope:

- As seen by a user.
- As seen by a tenant admin, who can grant admin consent.

App roles can't be consented to by a user (as they're used by an application that calls the web API on behalf of itself). A tenant administrator needs to consent to client applications of your web API exposing app roles. See [Admin consent](v2-admin-consent) for details.

### Expose delegated permissions (scopes)

To expose delegated permissions, or *scopes*, follow the steps in [Configure an application to expose a web API](quickstart-configure-app-expose-web-apis).

If you're following along with the web API scenario described in this set of articles, use these settings:

- **Application ID URI**: Accept the proposed application ID URI (*api://&lt;clientId&gt;*) (if prompted)
- **Scope name**: *access\_as\_user*
- **Who can consent**: *Admins and users*
- **Admin consent display name**: *Access TodoListService as a user*
- **Admin consent description**: *Accesses the TodoListService web API as a user*
- **User consent display name**: *Access TodoListService as a user*
- **User consent description**: *Accesses the TodoListService web API as a user*
- **State**: *Enabled*

Tip

For the **Application ID URI**, you can set it to the physical authority of the API, for example `https://graph.microsoft.com`. This can be useful if the URL of the API that needs to be called is known.

### If your web API is called by a service or daemon app

Expose *application permissions* instead of delegated permissions if your API should be accessed by daemons, services, or other non-interactive (by a human) applications. Because daemon- and service-type applications run unattended and authenticate with their own identity, there's no user to "delegate" their permission.

#### Expose application permissions (app roles)

To expose application permissions, follow the steps in [Add app roles to your app](howto-add-app-roles-in-apps).

In the **Create app role** pane under **Allowed member types**, select **Applications**. Or, add the role by using the **Application manifest editor** as described in the article.

#### Restrict access tokens to specific clients apps

App roles are the mechanism an application developer uses to expose their app's permissions. Your web API's code should check for app roles in the access tokens it receives from callers.

To add another layer of security, a Microsoft Entra tenant administrator can configure their tenant so the Microsoft identity platform issues security tokens *only* to the client apps the tenant administrator has approved for API access.

To increase security by restricting token issuance only to client apps that have been assigned app roles:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), select your app under **Entra ID** &gt; **App registrations**.
2. On the application's **Overview** page, in **Essentials**, find and select its **Managed application in local directory** link to navigate to its **Enterprise Application Overview** page.
3. Under **Manage**, select **Properties**.
4. Set **Assignment required?** to **Yes**.
5. Select **Save**.

Microsoft Entra ID will now check for app role assignments of client applications that request access tokens for your web API. If a client app hasn't been assigned any app roles, Microsoft Entra ID returns an error message to the client similar to `_invalid_client: AADSTS501051: Application \<application name\> isn't assigned to a role for the \<web API\>_`.

Warning

**DO NOT use AADSTS error codes** or their message strings as literals in your application's code. The "AADSTS" error codes and the error message strings returned by Microsoft Entra ID aren't immutable\*, and may be changed by Microsoft at any time and without your knowledge. If you make branching decisions in your code based on the values of either the AADSTS codes or their message strings, you put your application's functionality and stability at risk.