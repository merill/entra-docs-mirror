---
layout: FAQ
title: Microsoft Entra Kerberos FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/kerberos-faq
summary: >
  <p>This article addresses frequently asked questions about how Microsoft Entra Kerberos works.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Frequently asked questions and answers for Microsoft Entra Kerberos.
ms.topic: faq
ms.date: 2025-11-04T00:00:00.0000000Z
ms.reviewer: vimrang
locale: en-us
document_id: 60338b5c-6f68-6d39-4129-0492c85a9f95
document_version_independent_id: 60338b5c-6f68-6d39-4129-0492c85a9f95
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/kerberos-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/kerberos-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/kerberos-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/798bd9d1-9cc5-4fc7-b0e5-8699d1f6ce2a
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b5dc5f65-34a8-4bfc-9917-97d1e20c88b2
platformId: 7a2d24d0-abf8-90e2-33bd-9e4c49d6b875
---

# Microsoft Entra Kerberos FAQ - Microsoft Entra ID | Microsoft Learn

This article addresses frequently asked questions about how Microsoft Entra Kerberos works.

## What is Cloud Kerberos Trust?

A deployment model that lets Windows Hello for Business use Entra ID as the trust anchor for Kerberos, removing the need for Active Directory Federated Server (ADFS) or issuing user certs. Devices get a Cloud TGT from Entra ID and (when needed) exchange a partial TGT with on‑prem DCs for on‑prem access.

## What is the difference between a Cloud ticket granting ticket (TGT) and a partial (referral) TGT?

Cloud TGT: Issued by Entra ID for the KERBEROS.MICROSOFTONLINE.COM realm; used to request service tickets for cloud-integrated resources (e.g., Azure Files, Azure SQL). Partial TGT (referral): Minimal ticket from Entra ID that the client exchanges with an on‑prem DC to obtain a full AD TGT for on‑prem resources.

## Which devices are supported for Cloud Kerberos Trust?

Windows 10, version 2004 and later, and Windows 11 devices that are Azure AD joined or hybrid Azure AD joined.

## Is macOS supported?

Yes, via Platform single sign-on with a Kerberos single sign-on profile. macOS can obtain tgt\_cloud (Entra) and tgt\_ad (on‑prem) tickets when configured with the Kerberos extension.

## What policies must I enable on Windows clients?

Turn on Windows Hello for Business and enable Use cloud trust for on‑premises authentication. This is typically deployed via Intune Settings Catalog or Group Policy Object.

## Which user sign-in methods are supported for Cloud Kerberos Trust?

Key-based sign-in methods only: Windows Hello for Business (PIN or FIDO2) or passwordless phone sign-in. Password sign-in isn't supported.

## How do clients retrieve Cloud TGTs at logon?

Configure the device policy CloudKerberosTicketRetrievalEnabled = 1 (Microsoft Intune Configuration Service Providers or Group Policy Object). Without it, clients won’t fetch Cloud TGTs automatically.

## How do I check if the device is properly joined and has single sign-on state?

Run `dsregcmd /status` and confirm AzureAdJoined = YES (or Hybrid), AzureAdPrt = YES, and CloudTgt = YES.

## How do I verify service tickets for a resource?

Use `klist get cifs/<storage>.file.core.windows.net` (Azure Files example) and then klist to view retrieved tickets.

## Why does `klist cloud_debug` show Cloud Kerberos enabled by policy: 0?

The client policy isn't applied. Set CloudKerberosTicketRetrievalEnabled = 1 via Intune or Group Policy Object and reboot to apply.

## Why is Cloud TGT missing even after enabling policy?

Ensure the user signed in with a key-based method (WHfB/FIDO2) and the device is Entra or hybrid joined. If hybrid access is needed, verify the Trusted Domain Object exists and DC connectivity.

## Why is Partial TGT (referral) missing in hybrid scenarios?

Validate that the AzureADKerberos object (trusted domain object) is created and healthy; confirm line-of-sight to DCs during the first interactive sign-in.

## How can I inspect Entra Kerberos traffic for deep diagnostics?

Use the Kerberos.NET Fiddler extension to decrypt Key Distribution Center proxy HTTPS traffic to Entra ID and investigate Authentication Server/Ticket Granting Service flows and error codes.

## Can I enforce Conditional Access and MFA for legacy apps via Entra Kerberos?

Yes, authentication goes through Entra ID first, so you can apply Conditional Access, then rely on Kerberos tickets for app access.

## Can Cloud Kerberos Trust coexist with WHfB certificate trust?

No. If certificate trust policies are present, they take precedence over cloud trust. Choose one trust model per device

## Do I need an AzureADKerberos computer object in AD for cloud-only identities?

No, AzureADKerberos computer object in AD is only required for hybrid scenarios.

## How does Entra Kerberos handle password changes?

For key-based sign-ins, password changes don't impact Kerberos tickets. The user continues to authenticate with WHfB/FIDO2 without interruption.

## How do I find cloud security identifier (SID) for a cloud only user?

```msgraph
GET https://graph.microsoft.com/v1.0/users/{userid}?$select=securityIdentifier
ConsistencyLevel: eventual
```

## How do I find on-premises SID for a Hybrid user?

```msgraph
GET https://graph.microsoft.com/v1.0/users/{userid}?$select=onPremisesSecurityIdentifier
ConsistencyLevel: eventual
```

## How do I find cloud group SIDs for a cloud only user?

```msgraph
GET https://graph.microsoft.com/v1.0/groups?$filter=securityEnabled eq true&$select=id,displayName,securityIdentifier
ConsistencyLevel: eventual
```

## How do I find on-premises group SIDs for a Hybrid user?

```msgraph
GET https://graph.microsoft.com/v1.0/groups?$filter=securityEnabled eq true&$select=id,displayName,onPremisesSecurityIdentifier
ConsistencyLevel: eventual
```