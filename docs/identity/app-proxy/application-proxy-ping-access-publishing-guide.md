---
layout: Conceptual
title: Header-based authentication with PingAccess for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-ping-access-publishing-guide
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Support header-based authentication with PingAccess and Microsoft Entra application proxy.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: de76ed4d-ce63-7f13-9646-1109696663d6
document_version_independent_id: facaf5f5-f66a-fb0f-9a40-dec50f972b55
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-ping-access-publishing-guide.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-ping-access-publishing-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-ping-access-publishing-guide.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: a7f6a466-b19f-9268-7612-1adfbcb27e93
---

# Header-based authentication with PingAccess for Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft partnered with PingAccess to provide more access applications. PingAccess provides another option beyond integrated [header-based single sign-on](application-proxy-configure-single-sign-on-with-headers).

## What's PingAccess for Microsoft Entra ID?

With PingAccess for Microsoft Entra ID, you give users access and single sign-on (SSO) to applications that use headers for authentication. Application proxy treats these applications like any other, using Microsoft Entra ID to authenticate access and then passing traffic through the connector service. PingAccess sits in front of the applications and translates the access token from Microsoft Entra ID into a header. The application then receives the authentication in the format it can read.

Users don't notice anything different when they sign in to use corporate applications. Applications still work from anywhere on any device. The private network connectors direct remote traffic to all apps without regard to their authentication type, so they still balance loads automatically.

## How do I get access?

You need a license for PingAccess and Microsoft Entra ID. However, Microsoft Entra ID P1 or P2 subscriptions include a basic PingAccess license that covers up to 20 applications. If you need to publish more than 20 header-based applications, you can purchase more licenses from PingAccess.

For more information, see [Microsoft Entra editions](../../fundamentals/licensing).

## Publish your application in Microsoft Entra

This article outlines the steps to publish an application for the first time. The article provides guidance for both application proxy and PingAccess.

Note

Some of the instructions exist on the Ping Identity site.

### Install a private network connector

The private network connector is a Windows Server service that directs traffic from your remote employees to your published applications. For more detailed installation instructions, see [Tutorial: Add an on-premises application for remote access through application proxy in Microsoft Entra ID](application-proxy-add-on-premises-application).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application proxy**.
3. Select **Download connector service**.
4. Follow the installation instructions.

Downloading the connector should automatically enable application proxy for your directory, but if not, you can select **Enable application proxy**.

### Add your application to Microsoft Entra ID with application proxy

There are two steps to add your application to Microsoft Entra ID. First, you need to publish your application with application proxy. Then, you need to collect information about the application that you can use during the PingAccess steps.

#### Publish your application

First, publish your application. This action involves:

- Adding your on-premises application to Microsoft Entra ID.
- Assigning a user for testing the application and choosing header-based single sign-on.
- Setting up the application's redirect URL.
- Granting permissions for users and other applications to use your on-premises application.

To publish your own on-premises application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an Application Administrator.
2. Browse to **Enterprise applications** &gt; **New application** &gt; **Add an on-premises application**. The **Add your own on-premises application** page appears.

    ![Application configuration form with fields for name, internal URL, and external URL settings.](media/application-proxy-configure-single-sign-on-with-ping-access/add-your-own-on-premises-application.png)
3. Fill in the required fields with information about your new application. Use the guidance for the settings.

    Note

    For a more detailed walkthrough of this step, see [Add an on-premises app to Microsoft Entra ID](application-proxy-add-on-premises-application).

    1. **Internal URL**: Normally you provide the URL that takes you to the app's sign-in page when you're on the corporate network. For this scenario, the connector needs to treat the PingAccess proxy as the front page of the application. Use this format: `https://<host name of your PingAccess server>:<port>`. The port is 3000 by default, but you can configure it in PingAccess.

        Warning

        For this type of single sign-on, the internal URL must use `https` and not `http`. Also, no two applications should have the same internal URL so application proxy can maintain a distinction between them.
    2. **Pre authentication method**: Choose **Microsoft Entra ID**.
    3. **Translate URL in Headers**: Choose **No**.

    Note

    For the first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration. For subsequent applications, the port needs to match the Listener configured in PingAccess.
