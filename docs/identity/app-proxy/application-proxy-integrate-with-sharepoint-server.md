---
layout: Conceptual
title: Enable remote access to SharePoint - Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-integrate-with-sharepoint-server
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Configure Microsoft Entra application proxy to enable secure external access to on-premises SharePoint Server using Kerberos Constrained Delegation for single sign-on.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: aad211da-8b38-846c-d439-54d8d8e2f7e2
document_version_independent_id: 734c3410-a632-8248-a93a-f2e6f240633a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-integrate-with-sharepoint-server.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-integrate-with-sharepoint-server
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-integrate-with-sharepoint-server.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8d67e2c0-dde8-ce17-9e5a-00cb81f5e0ba
---

# Enable remote access to SharePoint - Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

This step-by-step guide explains how to integrate an on-premises SharePoint farm with Microsoft Entra application proxy.

## Prerequisites

To perform the configuration, you need the following resources:

- A SharePoint 2016 farm or newer.
- A Microsoft Entra tenant with a plan that includes application proxy. Learn more about [Microsoft Entra ID plans and pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing).
- A Microsoft Office Web Apps Server farm to properly launch Office files from the on-premises SharePoint farm.
- A [custom, verified domain](../../fundamentals/add-custom-domain) in the Microsoft Entra tenant.
- On-premises Active Directory deployments synchronized with Microsoft Entra Connect, through which users can [sign in to Azure](../hybrid/connect/plan-connect-user-signin).
- A private network connector installed and running on a machine within the corporate domain.

Configuring SharePoint with application proxy requires two URLs:

- An external URL, visible to end-users and determined in Microsoft Entra ID. This URL can use a custom domain. Learn more about [working with custom domains in Microsoft Entra application proxy](how-to-configure-custom-domain).
- An internal URL, known only within the corporate domain and never used directly.

Important

To make sure the links are mapped correctly, follow these recommendations for the internal URL:

- Use HTTPS.
- Don't use custom ports.
- Create a host (`A` record) in the corporate Domain Name System (DNS) that points to the SharePoint Web Front End (WFE) (or load balancer), and not an alias (`CName` record).

This article uses the following values:

- Internal URL: `https://sharepoint`.
- External URL: `https://spsites-demo1984.msappproxy.net/`.
- Application pool account for the SharePoint web application: `Contoso\spapppool`.

## Step 1: Configure an application in Microsoft Entra ID that uses application proxy

In this step, you create an application in your Microsoft Entra tenant that uses application proxy. You set the external URL and specify the internal URL, both of which are used later in SharePoint.

1. Create the app with the following settings. For step-by-step instructions, see [Publishing applications using Microsoft Entra application proxy](application-proxy-add-on-premises-application).

    - **Internal URL**: SharePoint internal URL that you set later in SharePoint, such as `https://sharepoint`.
    - **Pre-Authentication**: `Microsoft Entra ID`.
    - **Translate URLs in Headers**: `No`.
    - **Translate URLs in Application Body**: `No`.

    ![Screenshot of Microsoft Entra application proxy settings showing fields for Name, Internal URL, External URL, and Pre-Authentication set to Microsoft Entra ID.](media/application-proxy-integrate-with-sharepoint-server/publish-app.png)
2. After you publish your app, follow these steps to configure the single sign-on settings.

    1. On the application page in the portal, select **Single sign-on**.
    2. For **Single Sign-on Mode**, select **Integrated Windows Authentication**.
    3. Set **Internal Application Service Principal Name (SPN)** to the value you set earlier. For this example, the value is `HTTP/sharepoint`.
    4. Under **Delegated Login Identity**, select the most suitable option for your Active Directory forest configuration. For example, if you have a single Active Directory domain in your forest, select **On-premises SAM account name** (as shown in the following screenshot). But if your users aren't in the same domain as SharePoint and the private network connector servers, select **On-premises user principal name** (not shown in the screenshot).

    ![Screenshot of the Configure Integrated Windows Authentication dialog showing SPN set to HTTP/SharePoint and Delegated Login Identity set to On-premises SAM account name.](media/application-proxy-integrate-with-sharepoint-server/configure-iwa.png)
3. Finish setting up your application, go to the **Users and groups** section, and assign users to access this application.

## Step 2: Configure the SharePoint web application

You must configure the SharePoint web application with Kerberos and the appropriate alternate access mappings to work correctly with Microsoft Entra application proxy. You have two options:

