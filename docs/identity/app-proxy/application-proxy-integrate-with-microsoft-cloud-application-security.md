---
layout: Conceptual
title: Use application proxy to integrate on-premises apps with Defender for Cloud Apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-integrate-with-microsoft-cloud-application-security
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Integrate Microsoft Defender for Cloud Apps with on-premises apps published through Microsoft Entra application proxy to monitor and control user sessions.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: 6a4ce5c6-bc68-4b91-b174-33137ae0fa4e
document_version_independent_id: 8462af4a-aa5c-264a-c2dd-f715f2772c0d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-integrate-with-microsoft-cloud-application-security.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-integrate-with-microsoft-cloud-application-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-integrate-with-microsoft-cloud-application-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ed84c723-6f29-feef-7881-53d17ebd6425
---

# Use application proxy to integrate on-premises apps with Defender for Cloud Apps - Microsoft Entra ID | Microsoft Learn

## Overview

Use Microsoft Defender for Cloud Apps for real-time monitoring with on-premises application in Microsoft Entra ID. Defender for Cloud Apps uses Conditional Access App Control to monitor and control sessions in real-time based on Conditional Access policies. Apply these policies to on-premises applications that use application proxy in Microsoft Entra ID.

Some examples of the policies you create with Defender for Cloud Apps include:

- Block or protect the download of sensitive documents on unmanaged devices.
- Monitor when high-risk users sign on to applications, and then log their actions from within the session. With this information, you can analyze user behavior to determine how to apply session policies.
- Use client certificates or device compliance to block access to specific applications from unmanaged devices.
- Restrict user sessions from noncorporate networks. You can give restricted access to users accessing an application from outside your corporate network. For example, this restricted access can block the user from downloading sensitive documents.

For more information, see [Protect apps with Microsoft Defender for Cloud Apps Conditional Access App Control](/en-us/defender-cloud-apps/proxy-intro-aad).

## Prerequisites

- EMS E5 license, or Microsoft Entra ID P1 and Defender for Cloud Apps Standalone.
- The on-premises application must use Kerberos Constrained Delegation (KCD).
- Configure Microsoft Entra ID to use application proxy. Configuring application proxy includes preparing your environment and installing the private network connector. For a tutorial, see [Add an on-premises application for remote access through application proxy in Microsoft Entra ID](application-proxy-add-on-premises-application).

## Add on-premises application to Microsoft Entra ID

Add an on-premises application to Microsoft Entra ID. For a quickstart, see [Add an on-premises app to Microsoft Entra ID](application-proxy-add-on-premises-application). When adding the application, be sure to set two settings in the **Add your on-premises application** page so it works with Defender for Cloud Apps:

- **Pre Authentication**: Enter **Microsoft Entra ID**.
- **Translate URLs in Application Body**: Choose **Yes**.

## Test the on-premises application

After adding your application to Microsoft Entra ID, use the steps in [Test the application](application-proxy-add-on-premises-application#test-the-application) to add a user for testing, and test the sign-on.

## Deploy Conditional Access App Control

To configure your application with the Conditional Access Application Control, follow the instructions in [Deploy Conditional Access Application Control for Microsoft Entra apps](/en-us/defender-cloud-apps/proxy-deployment-aad).

## Test Conditional Access App Control

To test the deployment of Microsoft Entra applications with Conditional Access Application Control, follow the instructions in [Test the deployment for Microsoft Entra apps](/en-us/defender-cloud-apps/proxy-deployment-aad).