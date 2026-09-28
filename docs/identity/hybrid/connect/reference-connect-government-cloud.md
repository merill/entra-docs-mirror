---
layout: Conceptual
title: 'Microsoft Entra Connect: Hybrid identity considerations for Azure Government cloud - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-government-cloud
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Special considerations for deploying Microsoft Entra Connect with the Azure Government cloud.
ms.topic: reference
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 1911c3b5-5dea-d5f3-9553-db1ec1f29b0e
document_version_independent_id: 9a29cedf-3977-f46d-b633-cea0f4f68ddf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/reference-connect-government-cloud.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/reference-connect-government-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/reference-connect-government-cloud.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/15545907-caea-48c1-a546-e84930c5b845
- https://authoring-docs-microsoft.poolparty.biz/devrel/653971be-c25b-47ce-b561-80221556af0c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fd70c557-2c67-40b8-b517-cf047ce6d0c3
- https://authoring-docs-microsoft.poolparty.biz/devrel/f998336e-f087-4bda-99f7-4001451d0bd2
platformId: 75e1aa9c-f34c-1fa6-d277-a9eb8e62f5fc
---

# Microsoft Entra Connect: Hybrid identity considerations for Azure Government cloud - Microsoft Entra ID | Microsoft Learn

This article describes considerations for integrating a hybrid environment with the Microsoft Azure Government cloud. This information is provided as a reference for administrators and architects who work with the Azure Government cloud.

Note

To integrate a Microsoft Active Directory environment (either on-premises or hosted in an IaaS that is part of the same cloud instance) with the Azure Government cloud, you need to upgrade to the latest release of [Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594).

For a full list of United States government Department of Defense endpoints, refer to the [documentation](/en-us/microsoft-365/enterprise/microsoft-365-u-s-government-dod-endpoints).

## Microsoft Entra pass-through authentication

The following information describes implementation of Pass-through Authentication and the Azure Government cloud.

### Allow access to URLs

Before you deploy the Pass-through Authentication agent, verify whether a firewall exists between your servers and Microsoft Entra ID. If your firewall or proxy allows Domain Name System (DNS) blocked or safe programs, add the following connections.

Important

The following guidance applies only to the following:

- the pass-through authentication agent
- [Microsoft Entra private network connector](../../app-proxy/overview-what-is-app-proxy)

For information on URLS for the Microsoft Entra provisioning agent see the [installation pre-requisites](/en-us/azure/active-directory/cloud-sync/how-to-prerequisites) for cloud sync.

| URL | How it's used |
| --- | --- |
| \*.msappproxy.us\*.servicebus.usgovcloudapi.net | The agent uses these URLs to communicate with the Microsoft Entra cloud service. |
| `mscrl.microsoft.us:80``crl.microsoft.us:80``ocsp.msocsp.us:80``www.microsoft.us:80` | The agent uses these URLs to verify certificates. |
| login.windows.us secure.aadcdn.microsoftonline-p.com \*.microsoftonline.us \*.microsoftonline-p.us \*.msauth.net \*.msauthimages.net \*.msecnd.net\*.msftauth.net \*.msftauthimages.net\*.phonefactor.net enterpriseregistration.windows.netmanagement.azure.com policykeyservice.dc.ad.msft.netctldl.windowsupdate.us:80 | The agent uses these URLs during the registration process. |

### Install the agent for the Azure Government cloud

Follow these steps to install the agent for the Azure Government cloud:

1. In the command-line terminal, go to the folder that contains the executable file that installs the agent.
2. Run the following commands, which specify that the installation is for Azure Government.

    For Pass-through Authentication:

    ```
    AADConnectAuthAgentSetup.exe ENVIRONMENTNAME="AzureUSGovernment"
    ```

    For Application Proxy:

    ```
    MicrosoftEntraPrivateNetworkConnectorInstaller.exe ENVIRONMENTNAME="AzureUSGovernment" 
    ```

## Single sign-on

### Set up your Microsoft Entra Connect server

If you use Pass-through Authentication as your sign-on method, no additional prerequisite check is required. If you use password hash synchronization as your sign-on method and there is a firewall between Microsoft Entra Connect and Microsoft Entra ID, ensure that:

- You use Microsoft Entra Connect version 1.1.644.0 or later.
- If your firewall or proxy allows DNS blocked or safe programs, add the connections to the \*.msappproxy.us URLs over port 443.

    If not, allow access to the Azure datacenter IP ranges, which are updated weekly. This prerequisite applies only when you enable the feature. It isn't required for actual user sign-ons.

### Roll out Seamless Single Sign-On

You can gradually roll out Microsoft Entra seamless single sign-on to your users by using the following instructions. You start by adding the Microsoft Entra URL `https://autologon.microsoft.us` to all or selected users' Intranet zone settings by using Group Policy in Active Directory.

You also need to enable the intranet zone policy setting **Allow updates to status bar via script through Group Policy**.

## Browser considerations

### Mozilla Firefox (all platforms)

Mozilla Firefox doesn't automatically use Kerberos authentication. Each user must manually add the Microsoft Entra URL to their Firefox settings by following these steps:

1. Run Firefox and enter **about:config** in the address bar. Dismiss any notifications that you might see.
2. Search for the **network.negotiate-auth.trusted-uris** preference. This preference lists the sites trusted by Firefox for Kerberos authentication.
3. Right-click the preference name and then select **Modify**.
4. Enter `https://autologon.microsoft.us` in the box.
5. Select **OK** and then reopen the browser.

### Microsoft Edge based on Chromium (all platforms)

If you have overridden the `AuthNegotiateDelegateAllowlist` or `AuthServerAllowlist` policy settings in your environment, ensure that you add the Microsoft Entra URL `https://autologon.microsoft.us` to them.

### Google Chrome (all platforms)

If you have overridden the `AuthNegotiateDelegateWhitelist` or `AuthServerWhitelist` policy settings in your environment, ensure that you add the Microsoft Entra URL `https://autologon.microsoft.us` to them.