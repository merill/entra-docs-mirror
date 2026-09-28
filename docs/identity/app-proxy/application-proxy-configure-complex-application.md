---
layout: Conceptual
title: Complex applications for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-configure-complex-application
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Understand complex applications in Microsoft Entra application proxy.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 4e0ab835-3327-427d-8deb-32afed4908c4
document_version_independent_id: 20d57ae0-5b4f-089e-0296-dc66838a2c20
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-configure-complex-application.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-configure-complex-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-configure-complex-application.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 05136eb6-39a4-4ac8-2e25-7b8a66f57441
---

# Complex applications for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Applications are often made up of multiple individual web applications. These situations use different domain suffixes or different ports or paths in the URL. The individual web application instances must be published in separate Microsoft Entra application proxy apps. In these situations, the following problems might arise:

- **Pre authentication:** The client must separately acquire an access token or cookie for each Microsoft Entra application proxy app. The multiple acquisitions lead to more redirects at sign in to `microsoftonline.com`.
- **Cross-Origin Resource Sharing (CORS):** CORS calls, using the `OPTIONS` method, are used to validate access for the URL between the caller web app and the targeted web app. The Microsoft Entra application proxy cloud service blocks these calls. Blocking occurs because the requests can't contain authentication information.
- **Poor app management:** Multiple enterprise apps are created to enable access to a private app adding friction to the app management experience.

The following figure shows an example for complex application domain structure.

![Diagram of domain structure for a complex application showing resource sharing between primary and secondary application.](media/application-proxy-configure-complex-application/complex-app-structure-1.png)

With [Microsoft Entra application proxy](overview-what-is-app-proxy), you can address these challenges by using complex application publishing that is made up of multiple URLs across various domains.

![Diagram of a Complex application with multiple application segments definition.](media/application-proxy-configure-complex-application/complex-app-flow-1.png)

A complex app has multiple app segments. Each app segment has an internal and external URL. One Conditional Access policy is associated with the app. Access to any of the external URLs works with preauthentication with the same set of policies. These policies are enforced for all app segments.

Complex apps provide several benefits:

- User authentication
- Mitigation of CORS issues
- Access for different domain suffixes or different ports or paths in the internal URL

This article shows you how to configure wildcard application publishing in your environment.

## Characteristics of application segments for complex applications

Application segments for complex applications have the following characteristics:

- Application segments are only configured on a wildcard application.
- External and alternate URL should match the wildcard external and alternate URL domain of the application respectively.
- Application segment URLs (internal and external) need to maintain uniqueness across complex applications.
- CORS Rules (optional) can be configured per application segment.
- Access is only granted to defined application segments for a complex application. 
    Note

    If you delete all application segments, the complex application acts like a wildcard application, allowing access to any valid URL under the specified domain.
- You can have an internal URL defined both as an application segment and a regular application. 
    Note

    Regular applications always take precedence over a complex app (wildcard application).

## Prerequisites

Complete the following prerequisites:

- Enable application proxy and install a connector that has line of sight to your applications. See the tutorial [Add an on-premises application for remote access through application proxy](application-proxy-add-on-premises-application) to learn how to prepare your on-premises environment, install and register a connector, and test the connector.

## Configure application segments for complex applications

Note

Two application segments per complex distributed application are supported for [Microsoft Entra ID P1 or P2 subscription](https://www.microsoft.com/security/business/microsoft-entra-pricing).

To publish a complex distributed app through application proxy with application segments:

1. [Create a wildcard application.](application-proxy-wildcard#create-a-wildcard-application)
2. On the application proxy basic settings page, select **Add application segments**.

    ![Screenshot of link to add an application segment.](media/application-proxy-configure-complex-application/add-application-segments.png)
3. On the manage and configure application segments page, select **+ Add app segment**.

    ![Screenshot of Manage and configure application segment page.](media/application-proxy-configure-complex-application/add-application-segment-1.png)
4. Enter the **Internal Url**.
5. Select a custom domain from the **External Url** drop down the list.
6. Add CORS Rules (optional). For more information, see [Configuring CORS Rule](/en-us/graph/api/resources/corsconfiguration_v2?view=graph-rest-beta&amp;preserve-view=true).
7. Select **Create**.

    ![Screenshot of add or edit application segment context pane.](media/application-proxy-configure-complex-application/create-app-segment.png)
8. Assign users to the application.

To edit/update an application segment, select the application segment from the list on the manage and configure application segments page. Upload a certificate for the application segment's custom domain, if necessary, and update the Domain Name System (DNS) record.

## Configuring single sign-on (SSO)

Note

Single sign-on with Integrated Windows Authentication (IWA) doesn't support wildcard Service Principal Names (SPNs). For example, a wildcard such as `http/*.contoso.com` uses the single configured SPN such as `http/app.contoso.com` for all the segments.

## Update DNS records

Important

The CNAME instructions shown in the portal UI when editing an application segment might differ from the instructions in this section. For complex (wildcard) applications, always use the CNAME configuration described here, pointing to `tenant.runtime.msappproxy.net`, not the generic `.msappproxy.net` endpoint shown in the portal.

When using custom domains, create a DNS entry with a CNAME record for the external URL. For example, point `*.adventure-works.com` to the external URL of the application proxy endpoint. For wildcard applications, point the CNAME record to the tenant runtime endpoint: `<yourAADTenantId>.tenant.runtime.msappproxy.net`.

Alternatively, a dedicated DNS entry with a CNAME record for every individual application segment can be created as follows:

> 
> `External URL of the application segment` &gt; `<yourAADTenantId>.tenant.runtime.msappproxy.net`

Additionally, adding a CNAME record for the application ID in the same DNS zone is required:

> 
> `<yourAppId>` &gt; `<yourAADTenantId>.tenant.runtime.msappproxy.net`

If the connector group that is assigned to the Complex App isn't in the region of the Default connector group, one of the following domain suffixes must be used in the DNS entries:

| Connector Assigned Region | External URL |
| --- | --- |
| Asia | `<yourAADTenantId>.asia.tenant.runtime.msappproxy.net` |
| Australia | `<yourAADTenantId>.aus.tenant.runtime.msappproxy.net` |
| Europe | `<yourAADTenantId>.eur.tenant.runtime.msappproxy.net` |
| North America | `<yourAADTenantId>.nam.tenant.runtime.msappproxy.net` |

For more detailed instructions for application proxy, see [Tutorial: Add an on-premises application for remote access through application proxy in Microsoft Entra ID](application-proxy-add-on-premises-application).