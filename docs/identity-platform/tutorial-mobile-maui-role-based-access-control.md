---
layout: Conceptual
title: 'Tutorial: Use role-based access control in your .NET MAUI mobile app using the Microsoft identity platform - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-mobile-maui-role-based-access-control
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This tutorial demonstrates how to add app roles to .NET Multi-platform App UI (.NET MAUI) and receive them in the ID token.
manager: pmwongera
ms.topic: tutorial
ms.custom: 
ms.date: 2025-03-12T00:00:00.0000000Z
locale: en-us
document_id: 15d66989-f9ae-aa32-4f58-b41a3d7d6230
document_version_independent_id: 15d66989-f9ae-aa32-4f58-b41a3d7d6230
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-mobile-maui-role-based-access-control.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-mobile-maui-role-based-access-control
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-mobile-maui-role-based-access-control.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e6ea396d-3fb5-4a51-91b5-e23ac7ee4d7e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/2b99fe23-e368-4e36-9b45-11c3e25ff3e5
platformId: 56a80123-8822-a4eb-f92d-69d449a3ec73
---

# Tutorial: Use role-based access control in your .NET MAUI mobile app using the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This tutorial demonstrates how to add app roles to .NET Multi-platform App UI (.NET MAUI) and receive them in the ID token.

In this tutorial, you:

- Access the roles in the ID token.

## Prerequisites

- [Tutorial: Sign in users in .NET MAUI shell app](tutorial-mobile-app-maui-sign-in-sign-out)
- [Using role-based access control (RBAC) for applications](../external-id/customers/how-to-use-app-roles-customers)

## Receive groups and roles claims in .NET MAUI

Once you configure your customer's tenant, you can retrieve your roles and groups claims in your client app. The roles and groups claims are both present in the ID token and the access token. Access tokens are only validated in the web APIs for which they were acquired by a client. The client shouldn't validate access tokens.

The .NET MAUI needs to check for the app roles claims in the ID token to implement authorization in the client side.

In this tutorial series, you created a .NET MAUI app where you developed the [*ClaimsView.xaml.cs*](tutorial-mobile-app-maui-sign-in-sign-out#handle-the-claimsview-data) to handle `ClaimsView` data. In this file, we inspect the contents of ID tokens.

To access the role claim, you can modify the code snippet as follows:

```csharp
var idToken = PublicClientSingleton.Instance.MSALClientHelper.AuthResult.IdToken;
var handler = new JwtSecurityTokenHandler();
var token = handler.ReadJwtToken(idToken);
// Get the role claim value
var roleClaim = token.Claims.FirstOrDefault(c => c.Type == "roles")?.Value;

if (!string.IsNullOrEmpty(roleClaim))
{
    // If the role claim exists, add it to the IdTokenClaims
    IdTokenClaims = new List<string> { roleClaim };
}
else
{
    // If the role claim doesn't exist, add a message indicating that no role claim was found
    IdTokenClaims = new List<string> { "No role claim found in ID token" };
}

Claims.ItemsSource = IdTokenClaims;
```

Note

To read the ID token, you must install the `System.IdentityModel.Tokens.Jwt` package.

If you assign a user to multiple roles, the roles string contains all roles separated by a comma, such as `Orders.Manager, Store.Manager,...`. Make sure you build your application to handle the following conditions:

- Absence of roles claims in the token
- User hasn't been assigned to any role
- Multiple values in the roles claim when you assign a user to multiple roles

When you define app roles for your app, it is your responsibility to implement authorization logic for those roles.