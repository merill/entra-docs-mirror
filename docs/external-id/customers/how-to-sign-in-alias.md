---
layout: Conceptual
title: Sign in with alias - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-sign-in-alias
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to sign in and sign up with alias/username with External ID for customer identity and access management (CIAM). Get detailed steps to enable username as a sign-in identifier and create users with both email address and username.
ms.topic: how-to
ms.date: 2026-01-13T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 69cb866e-f3e6-12af-2ba2-32685f93ebdf
document_version_independent_id: 69cb866e-f3e6-12af-2ba2-32685f93ebdf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-sign-in-alias.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-sign-in-alias
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-sign-in-alias.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: cb5e6b30-23da-cbf2-901c-11e8958133d5
---

# Sign in with alias - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

You can allow users who sign in with an email address and password also sign up or sign in with a username and password. A username, also called an alternate sign-in identifier, can be a customer ID, account number, or another identifier that you choose.

![Screenshot of the username sign-in option.](media/how-to-sign-in-alias/username-login-option.png)

## Prerequisites

- If you haven't already created your own Microsoft Entra external tenant, [create one now](how-to-create-external-tenant-portal).
- [Register an app](/en-us/entra/identity-platform/quickstart-register-app).
- [Create a user flow](how-to-user-flow-sign-up-sign-in-customers).
- [Add your application](how-to-user-flow-add-application) to the user flow.

## Enable username in sign-in identifier policy

