---
layout: Conceptual
title: How to enable QR code authentication in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-authentication-qr-code
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about how to enable QR code authentication method in Microsoft Entra ID to help improve and secure sign-in events for frontline workers.
ms.topic: how-to
ms.date: 2025-06-24T00:00:00.0000000Z
contributors: minatoruan
ms.reviewer: anjusingh
locale: en-us
document_id: c59d1f6d-257d-d326-ff82-3603d8fe3a72
document_version_independent_id: c59d1f6d-257d-d326-ff82-3603d8fe3a72
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-authentication-qr-code.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-authentication-qr-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-authentication-qr-code.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 8d4c6c1a-8850-b538-9746-6521b44c6cb7
---

# How to enable QR code authentication in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This topic covers how to enable the QR code authentication method in the Authentication methods policy in Microsoft Entra ID. It also covers how to manage the QR code authentication method for users, and how they can sign in with a QR code and PIN.

Before you enable QR code authentication method, review the best practices for using security controls for work or home access for frontline workers. For more information, see [Best practices to protect frontline workers](/en-us/entra/identity-platform/security-best-practices-for-frontline-workers).

## Prerequisites to enable the QR code authentication method

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription.
    - If needed, [create a Microsoft Entra tenant](../../fundamentals/sign-up-organization) or [associate an Azure subscription with your account](../../fundamentals/how-subscriptions-associated-directory).
