---
layout: Conceptual
title: Frontline worker management - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/frontline-worker-management
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about frontline worker management capabilities that are provided through the My Staff portal.
ms.topic: concept-article
ms.date: 2025-03-19T00:00:00.0000000Z
ms.reviewer: stevebal
ms.custom: sfi-image-nochange
locale: en-us
document_id: 38d8dd75-1d58-e777-008c-5ca66a2d9d52
document_version_independent_id: d7927e71-d5f7-07ec-c881-8857e5c9b8f7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/frontline-worker-management.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/frontline-worker-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/frontline-worker-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 787e8cac-5730-5dc3-4473-d2940335ca50
---

# Frontline worker management - Microsoft Entra | Microsoft Learn

Frontline workers account for over 80 percent of the global workforce. Yet because of high scale, rapid turnover, and fragmented processes, frontline workers often lack the tools to make their demanding jobs a little easier. Frontline worker management brings digital transformation to the entire frontline workforce. The workforce might include managers, frontline workers, operations, and IT.

Frontline worker management empowers the frontline workforce by making the following activities easier to accomplish:

- Streamlining common IT tasks with My Staff
- Easy onboarding of frontline workers through simplified authentication
- Seamless provisioning of shared devices and secure sign-out of frontline workers

## Delegated user management through My Staff

Microsoft Entra ID in the My Staff portal enables delegation of user management. Frontline managers can save valuable time and reduce risks using the [My Staff portal](../identity/role-based-access-control/my-staff-configure). When an administrator enables simplified password resets and phone management directly from the store or factory floor, managers can grant access to employees without routing the request through the help-desk, IT, or operations.

![Screenshot of delegated user management in the My Staff portal.](media/concept-fundamentals-frontline-worker/delegated-user-management.png)

## Accelerated onboarding with simplified authentication

Frontline workers often need quick and easy access to tools and information. Microsoft Entra ID provides accelerated onboarding with simplified authentication to meet this need. Frontline workers can use SMS sign-in or QR code sign-in to access their devices and applications easily.

### SMS authentication

My Staff also enables frontline managers to register their team members' phone numbers for [SMS sign-in](../identity/authentication/howto-authentication-sms-signin). In many verticals, frontline workers maintain a local username and password combination, a solution that is often cumbersome, expensive, and error-prone. When IT enables authentication using SMS sign-in, frontline workers can sign in with [single sign-on (SSO)](../identity/enterprise-apps/what-is-single-sign-on) for Microsoft Teams and other applications using just their phone number and a one-time passcode (OTP) sent via SMS. Single sign-on makes signing in for frontline workers simple and secure, delivering quick access to the apps they need most.

![Screenshot of SMS sign-in.](media/concept-fundamentals-frontline-worker/sms-signin.png)

### QR code authentication (preview)

QR code authentication provides a fast and cost-effective way to sign in, improving productivity and offering a seamless experience for frontline workers. This method uses a QR code and a user-defined 8-digit PIN. You use the QR code and PIN together to sign in to a device or application.

The QR code includes a User Principal Name (UPN), tenant ID, and a secret key. You set the PIN, which replaces the default temporary PIN assigned by the administrator. The PIN works only with the QR code and not with other identifiers like UPN or phone numbers. You also can't use the QR code without the PIN.

![Screenshot of a QR code plus PIN.](media/concept-fundamentals-frontline-worker/qr-code-plus-pin.png)

The QR code authentication method offers two main advantages for frontline workers compared to traditional methods:

- Faster sign-in: QR code authentication eliminates the need for usernames and passwords, which benefits users who are less tech-savvy or have accessibility challenges. Scanning a QR code reduces login time by about two seconds, enhancing worker productivity. It also decreases IT tickets related to forgotten usernames, as users don't need to remember them for sign-in.
- Cost-effective: Printing QR codes is cheaper than providing hardware keys and workers can attach the QR code to a badge or wearable. Organizations prefer this method because frontline workers often hold temporary positions and may not return, reducing the risk of investment loss in costly devices.

Learn more about [QR code authentication](/en-us/entra/identity/authentication/concept-authentication-qr-code) and how to [enable it](/en-us/entra/identity/authentication/how-to-authentication-qr-code) for your organization.

## Shared devices for frontline workers

Frontline managers can also use Managed Home Screen (MHS) application to allow workers to have access to a specific set of applications on their Intune-enrolled Android dedicated devices. The dedicated devices are enrolled with [Microsoft Entra shared device mode](../identity-platform/msal-shared-devices). When configured in multiapp kiosk mode in the Microsoft Intune admin center, MHS is automatically launched as the default home screen on the device and appears to the end user as the *only* home screen. To learn more, see how to [configure the Microsoft Managed Home Screen app for Android Enterprise](/en-us/mem/intune/apps/app-configuration-managed-home-screen-app).

### Secure sign-out of frontline workers from shared devices

Frontline workers in many companies use shared devices to do inventory management and sales transactions. Sharing devices reduces the IT burden of provisioning and tracking them individually. With shared device sign-out, it's easy for a frontline worker to securely sign out of all apps on any shared device before handing it back to a hub or passing it off to a teammate on the next shift. Frontline workers can use Microsoft Teams to view their assigned tasks. Once a worker signs out of a shared device, Intune and Microsoft Entra ID clear all of the company data so the device can safely be handed off to the next associate. You can choose to integrate this capability into all your line of business [iOS](/en-us/entra/msal/objc/shared-devices-ios) and [Android](../identity-platform/msal-shared-devices) apps using the [Microsoft Authentication Library](../identity-platform/msal-overview).

![Screenshot of shared device sign-out.](media/concept-fundamentals-frontline-worker/shared-device-signout.png)