---
layout: Conceptual
title: Header-based single sign-on (SSO) for on-premises apps with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-configure-single-sign-on-with-headers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Configure header-based single sign-on for on-premises applications published through Microsoft Entra application proxy. Pass user identity attributes as HTTP headers.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 4eed8082-7b9c-c4c9-d484-8c03ba5df9ec
document_version_independent_id: fedfc485-9487-7637-5a74-79041b5f4df5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-configure-single-sign-on-with-headers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-configure-single-sign-on-with-headers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-configure-single-sign-on-with-headers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: af615e44-54bd-3102-5ca4-f8cad33fe1f8
---

# Header-based single sign-on (SSO) for on-premises apps with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra application proxy natively supports single sign-on (SSO) access to applications that use headers for authentication. You configure header values required by your application in Microsoft Entra ID. The header values are sent to the application via application proxy. Benefits to using native support for header-based authentication with application proxy include:

- **Simplify remote access to your on-premises apps** - Application proxy simplifies your existing remote access architecture. You replace Virtual Private Network (VPN) access to these apps. You remove dependencies on on-premises identity solutions for authentication. You streamline the experience for users and they don't notice anything different when they use corporate applications. Users can work from anywhere on any device.
- **No extra software or changes to your apps** - You use your existing private network connectors. No extra software is required.
- **Wide list of attributes and transformations available** - All header values available are based on standard claims that are issued by Microsoft Entra ID. All attributes and transformations available for [configuring claims for Security Assertion Markup Language (SAML) or OpenID Connect (OIDC) applications](../../identity-platform/saml-claims-customization#attributes) are also available as header values.

## Prerequisites

Enable application proxy and install a connector that has direct network access to your applications. For more information, see [Add an on-premises application for remote access through application proxy](application-proxy-add-on-premises-application).

## Supported capabilities

The table lists common capabilities required for header-based authentication applications.

| Requirement | Description |
| --- | --- |
| Federated SSO | In preauthenticated mode, all applications are protected with Microsoft Entra authentication and users have single sign-on. |
| Remote access | Application proxy provides remote access to the app. Users access the application from the internet on any web browser using the external Uniform Resource Locator (URL). Application proxy isn't intended for general corporate access. For general corporate access, see [Microsoft Entra Private Access](/en-us/entra/global-secure-access). |
| Header-based integration | Application proxy handles SSO integration with Microsoft Entra ID and then passes identity or other application data as HTTP headers to the application. |
| Application authorization | Common policies are specified based on the application being accessed, the user’s group membership, and other policies. In Microsoft Entra ID, policies are implemented using [Conditional Access](../conditional-access/overview). Application authorization policies only apply to the initial authentication request. |
| Step-up authentication | Policies are defined to force added authentication, for example, to gain access to sensitive resources. |
| Fine grained authorization | Provides access control at the URL level. Added policies can be enforced based on the URL being accessed. The internal URL configured for the app defines the scope of the app that the policy is applied to. The policy configured for the most granular path is enforced. |

Note

This article describes the connection between header-based authentication applications and Microsoft Entra ID using application proxy and is the recommended pattern. As an alternative, there's an integration pattern that uses PingAccess with Microsoft Entra ID to enable header-based authentication. For more information, see [Header-based authentication for single sign-on with application proxy and PingAccess](application-proxy-ping-access-publishing-guide).

## How it works

[![How header-based single sign-on works with application proxy.](media/application-proxy-configure-single-sign-on-with-headers/how-it-works-updated.png)](media/application-proxy-configure-single-sign-on-with-headers/how-it-works-updated.png#lightbox)

1. The admin customizes the attribute mappings required by the application in the Microsoft Entra admin center.
2. Application proxy ensures a user is authenticated using Microsoft Entra ID.
3. The application proxy cloud service is aware of the attributes required. So the service fetches the corresponding claims from the ID token received during authentication. The service then translates the values into the required HTTP headers as part of the request to the connector.
4. The request is then passed along to the connector, which is then passed to the backend application.
5. The application receives the headers and can use these headers as needed.

## Publish the application with application proxy

1. Publish your application according to the instructions in [Publish applications with application proxy](application-proxy-add-on-premises-application).

    - The internal URL value determines the scope of the application. You configure the internal URL value at the root path of the application, and all sub paths underneath the root receive the same header and application configuration.
    - Create a new application to set a different header configuration or user assignment for a more granular path than the application you configured. In the new application, configure the internal URL with the specific path you require and then configure the specific headers needed for this URL. Application proxy always matches your configuration settings to the most granular path set for an application.
2. Select **Microsoft Entra ID** as the **pre-authentication method**.
3. Assign a test user by navigating to **Users and groups** and assigning the appropriate users and groups.
4. Open a browser and navigate to the **External URL** from the application proxy settings.
5. Verify that you can connect to the application. Even though you can connect, you can't access the app yet since the headers aren't configured.

## Configure single sign-on

Before you get started with single sign-on for header-based applications, install a private network connector. The connector must be able to access the target applications. For more information, see [Tutorial: Microsoft Entra application proxy](application-proxy-add-on-premises-application).

1. After your application appears in the list of enterprise applications, select it, and select **Single sign-on**.
2. Set the single sign-on mode to **Header-based**.
3. In **Basic Configuration**, **Microsoft Entra ID** is selected as the default.
4. In **Headers**, select the edit pencil to configure the headers to send to the application.
5. Select **Add new header**. Provide a name for the header, select either **Attribute** or **Transformation**, and then select from the drop-down which header your application needs.
    - To learn more about the list of available attributes, see [Claims Customizations- Attributes](../../identity-platform/saml-claims-customization#attributes).
    - To learn more about the list of available transformations, see [Claims Customizations- Claim Transformations](../../identity-platform/saml-claims-customization#claim-transformations).
    - You can also add a **Group Header**. For more information about configuring groups, see [Configure group claims for applications](../hybrid/connect/how-to-connect-fed-group-claims#add-group-claims-to-tokens-for-saml-applications-using-sso-configuration).
6. Select **Save**.

## Test your app

The application is now running and available. To test the app:

1. Clear previously cached headers by opening a new browser or private browser window.
2. Navigate to the external URL. You can find this setting listed as **External URL** in application proxy settings.
3. Sign in with the test account that you assigned to the app.
4. Confirm you can load and sign into the application using SSO.

## Considerations

- Application proxy provides remote access to on-premises apps or apps on a private cloud. Application proxy isn't recommended for traffic originating inside the same network as the intended application.
- **Access to header-based authentication applications should be restricted to only traffic from the connector or other permitted header-based authentication solution**. Access restriction is commonly performed using a firewall or IP restriction on the application server.