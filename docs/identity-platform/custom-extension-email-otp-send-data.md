---
layout: Conceptual
title: Retrieve and return data from an emailOtpSend event - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-extension-email-otp-send-data
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Reference documentation for a custom authentication extension that invokes the emailOtpSend event for External ID customer configurations.
manager: pmwongera
ms.date: 2025-05-20T00:00:00.0000000Z
ms.topic: how-to
locale: en-us
document_id: c4a17a2e-f421-f9d7-6cf4-8a58e831ff70
document_version_independent_id: c4a17a2e-f421-f9d7-6cf4-8a58e831ff70
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-extension-email-otp-send-data.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-extension-email-otp-send-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-extension-email-otp-send-data.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: ea0e3f2c-1473-5260-d731-d14c9ca7e1a6
---

# Retrieve and return data from an emailOtpSend event - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

To configure a custom email provider for [email one time passcode (OTP) send](custom-extension-email-otp-get-started) events, you create a custom authentication extension and invoke it at specific points in the user flow. When the **emailOtpSend** event is activated, Microsoft Entra sends a one-time passcode to the specified REST API you own.

The REST API then uses your chosen email provider, such as Azure Communication Service or SendGrid to send the one-time passcode with your custom email template, from address, email subject and more. This article describes the REST API schema for the emailOtpSend event.

## Request to the external REST API

The custom authentication extension you defined in Microsoft Entra ID makes an HTTP call to your REST API with a JSON payload. The JSON payload contains the user's email address and the one-time-passcode. The request also includes authentication context attributes and information about the application the user intends to sign in.

The following HTTP request demonstrates how Microsoft Entra invokes your REST API. This HTTP request can be used to debug your REST API by simulating a request from Microsoft Entra.

```http
POST https://example.azureWebsites.net/api/functionName

Content-Type: application/json

[Request payload]
```

The following JSON document provides an example of a request payload:

```json
{
    "type": "microsoft.graph.authenticationEvent.emailOtpSend",
    "source": "/tenants/ffff5f5f-aa6a-bb7b-cc8c-dddddd9d9d9d/applications/bbbbbbbb-cccc-dddd-2222-333333333333",
    "data": {
        "@odata.type": "microsoft.graph.onOtpSendCalloutData",
        "otpContext": {
            "identifier": "someone@example.com",
            "oneTimeCode": "12345678"
        },
        "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
        "authenticationEventListenerId": "00001111-aaaa-2222-bbbb-3333cccc4444",
        "customAuthenticationExtensionId": "11112222-bbbb-3333-cccc-4444dddd5555",
        "authenticationContext": {
            "correlationId": "aaaa0000-bb11-2222-33cc-444444dddddd",
            "client": {
                "ip": "192.168.0.0",
                "locale": "en-us",
                "market": "en-us"
            },
            "protocol": "OAUTH2.0",
            "requestType": "signUp",
            "clientServicePrincipal": {
                "id": "aaaaaaaa-bbbb-cccc-1111-222222222222",
                "appId": "00001111-aaaa-2222-bbbb-3333cccc4444",
                "appDisplayName": "My Test application",
                "displayName": "My Test application"
            },
            "resourceServicePrincipal": {
                "id": "aaaaaaaa-bbbb-cccc-1111-222222222222",
                "appId": "00001111-aaaa-2222-bbbb-3333cccc4444",
                "appDisplayName": "My Test application",
                "displayName": "My Test application"
            }
        }
    }
}
```

### Response from the external REST API

Microsoft Entra ID expects a REST API response in the following HTTP.

```http
HTTP/1.1 200 OK

Content-Type: application/json

[JSON document]
```

In the HTTP response, provide the following JSON document:

```json
{
    "data": {
        "@odata.type": "microsoft.graph.OnOtpSendResponseData",
        "actions": [
            {
                "@odata.type": "microsoft.graph.OtpSend.continueWithDefaultBehavior"
            }
        ]
    }
}
```