---
layout: Conceptual
title: Add your own Traffic Manager solution to application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-integrate-with-traffic-manager
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Combine Microsoft Entra application proxy with Azure Traffic Manager for geographic load balancing and high availability across multiple connector groups.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ms.custom: template-how-to
ai-usage: ai-assisted
locale: en-us
document_id: 50339a1a-3ea2-f9e3-9eb3-3e30ac285126
document_version_independent_id: 768f8fc1-032b-13d6-3aca-29aeddfdffd3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-integrate-with-traffic-manager.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-integrate-with-traffic-manager
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-integrate-with-traffic-manager.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a21829dd-8109-415c-84d3-07c42e4d33fd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/70f417fa-3512-48b5-a80a-bb8985120ba9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: be8e8e8b-8f6d-5d9d-65b8-3d8a0a25e187
---

# Add your own Traffic Manager solution to application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

This article explains how to configure Microsoft Entra application proxy and Azure Traffic Manager.

With the application proxy geo-routing feature, you can optimize which region of application proxy your connector groups use. You can combine this functionality with a Traffic Manager solution of your choice. This combination enables a fully dynamic geo-aware solution based on your user location. It unlocks the rich rule set of your preferred Traffic Manager solution to prioritize how traffic is routed to the apps that you help protect by using application proxy. With this combination, users can use a single URL to access the instance of the app that's closest to them.

![Diagram that shows Traffic Manager integration with application proxy.](media/application-proxy-integrate-with-traffic-manager/application-proxy-integrate-with-traffic-manager-diagram.png)

## Prerequisites

- A Traffic Manager solution.
- Apps that exist in different regions. Geo-routing is enabled per connector group colocated with the app.
- A custom domain to use for each app.

## Configure application proxy

To use Traffic Manager, you must configure application proxy. The configuration steps that follow refer to these URL definitions:

- **Regional URL**: The application proxy endpoints for each app. For example, `nam.contoso.com` and `india.contoso.com`.
- **Alternate URL**: The URL configured for the Traffic Manager solution. For example, `contoso.com`.

To configure application proxy for Traffic Manager:

1. Install connectors for each location that contains your app instances. For each connector group, use the geo-routing feature to assign the connectors to their respective regions.
2. Set up your app instances with application proxy:

    1. For each app, upload a custom domain. Include the alternate URL to use for the apps as a subject alternative name (SAN) URL to the uploaded certificate.
    2. Assign each app to its respective connector group.
    3. If you prefer the alternate URL to be maintained throughout the user session, register each app and add the URL as a reply URL. This step is optional.
3. In the Traffic Manager solution, add the regional URLs for application proxy that you created for each app as endpoints.
4. Configure the Traffic Manager solution's load-balancing rules with a standard license.
5. To give your Traffic Manager solution a user-friendly URL, create a `CNAME` record that points the alternate URL to the Traffic Manager solution's endpoint.
6. Configure the alternate URL on the app by using the Microsoft Graph API to update the `alternateUrl` property on the [`onPremisesPublishing` resource type](/en-us/graph/api/resources/onpremisespublishing). The `alternateUrl` property isn't available in the Microsoft Entra admin center. You must configure it by using the Graph API. For more information, see [Update application](/en-us/graph/api/application-update).

    The following example shows the request body for setting `alternateUrl`:

    ```http
    PATCH https://graph.microsoft.com/beta/applications/{id}
    Content-Type: application/json
    
    {
      "onPremisesPublishing": {
        "alternateUrl": "https://www.contoso.com"
      }
    }
    ```

    Note

    The `onPremisesPublishing` property can't be updated in the same request as other application properties.
7. If you want the alternate URL to be maintained throughout the user session, set the `useAlternateUrlForTranslationAndRedirect` flag to `true` in the same `onPremisesPublishing` object:

    ```http
    PATCH https://graph.microsoft.com/beta/applications/{id}
    Content-Type: application/json
    
    {
      "onPremisesPublishing": {
        "alternateUrl": "https://www.contoso.com",
        "useAlternateUrlForTranslationAndRedirect": true
      }
    }
    ```

## Sample application proxy configuration

The following table shows a sample application proxy configuration. This configuration uses the sample app domain `www.contoso.com` as the alternate URL.

| - | North America-based app | India-based app | Additional information |
| --- | --- | --- | --- |
| **Internal URL** | `contoso.com` | `contoso.com` | If the apps are hosted in different regions, you can use the same internal URL for each app. |
| **External URL** | `nam.contoso.com` | `india.contoso.com` | Configure a custom domain for each app. |
| **Custom domain certificate** | Domain Name System (DNS): `nam.contoso.com` SAN: `www.contoso.com` | DNS: `india.contoso.com` SAN: `www.contoso.com` | In the certificate that you upload for each app, set the SAN value to the alternate URL. The alternate URL is the URL that all users use to reach the app. |
| **Connector group** | North America Geo Group | India Geo Group | Ensure that you assign each app to the correct connector group by using the geo-routing functionality. |
| **Redirects** | (Optional) To maintain redirects for the alternate URL, add the application registration for the app. | (Optional) To maintain redirects for the alternate URL, add the application registration for the app. | This step is required if the alternate URL `www.contoso.com` will be maintained for all redirections. |
| **Reply URL** | `www.contoso.com` | `www.contoso.com` |  |

## Configure Traffic Manager

Follow these steps to configure Traffic Manager:

1. Create a Traffic Manager profile with your preferred routing rules.
2. In Traffic Manager, add the North America endpoint: `nam.contoso.com`.
3. Add the India endpoint: `india.contoso.com`.
4. Add the app proxy endpoints.
5. Add a `CNAME` record to point `www.contoso.com` to the Traffic Manager solution's URL. For example, use `contoso.trafficmanager.net`. The alternate URL now points to the Traffic Manager solution.