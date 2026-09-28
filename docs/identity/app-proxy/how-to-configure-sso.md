---
layout: Conceptual
title: Understand single sign-on with an on-premises app using application proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/how-to-configure-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Configure single sign-on for on-premises apps published through Microsoft Entra application proxy. Covers password-based, SAML, Kerberos, and header-based SSO options.
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: KaTabish
ai-usage: ai-assisted
locale: en-us
document_id: ab65e9bd-17c1-50ce-47e9-1f4eae294c4a
document_version_independent_id: ab65e9bd-17c1-50ce-47e9-1f4eae294c4a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/how-to-configure-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/how-to-configure-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/how-to-configure-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 585117e9-1923-9325-8f1d-df9d0717918b
---

# Understand single sign-on with an on-premises app using application proxy - Microsoft Entra ID | Microsoft Learn

## Overview

Single sign-on (SSO) lets your users access an application without authenticating multiple times. The authentication occurs in the cloud, against Microsoft Entra ID, and the service or connector impersonates the user to complete additional authentication challenges from the application.

## How to configure single sign-on

To configure SSO, first make sure that your application is configured for preauthentication through Microsoft Entra ID.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Select your username in the upper-right corner. Verify you're signed in to a directory that uses application proxy. If you need to change directories, select **Switch directory** and choose a directory that uses application proxy.
3. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application proxy**.

Look for the **Pre Authentication** field, and make sure that it's set.

For more information about preauthentication methods, see step 4 of [Add an on-premises application for remote access through application proxy in Microsoft Entra ID](application-proxy-add-on-premises-application).

![Screenshot that shows the pre-authentication method in the Microsoft Entra admin center.](media/application-proxy-config-sso-how-to/app-proxy.png)

## Configure single sign-on modes for application proxy applications

Configure the specific type of single sign-on. The sign-on methods are classified based on what type of authentication the backend application uses. Application proxy applications support four types of sign-on:

- **Password-based sign-on:** Password-based sign-on can be used for any application that uses username and password fields to sign in. Configuration steps are in [Configure password single sign-on for a Microsoft Entra gallery application](../enterprise-apps/configure-password-single-sign-on-non-gallery-applications).
- **Integrated Windows authentication:** For applications using integrated Windows authentication (IWA), single sign-on is enabled through Kerberos Constrained Delegation (KCD). This method gives private network connectors permission in Active Directory to impersonate users, and to send and receive tokens on their behalf. For details about configuring KCD, see [Single sign-on with KCD](how-to-configure-sso-with-kcd).
- **Header-based sign-on:** Header-based sign-on provides single sign-on capabilities using HTTP headers. To learn more, see [Header-based single sign-on](application-proxy-configure-single-sign-on-with-headers).
- **SAML single sign-on:** With Security Assertion Markup Language (SAML) single sign-on, Microsoft Entra ID authenticates to the application by using the user's Microsoft Entra account. Microsoft Entra ID communicates the sign-in information to the application through a connection protocol. With SAML-based single sign-on, you can map users to specific application roles based on rules you define in your SAML claims. For information about setting up SAML single sign-on, see [SAML for single sign-on with application proxy](conceptual-sso-apps).

To find these options, go to your application in **Enterprise apps**, and open the **Single sign-on** page on the left menu. If your application was created in the old portal, you might not see all these options.

On this page, you also see one more sign-on option: **Linked Sign-On**. Application proxy supports this option. However, this option doesn't add single sign-on to the application. That said, the application might already have single sign-on implemented using another service such as Active Directory Federation Services.

This option lets an admin create a link to an application that users first land on when accessing the application. For example, an application that is configured to authenticate users using Active Directory Federation Services 2.0 can use the **Linked Sign-On** option to create a link to it on the **My Apps** page.