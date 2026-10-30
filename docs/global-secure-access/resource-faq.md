---
layout: FAQ
title: Global Secure Access FAQ - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/resource-faq
summary: >
  <p>Frequently asked questions related to Microsoft Entra Internet Access and Microsoft Entra Private Access, which are part of Global Secure Access.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Frequently asked questions for Global Secure Access.
ms.topic: faq
ms.date: 2024-08-03T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 5913e840-eac9-9efe-db04-1dc98b597b77
document_version_independent_id: 8dcc78b7-b253-2ad3-056c-92b532061cb1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/resource-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/resource-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/resource-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: f7f7f70b-6708-7f71-cd38-4e5bb3bd82df
---

# Global Secure Access FAQ - Global Secure Access | Microsoft Learn

Frequently asked questions related to Microsoft Entra Internet Access and Microsoft Entra Private Access, which are part of Global Secure Access.

## Common platform questions

### I received an error when trying to access a tenant I have access to.

If you enabled universal tenant restrictions and access the Microsoft Entra admin center for one of the allow listed tenants, you see an "Access denied" error. Add the feature flag to the Microsoft Entra admin center: `?feature.msaljs=true&exp.msaljsexp=true`. For example, you work for Contoso and you have allow listed Fabrikam as a partner tenant. You see the error message for the Fabrikam tenant's Microsoft Entra admin center. If you received the "access denied" error message for this URL: `https://entra.microsoft.com/` then add the feature flag as follows: `https://entra.microsoft.com/?feature.msaljs%253Dtrue%2526exp.msaljsexp%253Dtrue#home`

### Does Global Secure Access allow B2B logins?

B2B logins are only supported when the user is accessing the service from a device that is Microsoft Entra joined. The Microsoft Entra tenant must match the users sign-in credentials. For example, a person works at Fabrikam and is working on a project for Contoso. Contoso provided the person a device and a Contoso identity, such as `v-Bob@contoso.com`. To access Contoso's Global Secure Access using the Contoso device, the person can use either `Bob@Fabrikam.com` or `v-Bob@Contoso.com`. However, the person can't use the Fabrikam device that is joined to the Fabrikam tenant to access Contoso's Global Secure Access.

### What is the difference between Security Service Edge (SSE) and Endpoint Detection and Response (EDR) platforms?

Secure Web Gateway capabilities as part of [Microsoft Entra Internet Access](overview-what-is-global-secure-access) and other Security Service Edge (SSE) platforms deliver advanced network security value from the cloud edge for all users connecting to any application. Microsoft's SSE Solution specifically leverages deep integration with Microsoft Entra ID to bring identity and context awareness to granular network security policies. Additionally, SSE platforms provide richer controls and deeper visibility via Transport Layer Security (TLS) Inspection, allowing these platforms to inspect and enforce security policy on the packet. Endpoint Detection and Response (EDR) platforms like [Microsoft Defender for Endpoint](/en-us/defender-endpoint/web-content-filtering/) provide device aware security value for managed devices. These policies allow you to target devices or device groups, rather than user-based identity constructs. EDR platforms also provide visibility via advanced hunting capabilities. It is best to use both network and endpoint protection controls in tandem to achieve a defense in depth approach. If an EDR platform is used together with Microsoft Entra Internet Access, the EDR platform’s on-device policies will always be enforced before reaching the cloud edge, where Microsoft Entra Internet Access policies are enforced.

### Does Global Secure Access support IPv6?

At this time, IPv4 is preferred over IPv6. If you encounter issues, disable IPv6. For more information, see [IPv4 preferred](troubleshoot-global-secure-access-client-diagnostics-health-check#ipv4-preferred).

### Can I manage Global Secure Access with Microsoft Graph APIs?

Yes, there's a set of Microsoft Graph APIs available to manage aspects of Microsoft Entra Internet Access and Microsoft Entra Private Access. For more information about these APIs, see the article [Secure access to cloud, public, and private apps using Microsoft Graph network access APIs](/en-us/graph/api/resources/networkaccess-global-secure-access-api-overview).

## Private Access

### How do we assure no Microsoft engineer (or someone pretending to be one) can make a call to one of customer's applications?

There are two safeguards for this that exist today:

- Authentication and authorization are performed for all Private Access Scenarios. Every network flow that comes to the Connector must come with a valid token for an Entra 3P app. In addition, the destination can be only one of the app segments configured in this 3P app. The network tunnel that connects the Connector to our service in the Cloud needs this app token for every network flow to the Connector for the Connector to receive the traffic. Thus, even if some Microsoft engineer were to try to send the traffic to the Connector, without this valid token, this traffic won't be delivered to the Connector.
- The communication between Connector and Private Access cloud Infrastructure with Global Secure Access is encrypted and authenticated using TLS tunnels which uses a service pinned certificate. This means that the traffic between our Service and Connector is not open for B&I and prevents MiTM (Man-in-the-Middle) attacks.

## Remote networks

### I configure my customer premises equipment (CPE) and Global Secure Access, but the two aren't connecting. I specify the Local and Peer Border Gateway Protocol (BGP) IP addresses, but the connection isn't working.

Make sure you reverse the BGP IP addresses between the CPE and Global Secure Access. For example, if you specified the Local BGP IP address as 1.1.1.1 and the Peer BGP IP address as 0.0.0.0 for the CPE, then swap the values in Global Secure Access. So the Local BGP IP address in Global Secure Access is 0.0.0.0 and the Peer GBP IP address is 1.1.1.1.

## Internet Access

### What is the difference between Microsoft Entra Internet Access web categories and Microsoft Defender for Endpoint web categories?

Microsoft Entra Internet Access and Microsoft Defender for Endpoint both leverage similar categorization engines, with a few distinct differences. The Microsoft Entra Internet Access engine aims to provide a valid categorization of every endpoint on the internet, while Microsoft Defender for Endpoint supports a smaller list of site categories, focused on categories of sites that could introduce liability for the organization that operates the endpoint. This means that many sites are not categorized, and an organization wishing to allow or deny access must manually create a Network Indicator for the site.