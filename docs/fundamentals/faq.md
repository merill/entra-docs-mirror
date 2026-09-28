---
layout: FAQ
title: Frequently asked questions (FAQ) about Microsoft Entra, Microsoft Entra ID, and Azure - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/faq
summary: >
  <p>Microsoft Entra ID is a cloud-based identity and access management solution. It's a directory and identity management service that operates in the cloud and offers authentication and authorization services to various Microsoft services, such as Microsoft 365, Dynamics 365, and Microsoft Azure.</p>

  <p>For more information, see <a href="what-is-entra">What is Microsoft Entra ID?</a></p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Common questions and answers about Microsoft Entra, Microsoft Entra ID and Azure, such as password management and application access.
ms.topic: faq
ms.date: 2025-03-05T00:00:00.0000000Z
ms.custom:
- sfi-ga-nochange
locale: en-us
document_id: 9af66eb7-1320-cd66-7eb8-9715dd1c0b96
document_version_independent_id: 3d40ebea-75cf-a8c1-1f2d-13a2d8704fd6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0638d930-e77e-ffd9-3579-0a17d260f399
---

# Frequently asked questions (FAQ) about Microsoft Entra, Microsoft Entra ID, and Azure - Microsoft Entra | Microsoft Learn

Microsoft Entra ID is a cloud-based identity and access management solution. It's a directory and identity management service that operates in the cloud and offers authentication and authorization services to various Microsoft services, such as Microsoft 365, Dynamics 365, and Microsoft Azure.

For more information, see [What is Microsoft Entra ID?](what-is-entra)

## Help with accessing Microsoft Entra ID and Azure

### Why do I get "No subscriptions found" when I try to access the Microsoft Entra admin center or the Azure portal?

To access the Microsoft Entra admin center or the Azure portal, each user needs permissions with a valid subscription. If you don't have a paid Microsoft 365 or Microsoft Entra subscription, you need to activate a free [Microsoft Entra Account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) or establish a paid subscription. All Azure subscriptions, whether paid or free, have a trust relationship with a Microsoft Entra tenant. All subscriptions rely on the Microsoft Entra tenant (directory) to authenticate and authorize security principals and devices.

For more information, see [How Azure subscriptions are associated with Microsoft Entra ID](how-subscriptions-associated-directory).

### What's the relationship between Microsoft Entra ID, Microsoft Azure, and other Microsoft services, such as Microsoft 365?

Microsoft Entra ID provides you with common identity and access capabilities to all web services. Whether you're using Microsoft services, such as Microsoft 365, Power Platform, Dynamics 365, or other Microsoft products, you're already using Microsoft Entra ID to help turn on sign-on and access management for all cloud services.

All users who are set up to use Microsoft services are defined as user accounts in one or more Microsoft Entra instances, providing these accounts access to Microsoft Entra ID.

For more information, see [Microsoft Entra ID Plans & Pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing)

Microsoft Entra paid services, such as Enterprise Mobility + Security (Microsoft Enterprise Mobility + Security) complement other Microsoft services like Microsoft 365, with comprehensive enterprise-scale development, management, and security solutions.

For more information, see The [Microsoft Cloud](/en-us/microsoft-cloud).

### What are the differences between Owner and Global Administrator?

By default, the person who signs up for a Microsoft Entra or Azure subscription is assigned the Owner role for Azure resources. An Owner can use either a Microsoft account or a work or school account from the directory that the Microsoft Entra or Azure subscription is associated with. This role is also authorized to manage services in the Azure portal.

If others need to sign in and access services by using the same subscription, you can assign them the appropriate [built-in role](/en-us/azure/role-based-access-control/built-in-roles). For more information, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

By default, the user who creates a Microsoft Entra tenant is automatically assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. This user has access to all Microsoft Entra directory features. Microsoft Entra ID has a different set of administrator roles to manage the directory and identity-related features. These administrators have access to various features in the Azure portal. The administrator's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.

