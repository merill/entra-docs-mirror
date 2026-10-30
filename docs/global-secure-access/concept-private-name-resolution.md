---
layout: Conceptual
title: Microsoft Entra Private DNS - Configure Secure Internal Name Resolution - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-private-name-resolution
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure Microsoft Entra Private DNS for secure and efficient internal DNS query resolution, replacing legacy VPNs with granular access.
contributors: 
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
locale: en-us
document_id: c44f3622-1c24-e9dd-df74-ef4d84d6cb55
document_version_independent_id: c44f3622-1c24-e9dd-df74-ef4d84d6cb55
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-private-name-resolution.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-private-name-resolution
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-private-name-resolution.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: e21fc1d8-9407-ae7d-c37a-b5a289e2249d
---

# Microsoft Entra Private DNS - Configure Secure Internal Name Resolution - Global Secure Access | Microsoft Learn

## Private DNS overview

Microsoft Entra Private Access provides a quick and easy way to replace legacy VPNs. It provides granular and secure access to internal resources without exposing your full network. DNS plays a vital role by enabling name resolution for critical internal resources, and remote users don't need to know the configuration of internal DNS systems. Microsoft Entra Private DNS with Quick Access offers a simple setup that uses Connector local resolvers to respond to DNS queries for internal resources.

Private DNS service allows you to add domain suffixes for the organization to the Quick Access configuration. This automatically updates the traffic forwarding profile for clients. Once configured, any DNS queries for a fully qualified domain name (FQDN) that ends with the matching suffixes from client devices are sent to the DNS proxy at a GSA edge for resolution. If a cached result is available, DNS responses are returned to the clients. Otherwise, the DNS proxy forwards the request to the Connector, which sends the DNS query to its DNS server for resolution. The Connector then passes the responses back to the edge, which returns the query to the client. The GSA client then assigns a synthetic IP address, and returns it back to the application. The synthetic IP is used to steer the application traffic to GSA edges.

A high-level Private DNS flow for Windows clients is shown in the following diagram.

**Configuration**

- An admin enables Private DNS and adds a DNS suffix from Quick Access.
- On the client, an entry in the Name Resolution Policy Table (NRPT) is generated for the suffix to resolve via the GSA client.
- Client traffic forwarding profile is updated to send private DNS queries to the GSA edge.

**Datapath**

1. User requests a DNS query for `app.contoso.com`. If not cached locally, the DNS query is sent to the DNS proxy at the GSA edge.
2. DNS proxy either responds from its cache or forwards the query to the Connector Group defined in Quick Access.
3. The connector server sends the DNS query to the DNS servers configured at operating system level.
4. DNS proxy responds back to the client with the internal IP. The client stores the internal IP address and returns a synthetic IP to the application.

![Screenshot of a diagram showing DNS queries resolved via Private DNS when a DNS suffix is configured in Quick Access.](media/concept-private-name-resolution/queries.png)

When a DNS suffix is configured in Quick Access, all DNS queries for a fully qualified domain name (FQDN) that ends with the matching suffixes are resolved by Private DNS, including those used to define Enterprise Apps.

## Single-label domain (SLD) resolution

The Private DNS provides name resolution for SLD without a domain suffix. An NRPT entry is created to send GSA suffix `globalsecureaccess.local.` to DNS proxy when Private DNS is configured. The client machine appends the `<appid>.globalsecureaccess.local.` suffix to the SLD and sends the DNS request to the DNS proxy. DNS proxy strips away the search suffix before sending the DNS query to the connector. The connector then uses its local search suffixes to resolve the SLD query. Resolved IP address for the resource is returned to the DNS proxy and passed along to the client.

Note

For some applications such as Kerberos authentication, it is important to have the correct SPN. GSA synthetic suffix might break Kerberos flow, so it's recommended to use FQDN for applications that require Kerberos authentication.