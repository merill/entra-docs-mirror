---
layout: Conceptual
title: Create an enterprise application from a multitenant application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/create-service-principal-cross-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: CelesteD
description: Create an enterprise application using the client ID for a multitenant application.
ms.topic: how-to
ms.date: 2025-07-10T00:00:00.0000000Z
ms.reviewer: karavar
ms.custom: mode-other, devx-track-azurecli
zone_pivot_groups: enterprise-apps-cli
locale: en-us
document_id: e04196e9-7028-462a-c2b4-48ecb13204f2
document_version_independent_id: 0603f7a0-71d9-abce-8a7e-641d18a7987b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/create-service-principal-cross-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/create-service-principal-cross-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/create-service-principal-cross-tenant.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5240d6a0-18e0-6ff5-09a1-a12ea8e31e15
---

# Create an enterprise application from a multitenant application - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to create an enterprise application in your tenant using the client ID for a multitenant application. An enterprise application refers to a service principal within a tenant. The service principal discussed in this article is the local representation, or application instance, of a global application object in a single tenant or directory.

Before you proceed to add the application using any of these options, check whether the enterprise application is already in your tenant by attempting to sign in to the application. If the sign-in is successful, the enterprise application already exists in your tenant.

If you verify that the application isn't in your tenant, proceed with any of the following ways to add the enterprise application to your tenant.

## Prerequisites

To add an enterprise application to your Microsoft Entra tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, or Application Administrator.
- The client ID (also called appId in Microsoft Graph) of the multitenant application.

## Create an enterprise application

::: zone pivot="admin-consent-url"

If you're provided with the admin consent URL, navigate to the URL through a web browser to [grant tenant-wide admin consent](grant-admin-consent) to the application. Granting tenant-wide admin consent to the application adds it to your tenant. The tenant-wide admin consent URL has the following format:

```http
https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=248e869f-0e5c-484d-b5ea1fba9563df41&redirect_uri=https://www.your-app-url.com
```

Where:

- `{client-id}` is the application's client ID (also known as appId).

Note

If you're attempting to use an enterprise application, and the service principal isn't yet created in your tenant, Microsoft Entra responds with a (401) Unauthorized error stating: "The client application {appId} is missing a service principal in the tenant {tenantId}." To resolve this, performing consent with the admin consent URL as mentioned earlier instantiates the service principal in your tenant and resolve the issue.

::: zone-end

::: zone pivot="msgraph-powershell"

1. Run `connect-MgGraph -Scopes "Application.ReadWrite.All"` and sign in with at least a Cloud Application Administrator role.
2. Run the following command to create the enterprise application:

    ```powershell
    New-MgServicePrincipal -AppId 00001111-aaaa-2222-bbbb-3333cccc4444
    ```
3. To delete the enterprise application you created, run the command:

    ```powershell
    Remove-MgServicePrincipal
       -ServicePrincipalId aaaaaaaa-bbbb-cccc-1111-222222222222
    
    ```

::: zone-end

::: zone pivot="ms-graph"

You can use an API client such as [Graph Explorer](https://aka.ms/ge) to work with Microsoft Graph.

1. Grant the client app the `Application.ReadWrite.All` permission.
2. To create the enterprise application, run the following query. The appId is the client ID of the application.

    ```http
    POST https://graph.microsoft.com/v1.0/servicePrincipals
    Content-type: application/json
    
    {
      "appId": "00001111-aaaa-2222-bbbb-3333cccc4444"
    }
    
    ```
3. To delete the enterprise application you created, run the query.

    ```http
    DELETE https://graph.microsoft.com/v1.0/servicePrincipals(appId='00001111-aaaa-2222-bbbb-3333cccc4444')
    ```

::: zone-end

::: zone pivot="azure-cli"

1. To create the enterprise application, run the following command:

    ```azurecli
    az ad sp create --id 00001111-aaaa-2222-bbbb-3333cccc4444
    ```
2. To delete the enterprise application you created, run the command:

    ```azurecli
    az ad sp delete --id bbbbbbbb-1111-2222-3333-cccccccccccc
    
    ```

::: zone-end