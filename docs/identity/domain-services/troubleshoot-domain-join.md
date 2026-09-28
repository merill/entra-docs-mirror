---
layout: Conceptual
title: Troubleshoot domain-join with Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/troubleshoot-domain-join
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to troubleshoot common problems when you try to domain-join a VM or connect an application to Microsoft Entra Domain Services and you can't connect or authenticate to the managed domain.
ms.topic: troubleshooting
ms.date: 2025-02-19T00:00:00.0000000Z
locale: en-us
document_id: b5ae865e-9bda-4437-254f-79bb14179b00
document_version_independent_id: ef3fd1bc-0b61-b28e-af79-40f36b75d270
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/troubleshoot-domain-join.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/troubleshoot-domain-join
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/troubleshoot-domain-join.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/20ed8455-bc18-4537-87a4-83784e7b2a39
- https://authoring-docs-microsoft.poolparty.biz/devrel/2ed91286-6cf7-4b83-810d-75d0ee3b09dd
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/9a7f703b-30bb-4d62-9eb4-97213f571849
- https://authoring-docs-microsoft.poolparty.biz/devrel/6735bd7e-4f7b-457d-b58c-29e6f0198677
platformId: ac0d9443-8040-841d-34a4-275e296d723d
---

# Troubleshoot domain-join with Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

When you try to join a virtual machine (VM) or connect an application to a Microsoft Entra Domain Services managed domain, you may get an error that you're unable to do so. To troubleshoot domain-join problems, review at which of the following points you have an issue:

- If you don't receive an authentication prompt, the VM or application can't connect to the Domain Services managed domain.
    - Start to troubleshoot connectivity issues for domain-join.
- If you receive an error during authentication, the connection to the managed domain is successful.
    - Start to troubleshoot credentials-related issues during domain-join.

## Connectivity issues for domain-join

If the VM can't find the managed domain, there's usually a network connection or configuration issue. Review the following troubleshooting steps to locate and resolve the issue:

1. Ensure the VM is connected to the same, or a peered, virtual network as the managed domain. If not, the VM can't find and connect to the domain in order to join.
    - If the VM isn't connected to the same virtual network, confirm that the virtual networking peering or VPN connection is *Active* or *Connected* to allow the traffic to flow correctly.
2. Try to ping the domain using the domain name of the managed domain, such as `ping aaddscontoso.com`.
    - If the ping response fails, try to ping the IP addresses for the domain displayed on the overview page in the portal for your managed domain, such as `ping 10.0.0.4`.
    - If you can successfully ping the IP address but not the domain, DNS may be incorrectly configured. Make sure that you've [configured the managed domain DNS servers for the virtual network](tutorial-create-instance#update-dns-settings-for-the-azure-virtual-network).
3. Try flushing the DNS resolver cache on the virtual machine, such as `ipconfig /flushdns`.

### Network Security Group (NSG) configuration

When you create a managed domain, a network security group is also created with the appropriate rules for successful domain operation. If you edit or create additional network security group rules, you may unintentionally block ports required for Domain Services to provide connection and authentication services. These network security group rules can cause issues such as password sync not completing, users not being able to sign in, or domain-join issues.

If you continue to have connection issues, review the following troubleshooting steps:

1. Check the health status of your managed domain in the Azure portal. If you have an alert for *AADDS001*, a network security group rule is blocking access.
2. Review the [required ports and network security group rules](network-considerations#network-security-groups-and-required-ports). Make sure that no network security group rules applied to the VM or virtual network you're connecting from block these network ports.
3. Once any network security group configuration issues are resolved, the *AADDS001* alert disappears from the health page in about 2 hours. With network connectivity now available, try to domain-join the VM again.

## Credentials-related issues during domain-join

If you get a dialog box that asks for credentials to join the managed domain, the VM is able to connect to the domain using the Azure virtual network. The domain-join process fails on authenticating to the domain or authorization to complete the domain-join process using the credentials provides.

To troubleshoot credentials-related issues, review the following troubleshooting steps:

1. Try using the UPN format to specify credentials, such as `dee@contoso.onmicrosoft.com`. Make sure that this UPN is configured correctly in Microsoft Entra ID.
    - The *SAMAccountName* for your account may be autogenerated if there are multiple users with the same UPN prefix in your tenant or if your UPN prefix is overly long. Therefore, the *SAMAccountName* format for your account may be different from what you expect or use in your on-premises domain.
2. Try to use the credentials for a user account that's a part of the managed domain to join VMs to the managed domain.
3. Make sure that you've [enabled password synchronization](tutorial-create-instance#enable-user-accounts-for-azure-ad-ds) and waited long enough for the initial password sync to complete.