---
layout: Conceptual
title: Publish an on-premises SharePoint farm with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-integrate-with-sharepoint-server-saml
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Configure Microsoft Entra application proxy with SAML-based authentication for secure external access to on-premises SharePoint Server.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8956fa16-70cc-ca82-aff2-57fbf5c436d2
document_version_independent_id: 9273907a-1346-81d1-3d47-48331f956b0c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-integrate-with-sharepoint-server-saml.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-integrate-with-sharepoint-server-saml
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-integrate-with-sharepoint-server-saml.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 43d4f1ec-3589-9d91-a272-64e663774388
---

# Publish an on-premises SharePoint farm with Microsoft Entra application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

This step-by-step guide explains how to secure the access to the [Microsoft Entra integrated on-premises SharePoint (SAML)](../saas-apps/sharepoint-on-premises-tutorial) using Microsoft Entra application proxy, where users in your organization (Microsoft Entra ID, B2B) connect to SharePoint through the Internet.

Note

If you're new to Microsoft Entra application proxy and want to learn more, see [Remote access to on-premises applications through Microsoft Entra application proxy](overview-what-is-app-proxy).

There are three primary advantages of this setup:

- Microsoft Entra application proxy ensures that authenticated traffic can reach your internal network and SharePoint.
- Your users can access SharePoint sites as usual without using VPN.
- You can control the access by user assignment on the Microsoft Entra application proxy level and you can increase the security with Microsoft Entra features like Conditional Access and multifactor authentication (MFA).

This process requires two Enterprise Applications. One is a SharePoint on premises instance that you publish from the gallery to your list of managed SaaS apps. The second is an on-premises application (non-gallery application) you use to publish the first Enterprise Gallery Application.

## Prerequisites

- A SharePoint 2013 farm or newer. The SharePoint farm must be [integrated with Microsoft Entra ID](../saas-apps/sharepoint-on-premises-tutorial).
- A Microsoft Entra tenant with a plan that includes application proxy. Learn more about [Microsoft Entra ID plans and pricing](https://www.microsoft.com/security/business/microsoft-entra-pricing).
- A Microsoft Office Web Apps Server farm to properly launch Office files from the on-premises SharePoint farm.
- A [custom, verified domain](../../fundamentals/add-custom-domain) in the Microsoft Entra tenant. The verified domain must match the SharePoint URL suffix.
- A Transport Layer Security (TLS) certificate is required. See the details in [custom domain publishing](how-to-configure-custom-domain).
- A private network connector installed and running on a machine within the corporate domain.

The list includes more prerequisites.

- On-premises Active Directory users must be synchronized with Microsoft Entra Connect, and must be configured to [sign in to Azure](../hybrid/connect/plan-connect-user-signin).
- Cloud-only and B2B guest users must be [granted access to a guest account to SharePoint on premises in the Microsoft Entra admin center](../saas-apps/sharepoint-on-premises-tutorial#manage-guest-users-access).

## Step 1: Integrate SharePoint on premises with Microsoft Entra ID

1. Configure the SharePoint on-premises application. For more information, see [Tutorial: Microsoft Entra single sign-on integration with SharePoint on-premises](../saas-apps/sharepoint-on-premises-tutorial).
2. Access SharePoint on premises from the internal network and confirm it's accessible internally.

## Step 2: Publish the SharePoint on-premises application with application proxy

In this step, you create an application in your Microsoft Entra tenant that uses application proxy. You set the external URL and specify the internal URL, both of which are used later in SharePoint.

Note

The Internal and External URLs must match the **Sign on URL** in the SAML Based Application configuration in Step 1.

![The Sign on URL value.](media/application-proxy-integrate-with-sharepoint-server/sso-url-saml.png)

1. Create a new Microsoft Entra application proxy application with custom domain. For step-by-step instructions, see [Custom domains in Microsoft Entra application proxy](how-to-configure-custom-domain).

    - Internal URL: 'https://portal.contoso.com/'
    - External URL: 'https://portal.contoso.com/'
    - Pre-Authentication: Microsoft Entra ID
    - Translate URLs in Headers: No
    - Translate URLs in Application Body: No

        ![The options you use to create the app.](media/application-proxy-integrate-with-sharepoint-server/create-application-azure-entra.png)
2. Assign the [same groups](../saas-apps/sharepoint-on-premises-tutorial#grant-permissions-to-a-security-group) you assigned to the on-premises SharePoint Gallery Application.
3. Finally, go to the **Properties** section and set **Visible to users?** to **No**. This option ensures that only the icon of the first application appears on the My Apps Portal (https://myapplications.microsoft.com).

    ![Set the Visible to users? option.](media/application-proxy-integrate-with-sharepoint-server/configure-properties.png)

## Step 3: Test your application

Using a browser from a computer on an external network, navigate to the link that you configured during the publish step. Make sure you can sign in with the test account that you set up.