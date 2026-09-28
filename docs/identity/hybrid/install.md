---
layout: Conceptual
title: Install your synchronization tool - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/install
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes the steps required to install either cloud sync or Microsoft Entra Connect.
ms.topic: install-set-up-deploy
ms.tgt_pltfrm: na
ms.date: 2025-09-18T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 34e19887-0e3d-8843-c01f-393fde81ed31
document_version_independent_id: 58b5f7a1-dd28-70a7-cb51-0d0d8f778a40
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/install.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/install
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/install.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 638270a2-26bc-ec42-872c-17eb1886b946
---

# Install your synchronization tool - Microsoft Entra ID | Microsoft Learn

The following document provides the steps to install either cloud sync or Microsoft Entra Connect.

## Install the Microsoft Entra provisioning agent for cloud sync

Cloud sync uses the Microsoft Entra provisioning agent. Use the steps below to install it.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Select **cloud sync**
2. On the left, select **Agent**.
3. Select **Download on-premises agent**, and select **Accept terms & download**.
4. Once the **Microsoft Entra provisioning agent package** has completed downloading, run the *AADConnectProvisioningAgentSetup.exe* installation file from your downloads folder.
5. On the splash screen, select **I agree to the license and conditions**, and then select **Install**.
6. Once the installation operation completes, the configuration wizard launches. Select **Next** to start the configuration.
7. On the **Select Extension** screen, select **HR-driven provisioning (Workday and SuccessFactors) / Microsoft Entra Connect cloud sync** and select **Next**.
8. Sign in with your Microsoft Entra Hybrid Identity Administrator account.
9. On the **Configure Service Account** screen, select a group Managed Service Account (gMSA). This account is used to run the agent service. To continue, select **Next**.
10. On the **Connect Active Directory** screen, if your domain name appears under **Configured domains**, skip to the next step. Otherwise, type your Active Directory domain name, and select **Add directory**.
11. Sign in with your Active Directory domain administrator account. Select **OK**, then select **Next** to continue.
12. Select **Next** to continue.
13. On the **Configuration complete** screen, select **Confirm**.
14. Once this operation completes, you should be notified that **Your agent configuration was successfully verified.** You can select **Exit**.
15. If you still get the initial splash screen, select **Close**.

For more information, see [Installing the provisioning agent](cloud-sync/how-to-install) in the cloud sync reference section.

## Install Microsoft Entra Connect with express settings

Express settings are the default option to install Microsoft Entra Connect, and it's used for the most commonly deployed scenario.

1. Sign in as Local Administrator on the server you want to install Microsoft Entra Connect on. The server you sign in on is the sync server.
2. Go to *AzureADConnect.msi* and double-select to open the installation file.
3. On **Welcome**, select the checkbox to agree to the licensing terms, and then select **Continue**.
4. On **Express settings**, select **Use express settings**.
5. On **Connect to Microsoft Entra ID**, enter the username and password of the Hybrid Identity Administrator account, and then select **Next**.
6. On **Connect to AD DS**, enter the username and password for an Enterprise Admin account. You can enter the domain part in either NetBIOS or FQDN format, like `FABRIKAM\administrator` or `fabrikam.com\administrator`. Select **Next**
7. The [Microsoft Entra sign-in configuration](connect/plan-connect-user-signin#azure-ad-sign-in-configuration) page appears only if you didn't complete the step to [verify your domains](../../fundamentals/add-custom-domain) in the [prerequisites](connect/how-to-connect-install-prerequisites)
8. On **Ready to configure**, select **Install**
9. When the installation is finished, select **Exit**.
10. Before you use Synchronization Service Manager or Synchronization Rule Editor, sign out, and then sign in again.

For more information, see [Installing the Microsoft Entra Connect with express settings](connect/how-to-connect-install-express) in the Microsoft Entra Connect Sync reference section.

## Microsoft Entra Connect with custom settings

Use *custom settings* in Microsoft Entra Connect when you want more options for the installation.

For more information, see [Installing the Microsoft Entra Connect with custom settings](connect/how-to-connect-install-custom) in the Microsoft Entra Connect Sync reference section.