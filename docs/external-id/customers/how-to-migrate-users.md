---
layout: Conceptual
title: Migrate users and credentials to Microsoft Entra External ID - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-migrate-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to migrate users and credentials from any legacy identity provider to Microsoft Entra External ID.
ms.topic: how-to
ms.date: 2026-03-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8f21a36c-3ae7-e662-d56c-b6e211966c98
document_version_independent_id: 8f21a36c-3ae7-e662-d56c-b6e211966c98
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-migrate-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-migrate-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-migrate-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: 3f505255-2e34-61d2-a154-e384bba829db
---

# Migrate users and credentials to Microsoft Entra External ID - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In this guide, you learn the fundamentals of how to migrate users and credentials from your current identity provider to Microsoft Entra External ID. This guide applies to any legacy identity provider (including Azure AD B2C) and covers directory preparation, bulk user migration, credential migration setup, and the available credential migration approaches.

Tip

If you're migrating from Azure AD B2C specifically, see [Plan your migration from Azure AD B2C to External ID](plan-your-migration-from-b2c-to-external-id) for B2C-specific decision guidance, password preservation options, and implementation steps.

## Prerequisites

Before you start migrating users to External ID, you need:

- An external tenant. To create one, choose from the following methods:
    - Use the [Microsoft Entra External ID extension](https://aka.ms/ciamvscode/samples/marketplace) to set up an external tenant directly in Visual Studio Code.
    - [Create a new external tenant](how-to-create-external-tenant-portal) in the Microsoft Entra admin center.

## Preparation: Directory cleanup

Before starting your user migration process, you should take the time to clean up data in your legacy identity provider directory. Doing this helps ensure that you only migrate the data you need and makes the migration process smoother.

- Identify the set of user attributes to be stored in External ID, and migrate only what you need. If necessary, you can [create custom attributes](concept-user-attributes) within External ID to store more data about a user.
- If you're migrating from an environment with multiple authentication sources (for example, each application has its own user directory), migrate to a unified account in External ID. You might need to apply your own business logic to merge and reconcile accounts for the same user from different sources.
- Usernames need to be unique per account in External. If multiple applications use different usernames, you need to apply your own business logic to reconcile and merge accounts. For the password, let the user choose one and set it in the directory. Only the chosen password should be stored in the External ID account.
- Remove unused user accounts, or don't migrate stale accounts.

## Stage 1: Migrate user data

The first step in the migration process is to migrate user data from your legacy identity provider to External ID. This includes usernames and any other relevant attributes. To do this, you need to:

1. Read the user accounts from your legacy identity provider.
2. Create the corresponding user accounts in your External ID directory. For information about programmatically creating user accounts, see [Manage Consumer user accounts with Microsoft Graph](/en-us/graph/api/user-post-users?view=graph-rest-1.0&amp;tabs=http#example-2-create-a-user-with-social-and-local-account-identities-in-azure-ad-b2c&amp;preserve-view=true).
3. If you have access to users' plaintext passwords, you can set them directly on the new accounts as you are migrating user data. If you don't have access to the plaintext passwords, you should set a random password for now that will be updated later as part of the password migration process.

Note

When migrating large numbers of objects, you might encounter throttling limits for Microsoft Graph. See [Throttling limits](/en-us/graph/throttling-limits) and [Throttling guidance](/en-us/graph/throttling) for best practices to handle or avoid throttling.

Not all information in your legacy identity provider needs to be migrated to your External ID directory. The following recommendations can help you determine the appropriate set of user attributes to store in External ID.

**DO** store in External ID:

- Username, password, email addresses, phone numbers, membership numbers/identifiers.
- Consent markers for privacy policy and end-user license agreements.

**DO NOT** store in External ID:

- Sensitive data like credit card numbers, social security numbers (SSN), medical records, or other data regulated by government or industry compliance bodies.
- Marketing or communication preferences, user behaviors, and insights.

## Alternatives to credential migration

Not every migration requires credential migration. If your users authenticate through social identity providers or enterprise federation, their passwords aren't stored in your directory and don't need to be migrated. You can also skip credential migration if you're moving to passwordless authentication or if you're comfortable having users reset their password via [self-service password reset (SSPR)](how-to-enable-password-reset-customers).

If you don't need credential migration, your user migration is complete. Return to the migrate guide to validate your environment and plan application cutover: [Stage 4: Validate, monitor, and plan cutover](migrate-from-b2c-to-external-id#stage-4-validate-monitor-and-plan-cutover).

## Stage 2: Prepare for credential migration

If you need to preserve existing passwords, prepare user accounts for credential migration before implementing either migration approach. This setup is shared by both the JIT and legacy IdP-initiated approaches described in Stage 3.

### Define an extension property for tracking migration status

Define a directory extension property to track whether each user's credentials have been migrated from the legacy identity provider. Microsoft Graph supports adding custom properties to directory objects through [directory (Microsoft Entra ID) extensions](/en-us/graph/extensibility-overview#directory-microsoft-entra-id-extensions).

# [Graph](#tab/graph)
Create an extension property using the Microsoft Graph API:

```http
POST https://graph.microsoft.com/v1.0/applications/00001111-aaaa-2222-bbbb-3333cccc4444/extensionProperties 

{ 
    "name": "toBeMigrated", 
    "dataType": "Boolean",
    "targetObjects":[ 
        "User" 
    ] 
} 
```

Replace `00001111-aaaa-2222-bbbb-3333cccc4444` with the object ID of your `b2c-extensions-app` application. The value of this extension should be set to `true` for all users who require migration.

# [Admin Center](#tab/admin-center)
To create an extension property using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Navigate to **Identity** &gt; **External Identities** &gt; **Custom user attributes**.
3. Select **Add**.
4. Enter the following values:
    - **Name**: Enter a name for the property (for example, `toBeMigrated`).
    - **Data Type**: Select **Boolean**.
    - **Description**: Enter a meaningful description (for example, "Tracks whether the user's password has been migrated from the legacy system").
5. Select **Create**.

---

#### Get the extension property ID

After creating the extension property, you need to retrieve its unique identifier to use in your credential migration implementation. The extension property ID follows this naming convention: `extension_{applicationId-without-hyphens}_{propertyName}`.

To construct your extension property ID:

1. Navigate to **Entra ID** &gt; **App registrations** in the [Microsoft Entra admin center](https://entra.microsoft.com/).
2. Select **All applications** from above the application list.
3. Find the application named `b2c-extensions-app` and copy its **Application (client) ID** value.
4. Remove the hyphens from the application ID and combine it with your attribute name.

For example, if your application ID is `00001111-aaaa-2222-bbbb-3333cccc4444` and your attribute name is `toBeMigrated`, your extension property ID would be `extension_00001111aaaa2222bbbb3333cccc4444_toBeMigrated`.

### Generate random strong passwords

Before creating users, generate unique, strong temporary passwords for each user account. These are replaced with the user's actual password from the legacy identity provider once credential migration completes.

Important

Ensure that the temporary passwords are unique and strong to maintain security during the migration process. Consider using a password generation library or service that meets your organization's security requirements.

### Create users with the migration flag

Create user accounts in your External ID tenant. You can create users through the [Microsoft Entra admin center](https://entra.microsoft.com/) or programmatically using the [Microsoft Graph API](/en-us/graph/api/user-post-users). For detailed instructions on user creation, see [How to create, invite, and delete users](/en-us/entra/fundamentals/how-to-create-delete-users).

The following example demonstrates how to create a user with the migration extension property set to `true` using the Microsoft Graph API. Replace `{extension-property-id}` with the actual extension property ID you constructed in the previous step.

```http
POST https://graph.microsoft.com/v1.0/users

{
    "creationType": "LocalAccount",
    "accountEnabled": true,
    "passwordProfile": {
        "forceChangePasswordNextSignIn": false,
        "password": "<unique-generated-random-strong-password>"
    },
    "{extension-property-id}": true
}
```

You can find sample code to support your user migration in the [B2C to MEEID migration tool](https://github.com/microsoft/b2c-to-meeid-migration-tool/).

## Stage 3: Migrate credentials

Once user accounts are prepared with the migration flag, choose a credential migration approach based on where applications authenticate during the migration.

### JIT password migration (External ID-initiated)

In JIT migration, applications have already moved to External ID endpoints. When a user signs in, External ID uses the `OnPasswordSubmit` custom authentication extension to validate the user's credentials against the legacy IdP, writes the password to the External ID account, and flags the account as migrated. Subsequent sign-ins authenticate directly against External ID.

For full implementation instructions, see [Just-in-time password migration](how-to-migrate-passwords-just-in-time).

### Legacy IdP-initiated credential harvesting

In this approach, applications remain on the legacy IdP endpoints while a custom policy or flow calls a REST API to validate each user's credentials and write them to the corresponding External ID account. Once enough credentials have been migrated, applications cut over to External ID.

This approach applies when plaintext passwords aren't accessible. For example, if:

- The password is stored by the legacy identity provider in a hashed or encrypted format.
- The password is managed by the legacy identity provider and can only be validated through its own authentication service.

The credential migration process consists of the following steps:

1. When a customer signs in, read the External ID user account corresponding to the email address entered.
2. If the account is already flagged as migrated, continue with normal sign-in.
3. If the account isn't flagged as migrated, validate the password against the legacy identity provider.
    1. If the legacy IdP determines the password is incorrect, return a friendly error to the user.
    2. If the legacy IdP determines the password is correct, write the password to the External ID account and update the migration flag.

Credential migration happens in two phases. First, legacy credentials are harvested and stored in External ID. Then, once credentials have been updated for a sufficient number of users, applications can be migrated to authenticate directly with External ID. Users who haven't been migrated need to reset their password when they sign in for the first time.

The high-level design for the credential migration process is shown in the following diagrams:

Harvest credentials from the legacy identity provider and update corresponding accounts in External ID.

![A diagram showing the high-level design for the first phase of credential migration.](media/how-to-migrate-users/pre-migration-stage1.png)

Stop harvesting credentials and migrate applications to authenticate with External ID. Decommission the legacy identity provider.

![A diagram showing the high-level design for the second phase of credential migration.](media/how-to-migrate-users/pre-migration-stage2.png)

Note

If you're using this approach, it's important to protect your REST API against brute-force attacks. An attacker can submit several passwords in the hope of eventually guessing a user's credentials. To help defeat such attacks, stop serving requests to your REST API when the number of sign-in attempts passes a certain threshold.

## Complete validation and cutover

After you complete user and credential migration, return to the migrate guide to validate end-to-end authentication flows and plan your application cutover: [Stage 4: Validate, monitor, and plan cutover](migrate-from-b2c-to-external-id#stage-4-validate-monitor-and-plan-cutover).