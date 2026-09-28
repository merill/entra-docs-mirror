---
layout: Conceptual
title: Deploy Microsoft Entra application proxy for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/deploy-azure-app-proxy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to provide secure access to internal applications for remote workers by deploying and configuring Microsoft Entra application proxy in a Microsoft Entra Domain Services managed domain
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: fc350ba1-81d0-e336-c0e0-e644c18af5f7
document_version_independent_id: a7268bd1-ac11-a044-eaea-59a842136f99
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/deploy-azure-app-proxy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/deploy-azure-app-proxy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/deploy-azure-app-proxy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 96836a92-0290-b15a-e887-477634cb7127
---

# Deploy Microsoft Entra application proxy for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

With Microsoft Entra Domain Services, you can lift-and-shift legacy applications running on-premises into Azure. Microsoft Entra application proxy then helps you support remote workers by securely publishing those internal applications part of a Domain Services managed domain so they can be accessed over the internet.

If you're new to the Microsoft Entra application proxy and want to learn more, see [How to provide secure remote access to internal applications](deploy-azure-app-proxy).

This article shows you how to create and configure a Microsoft Entra private network connector to provide secure access to applications in a managed domain.

## Before you begin

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
    - A **Microsoft Entra ID P1 or P2 license** is required to use the Microsoft Entra application proxy.
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).

## Create a domain-joined Windows VM

To route traffic to applications running in your environment, you install the Microsoft Entra private network connector component. This Microsoft Entra private network connector must be installed on a Windows Server virtual machine (VM) that's joined to the managed domain. For some applications, you can deploy multiple servers that each have the connector installed. This deployment option gives you greater availability and helps handle heavier authentication loads.

The VM that runs the Microsoft Entra private network connector must be on the same, or a peered, virtual network as your managed domain. The VMs that then host the applications you publish using the Application Proxy must also be deployed on the same Azure virtual network.

To create a VM for the Microsoft Entra private network connector, complete the following steps:

1. [Create a custom OU](create-ou). You can delegate permissions to manage this custom OU to users within the managed domain. The VMs for Microsoft Entra application proxy and that run your applications must be a part of the custom OU, not the default *Microsoft Entra DC Computers* OU.
2. [Domain-join the virtual machines](join-windows-vm), both the one that runs the Microsoft Entra private network connector, and the ones that run your applications, to the managed domain. Create these computer accounts in the custom OU from the previous step.

## Download the Microsoft Entra private network connector

Perform the following steps to download the Microsoft Entra private network connector. The setup file you download is copied to your application proxy VM in the next section.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Search for and select **Enterprise applications**.
3. Select **Application proxy** from the menu on the left-hand side. To create your first connector and enable application proxy, select the link to **download a connector**.
4. On the download page, accept the license terms and privacy agreement, then select **Accept terms & Download**.

    ![Download the Microsoft Entra private network connector](media/app-proxy/download-app-proxy-connector.png)

## Install and register the Microsoft Entra private network connector

With a VM ready to be used as the Microsoft Entra private network connector, now copy and run the setup file downloaded from the Microsoft Entra admin center.

1. Copy the Microsoft Entra private network connector setup file to your VM.
2. Run the setup file, such as *MicrosoftEntraPrivateNetworkConnectorInstaller.exe*. Accept the software license terms.
3. During the install, you're prompted to register the connector with the Application Proxy in your Microsoft Entra directory.

    Note

    The account used to register the connector must belong to the same directory where you enable the Application Proxy service.

    For example, if the Microsoft Entra domain is *contoso.com*, the account should be `admin@contoso.com` or another valid alias on that domain.

    - If Internet Explorer Enhanced Security Configuration is turned on for the VM where you install the connector, the registration screen might be blocked. To allow access, follow the instructions in the error message, or turn off Internet Explorer Enhanced Security during the install process.
    - If connector registration fails, see [Troubleshoot Application Proxy](/en-us/azure/active-directory/app-proxy/application-proxy-troubleshoot).
4. At the end of the setup, a note is shown for environments with an outbound proxy. To configure the Microsoft Entra private network connector to work through the outbound proxy, run the provided script, such as `C:\Program Files\Microsoft Entra private network connector\ConfigureOutBoundProxy.ps1`.
5. On the Application proxy page in the Microsoft Entra admin center, the new connector is listed with a status of *Active*, as shown in the following example:

    ![The new Microsoft Entra private network connector shown as active in the Microsoft Entra admin center](media/app-proxy/connected-app-proxy.png)

Note

To provide high availability for applications authenticating through the Microsoft Entra application proxy, you can install connectors on multiple VMs. Repeat the same steps listed in the previous section to install the connector on other servers joined to the managed domain.

## Enable resource-based Kerberos constrained delegation

If you want to use single sign-on to your applications using integrated Windows authentication (IWA), grant the Microsoft Entra private network connectors permission to impersonate users and send and receive tokens on their behalf. To grant these permissions, you configure Kerberos constrained delegation (KCD) for the connector to access resources on the managed domain. As you don't have domain administrator privileges in a managed domain, traditional account-level KCD cannot be configured on a managed domain. Instead, use resource-based KCD.

For more information, see [Configure Kerberos constrained delegation (KCD) in Microsoft Entra Domain Services](deploy-kcd).

Note

You must be signed in to a user account that's a member of the *Microsoft Entra DC administrators* group in your Microsoft Entra tenant to run the following PowerShell cmdlets.

The computer accounts for your private network connector VM and application VMs must be in a custom OU where you have permissions to configure resource-based KCD. You can't configure resource-based KCD for a computer account in the built-in *Microsoft Entra DC Computers* container.

Use the [Get-ADComputer](/en-us/powershell/module/activedirectory/get-adcomputer) to retrieve the settings for the computer on which the Microsoft Entra private network connector is installed. From your domain-joined management VM and logged in as user account that's a member of the *Microsoft Entra DC administrators* group, run the following cmdlets.

The following example gets information about the computer account named *appproxy.aaddscontoso.com*. Provide your own computer name for the Microsoft Entra application proxy VM configured in the previous steps.

```powershell
$ImpersonatingAccount = Get-ADComputer -Identity appproxy.aaddscontoso.com
```

For each application server that runs the apps behind Microsoft Entra application proxy use the [Set-ADComputer](/en-us/powershell/module/activedirectory/set-adcomputer) PowerShell cmdlet to configure resource-based KCD. In the following example, the Microsoft Entra private network connector is granted permissions to use the *appserver.aaddscontoso.com* computer:

```powershell
Set-ADComputer appserver.aaddscontoso.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

If you deploy multiple Microsoft Entra private network connectors, you must configure resource-based KCD for each connector instance.