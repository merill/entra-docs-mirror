---
layout: Conceptual
title: Configure Microsoft Entra Global Secure Access with Infoblox - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-infoblox-coexistence
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: lirazbarak
ms.author: lirazb
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure Microsoft Entra Private Access and Infoblox Threat Defense together for private application access and DNS security.
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 2026-10-21T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a6a10e43-25b9-c853-4195-dbddbbf1ac68
document_version_independent_id: a6a10e43-25b9-c853-4195-dbddbbf1ac68
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-infoblox-coexistence.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-infoblox-coexistence
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-infoblox-coexistence.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: dc9c3692-256b-cd46-31ce-325ac6607dc1
---

# Configure Microsoft Entra Global Secure Access with Infoblox - Global Secure Access | Microsoft Learn

This article describes how to configure Microsoft Entra Global Secure Access with Infoblox Threat Defense so private application traffic and DNS security work together.

## Overview

In today's rapidly evolving digital landscape, organizations require robust and unified solutions to ensure secure and seamless connectivity. Microsoft and Infoblox offer complementary Secure Access Service Edge (SASE) and Threat Defense security capabilities that, when integrated, provide enhanced security and connectivity for diverse access scenarios.

This guide outlines how to configure and deploy Microsoft Entra solutions alongside Infoblox's Threat Defense offerings. By using the strengths of both platforms, you can optimize your organization's security posture while maintaining high-performance connectivity for private applications, Microsoft 365 traffic, and internet access.

## Prerequisites

Before you begin:

- Set up Microsoft Entra Private Access and Infoblox Threat Defense DNS security.
- Configure the Global Secure Access fully qualified domain name (FQDN) and IP bypasses for coexistence.

## Prepare Microsoft Entra Private Access

Configure Microsoft Entra Private Access so Global Secure Access can handle private application traffic.

1. Enable the [Microsoft Entra Private Access traffic forwarding profile](how-to-manage-private-access-profile).
2. Install a [Private Network Connector](how-to-configure-connectors) for Microsoft Entra Private Access.

    Note

    Private Network Connectors are required for Microsoft Entra Private Access applications.
3. Configure Global Secure Access Enterprise Applications and Quick Access for your private resources, and set up Private DNS and DNS suffixes. For more information, see [How to configure Quick Access](how-to-configure-quick-access).
4. Install and configure the [Global Secure Access client for Windows](how-to-install-windows-client) or [Global Secure Access client for macOS](how-to-install-macos-client).

## Create Infoblox Threat Defense Internal Domains