To enable username as a sign-in identifier, first enable the sign-in identifier policy in the Microsoft Entra admin center. UserPrincipalName (UPN) and email address are selected by default. Once username is also enabled, users who have been assigned a username will be able to sign in using either their email address or username.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. Browse to **Sign-in identifiers** either from **Entra ID** &gt; **External Identities** or from **Entra ID** &gt; **Authentication methods**.
4. On the **Sign-in identifiers** page, enable **Username** as a sign-in identifier by choosing **Default regex**, which accepts any string, or specifying up to two custom regular expression patterns for stricter validation. If any pattern matches, the username is considered valid. Note that there is no built-in validation for custom regular expressions, apart from ensuring they don’t match the format of an email address. Authentication may fail at runtime if the provided value doesn’t match the regex or if the regex itself is invalid.

    [![Screenshot of the Sign-in identifiers option in the Microsoft Entra admin center.](media/how-to-sign-in-alias/sign-in-identifiers.png)](media/how-to-sign-in-alias/sign-in-identifiers.png#lightbox)
5. Select **Save** at the top of the page.

## Create and update users with username

Once you enable username as a sign-in identifier, you can create new users with both email address and username as sign-in identifiers. You can also update existing users to add a username. You can do this using either the Microsoft Entra admin center or the Microsoft Graph API.

# [Microsoft Entra admin center](#tab/admin-center)
### Create users with username in the admin center

You can create external users with both email address and username as sign-in identifiers using either the Microsoft Entra admin center or the Microsoft Graph API. This section describes creating users in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. In your external tenant, browse to **Entra ID** &gt; **Users**.
4. Select **+ New user** &gt; **Create external user**.
5. Next to **Identities**, enter values for both **Email** and **User Name** sign-in methods. The selection order doesn’t matter.

    [![Screenshot of the Sign-in method dropdown in the Create external user pane in the Microsoft Entra admin center.](media/how-to-sign-in-alias/sign-in-method-dropdown.png)](media/how-to-sign-in-alias/sign-in-method-dropdown.png#lightbox)
6. On the **Properties** tab, specify the email attribute for the user.

    [![Screenshot of the Email attribute field in the Create external user pane in the Microsoft Entra admin center.](media/how-to-sign-in-alias/email-attribute.png)](media/how-to-sign-in-alias/email-attribute.png#lightbox)
7. Select **Review + create** to create the user.

### Update existing users to add a username in the admin center

Follow these steps to add a username to an existing external user in the Microsoft Entra admin center. Username can only be added to external users with email and password accounts.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. In your external tenant, browse to **Entra ID** &gt; **Users**.
4. Select the external user you want to update.
5. In the user pane, select **Edit properties**.
6. On the **Identity** tab, in the **Identities** section select **+ Add identity**.
7. Select **User Name** from the dropdown and enter the username you want to assign to the user.

    [![Screenshot of adding username to an existing user in the Microsoft Entra admin center.](media/how-to-sign-in-alias/edit-user-to-add-alias.png)](media/how-to-sign-in-alias/edit-user-to-add-alias.png#lightbox)
8. Select **Save** to apply the changes.

# [Microsoft Graph API](#tab/graph-api)
### Create users with username with the Microsoft Graph API

After you sign in to the [MS Graph explorer](https://developer.microsoft.com/en-us/graph/graph-explorer), you can use the [Users API](/en-us/graph/api/user-post-users) to create users with both email address and username as sign-in identifiers. The following request example shows how to create a user with both email address and username as sign-in identifiers.

```http
POST https://graph.microsoft.com/v1.0/users
Content-type: application/json
{
    "displayName": "Test User",
    "identities": [
        {
            "signInType": "emailAddress",
            "issuer": "contoso.onmicrosoft.com",
            "issuerAssignedId": "dylan@woodgrovebank.com"
        },
        {
            "signInType": "username",
            "issuer": "contoso.onmicrosoft.com",
            "issuerAssignedId": "dylan123"
        }
    ],
    "mail": "dylan@woodgrovebank.com",
    "passwordProfile": {
        "password": "passwordValue",
        "forceChangePasswordNextSignIn": false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

### Add a username to existing users with the Microsoft Graph API

You can also add a username to an existing external user.

### Step 1: Get the user details

Use `$filter` to get the user object, and `$select` to return the ID and `identities[]` properties. The following request example shows how to retrieve a user account using the email address as a sign-in identifier.

```http
GET https://graph.microsoft.com/v1.0/users?$select=displayName,id,identities&$filter=identities/any(c:c/issuerAssignedId eq 'dylan@woodgrovebank.com' and c/issuer eq 'contoso.onmicrosoft.com')
```

The following response example shows the response with the user details.

```http
HTTP/1.1 200 OK
Content-type: application/json
 
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users(displayName,id,identities)",
    "value": [
        {
            "displayName": "ciam test 1",
            "id": "0daaf9dd-3583-4cd4-8934-a2ffd0490287",
            "identities": [
                {
                    "signInType": "userPrincipalName",
                    "issuer": "contoso.onmicrosoft.com",
                    "issuerAssignedId": "0daaf9dd-3583-4cd4-8934-a2ffd0490287@contoso.onmicrosoft.com"
                },
                {
                    "signInType": "emailAddress",
                    "issuer": "contoso.onmicrosoft.com",
                    "issuerAssignedId": "dylan@woodgrovebank.com"
                }
            ]
        }
    ]
}
```

### Step 2: Update the user details

Once you have the user details from the query above, you can update the `identities[]` property of the user. You must replace the entire `identities[]` property of the user.

The following request example shows how to update the `identities[]` property of an email/password user to add a username.

```http
POST https://graph.microsoft.com/v1.0/users/00aa00aa-bb11-cc22-dd33-44ee44ee44ee
Content-type: application/json 
{
            "identities": [
                {
                    "signInType": "userPrincipalName",
                    "issuer": "contoso.onmicrosoft.com",
                    "issuerAssignedId": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee@contoso.onmicrosoft.com"
                },
                {
                    "signInType": "emailAddress",
                    "issuer": "contoso.onmicrosoft.com",
                    "issuerAssignedId": "dylan@woodgrovebank.com"
                },
                {
                    "signInType": "userName",
                    "issuer": "contoso.onmicrosoft.com",
                    "issuerAssignedId": "dylan1234"
                }
            ]
}
```

---

## Sign up with an alias or username (preview)

You can allow users to sign up with a username or alias in addition to their email address in Microsoft Entra External ID. During sign-up, you collect the username from the user. The username must be unique across the tenant. To configure your user flow to collect a username, follow these steps.

### Step 1: Add the username attribute to your user flow

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-policy-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to your external tenant from the **Directories + subscriptions** menu.
3. In your external tenant, browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
4. Select the user flow you created in the prerequisites.
5. Under **Settings**, select **User attributes**.
6. Select the **Username** attribute.
7. Select **Save** to add the attribute to your user flow.

    [![Screenshot of the Username attribute in the Microsoft Entra admin center.](media/how-to-sign-in-alias/username-attribute.png)](media/how-to-sign-in-alias/username-attribute.png#lightbox)

### Step 2: (Optional) Change the label of the username field

You can change the label of the username field that appears on the sign-up page.

1. In your external tenant, browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
2. Go to **Page Layout**.
3. Find the **Username** attribute and edit the label. For example, you can change it to "Alias" or "User ID".
4. Select **Save**.

    [![Screenshot of the change label option in the Microsoft Entra admin center.](media/how-to-sign-in-alias/change-label.png)](media/how-to-sign-in-alias/change-label.png#lightbox)

### Step 3: (Optional) Set custom validation regex for username with Microsoft Graph API

You can set a custom regular expression for input validation by configuring the `validationRegEx` for the username attribute. This setting isn't currently available in the admin center UI, but you can configure it using Microsoft Graph. To set this value, use the [authenticationAttributeCollectionInputConfiguration](/en-us/graph/api/resources/authenticationattributecollectioninputconfiguration) resource type. For reference, see the example on [updating the page layout of a self-service sign up user flow](/en-us/graph/api/authenticationeventsflow-update#example-2-update-the-page-layout-of-a-self-service-sign-up-user-flow).

Note that there is no built-in validation for custom regular expressions, apart from ensuring they don't match the format of an email address. Validation may fail at runtime if the provided value doesn't match the regex or if the regex itself is invalid.

Also, if you configure a custom regex for both the sign-up attribute validation (this step) and the sign-in identifier policy they must be compatible or authentication may fail. For example, a username that passes sign-up validation but doesn't match the sign-in identifier policy regex will cause authentication to fail at runtime.

## Prefill or assign usernames (preview)

Like other attributes, you can customize signup by pre-filling username or assigning it after gathering other user information. To prefill the value, use a custom extension with the [onAttributeCollectionStart](../../identity-platform/custom-extension-onattributecollectionstart-retrieve-return-data) event, and configure how it is presented via Page Layout or [via Microsoft Graph](how-to-define-custom-attributes#configure-attribute-visibility-and-editability-with-microsoft-graph). If you need to assign, modify, or validate the username after collecting more details, use the [onAttributeCollectionSubmit](../../identity-platform/custom-extension-onattributecollectionsubmit-retrieve-return-data) event.

Note

If the username field is hidden from the user and the username value is assigned programmatically, make sure that the username value is unique or sign-up will be blocked.

## Test signing in with the alias or username

You can test signing up and signing in with the email address and username you assigned to the user you created using the [Run user flow](how-to-test-user-flows) feature. If you sign in with email address, you'll see email address in `preferred_username` claim. If you sign in with username, you'll see the username in `preferred_username` claim.

Note

The `identities[]` property on a user object isn’t enforced by the Microsoft Entra sign-in identifiers policy. While administrators can assign values to a user’s `identities[]` property, authentication is determined by the configured sign-in identifier policy. In other words, if a sign-in type is specified for a user but isn't enabled in the policy, the authentication attempt fails at runtime. For example, a user might be assigned the username *User1234*, but if the username sign-in method isn't enabled in the policy, the user won't be able to sign in using that username.

## Customize the sign-in page (optional)

You can customize the sign-in page to provide a better experience for your users. You can customize the hint text of the identifier field on the sign-in page and localize other strings related to username.

### Customize the hint text of the identifier field on the sign-in page

You can customize the hint text of identifier field on the sign-in page for all apps via [Custom branding](/en-us/entra/external-id/customers/how-to-customize-branding-customers#to-customize-the-sign-in-form).

Tip

You can also customize the hint text for a specific application, or subset of applications, by using [Branding themes](../../fundamentals/how-to-customize-branding-themes-apps#apply-a-theme-to-applications).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Organizational Branding Administrator](../../identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant you created earlier from the **Directories + subscriptions** menu.
3. Browse to **Company branding** either by using the search bar or by navigating to **Entra ID** &gt; **Custom Branding**.
4. Select **Edit** to modify the branding.
5. In the **Sign-in form** tab, you can customize the hint text of identifier field on the sign-in page. For example, you can change it to *Email address or Member ID*.

    [![Screenshot of customizing the username hint text  in the Microsoft Entra admin center.](media/how-to-sign-in-alias/edit-username-hint.png)](media/how-to-sign-in-alias/edit-username-hint.png#lightbox)
6. Select **Review + save** to save your changes.

### Customize and localize other strings related to username

You can customize and localize other strings related to an end user's experience of signing in with a username by uploading a language file. For more information, see [Add language customization to a user flow](/en-us/entra/external-id/customers/how-to-customize-languages-customers#add-language-customization-to-a-user-flow).