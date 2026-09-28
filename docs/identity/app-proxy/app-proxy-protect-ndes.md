---
layout: Conceptual
title: Use Microsoft Entra application proxy with a Network Device Enrollment Service (NDES) server - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/app-proxy-protect-ndes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Secure NDES certificate enrollment for mobile devices using Microsoft Entra application proxy. Includes connector setup and certificate request validation.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: f49a9221-b949-95db-f53b-ba6bd4337000
document_version_independent_id: c170ba58-5d57-90e4-10ff-e9f4c0546d0f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/app-proxy-protect-ndes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/app-proxy-protect-ndes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/app-proxy-protect-ndes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 2eb6e9c9-7b88-0eb2-ba52-6c30189dc74d
---

# Use Microsoft Entra application proxy with a Network Device Enrollment Service (NDES) server - Microsoft Entra ID | Microsoft Learn

## Overview

Learn how to use Microsoft Entra application proxy to protect your Network Device Enrollment Service (NDES).

## Install and register the connector on the NDES server

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Select your username in the upper-right corner. Verify you're signed in to a directory that uses application proxy. If you need to change directories, select **Switch directory** and choose a directory that uses application proxy.
3. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application proxy**.
4. Select **Download connector service**. ![Download connector service to see the Terms of Service.](media/app-proxy-protect-ndes/application-proxy-download-connector-service.png)
5. Read the Terms of Service. When you're ready, select **Accept terms & Download**.
6. Copy the Microsoft Entra private network connector setup file to your NDES server.

> 
> You install the connector on any server within your corporate network with access to NDES. You don't have to install it on the NDES server itself.
7. Run the setup file, such as *MicrosoftEntraPrivateNetworkConnectorInstaller.exe*. Accept the software license terms.
8. During the install, you're prompted to register the connector with application proxy in your Microsoft Entra directory. Provide the credentials for an Application Administrator in your Microsoft Entra directory. The Microsoft Entra Application Administrator credentials are often different from your Azure credentials in the portal.

    Note

    The account with the Application Administrator role used to register the connector must belong to the same directory where you enable the application proxy service.

    For example, if the Microsoft Entra domain is *contoso.com*, the Application Administrator should be `admin@contoso.com` or another valid alias on that domain.

    If Internet Explorer Enhanced Security Configuration is turned on for the server where you install the connector, the registration screen might be blocked. To allow access, follow the instructions in the error message, or turn off Internet Explorer Enhanced Security during the install process.

    If connector registration fails, see [Troubleshoot application proxy](application-proxy-troubleshoot).
9. At the end of the setup, a note is shown for environments with an outbound proxy. To configure the Microsoft Entra private network connector to work through the outbound proxy, run the provided script, such as `C:\Program Files\Microsoft Entra private network connector\ConfigureOutBoundProxy.ps1`.
10. On the Application proxy page in the Microsoft Entra admin center, the new connector is listed with a status of *Active*, as shown in the example. ![The new Microsoft Entra private network connector shown as active in the Microsoft Entra admin center.](media/app-proxy-protect-ndes/connected-app-proxy.png)

    Note

    To provide high availability for applications authenticating through the Microsoft Entra application proxy, you can install connectors on multiple VMs. Repeat the same steps listed in the previous section to install the connector on other servers joined to the Microsoft Entra Domain Services managed domain.
11. After successful installation, go back to the Microsoft Entra admin center.
12. Select **Enterprise applications**. ![Ensure that you're engaging the right stakeholders.](media/app-proxy-protect-ndes/enterprise-applications.png)
13. Select **+New Application**, and then select **On-premises application**.
14. On the **Add your own on-premises application**, configure the fields.

    **Name**: Enter a name for the application.

    **Internal Url**: Enter the internal URL/FQDN of your NDES server on which you installed the connector.

    **Pre Authentication**: Select **Passthrough**. It’s not possible to use any form of preauthentication. The protocol used for certificate requests, Simple Certificate Enrollment Protocol (SCEP), doesn't provide such option.

    Copy the provided **External URL** to your clipboard.
15. Select **+Add** to save your application.
16. Test whether you can access your NDES server via the Microsoft Entra application proxy by pasting the link you copied in step 15 into a browser. You should see a default Internet Information Services (IIS) welcome page.
17. As a final test, add the *mscep.dll* path to the existing URL you pasted in the previous step. `https://scep-test93635307549127448334.msappproxy.net/certsrv/mscep/mscep.dll`
18. You should see an **HTTP Error 403 – Forbidden** response.
19. Change the NDES URL provided (via Microsoft Intune) to devices. This change could either be in Microsoft Configuration Manager or the Microsoft Intune admin center.

    - For Configuration Manager, go to the certificate registration point and adjust the URL. This URL is what devices call out to and present their challenge.
    - For Intune standalone, either edit or create a new SCEP policy and add the new URL.