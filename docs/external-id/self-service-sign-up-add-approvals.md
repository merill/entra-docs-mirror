---
layout: Conceptual
title: Add custom approvals to self-service sign-up flows - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/self-service-sign-up-add-approvals
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Add API connectors for custom approval workflows in External ID self-service sign-up
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 37c2b73d-8562-512a-582a-113f4153cf9b
document_version_independent_id: 8944bf6a-c3ea-814e-92be-6a39ed0193f7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/self-service-sign-up-add-approvals.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/self-service-sign-up-add-approvals
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/self-service-sign-up-add-approvals.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 77d31a54-8a07-ab25-a1c7-a5f408eb1419
---

# Add custom approvals to self-service sign-up flows - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

With [API connectors](api-connectors-overview), you can integrate with your own custom approval workflows with self-service sign-up so you can manage which guest user accounts are created in your tenant.

This article gives an example of how to integrate with an approval system. In this example, the self-service sign-up user flow collects user data during the sign-up process and passes it to your approval system. Then, the approval system can:

- Automatically approve the user and allow Microsoft Entra ID to create the user account.
- Trigger a manual review. If the request is approved, the approval system uses Microsoft Graph to provision the user account. The approval system can also notify the user that their account has been created.

## Register an application for your approval system

You need to register your approval system as an application in your Microsoft Entra tenant so it can authenticate with Microsoft Entra ID and have permission to create users. Learn more about [authentication and authorization basics for Microsoft Graph](/en-us/graph/auth/auth-concepts).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **App registrations**, and then select **New registration**.
3. Enter a **Name** for the application, for example, *Sign-up Approvals*.
4. Select **Register**. You can leave other fields at their defaults.

![Screenshot that highlights the Register button.](media/self-service-sign-up-add-approvals/register-approvals-app.png)

1. Under **Manage** in the left menu, select **API permissions**, and then select **Add a permission**.
2. On the **Request API permissions** page, select **Microsoft Graph**, and then select **Application permissions**.
3. Under **Select permissions**, expand **User**, and then select the **User.ReadWrite.All** check box. This permission allows the approval system to create the user upon approval. Then select **Add permissions**.

![Screenshot of requesting API permissions.](media/self-service-sign-up-add-approvals/request-api-permissions.png)

1. On the **API permissions** page, select **Grant admin consent for (your tenant name)**, and then select **Yes**.
2. Under **Manage** in the left menu, select **Certificates & secrets**, and then select **New client secret**.
3. Enter a **Description** for the secret, for example *Approvals client secret*, and select the duration for when the client secret **Expires**. Then select **Add**.
4. Copy the value of the client secret. Client secret values can be viewed only immediately after creation. Make sure to save the secret when created, before leaving the page.

![Screenshot of copying the client secret. ](media/self-service-sign-up-add-approvals/client-secret-value-copy.png)

1. Configure your approval system to use the **Application ID** as the client ID and the **client secret** you generated to authenticate with Microsoft Entra ID.

## Create the API connectors

Next you'll [create the API connectors](self-service-sign-up-add-api-connector#create-an-api-connector) for your self-service sign-up user flow. Your approval system API needs two connectors and corresponding endpoints, like the examples shown below. These API connectors do the following:

- **Check approval status**. Send a call to the approval system immediately after a user signs-in with an identity provider to check if the user has an existing approval request or has already been denied. If your approval system only does automatic approval decisions, this API connector may not be needed. Example of a "Check approval status" API connector.

![Screenshot of check approval status API connector configuration.](media/self-service-sign-up-add-approvals/check-approval-status-api-connector-config-alt.png)

- **Request approval** - Send a call to the approval system after a user completes the attribute collection page, but before the user account is created, to request approval. The approval request can be automatically granted or manually reviewed. Example of a "Request approval" API connector.

![Screenshot of request approval API connector configuration.](media/self-service-sign-up-add-approvals/create-approval-request-api-connector-config-alt.png)

