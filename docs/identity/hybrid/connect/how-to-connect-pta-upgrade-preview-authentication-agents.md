---
layout: Conceptual
title: Microsoft Entra Connect - Pass-through Authentication - Upgrade auth agents - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta-upgrade-preview-authentication-agents
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes how to upgrade your Microsoft Entra pass-through authentication configuration.
keywords: Azure AD Connect Pass-through Authentication, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 07999a24-b45a-1ff0-8cf4-33786545e2a0
document_version_independent_id: d61cb636-2164-ce55-8ad4-c3c622ee399e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-pta-upgrade-preview-authentication-agents.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-pta-upgrade-preview-authentication-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-pta-upgrade-preview-authentication-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 94073efa-fd31-db10-61ab-6d0338212d3b
---

# Microsoft Entra Connect - Pass-through Authentication - Upgrade auth agents - Microsoft Entra ID | Microsoft Learn

## Overview

This article is for customers using Microsoft Entra pass-through authentication through preview. We recently upgraded (and rebranded) the Authentication Agent software. You need to *manually* upgrade preview Authentication Agents installed on your on-premises servers. This manual upgrade is a one-time action only. All future updates to Authentication Agents are automatic. The reasons to upgrade are as follows:

- The preview versions of Authentication Agents won't receive any further security or bug fixes.
- The preview versions of Authentication Agents can't be installed on other servers, for high availability.

## Check versions of your Authentication Agents

### Step 1: Check where your Authentication Agents are installed

Follow these steps to check where your Authentication Agents are installed:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Connect sync**.
3. Select **Pass-through Authentication**. This blade lists the servers where your Authentication Agents are installed.

![Microsoft Entra admin center - Pass-through Authentication blade](media/how-to-connect-pta-upgrade-preview-authentication-agents/pta8.png)

### Step 2: Check the versions of your Authentication Agents

To check the versions of your Authentication Agents, on each server identified in the preceding step, follow these instructions:

1. Go to **Control Panel -&gt; Programs -&gt; Programs and Features** on the on-premises server.
2. If there's an entry for "**Microsoft Entra Connect Authentication Agent**", you don't need to take any action on this server.
3. If there's an entry for "**Microsoft Entra private network connector**", you need to manually upgrade on this server.

![Preview version of Authentication Agent](media/how-to-connect-pta-upgrade-preview-authentication-agents/pta6.png)

## Best practices to follow before starting the upgrade

Before upgrading, ensure that you have the following items in place:

1. **Create cloud-only Hybrid Identity Administrator account**: Don’t upgrade without having a cloud-only Hybrid Identity Administrator account to use in emergency situations where your Pass-through Authentication Agents aren't working properly. Learn about [emergency access accounts in Microsoft Entra ID](../../role-based-access-control/security-emergency-access). This step is critical and ensures that you don't get locked out of your tenant.
2. **Ensure high availability**: If not completed previously, install a second standalone Authentication Agent to provide high availability for sign-in requests, using these [instructions](how-to-connect-pta-quick-start#step-4-ensure-high-availability).

## Upgrading the Authentication Agent on your Microsoft Entra Connect server

You need upgrade Microsoft Entra Connect before upgrading the Authentication Agent on the same server. Follow these steps on both your primary and staging Microsoft Entra Connect servers:

1. **Upgrade Microsoft Entra Connect**: Follow this [article](how-to-upgrade-previous-version) and upgrade to the latest Microsoft Entra Connect version.
2. **Uninstall the preview version of the Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on the server.
3. **Download the latest version of the Authentication Agent (versions 1.5.2482.0 or later)**: Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator). Browse to **Entra ID** &gt; **Entra Connect** &gt; **Connect sync**.

Select **Pass-through Authentication -&gt; Download agent**. Accept the [terms of service](https://aka.ms/authagenteula) and download the latest version of the Authentication Agent. You can also download the Authentication Agent from [here](https://aka.ms/getauthagent). 4. **Install the latest version of the Authentication Agent**: Run the executable downloaded in Step 3. Provide your tenant's Hybrid Identity Administrator credentials when prompted. 5. **Verify that the latest version has been installed**: As shown before, go to **Control Panel -&gt; Programs -&gt; Programs and Features** and verify that there's an entry for "**Microsoft Entra Connect Authentication Agent**".

Note

If you check the Pass-through Authentication blade on the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator). after completing the preceding steps, you'll see two Authentication Agent entries per server - one entry showing the Authentication Agent as **Active** and the other as **Inactive**. This is *expected*. The **Inactive** entry is automatically dropped after a few days.

## Upgrading the Authentication Agent on other servers

Follow these steps to upgrade Authentication Agents on other servers (where Microsoft Entra Connect isn't installed):

1. **Uninstall the preview version of the Authentication Agent**: Download [this PowerShell script](https://aka.ms/rmpreviewagent) and run it as an Administrator on the server.
2. **Download the latest version of the Authentication Agent (versions 1.5.2482.0 or later)**: Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) with your tenant's Hybrid Identity Administrator credentials. Select **Microsoft Entra ID -&gt; Microsoft Entra Connect -&gt; Pass-through Authentication -&gt; Download agent**. Accept the terms of service and download the latest version.
3. **Install the latest version of the Authentication Agent**: Run the executable downloaded in Step 2. Provide your tenant's Hybrid Identity Administrator credentials when prompted.
4. **Verify that the latest version has been installed**: As shown before, go to **Control Panel -&gt; Programs -&gt; Programs and Features** and verify that there's an entry called **Microsoft Entra Connect Authentication Agent**.

Note

If you check the Pass-through Authentication blade on the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) after completing the preceding steps, you'll see two Authentication Agent entries per server - one entry showing the Authentication Agent as **Active** and the other as **Inactive**. This is *expected*. The **Inactive** entry is automatically dropped after a few days.