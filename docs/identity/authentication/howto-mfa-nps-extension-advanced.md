---
layout: Conceptual
title: Configure the Microsoft Entra multifactor authentication NPS extension - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-mfa-nps-extension-advanced
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: After you install the NPS extension, use these steps for advanced configuration like allowed IP lists and UPN replacement.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: michmcla
locale: en-us
document_id: 17f663ca-635a-10ab-d78a-f60424a5484c
document_version_independent_id: cd178cad-c4c4-16a0-ca02-ac336165cad7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-mfa-nps-extension-advanced.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-mfa-nps-extension-advanced
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-mfa-nps-extension-advanced.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: fa5cd2ba-f506-4375-8de7-9f9ad542da2b
---

# Configure the Microsoft Entra multifactor authentication NPS extension - Microsoft Entra ID | Microsoft Learn

The Network Policy Server (NPS) extension extends your cloud-based Microsoft Entra multifactor authentication features into your on-premises infrastructure. This article assumes that you already have the extension installed, and now want to know how to customize the extension for your needs.

## Alternate sign-in ID

Since the NPS extension connects to both your on-premises and cloud directories, you might encounter an issue where your on-premises user principal names (UPNs) don't match the names in the cloud. To solve this problem, use alternate sign-in IDs.

Within the NPS extension, you can designate an Active Directory attribute to be used as the UPN for Microsoft Entra multifactor authentication. This enables you to protect your on-premises resources with two-step verification without modifying your on-premises UPNs.

To configure alternate sign-in IDs, go to `HKLM\SOFTWARE\Microsoft\AzureMfa` and edit the following registry values:

| Name | Type | Default value | Description |
| --- | --- | --- | --- |
| LDAP\_ALTERNATE\_LOGINID\_ATTRIBUTE | string | Empty | Designate the name of Active Directory attribute that you want to use as the UPN. This attribute is used as the AlternateLoginId attribute. If this registry value is set to a [valid Active Directory attribute](/en-us/windows/win32/adschema/attributes-all) (for example, mail or displayName), then the attribute's value is used as the user's UPN for authentication. If this registry value is empty or not configured, then AlternateLoginId is disabled and the user's UPN is used for authentication. |
| LDAP\_FORCE\_GLOBAL\_CATALOG | boolean | False | Use this flag to force the use of Global Catalog for LDAP searches when looking up AlternateLoginId. Configure a domain controller as a Global Catalog, add the AlternateLoginId attribute to the Global Catalog, and then enable this flag.  If LDAP\_LOOKUP\_FORESTS is configured (not empty), **this flag is enforced as true**, regardless of the value of the registry setting. In this case, the NPS extension requires the Global Catalog to be configured with the AlternateLoginId attribute for each forest. |
| LDAP\_LOOKUP\_FORESTS | string | Empty | Provide a semi-colon separated list of forests to search. For example, *contoso.com;foobar.com*. If this registry value is configured, the NPS extension iteratively searches all the forests in the order in which they were listed, and returns the first successful AlternateLoginId value. If this registry value isn't configured, the AlternateLoginId lookup is confined to the current domain. |

To troubleshoot problems with alternate sign-in IDs, use the recommended steps for [Alternate sign-in ID errors](howto-mfa-nps-extension-errors#alternate-login-id-errors).

## IP exceptions

If you need to monitor server availability, like if load balancers verify which servers are running before sending workloads, you don't want verification requests to block these checks. Instead, create a list of IP addresses that you know are used by service accounts, and disable multifactor authentication requirements for that list.

To configure an IP allowed list, go to `HKLM\SOFTWARE\Microsoft\AzureMfa` and configure the following registry value:

| Name | Type | Default value | Description |
| --- | --- | --- | --- |
| IP\_WHITELIST | string | Empty | Provide a semi-colon separated list of IP addresses. Include the IP addresses of machines where service requests originate, like the NAS/VPN server. IP ranges and subnets aren't supported.  For example, *10.0.0.1;10.0.0.2;10.0.0.3*. |

Note

This registry key isn't created by default by the installer and an error appears in the AuthZOptCh log when the service is restarted. This error in the log can be ignored, but if this registry key is created and left empty if not needed then the error message doesn't return.

When a request comes in from an IP address that exists in the `IP_WHITELIST`, two-step verification is skipped. The IP list is compared to the IP address that is provided in the *ratNASIPAddress* attribute of the RADIUS request. If a RADIUS request comes in without the ratNASIPAddress attribute, a warning is logged: "IP\_WHITE\_LIST\_WARNING::IP Whitelist is being ignored as the source IP is missing in the RADIUS request NasIpAddress attribute."