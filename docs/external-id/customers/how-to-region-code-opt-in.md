---
layout: Conceptual
title: Regional opt-in for MFA telephony verification with external tenants (preview) - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-region-code-opt-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: To protect customers, some regions require you to enable the country codes to receive SMS telephony verification for Microsoft Entra External ID external tenants.
ms.topic: how-to
ms.date: 2026-04-17T00:00:00.0000000Z
ms.reviewer: aloom3
ms.custom: it-pro, references_regions
ai-usage: ai-assisted
locale: en-us
document_id: e6cc4405-f59f-08c8-b1fe-fff4b407a61c
document_version_independent_id: e6cc4405-f59f-08c8-b1fe-fff4b407a61c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-region-code-opt-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-region-code-opt-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-region-code-opt-in.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 93ec87cc-4dbe-146d-86f0-5f993db75144
---

# Regional opt-in for MFA telephony verification with external tenants (preview) - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

To safeguard against telephony fraud, Microsoft disallows traffic from certain phone number country codes. Doing so helps prevent unauthorized access and protect customers from fraudulent activities such as International Revenue Share Fraud (IRSF). With IRSF, criminals gain unauthorized access to a network and divert traffic to premium-rate numbers. They generate profits through a technique called traffic pumping. This technique often targets multifactor authentication systems, causing inflated charges, service instability, and system errors, making it harder for your customers to access your services.

When a country code is blocked, customers trying to set up SMS verification for multifactor authentication (MFA) for your application might encounter the message "Try another verification method." To resolve this issue, you can enable telephony traffic for specific country codes in your application.

You can use the Microsoft Graph API `onPhoneMethodLoadStart` event policy to manage telephony traffic for apps in your external tenant. With this event policy, you can enable or disable country codes for specific countries and regions.

Important

This feature is currently in preview. See the [Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) for legal terms that apply to Azure features and services that are in beta, preview, or otherwise not generally available.

## Country codes requiring opt-in

The following country codes are deactivated by default for SMS verification. If you want to allow traffic from deactivated regions, you need to enable them by using the `onPhoneMethodLoadStart` event policy.

**Table 1. SMS verification country codes requiring opt-in**

| Country code | Region Name |
| --- | --- |
| 93 | Afghanistan |
| 213 | Algeria |
| 244 | Angola |
| 374 | Armenia |
| 994 | Azerbaijan |
| 880 | Bangladesh |
| 375 | Belarus |
| 501 | Belize |
| 229 | Benin |
| 975 | Bhutan |
| 591 | Bolivia |
| 387 | Bosnia and Herzegovina |
| 359 | Bulgaria |
| 226 | Burkina Faso |
| 257 | Burundi |
| 238 | Cabo Verde |
| 855 | Cambodia |
| 237 | Cameroon |
| 235 | Central African Republic |
| 269 | Comoros |
| 243 | Congo (Democratic Republic of the) |
| 242 | Congo (Republic of the) |
| 225 | Côte d'Ivoire |
| 385 | Croatia |
| 53 | Cuba |
| 253 | Djibouti |
| 593 | Ecuador |
| 20 | Egypt |
| 503 | El Salvador |
| 291 | Eritrea |
| 251 | Ethiopia |
| 679 | Fiji |
| 689 | French Polynesia |
| 241 | Gabon |
| 220 | Gambia |
| 995 | Georgia |
| 233 | Ghana |
| 590 | Guadeloupe |
| 502 | Guatemala |
| 224 | Guinea |
| 245 | Guinea-Bissau |
| 592 | Guyana |
| 509 | Haiti |
| 62 | Indonesia |
| 98 | Iran |
| 964 | Iraq |
| 1876 | Jamaica |
| 962 | Jordan |
| 254 | Kenya |
| 686 | Kiribati |
| 383 | Kosovo |
| 965 | Kuwait |
| 996 | Kyrgyzstan |
| 961 | Lebanon |
| 266 | Lesotho |
| 231 | Liberia |
| 218 | Libya |
| 261 | Madagascar |
| 265 | Malawi |
| 223 | Mali |
| 222 | Mauritania |
| 230 | Mauritius |
| 262 | Mayotte |
| 691 | Micronesia |
| 373 | Moldova |
| 976 | Mongolia |
| 212 | Morocco |
| 258 | Mozambique |
| 95 | Myanmar |
| 977 | Nepal |
| 687 | New Caledonia |
| 505 | Nicaragua |
| 227 | Niger |
| 234 | Nigeria |
| 968 | Oman |
| 92 | Pakistan |
| 970 | Palestinian Authority |
| 675 | Papua New Guinea |
| 63 | Philippines |
| 974 | Qatar |
| 7 | Russia, Kazakhstan |
| 250 | Rwanda |
| 290 | Saint Helena |
| 508 | Saint Pierre and Miquelon |
| 1784 | Saint Vincent and the Grenadines |
| 685 | Samoa |
| 377 | San Marino |
| 966 | Saudi Arabia |
| 221 | Senegal |
| 232 | Sierra Leone |
| 1721 | Sint Maarten |
| 386 | Slovenia |
| 252 | Somalia |
| 211 | South Sudan |
| 94 | Sri Lanka |
| 249 | Sudan |
| 963 | Syria |
| 992 | Tajikistan |
| 255 | Tanzania |
| 670 | Timor-Leste |
| 672 | Timor-Leste |
| 228 | Togo |
| 690 | Tonga |
| 216 | Tunisia |
| 993 | Turkmenistan |
| 256 | Uganda |
| 380 | Ukraine |
| 971 | United Arab Emirates |
| 998 | Uzbekistan |
| 678 | Vanuatu |
| 84 | Vietnam |
| 967 | Yemen |
| 260 | Zambia |
| 263 | Zimbabwe |

