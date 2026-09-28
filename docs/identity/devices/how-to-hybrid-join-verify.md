---
layout: HowTo
title: Verify Microsoft Entra hybrid join state - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/how-to-hybrid-join-verify
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Verify configurations for Microsoft Entra hybrid joined devices
ms.reviewer: sandeo
ms.date: 2024-11-25T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- has-azure-ad-ps-ref
- azure-ad-ref-level-one-done
- ge-structured-content-pilot
locale: en-us
document_id: 0e628715-1bb4-d2b9-3759-6666a3554503
document_version_independent_id: 8dd9934c-d595-b6fc-c217-3d0b58f12a51
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/how-to-hybrid-join-verify.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/how-to-hybrid-join-verify
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/how-to-hybrid-join-verify.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 533679e3-7a67-3c6a-4444-05812d7e0692
---

# Verify Microsoft Entra hybrid join state - Microsoft Entra ID | Microsoft Learn

This article describes three ways to locate and verify the Microsoft Entra hybrid joined device state.

## Prerequisites

None

## Locally on the device

Follow these steps:

1. Open Windows PowerShell.
2. Enter `dsregcmd /status`.
3. Verify that both **AzureAdJoined** and **DomainJoined** are set to **YES**.
4. You can use the **DeviceId** and compare the status on the service using either the Microsoft Entra admin center or PowerShell.

## Using the Microsoft Entra admin center

Follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Device Administrator](../role-based-access-control/permissions-reference#cloud-device-administrator).
2. Browse to **Entra ID** &gt; **Devices** &gt; **All devices**.
3. If the **Registered** column says **Pending**, then Microsoft Entra hybrid join hasn't completed. In federated environments, this state happens only if it failed to register and Microsoft Entra Connect is configured to sync the devices. Wait for Microsoft Entra Connect to complete a sync cycle.
4. If the **Registered** column contains a **date/time**, then Microsoft Entra hybrid join has completed.

## Using PowerShell

Verify the device registration state in your Azure tenant by using [Get-MgDevice](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice). This cmdlet is in the [Microsoft Graph PowerShell SDK](/en-us/powershell/microsoftgraph/overview).

When you use the **Get-MgDevice** cmdlet to check the service details:

- An object with the **device ID** that matches the ID on the Windows client must exist.
- The value for **DeviceTrustType** is **Domain Joined**. This setting is equivalent to the **Microsoft Entra hybrid joined** state on the **Devices** page in the Microsoft Entra admin center.
- For devices that are used in Conditional Access, the value for **Enabled** is **True** and **DeviceTrustLevel** is **Managed**.

1. Open Windows PowerShell as an administrator.
2. Enter [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands#using-connect-mggraph) to connect to your Azure tenant.

### Count all Microsoft Entra hybrid joined devices (excluding **Pending** state)

    ```powershell
    (Get-MgDevice -All | where {($_.TrustType -eq 'ServerAd') -and ($_.ProfileType -eq 'RegisteredDevice')}).count
    ```

### Count all Microsoft Entra hybrid joined devices with **Pending** state

    ```powershell
    (Get-MgDevice -All | where {($_.TrustType -eq 'ServerAd') -and ($_.ProfileType -ne 'RegisteredDevice')}).count
    ```

### List all Microsoft Entra hybrid joined devices

    ```powershell
    Get-MgDevice -All | where {($_.TrustType -eq 'ServerAd') -and ($_.ProfileType -eq 'RegisteredDevice')}
    ```

### List all Microsoft Entra hybrid joined devices with **Pending** state

    ```powershell
    Get-MgDevice -All | where {($_.TrustType -eq 'ServerAd') -and ($_.ProfileType -ne 'RegisteredDevice')}
    ```

### List details of a single device:

    1. Enter the following command. Obtain the device ID locally on the device.

    ```powershell
    $Device = Get-MgDevice -DeviceId <ObjectId>
    ```

    1. Verify that `AccountEnabled` is set to `True`.

    ```powershell
    $Device.AccountEnabled
    ```