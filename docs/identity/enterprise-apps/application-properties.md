---
layout: Conceptual
title: Properties of an enterprise application - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/application-properties
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn about the properties of an enterprise application in Microsoft Entra ID.
ms.topic: concept-article
ai-usage: ai-assisted
ms.date: 2026-10-20T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: enterprise-apps
locale: en-us
document_id: f819d1f9-ac69-8ff5-f19c-5ce76c703593
document_version_independent_id: 1504eddc-e7a3-91e1-7275-bb6354dc536e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/application-properties.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/application-properties
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/application-properties.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8fdfbd1b-e78a-96f8-1926-bdd5d864f58b
---

# Properties of an enterprise application - Microsoft Entra ID | Microsoft Learn

This article describes the properties that you can configure for an enterprise application in your Microsoft Entra tenant. To configure the properties, see [Configure enterprise application properties](add-application-portal-configure).

## Activation status

**Activation status** summarizes disablement conditions for the enterprise application. It shows **Deactivated** if any of the following conditions applies:

- Sign-in is disabled for the service principal in your tenant (`accountEnabled=false`).
- The app registration is deactivated (`isDisabled=true` on the app registration), which is reflected on the service principal.
- Microsoft has disabled the application (`disabledByMicrosoftStatus=DisabledDueToViolationOfServicesAgreement`).

The label alone doesn't identify which condition applies or prove that the app registration is deactivated. More than one condition can apply.

| Condition | How to check | Guidance |
| --- | --- | --- |
| Tenant-local sign-in disablement | Check **Enabled for users to sign-in?** on the enterprise application's **Properties** page, or read the service principal's `accountEnabled` property in Microsoft Graph. | Review why sign-in was disabled before restoring it. To restore tenant-local sign-in, set **Enabled for users to sign-in?** to **Yes** and save, or set `accountEnabled=true`. See [Disable user sign-in](disable-user-sign-in-portal). |
| App registration deactivation | Check the app registration's **State** in its home tenant, or read the application object's `isDisabled` property in Microsoft Graph. | An authorized administrator in the application's home tenant can [reactivate the app registration](deactivate-app-registration#reactivate-an-application). |
| Microsoft disablement | Read the service principal's `disabledByMicrosoftStatus` property in Microsoft Graph. | Tenant administrators can't reverse Microsoft disablement by enabling tenant-local sign-in or reactivating the app registration. See [Protect against consent phishing](protect-against-consent-phishing#recommended-response-and-remediation) for investigation guidance and support options if you believe the disablement is an error. |

You need appropriate permissions in the tenant where you make a change. Enabling tenant-local sign-in doesn't override app registration deactivation or Microsoft disablement. Reactivating the app registration doesn't enable a service principal whose `accountEnabled` remains `false`.

## Enabled for users to sign in?

If this option is set to **Yes**, then assigned users are able to sign in to the application from the My Apps portal, the User access URL, or by navigating to the application URL directly. If assignment is required, then only users who are assigned to the application are able to sign-in. If assignment is required, applications must be assigned to get a token.

If this option is set to **No**, then no users are able to sign in to the application, even if they're assigned to it. Tokens aren't issued for the application. This setting not only prevents users from signing in but also restricts service principals from accessing the application using application permissions.

This setting maps to the service principal's `accountEnabled` property in your tenant. Setting it to **No** (`accountEnabled=false`) also makes **Activation status** show **Deactivated**, even if the app registration isn't deactivated. For instructions, see [Disable user sign-in for an application](disable-user-sign-in-portal).

## Name

This property is the name of the application that users see on the My Apps portal. Administrators see the name when they manage access to the application. Other tenants see the name when integrating the application into their directory.

We recommend that you choose a name that users can understand. It's important because this name is visible in the various portals, such as My Apps and Microsoft 365 Launcher.

## Homepage URL

If the application is custom-developed, the homepage URL is the URL that a user can use to sign in to the application. For example, it's the URL that is launched when the application is selected in the My Apps portal. If this application is from the Microsoft Entra Gallery, this URL is where you can go to learn more about the application or its vendor.

The homepage URL can't be edited within enterprise applications. The homepage URL must be edited on the application object.

## Logo

This property is the application logo that users see on the My Apps portal and the Office 365 application launcher. Administrators also see the logo in the Microsoft Entra gallery.

Custom logos must be exactly 215x215 pixels in size and be in the PNG format. You should use a solid color background with no transparency in your application logo. The logo file size can't be over 100 KB.

## Application ID

This property is the unique identifier for the application in your directory. You can use this application ID if you ever need help from Microsoft Support. You can also use the identifier to perform operations using the Microsoft Graph APIs or the Microsoft Graph PowerShell SDK.

## Object ID

This ID is the unique identifier of the service principal object associated with the application. This identifier can be useful when performing management operations against this application using PowerShell or other programmatic interfaces. This identifier is different than the identifier for the application object.

The identifier is used to update information for the local instance of the application, such as assigning users and groups to the application. The identifier can also be used to update the properties of the enterprise application or to configure single-sign on.

## Assignment required

This setting controls who or what in the directory can obtain an access token for the application. You can use this setting to further lock down access to the application and let only specified users and applications obtain access tokens.

This option determines whether or not an application appears on the My Apps portal. To show the application there, assign an appropriate user or group to the application. This option has no effect on users' access to the application when you configure it for any of the other single sign-on modes.

If this option is set to **Yes**, then users and other applications or services must first be assigned this application before being able to access it.

If this option is set to **No**, then all users are able to sign in, and other applications and services are able to obtain an access token to the application. This option also allows any external users that could be invited into your organization to sign in.

This option only applies to the following types of applications and services:

- Applications using Security Assertion Markup Language (SAML)
- OpenID Connect
- OAuth 2.0
- WS-Federation for user sign
- Application Proxy applications with Microsoft Entra preauthentication enabled
- Applications or services for which other applications or service are requesting access tokens

Note

Users with a Global Administrator role can sign in to applications, regardless of the assignment required settings.

## Visible to users

Makes the application visible in My Apps and the Microsoft 365 Launcher

If this option is set to **Yes**, then assigned users see the application on the My Apps portal and Microsoft 365 app launcher.

If this option is set to **No**, then no users see this application on their My Apps portal and Microsoft 365 launcher.

Make sure that a homepage URL is included or else the application can't be launched from the My Apps portal.

Regardless of whether assignment is required or not, only assigned users are able to see this application in the My Apps portal. If you want certain users to see the application in the My Apps portal, but everyone to be able to access it, assign the users in the **Users and Groups** tab, and set assignment required to **No**.

## Notes

You can use this field to add any information that is relevant for the management of the application. The field is a free text field with a maximum size of 1,024 characters.