- Create a new web application and use only the **default** zone. Use the default zone for the best experience with SharePoint. For example, the links in email alerts that SharePoint generates point to the **default** zone.
- Extend an existing web application to configure Kerberos in a nondefault zone.

Important

Regardless of the zone you use, the application pool account of the SharePoint web application must be a domain account for Kerberos to work correctly.

### Create the SharePoint web application

- The script shows an example of creating a new web application using the **default** zone. We recommend that you use the default zone.

    1. Start the **SharePoint Management Shell** and run the script.

        ```powershell
        # This script creates a web application and configures the Default zone with the internal/external URL needed to work with Microsoft Entra application proxy
        # Edit variables below to fit your environment. Note that the managed account must exist and it must be a domain account
        $internalUrl = "https://sharepoint"
        $externalUrl = "https://spsites-demo1984.msappproxy.net/"
        $applicationPoolManagedAccount = "Contoso\spapppool"
        
        $winAp = New-SPAuthenticationProvider -UseWindowsIntegratedAuthentication -DisableKerberos:$false
        $wa = New-SPWebApplication -Name "SharePoint - AAD Proxy" -Port 443 -SecureSocketsLayer -URL $externalUrl -ApplicationPool "SharePoint - AAD Proxy" -ApplicationPoolAccount (Get-SPManagedAccount $applicationPoolManagedAccount) -AuthenticationProvider $winAp
        New-SPAlternateURL -Url $internalUrl -WebApplication $wa -Zone Default -Internal
        ```
    2. Open the **SharePoint Central Administration** site.
    3. Under **System Settings**, select **Configure Alternate Access Mappings**. The **Alternate Access Mapping Collection** box opens.
    4. Filter the display with the new web application.

        ![Screenshot of Alternate Access Mappings page showing internal and public URLs for the SharePoint web application in the Default zone.](media/application-proxy-integrate-with-sharepoint-server/new-webapp-aam.png)
- If you extend an existing web application to a new zone.

    1. Start the SharePoint Management Shell and run the following script.

        ```powershell
        # This script extends an existing web application to Internet zone with the internal/external URL needed to work with Microsoft Entra application proxy
        # Edit variables below to fit your environment
        $webAppUrl = "http://spsites/"
        $internalUrl = "https://sharepoint"
        $externalUrl = "https://spsites-demo1984.msappproxy.net/"
        
        $winAp = New-SPAuthenticationProvider -UseWindowsIntegratedAuthentication -DisableKerberos:$false
        $wa = Get-SPWebApplication $webAppUrl
        New-SPWebApplicationExtension -Name "SharePoint - AAD Proxy" -Identity $wa -SecureSocketsLayer -Zone Extranet -Url $externalUrl -AuthenticationProvider $winAp
        New-SPAlternateURL -Url $internalUrl -WebApplication $wa -Zone Extranet -Internal
        ```

    Open the **SharePoint Central Administration** site.

    1. Under **System Settings**, select **Configure Alternate Access Mappings**. The **Alternate Access Mapping Collection** box opens.
    2. Filter the display with the web application that you extended.

        ![Screenshot of Alternate Access Mappings page showing internal and public URLs for Default and Extranet zones with SharePoint web application selected.](media/application-proxy-integrate-with-sharepoint-server/extend-webapp-aam.png)

### Make sure the SharePoint web application is running under a domain account

To identify the account running the application pool of the SharePoint web application and to make sure it's a domain account, follow these steps:

1. Open the **SharePoint Central Administration** site.
2. Go to **Security** and select **Configure service accounts**.
3. Select **Web Application Pool - YourWebApplicationName**.

    ![Screenshot of service account selection dialog with Web Application Pool - SharePoint 80 and domain account dropdown.](media/application-proxy-integrate-with-sharepoint-server/service-web-application.png)
4. Confirm that **Select an account for this component** returns a domain account, and remember it, since you use it in the next step.

### Make sure that an HTTPS certificate is configured for the IIS site of the extranet zone

Because the Internal URL uses HTTPS protocol (`https://SharePoint/`), you must set a certificate on the Internet Information Services (IIS) site.