To create these connectors, follow the steps in [create an API connector](self-service-sign-up-add-api-connector#create-an-api-connector).

## Enable the API connectors in a user flow

Now you'll add the API connectors to a self-service sign-up user flow with these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**, and then select the user flow you want to enable the API connector for.
3. Select **API connectors**, and then select the API endpoints you want to invoke at the following steps in the user flow:

    - **After federating with an identity provider during sign-up**: Select your approval status API connector, for example *Check approval status*.
    - **Before creating the user**: Select your approval request API connector, for example *Request approval*.

![Screenshot of API connector in a user flow.](media/self-service-sign-up-add-approvals/api-connectors-user-flow-api.png)

1. Select **Save**.

## Control the sign-up flow with API responses

Your approval system can use its responses when called to control the sign-up flow.

### Request and responses for the "Check approval status" API connector

Example of the request received by the API from the "Check approval status" API connector:

```http
POST <API-endpoint>
Content-type: application/json

{
 "email": "johnsmith@fabrikam.onmicrosoft.com",
 "identities": [ //Sent for Google, Facebook, and Email One Time Passcode identity providers 
     {
     "signInType":"federated",
     "issuer":"facebook.com",
     "issuerAssignedId":"0123456789"
     }
 ],
 "displayName": "John Smith",
 "givenName":"John",
 "lastName":"Smith",
 "ui_locales":"en-US"
}
```

The exact claims sent to the API depend on which information is provided by the identity provider. 'email' is always sent.

#### Continuation response for "Check approval status"

The **Check approval status** API endpoint should return a continuation response if:

- The user hasn't previously requested an approval.

Example of the continuation response:

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "Continue"
}
```

#### Blocking response for "Check approval status"

The **Check approval status** API endpoint should return a blocking response if:

- User approval is pending.
- The user was denied and shouldn't be allowed to request approval again.

The following are examples of blocking responses:

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "ShowBlockPage",
    "userMessage": "Your access request is already processing. You'll be notified when your request has been approved.",
}
```

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "ShowBlockPage",
    "userMessage": "Your sign up request has been denied. Please contact an administrator if you believe this is an error",
}
```

### Request and responses for the "Request approval" API connector

Example of an HTTP request received by the API from the "Request approval" API connector:

```http
POST <API-endpoint>
Content-type: application/json

{
 "email": "johnsmith@fabrikam.onmicrosoft.com",
 "identities": [ // Sent for Google, Facebook, and Email One Time Passcode identity providers 
     {
     "signInType":"federated",
     "issuer":"facebook.com",
     "issuerAssignedId":"0123456789"
     }
 ],
 "displayName": "John Smith",
 "givenName":"John",
 "surname":"Smith",
 "jobTitle":"Supplier",
 "streetAddress":"1000 Microsoft Way",
 "city":"Seattle",
 "postalCode": "12345",
 "state":"Washington",
 "country":"United States",
 "extension_<extensions-app-id>_CustomAttribute1": "custom attribute value",
 "extension_<extensions-app-id>_CustomAttribute2": "custom attribute value",
 "ui_locales":"en-US"
}
```

The exact claims sent to the API depend on which information is collected from the user or is provided by the identity provider.

#### Continuation response for "Request approval"

The **Request approval** API endpoint should return a continuation response if:

- The user can be ***automatically approved***.

Example of the continuation response:

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "Continue"
}
```

Important

If a continuation response is received, Microsoft Entra ID creates a user account and directs the user to the application.

#### Blocking Response for "Request approval"

The **Request approval** API endpoint should return a blocking response if:

- A user approval request was created and is now pending.
- A user approval request was automatically denied.

The following are examples of blocking responses:

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "ShowBlockPage",
    "userMessage": "Your account is now waiting for approval. You'll be notified when your request has been approved.",
}
```

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "version": "1.0.0",
    "action": "ShowBlockPage",
    "userMessage": "Your sign up request has been denied. Please contact an administrator if you believe this is an error",
}
```

The `userMessage` in the response is displayed to the user, for example:

![Example pending approval page](media/self-service-sign-up-add-approvals/approval-pending.png)

## User account creation after manual approval

