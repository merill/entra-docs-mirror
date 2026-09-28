---
layout: FAQ
title: Frequently asked questions about Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/faqs
summary: >
  <p>This page answers frequently asked questions about Microsoft Entra Domain Services.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Read and understand some of the frequently asked questions around configuration, administration, and availability for Microsoft Entra Domain Services
services: active-directory-ds
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.topic: faq
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 1ac3ceff-f36d-91b3-c722-a7a280cc17c4
document_version_independent_id: 32420f48-3d50-1e20-a994-66230dc3a00f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/faqs.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/faqs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/faqs.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e7ce5e46-811d-9038-412b-2cfb8ca79b26
---

# Frequently asked questions about Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

This page answers frequently asked questions about Microsoft Entra Domain Services.

## Configuration

### Can I create multiple managed domains for a single Microsoft Entra directory?

No. You can only create a single managed domain serviced by Microsoft Entra Domain Services for a single Microsoft Entra directory.

### Can I enable Microsoft Entra Domain Services in a Classic virtual network?

Classic virtual networks aren't supported.

For more information, see the [official deprecation notice](https://azure.microsoft.com/updates/we-are-retiring-azure-ad-domain-services-classic-vnet-support-on-march-1-2023/).

### Can I enable Microsoft Entra Domain Services in an Azure Resource Manager virtual network?

Yes. Microsoft Entra Domain Services can be enabled in an Azure Resource Manager virtual network. Classic Azure virtual networks are no longer available when you create a managed domain.

### Can I enable Microsoft Entra Domain Services in an Azure CSP (Cloud Solution Provider) subscription?

Yes. For more information, see [how to enable Microsoft Entra Domain Services in Azure CSP subscriptions](csp).

### Can I make Microsoft Entra Domain Services available in multiple virtual networks within my subscription?

The service itself doesn't directly support this scenario. Your managed domain is available in only one virtual network at a time. However, you can configure connectivity between multiple virtual networks to expose Microsoft Entra Domain Services to other virtual networks. For more information, see [how to connect virtual networks in Azure using VPN gateways](/en-us/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-portal-classic) or [virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview).

### Can I add domain controllers to a Microsoft Entra Domain Services managed domain?

No. The domain provided by Microsoft Entra Domain Services is a managed domain. You don't need to provision, configure, or otherwise manage domain controllers for this domain. These management activities are provided as a service by Microsoft. Therefore, you can't add more domain controllers (read-write or read-only) for the managed domain.

### Can I expand a managed domain to different Azure regions for application recovery if an Azure region goes offline?

Yes. You can create replica sets that share the same namespace and configuration with your managed domain. Replica sets can be added to any peered virtual network in any Azure region that supports Domain Services. For more information, see [Replica sets concepts and features for Microsoft Entra Domain Services](concepts-replica-sets).

### Can I enable Microsoft Entra Domain Services in a federated Microsoft Entra directory without password hash synchronization?

No. To authenticate users via NTLM or Kerberos, Microsoft Entra Domain Services needs access to the password hashes of user accounts. In a federated directory, password hashes aren't stored in the Microsoft Entra directory. Therefore, Microsoft Entra Domain Services doesn't work with such Microsoft Entra directories.

However, if you're using Microsoft Entra Connect for password hash synchronization, you can use Microsoft Entra Domain Services because the password hash values are stored in Microsoft Entra ID.

### Can I enable Microsoft Entra Domain Services using PowerShell?

Yes. For more information, see [how to enable Microsoft Entra Domain Services using PowerShell](powershell-create-instance).

### Can I enable Microsoft Entra Domain Services using a Resource Manager Template?

Yes, you can create a Microsoft Entra Domain Services managed domain using a Resource Manager template. A service principal and a Microsoft Entra group for administration must be created using the Microsoft Entra admin center or PowerShell before the template is deployed. When you create a Microsoft Entra Domain Services managed domain in the Microsoft Entra admin center, there's also an option to export the template for use with other deployments. For more information, see [Create a Domain Services managed domain using an Azure Resource Manager template](template-create-instance).

### Can guest users who are invited to my directory use Microsoft Entra Domain Services?

No. Guest users invited to your Microsoft Entra directory using the [Microsoft Entra B2B](/en-us/azure/active-directory/external-identities/what-is-b2b) invite process are synchronized into your Microsoft Entra Domain Services managed domain. However, passwords for these users aren't stored in your Microsoft Entra directory. Therefore, Microsoft Entra Domain Services has no way to synchronize NTLM and Kerberos hashes for these users into your managed domain. Such users can't sign in or join computers to the managed domain.

### Can a two-way forest trust be created between Domain Services and an on-premises forest?

Yes, you can create a two-way trust. You can also create a one-way outgoing trust or one-way incoming trust to support different scenarios for users authentication and access. For more information, see [Create a forest trust](tutorial-create-forest-trust).

### Does Domain Services support external trust creation with an on-premises child domains?

Domain Services currently only supports forest trust, and doesn't support external domain trusts.

### Can I move a managed domain?

After you create a Domain Services managed domain, you can't move it to a different subscription, resource group, or region. To change the region, a possible workaround would be deploying a new replica set in the region that you want to migrate to. Once that completes, delete the replica set in the region you don't want any more. As a workaround for the rest of the settings, you can [delete the managed domain](delete-aadds) by using PowerShell or the Microsoft Entra admin center and re-create it with your desired setup. No restore operations can be provided while the managed domain is re-created.

### Can I rename an existing Microsoft Entra Domain Services domain name?

No. After you create a Microsoft Entra Domain Services managed domain, you can't change the DNS domain name. Choose the DNS domain name carefully when you create the managed domain. For considerations when you choose the DNS domain name, see the [tutorial to create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance#create-a-managed-domain).

### Does Microsoft Entra Domain Services include high availability options?

Yes. Each Microsoft Entra Domain Services managed domain includes two domain controllers. You don't manage or connect to these domain controllers, they're part of the managed service. If you deploy Microsoft Entra Domain Services into a region that supports Availability Zones, the domain controllers are distributed across zones. In regions that don't support Availability Zones, the domain controllers are distributed across Availability Sets. You have no configuration options or management control over this distribution. For more information, see [Availability options for virtual machines in Azure](/en-us/azure/virtual-machines/availability).

## Administration and operations

### Can I connect to the domain controller for my managed domain using Remote Desktop?

No. You don't have permissions to connect to domain controllers for the managed domain using Remote Desktop. Members of the *Microsoft Entra DC Administrators* group can administer the managed domain using AD administration tools such as the Active Directory Administration Center (ADAC) or AD PowerShell. These tools are installed using the *Remote Server Administration Tools* feature on a Windows server joined to the managed domain. For more information, see [Create a management VM to configure and administer a Microsoft Entra Domain Services managed domain](tutorial-create-management-vm).

### I've enabled Microsoft Entra Domain Services. What user account do I use to domain join machines to this domain?

Any user account that's part of the managed domain can join a VM. Members of the *Microsoft Entra DC Administrators* group are granted remote desktop access to machines that have been joined to the managed domain.

### Is there any quota for the number of machines that I can join to the domain?

There's no quota in Domain Services for domain-joined machines.

### How is time synchronized for virtual machines (VMs) that are joined to a managed domain?

VMs that run on Azure are synchronized with Azure hosts for highly accurate time. Non-Azure VMs that run on premises need to have Windows Time Services configured for synchronization with an external NTP time source, similarly to domain-joined VMs. For more information, see [Configure the time mechanism for Active Directory Windows Virtual Machines in Azure](/en-us/azure/virtual-machines/windows/external-ntpsource-configuration).

### Do I have domain administrator privileges for the managed domain provided by Microsoft Entra Domain Services?

No. You aren't granted administrative privileges on the managed domain. *Domain Administrator* and *Enterprise Administrator* privileges aren't available for you to use within the domain. Members of the domain administrator or enterprise administrator groups in your on-premises Active Directory are also not granted domain / enterprise administrator privileges on the managed domain.

### Can I modify group memberships using LDAP or other AD administrative tools on managed domains?

Users and groups that are synchronized from Microsoft Entra ID to Microsoft Entra Domain Services can't be modified because their source of origin is Microsoft Entra ID. This includes moving users or groups from the **AADDC Users** managed organizational unit to a custom organizational unit. Any user or group originating in the managed domain may be modified.

### Can I authorize a DHCP server in a managed domain?

No. Domain Admins membership is required to authorize a DHCP server, which isn't available in a managed domain.

### How long does it take for changes I make to my Microsoft Entra directory to be visible in my managed domain?

Changes made in your Microsoft Entra directory using either the Microsoft Entra UI or PowerShell are automatically synchronized to your managed domain. This synchronization process runs in the background. There's no defined time period for this synchronization to complete all the object changes.

### Can I extend the schema of the managed domain provided by Microsoft Entra Domain Services?

No. The schema is administered by Microsoft for the managed domain. Schema extensions aren't supported by Microsoft Entra Domain Services.

### Can I modify or add DNS records in my managed domain?

Yes. Members of the *Microsoft Entra DC Administrators* group are granted *DNS Administrator* privileges to modify DNS records in the managed domain. Those users can use the DNS Manager console on a machine running Windows Server joined to the managed domain to manage DNS. To use the DNS Manager console, install *DNS Server Tools*, which are part of the *Remote Server Administration Tools* optional feature on the server. For more information, see [Administer DNS in a Microsoft Entra Domain Services managed domain](manage-dns).

### What is the password lifetime policy on a managed domain?

The default password lifetime on a Microsoft Entra Domain Services managed domain is 90 days. This password lifetime isn't synchronized with the password lifetime configured in Microsoft Entra ID. Therefore, you may have a situation where users' passwords expire in your managed domain, but are still valid in Microsoft Entra ID. In such scenarios, users need to change their password in Microsoft Entra ID and the new password will synchronize to your managed domain. If you want to change the default password lifetime in a managed domain, you can [create and configure custom password policies](password-policy).

Additionally, the Microsoft Entra password policy for *DisablePasswordExpiration* is synchronized to a managed domain. When *DisablePasswordExpiration* is applied to a user in Microsoft Entra ID, the *UserAccountControl* value for the synchronized user in the managed domain has *DONT\_EXPIRE\_PASSWORD* applied.

When users reset their password in Microsoft Entra ID, the *forceChangePasswordNextSignIn=True* attribute is applied. A managed domain synchronizes this attribute from Microsoft Entra ID. When the managed domain detects *forceChangePasswordNextSignIn* is set for a synchronized user from Microsoft Entra ID, the *pwdLastSet* attribute in the managed domain is set to *0*, which invalidates the currently set password.

### Does Microsoft Entra Domain Services provide AD account lockout protection?

Yes. Five invalid password attempts within 2 minutes on the managed domain cause a user account to be locked out for 30 minutes. After 30 minutes, the user account is automatically unlocked. Invalid password attempts on the managed domain don't lock out the user account in Microsoft Entra ID. The user account is locked out only within your Microsoft Entra Domain Services managed domain. For more information, see [Password and account lockout policies on managed domains](password-policy).

### Can I configure Distributed File System and replication within Microsoft Entra Domain Services?

No. Distributed File System (DFS) and replication aren't available when using Microsoft Entra Domain Services.

### How are Windows Updates applied in Microsoft Entra Domain Services?

Domain controllers in a managed domain automatically apply required Windows updates. There's nothing for you to configure or administer here. Make sure you don't create network security group rules that block outbound traffic to Windows Updates. For your own VMs joined to the managed domain, you are responsible for configuring and applying any required OS and application updates.

### Should I remove the AzureUpdateDelivery and AzureFrontDoor.FirstParty tags in the outbound network security group (NSG)?

With the deprecation of AzureUpdateDelivery and AzureFrontDoor.FirstParty tags, Microsoft Entra Domain Services manages WindowsUpdate independently, which removes the need for these tags. NSG adjustments aren't needed, with or without deprecated tags.

### Where does Microsoft Entra Domain Services store customer data?

Microsoft Entra Domain Services stores customer data. By default, customer data stays within the region where the service instance is deployed. Customers can use replica sets to store data in other regions.

### How is patching performed on domain controllers that are part of a managed domain?

Patches are installed as soon as they become available (every second Tuesday). They are installed in phases during the week they become available, starting on Tuesdays.

### Why do my domain controllers change names?

It's possible that during the maintenance of domain controllers, there is a change in their names. To avoid problems with this type of change, it's recommended to not use the names of the domain controllers hardcoded in applications and/or other domain resources, but the FQDN of the domain. This way, no matter what the names of the domain controllers are, you won't need to reconfigure anything after a name change.

### Is the password of the KRBTGT account in a managed domain rolled periodically? If so, what is the frequency?

The password of the KRBTGT account in a managed domain is rolled over every seven (7) days.

## Billing and availability

### Is Microsoft Entra Domain Services a paid service?

Yes. For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/active-directory-ds/).