- You need at least the [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) role in your Microsoft Entra tenant to enable the QR code authentication method.
- Each user that's enabled in the QR code authentication method policy must be licensed, even if they don't use it. Each enabled user must have one of the following Microsoft Entra ID, EMS, Microsoft 365 licenses:
    - [Microsoft 365 F1 or F3](https://www.microsoft.com/licensing/news/m365-firstline-workers)
    - [Microsoft Entra ID P1 or P2](https://www.microsoft.com/security/business/microsoft-entra-pricing)
    - [Enterprise Mobility + Security (EMS) E3 or E5](https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing) or [Microsoft 365 E3 or E5](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans)
    - [Office 365 F3](https://www.microsoft.com/microsoft-365/business/office-365-f3?activetab=pivot%3aoverviewtab)
- Android, iOS, or iPadOS (iOS/iPadOS version 15.0 or later) shared devices.
- Shared device mode enabled on the shared devices (optional but highly recommended).
- A printer to print 2" x 2" QR codes.
- To access QR code authentication on Teams, Teams app installed on the shared device would require these versions: Android version 1.0.0.2024143204 or later, and iOS version 1.0.0.77.2024132501 or later.
- [Set up the My Staff portal](../role-based-access-control/my-staff-configure) if you plan for frontline managers to use My Staff to provision, manage, and reset QR code and PINs.

## Enable QR code authentication method

You can enable the QR code authentication method by using the Microsoft Entra admin center or Microsoft Graph API.

### Enable QR code authentication method in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Go to **Entra ID** &gt; **Authentication methods** &gt; **Policies**.
3. Click **QR code** &gt; **Enable and target** &gt; **Add target** &gt; select a group of users who need to sign in with a QR code.

    ![Screenshot that shows how to enable QR code for an organization.](media/how-to-authentication-qr-code/enable-qr-code.png)
4. Update default QR code settings as needed:

    - By default, the PIN length is 8 digits. The PIN length can be 8 to 20 digits. If you increase the PIN length, the new value becomes the minimum number of digits required for the PIN. For example, if you increase the PIN length to 10, a user needs to provide a 10-digit PIN during next sign-in.
    - The default lifetime of a standard QR code (provided to the users for long term use) is 365 days. The range is between 1-395 days. You can change the lifetime of a standard QR code for specific user when you add the QR code authentication method for them.

    ![Screenshot that shows how to updates QR code settings.](media/concept-authentication-qr-code/qr-code-settings.png)
5. When you're done, click **Save**.

### Enable QR code authentication method in Microsoft Graph API

This example enables QR code authentication for a group, with a PIN length of 10 digits, and a Standard QR code lifetime of 395 days:

- **Request**

    ```https
    PATCH https://graph.microsoft.com/beta/policies/authenticationMethodsPolicy/authenticationMethodConfigurations/qrCodePin
    {
      "@odata.type" : "microsoft.graph.qrCodePinAuthenticationMethodConfiguration", 
      "id": "qrCodePin", 
      "state": "enabled", 
      "includeTargets": [{ 
        "targetType": "group", 
        "id": "b185b746-e7db-4fa2-bafc-69ecf18850dd", 
        }], 
      "excludeTargets": [], 
      "standardQRCodeLifetimeInDays":395,
      "pinLength": 10
    }
    ```
- **Response**

    ```https
    204 No Response
    ```

## Add QR code authentication method for a user

You can add a QR code authentication method for a user by using the Microsoft Entra admin center, My Staff, or Microsoft Graph API. At a time, only one active QR code auth method is allowed. Standard QR code is generated during 'Add authentication method'. You can add Temporary QR code, which is short-lived, if user is not carrying Standard QR code. You can delete Standard/Temporary QR code to add a new Standard/Temporary QR code. A user can have only one Standard and one Temporary QR code active at any point of time.

### Add QR code authentication method for a user in the Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator).
2. Go to **Users**, select a user, and click **Authentication methods**.
3. Click **Add authentication method** and choose **QR code**.

    ![Screenshot that shows how to choose QR code for a user.](media/how-to-authentication-qr-code/choose-qr-code.png)
4. Modify the expiration date for the user if needed. Set **Activation time** to now or later. Provide or generate a temporary PIN. The custom PIN can be specified only when you add the QR code authentication method. A PIN is autogenerated during reset events. When ready, click **Add** to add the QR code authentication method for the user.

    ![Screenshot that shows how to add QR code for a user.](media/how-to-authentication-qr-code/add-qr-code.png)
5. Save the PIN, and click **Download image** to download and print the QR code. The QR code image download has the smallest optimal print size. If you reduce the size of the QR code, it may impact QR code scan performance.

    You can't regenerate the same QR code because it has a unique secret. If the QR code can't work for some reason, delete it. Create a new QR code for the user.

    ![Screenshot that shows how to download the QR code image for a user.](media/how-to-authentication-qr-code/download-qr-code.png)
6. After you add the QR code authentication method, it appears as a usable authentication method for the user.

    ![Screenshot that shows the QR code authentication method listed in usable authentication methods for a user.](media/how-to-authentication-qr-code/usable-authentication-methods.png)

### Add the QR code authentication method for a user in My Staff

1. Sign in to the My Staff portal as a frontline manager. Select an administrative unit and a frontline worker.

    ![Screenshot that shows how to select an admin unit.](../../includes/media/add-qr-code-my-staff/select-admin-unit.png)

    ![Screenshot that shows how to select a user.](../../includes/media/add-qr-code-my-staff/select-user.png)
2. Click **Manage QR code authentication method**.

    ![Screenshot that shows how to manage a QR code authentication method.](../../includes/media/add-qr-code-my-staff/manage-qr-code-authentication-method.png)
3. Click **Add QR code method**.

    ![Screenshot that shows how to add a QR code authentication method.](../../includes/media/add-qr-code-my-staff/add-qr-code-authentication-method.png)
4. Specify the expiration and activation date, and click **Add** to generate a QR code and PIN for the user.

    ![Screenshot that shows how to set the activation date for a QR code authentication method.](../../includes/media/add-qr-code-my-staff/activation-date.png)
5. Save the PIN, download or print the QR code, and then click **Done**. The QR code image download has the smallest optimum print size. If you reduce the size, the QR code is hard to scan. You can't regenerate the same QR code because it has a unique secret. If the QR code can't work for some reason, delete it. Create a new QR code for the user.

    ![Screenshot that shows a QR code authentication method after an administrator adds it.](../../includes/media/add-qr-code-my-staff/qr-code-done.png)

### Add QR code authentication method for a user in Microsoft Graph API

This example adds QR code authentication method for a user:

- **Request**

    ```https
    HTTP PUT/users/{id | userPrincipalName}/authentication/qrCodePinMethod

    {
      "standardQRCode": {
        "expireDateTime": "2024-12-30T12:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
      },
      "pin": {
        "code": "<PIN>"
      }
    }
    ```
- **Response**

    ```https
    HTTP/1.1 201 Created
    Location: /beta/users/aaaaaaaa-bbbb-cccc-1111-222222222222/authentication/qrCodePinMethod`
    Content-type: application/json
    
    {
      "standardQRCode": {
        "id": "BBBBBBBB-1C1C-2D2D-3E3E-444444444444"
        "expireDateTime": "2024-12-30T12:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
        "createdDateTime": "2024-10-30T12:00:00Z",
        "lastUsedDateTime": null,
         "image":
            {
      "binaryValue": "<binaryImageData>",
             "version": 1,
             "errorCorrectionLevel": "H".
             "rawContent": <binary data encoded in QR>        
      }
        },
      "temporaryQRCode": null,
      "pin": {
        "code": "<PIN>",
        "isForcePinChangeRequired": true,
        "createdDateTime": "2024-10-30T12:00:00Z",
        "updatedDateTime": null
      }  
    }
    ```

This example confirms whether QR code authentication method is added for the user:

- **Request**

    ```https
    GET https://graph.microsoft.com/beta/users/flokreg@contoso.com/authentication/qrCodePinMethod`
    ```
- **Response**

    ```https
    HTTP/1.1 200 OK
    Content-type: application/json
    
    {
      "id": "<id>",
      "standardQRCode": {
        "id": "BBBBBBBB-1C1C-2D2D-3E3E-444444444444"
        "image": null,
        "expireDateTime": "2024-12-30T12:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
        "createdDateTime": "2024-10-30T12:00:00Z",
        "lastUsedDateTime": "2024-12-30T12:00:00Z"
      },
      "temporaryQRCode": {
        "id": "CCCCCCCC-2D2D-3E3E-4F4F-555555555555"
        "image": null,
        "expireDateTime": "2024-12-30T12:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
        "createdDateTime": "2024-10-30T12:00:00Z",
        "lastUsedDateTime": "2024-12-30T12:00:00Z"
      },
      "pin": {
        "code": null,
        "isForcePinChangeRequired": false,
        "createdDateTime": "2024-10-30T12:00:00Z",
        "updatedDateTime": "2024-11-30T12:00:00Z"
      }
    }
    
    ```

## Edit the QR code authentication method for a user

You can edit QR code authentication method for a user by using the Microsoft Entra admin center, My Staff, or Microsoft Graph API.

### Edit the QR code authentication method for a user in the Microsoft Entra admin center

- Navigate to the usable authentication methods for a user, and click **Edit** to edit the properties of the QR code authentication method.

    ![Screenshot that shows how to edit the usable authentication method for a user.](media/how-to-authentication-qr-code/edit-usable-authentication-method.png)
- Change the expiration time for the standard QR code, and click **Save**. After you make edits, click **Done**.

    ![Screenshot that shows how to change the expiration date.](media/how-to-authentication-qr-code/change-expiration.png)
- Delete a standard QR code. You might want to delete the standard QR code if it's reported as expired, compromised, or stolen.

    ![Screenshot that shows how to delete a QR code.](media/how-to-authentication-qr-code/delete-qr-code.png)

    After you delete the standard QR code, click the add symbol (**+**) to add a new standard QR code for the user. The deleted QR code is no longer valid for login.

    You need to print and distribute the new QR code to the user. The user can continue to use their existing PIN.

    ![Screenshot that shows how to replace a lost or stolen QR code.](media/how-to-authentication-qr-code/replace-qr-code.png)
- Reset a PIN. If you need to reset a user PIN, generate a temporary one and distribute it to the user. The user will be required to change the temporary PIN at the next sign-in. Click the pencil icon after the masked PIN. Click **Generate new PIN** to create a new temporary PIN. Click **OK** to confirm that the user is forced to change the temporary PIN when they next sign in. Copy the temporary PIN and share it with the user.

    ![Screenshot that shows how to reset a PIN.](media/how-to-authentication-qr-code/reset-pin.png)
- Add or delete a temporary QR code. A temporary QR code reduces admin overhead of provisioning and deprovisioning the QR code on a badge if a user didn't bring their badge to work. It also reduces the stress of retaining the QR code after their shift. A temporary QR code has a lifetime of 1-12 hours and can be activated instantly or later. To deprovision the QR code, you can delete the temporary QR code or let it expire as it's unusable after expiry.

    ![Screenshot that shows how to add a temporary QR code.](media/how-to-authentication-qr-code/add-temporary-qr-code.png)

    ![Screenshot that shows how to download a temporary QR code.](media/how-to-authentication-qr-code/download-temporary-qr-code.png)

### Edit the QR code authentication method for a user in My Staff

- To edit the expiration date for a standard QR code, click **Edit**. Edit the expiration date and save the changes.

    ![Screenshot that shows how to edit a QR code in My Staff.](../../includes/media/edit-qr-code-my-staff/edit-qr-code-my-staff.png)
- To delete a standard QR code, click **Delete**, and confirm the action.

    ![Screenshot that shows how to delete a QR code in My Staff.](../../includes/media/edit-qr-code-my-staff/delete-qr-code-my-staff.png)
- To add a new standard QR code, click **Add new** next to the standard QR code.

    ![Screenshot that shows how to add a new QR code in My Staff.](../../includes/media/edit-qr-code-my-staff/add-new-qr-code-my-staff.png)

    Select the activation time and expiration date for the QR code, and click **Add**.

    ![Screenshot that shows how to select the expiration date of a QR code in My Staff.](../../includes/media/edit-qr-code-my-staff/select-qr-code-expiration-my-staff.png)

    Download or print the QR code, and click **Done**.

    ![Screenshot that shows how to view a newly added QR code in My Staff.](../../includes/media/edit-qr-code-my-staff/view-qr-code-my-staff.png)
- To add a temporary QR code, click **Add new** next to the temporary QR code. Specify the **Lifetime in hours** and the **Activation date**, and click **Add**.

    ![Screenshot that shows how to set the expiration date for a temporary QR code.](../../includes/media/edit-qr-code-my-staff/set-temporary-qr-code-expiration.png)

    Download or print the QR code, and click **Done**.

    ![Screenshot that shows how to view a temporary QR code in My Staff.](../../includes/media/edit-qr-code-my-staff/view-temporary-qr-code-my-staff.png)
- To reset a PIN, click **Reset PIN**.

    ![Screenshot that shows how to reset a PIN in My Staff.](../../includes/media/edit-qr-code-my-staff/reset-pin-my-staff.png)

    Click **Copy PIN** to copy the PIN to your clipboard.

    ![Screenshot that shows how to copy a PIN in My Staff.](../../includes/media/edit-qr-code-my-staff/copy-pin-my-staff.png)

### Edit the QR code authentication method for a user in Microsoft Graph API

This example shows how to delete the standard QR code for a user if they lose their badge, and create a new standard QR code. The user isn't required to change their PIN.

Delete a standard QR code:

- **Request**

    ```https
    DELETE https://graph.microsoft.com/beta/users/flokreg@contoso.com/authentication/qrCodePinMethod/standardQRCode`
    ```
- **Response**

    ```https
    HTTP/1.1 204 No Content
    ```

Create a standard QR code:

- **Request**

    ```https
    HTTP PATCH/users/{id | userPrincipalName}/authentication/qrCodePinMethod/standardQRCode`

    {
        "startDateTime": "2024-10-30T12:00:00Z",
        "expireDateTime": "2024-12-30T12:00:00Z"
    }
    ```
- **Response**

    ```https
    HTTP/1.1 201 Created
    Location: /beta/users/aaaaaaaa-bbbb-cccc-1111-222222222222/authentication/qrCodePinMethod/standardQRCode`
    Content-type: application/json
    
    {
        "id": "BBBBBBBB-1C1C-2D2D-3E3E-444444444444"
        "expireDateTime": "2024-12-30T12:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
        "createdDateTime": "2024-10-30T12:00:00Z",
        "lastUsedDateTime": null,
         "image":
            {
      "binaryValue": "<binaryImageData>",
             "version": 1,
             "errorCorrectionLevel": "H".
             "rawContent": <binary data encoded in QR>        
      }
      }
    
    ```

Get a standard QR code:

- **Request**

    ```https
    GET https://graph.microsoft.com/beta/users/{id|UPN}/authentication/qrCodePinMethod/standardQRCode`
    ```
- **Response**

    ```https
    HTTP/1.1 200 OK
    Content-type: application/json
    
    {
        "id": "BBBBBBBB-1C1C-2D2D-3E3E-444444444444",
        "image": null,
        "expireDateTime": "2024-12-30T12:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
        "createdDateTime": "2024-10-30T12:00:00Z",
        "lastUsedDateTime": "2024-12-30T12:00:00Z"
    }
    
    ```

This example shows how to create a temporary QR code for a user. The user can use the existing PIN. This operation returns an error if a temporary QR code already exists for the user, or if the **expireDateTime** is more than 12 hours past the **startDateTime**.

- **Request**

    ```https
    HTTP PATCH/users/{id | userPrincipalName}/authentication/qrCodePinMethod/temporaryQRCode`

    {
        "startDateTime": "2024-10-30T12:00:00Z",
        "expireDateTime": "2024-10-30T22:00:00Z"
    }
    ```
- **Response**

    ```https
    HTTP/1.1 201 Created
    Location: /beta/users/aaaaaaaa-bbbb-cccc-1111-222222222222/authentication/qrCodePinMethod/temporaryQRCode`
    Content-type: application/json
    
    {
        "id": "EEEEEEEE-4F$F-5A5A-6B6B-777777777777"
        "expireDateTime": "2024-10-30T22:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
        "createdDateTime": "2024-10-30T12:00:00Z",
        "lastUsedDateTime": null,
         "image":
            {
      "binaryValue": "<binaryImageData>",
             "version": 1,
             "errorCorrectionLevel": "H".
             "rawContent": <binary data encoded in QR>        
      }
      }

    ```

Get a temporary QR code:

- **Request**

    ```https
    GET https://graph.microsoft.com/beta/users/{id|UPN}/authentication/qrCodePinMethod/temporaryQRCode`
    ```
- **Response**

    ```https
    HTTP/1.1 200 OK
    Content-type: application/json
    
    {
        "id": "EEEEEEEE-4F$F-5A5A-6B6B-777777777777",
        "image": null,
        "expireDateTime": "2024-10-30T22:00:00Z",
        "startDateTime": "2024-10-30T12:00:00Z"
        "createdDateTime": "2024-10-30T12:00:00Z",
        "lastUsedDateTime": "2024-10-30T20:00:00Z"
    }
    
    ```

This example shows how to delete a temporary QR code for a user.

- **Request**

    ```https
    DELETE https://graph.microsoft.com/beta/users/flokreg@contoso.com/authentication/qrCodePinMethod/temporaryQRCode`
    ```
- **Response**

    ```https
    HTTP/1.1 204 No Content
    ```

This example shows how to reset the PIN a QR code authentication method:

- **Request**

    ```https
    PATCH https://graph.microsoft.com/beta/users/flokreg@contoso.com/authentication/qrCodePinMethod/pin`
    ```
- **Response**

    ```https
    {
      "code": <PIN>,
      "forceChangePinNextSignIn": true,
      "createdDateTime": "2024-10-30T12:00:00Z",
      "updatedDateTime": null
    }
    ```

This example shows how to force a user to change their PIN for a QR code authentication method:

- **Request**

    ```https
    PATCH https://graph.microsoft.com/beta/users/flokreg@contoso.com/authentication/qrCodePinMethod/updatePin`
    
    {
      "currentPin": "<Old PIN>",
      "newPin": "<New PIN>"
    }
    ```
- **Response**

    ```https
    HTTP/1.1 204 No Content
    ```

## Delete the QR code authentication method for a user

You can delete the QR code authentication method for a user by using the Microsoft Entra admin center, My Staff, or Microsoft Graph API.

### Delete the QR code authentication method for a user in the Microsoft Entra admin center

If a QR code authentication method is deleted for a user, they can no longer sign in by using that authentication method.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Administrator](../role-based-access-control/permissions-reference#authentication-administrator).
2. Go to **Users**, select a user, and click **Authentication methods**.
3. Under **Usable authentication methods**, click the ellipsis on the right side of the QR code, and click **Delete**.

    ![Screenshot that shows how to delete the QR code authentication method for a user in the Microsoft Entra admin center.](media/how-to-authentication-qr-code/delete-qr-code-method-admin-center.png)

### Delete the QR code authentication method for a user in My Staff

1. To delete the QR code auth method itself, click **Delete QR code method**.

    ![Screenshot that shows how to delete the QR code authentication method in My Staff.](../../includes/media/delete-qr-code-authentication-method-my-staff/delete-qr-code-method-my-staff.png)
2. Click **Delete** to confirm the action.

    ![Screenshot that shows how to confirm deletion of the QR code authentication method in My Staff.](../../includes/media/delete-qr-code-authentication-method-my-staff/confirm-delete-qr-code-method-my-staff.png)

### Delete the QR code authentication method for a user in Microsoft Graph API

This example shows how to delete a standard QR code for a user.

- **Request**

    ```https
    DELETE https://graph.microsoft.com/beta/users/flokreg@contoso.com/authentication/qrCodePinMethod/standardQRCode`
    ```
- **Response**

    ```https
    HTTP/1.1 204 No Content
    ```

## Sign in to Microsoft Teams or Managed Home Screen (MHS) with QR code

Microsoft Teams and Managed Home Screen (MHS) have an optimized QR code sign-in experience. An Authentication Policy Administrator needs to configure Intune or another mobile device management (MDM) solution to enable the QR code authentication method for mobile devices.

### Enable sign-in with a QR code in Teams or MHS

When configuring with Intune, assign Microsoft Authenticator as a required app for all devices you want to add QR code authentication for.

| Platform | MDM app config key | Value | Configuration location |
| --- | --- | --- | --- |
| iOS | preferred\_auth\_config | qrpin | Device management profile, which configures a single sign-on (SSO) extension |
| Android | preferred\_auth\_config | qrpin | Microsoft Authenticator |

Note

MHS is only available on Android devices.

### QR code authentication Teams sign-in experience

Users need to [download Teams](https://aka.ms/teamsmobiledownload). The following table lists the minimum Teams version for mobile operating systems. For more information about Teams versions, see [Version update history for the new and classic Microsoft Teams app](/en-us/officeupdates/teams-app-versioning).

| Mobile OS | Release date | Teams version |
| --- | --- | --- |
| iOS and iPadOS | July 21, 2024 | 6.13.1 (1.0.0.77.2024132501) |
| Android | August 08, 2024 | 1416/1.0.0.2024143204 (2024143204) |

Users can follow these steps to sign in with a QR code in Teams:

1. Click **Scan QR code** in Microsoft Teams.
2. Scan the QR code. Give consent if you're asked for camera permission.
3. Enter your PIN.
4. You're now signed in to the app.

    ![Screenshot that shows how to enter a PIN.](media/how-to-authentication-qr-code/enter-pin.png)
5. When you sign in with a temporary PIN, you need to change it.

    ![Screenshot that shows how to change a PIN.](media/how-to-authentication-qr-code/change-pin.png)

## QR code authentication web sign-in experience (login.microsoftonline.com)

1. Click **More sign-in options** &gt; **Sign in to an organization** &gt; **Sign in with QR code**.
2. Allow the camera when prompted &gt; scan the QR code &gt; enter your PIN &gt; you're successfully signed in.

    ![Screenshot that shows web sign-in experience.](media/concept-authentication-qr-code/sign-in-web.png)

## Add security with QR code authentication using Conditional Access policies

Restrict the QR code authentication method to only frontline workers, compliant, and shared devices. This section covers how to create policies that restrict QR code authentication method to only frontline workers and shared devices.

### Restrict QR code authentication to frontline workers

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **QR code** &gt; **Enable and target**.
3. Click **Add target** &gt; select a group that only includes frontline workers, such as **Frontline workers** in the following screenshot. This group selection restricts enablement of the QR code authentication method only to frontline workers added to the **Frontline workers** group.

    ![Screenshot that shows the Microsoft Entra admin center that shows how to add groups to the QR code settings.](media/how-to-authentication-qr-code/add-groups-and-roles.png)

### Restrict QR code authentication to shared devices

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator).
2. Click **Conditional Access** &gt; **Authentication strengths** &gt; **New authentication strength**.

    ![Screenshot that shows how to create a new authentication strength.](media/how-to-authentication-qr-code/new-authentication-strength.png)
3. Create a custom authentication strength Conditional Access policy. Select authentication **QR code**.
4. Create a Conditional Access policy that requires shared devices be marked as compliant with policies from Intune or another MDM solution. This policy makes sure that frontline workers can access only specific resources from a compliant, shared device that they signed into with a QR code.

    1. Under **Users or workload identities** &gt; **Include** &gt; select **Users and groups**, and choose your **Frontline workers** frontline worker group.
    2. Under **Target resources** &gt; **Include** &gt; select specific resources that frontline workers can access.
    3. Under **Conditions**, click **Filter for devices**, set **Configure** to **Yes**.
    4. Click **Include filtered devices from policy**.
    5. For **Property**, select **ProfileType**.
    6. For **Operator**, select **Equals**.
    7. For **Value**, select **Shared**.

        ![Screenshot that shows how to include filtered devices from a policy for an authentication strength.](media/how-to-authentication-qr-code/include-filtered-devices.png)
    8. Under **Access controls** &gt; **Grant** &gt; select **Require device to be marked as compliant**, and click **Select**.
    9. Click **Create**.