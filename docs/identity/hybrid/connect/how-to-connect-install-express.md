---
layout: Conceptual
title: 'Microsoft Entra Connect Sync: Get started by using express settings - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-express
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to download, install, and run the setup wizard for Microsoft Entra Connect Sync.
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4f7c88b3-131c-9f98-94df-b8308502a4bf
document_version_independent_id: 9c90bdab-00aa-193a-ac46-719de2f6b2d6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-install-express.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-install-express
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-install-express.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7ac9db1d-15ab-1fd5-4e79-3a2fbc34b89b
---

# Microsoft Entra Connect Sync: Get started by using express settings - Microsoft Entra ID | Microsoft Learn

If you have a single-forest topology and use [password hash sync](how-to-connect-password-hash-synchronization) for authentication, express settings are a good option to use when you install Microsoft Entra Connect Sync. Express settings the default option to install Microsoft Entra Connect Sync, and it's used for the most commonly deployed scenario. It's only a few short steps to extend your on-premises directory to the cloud.

Before you start installing Microsoft Entra Connect Sync, [download Microsoft Entra Connect Sync](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted), and be sure to complete the prerequisite steps in [Microsoft Entra Connect: Hardware and prerequisites](how-to-connect-install-prerequisites).

If the express settings installation doesn't match your topology, see Related articles for information about other scenarios.

## TLS 1.2 enforcement for Microsoft Entra Connect Sync

Transport Layer Security (TLS) protocol version 1.2 is a cryptography protocol that is designed to provide secure communications. The TLS protocol aims primarily to provide privacy and data integrity. TLS has gone through many iterations, with version 1.2 being defined in [RFC 5246](https://tools.ietf.org/html/rfc5246). The latest version of Microsoft Entra Connect Sync fully supports using only TLS 1.2 for communications with Microsoft Entra ID. Before installing the latest versions of Microsoft Entra Connect Sync, be sure to enable TLS 1.2.

[![Screenshot of TLS warning screen.](media/how-to-connect-install-express/install-10.png)](media/how-to-connect-install-express/install-10.png#lightbox)

For more information see [TLS 1.2 enforcement for Microsoft Entra Connect Sync](reference-connect-tls-enforcement)

## Express installation of Microsoft Entra Connect Sync

1. Sign in as Local Administrator on the server you want to install Microsoft Entra Connect on. The server you sign in on will be the sync server.
2. Go to *AzureADConnect.msi* and double-click to open the installation file.
3. In **Welcome**, select the checkbox to agree to the licensing terms, and then select **Continue**.

[![Screenshot that shows the welcome page in the Microsoft Entra Connect Sync installation wizard.](media/how-to-connect-install-express/install-3.png)](media/how-to-connect-install-express/install-3.png#lightbox)

1. In **Express settings**, select **Use express settings**.

[![Screenshot of Express settings.](media/how-to-connect-install-express/install-4.png)](media/how-to-connect-install-express/install-4.png#lightbox)

1. In **Connect to Microsoft Entra ID**, enter the username and password of the Hybrid Identity Administrator account, and then select **Next**.

[![Screenshot that shows the Connect to Microsoft Entra ID page in the installation wizard.](media/how-to-connect-install-express/install-5.png)](media/how-to-connect-install-express/install-5.png#lightbox)

1. In **Connect to AD DS**, enter the username and password for an Enterprise Admin account. You can enter the domain part in either NetBIOS or FQDN format, like `FABRIKAM\administrator` or `fabrikam.com\administrator`. Select **Next**.

[![Screenshot that shows the Connect to AD DS page in the installation wizard.](media/how-to-connect-install-express/install-6.png)](media/how-to-connect-install-express/install-6.png#lightbox)

1. The [Microsoft Entra ID sign-in configuration](plan-connect-user-signin#azure-ad-sign-in-configuration) page appears only if you didn't complete the step to [verify your domains](../../../fundamentals/add-custom-domain) in the [prerequisites](how-to-connect-install-prerequisites).

[![Screenshot that shows examples of unverified domains in the installation wizard.](media/how-to-connect-install-express/install-7.png)](media/how-to-connect-install-express/install-7.png#lightbox)

If you see this page, review each domain that's marked **Not Added** or **Not Verified**. Make sure that those domains have been verified in Microsoft Entra ID. When you've verified your domains, select the **Refresh** icon.

1. In **Ready to configure**, select **Install**.

- Optionally in **Ready to configure**, you can clear the **Start the synchronization process as soon as configuration completes** checkbox. You should clear this checkbox if you want to do more configurations, such as to add [filtering](how-to-connect-sync-configure-filtering). If you clear this option, the wizard configures sync but leaves the scheduler disabled. The scheduler doesn't run until you enable it manually by [rerunning the installation wizard](how-to-connect-installation-wizard).
- If you leave the **Start the synchronization process when configuration completes** checkbox selected, a full sync of all users, groups, and contacts to Microsoft Entra ID begins immediately.
- If you have Exchange in your instance of Windows Server Active Directory, you also have the option to enable [Exchange Hybrid deployment](/en-us/exchange/exchange-hybrid). Enable this option if you plan to have Exchange mailboxes both in the cloud and on-premises at the same time.

    [![Screenshot that shows the Ready to configure Microsoft Entra Connect Sync page in the wizard.](media/how-to-connect-install-express/install-8.png)](media/how-to-connect-install-express/install-8.png#lightbox)

1. When the installation is finished, select **Exit**.

[![Screenshot that shows installation was successful.](media/how-to-connect-install-express/install-9.png)](media/how-to-connect-install-express/install-9.png#lightbox)

1. Before you use Synchronization Service Manager or Synchronization Rule Editor, sign out, and then sign in again.