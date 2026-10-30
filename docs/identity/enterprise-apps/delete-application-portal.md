---
layout: Conceptual
title: Delete an enterprise application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/delete-application-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Delete an enterprise application in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-06T00:00:00.0000000Z
ms.reviewer: sureshja
zone_pivot_groups: enterprise-apps-all
ms.custom: enterprise-apps, no-azure-ad-ps-ref, sfi-image-nochange
locale: en-us
document_id: 855b5bca-25b0-952a-9fa8-404903df8076
document_version_independent_id: 5e312a51-df80-815f-3ef9-aa9733013b1f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/delete-application-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/delete-application-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/delete-application-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4d61c759-b7ed-1373-34ec-de22ee281bc0
---

# Delete an enterprise application - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to delete an enterprise application that was added to your Microsoft Entra tenant.

When you delete and enterprise application, it remains in a suspended state in the recycle bin for 30 days. During the 30 days, you can [Restore the application](restore-application). Deleted items are automatically hard deleted after the 30-day period. For more information on frequently asked questions about deletion and recovery of applications, see [Deleting and recovering applications FAQs](delete-recover-faq).

Important

Before deleting an enterprise application, consider whether [deactivating it](deactivate-application-portal) meets your needs. Deactivation prevents token issuance and user sign-in while preserving the application configuration, making it ideal for investigation, security incidents, or temporary suspension.

## Prerequisites

To delete an enterprise application, you need:

- A Microsoft Entra user account. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - One of the following roles:
    - Cloud Application Administrator
    - Application Administrator
    - Owner of the service principal
- An [enterprise application added to your tenant](add-application-portal).

::: zone pivot="portal"

## Delete an enterprise application using Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps | All applications**
3. Enter the name of the existing application in the search box, and then select the application from the search results. In this article, we use the **Microsoft Graph Command Line Tools** as an example.
4. In the **Manage** section of the left menu, select **Properties**.
5. At the top of the **Properties** pane, select **Delete**, and then select **Yes** to confirm you want to delete the application from your Microsoft Entra tenant.

    [![screenshot of how to delete an enterprise application.](media/delete-application-portal/delete-application.png)](media/delete-application-portal/delete-application.png#lightbox)

::: zone-end

::: zone pivot="entra-powershell"

## Delete an enterprise application using Microsoft Entra PowerShell

Make sure you're using the [Microsoft Entra PowerShell](/en-us/powershell/entra-powershell/?preserve-view=true&amp;view=entra-powershell) module.

1. Connect to Microsoft Entra PowerShell and sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Get the application you want to delete by filtering by the application name, then delete the application.

    ```powershell
    Connect-Entra -Scopes 'Application.ReadWrite.All'
    Get-EntraServicePrincipal -Filter "displayName eq 'Test-app1'" | Remove-EntraServicePrincipal
    ```

::: zone-end

::: zone pivot="ms-powershell"

## Delete an enterprise application using Microsoft Graph PowerShell

1. Connect to Microsoft Graph PowerShell and sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator):

    ```powershell
    Connect-MgGraph -Scopes 'Application.ReadWrite.All'
    ```
2. Get the list of enterprise applications in your tenant.

    ```powershell
    Get-MgServicePrincipal
    ```
3. Record the object ID of the enterprise app you want to delete.
4. Delete the enterprise application.

    ```powershell
    Remove-MgServicePrincipal -ServicePrincipalId 'aaaaaaaa-bbbb-cccc-1111-222222222222'
    ```

::: zone-end

::: zone pivot="ms-graph"

## Delete an enterprise application using Microsoft Graph API

To delete an enterprise application using [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer), you need to sign in as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).

1. To get the list of service principals in your tenant, run the following query.

    ```http
    GET https://graph.microsoft.com/v1.0/servicePrincipals
    ```
2. Record the ID of the enterprise app you want to delete.
3. Delete the enterprise application.

    ```http
    DELETE https://graph.microsoft.com/v1.0/servicePrincipals/{servicePrincipal-id}
    ```

::: zone-end