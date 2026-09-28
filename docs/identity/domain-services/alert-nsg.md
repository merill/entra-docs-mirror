---
layout: Conceptual
title: Resolve network security group alerts in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/alert-nsg
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to troubleshoot and resolve network security group configuration alerts for Microsoft Entra Domain Services
ms.assetid: 95f970a7-5867-4108-a87e-471fa0910b8c
ms.topic: troubleshooting
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 61590171-058a-bd67-e9c1-7b60dd0351da
document_version_independent_id: 0ce24aba-4f3b-cbc9-d020-bedc8f535a6b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/alert-nsg.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/alert-nsg
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/alert-nsg.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/20ed8455-bc18-4537-87a4-83784e7b2a39
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/9a7f703b-30bb-4d62-9eb4-97213f571849
platformId: f2133c8f-5109-aff5-8e4f-3de4bf61040d
---

# Resolve network security group alerts in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

To let applications and services correctly communicate with a Microsoft Entra Domain Services managed domain, specific network ports must be open to allow traffic to flow. In Azure, you control the flow of traffic using network security groups. The health status of a Domain Services managed domain shows an alert if the required network security group rules aren't in place.

This article helps you understand and resolve common alerts for network security group configuration issues.

## Alert AADDS104: Network error

### Alert message

*Microsoft is unable to reach the domain controllers for this managed domain. This may happen if a network security group (NSG) configured on your virtual network blocks access to the managed domain. Another possible reason is if there's a user-defined route that blocks incoming traffic from the internet.*

Invalid network security group rules are the most common cause of network errors for Domain Services. The network security group for the virtual network must allow access to specific ports and protocols. If these ports are blocked, the Azure platform can't monitor or update the managed domain. The synchronization between the Microsoft Entra directory and Domain Services is also impacted. Make sure you keep the default ports open to avoid interruption in service.

## Default security rules

The following default inbound and outbound security rules are applied to the network security group for a managed domain. These rules keep Domain Services secure and allow the Azure platform to monitor, manage, and update the managed domain.

### Inbound security rules

| Priority | Name | Port | Protocol | Source | Destination | Action |
| --- | --- | --- | --- | --- | --- | --- |
| 301 | AllowPSRemoting | 5986 | TCP | AzureActiveDirectoryDomainServices | Any | Allow |
| 201 | AllowRD | 3389 | TCP | CorpNetSaw | Any | Allow^1^ |
| 65000 | AllVnetInBound | Any | Any | VirtualNetwork | VirtualNetwork | Allow |
| 65001 | AllowAzureLoadBalancerInBound | Any | Any | AzureLoadBalancer | Any | Allow |
| 65500 | DenyAllInBound | Any | Any | Any | Any | Deny |

^1^Optional for debugging but change the default to deny when not needed. Allow the rule when required for advanced troubleshooting.

Note

You may also have a rule that allows inbound traffic if you [configure secure LDAP](tutorial-configure-ldaps). This rule is required for the correct LDAPS communication.

### Outbound security rules

| Priority | Name | Port | Protocol | Source | Destination | Action |
| --- | --- | --- | --- | --- | --- | --- |
| 65000 | AllVnetOutBound | Any | Any | VirtualNetwork | VirtualNetwork | Allow |
| 65001 | AllowAzureLoadBalancerOutBound | Any | Any | Any | Internet | Allow |
| 65500 | DenyAllOutBound | Any | Any | Any | Any | Deny |

Note

Domain Services needs unrestricted outbound access from the virtual network. We don't recommend that you create any other rules that restrict outbound access for the virtual network.

## Verify and edit existing security rules

To verify the existing security rules and make sure the default ports are open, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Network security groups**.
2. Choose the network security group associated with your managed domain, such as *AADDS-contoso.com-NSG*.
3. On the **Overview** page, the existing inbound and outbound security rules are shown.

    Review the inbound and outbound rules and compare to the list of required rules in the previous section. If needed, select and then delete any custom rules that block required traffic. If any of the required rules are missing, add a rule in the next section.

    After you add or delete rules to allow the required traffic, the managed domain's health automatically updates itself within two hours and removes the alert.

### Add a security rule

To add a missing security rule, complete the following steps:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com), search for and select **Network security groups**.
2. Choose the network security group associated with your managed domain, such as *AADDS-contoso.com-NSG*.
3. Under **Settings** in the left-hand panel, select *Inbound security rules* or *Outbound security rules* depending on which rule you need to add.
4. Select **Add**, then create the required rule based on the port, protocol, direction, and so on. When ready, select **OK**.

It takes a few moments for the security rule to be added and show in the list.