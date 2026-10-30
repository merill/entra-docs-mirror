---
layout: Conceptual
title: Browser access guidance for third party mobile device management providers - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/browser-access-guidance-third-party-devices
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: As an MDM provider, I want to update my Android Device policy to enable browser access during device registration so that my customers can access CA-protected resources seamlessly.
ms.topic: reference
ms.date: 2025-10-15T00:00:00.0000000Z
ms.reviewer: zhvolosh
locale: en-us
document_id: c1d14497-8b25-c6be-26fa-0a8968e1731f
document_version_independent_id: c1d14497-8b25-c6be-26fa-0a8968e1731f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/browser-access-guidance-third-party-devices.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/browser-access-guidance-third-party-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/browser-access-guidance-third-party-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 6284d76f-e0fc-8d09-22b2-410adef7f4b8
---

# Browser access guidance for third party mobile device management providers - Microsoft Entra ID | Microsoft Learn

Update your [Android Device policy](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies) resource to support automatically enabling browser access during device registration.

As announced in September 2024 and November 2025 in the What’s New in Microsoft Entra blog, we're automatically enabling browser access by default for Android users. This change is part of hardening all Microsoft products as part of the [Secure Future Initiative](https://www.microsoft.com/microsoft-cloud/resources/secure-future-initiative). As part of this initiative, we're eliminating the mechanism to export device registration keys from device storage after registration completes.

This change means that users of Android devices will no longer be able to modify their browser access settings in Authenticator app or Company Portal after their device has been registered in Microsoft Entra ID. Instead, Android users have browser access enabled by default.

## If you're an MDM provider

We request that you modify your [Android Device policy](https://developers.google.com/android/management/reference/rest/v1/enterprises.policies) resource to support enabling browser access during device registration. The policy resource is used to create and save groups of device and app management settings for your customers to apply to devices.

To enable browser access on behalf of your customers, you need to either create or modify an existing policy to provide a delegated certificate to the Authenticator app and Company Portal.

The following is an example of a policy:

**Policy example for setting delegated scope CERT\_INSTALL for authenticator**

```html
"applications": [{
    "packageName": "com.azure.authenticator"
    "installType": "REQUIRED_FOR_SETUP"
    "delegatedScopes": [
        "CERT_INSTALL"
      ]   
}],
```

CERT\_INSTALL - Grants access to certificate installation and management. - https://developer.android.com/reference/android/app/admin/DevicePolicyManager#DELEGATION_CERT_INSTALL

More information can be found here: [Android MDM create and apply policy](https://microsoft.sharepoint-df.com/:w:/t/AzureADDevices/EUBvQT-nqK1GhgrNwoOsUbYBUfCGH0uZM7bLQBPS56bggw?e=UvUuF0).

If you fail to make the requested change, your end users encounter the following behavior:

- If the device is registered in Microsoft Entra with Browser Access enabled
    - No effect
- If the device is registered in Microsoft Entra but Browser Access isn't enabled:
    - Access to CA-protected resources on a non Microsoft Edge browser will be blocked.
    - If the user requires access to CA-protected resources on a web browser, they'll have to use Microsoft Edge.
- If the device is undergoing registration for the first time:
    - The user is prompted to choose a certificate type and name their certificate as part of the registration flow.
    - This certificate is used to enable browser access.
    - Once this certificate is on the device, browser access is enabled, and the user can access CA-protected resources on any browser of their choice.

[![Screenshot of setting device certificates.](media/browser-access-guidance-third-party-devices/device-certificates.png)](media/browser-access-guidance-third-party-devices/device-certificates.png#lightbox)