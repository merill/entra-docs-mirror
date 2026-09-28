---
layout: Conceptual
title: Assign enterprise application owners - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/assign-app-owners
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to assign an owner to an enterprise application in Microsoft Entra ID, manage configurations, and streamline user access efficiently.
ms.topic: how-to
ms.date: 2024-12-06T00:00:00.0000000Z
ms.reviewer: saibandaru
zone_pivot_groups: enterprise-apps-minus-legacy-powershell
ms.custom: enterprise-apps
locale: en-us
document_id: 04afeb04-37a2-4613-ede7-84dbc3ee2031
document_version_independent_id: 11d52bff-1fa4-343c-8745-2db25577031c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/assign-app-owners.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/assign-app-owners
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/assign-app-owners.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 96db16ff-3118-cf08-5995-9289d8ba2c1c
---

# Assign enterprise application owners - Microsoft Entra ID | Microsoft Learn

An [owner of an enterprise application](overview-assign-app-owners) in Microsoft Entra ID can manage the organization-specific configuration of the application, such as single sign-on, provisioning, and user assignments. An owner can also add or remove other owners. Unlike other Application Administrators, owners can manage only the enterprise applications they own. In this article, you learn how to assign an owner of an application.

## Prerequisites

To add an enterprise application to your Microsoft Entra tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, or Application Administrator.

## Assign an owner

::: zone pivot="portal"

To assign an owner to an enterprise application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Select the application that you want to add an owner to.
4. Select **Owners**, and then select **Add** to get a list of user accounts that you can choose an owner from.
5. Search for and select the user account that you want to be an owner of the application.
6. Select **Select** to add the user account that you chose as an owner of the application.

::: zone-end

::: zone pivot="ms-powershell"

To add an owner to an enterprise application using Microsoft Graph PowerShell, you need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) and consent to the `Application.ReadWrite.All` permission.

In the following example, the user's object ID is aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb and the applicationId is 00001111-aaaa-2222-bbbb-3333cccc4444.

```powershell
1. Connect-MgGraph -Scopes 'Application.ReadWrite.All'

1. Import-Module Microsoft.Graph.Applications

$params = @{
    "@odata.id" = "https://graph.microsoft.com/v1.0/directoryObjects/aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
}

New-MgServicePrincipalOwnerByRef -ServicePrincipalId 'aaaaaaaa-bbbb-cccc-1111-222222222222' -BodyParameter $params
```

::: zone-end

::: zone pivot="ms-graph"

To assign an owner to an application using Microsoft Graph API, sign in to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

You need to consent to the `Application.ReadWrite.All` permission.

Run the following Microsoft Graph query to assign an owner to an application. You need the object ID of the user you want to assign the application to. In the following example, the user's object ID is aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb and the appId is 00001111-aaaa-2222-bbbb-3333cccc4444.

```http
POST https://graph.microsoft.com/v1.0/servicePrincipals(appId='00001111-aaaa-2222-bbbb-3333cccc4444')/owners/$ref
Content-Type: application/json

{
    "@odata.id": "https://graph.microsoft.com/v1.0/directoryObjects/aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
}
```

::: zone-end

Note

If the user setting **Restrict access to Microsoft Entra administration portal** is set to `Yes`, non-admin users aren't able to use the Microsoft Entra admin center to manage the applications they own. For more information about the actions that can be performed on owned enterprise applications, see [Owned enterprise applications](../../fundamentals/users-default-permissions#owned-enterprise-applications).

Note

Currently due to background applications and service principals objects settings dependencies, the application owners added by other than Entra admin center means (Graph API, PowerShell), will not be able to manage some enterprise applications settings like attributes and claims, modify configured SAML certificates properties or token encryption settings, etc.