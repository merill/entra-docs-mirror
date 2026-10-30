---
layout: Conceptual
title: Proxy Automatic Configuration (PAC) - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-proxy-automatic-configuration-files
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Learn about Explicit Forward Proxy PAC file concepts.
ms.topic: concept-article
ms.date: 2026-04-06T00:00:00.0000000Z
locale: en-us
document_id: 88047c8b-8bcd-f279-6fbc-130a78a06831
document_version_independent_id: 88047c8b-8bcd-f279-6fbc-130a78a06831
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-proxy-automatic-configuration-files.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-proxy-automatic-configuration-files
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-proxy-automatic-configuration-files.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 8c7b2c48-889f-c10e-a63d-6a48586ebefd
---

# Proxy Automatic Configuration (PAC) - Global Secure Access | Microsoft Learn

A proxy automatic configuration (PAC) file is a mechanism for automatically determining which proxy server a web browser or application should use for a request. PAC files are an integral part of Explicit Forward Proxy configuration, where they enable flexible and dynamic traffic-steering decisions. In the context of Global Secure Access, PAC files are similar to the traffic forwarding policies of the Global Secure Access client.

## How PAC files work

After you configure PAC files, they operate by providing browsers with a JavaScript function called `FindProxyForURL`. When a browser requests a resource, it calls this function. The function then evaluates conditions such as destination address, protocol, or host name. The function returns a directive that indicates which proxy (or proxies) to use, or whether to connect directly (bypass).

This approach allows for granular control over network traffic, so that you can define routing logic that's tailored to your specific needs.

## PAC file structure and syntax

The core of a PAC file is the JavaScript block that defines the `FindProxyForURL(url, host)` function. Within this function, you can use JavaScript constructs like `if` statements, regular expressions, and built-in helper functions (for example, `dnsDomainIs`, `isInNet`, `shExpMatch`) to determine proxy behavior. The function returns a string that specifies proxy settings, such as `"PROXY <tenantID>.internet.efp.globalsecureaccess.microsoft.com:443\"` for proxy use or `"DIRECT"` for direct connections.

The following example PAC file snippet shows a configuration where a Microsoft Entra ID sign-in is allowed to be accessed directly (required for Explicit Forward Proxy for Internet Access), while all other URLs are accessed via Explicit Forward Proxy:

```javascript
function FindProxyForURL(url, host) {

if (dnsDomainIs(host, \"login.microsoftonline.com\"))

return \"DIRECT\";

else

return \"PROXY *tenantId*.internet.efp.globalsecureaccess.microsoft.com:443\";

}
```

## Applying PAC file settings to browsers

The mechanism for applying PAC file settings varies depending on device management and browser type.

On managed devices, such as those governed by browser policy or enterprise mobility management, you can distribute PAC file URLs or content through centralized configuration tools.

For unmanaged devices, you can instruct users to manually enter the PAC file location in browser settings or rely on a network-provided configuration. A network-provided configuration might be Dynamic Host Configuration Protocol (DHCP) or Web Proxy Auto-Discovery (WPAD).