Create Internal Domain lists to bypass Infoblox DNS for Global Secure Access and private application FQDNs. For more information, see [Configuring Internal Domains](https://docs.infoblox.com/space/BloxOneThreatDefense/35437388/Configuring+Internal+Domains).

1. In the Infoblox portal, go to **Configure** &gt; **Security** &gt; **Internal Domains**, and select **Create Internal Domain**.
2. Create an Internal Domain list named `MSFT GSA`. Add `globalsecureaccess.microsoft.com`, and then select **Save & Close**.
3. Create another Internal Domain list for the FQDNs of your private application app segments in the Microsoft Entra portal. For example, if a private application for a Remote Desktop Protocol (RDP) server uses the FQDN `termsrv.example.com`, add that FQDN to the list.
4. Add the FQDNs for your private applications, such as `termsrv.example.com` and `smb.example.com`, and save the list as `Private Apps`.

## Create an Infoblox Threat Defense category filter

Create a category filter to test Infoblox category filtering alongside Global Secure Access. For more information, see the Infoblox [Filters documentation](https://docs.infoblox.com/space/BloxOneThreatDefense/35469571/Filters).

1. In the Infoblox portal, go to **Configure** &gt; **Security** &gt; **Policies** &gt; **Filters**.
2. Select **Create Filter** &gt; **Create Category Filter**.
3. Enter a name, such as `Block Real Estate`, select a category, such as **Real Estate**, and then select **Save & Close**.

Use this filter when you configure the security policy.

## Configure an Infoblox Endpoint Group and security policy

Create an Endpoint Group that uses the Internal Domain lists, then create a security policy to apply the category filter to that group. For more information, see [Creating Endpoint Groups](https://docs.infoblox.com/space/BloxOneThreatDefense/35473957/Creating+Endpoint+Groups) and [Configuring Security Policies](https://docs.infoblox.com/space/BloxOneThreatDefense/35371559/Configuring+Security+Policies).

Note

If you have multiple policy rules, make sure the category filter rule order enforces the filter. Also make sure the security policy precedence doesn't prevent users from receiving the correct Infoblox policy for coexistence.

1. In the Infoblox portal, go to **Configure** &gt; **Security** &gt; **Endpoints**.
2. Select **Endpoint Groups** &gt; **Create**.
3. Name the Endpoint Group, such as `GSA endpoints`, and expand **Internal Domain Lists**.
4. Select **Add**, select `MSFT GSA` and `Private Apps`, and then select **Save & Close**. Leave the other settings at their defaults.
5. Go to **Configure** &gt; **Security** &gt; **Policies**, and select **Create Security Policy**.
6. Enter a name for the policy, such as `GSA policy`.
7. On the **Network Scope** page, select **Add Source** &gt; **Endpoint Groups**.
8. Select `GSA endpoints` from **Available Endpoint Groups**, and select the arrow to move it to the **Selected** section.
9. On the **Policy Rules** page, select **Add Rule** &gt; **Category Filter**.
10. Select **Object** &gt; `Block Real Estate` &gt; **Select**.
11. Set **Action** to **Block**, set **Default Redirect**, and select **Finish**.
12. Install the Infoblox BloxOne Endpoint software on end-user devices. For more information, see [Managing Endpoint](https://docs.infoblox.com/space/BloxOneThreatDefense/35374260/Managing+Endpoint). For standalone installation instructions for Windows and macOS, see [Standalone Deployment](https://docs.infoblox.com/space/BloxOneThreatDefense/35436945/Standalone+Deployment).
13. Check the system tray to make sure the Global Secure Access and Infoblox clients are enabled.

## Verify the client configuration and traffic flow

Verify the client configuration and test traffic to confirm that Global Secure Access handles private application traffic and Infoblox handles DNS activity for internet sites.

1. Right-click the **Global Secure Access Client**, select **Advanced Diagnostics** &gt; **Forwarding Profile**, and verify that Private Access and Private DNS rules are applied to the client.
2. In **Advanced Diagnostics**, select **Health Check** and make sure no checks are failing.
3. Select the Infoblox Endpoint system tray icon and verify that the status is **Protected**.

    Note

    For information about troubleshooting health check failures, see [Troubleshoot the Global Secure Access client: Health check](troubleshoot-global-secure-access-client-diagnostics-health-check).
4. In the system tray, right-click **Global Secure Access Client**, select **Advanced Diagnostics**, select the **Traffic** tab, and select **Start collecting**.
5. In a browser, access `bing.com`, `salesforce.com`, and `Instagram.com`.
6. In **Advanced Diagnostics**, select the **Traffic** tab and verify that the Global Secure Access client isn't capturing traffic from these websites.
7. In the Microsoft Entra admin center, go to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Verify that traffic for these sites is missing from the Global Secure Access traffic logs.
8. In the Infoblox portal, go to **Monitor** &gt; **Reports** &gt; **Security** &gt; **DNS Activity**. Verify that traffic for these sites is present in Infoblox logs.
9. Access a private application configured in Microsoft Entra Private Access, such as a file share over Server Message Block (SMB).
10. In the Microsoft Entra admin center, go to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. Verify that traffic for the file share is captured in the Global Secure Access traffic logs.
11. In the Infoblox portal, go to **Monitor** &gt; **Reports** &gt; **Security** &gt; **DNS Activity**. Verify that traffic for the private application isn't present in the traffic logs.
12. In the system tray, right-click **Global Secure Access Client**, select **Advanced Diagnostics**, and in the **Traffic** dialog box, select **Stop collecting**.
13. Verify that the Global Secure Access client handled only private application traffic.