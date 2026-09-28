---
layout: Conceptual
title: 'Troubleshoot the Global Secure Access Mobile Client: Advanced Diagnostics - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Discover how to use advanced diagnostics to resolve issues with the Global Secure Access mobile client for Android and iOS.
ms.topic: troubleshooting
ms.date: 2026-03-09T00:00:00.0000000Z
ms.reviewer: cagautham
ai-usage: ai-assisted
locale: en-us
document_id: bc828731-cc29-4d1b-1dee-44d73c55ad73
document_version_independent_id: bc828731-cc29-4d1b-1dee-44d73c55ad73
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ce5ffe65-41a3-024a-cbe5-9f7ffaa07802
---

# Troubleshoot the Global Secure Access Mobile Client: Advanced Diagnostics - Global Secure Access | Microsoft Learn

This article explains how to troubleshoot the Global Secure Access mobile client for Android and iOS using the advanced diagnostics utility.

## Introduction

The Global Secure Access client runs in the background and routes relevant network traffic to Global Secure Access. It doesn't require user interaction. The advanced diagnostics tool makes the client's behavior visible to the administrator and helps with troubleshooting.

## Services section

The **Services** section shows the active services running in the traffic forwarding profiles.

![Screenshot of the Services section in the Global Secure Access mobile client.](media/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics/services-section.png)

## Troubleshooting section

The Troubleshooting section enables users to troubleshoot and share information with the administrator. To view the **Troubleshooting** section:

1. Open the Microsoft Defender app and select the **Global Secure Access client** tile.
2. Select the **Troubleshooting** section to open it.

In addition to **Get latest policy** and **Clear cached data**, users can also collect and send logs and run advanced diagnostics.

### Collect and send logs

This troubleshooting function allows users to collect logs from the client and send the logs to Microsoft support for investigation. To access the **Collect and send logs** function:

1. Open the Microsoft Defender app and select the **Global Secure Access client** tile.
2. Expand the **Troubleshooting** section and select **Collect and send logs**.

The user can copy and share the Incident ID with Microsoft Support for their reference.

![Screenshot of a sample pop-up Incident ID message.](media/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics/incident-id.png)

### Advanced diagnostics

This troubleshooting function shows the client's health and lets users capture network and hostname traffic. To access the **Advanced diagnostics** function:

1. Open the Microsoft Defender app and select the **Global Secure Access client** tile.
2. Expand the **Troubleshooting** section and select **Advanced diagnostics**.

#### Health Check tests

The **Health Check** runs a series of device and policy tests to verify that the client and its components are working correctly. To run the health check:

1. Navigate to the **Advanced diagnostics** view.
2. Select **Health Check**.

To update the health check status, select **Refresh Health Check**.

![Screenshot of the Health Check view showing that the completed device and policy tests passed.](media/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics/refresh-health-check.png)

#### Network and hostname traffic

This function allows users to capture information about their network and hostname traffic. A good practice is to start the traffic capture, reproduce the issue, and then stop the capture. To capture network and hostname traffic:

1. Navigate to the **Advanced diagnostics** view.
2. Select **Network and hostname traffic**.
3. Select **START**.
4. Reproduce the issue.
5. Select **STOP** to stop capturing network and hostname traffic.

To review the captured traffic, go to the **NETWORK** and **HOSTNAME** tabs.

To download the captured traffic to share with Microsoft Support, select **DOWNLOAD**.

![Screenshot of Network and hostname traffic view showing a list of sample network traffic.](media/troubleshoot-global-secure-access-mobile-client-advanced-diagnostics/network-host-name.png)