For more information, see [Assign a user to administrator roles in Microsoft Entra ID](how-subscriptions-associated-directory) and [Assigning administrator roles in Microsoft Entra ID](../identity/role-based-access-control/permissions-reference).

### Is there a report that shows when my Microsoft Entra user licenses expire?

No. This isn't currently available.

### How can I allow Microsoft Entra admin center URLs on my firewall or proxy server?

To optimize connectivity between your network and the Microsoft Entra admin center and its services, you might want to add specific Microsoft Entra admin center URLs to your allowlist. Doing so can improve performance and connectivity between your local- or wide area network. Network administrators often deploy proxy servers, firewalls, or other devices, which can help secure and give control over how users access the internet. Rules designed to protect users can sometimes block or slow down legitimate business-related internet traffic. This traffic includes communications between you and Microsoft Entra admin center over the following URLs:

- \*.entra.microsoft.com
- \*.entra.microsoft.us
- \*.entra.microsoftonline.cn

For more information, see [Using Microsoft Entra application proxy to publish on-premises apps for remote users](../identity/app-proxy/overview-what-is-app-proxy). Additional URLs that you should include are listed in the article [Allow the Azure portal URLs on your firewall or proxy server](/en-us/azure/azure-portal/azure-portal-safelist-urls).

## Help with hybrid Microsoft Entra ID

### How do I leave a tenant when I'm added as a collaborator?

You can usually leave an organization on your own without having to contact an administrator. However, in some cases this option isn't available and you need to contact your tenant admin, who can delete your account in the external organization.

For more information, see [Leave an organization as an external user](../external-id/leave-the-organization).

### How can I connect my on-premises directory to Microsoft Entra ID?

You can connect your on-premises directory to Microsoft Entra ID by using Microsoft Entra Connect.

For more information, see [Integrating your on-premises identities with Microsoft Entra ID](../identity/hybrid/whatis-hybrid-identity).

### How do I set up SSO between my on-premises directory and my cloud applications?

You only need to set up single sign-on (SSO) between your on-premises directory and Microsoft Entra ID. As long as you access your cloud applications through Microsoft Entra ID, the service automatically drives your users to correctly authenticate with their on-premises credentials.

Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Microsoft Entra Connect configuration wizard.

For more information, see [Integrating your on-premises identities with Microsoft Entra ID](../identity/hybrid/whatis-hybrid-identity).

### Does Microsoft Entra ID provide a self-service portal for users in my organization?

Yes, Microsoft Entra ID provides you with the [Microsoft Entra ID Access Panel](https://myapps.microsoft.com) for user self-service and application access. If you're a Microsoft 365 customer, you can find many of the same capabilities in the [Office 365 portal](https://portal.office.com).

For more information, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

### Does Microsoft Entra ID help me manage my on-premises infrastructure?

Yes. The Microsoft Entra ID P1 or P2 edition provides you with Microsoft Entra Connect Health. Microsoft Entra Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.

For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](../identity/hybrid/connect/whatis-azure-ad-connect).

## Help with password management

### Can I use Microsoft Entra password write-back without password sync?

(For example, is it possible to use Microsoft Entra self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)

This example scenario doesn't require the on-premises password to be tracked in Microsoft Entra. This is because you don't need to synchronize your Active Directory passwords to Microsoft Entra ID to enable write-back. In a federated environment, Microsoft Entra single sign-on (SSO) relies on the on-premises directory to authenticate the user.

### How long does it take for a password to be written back to Active Directory on-premises?

Password write-back operates in real time.

For more information, see [Getting started with password management](../identity/authentication/tutorial-enable-sspr).

### Can I use password write-back with passwords that are managed by an admin?

Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.

For more answers to password-related questions, see [Password management frequently asked questions](../identity/authentication/passwords-faq).

### What can I do if I can't remember my existing Microsoft 365 / Microsoft Entra password while trying to change my password?

There are a couple of options. You can use the self-service password reset (SSPR) if it's available. Whether SSPR works depends on how it's configured. For more information about resetting Microsoft Entra passwords, see [How does the password reset portal work](../identity/authentication/howto-sspr-deployment).