4. Select **Add**. The overview page for the new application appears.

Now assign a user for application testing and choose header-based single sign-on:

1. From the application sidebar, select **Users and groups** &gt; **Add user** &gt; **Users and groups (&lt;Number&gt; Selected)**. A list of users and groups appears for you to choose from.

    ![Users and groups assignment page for the application.](media/application-proxy-configure-single-sign-on-with-ping-access/users-and-groups.png)
2. Select a user for application testing, and select **Select**. Make sure the test account has access to the on-premises application.
3. Select **Assign**.
4. From the application sidebar, select **Single sign-on** &gt; **Header-based**.

    Tip

    Install PingAccess the first time you use header-based single sign-on. To make sure your Microsoft Entra subscription is automatically associated with your PingAccess installation, use the link on the single sign-on page to download PingAccess. You can open the download site now, or come back to this page later.

    ![Header-based sign-on configuration page with PingAccess download link.](media/application-proxy-configure-single-sign-on-with-ping-access/sso-header.png)
5. Select **Save**.

Then make sure your redirect URL is set to your external URL:

1. Browse to **Entra ID** &gt; **App registrations** and select your application.
2. Select the link next to **Redirect URIs**. The link shows the amount of redirect Uniform Resource Identifiers (URIs) setup for web and public clients. The **&lt;application name&gt; - Authentication** page appears.
3. Check whether the external URL that you assigned to your application earlier is in the **Redirect URIs** list. If it isn't, add the external URL now, using a redirect URI type of **Web**, and select **Save**.

In addition to the external URL, an authorize endpoint of Microsoft Entra ID on the external URL should be added to the Redirect URIs list.

`https://*.msappproxy.net/pa/oidc/cb``https://*.msappproxy.net/`

Finally, set up the on-premises application so that users have `read` access and other applications have `read/write` access:

1. From the **App registrations** sidebar for your application, select **API permissions** &gt; **Add a permission** &gt; **Microsoft APIs** &gt; **Microsoft Graph**. The **Request API permissions** page for **Microsoft Graph** appears, which contains the permissions for Microsoft Graph.

    ![Request API permissions page for Microsoft Graph API selection.](media/application-proxy-configure-single-sign-on-with-ping-access/required-permissions.png)
2. Select **Delegated permissions** &gt; **User** &gt; **User.Read**.
3. Select **Application permissions** &gt; **Application** &gt; **Application.ReadWrite.All**.
4. Select **Add permissions**.
5. In the **API permissions** page, select **Grant admin consent for &lt;your directory name&gt;**.

#### Collect information for the PingAccess steps

Collect three Globally Unique Identifiers (GUIDs). Use the GUIDs to set up your application with PingAccess.

| Name of Microsoft Entra field | Name of PingAccess field | Data format |
| --- | --- | --- |
| **Application (client) ID** | **Client ID** | GUID |
| **Directory (tenant) ID** | **Issuer** | GUID |
| `PingAccess key` | **Client Secret** | Random string |

To collect this information:

1. Browse to **Entra ID** &gt; **App registrations** and select your application.
2. Next to the **Application (client) ID** value, select the **Copy to clipboard** icon, then copy and save it. You specify this value later as PingAccess's client ID.
3. Next the **Directory (tenant) ID** value, also select **Copy to clipboard**, then copy and save it. You specify this value later as PingAccess's issuer.
4. From the sidebar of the **App registrations** for your application, select **Certificates and secrets** &gt; **New client secret**. The **Add a client secret** page appears.

    ![Client secret creation form with expiration settings.](media/application-proxy-configure-single-sign-on-with-ping-access/add-a-client-secret.png)
5. In **Description**, type `PingAccess key`.
6. Under **Expires**, choose how to set the PingAccess key: **In 1 year**, **In 2 years**, or **Never**.
7. Select **Add**. The PingAccess key appears in the table of client secrets, with a random string that autofills in the **VALUE** field.
8. Next to the PingAccess key's **VALUE** field, select the **Copy to clipboard** icon, then copy and save it. You specify this value later as PingAccess's client secret.

