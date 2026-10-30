---
layout: Conceptual
title: Configure ICIMS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/icims-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra ID and ICIMS.
ms.topic: how-to
ms.date: 2024-08-29T00:00:00.0000000Z
locale: en-us
document_id: c3e4dadc-b84d-feda-330b-14e258014b20
document_version_independent_id: ac5b133b-99e9-7446-6127-f3b785ab0829
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/icims-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/icims-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/icims-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 64d91050-0d23-3ae9-7b0a-d29be1d04ccc
---

# Configure ICIMS for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate ICIMS with Microsoft Entra ID. When you integrate ICIMS with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to ICIMS.
- Enable your users to be automatically signed-in to ICIMS with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An iCIMS ATS subscription.
- Access to submit support tickets at community.icims.com

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- ICIMS supports **SP** initiated SSO.

## Add ICIMS from the gallery

To configure the integration of ICIMS into Microsoft Entra ID, you need to use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides) Configure and test Microsoft Entra SSO with ICIMS using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in ICIMS.

To configure and test Microsoft Entra SSO with ICIMS, perform the following steps:

1. **Configure Microsoft Entra Application Registration**- to enable your users to use this feature.
    1. **Add credentials to your Entra Application** - to establish a client secret for the SSO integration.
    2. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    3. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure ICIMS SSO**- to configure the single sign-on settings on application side.
    1. **Determine how you want to map your users between Entra and iCIMS** - to configure how to map user accounts between iCIMS and Entra.
    2. **Submit a support ticket for your SSO integration** - to provide iCIMS staff with the details needed to configure your SSO integration.
    3. **Create ICIMS test user** - to have a counterpart of B.Simon in ICIMS that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra Application Registration

Follow these steps to create a Microsoft Entra Application Registration for your iCIMS application.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. If you have access to multiple tenants, use the Settings icon in the top menu to switch to the tenant in which you want to register the application from the Directories + subscriptions menu.
3. Browse to **Entra ID** &gt; **App registrations** and select **New registration**.
4. Enter a display Name for your application. Users of your application might see the display name when they use the app, for example during sign-in. You can change the display name at any time and multiple app registrations can share the same name.
5. Specify who can use the application, sometimes called its sign-in audience as **Accounts in this organizational directory only**.
6. Specify a Redirect URI based on your ICIMS datacenter:

    a. US: `https://login.icims.com/login/callback`

    b. EU: `https://login.icims.ca/login/callback`

    c. CA: `https://login.icims.eu/login/callback`

Note

If you aren't sure about which redirect URI to use, navigate to your iCIMS ATS domain without being logged in. The domain is in the format `<customernickname>.icims.com`, for example notacustomer.icims.com. You be redirected to a login page whose domain will match one of the options datacenter domains listed on step 6.

1. Make note of your application/client\_id.

### Add credentials to your Entra Application

In this section, you add a client secret for your application.

1. In the Microsoft Entra admin center, in App registrations, select your application.
2. Select **Certificates & secrets** &gt; **Client secrets** &gt; **New client secret**.
3. Add a description for your client secret.
4. Select an expiration for the secret or specify a custom lifetime.

    Note

    Client secret lifetime is limited to two years (24 months) or less. You can't specify a custom lifetime longer than 24 months. Microsoft recommends that you set an expiration value of less than 12 months.

    Note

    You must contact iCIMS Technical Support at least 30 days in advance of expiration to provide a new secret and avoid a service interruption.
5. Record the Client secret and expiration date to provide to the iCIMS support team.

### Add permissions to your Entra Application

In this section, you add a permission to your application to sign in users and read the signed-in users' profiles.

1. In the Microsoft Entra admin center, in App registrations, select your application.
2. From the Overview page of your client application, select **API permissions** &gt; **Add a permission** &gt; **Microsoft Graph**.
3. Select Delegated permissions.
4. Under Select permissions, select the following permissions:

    a. Delegated Users &gt; User.Read

    Note

    iCIMS recommends that you grant Admin Consent to User.Read to avoid prompting users to trust the Microsoft Entra ID Application.

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign the Microsoft Entra test user

In this section, you enable B.Simon to use single sign-on by granting access to ICIMS.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **ICIMS**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. Assign the "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure ICIMS SSO

### Determine how you want to map your users between Entra and iCIMS

You must determine the Match From and Match To settings to map your organization’s Entra user accounts to your iCIMS ATS users as desired. The Match From setting indicates which Microsoft Entra ID attribute to match against an ATS user account. The Match To setting indicates the ATS user attribute to match against.

#### Match From setting options:

- **Subject / NameID**: An immutable identifier for the user, unique with respect to the Microsoft Entra ID application used to authenticate the user. If a single user signs into two different apps using two different client IDs, those apps will receive two different values for the subject claim.
- **OID**: The immutable identifier for an object in the Microsoft identity system, in this case, a user account. This ID uniquely identifies the user across applications. Two different applications signing in the same user will receive the same value in the oid claim. The Microsoft Graphs will return this ID as the ID property for a given user account.
- **Email**: The email of the user. Emails are mutable and only need to match during the first login, at which point the account is bound with an ATS user. This option isn't recommended for mutable email addresses.

Note

iCIMS recommends that you verify the Microsoft Entra ID user’s email address before accessing iCIMS ATS via Corporate SSO. This prevents linking an account with an invalid email address.

#### Match To setting options:

- **Login**: The ATS person record’s log in field, also known as the username.
- **Email**: The ATS person record’s email field.
- **ExternalID**: The ATS person record’s external ID field.

### Submit a support ticket for your SSO integration

In this section, you submit a support ticket to request iCIMS technical support to set up your SSO integration.

1. Ask your iCIMS user admin to visit https://community.icims.com/login.
2. Select Support &gt; Create a Case.
3. When submitting the ticket please provide the following details:
    - Provide the **application (client) id**.
    - Provide the **client secret**.
    - Provide the **Microsoft Microsoft Entra ID Domain**.
    - Provide the **IdP Domain(s)** - Typically, the domain of your organization’s corporate email addresses (e.g., corporate-domain.com is the domain of name@corporate-domain.com.). Your organization can leverage multiple IdP domains. The domain must be unique within the region (e.g, gmail.com is an invalid domain.)
    - Provide the **display name** for the integration. This is the name that displays for your organization’s employee users.
    - Provide your organization’s **logo URL** for the integration. It's displayed as a 20x20 pixel square.
    - Disclose whether you're enforcing Two-step Verification or **Multi-Factor Authentication**. Answer yes or no.
    - Provide the user **Match From** and **Match To** settings you selected in the previous step.

### Create ICIMS test user

In this section, you enable B.Simon to use single sign-on by creating a record in ICIMS for that user.

1. Browser to your ATS application at `<customernickname>.icims.com`.
2. Login as a user admin.
3. Select Create &gt; People &gt; Employee.
4. Provided details for this employee including name, email.
5. Once you've created the user based on your **MatchTo** setting fill out the appropriate field to match the data you expect to send via the **MatchFrom** setting. For example, if your MatchFrom is **OID** and your MatchTo is **External ID**, then visit the Login tab and edit the externalID to be Simon B.'s OID.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Once iCIMS support has setup the SSO integration they will provide a test url.
- The url is in the format, [https://iam-federated-testing-bff.production.env.icims.tools/login/hs-#####-azure](https://iam-federated-testing-bff.production.env.icims.tools/login/hs-#####-azure). The digits in the url are your unique icims ATS customer ID.