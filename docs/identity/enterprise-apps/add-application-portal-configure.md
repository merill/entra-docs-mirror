---
layout: Conceptual
title: Configure enterprise application properties - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/add-application-portal-configure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to configure the properties of an enterprise to how users access and interact with the application.
ms.topic: how-to
ms.date: 2025-06-10T00:00:00.0000000Z
ms.reviewer: ergreenl
zone_pivot_groups: enterprise-apps-minus-legacy-powershell
ms.custom: enterprise-apps
ai-usage: ai-assisted
locale: en-us
document_id: a8a844d8-1aab-daf1-0567-35f2de89fa23
document_version_independent_id: 6d8a875c-8038-5d1d-b0dc-e4c7094844c1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/add-application-portal-configure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/add-application-portal-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/add-application-portal-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c48099d8-1660-5b1a-b334-d0b2c8faaa14
---

# Configure enterprise application properties - Microsoft Entra ID | Microsoft Learn

This article shows you where you can configure the properties of an enterprise application in your Microsoft Entra tenant. For more information about the properties that you can configure, see [Properties of an enterprise application](application-properties).

## Prerequisites

To configure the properties of an enterprise application, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - Cloud Application Administrator
    - Application Administrator, or owner of the service principal.

## Configure application properties

Application properties control how the application is represented and how the application is accessed.

::: zone pivot="portal"

To configure the application properties:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Search for and select the application that you want to use.
4. In the **Manage** section, select **Properties** to open the **Properties** pane for editing.
5. On the **Properties**pane, you might want to configure the following properties for your application.
    - Logo
    - User sign in options
    - App visibility to users
    - Set available URL options
    - Choose whether app assignment is required
6. After you configure the properties according to your apps needs, select **Save**.

::: zone-end

::: zone pivot="ms-powershell"

Use the following Microsoft Graph PowerShell script to configure basic application properties.

You need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) and consent to the `Application.ReadWrite.All` permission.

```powershell

Import-Module Microsoft.Graph.Applications

$params = @{
    Tags = @(
        "HR"
        "Payroll"
        "HideApp"
    )
    Info = @{
        LogoUrl = "https://cdn.pixabay.com/photo/2016/03/21/23/25/link-1271843_1280.png"
        MarketingUrl = "https://www.contoso.com/app/marketing"
        PrivacyStatementUrl = "https://www.contoso.com/app/privacy"
        SupportUrl = "https://www.contoso.com/app/support"
        TermsOfServiceUrl = "https://www.contoso.com/app/termsofservice"
    }
    Web = @{
        HomePageUrl = "https://www.contoso.com/"
        LogoutUrl = "https://www.contoso.com/frontchannel_logout"
        RedirectUris = @(
            "https://localhost"
        )
    }
    ServiceManagementReference = "Owners aliases: Finance @ contosofinance@contoso.com; The Phone Company HR consulting @ hronsite@thephone-company.com;"
}

Update-MgApplication -ApplicationId $applicationId -BodyParameter $params
```

::: zone-end

::: zone pivot="ms-graph"

To configure the basic properties of an application, sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

You need to consent to the `Application.ReadWrite.All` permission.

Run the following Microsoft Graph query to configure basic application properties.

```http
PATCH https://graph.microsoft.com/v1.0/applications/00001111-aaaa-2222-bbbb-3333cccc4444/
Content-type: application/json

{
    "tags": [
        "HR",
        "Payroll",
        "HideApp"
    ],
    "info": {
        "logoUrl": "https://cdn.pixabay.com/photo/2016/03/21/23/25/link-1271843_1280.png",
        "marketingUrl": "https://www.contoso.com/app/marketing",
        "privacyStatementUrl": "https://www.contoso.com/app/privacy",
        "supportUrl": "https://www.contoso.com/app/support",
        "termsOfServiceUrl": "https://www.contoso.com/app/termsofservice"
    },
    "web": {
        "homePageUrl": "https://www.contoso.com/",
        "logoutUrl": "https://www.contoso.com/frontchannel_logout",
        "redirectUris": [
            "https://localhost"
        ]
    },
    "serviceManagementReference": "Owners aliases: Finance @ contosofinance@contoso.com; The Phone Company HR consulting @ hronsite@thephone-company.com;"
}
```

::: zone-end

Enterprise applications (service principals) inherit specific properties from their associated app registrations. These properties are synchronized from the app registration, but the synchronization isn't immediate or continuous. Sometimes, updating an enterprise application might prompt the directory to refresh properties from the app registration, causing updates that weren't part of the original request.

Note

Managed identities are distinct from Microsoft Entra App Registrations. Managed identities only have a service principal object and don't possess an application object, which is typically used for granting app permissions. As a result, global admins can't change the settings of a managed identity, as the security boundary is the resource itself.

## Use Microsoft Graph to configure advanced app properties

You can also configure other advanced properties of both app registrations and enterprise applications (service principals) through Microsoft Graph. These properties include permissions and role assignments. For more information, see [Create and manage a Microsoft Entra application using Microsoft Graph](/en-us/graph/tutorial-applications-basics#configure-other-basic-properties-for-your-app).