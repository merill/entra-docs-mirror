---
layout: Conceptual
title: Targeted deployments of Microsoft Entra hybrid join - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/hybrid-join-control
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Learn how to do a targeted deployment of Microsoft Entra hybrid join before enabling it across the entire organization all at once.
ms.topic: how-to
ms.date: 2024-06-27T00:00:00.0000000Z
ms.reviewer: sandeo
locale: en-us
document_id: 2928e23e-3210-9e74-9cdb-1a19b703eac7
document_version_independent_id: 44e303ca-e4bc-ba30-5aae-311aa9318278
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/hybrid-join-control.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/hybrid-join-control
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/hybrid-join-control.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 26f972be-d1ec-063f-a5d5-8686d431acfa
---

# Targeted deployments of Microsoft Entra hybrid join - Microsoft Entra ID | Microsoft Learn

You can validate your [planning and prerequisites](hybrid-join-plan) for hybrid Microsoft Entra joining devices using a targeted deployment before enabling it across the entire organization. This article explains how to accomplish a targeted deployment of Microsoft Entra hybrid join.

Caution

Use caution when modifying values in Active Directory. Making changes in an established environment might have unintended consequences.

## Targeted deployment of Microsoft Entra hybrid join on Windows devices

For devices running Windows 10, the minimum supported version is Windows 10 (version 1607) to do hybrid join. As a best practice, upgrade to the latest version of Windows 10 or 11.

To do a targeted deployment of Microsoft Entra hybrid join on Windows devices, you need to:

1. Clear the Service Connection Point (SCP) entry from Windows Server Active Directory if it exists.
2. Configure client-side registry setting for SCP on your domain-joined computers using a Group Policy Object (GPO).
3. If you're using Active Directory Federation Services (AD FS), you must also configure the client-side registry setting for SCP on your AD FS server using a GPO.
4. You might need to [customize synchronization options](../hybrid/connect/how-to-connect-post-installation#additional-tasks-available-in-azure-ad-connect) in Microsoft Entra Connect to enable device synchronization.

Tip

The SCP might be configured locally in the registry of the device in certain situations. If the device finds a value in the registry it uses that configuration, otherwise it queries the directory for the SCP and attempts to hybrid join.

### Clear the SCP from Microsoft Windows Server Active Directory

Use the Active Directory Services Interfaces Editor (ADSI Edit) to modify the SCP objects in Microsoft Windows Server Active Directory.

1. Launch the **ADSI Edit** desktop application from and administrative workstation or a domain controller as an Enterprise Administrator.
2. Connect to the **Configuration Naming Context** of your domain.
3. Browse to **CN=Configuration,DC=contoso,DC=com** &gt; **CN=Services** &gt; **CN=Device Registration Configuration**.
4. Right-click on the leaf object **CN=62a0ff2e-97b9-4513-943f-0d221bd30080** and select **Properties**.
    1. Select **keywords** from the **Attribute Editor** window and select **Edit**.
    2. Select the values of **azureADId** and **azureADName** (one at a time) and select **Remove**.
5. Close **ADSI Edit**.

### Configure client-side registry setting for SCP

Use the following example to create a Group Policy Object (GPO) to deploy a registry setting configuring an SCP entry in the registry of your devices.

1. Open a Group Policy Management console and create a new Group Policy Object in your domain.
    1. Provide your newly created GPO a name (for example, ClientSideSCP).
2. Edit the GPO and locate the following path: **Computer Configuration** &gt; **Preferences** &gt; **Windows Settings** &gt; **Registry**.
3. Right-click on the Registry and select **New** &gt; **Registry Item**.
    1. On the **General**tab, configure the following.
        1. Action: **Update**.
        2. Hive: **HKEY\_LOCAL\_MACHINE**.
        3. Key Path: **SOFTWARE\Microsoft\Windows\CurrentVersion\CDJ\AAD**.
        4. Value name: **TenantId**.
        5. Value type: **REG\_SZ**.
        6. Value data: The globally unique identifier (GUID) or **Tenant ID** of your Microsoft Entra tenant, which can be found in **Entra ID** &gt; **Overview** &gt; **Properties** &gt; **Tenant ID**.
    2. Select **OK**.
4. Right-click on the Registry and select **New** &gt; **Registry Item**.
    1. On the **General**tab, configure the following.
        1. Action: **Update**.
        2. Hive: **HKEY\_LOCAL\_MACHINE**.
        3. Key Path: **SOFTWARE\Microsoft\Windows\CurrentVersion\CDJ\AAD**.
        4. Value name: **TenantName**.
        5. Value type: **REG\_SZ**.
        6. Value data: Your verified **domain name** if you're using federated environment such as AD FS. Your verified **domain name** or your onmicrosoft.com domain name, for example `contoso.onmicrosoft.com` if you're using managed environment.
    2. Select **OK**.
5. Close the editor for the newly created GPO.
6. Link the newly created GPO to the correct organizational unit (OU) containing domain-joined computers that belong to your controlled rollout population.

### Configure AD FS settings

If your Microsoft Entra ID is federated with AD FS, you first need to configure client-side SCP using the instructions mentioned earlier by linking the GPO to your AD FS servers. The SCP object defines the source of authority for device objects. It can be on-premises or Microsoft Entra ID. When client-side SCP is configured for AD FS, the source for device objects is established as Microsoft Entra ID.

Note

If you failed to configure client-side SCP on your AD FS servers, the source for device identities would be considered as on-premises. AD FS will then start deleting device objects from on-premises directory after the stipulated period defined in the AD FS Device Registration's attribute "MaximumInactiveDays". AD FS Device Registration objects can be found using the [Get-AdfsDeviceRegistration cmdlet](/en-us/powershell/module/adfs/get-adfsdeviceregistration).

## Why a device might be in a pending state

When you configure a **Microsoft Entra hybrid join** task in the Microsoft Entra Connect Sync for your on-premises devices, the task syncs device objects to Microsoft Entra ID, and temporarily set the registered state of the devices to "pending" before the device completes the device registration. This pending state is because the device must be added to the Microsoft Entra directory before it can be registered. For more information about the device registration process, see [How it works: Device registration](device-registration-how-it-works#hybrid-azure-ad-joined-in-managed-environments).

## Post validation

After you verify that everything works as expected, you can automatically register the rest of your Windows devices with Microsoft Entra ID. Automate Microsoft Entra hybrid join by [configuring the SCP using Microsoft Entra Connect](how-to-hybrid-join).