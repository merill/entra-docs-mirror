---
layout: Conceptual
title: My Apps portal overview - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/myapps-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn about how to manage applications in the My Apps portal.
ms.topic: concept-article
ms.date: 2024-10-31T00:00:00.0000000Z
ms.reviewer: saibandaru
ms.custom: enterprise-apps
locale: en-us
document_id: 99b4887c-ba4c-a47e-ff49-4423941926b4
document_version_independent_id: 39ce9137-e3b6-998b-0492-794592f59785
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/myapps-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/myapps-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/myapps-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: de2264f7-a8a5-7f67-5101-6fa47e0f1b6c
---

# My Apps portal overview - Microsoft Entra ID | Microsoft Learn

My Apps is a web-based portal that is used for managing and launching applications in Microsoft Entra ID. To work with applications in My Apps, use an organizational account in Microsoft Entra ID and obtain access granted by the Microsoft Entra administrator.

My Apps is separate from the Microsoft Entra admin center and doesn't require users to have an Azure subscription or Microsoft 365 subscription.

Users access the My Apps portal to:

- Discover applications to which they have access
- Request new applications that the organization supports for self-service
- Create personal collections of applications
- Manage access to applications

The following conditions determine whether an application in the enterprise applications list in the Microsoft Entra admin center appears to a user or group in the My Apps portal:

- The application is set to be visible in its properties
- The application is assigned to the user or group

Note

The **Users can only see Office 365 apps in the Office 365 portal** property in the Microsoft Entra admin center can affect whether users can only see Office 365 applications in the Office 365 portal. If this setting is set to **No**, then users will be able to see Office 365 applications in both the My Apps portal and the Office 365 portal. This setting can be found under **Manage** in **Enterprise applications &gt; User settings**.

Administrators can configure:

- Consent experiences including terms of service
- Self-service application discovery and access requests
- Collections of applications
- Company and application branding

## Understand application properties

Properties that are defined for an application can affect how the user interacts with it in the My Apps portal.

- **Enabled for users to sign in?** – If this property is set to **Yes**, then assigned users are able to sign into the application from the My Apps portal.
- **Name** - The name of the application that users see on the My Apps portal. Administrators see the name when they manage access to the application.
- **Homepage URL** -The URL that is launched when the application is selected in the My Apps portal.
- **Logo** - The application logo that users see on the My Apps portal.
- **Visible to users** - Makes the application visible in the My Apps portal. When this value is set to **Yes**, applications still don't appear in the My Apps portal if they don’t yet have users or groups assigned to it. Only assigned users are able to see the application in the My Apps portal.

For more information, see [Properties of an enterprise application](application-properties).

### Discover applications

