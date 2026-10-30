---
layout: Conceptual
title: Add Apple for customer sign-in - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-apple-federation-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add Apple as an identity provider for your external tenant.
ms.topic: how-to
ms.date: 2026-04-17T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: d7d6c330-d988-b4e3-0262-0d100436806c
document_version_independent_id: d7d6c330-d988-b4e3-0262-0d100436806c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-apple-federation-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-apple-federation-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-apple-federation-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: dfbfbe8e-43b5-a973-45c0-7646ba22d6a8
---

# Add Apple for customer sign-in - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

By setting up federation with Apple, you can let customers sign in to your applications by using their own Apple accounts. Learn more about [authentication methods and identity providers for customers](concept-authentication-methods-customers).

## Create an Apple application

To enable sign-in for customers with an Apple ID, you need to create an application in the [Apple Developer portal](https://developer.apple.com/). If you don't already have an Apple ID, you can create one in the **Certificates, IDs, & Profiles** section.

Note

This document was created using the state of the provider’s developer page at the time of creation, and changes may occur.

1. Sign in to the Apple Developer Portal with your account credentials.
2. From the menu, select **Certificates, IDs, & Profiles**, and then select **(+)**.
3. In the Register a New Identifier section, select **App IDs**, and then select **Continue**.
4. For Select a type, select **App**, and then select **Continue**.
5. To Register your App ID:

    1. Enter a Description.
    2. Enter the Bundle ID, such as `com.contoso.azure-ad`. Explicit naming such as `com.myappdomain.myappname` recommended.
    3. For Capabilities, select **Sign in with Apple** from the capabilities list.
    4. Take note of your Team ID (App ID Prefix) from this step. You'll need it later.
    5. Select **Continue** and then **Register**.
6. From the menu, select **Certificates, IDs, & Profiles**, and then select **(+)**.
7. In the **Register a new identifier** section, select **Services IDs**, and then select **Continue**.
8. In Register a Services ID:

    1. Enter a **Description**. The description is shown to the user on the consent screen.
    2. Enter the **Identifier**, such as `com.contoso.entra-service`. Explicit naming such as `com.myappdomain.myappname.service` is recommended. Take note of your Service ID identifier. The identifier is your Client ID.
    3. Select **Continue**, and then select **Register**.
9. From **Identifiers**, select the Service ID identifier you created.
10. Select **Sign In with Apple**, and then select **Configure**.

    1. Select the Primary App ID you want to configure Sign in with Apple with.
    2. In **Domains and Subdomains**, enter the following by replacing

    - `<tenant-id>` with your tenant ID or your primary domain name, and
    - `<tenant-name>`with your tenant name. All characters should be in lower-case. As an example:
        - `<tenant-name>.ciamlogin.com`
        - `<tenant-id>.ciamlogin.com`

    1. In **Return URLs**, enter the following by replacing `<tenant-id>`with your tenant ID or your primary domain name, and `<tenant-name>` with your tenant name. All characters should be in lower-case.

        As an example:

        - `https://<tenant-id>.ciamlogin.com/<tenant-id>/federation/oauth2`
        - `https://<tenant-id>.ciamlogin.com/<tenant-name>/federation/oauth2`
        - `https://<tenant-name>.ciamlogin.com/<tenant-id>/federation/oauth2`
    2. Select **Next**, and then select **Done**.
    3. When the pop-up window is closed, select **Continue**, and then select **Save**.

## Create an Apple client secret

1. From the Apple Developer portal menu, select **Keys**, and then select **(+)**.
2. To Register a New Key:
    1. Type a **Key Name**.
    2. Select **Sign in with Apple**, and then select **Configure**.
    3. For the Primary App ID, select the app you created previously, and then select **Save**.
3. Select **Continue**, and then select **Register** to finish the key registration process.
4. Take note of the **Key ID**. This key is required when you configure the identity provider.
5. To Download Your Key, select **Download** to download the `.p8` file that contains your key.
6. Select **Done**.

Important

Sign in with Apple requires the admin to renew their client secret every 6 months. You'll need to manually renew the Apple client secret if it expires and store the new value in the policy key. We recommend you set your own reminder within 6 months to generate a new client secret.

## Configure Apple federation in Microsoft Entra External ID

After you create the Apple app, in this step you set the Apple app details in Microsoft Entra External ID. You can use the Microsoft Entra admin center to do so. To configure Apple federation in the Microsoft Entra admin center, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **All identity providers**.
3. Under the Built-in tab, select **Apple**.

    ![Screenshot of the Apple identity provider configuration page in the Microsoft Entra admin center with fields for client ID, team ID, key ID, and client secret key.](media/how-to-apple-federation-customers/configure-apple-identity-provider.png)
4. The **Name***Apple* is autopopulated. It cannot be changed.
5. Enter the following details:

    - **Client (Apple service) ID**: The client ID of the Apple application you created in the previous step.
    - **Apple developer team ID**: The Apple developer team ID related to the Apple application you created in the previous step.
    - **Key ID**: The key ID of the Apple application you created in the previous step.
    - **Client secret (.p8) key**: The client secret key of the Apple application you created in the previous step.
6. Select **Save**. You see Apple listed as a configured identity provider.

    ![Screenshot of the All identity providers list showing Apple as a configured built-in identity provider.](media/how-to-apple-federation-customers/configured-apple-identity-provider.png)

## Enable users to sign in and sign up with the identity provider

After you configure Apple as an identity provider, add it to a user flow to allow sign-in and sign-up with the identity provider. See [Add an identity provider to a user flow](how-to-add-identity-provider-to-user-flow-customers).