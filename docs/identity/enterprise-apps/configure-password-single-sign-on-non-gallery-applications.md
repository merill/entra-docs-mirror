---
layout: Conceptual
title: Add password-based single sign-on to an application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-password-single-sign-on-non-gallery-applications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Add password-based single sign-on to an application in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-06-20T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: enterprise-apps
locale: en-us
document_id: e973cbe2-df0f-d310-b439-17e14a0af060
document_version_independent_id: b4649ad0-6baa-a2e4-dd13-20593f10c09a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/configure-password-single-sign-on-non-gallery-applications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/configure-password-single-sign-on-non-gallery-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/configure-password-single-sign-on-non-gallery-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 232b13a1-5ab3-7228-f7ed-54104b2f0f81
---

# Add password-based single sign-on to an application - Microsoft Entra ID | Microsoft Learn

This article shows you how to set up password-based single sign-on (SSO) in Microsoft Entra ID. With password-based SSO, a user signs in to the application with a username and password the first time they sign in to it. After the first sign-on, Microsoft Entra ID sends the username and password to the application.

Password-based SSO uses the existing authentication process provided by the application. When you enable password-based SSO for an application, Microsoft Entra ID collects and securely stores usernames and passwords for the application. User credentials are stored in an encrypted state in the directory. Password-based SSO is supported for any cloud-based application that has an HTML-based sign-in page.

Choose password-based SSO when:

- An application doesn't support the Security Assertion Markup Language (SAML) SSO protocol.
- An application authenticates with a username and password instead of access tokens and headers.

The configuration page for password-based SSO is simple. It includes only the URL of the sign-on page that the application uses. This string must be the page that includes the username input field.

## Prerequisites

To configure password-based SSO in your Microsoft Entra tenant, you need:

- An Azure account with an active subscription. If you don't already have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- Application Administrator, Cloud Application Administrator, or owner of the service principal.
- An application that supports password-based SSO.

## Configure password-based single sign-on

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application from the search results.
4. Select **Single sign-on** and then select **Password-based**.
5. Enter the URL for the sign-in page of the application.
6. Select **Save**.

Microsoft Entra ID parses the HTML of the sign-in page for username and password input fields. If the attempt succeeds, you're signed in. Your next step is to [Assign users or groups](add-application-portal-assign-users) to the application.

After assigning users and groups, you can provide credentials to be used for a user when they sign in to the application.

1. Select **Users and groups**, select the checkbox for the user's or group's row, and then select **Update Credentials**.
2. Enter the username and password to be used for the user or group. If you don't, users are prompted to enter the credentials themselves upon launch.

## Manual configuration

If the parsing attempt by Microsoft Entra ID fails, you can configure sign-on manually.

1. Select **Configure {application name} Password Single Sign-on Settings** to display the **Configure sign-on** page.
2. Select **Manually detect sign-in fields**. More instructions that describe manual detection of sign-in fields appear.
3. Select **Capture sign-in fields**. A capture status page opens in a new tab, showing the message metadata capture is currently in progress.
4. If the **My Apps Extension Required** box appears in a new tab, select **Install Now** to install the My Apps Secure Sign-in Extension browser extension. (The browser extension requires Microsoft Edge or Chrome.) Then install, launch, and enable the extension, and refresh the capture status page. The browser extension then opens another tab that displays the entered URL.
5. In the tab with the entered URL, go through the sign-in process. Fill in the username and password fields, and try to sign in. (You don't have to provide the correct password.) A prompt asks you to save the captured sign-in fields.
6. Select **OK**. The browser extension updates the capture status page with the message **Metadata has been updated for the application**. The browser tab closes.
7. In the Microsoft Entra ID Configure sign-on page, select **Ok, I was able to sign-in to the app successfully**.
8. Select **OK**.

## Limitations

For password-based SSO, the end user’s browsers can be:

- Internet Explorer 8, 9, 10, 11--on Windows 7 or later (limited support)
- Microsoft Edge on Windows 10 Anniversary Edition or later
- Chrome--on Windows 7 or later, and on macOS X or later

Users might only have a maximum of [48 credentials](../users/directory-service-limits-restrictions) configured for applications utilizing password-based single sign-on.