**Update the `acceptMappedClaims` field:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Select your username in the upper-right corner. Verify you're signed in to a directory that uses application proxy. If you need to change directories, select **Switch directory** and choose a directory that uses application proxy.
3. Browse to **Entra ID** &gt; **App registrations** and select your application.
4. From the sidebar of the **App registrations** page for your application, select **Manifest**. The manifest JSON code for your application's registration appears.
5. Search for the `acceptMappedClaims` field, and change the value to `True`.
6. Select **Save**.

### Use of optional claims (optional)

Optional claims allow you to add standard-but-not-included-by-default claims that every user and tenant has. You can configure optional claims for your application by modifying the application manifest. For more info, see the [Understanding the Microsoft Entra application manifest article](../../identity-platform/reference-app-manifest).

Example to include email address into the access\_token that PingAccess consumes:

```json
    "optionalClaims": {
        "idToken": [],
        "accessToken": [
            {
                "name": "email",
                "source": null,
                "essential": false,
                "additionalProperties": []
            }
        ],
        "saml2Token": []
    },
```

### Use of claims mapping policy (optional)

Claims mapping lets you migrate old on-premises apps to the cloud by adding more custom claims that back your Active Directory Federation Services (ADFS) or user objects. For more information, see [Claims Customization](/en-us/entra/identity-platform/reference-claims-mapping-policy-type#claims-customization-using-a-policy).

To use a custom claim and include more fields in your application. [Created a custom claims mapping policy and assigned it to the application](../../identity-platform/saml-claims-customization).

Note

To use a custom claim, you must also have a custom policy defined and assigned to the application. The policy should include all required custom attributes.

You can do policy definition and assignment through PowerShell or Microsoft Graph. If you're doing them in PowerShell, you need to first use `New-AzureADPolicy` and then assign it to the application with `Add-AzureADServicePrincipalPolicy`. For more information, see [Claims mapping policy assignment](../../identity-platform/saml-claims-customization).

Note

Azure AD and MSOnline PowerShell modules are deprecated as of March 30, 2024. To learn more, read the [deprecation update](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/important-azure-ad-graph-retirement-and-powershell-module/ba-p/3848270). After this date, support for these modules are limited to migration assistance to Microsoft Graph PowerShell SDK and security fixes. The deprecated modules will continue to function through March, 30 2025.

We recommend migrating to [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview) to interact with Microsoft Entra ID (formerly Azure AD). For common migration questions, refer to the [Migration FAQ](/en-us/powershell/azure/active-directory/migration-faq). *Note:* Versions 1.0.x of MSOnline may experience disruption after June 30, 2024.

Example:

```powershell
$pol = New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","JwtClaimType":"employeeid"}]}}') -DisplayName "AdditionalClaims" -Type "ClaimsMappingPolicy"

Add-AzureADServicePrincipalPolicy -Id "<<The object Id of the Enterprise Application you published in the previous step, which requires this claim>>" -RefObjectId $pol.Id
```

### Enable PingAccess to use custom claims

Enabling PingAccess to use custom claims is optional, but required if you expect the application to consume more claims.

When you configure PingAccess in the following step, the Web Session you create (Settings-&gt;Access-&gt;Web Sessions) must have **Request Profile** deselected and **Refresh User Attributes** set to **No**.

## Download PingAccess and configure your application

The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation.

To create a Microsoft Entra ID OpenID Connect (OIDC) connection, set up a token provider with the **Directory (tenant) ID** value that you copied from the Microsoft Entra admin center. Create a web session on PingAccess. Use the `Application (client) ID` and `PingAccess key` values. Set up identity mapping and create a virtual host, site, and application.

### Test your application

The application is up and running. To test it, open a browser and navigate to the external URL that you created when you published the application in Microsoft Entra. Sign in with the test account you assigned to the application.