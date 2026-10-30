---
layout: Conceptual
title: Support single sign-on and app protection policies in mobile apps you develop - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/mobile-sso-support-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Explanation and overview of building mobile applications that support single sign-on and app protection policies using the Microsoft identity platform and integrating with Microsoft Entra ID.
manager: pmwongera
ms.date: 2020-10-14T00:00:00.0000000Z
ms.reviewer: janicericketts
ms.subservice: workforce
ms.topic: concept-article
locale: en-us
document_id: 6052bf66-faba-91f7-8b4f-ee077e5345e7
document_version_independent_id: 612d1d27-d816-947e-34fc-07c561751794
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/mobile-sso-support-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/mobile-sso-support-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/mobile-sso-support-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f6169045-25a3-dc75-71a3-a17776dcec57
---

# Support single sign-on and app protection policies in mobile apps you develop - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Single sign-on (SSO) is a key offering of the Microsoft identity platform and Microsoft Entra ID, providing easy and secure logins for users of your app. In addition, app protection policies (APP) enable support of the key security policies that keep your user's data safe. Together, these features enable secure user logins and management of your app's data.

This article explains why SSO and APP are important and provides the high-level guidance for building mobile applications that support these features. This applies for both phone and tablet apps. If you're an IT administrator that wants to deploy SSO across your organization's Microsoft Entra tenant, check out our [guidance for planning a single sign-on deployment](../identity/enterprise-apps/plan-sso-deployment)

## About single sign-on and app protection policies

[Single sign-on (SSO)](../identity/enterprise-apps/plan-sso-deployment) allows a user to sign in once and get access to other applications without re-entering credentials. This makes accessing apps easier and eliminates the need for users to remember long lists of usernames and passwords. Implementing it in your app makes accessing and using your app easier.

In addition, enabling single sign-on in your app unlocks new authentication mechanisms that come with modern authentication, like [passwordless logins](../identity/authentication/concept-authentication-passkeys-fido2). Usernames and passwords are one of the most popular attack vectors against applications, and enabling SSO allows you to mitigate this risk by enforcing Conditional Access or passwordless logins that add extra security or rely on more secure authentication mechanisms. Finally, enabling single sign-on also enables [single sign-out](v2-protocols-oidc#single-sign-out). This is useful in situations like work applications that will be used on shared devices.

[App protection policies (APP)](/en-us/mem/intune/apps/app-protection-policy) ensure that an organization's data remains safe and contained. They allow companies to manage and protect their data within an app and allow control over who can access the app and its data. Implementing app protection policies enables your app to connect users to resources protected by Conditional Access policies and securely transfer data to and from other protected apps. Scenarios unlocked by app protection policies include requiring a PIN to open an app, control the sharing of data between apps, and preventing company app data from being saved to personal storage locations.

## Implementing single sign-on

We recommend the following to enable your app to take advantage of single sign-on.

### Use the Microsoft Authentication Library (MSAL)

The best choice for implementing single sign-on in your application is to use [the Microsoft Authentication Library (MSAL)](msal-overview). By using MSAL you can add authentication to your app with minimal code and API calls, get the full features of the [Microsoft identity platform](./), and let Microsoft handle the maintenance of a secure authentication solution. By default, MSAL adds SSO support for your application. In addition, using MSAL is a requirement if you also plan to implement app protection policies.

Note

It is possible to configure MSAL to use an embedded web view. This will prevent single sign-on. Use the default behavior (that is, the system web browser) to ensure that SSO will work.

For iOS applications, we have a [quickstart](quickstart-v2-ios) that shows you how to set up sign-ins using MSAL, and [guidance for configuring MSAL for various SSO scenarios](/en-us/entra/msal/objc/single-sign-on-macos-ios).

For Android applications, we have a [quickstart](quickstart-v2-android) that shows you how to set up sign-ins using MSAL, and guidance for [how to enable cross-app SSO on Android using MSAL](msal-android-single-sign-on).

### Use the system web browser

A web browser is required for interactive authentication. For mobile apps that use modern authentication libraries other than MSAL (that is, other OpenID Connect or SAML libraries), or if you implement your own authentication code, you should use the system browser as your authentication surface to enable SSO.

Google has guidance for doing this in Android Applications: [Chrome Custom Tabs - Google Chrome](https://developer.chrome.com/multidevice/android/customtabs).

Apple has guidance for doing this in iOS applications: [Authenticating a User Through a Web Service | Apple Developer Documentation](https://developer.apple.com/documentation/authenticationservices/authenticating_a_user_through_a_web_service).

Tip

The [SSO plug-in for Apple devices](apple-sso-plugin) allows SSO for iOS apps that use embedded web views on managed devices using Intune. We recommend MSAL and system browser as the best option for developing apps that enable SSO for all users, but this will allow SSO in some scenarios where it otherwise is not possible.

## Enable App Protection Policies

To enable app protection policies, use the [Microsoft Authentication Library (MSAL)](msal-overview). MSAL is the Microsoft identity platform's authentication and authorization library and the Intune SDK is developed to work in tandem with it.

In addition, you must use a broker app for authentication. The broker requires the app to provide application and device information to ensure app compliance. iOS users will use the [Microsoft Authenticator app](https://support.microsoft.com/account-billing/sign-in-to-your-accounts-using-the-microsoft-authenticator-app-582bdc07-4566-4c97-a7aa-56058122714c) and Android users will use either the Microsoft Authenticator app or the [Company Portal app](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) for [brokered authentication](msal-android-single-sign-on). By default, MSAL uses a broker as its first choice for fulfilling an authentication request, so using the broker to authenticate will be enabled for your app automatically when using MSAL out-of-the-box.

Finally, [add the Intune SDK](/en-us/mem/intune/developer/app-sdk-get-started) to your app to enable app protection policies. The SDK for the most part follows an intercept model and will automatically apply app protection policies to determine if actions the app is taking are allowed or not. There are also APIs you can call manually to tell the app if there are restrictions on certain actions.