### Is there a free trial for the service?

Microsoft Entra Domain Services is included in the free trial for Azure. You can sign up for a [free one-month trial of Azure](https://azure.microsoft.com/pricing/free-trial/).

### Can I pause a Microsoft Entra Domain Services managed domain?

No. Once you've enabled a Microsoft Entra Domain Services managed domain, the service is available within your selected virtual network until you delete the managed domain. There's no way to pause the service. Billing continues on an hourly basis until you delete the managed domain.

### Can I fail over Microsoft Entra Domain Services to another region for a DR event?

Yes, to provide geographical resiliency for a managed domain, you can create another [replica set](tutorial-create-replica-set) to a peered virtual network in any Azure region that supports Domain Services. Replica sets share the same namespace and configuration with the managed domain.

### Can I get Microsoft Entra Domain Services as part of Enterprise Mobility Suite (EMS)? Do I need Microsoft Entra ID P1 or P2 to use Microsoft Entra Domain Services?

No. Microsoft Entra Domain Services is a pay-as-you-go Azure service and isn't part of EMS. Microsoft Entra Domain Services can be used with all editions of Microsoft Entra ID (Free and Premium). You're billed on an hourly basis, depending on usage.

### Can I create a child domain under a managed domain?

No. Microsoft Entra Domain Services has a single-domain, single-forest design, and you can't create child domains.

### Which Azure regions have the service available?

Refer to the [Azure Services by region](https://azure.microsoft.com/regions/#services/) page to see a list of the Azure regions where Microsoft Entra Domain Services is available.

## Troubleshooting

Refer to the [Troubleshooting guide](troubleshoot) for solutions to common issues with configuring or administering Azure AD Domain Services.