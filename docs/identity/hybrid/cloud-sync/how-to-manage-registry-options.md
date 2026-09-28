---
layout: Conceptual
title: 'Microsoft Entra Connect cloud provisioning agent: Manage registry options - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-manage-registry-options
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to manage registry options in the Microsoft Entra Connect cloud provisioning agent.
ms.topic: how-to
ms.tgt_pltfrm: na
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.reviewer: chmutali
locale: en-us
document_id: b5938e3a-c68d-11fa-8bd3-c0c671bb9ee4
document_version_independent_id: 8d2a0b32-c834-5473-8fd2-3e7740e1f99b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-manage-registry-options.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-manage-registry-options
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-manage-registry-options.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 10d27bbc-1f82-f5ce-f44a-683cc9c3f9a0
---

# Microsoft Entra Connect cloud provisioning agent: Manage registry options - Microsoft Entra ID | Microsoft Learn

This section describes registry options that you can set to control the runtime processing behavior of the Microsoft Entra provisioning agent.

## Configure LDAP connection timeout

When performing LDAP operations on configured Active Directory domain controllers, by default, the provisioning agent uses the default connection timeout value of 30 seconds. If your domain controller takes more time to respond, then you might see the following error message in the agent log file:

`System.DirectoryServices.Protocols.LdapException: The operation was aborted because the client side timeout limit was exceeded.`

LDAP search operations can take longer if the search attribute isn't indexed. As a first step, if you get the aforementioned error, first check if the search/lookup attribute is [indexed](/en-us/windows/win32/ad/indexed-attributes). If the search attributes are indexed and the error persists, you can increase the LDAP connection timeout using the following steps:

1. Sign-in as Administrator on the Windows server running the Microsoft Entra provisioning agent.
2. Use the *Run* menu item to open the registry editor (regedit.exe)
3. Locate the key folder **HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Azure AD Connect Agents\Azure AD Connect Provisioning Agent**
4. Right-select and select "New -&gt; String Value"
5. Provide the name: `LdapConnectionTimeoutInMilliseconds`
6. Double-select on the **Value Name** and enter the value data as `60000` milliseconds. 
![LDAP Connection Timeout](media/how-to-manage-registry-options/ldap-connection-timeout.png)
7. Restart the Microsoft Entra Connect Provisioning Service from the *Services* console.
8. If you've deployed multiple provisioning agents, apply this registry change to all agents for consistency.

## Configure referral chasing

By default, the Microsoft Entra provisioning agent doesn't chase [referrals](/en-us/windows/win32/ad/referrals). You might want to enable referral chasing, to support certain HR inbound provisioning scenarios such as:

- Checking uniqueness of UPN across multiple domains
- Resolving cross-domain manager references

Use the following steps to turn on referral chasing:

1. Sign-in as Administrator on the Windows server running the Microsoft Entra provisioning agent.
2. Use the *Run* menu item to open the registry editor (regedit.exe)
3. Locate the key folder **HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Azure AD Connect Agents\Azure AD Connect Provisioning Agent**
4. Right-select and select "New -&gt; String Value"
5. Provide the name: `ReferralChasingOptions`
6. Double-select on the **Value Name** and enter the value data as `96`. This value corresponds to the constant value for `ReferralChasingOptions.All` and specifies that both subtree and base-level referrals are followed by the agent. 
![Referral Chasing](media/how-to-manage-registry-options/referral-chasing.png)
7. Restart the Microsoft Entra Connect Provisioning Service from the *Services* console.
8. If you've deployed multiple provisioning agents, apply this registry change to all agents for consistency.

Note

You can confirm the registry options have been set by enabling [verbose logging](how-to-troubleshoot#log-files). The logs emitted during agent startup display the config values picked from the registry.