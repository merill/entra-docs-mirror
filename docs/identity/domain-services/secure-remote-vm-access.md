---
layout: Conceptual
title: Secure remote VM access in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/secure-remote-vm-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to secure remote access to VMs using Network Policy Server (NPS) and Microsoft Entra multifactor authentication with a Remote Desktop Services deployment in a Microsoft Entra Domain Services managed domain.
ms.topic: how-to
ms.date: 2025-02-05T00:00:00.0000000Z
locale: en-us
document_id: 4d6043ab-49fa-d157-df04-0fc4bbfa7a39
document_version_independent_id: c55fca2a-8376-1f4a-2133-8da7e682ff31
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/secure-remote-vm-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/secure-remote-vm-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/secure-remote-vm-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7c01134-b8f3-438c-822d-13471e513908
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/82fff6b2-939d-4e9a-8f9c-d1c41a59749b
platformId: 1189d117-103a-5b48-184c-9fb5b4678529
---

# Secure remote VM access in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

To secure remote access to virtual machines (VMs) that run in a Microsoft Entra Domain Services managed domain, you can use Remote Desktop Services (RDS) and Network Policy Server (NPS). Domain Services authenticates users as they request access through the RDS environment. For enhanced security, you can integrate Microsoft Entra multifactor authentication to provide another authentication prompt during sign-in events. Microsoft Entra multifactor authentication uses an extension for NPS to provide this feature.

Important

The recommended way to securely connect to your VMs in a Domain Services managed domain is using Azure Bastion, a fully platform-managed PaaS service that you provision inside your virtual network. A bastion host provides secure and seamless Remote Desktop Protocol (RDP) connectivity to your VMs directly in the Azure portal over SSL. When you connect via a bastion host, your VMs don't need a public IP address, and you don't need to use network security groups to expose access to RDP on TCP port 3389.

We strongly recommend that you use Azure Bastion in all regions where it's supported. In regions without Azure Bastion availability, follow the steps detailed in this article until Azure Bastion is available. Take care with assigning public IP addresses to VMs joined to Domain Services where all incoming RDP traffic is allowed.

For more information, see [What is Azure Bastion?](/en-us/azure/bastion/bastion-overview).

This article shows you how to configure RDS in Domain Services and optionally use the Microsoft Entra multifactor authentication NPS extension.

![Remote Desktop Services (RDS) overview](media/enable-network-policy-server/remote-desktop-services-overview.png)

## Prerequisites

To complete this article, you need the following resources:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
- A *workloads*subnet created in your Microsoft Entra Domain Services virtual network.
    - If needed, [Configure virtual networking for a Microsoft Entra Domain Services managed domain](tutorial-configure-networking).
- A user account that's a member of the *AAD DC administrators* group in your Microsoft Entra tenant.

## Deploy and configure the Remote Desktop environment

To get started, create a minimum of two Azure VMs that run Windows Server 2016 or Windows Server 2019. For redundancy and high availability of your Remote Desktop (RD) environment, you can add and load balance hosts later.

A suggested RDS deployment includes the following two VMs:

- *RDGVM01* - Runs the RD Connection Broker server, RD Web Access server, and RD Gateway server.
- *RDSHVM01* - Runs the RD Session Host server.

Make sure that VMs are deployed into a *workloads* subnet of your Domain Services virtual network, then join the VMs to managed domain. For more information, see how to [create and join a Windows Server VM to a managed domain](join-windows-vm).

The RD environment deployment contains a number of steps. The existing RD deployment guide can be used without any specific changes to use in a managed domain:

1. Sign in to VMs created for the RD environment with an account that's part of the *AAD DC Administrators* group, such as *contosoadmin*.
2. To create and configure RDS, use the existing [Remote Desktop environment deployment guide](/en-us/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure). Distribute the RD server components across your Azure VMs as desired.
    - Specific to Domain Services - when you configure RD licensing, set it to **Per Device** mode, not **Per User** as noted in the deployment guide.
3. If you want to provide access using a web browser, [set up the Remote Desktop web client for your users](/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-web-client-admin).

With RD deployed into the managed domain, you can manage and use the service as you would with an on-premises AD DS domain.

## Deploy and configure NPS and the Microsoft Entra multifactor authentication NPS extension

If you want to increase the security of the user sign-in experience, you can optionally integrate the RD environment with Microsoft Entra multifactor authentication. With this configuration, users receive another prompt during sign-in to confirm their identity.

To provide this capability, a Network Policy Server (NPS) is installed in your environment along with the Microsoft Entra multifactor authentication NPS extension. This extension integrates with Microsoft Entra ID to request and return the status of multifactor authentication prompts.

Users must be [registered to use Microsoft Entra multifactor authentication](/en-us/azure/active-directory/authentication/howto-mfa-nps-extension#register-users-for-mfa), which may require other Microsoft Entra ID licenses. For more information, see [Microsoft Entra Plans & Pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing).

To integrate Microsoft Entra multifactor authentication in to your Remote Desktop environment, create an NPS Server and install the extension:

1. Create another Windows Server 2016 or 2019 VM, such as *NPSVM01*, that's connected to a *workloads* subnet in your Domain Services virtual network. Join the VM to the managed domain.
2. Sign in to NPS VM as account that's part of the *AAD DC Administrators* group, such as *contosoadmin*.
3. From **Server Manager**, select **Add Roles and Features**, then install the *Network Policy and Access Services* role.
4. Delegate Full Control permission of the RAS and IAS Servers group to the **AAD DC Administrators** group. This step is needed for NPS or Radius server setup.
5. Use the existing how-to article to [install and configure the Microsoft Entra multifactor authentication NPS extension](/en-us/azure/active-directory/authentication/howto-mfa-nps-extension).

With the NPS server and Microsoft Entra multifactor authentication NPS extension installed, complete the next section to configure it for use with the RD environment.

## Integrate Remote Desktop Gateway and Microsoft Entra multifactor authentication

To integrate the Microsoft Entra multifactor authentication NPS extension, use the existing how-to article to [integrate your Remote Desktop Gateway infrastructure using the Network Policy Server (NPS) extension and Microsoft Entra ID](/en-us/azure/active-directory/authentication/howto-mfa-nps-extension-rdg).

The following configuration options are needed to integrate with a managed domain:

1. Don't [register the NPS server in Active Directory](/en-us/azure/active-directory/authentication/howto-mfa-nps-extension-rdg#register-server-in-active-directory). This step fails in a managed domain.
2. In [step 4 to configure network policy](/en-us/azure/active-directory/authentication/howto-mfa-nps-extension-rdg#configure-network-policy), also check the box to **Ignore user account dial-in properties**.
3. If you use Windows Server 2019 or later for the NPS server and Microsoft Entra multifactor authentication NPS extension, run the following command to update the secure channel to allow the NPS server to communicate correctly:

    ```powershell
    sc sidtype IAS unrestricted
    ```

Users are now prompted for another authentication factor when they sign in, such as a text message or prompt in the Microsoft Authenticator app.