When signed in to the [My Apps](https://myapps.microsoft.com) portal, the applications that are made visible are shown. For an application to be visible in the My Apps portal, set the appropriate properties in the [Microsoft Entra admin center](https://entra.microsoft.com). Also in the Microsoft Entra admin center, assign a user or group with the appropriate members.

In the My Apps portal, to search for an application, enter an application name in the search box at the top of the page to find an application. The applications that are listed can be formatted in **List view** or a **Grid view**.

Note

End users are no longer be able to add password SSO apps in My Apps. If you need to add a password SSO app for your end users, you can do so in the Microsoft Entra admin center. For more information, see [Add an application for password-based single sign-on](configure-password-single-sign-on-non-gallery-applications).

![Screenshot that shows the search box for the My Apps portal.](media/myapps-overview/myapp-app-list.png)

Important

It can take several minutes for an application to appear in the My Apps portal after it has been added to the tenant in the Microsoft Entra admin center. There may also be a delay in how soon users can access the application after it has been added.

Applications can be hidden. For more information, see [Hide an Enterprise application](hide-application-from-user-portal).

## Assign company branding

In the Microsoft Entra admin center, define the logo and name for the application to represent company branding in the My Apps portal. The banner logo appears at the top of the page, such as the following Contoso demo logo.

![Screenshot that shows the banner logo in the My Apps portal.](media/myapps-overview/banner-logo.png)

For more information, see [Add branding to your organization's sign-in page](../../fundamentals/how-to-customize-branding).

## Manage access to applications

Multiple factors affect how and whether an application is accessed by users. Permissions that are assigned to the application can affect what can be done with it. Applications can be configured to allow self-service access, or access can be only granted by an administrator of the tenant.

### My Apps Secure Sign-in Extension

Install the My Apps secure sign-in extension to sign in to some applications. The extension is required for sign-in to password-based SSO applications, or to applications that are accessed by Microsoft Entra application proxy. Users are prompted to install the extension when they first launch the password-based single sign-on or an Application Proxy application.

To integrate these applications, define a mechanism to deploy the extension at scale with supported browsers. Options include:

- User-driven download and configuration for Chrome, Microsoft Edge, or IE
- Configuration Manager for Internet Explorer

For applications that use password-based SSO or accessed by using Microsoft Entra application proxy, use Microsoft Edge mobile. For other applications, any mobile browser can be used. Be sure to enable password-based SSO in the mobile settings, which can be off by default. For example, **Settings &gt; Privacy and Security &gt; Microsoft Entra Password SSO**.

To download and install the extension:

- **Microsoft Edge** - From the Microsoft Store, go to the [My Apps Secure Sign-in Extension](https://microsoftedge.microsoft.com/addons/detail/my-apps-secure-signin-ex/gaaceiggkkiffbfdpmfapegoiohkiipl) feature, and then select **Get to get the extension for Microsoft Edge legacy browser**.
- **Google Chrome** - From the Chrome Web Store, go to the [My Apps Secure Sign-in Extension](https://chrome.google.com/webstore/detail/my-apps-secure-sign-in-ex/ggjhpefgjjfobnfoldnjipclpcfbgbhl) feature, and then select **Add to Chrome**.

An icon is added to the right of the address bar, which enables sign in and customization of the extension.

Note

Sign-in into the extension is currently not supported for Guest B2B Microsoft Accounts (MSA).

### Permissions

Permissions that are granted to an application can be reviewed by selecting the upper right corner of the tile that represents the application and then selecting **Manage your application**.

The permissions that are shown are consented to by an administrator or are consented to by the user. Permissions consented to by the user can be revoked by the user.

### Self-service access

Access can be granted on a tenant level, assigned to specific users, or from self-service access. Before users can self-discover applications from the My Apps portal, enable self-service application access in the Microsoft Entra admin center. This feature is available for applications when added using these methods:

- The Microsoft Entra application gallery
- Microsoft Entra application proxy
- Using user or admin consent

Enable users to discover and request access to applications by using the My Apps portal. To do so, complete the following tasks in the Microsoft Entra admin center:

- Enable self-service group management
- Enable the application for single sign-on
- Create a group for application access

When users request access, they request access to the underlying group, and group owners can be delegated permission to manage the group membership and application access. Approval workflows are available for explicit approval to access applications. Users who are approvers receive notifications within the My Apps portal when there are pending requests for access to the application.

For more information, see [Enable self-service application assignment](manage-self-service-access)

### Single sign-on

Enable single sign-on (SSO) in the Microsoft Entra admin center for all applications that are made available in the My Apps portal whenever possible. If SSO is set up, users have a seamless experience without the need to enter their credentials. To learn more, see [Single sign-on options in Microsoft Entra ID](what-is-single-sign-on#single-sign-on-options).

Applications can be added by using the Linked SSO option. Configure an application tile that links to the URL of the existing web application. Linked SSO allows the direction of users to the My Apps portal without migrating all the applications to Microsoft Entra SSO. Gradually move to Microsoft Entra SSO-configured applications to prevent disrupting the users’ experience.

For more information, see [Add linked single sign-on to an application](configure-linked-sign-on).

## Create collections

By default, all applications are listed together on a single page. Collections can be used to group together related applications and present them on a separate tab, making them easier to find. For example, use collections to create logical groupings of applications for specific job roles, tasks, projects, and so on. Every application to which a user has access appears in the default Apps collection, but a user can remove applications from the collection.

Users can also customize their experience by:

- Creating their own application collections
- Hiding and reordering application collections

Applications can be hidden from the My Apps portal by a user or administrator. A hidden application can still be accessed from other locations, such as the Microsoft 365 portal. Only 950 applications to which a user has access can be accessed through the My Apps portal.

For more information, see [Create collections on the My Apps portal](access-panel-collections).

Important

In case there is domain federation and for the user to be redirected to an external federation endpoint for authentication, the request to My Apps must contain a domain hint URL parameter such as "domain\_hint=example.com".