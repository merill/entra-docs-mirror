---
layout: Conceptual
title: How to manage OATH tokens in Microsoft Entra ID (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-mfa-manage-oath-tokens
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about how to manage OATH tokens in Microsoft Entra ID to help improve and secure sign-in events.
services: active-directory
ms.topic: how-to
ms.date: 2025-03-26T00:00:00.0000000Z
ms.reviewer: lvandenende
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
locale: en-us
document_id: 80b99104-e861-2404-fb9c-93b3d30cf647
document_version_independent_id: 80b99104-e861-2404-fb9c-93b3d30cf647
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-mfa-manage-oath-tokens.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-mfa-manage-oath-tokens
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-mfa-manage-oath-tokens.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: b0bdfb8e-1430-4704-3c69-436461b7c156
---

# How to manage OATH tokens in Microsoft Entra ID (Preview) - Microsoft Entra ID | Microsoft Learn

This topic covers how to manage hardware oath tokens in Microsoft Entra ID, including Microsoft Graph APIs that you can use to upload, activate, and assign hardware OATH tokens.

## Manage hardware OATH tokens in the Authentication methods policy (Preview)

You can view and enable hardware OATH tokens in the Authentication methods policy by using Microsoft Graph APIs or the Microsoft Entra admin center.

- To view the hardware OATH tokens policy status by using the APIs:

    ```https
    GET https://graph.microsoft.com/beta/policies/authenticationMethodsPolicy/authenticationMethodConfigurations/hardwareOath
    ```
- To enable hardware OATH tokens policy by using the APIs.

    ```https
    PATCH https://graph.microsoft.com/beta/policies/authenticationMethodsPolicy/authenticationMethodConfigurations/hardwareOath
    ```

    In the request body, add:

    ```https
    {
      "state": "enabled"
    }
    ```

To enable hardware OATH tokens in the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Hardware OATH tokens (Preview)**.
3. Select **Enable**, choose which groups of users to include in the policy, and select **Save**.

    ![Screenshot of how to enable hardware OATH tokens in the Microsoft Entra admin center.](media/concept-authentication-oath-tokens/enable.png)

We recommend that you [migrate to the Authentication methods policy](how-to-authentication-methods-manage) to manage hardware OATH tokens. If you enable OATH tokens in the legacy MFA policy, browse to the policy in the Microsoft Entra admin center as an Authentication Policy Administrator: **Entra ID** &gt; **Multifactor authentication** &gt; **Additional cloud-based multifactor authentication settings**. Clear the checkbox for **Verification code from mobile app or hardware token**.

## Manage third-party software OATH tokens

Third-party software OATH tokens are enabled for sign in by default. An [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) can disable them to prevent users from signing in with a one-time password from a third-party Identity Provider.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Third-party software OATH tokens**.
3. Move the silder for the **Enable** control to prevent users from signing in with third-party software OATH tokens.
4. Click **I Acknowledge**, then click **Save**.

## Scenario: Admin creates, assigns, and activates a hardware OATH token

This scenario covers how to create, assign, and activate a hardware OATH token as an admin, including the necessary API calls and verification steps. For more information about the permissions required to invoke these APIs and to inspect the request-response samples, see [Create hardwareOathTokenAuthenticationMethodDevice](/en-us/graph/api/authenticationmethoddevice-post-hardwareoathdevices?view=graph-rest-beta&amp;preserve-view=true).

Note

There might be up to a 20-minute delay for the policy propagation. Allow an hour for the policy to update before users can sign in with their hardware OATH token and see it in their [Security info](https://mysignins.microsoft.com/security-info).

Let's look at an example where an Global Administrator creates a token and assigns it to a user. You can allow assignment without activation.

For the body of the POST in this example, you can find the **serialNumber** from your device and the **secretKey** is delivered to you.

```https
POST https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices
{ 
"serialNumber": "GALT11420104", 
"manufacturer": "Thales", 
"model": "OTP 110 Token", 
"secretKey": "C2dE3fH4iJ5kL6mN7oP1qR2sT3uV4w", 
"timeIntervalInSeconds": 30, 
"assignTo": {"id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"}
}
```

The response includes the token **id**, and the user **id** that the token is assigned to:

```http
{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#directory/authenticationMethodDevices/hardwareOathDevices/$entity",
    "id": "3dee0e53-f50f-43ef-85c0-b44689f2d66d",
    "displayName": null,
    "serialNumber": "GALT11420104",
    "manufacturer": "Thales",
    "model": "OTP 110 Token",
    "secretKey": null,
    "timeIntervalInSeconds": 30,
    "status": "available",
    "lastUsedDateTime": null,
    "hashFunction": "hmacsha1",
    "assignedTo": {
        "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
        "displayName": "Test User"
    }
}
```

Here's how the Authentication Policy Administrator can activate the token. Replace the verification code in the Request body with the code from your hardware OATH token.

```https
POST https://graph.microsoft.com/beta/users/00aa00aa-bb11-cc22-dd33-44ee44ee44ee/authentication/hardwareOathMethods/3dee0e53-f50f-43ef-85c0-b44689f2d66d/activate

{ 
    "verificationCode" : "903809" 
}
```

To validate the token is activated, sign in to [Security info](https://aka.ms/mysecurityinfo) as the test user. If you're prompted to approve a sign-in request from Microsoft Authenticator, select Use a verification code.

You can GET to list tokens:

```https
GET https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices 
```

This example Authentication Policy Administrator creates a single token:

```https
POST https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices
```

In the request body, add:

```https
{ 
"serialNumber": "GALT11420104", 
"manufacturer": "Thales", 
"model": "OTP 110 Token", 
"secretKey": "abcdef2234567abcdef2234567", 
"timeIntervalInSeconds": 30, 
"hashFunction": "hmacsha1" 
}

```

The response includes the token ID.

```http
#### Response
{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#directory/authenticationMethodDevices/hardwareOathDevices/$entity",
    "id": "3dee0e53-f50f-43ef-85c0-b44689f2d66d",
    "displayName": null,
    "serialNumber": "GALT11420104",
    "manufacturer": "Thales",
    "model": "OTP 110 Token",
    "secretKey": null,
    "timeIntervalInSeconds": 30,
    "status": "available",
    "lastUsedDateTime": null,
    "hashFunction": "hmacsha1",
    "assignedTo": null
}
```

Authentication Policy Administrators or an end user can unassign a token:

```https
DELETE https://graph.microsoft.com/beta/users/66aa66aa-bb77-cc88-dd99-00ee00ee00ee/authentication/hardwareoathmethods/6c0272a7-8a5e-490c-bc45-9fe7a42fc4e0
```

This example shows how to delete a token with token ID 3dee0e53-f50f-43ef-85c0-b44689f2d66d:

```https
DELETE https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices/3dee0e53-f50f-43ef-85c0-b44689f2d66d
```

## Scenario: Admin creates and assigns a hardware OATH token that a user activates

In this scenario, a Global Administrator creates and assigns a token, and then a user can activate it on their Security info page, or by using Microsoft Graph Explorer. When you assign a token, you can share steps for the user to sign in to [Security info](https://aka.ms/mysecurityinfo) to activate their token. They can choose **Add sign-in method** &gt; **Hardware token**. They need to provide the hardware token serial number, which is typically on the back of the device.

```https
POST https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices
{ 
"serialNumber": "GALT11420104", 
"manufacturer": "Thales", 
"model": "OTP 110 Token", 
"secretKey": "C2dE3fH4iJ5kL6mN7oP1qR2sT3uV4w", 
"timeIntervalInSeconds": 30, 
"assignTo": {"id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"}
}
```

An Authentication Administrator can assign the token to a user:

```https
POST https://graph.microsoft.com/beta/users/00aa00aa-bb11-cc22-dd33-44ee44ee44ee/authentication/hardwareOathMethods
{
    "device": 
    {
        "id": "6c0272a7-8a5e-490c-bc45-9fe7a42fc4e0" 
    }
}
```

Here are steps a user can follow to self-activate their hardware OATH token in Security info:

1. Sign in to [Security info](https://aka.ms/mysecurityinfo).
2. Select **Add sign-in method** and choose **Hardware token**.

    ![Screenshot of how to add a new sign-in method in Security info.](media/concept-authentication-oath-tokens/add-sign-in-method.png)
3. After you select **Hardware token**, select **Add**.

    ![Screenshot of how to add a hardware OATH token in Security info.](media/concept-authentication-oath-tokens/add-hardware-token.png)
4. Check the back of the device for the serial number, enter it, and select **Next**.

    ![Screenshot of how to add the serial number of a hardware OATH token.](media/concept-authentication-oath-tokens/add-serial-number.png)
5. Create a friendly name to help you choose this method to complete multifactor authentication, and select **Next**.

    ![Screenshot of how to add a friendly name for a hardware OATH token.](media/concept-authentication-oath-tokens/add-name.png)
6. Supply the random verification code that appears when you tap the button on the device. For a token that refreshes its code every 30 seconds, you need to enter the code and select **Next** within one minute. For a token that refreshes every 60 seconds, you have two minutes.

    ![Screenshot of how to add a verification code to activate a hardware OATH token.](media/concept-authentication-oath-tokens/add-code.png)
7. When you see the hardware OATH token is successfully added, select **Done**.

    ![Screenshot of a hardware OATH token after it's added.](media/concept-authentication-oath-tokens/success.png)
8. The hardware OATH token appears in the list of your available authentication methods.

    ![Screenshot of a hardware OATH token in Security info.](media/concept-authentication-oath-tokens/new-token.png)

Here are steps users can follow to self-activate their hardware OATH token by using Graph Explorer.

1. Open Microsoft Graph Explorer, sign in, and consent to the required permissions.
2. Make sure you have the required permissions. For a user to be able to do the self-service API operations, admin consent is required for `Directory.Read.All`, `User.Read.All`, and `User.ReadWrite.All`.
3. Get a list of hardware OATH tokens that are assigned to your account, but not yet activated.

    ```https
    GET https://graph.microsoft.com/beta/me/authentication/hardwareOathMethods
    ```
4. Copy the **id** of the token device, and add it to the end of the URL followed by */activate*. You need to enter the verification code in the request body and submit the POST call before the code changes.

    ```https
    POST https://graph.microsoft.com/beta/me/authentication/hardwareOathMethods/b65fd538-b75e-4c88-bd08-682c9ce98eca/activate
    ```

    Request body:

    ```https
    {
       "verificationCode": "988659"
    }
    ```

## Scenario: Admin creates multiple hardware OATH tokens in bulk that users self-assign and activate

In this scenario, an Authentication Policy Administrator creates tokens without assignment, and users self-assign and activate the tokens. You can upload new tokens to the tenant in bulk. Users can sign in to [Security info](https://aka.ms/mysecurityinfo) to activate their token. They can choose **Add sign-in method** &gt; **Hardware token**. They need to provide the hardware token serial number, which is typically on the back of the device.

For greater assurance that the token is only activated by a specific user, you can assign the token to the user, and send the device to them for self-activation.

```https
PATCH https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices
{
"@context":"#$delta", 
"value": [ 
    { 
        "@contentId": "1", 
        "serialNumber": "GALT11420108", 
        "manufacturer": "Thales", 
        "model": "OTP 110 Token", 
        "secretKey": "abcdef2234567abcdef2234567", 
        "timeIntervalInSeconds": 30, 
        "hashFunction": "hmacsha1" 
        },
    { 
        "@contentId": "2", 
        "serialNumber": "GALT11420112", 
        "manufacturer": "Thales", 
        "model": "OTP 110 Token", 
        "secretKey": "2234567abcdef2234567abcdef", 
        "timeIntervalInSeconds": 30, 
        "hashFunction": "hmacsha1" 
        }
    ]          
} 
```

## Troubleshooting hardware OATH token issues

This section covers common

### User has two tokens with the same serial number

A user might have two instances of the same hardware OATH token registered as authentication methods. This happens if the legacy token isn't removed from **OATH tokens (Preview)** in the Microsoft Entra admin center after it's uploaded by using Microsoft Graph.

When this happens, both instances of the token are listed as registered for the user:

```https
GET https://graph.microsoft.com/beta/users/{user-upn-or-objectid}/authentication/hardwareOathMethods
```

Both instances of the token are also listed in **OATH tokens (Preview)** in the Microsoft Entra admin center:

![Screenshot of the duplicate tokens in the Microsoft Entra admin center.](media/concept-authentication-oath-tokens/duplicate-tokens.png)

To identify and remove the legacy token.

1. List all hardware OATH tokens on the user.

    ```https
    GET https://graph.microsoft.com/beta/users/{user-upn-or-objectid}/authentication/hardwareOathMethods
    ```

    Find the **id** of both tokens and copy the **serialNumber** of the duplicate token.
2. Identify the legacy token. Only one token is returned in the response of the following command. That token was created by using Microsoft Graph.

    ```https
    GET https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices?$filter=serialNumber eq '20033752'
    ```
3. Remove the legacy token assignment from the user. Now that you know the **id** of the new token, you can identify the **id** of the legacy token from the list returned in step 1. Craft the URL using the legacy token **id**.

    ```https
    DELETE https://graph.microsoft.com/beta/users/{user-upn-or-objectid}/authentication/hardwareOathMethods/{legacyHardwareOathMethodId}
    ```
4. Delete the legacy token by using the legacy token **id** in this call.

    ```https
    DELETE https://graph.microsoft.com/beta/directory/authenticationMethodDevices/hardwareOathDevices/{legacyHardwareOathMethodId}
    ```