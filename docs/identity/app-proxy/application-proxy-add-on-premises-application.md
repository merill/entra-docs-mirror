---
layout: Conceptual
title: Add an on-premises application for remote access through application proxy in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-add-on-premises-application
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Learn how to prepare your environment for application proxy and add an on-premises application to your Microsoft Entra tenant.
ms.topic: tutorial
ms.date: 2026-03-10T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 861ceb04-ecea-4eb3-62b5-14163d12e3f2
document_version_independent_id: edac4607-e5d1-4d17-0af5-9ea432bfc5c6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-add-on-premises-application.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-add-on-premises-application
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-add-on-premises-application.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 152a051d-97b1-9a39-8873-3ca6a7f4c883
---

# Add an on-premises application for remote access through application proxy in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra ID has an application proxy service that enables users to access on-premises applications by signing in with their Microsoft Entra account. To learn more about application proxy, see [What is application proxy?](overview-what-is-app-proxy). This tutorial prepares your environment for use with application proxy. After your environment is ready, use the Microsoft Entra admin center to add an on-premises application to your tenant.

[![Application proxy overview diagram.](media/application-proxy-add-on-premises-application/app-proxy-diagram.png)](media/application-proxy-add-on-premises-application/app-proxy-diagram.png#lightbox)

In this tutorial, you:

- Install and verify the connector on your Windows server, and register it with application proxy.
- Add an on-premises application to your Microsoft Entra tenant.
- Grant admin consent for User.Read permission
- Verify a test user can sign in to the application by using a Microsoft Entra account.

Important

Starting June 30, 2026, Microsoft Entra application proxy no longer automatically grants admin consent for the **User.Read** delegated permission when you create a new application proxy enterprise application. You must now explicitly grant this permission after creating the application.

This change applies only to **newly created** application proxy applications. Existing applications are not affected.

## Prerequisites

To add an on-premises application to Microsoft Entra ID, you need:

- A [Microsoft Entra ID P1 or P2 subscription](https://azure.microsoft.com/pricing/details/active-directory).
- An Application Administrator account.
- A synchronized set of user identities with an on-premises directory, or identities created directly in your Microsoft Entra tenant. Identity synchronization allows Microsoft Entra ID to preauthenticate users before granting them access to application proxy published applications. Synchronization also provides the necessary user identifier information to perform single sign-on (SSO).
- An understanding of application management in Microsoft Entra. For more information, see [View enterprise applications in Microsoft Entra](../enterprise-apps/view-applications-portal).
- An understanding of single sign-on (SSO). For more information, see [Understand single sign-on](../enterprise-apps/what-is-single-sign-on).

## Install and verify the Microsoft Entra private network connector

Application proxy uses the same connector as Microsoft Entra Private Access. The connector is called Microsoft Entra private network connector. To learn how to install and verify a connector, see [How to configure connectors](../../global-secure-access/how-to-configure-connectors).

## General remarks

Public Domain Name System (DNS) records for Microsoft Entra application proxy endpoints are chained CNAME records pointing to an A record. Setting up the records this way ensures fault tolerance and flexibility. The Microsoft Entra private network connector always accesses host names with the domain suffixes `*.msappproxy.net` or `*.servicebus.windows.net`. However, during the name resolution the CNAME records might contain DNS records with different host names and suffixes.

Due to the difference, you must ensure that the device — connector server, firewall, or outbound proxy depending on your setup — can resolve all the records in the chain and allows connection to the resolved IP addresses. Since the DNS records in the chain might change from time to time, there's no fixed list of DNS records available.

If you install connectors in different regions, you should optimize traffic by selecting the closest application proxy cloud service region with each connector group. To learn more, see [Optimize traffic flow with Microsoft Entra application proxy](application-proxy-network-topology).

If your organization uses proxy servers to connect to the internet, you need to configure them for application proxy. For more information, see [Work with existing on-premises proxy servers](application-proxy-configure-connectors-with-proxy-servers).

## Add an on-premises app to Microsoft Entra ID

Add on-premises applications to Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select **New application**.
4. Select **Add an on-premises application** button, which appears about halfway down the page in the **On-premises applications** section. Alternatively, you can select **Create your own application** at the top of the page and then select **Configure application proxy for secure remote access to an on-premises application**.
5. In the **Add your own on-premises application** section, provide the following information about your application:

    | Field | Description |
    | --- | --- |
    | **Name** | The name of the application that appears on My Apps and in the Microsoft Entra admin center. |
    | **Maintenance Mode** | Select if you would like to enable maintenance mode and temporarily disable access for all users to the application. |
    | **Internal URL** | The URL for accessing the application from inside your private network. You can provide a specific path on the backend server to publish, while the rest of the server is unpublished. In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application. For example, if your app is at `https://yourapp/app` and uses images located at `https://yourapp/media`, then you should publish `https://yourapp/` as the path. This internal URL doesn't have to be the landing page your users see. For more information, see [Set a custom home page for published apps](application-proxy-configure-custom-home-page). |
    | **External URL** | The address for users to access the app from outside your network. If you don't want to use the default application proxy domain, read about [custom domains in Microsoft Entra application proxy](how-to-configure-custom-domain). |
    | **Pre Authentication** | How application proxy verifies users before giving them access to your application.**Microsoft Entra ID** - Application proxy redirects users to sign in with Microsoft Entra ID, which authenticates their permissions for the directory and application. **Keep this as the default option** so that you can take advantage of Microsoft Entra security features like Conditional Access and multifactor authentication. **Microsoft Entra ID** is required for monitoring the application with Microsoft Defender for Cloud Apps.**Passthrough** - Users don't have to authenticate against Microsoft Entra ID to access the application. You can still set up authentication requirements on the backend. |
    | **Connector Group** | Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose. If you don't have any connector groups created yet, your app is assigned to **Default**.If your application uses WebSockets to connect, all connectors in the group must be version 1.5.612.0 or later. |
6. If necessary, configure **Additional settings**. For most applications, you should keep these settings in their default states.

    | Field | Description |
    | --- | --- |
    | **Backend Application Timeout** | Set this value to **Long** only if your application is slow to authenticate and connect. At default, the backend application time-out has a length of 85 seconds. When set too long, the backend time out is increased to 180 seconds. |
    | **Use HTTP-Only Cookie** | Select to have application proxy cookies include the HTTPOnly flag in the HTTP response header. If using Remote Desktop Services, keep the option unselected. |
    | **Use Persistent Cookie** | Keep the option unselected. Only use this setting for applications that can't share cookies between processes. For more information about cookie settings, see [Cookie settings for accessing on-premises applications in Microsoft Entra ID](application-proxy-configure-cookie-settings). |
    | **Translate URLs in Headers** | Keep the option selected unless your application requires the original host header in the authentication request. |
    | **Translate URLs in Application Body** | Keep the option unselected unless HTML links are hardcoded to other on-premises applications and don't use custom domains. For more information, see [Link translation with application proxy](application-proxy-configure-hard-coded-link-translation).Select if you plan to monitor this application with Microsoft Defender for Cloud Apps. For more information, see [Configure real-time application access monitoring with Microsoft Defender for Cloud Apps and Microsoft Entra ID](application-proxy-integrate-with-microsoft-cloud-application-security). |
    | **Validate Backend TLS Certificate** | Select to enable backend Transport Layer Security (TLS) certificate validation for the application. |
7. Select **Add**.

## Grant admin consent

After creating a new application proxy application, grant admin consent for the **User.Read** delegated permission in the Microsoft Entra admin center or using the Microsoft Graph PowerShell.

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Identity** &gt; **Applications** &gt; **Enterprise applications**.
3. Select the newly created application proxy application.
4. Select **Permissions** in the left navigation.
5. Select **Grant admin consent for [your tenant]**.
6. Review the permissions and select **Accept**.

# [Microsoft Graph PowerShell](#tab/microsoft-graph-powershell)
```powershell
# Connect with the required scope
Connect-MgGraph -Scopes "Application.ReadWrite.All", "DelegatedPermissionGrant.ReadWrite.All"

# Define variables
$appObjectId = "<your-enterprise-app-object-id>"
$microsoftGraphId = "00000003-0000-0000-c000-000000000000"  # Microsoft Graph
$userReadPermissionId = "e1fe6dd8-ba31-4d61-89e7-88639da4683d"  # User.Read

# Get the service principal for your app
$sp = Get-MgServicePrincipal -Filter "id eq '$appObjectId'"

# Get the Microsoft Graph service principal
$graphSp = Get-MgServicePrincipal -Filter "appId eq '$microsoftGraphId'"

# Create the delegated permission grant
New-MgOauth2PermissionGrant -ClientId $sp.Id `
    -ConsentType "AllPrincipals" `
    -ResourceId $graphSp.Id `
    -Scope "User.Read"
```

---

### Verify the permission was granted

1. In the Microsoft Entra admin center, navigate to your enterprise application.
2. Select **Permissions**.
3. Confirm that **User.Read** appears under **Admin consent** with Type **Delegated** and Granted through **Admin consent**.

## Test the application

You're ready to test that the application was added correctly. In the following steps, you add a user account to the application, and try signing in.

### Add a user for testing

Before adding a user to the application, verify the user account already has permissions to access the application from inside the corporate network.

To add a test user:

1. Select **Enterprise applications**, and then select the application you want to test.
2. Select **Getting started**, and then select **Assign a user for testing**.
3. Under **Users and groups**, select **Add user**.
4. Under **Add assignment**, select **Users and groups**. The **Users and groups** section appears.
5. Choose the account you want to add.
6. Choose **Select**, and then select **Assign**.

### Test the sign-on

To test authentication to the application:

1. From the application you want to test, select **Application Proxy**.
2. At the top of the page, select **Test Application** to run a test on the application and check for any configuration issues.
3. First, launch the application to test signing in to it. Then download the diagnostic report to review the resolution guidance for any detected issues.

For troubleshooting, see [Troubleshoot application proxy problems and error messages](application-proxy-troubleshoot).

## Clean up resources

Delete any resources you created in this tutorial when you're done.

## Troubleshooting

Learn about common issues and how to troubleshoot them.

### Create the application/set the URLs

Check the error details for information and suggestions for how to fix the application. Most error messages include a suggested fix. To avoid common errors, verify:

- You're an administrator with permission to create an application proxy application
- The internal URL is unique
- The external URL is unique
- The URLs start with http or https, and end with a “/”
- The URL should be a domain name, not an IP address

The error message should display in the top-right corner when you create the application. You can also select the notification icon to see the error messages.

### Upload certificates for custom domains

Custom domains let you specify the domain of your external URLs. To use custom domains, you need to upload the certificate for that domain. For information on using custom domains and certificates, see [Working with custom domains in Microsoft Entra application proxy](how-to-configure-custom-domain).

If you're encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate. Common certificate problems include:

- Expired certificate
- Certificate is self-signed
- Certificate is missing the private key

The error message displays in the top-right corner as you try to upload the certificate. You can also select the notification icon to see the error messages.