After the custom approval system obtains manual approval, it creates a [user](/en-us/graph/azuread-users-concept-overview) account by using [Microsoft Graph](/en-us/graph/use-the-api). The way your approval system provisions the user account depends on the identity provider that was used by the user.

### For a federated Google or Facebook user and email one-time passcode

Important

The approval system should explicitly check that `identities`, `identities[0]` and `identities[0].issuer` are present and that `identities[0].issuer` equals 'facebook', 'google' or 'mail' to use this method.

If your user signed in with a Google or Facebook account or email one-time passcode, you can use the [User creation API](/en-us/graph/api/user-post-users?tabs=http).

1. The approval system uses receives the HTTP request from the user flow.

```http
POST <Approvals-API-endpoint>
Content-type: application/json

{
 "email": "johnsmith@outlook.com",
 "identities": [
     {
     "signInType":"federated",
     "issuer":"facebook.com",
     "issuerAssignedId":"0123456789"
     }
 ],
 "displayName": "John Smith",
 "city": "Redmond",
 "extension_<extensions-app-id>_CustomAttribute": "custom attribute value",
 "ui_locales":"en-US"
}
```

1. The approval system uses Microsoft Graph to create a user account.

```http
POST https://graph.microsoft.com/v1.0/users
Content-type: application/json

{
 "userPrincipalName": "johnsmith_outlook.com#EXT@contoso.onmicrosoft.com",
 "accountEnabled": true,
 "mail": "johnsmith@outlook.com",
 "userType": "Guest",
 "identities": [
     {
     "signInType":"federated",
     "issuer":"facebook.com",
     "issuerAssignedId":"0123456789"
     }
 ],
 "displayName": "John Smith",
 "city": "Redmond",
 "extension_<extensions-app-id>_CustomAttribute": "custom attribute value"
}
```

| Parameter | Required | Description |
| --- | --- | --- |
| userPrincipalName | Yes | Can be generated by taking the `email` claim sent to the API, replacing the `@`character with `_`, and pre-pending it to `#EXT@<tenant-name>.onmicrosoft.com`. |
| accountEnabled | Yes | Must be set to `true`. |
| mail | Yes | Equivalent to the `email` claim sent to the API. |
| userType | Yes | Must be `Guest`. Designates this user as a guest user. |
| identities | Yes | The federated identity information. |
| &lt;otherBuiltInAttribute&gt; | No | Other built-in attributes like `displayName`, `city`, and others. Parameter names are the same as the parameters sent by the API connector. |
| &lt;extension\_{extensions-app-id}\_CustomAttribute&gt; | No | Custom attributes about the user. Parameter names are the same as the parameters sent by the API connector. |

### For a federated Microsoft Entra user or Microsoft account user

If a user signs in with a federated Microsoft Entra account or a Microsoft account, you must use the [invitation API](/en-us/graph/api/invitation-post) to create the user and then optionally the [user update API](/en-us/graph/api/user-update) to assign more attributes to the user.

1. The approval system receives the HTTP request from the user flow.

```http
POST <Approvals-API-endpoint>
Content-type: application/json

{
 "email": "johnsmith@fabrikam.onmicrosoft.com",
 "displayName": "John Smith",
 "city": "Redmond",
 "extension_<extensions-app-id>_CustomAttribute": "custom attribute value",
 "ui_locales":"en-US"
}
```

1. The approval system creates the invitation using the `email` provided by the API connector.

```http
POST https://graph.microsoft.com/v1.0/invitations
Content-type: application/json

{
    "invitedUserEmailAddress": "johnsmith@fabrikam.onmicrosoft.com",
    "inviteRedirectUrl" : "https://myapp.com"
}
```

Example of the response:

```http
HTTP/1.1 201 OK
Content-type: application/json

{
    ...
    "invitedUser": {
        "id": "<generated-user-guid>"
    }
}
```

1. The approval system uses the invited user's ID to update the user's account with collected user attributes (optional).

```http
PATCH https://graph.microsoft.com/v1.0/users/<generated-user-guid>
Content-type: application/json

{
    "displayName": "John Smith",
    "city": "Redmond",
    "extension_<extensions-app-id>_AttributeName": "custom attribute value"
}
```