1. Open the Windows PowerShell console.
2. Run the following script to generate a self-signed certificate and add it to the computer's `MY store`.

    ```powershell
    # Replace "SharePoint" with the actual hostname of the Internal URL of your Microsoft Entra proxy application
    New-SelfSignedCertificate -DnsName "SharePoint" -CertStoreLocation "cert:\LocalMachine\My"
    ```

    Important

    Self-signed certificates are suitable only for test purposes. In production environments, use certificates issued by a certificate authority instead.
3. Open the Internet Information Services Manager console.
4. Expand the server in the tree view, expand **Sites**, select the **SharePoint - Microsoft Entra ID Proxy** site, and select **Bindings**.
5. Select **https binding** and then select **Edit**.
6. In the Transport Layer Security (TLS) certificate field, choose **SharePoint** certificate and then select **OK**.

You can now access the SharePoint site externally through Microsoft Entra application proxy.

## Step 3: Configure Kerberos Constrained Delegation

Users initially authenticate in Microsoft Entra ID and then to SharePoint by using Kerberos through the Microsoft Entra private network connector. To allow the connector to obtain a Kerberos token on behalf of the Microsoft Entra user, you must configure Kerberos Constrained Delegation (KCD) with protocol transition. For more information about KCD, see [Kerberos Constrained Delegation overview](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj553400%28v=ws.11%29).

### Set the Service Principal Name (SPN) for the SharePoint service account

In this article, the internal URL is `https://sharepoint`, and so the service principal name (SPN) is `HTTP/sharepoint`. Replace those values with the values that correspond to your environment. To register SPN `HTTP/sharepoint` for the SharePoint application pool account `Contoso\spapppool`, run the following command from a command prompt, as an administrator of the domain:

`setspn -S HTTP/sharepoint Contoso\spapppool`

The `Setspn` command searches for the SPN before it adds it. If the SPN already exists, you see a **Duplicate SPN Value** error. Remove the existing SPN. Verify that the SPN was added successfully by running the `Setspn` command with the `-L` option. For more information about the command, see [Setspn](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241%28v=ws.11%29).

### Make sure the connector is trusted for delegation to the SPN that you added to the SharePoint application pool account

Configure the KCD so that the Microsoft Entra application proxy service can delegate user identities to the SharePoint application pool account. Configure KCD by enabling the private network connector to retrieve Kerberos tickets for your users who are authenticated in Microsoft Entra ID. Then, that server passes the context to the target application (SharePoint in this case).

To configure the KCD, follow these steps for each connector machine:

1. Sign in to a domain controller as a domain administrator, and then open Active Directory Users and Computers.
2. Find the computer running the Microsoft Entra private network connector. In this example, it's the computer that's running SharePoint Server.
3. Double-click the computer, and then select the **Delegation** tab.
4. Make sure the delegation options are set to **Trust this computer for delegation to the specified services only**. Then, select **Use any authentication protocol**.
5. Select the **Add** button, select **Users or Computers**, and locate the SharePoint application pool account. For example: `Contoso\spapppool`.
6. In the SPN list, select the one that you created earlier for the service account.
7. Select **OK** and then select **OK** again to save your changes.

    ![Screenshot of Delegation tab showing 'Trust this computer for delegation to specified services only' and 'Use any authentication protocol' selected.](media/application-proxy-integrate-with-sharepoint-server/delegation-box2.png)

You're now ready to sign in to SharePoint by using the external URL and to authenticate with Azure.

## Troubleshoot sign-in errors

If sign-in to the site isn't working, you can get more information about the issue in the Connector logs. From the machine running the connector, open the event viewer, go to **Applications and Services Logs** &gt; **Microsoft** &gt; **Microsoft Entra private network** &gt; **Connector**, and inspect the **Admin** log.

## Troubleshoot BadGateway Kerberos error

If you see the **BadGateway Incorrect Kerberos** error, run the following commands in Windows PowerShell in the domain controller, as an admin. Replace `[servername]` and `[serviceaccount]` with the actual values from your environment.

1. `$connector = Get-ADComputer -Identity "[servername]$"`
2. `Set-ADUser -Identity "[serviceaccount]" -PrincipalsAllowedToDelegateToAccount $connector`

[![Screenshot of error message stating 'BadGateway: The corporate app can't be accessed' due to incorrect Kerberos constrained delegation configuration.](media/application-proxy-integrate-with-sharepoint-server/bad-gateway-kerberos-error.png)](media/application-proxy-integrate-with-sharepoint-server/bad-gateway-kerberos-error.png#lightbox)