## Manage telephony for regions with Microsoft Graph

Use the `OnPhoneMethodLoadStartExternalUsersAuthHandler` event policy to enable or disable country codes.

**Table 2. Properties of OnPhoneMethodLoadStartExternalUsersAuthHandler**

| Property | Description |
| --- | --- |
| DefaultRegions | An array of country codes where telephony service is enabled by default. This property is read-only. |
| IncludeAdditionalRegions | An array of country codes to enable for telephony service in addition to default country codes. Codes are validated against current International Subscriber Dialing (ISD) country codes, where the maximum length is 4. The same code can't be specified in both IncludeAdditionalRegions and ExcludeRegions. |
| ExcludeRegions | An array of country codes to disable for telephony service. Codes are validated against current ISD country codes, where the maximum length is 4. The same code can't be specified in both IncludeAdditionalRegions and ExcludeRegions. |

### How to enable telephony for regions

To enable telephony traffic from currently deactivated country codes, use the Microsoft Graph API to set the `includeAdditionalRegions` property in the `onPhoneMethodLoadStart` event policy for one or more applications. Include the relevant country codes in the `includeAdditionalRegions` property of the API request body for the regions you want to enable. For example, to send SMS requests in South Asia, enable the numeric country codes for the specific countries in that region.

#### Example REST APIs

```http
POST https://graph.microsoft.com/v1.0/identity/authenticationEventListeners  
{  
    "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartListener",  
    "conditions": {  
        "applications": {  
            "includeApplications": [  
                "3dfff01b-0afb-4a07-967f-d1ccbd81102a"  
            ]  
        }  
    },  
    "priority": 500,  
    "handler": {
        "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartExternalUsersAuthHandler",
        "smsOptions": {
            "includeAdditionalRegions": [222, 998],
            "excludeRegions": []
        },
        "voiceOptions": {
          "includeAdditionalRegions": [],
          "excludeRegions": []
        }
    }
} 

HTTP/1.1 201 Created 
{ 
    "@odata.context": "https://microsoft.graph.microsoft.com/v1.0/$metadata#identity/authenticationEventListeners/$entity", 
    "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartListener", 
    "id": "2be3336b-e3b4-44f3-9128-b6fd9ad39bb8", 
    "conditions": {  
        "applications": { 
            "includeApplications": [  
                "3dfff01b-0afb-4a07-967f-d1ccbd81102a"  
            ] 
        }   
    },   
    "handler": {
        "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartExternalUsersAuthHandler",
        "smsOptions": {
            "includeAdditionalRegions": [222, 998],
            "excludeRegions": []
        },
        "voiceOptions": {
            "includeAdditionalRegions": [],
            "excludeRegions": []
        }
    }
} 
```

### How to disable telephony for regions

If you want to block suspected fraudulent requests coming from a region, you can disable country codes by using the `excludeRegions` property in the `onPhoneMethodLoadStart` policy.

For example, if an External ID application detects a high volume of nonverification SMS messages from a specific country code, you can disable telephony in that region. To do so, place the country code in the `excludeRegions` list.

#### Example REST APIs

```http
POST https://graph.microsoft.com/v1.0/identity/authenticationEventListeners  
{  
    "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartListener",  
    "conditions": {  
        "applications": {  
            "includeApplications": [  
                "3dfff01b-0afb-4a07-967f-d1ccbd81102a"  
            ]  
        }  
    },  
    "priority": 500,
    "handler": {
        "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartExternalUsersAuthHandler",
        "smsOptions": {
            "includeAdditionalRegions": [222, 998],
            "excludeRegions": [234, 971]
        },
        "voiceOptions": {
            "includeAdditionalRegions": [],
            "excludeRegions": []
        }
    }
} 

HTTP/1.1 201 Created 
{ 
    "@odata.context": "https://microsoft.graph.microsoft.com/v1.0/$metadata#identity/authenticationEventListeners/$entity", 
    "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartListener", 
    "id": "2be3336b-e3b4-44f3-9128-b6fd9ad39bb8", 
    "conditions": {  
        "applications": { 
            "includeApplications": [  
                "3dfff01b-0afb-4a07-967f-d1ccbd81102a"  
            ] 
        }   
    },
    "handler": {
        "@odata.type": "#microsoft.graph.onPhoneMethodLoadStartExternalUsersAuthHandler",
        "smsOptions": {
            "includeAdditionalRegions": [222, 998],
            "excludeRegions": [234, 971]
        },
        "voiceOptions": {
            "includeAdditionalRegions": [],
            "excludeRegions": []
        }
    }
}  
```