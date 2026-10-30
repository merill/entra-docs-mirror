---
layout: Conceptual
title: Use role-based access control in your Node.js web app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-web-app-role-based-access-control
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure groups and user roles in your external tenant, so you can receive them as claims in a security token for your Node.js application
manager: dougeby
ms.topic: how-to
ms.date: 2025-03-16T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: e37de24c-9781-4dca-066f-5c2f4381e11e
document_version_independent_id: e37de24c-9781-4dca-066f-5c2f4381e11e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-web-app-role-based-access-control.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-web-app-role-based-access-control
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-web-app-role-based-access-control.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 251a035e-b13f-ffaf-a702-363d846c6df5
---

# Use role-based access control in your Node.js web app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Role-based access control (RBAC) is a mechanism to enforce authorization in applications. Microsoft Entra External ID allows you to define application roles for your application and assign those roles to users and groups. The roles you assign to a user or group define their level of access to the resources and operations in your application. When External ID issues a security token for an authenticated user, it includes the names of the roles you've assigned the user or group in the security token's roles claim.

You can also configure your external tenant to return the group memberships of the user. Developers can then use security groups to implement RBAC in their applications, where the memberships of the user in specific groups are interpreted as their role memberships.

Once you assign users and groups to roles, the *roles* claim is emitted in your security token. However, to emit the *groups* membership claim in security tokens, you need additional configuration in your external tenant.

In this article, you learn how to receive user roles or group membership or both as claims in a security token for your Node.js web app.

## Prerequisites

- If you've not done so, complete the steps in [Using role-based access control for applications](../external-id/customers/how-to-use-app-roles-customers) article. This article shows you how to create roles for your application, how to assign users and groups to those roles, how to add members to a group and how to add a group claim to a to security token. Learn more about [ID tokens](id-tokens) and [access tokens](access-tokens).
- If you've not done so, complete the steps in [Sign in users in your own Node.js web application](tutorial-web-app-node-sign-in-prepare-app)

## Receive groups and roles claims in your Node.js web app

Once you configure your external tenant, you can retrieve your *roles* and *groups* claims in your client app. The *roles* and *groups* claims are both present in the ID token and the access token, but your client app only needs to check for these claims in the ID token to implement authorization in the client side. The API app can also retrieve these claims when it receives the access token.

You check your *roles* claim value as shown in the following code snippet example:

```javascript
const msal = require('@azure/msal-node');
const { msalConfig, TENANT_SUBDOMAIN, REDIRECT_URI, POST_LOGOUT_REDIRECT_URI } = require('../authConfig');

...
class AuthProvider {
...
    async handleRedirect(req, res, next) {
        const authCodeRequest = {
            ...req.session.authCodeRequest,
            code: req.body.code, // authZ code
            codeVerifier: req.session.pkceCodes.verifier, // PKCE Code Verifier
        };
    
        try {
            const msalInstance = this.getMsalInstance(this.config.msalConfig);
            const tokenResponse = await msalInstance.acquireTokenByCode(authCodeRequest, req.body);
            let roles = tokenResponse.idTokenClaims.roles;
        
            //Check roles
            if (roles && roles.includes("Orders.Manager")) {
                //This user can view the ID token claims page.
                res.redirect('/id');
            }
            
            //User can only view the index page.
            res.redirect('/');
        } catch (error) {
            next(error);
        }
    }
...
}

```

If you assign a user to multiple roles, the `roles` string contains all roles separated by a comma, such as `Orders.Manager,Store.Manager,...`. Make sure you build your application to handle the following conditions:

- absence of `roles` claim in the token
- user hasn't been assigned to any role
- multiple values in the `roles` claim when you assign a user to multiple roles

You can also check your *groups* claim value as shown in the following code snippet example:

```javascript
const tokenResponse = await msalInstance.acquireTokenByCode(authCodeRequest, req.body);
let groups = tokenResponse.idTokenClaims.groups;
```

The groups claim value is the group's *objectId*. If a user is a member of multiple groups, the `groups` string contains all groups separated by a comma, such as `7f0621bc-b758-44fa-a2c6-...,6b35e65d-f3c8-4c6e-9538-...`.

Note

If you assign a user [Microsoft Entra in-built roles](../identity/role-based-access-control/permissions-reference) or commonly known as directory roles, those roles appear in the *groups* claim of the security token.

## Handle groups overage

To ensure that the size of the security token doesn’t exceed the HTTP header size limit, External ID limits the number of object IDs that it includes in the *groups* claim. The overage limit is **150 for SAML tokens and 200 for JWT tokens**. It's possible to exceed this limit if a user belongs to many groups, and you request for all the groups.

### Detect group overage in your source code

If you can't avoid groups overages, then you need to handle it in your code. When you exceed the overage limit, the token doesn't contain the *groups* claim. Instead, the token contains a *\_claim\_names* claim that contains a *groups* member of the array. So, you need to check the existence of *\_claim\_names* claim to tell that an overage has occurred. The following code snippet shows you how to detect a groups overage:

```javascript
const tokenResponse = await msalInstance.acquireTokenByCode(authCodeRequest, req.body);

if(tokenResponse.idTokenClaims.hasOwnProperty('_claim_names') && tokenResponse.idTokenClaims['_claim_names'].hasOwnProperty('groups')) {
    //overage has occurred
}
```

Use the instructions in [Configuring group claims and app roles in tokens](/en-us/security/zero-trust/develop/configure-tokens-group-claims-app-roles#group-overages) article to learn how request for the full groups list when groups overage occurs.

## How to use groups and roles values in your Node.js web app

In the client app, you can verify whether a signed-in user has the necessary role(s) to access a protected route or call an API endpoint. To do so, you check the `roles` claim in the ID token. To implement this protection in your app, you can build guards by using a custom middleware.

In your service app (API app), you can also protect the API endpoints. After you [validate the access token](access-tokens#validate-tokens) sent by the client app, you can check for the *roles* or *groups* claims in the payload claims of the access token.

## Do I use App Roles or Groups?

In this article, you have learned that you can use *App Roles* or *Groups* to implement RBAC in your application. The preferred approach is to use app roles as it provides more granular control when managing access/permissions at the application level. For more information on how to choose an approach, see [Choose an approach](custom-rbac-for-developers#choose-an-approach).