For Microsoft 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&amp;rs=en-US&amp;ad=US).

For Microsoft Entra accounts, admins can reset passwords by using one of the following:

- [Reset a user's password using Microsoft Entra ID](users-reset-password-azure-portal)
- [Reset a password using PowerShell](/en-us/powershell/module/microsoft.graph.identity.signins/reset-mguserauthenticationmethodpassword)

## Help with security

### Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?

Microsoft Entra ID uses a more sophisticated strategy to lock accounts. This is based on the IP of the request and the passwords entered. The duration of the lockout also increases based on the likelihood that it's an attack.

### For certain (common) passwords that get rejected, does this apply to passwords used only in the current directory?

Rejected passwords return the message 'This password has been used too many times'. This refers to passwords that are globally common, such as any variants of "Password" and "123456".

### Will sign-in requests from dubious sources (botnets, for example) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?

We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.

## Help with application access

### Where can I find a list of applications that are pre-integrated with Microsoft Entra ID and their capabilities?

Microsoft Entra ID has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners. All pre-integrated applications support single sign-on (SSO). SSO lets you use your organizational credentials to access your apps. Some of the applications also support automated provisioning and de-provisioning.

For a complete list of the pre-integrated applications, see the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActiveDirectory).

### What if the application I need is not in the Microsoft Entra marketplace?

With Microsoft Entra ID P1 or P2, you can add and configure any application that you want. Depending on your application's capabilities and your preferences, you can configure SSO and automated provisioning.

For more information, see [Single sign-on SAML protocol](../identity-platform/single-sign-on-saml-protocol) and [Develop and plan provisioning for a SCIM endpoint](../identity/app-provisioning/use-scim-to-provision-users-and-groups).

### How do users sign in to applications using Microsoft Entra ID?

Microsoft Entra ID provides several ways for users to view and access their applications, such as:

- The [Microsoft Entra access panel](https://entra.microsoft.com/#home)
- The Microsoft 365 application launcher
- Direct sign-in to federated apps
- Deep links to federated, password-based, or existing apps

For more information, see [End user experiences for applications](../identity/enterprise-apps/end-user-experiences).

### What are the different ways Microsoft Entra ID enables authentication and single sign-on to applications?

Microsoft Entra ID supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation. Microsoft Entra ID also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.

For more information, see [Identity fundamentals](identity-fundamental-concepts) and [Single sign-on for applications in Microsoft Entra ID](../identity/enterprise-apps/what-is-single-sign-on).

### Can I add applications that I'm running on-premises?

[Microsoft Entra application proxy](/en-us/entra/identity/app-proxy) provides you with easy and secure access to on-premises web applications that you choose. You can access these applications in the same way that you access your software as a service (SaaS) apps in Microsoft Entra ID. There's no need for a VPN or to change your network infrastructure.

For more information, see [How to provide secure remote access to on-premises applications](/en-us/entra/identity/app-proxy).

### How do I require multifactor authentication for users who access a particular application?

With [Microsoft Entra Conditional Access](../identity/conditional-access/overview), you can assign a unique access policy for each application. In your policy, you can require multifactor authentication always, or when users aren't connected to the local network.

For more information, see [Securing access to Microsoft 365 and other apps connected to Microsoft Entra ID](../identity/conditional-access/overview).

### What is automated user provisioning for SaaS apps?

Use Microsoft Entra ID to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.

For more information, see [What is app provisioning in Microsoft Entra ID?](../identity/app-provisioning/user-provisioning).

### Can I set up a secure LDAP connection with Microsoft Entra ID?

No. Microsoft Entra ID doesn't support the Lightweight Directory Access Protocol (LDAP) protocol or Secure LDAP directly. However, it's possible to enable Microsoft Entra Domain Services instance on your Microsoft Entra tenant with properly configured network security groups through Azure Networking to achieve LDAP connectivity.

For more information, see [Configure secure LDAP for a Microsoft Entra Domain Services managed domain](/en-us/entra/identity/domain-services/tutorial-configure-ldaps).