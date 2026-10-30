---
layout: Conceptual
title: How SSO to on-premises resources works on Microsoft Entra joined devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/device-sso-to-on-premises-resources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Extend the SSO experience by configuring Microsoft Entra hybrid joined devices.
ms.topic: concept-article
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: 
locale: en-us
document_id: 0d912434-0693-e158-f371-51b010f8a533
document_version_independent_id: 51892e2c-8bd5-df84-28a1-548bbf0d8d96
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/device-sso-to-on-premises-resources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/device-sso-to-on-premises-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/device-sso-to-on-premises-resources.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d7f47930-488c-9be9-f2c2-e6e878a4cccc
---

# How SSO to on-premises resources works on Microsoft Entra joined devices - Microsoft Entra ID | Microsoft Learn

Microsoft Entra joined devices give users a single sign-on (SSO) experience to your tenant's cloud apps. If your environment has on-premises Active Directory Domain Services (AD DS), users can also SSO to resources and applications that rely on on-premises Active Directory Domain Services.

This article explains how this works.

## Prerequisites

- An [Microsoft Entra joined device](concept-directory-join).
- On-premises SSO requires line-of-sight communication with your on-premises AD DS domain controllers. If Microsoft Entra joined devices aren't connected to your organization's network, a VPN or other network infrastructure is required.
- Microsoft Entra Connect or Microsoft Entra Cloud Sync: To synchronize default user attributes like SAM Account Name, Domain Name, and UPN. For more information, see the article [Attributes synchronized by Microsoft Entra Connect](../hybrid/connect/reference-connect-sync-attributes-synchronized#windows-10).

## How it works

With a Microsoft Entra joined device, your users already have an SSO experience to the cloud apps in your environment. If your environment has Microsoft Entra ID and on-premises AD DS, you might want to expand the scope of your SSO experience to your on-premises Line Of Business (LOB) apps, file shares, and printers.

Microsoft Entra joined devices have no knowledge about your on-premises AD DS environment because they aren't joined to it. However, you can provide additional information about your on-premises AD to these devices with Microsoft Entra Connect.

Microsoft Entra Connect or Microsoft Entra Cloud Sync synchronize your on-premises identity information to the cloud. As part of the synchronization process, on-premises user and domain information is synchronized to Microsoft Entra ID. When a user signs in to a Microsoft Entra joined device in a hybrid environment:

1. Microsoft Entra ID sends the details of the user's on-premises domain back to the device, along with the [Primary Refresh Token](concept-primary-refresh-token)
2. The local security authority (LSA) service enables Kerberos and NTLM authentication on the device.

Note

Additional configuration is required when passwordless authentication to Microsoft Entra joined devices is used.

For FIDO2 security key based passwordless authentication and Windows Hello for Business Hybrid Cloud Trust, see [Enable passwordless security key sign-in to on-premises resources with Microsoft Entra ID](../authentication/howto-authentication-passwordless-security-key-on-premises).

For Windows Hello for Business Cloud Kerberos Trust, see [Configure and provision Windows Hello for Business - cloud Kerberos trust](/en-us/windows/security/identity-protection/hello-for-business/hello-hybrid-cloud-kerberos-trust-provision).

For Windows Hello for Business Hybrid Key Trust, see [Configure Microsoft Entra joined devices for On-premises Single-Sign On using Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-hybrid-aadj-sso).

For Windows Hello for Business Hybrid Certificate Trust, see [Using Certificates for AADJ On-premises Single-sign On](/en-us/windows/security/identity-protection/hello-for-business/hello-hybrid-aadj-sso-cert).

During an access attempt to an on-premises resource requesting Kerberos or NTLM, the device:

1. Sends the on-premises domain information and user credentials to the located DC to get the user authenticated.
2. Receives a Kerberos [Ticket-Granting Ticket (TGT)](/en-us/windows/win32/secauthn/ticket-granting-tickets) or NTLM token based on the protocol the on-premises resource or application supports. If the attempt to get the Kerberos TGT or NTLM token for the domain fails, Credential Manager entries are tried, or the user might receive an authentication pop-up requesting credentials for the target resource. This failure can be related to a delay caused by a DCLocator timeout.

All apps that are configured for **Windows-Integrated authentication** seamlessly get SSO when a user tries to access them.

## What you get

With SSO, on a Microsoft Entra joined device you can:

- Access a UNC path on an AD member server
- Access an AD DS member web server configured for Windows-integrated security

If you want to manage your on-premises AD from a Windows device, install the [Remote Server Administration Tools](https://www.microsoft.com/download/details.aspx?id=45520).

You can use:

- The Active Directory Users and Computers (ADUC) snap-in to administer all AD objects. However, you have to specify the domain that you want to connect to manually.
- The DHCP snap-in to administer an AD-joined DHCP server. However, you might need to specify the DHCP server name or address.

## What you should know

- You might have to adjust your [domain-based filtering](../hybrid/connect/how-to-connect-sync-configure-filtering#domain-based-filtering) in Microsoft Entra Connect to ensure that the data about the required domains is synchronized if you have multiple domains.
- Apps and resources that depend on Active Directory machine authentication don't work because Microsoft Entra joined devices don't have a computer object in AD DS.
- You can't share files with other users on a Microsoft Entra joined device.
- Applications running on your Microsoft Entra joined device might authenticate users. They must use the implicit UPN or the NT4 type syntax with the domain FQDN name as the domain part, for example: user@contoso.corp.com or contoso.corp.com\user.
    - If applications use the NETBIOS or legacy name like contoso\user, the errors the application gets would be either, NT error STATUS\_BAD\_VALIDATION\_CLASS - 0xc00000a7, or Windows error ERROR\_BAD\_VALIDATION\_CLASS - 1348 "The validation information class requested was invalid." This error happens even if you can resolve the legacy domain name.