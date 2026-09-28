---
layout: Conceptual
title: End-user experiences for applications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/end-user-experiences
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn about the customizable ways to deploy applications to end users in your organization with Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-09-04T00:00:00.0000000Z
ms.reviewer: lenalepa
ms.custom: enterprise-apps
ai-usage: ai-assisted
locale: en-us
document_id: d2507e59-a43d-b5ce-b046-7ebb3dc39b00
document_version_independent_id: 0e723cfb-4d9f-3095-58d2-73aef25a22f9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/end-user-experiences.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/end-user-experiences
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/end-user-experiences.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 6d7e5e25-18e6-f572-48a6-505445e260c4
---

# End-user experiences for applications - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID provides several customizable ways to deploy applications to end users in your organization:

- Microsoft Entra My Apps
- Microsoft 365 application launcher
- Direct sign-on to federated apps
- Deep links to federated, password-based, or existing apps

Which method you choose to deploy in your organization is your discretion.

## Microsoft Entra My Apps

My Apps is a web-based portal that allows an organization user in Microsoft Entra ID to view and launch apps which they're granted access to by an admin. If you're an end user with [Microsoft Entra ID P1 or P2](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing), you can also utilize self-service group management capabilities through My Apps.

By default, all applications are listed together on a single page. But you can use collections to group together related applications and present them on a separate tab, making them easier to find. For example, you can use collections to create logical groupings of applications for specific job roles, tasks, projects, and so on. For information, see [Create collections on the My Apps portal](access-panel-collections).

[My Apps](https://myapps.microsoft.com) is separate from the Microsoft Entra admin center and doesn't require users to have an Azure subscription or Microsoft 365 subscription.

For more information on Microsoft Entra My Apps, see the [introduction to My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Microsoft 365 application launcher

Microsoft 365 application launcher is the recommended app launching solution for organizations using Microsoft 365.

For more information about the Office 365 application launcher, see [Have your app appear in the Office 365 app launcher](/en-us/previous-versions/office/office-365-api/).

## Direct sign-on to federated apps

Most federated applications that support SAML 2.0, WS-Federation, or OpenID connect also support the ability for users to start at the application. The users then get signed in through Microsoft Entra ID either by automatic redirection or by selecting a link to sign in. Direct sign-on is a service provider-initiated sign-on, and most federated applications in Microsoft Entra application gallery support it. See the documentation linked from the app’s single sign-on configuration wizard in the Microsoft Entra admin center for details.

## Direct sign-on links

Microsoft Entra ID also supports direct single sign-on links to individual applications that support password-based single sign-on, linked single sign-on, and any form of federated single sign-on.

Direct sign-on links are crafted URLs that send a user through the Microsoft Entra sign-in process for a specific application. The user doesn't need to launch the application from My Apps or Microsoft 365. These **User access URLs** can be found under the properties of available enterprise applications. In the Microsoft Entra admin center, select **Entra ID** &gt; **Enterprise apps**. Select the application, and then select **Properties**.

![Example of the User access URL in X properties](media/end-user-experiences/direct-sign-on-link.png)

Direct sign-on links can be copied and pasted anywhere you want to provide a sign-in link to the selected application. They can be placed in an email, or in any custom web-based portal that you set up for user application access. The following URL is an example of a Microsoft Entra ID direct single sign-on URL for X:

`https://myapps.microsoft.com/signin/X/230848d52c8745d4b05a60d29a40fced`

Similar to organization-specific URLs for My Apps, you can further customize direct sign-on URL by adding one of the active or verified domains for your directory after the *myapps.microsoft.com* domain. Customizing direct sign-on URL ensures any organizational branding is loaded immediately on the sign-in page without the user needing to enter their user ID first:

`https://myapps.microsoft.com/contosobuild.com/signin/X/230848d52c8745d4b05a60d29a40fced`

When an authorized user selects one of these application-specific links, they first see their organizational sign-in page (assuming they aren't already signed in). After sign-in, they're redirected to their app without stopping at My Apps first. If the user is missing prerequisites to access the application, such as the password-based single sign browser extension, then the link prompts the user to install the missing extension. The link URL also remains constant if the single sign-on configuration for the application changes.

These links use the same access control mechanisms as My Apps and Microsoft 365. Only those users or groups who are assigned to the application in the Microsoft Entra admin center are able to successfully authenticate. However, any user who is unauthorized see's a message explaining that they aren't granted access. The unauthorized user is given a link to load My Apps to view available applications that they do have access to.

## Legacy My Apps experience settings

The legacy My Apps preview settings, such as **Users can use preview features for My Apps**, are no longer used by the My Apps portal or other app launchers. These settings don't affect what your users see or how the app launchers behave.

Note

The legacy My Apps and My Staff experience settings are no longer used by the service and don't affect user behavior. These settings are being removed from the Microsoft Entra admin center. No administrator action is required.

To control what your users see in My Apps, assign users and groups to applications and organize applications with collections. For more information, see [Create collections on the My Apps portal](access-panel-collections).