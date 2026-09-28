---
layout: Conceptual
title: Hide an enterprise application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/hide-application-from-user-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: How to hide an Enterprise application from user's experience in Microsoft Entra ID access portals or Microsoft 365 launchers.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: ergreenl, lenalepa
ms.collection: M365-identity-device-management
zone_pivot_groups: enterprise-apps-all
ms.custom: enterprise-apps, no-azure-ad-ps-ref, sfi-ga-blocked
locale: en-us
document_id: 36e1110f-232a-659e-d35e-06044409d4fa
document_version_independent_id: b419025c-acc1-ed0e-3d4d-e22721d6796b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/hide-application-from-user-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/hide-application-from-user-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/hide-application-from-user-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2503b4af-9f0f-d82a-d48b-aa2c3f8dd245
---

# Hide an enterprise application - Microsoft Entra ID | Microsoft Learn

Learn how to hide enterprise applications in Microsoft Entra ID. When an application is hidden, users still have permissions to the application.

## Prerequisites

To hide an application from the My Apps portal and Microsoft 365 launcher, you need:

- A Microsoft Entra account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - Cloud Application Administrator
    - Application Administrator.
    - Global Administrator is required to hide all Microsoft 365 applications.

## Hide an application from the end user

::: zone pivot="portal"

Use the following steps to hide an application from My Apps portal and Microsoft 365 application launcher.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Search for the application you want to hide, and select the application.
4. In the left navigation pane, select **Properties**.
5. Select **No** for the **Visible to users?** question.
6. Select **Save**.

::: zone-end

Note

These instructions apply only to non-first-party Microsoft Enterprise Applications. To learn more about first-party Microsoft applications see [First-party Microsoft applications in sign-in reports](/en-us/troubleshoot/azure/entra/entra-id/governance/verify-first-party-apps-sign-in). Administrators also need to keep in mind that hiding the application from the users doesn't prevent them from signing into these applications via methods other than the My Apps portal, such as shared links or service dependencies.

::: zone pivot="entra-powershell"

To hide an application from the My Apps portal, using Microsoft Entra PowerShell, you need to connect to Microsoft Entra PowerShell and sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator). You can manually add the **HideApp** tag to the service principal for the application. Run the following Microsoft Entra PowerShell commands to set the application's **Visible to Users?** property to **No**.

```PowerShell
Connect-Entra -scopes "Application.ReadWrite.All"

$objectId = "<objectId>"
$servicePrincipal = Get-EntraServicePrincipal -ObjectId $objectId
$tags = $servicePrincipal.tags
$tags += "HideApp"
Set-EntraServicePrincipal -ObjectId $objectId -Tags $tags
```

::: zone-end

::: zone pivot="ms-powershell"

To hide an application from the My Apps portal, using Microsoft Graph PowerShell, you need to connect to Microsoft Graph PowerShell and sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator). You can manually add the HideApp tag to the service principal for the application. Run the following Microsoft Graph PowerShell commands to set the application's **Visible to Users?** property to **No**.

```PowerShell
Connect-MgGraph "Application.ReadWrite.All"
$tags = $servicePrincipal.tags
$tags += "HideApp"
Update-MgServicePrincipal -ServicePrincipalID  $objectId -Tags $tags
```

::: zone-end

::: zone pivot="ms-graph"

To hide an enterprise application using [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), you need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

Ensure you consent to the `Application.ReadWrite.All` permission before running the queries.

Run the following queries.

1. Get the application you want to hide.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals/00001111-aaaa-2222-bbbb-3333cccc4444
    ```
2. Update the application to hide it from users.

    ```http
    PATCH https://graph.microsoft.com/v1.0/servicePrincipals/00001111-aaaa-2222-bbbb-3333cccc4444/
    ```

    Supply the following request body.

    ```json
    {
        "tags": [
        "HideApp"
        ]
    }
    ```

    Warning

    If the application has other tags, you must include them in the request body. Otherwise, the query will overwrite them.

::: zone-end

::: zone pivot="portal"

## Hide Microsoft 365 applications from the My Apps portal

Use the following steps to hide all Microsoft 365 applications from the My Apps portal. The applications are still visible in the Office 365 portal.

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select **App launchers** under **Manage** menu items.
4. Select **Settings**.
5. Enable the option of **Users can only see Microsoft 365 apps in the Microsoft 365 portal**.
6. Select **Save**.

::: zone-end