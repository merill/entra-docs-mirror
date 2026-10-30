---
layout: Conceptual
title: Kerberos constrained delegation for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/deploy-kcd
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to enable resource-based Kerberos constrained delegation (KCD) in a Microsoft Entra Domain Services managed domain.
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.topic: how-to
ms.date: 2025-01-21T00:00:00.0000000Z
locale: en-us
document_id: 1d8f9d8f-cfa2-1d9e-1f13-3888ebf1a4fa
document_version_independent_id: 09af4392-a4a5-c4fb-f04e-f63074750051
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/deploy-kcd.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/deploy-kcd
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/deploy-kcd.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 274e2c87-ce93-755a-085e-a55e3cd086b5
---

# Kerberos constrained delegation for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

As you run applications, there may be a need for those applications to access resources in the context of a different user. Active Directory Domain Services (AD DS) supports a mechanism called *Kerberos delegation* that enables this use-case. Kerberos *constrained* delegation (KCD) then builds on this mechanism to define specific resources that can be accessed in the context of the user.

Microsoft Entra Domain Services managed domains are more securely locked down than traditional on-premises AD DS environments, so use a more secure *resource-based* KCD.

This article shows you how to configure resource-based Kerberos constrained delegation in a Domain Services managed domain.

## Prerequisites

To complete this article, you need the following resources:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
- A Windows Server management VM that is joined to the Domain Services managed domain.
    - If needed, complete the tutorial to [create a Windows Server VM and join it to a managed domain](join-windows-vm) then [install the AD DS management tools](tutorial-create-management-vm).
- A user account that's a member of the *Microsoft Entra DC administrators* group in your Microsoft Entra tenant.

## Kerberos constrained delegation overview

Kerberos delegation lets one account impersonate another account to access resources. For example, a web application that accesses a back-end web component can impersonate itself as a different user account when it makes the back-end connection. Kerberos delegation is insecure as it doesn't limit what resources the impersonating account can access.

Kerberos *constrained* delegation (KCD) restricts the services or resources that a specified server or application can connect when impersonating another identity. Traditional KCD requires domain administrator privileges to configure a domain account for a service, and it restricts the account to run on a single domain.

Traditional KCD also has a few issues. For example, in earlier operating systems, the service administrator had no useful way to know which front-end services delegated to the resource services they owned. Any front-end service that could delegate to a resource service was a potential attack point. If a server that hosted a front-end service configured to delegate to resource services was compromised, the resource services could also be compromised.

In a managed domain, you don't have domain administrator privileges. As a result, traditional account-based KCD can't be configured in a managed domain. Resource-based KCD can instead be used, which is also more secure.

### Resource-based KCD

Windows Server 2012 and later gives service administrators the ability to configure constrained delegation for their service. This model is known as resource-based KCD. With this approach, the back-end service administrator can allow or deny specific front-end services from using KCD.

Resource-based KCD is configured using PowerShell. You use the [Set-ADComputer](/en-us/powershell/module/activedirectory/set-adcomputer) or [Set-ADUser](/en-us/powershell/module/activedirectory/set-aduser) cmdlets, depending on whether the impersonating account is a computer account or a user account / service account.

## Configure resource-based KCD for a computer account

In this scenario, let's assume you have a web app that runs on the computer named *contoso-webapp.aaddscontoso.com*.

The web app needs to access a web API that runs on the computer named *contoso-api.aaddscontoso.com* in the context of domain users.

Complete the following steps to configure this scenario:

1. [Create a custom OU](create-ou). You can delegate permissions to manage this custom OU to users within the managed domain.
2. [Domain-join the virtual machines](join-windows-vm), both the one that runs the web app, and the one that runs the web API, to the managed domain. Create these computer accounts in the custom OU from the previous step.

    Note

    The computer accounts for the web app and the web API must be in a custom OU where you have permissions to configure resource-based KCD. You can't configure resource-based KCD for a computer account in the built-in *Microsoft Entra DC Computers* container.
3. Finally, configure resource-based KCD using the [Set-ADComputer](/en-us/powershell/module/activedirectory/set-adcomputer) PowerShell cmdlet.

    From your domain-joined management VM and logged in as user account that's a member of the *Microsoft Entra DC administrators* group, run the following cmdlets. Provide your own computer names as needed:

    ```powershell
    $ImpersonatingAccount = Get-ADComputer -Identity contoso-webapp.aaddscontoso.com
    Set-ADComputer contoso-api.aaddscontoso.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
    ```

## Configure resource-based KCD for a user account

In this scenario, let's assume you have a web app that runs as a service account named *appsvc*. The web app needs to access a web API that runs as a service account named *backendsvc* in the context of domain users. Complete the following steps to configure this scenario:

1. [Create a custom OU](create-ou). You can delegate permissions to manage this custom OU to users within the managed domain.
2. [Domain-join the virtual machines](join-windows-vm) that run the backend web API/resource to the managed domain. Create its computer account within the custom OU.
3. Create the service account (for example, *appsvc*) used to run the web app within the custom OU.

    Note

    Again, the computer account for the web API VM, and the service account for the web app, must be in a custom OU where you have permissions to configure resource-based KCD. You can't configure resource-based KCD for accounts in the built-in *Microsoft Entra DC Computers* or *Microsoft Entra DC Users* containers. This also means that you can't use user accounts synchronized from Microsoft Entra ID to set up resource-based KCD. You must create and use service accounts specifically created in Domain Services.
4. Finally, configure resource-based KCD using the [Set-ADUser](/en-us/powershell/module/activedirectory/set-aduser) PowerShell cmdlet.

    From your domain-joined management VM and logged in as user account that's a member of the *Microsoft Entra DC administrators* group, run the following cmdlets. Provide your own service names as needed:

    ```powershell
    $ImpersonatingAccount = Get-ADUser -Identity appsvc
    Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
    ```