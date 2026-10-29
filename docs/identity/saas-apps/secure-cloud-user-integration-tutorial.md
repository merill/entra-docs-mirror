---
layout: Conceptual
title: Configure Secure Cloud User Integration for single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/secure-cloud-user-integration-tutorial
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
description: Learn how to configure single sign-on (SSO) between Microsoft Entra ID and Secure Cloud User Integration using OpenID Connect (OIDC).
ms.topic: how-to
ms.date: 2026-10-23T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d6298b65-e97c-b464-f9f1-a6ea13010b52
document_version_independent_id: d6298b65-e97c-b464-f9f1-a6ea13010b52
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/secure-cloud-user-integration-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/secure-cloud-user-integration-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/secure-cloud-user-integration-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 979080a1-f855-ed1a-27de-91df08a17669
---

# Configure Secure Cloud User Integration for single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to configure single sign-on (SSO) between Microsoft Entra ID and Secure Cloud using OpenID Connect (OIDC). When you integrate Secure Cloud with Microsoft Entra ID, users can sign in with their Microsoft Entra accounts, and administrators can centrally manage access.

The **Secure Cloud User Integration** enterprise application is created in your Microsoft Entra tenant during the initial Microsoft Entra sign-in and consent process.

## Prerequisites

Before you begin, ensure that you have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant).
- A Microsoft Entra account with one of the following roles or ownership permissions:
    - [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
    - [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
    - [Application owner](../../fundamentals/users-default-permissions#owned-enterprise-applications).
- An account authorized to grant the required application consent in your tenant. The ability to manage an application doesn't by itself determine whether you can grant consent. For more information, see [Overview of user and admin consent](../enterprise-apps/user-admin-consent-overview).
- A [Secure Cloud](https://cp.appriver.com/) administrator account.
- A Secure Cloud user account whose email address matches the Microsoft Entra account that you use for the initial setup.

Important

Secure Cloud User Integration uses consent-based onboarding. The enterprise application doesn't exist in your tenant until an administrator completes the initial Microsoft Entra sign-in and grants consent. Follow the setup steps in order before looking for the application in Microsoft Entra ID.

## Scenario description

In this article, you enable Microsoft Entra authentication in Secure Cloud, sign in with Microsoft Entra credentials, grant consent, and verify SSO.

- Secure Cloud supports service provider (SP)-initiated and identity provider (IdP)-initiated SSO.
- Secure Cloud uses OpenID Connect (OIDC) for Microsoft Entra ID authentication.
- Secure Cloud also supports automatic user provisioning.

## Step 1: Enable Microsoft Entra authentication

Configure authentication in Secure Cloud before you initiate the first Microsoft Entra sign-in.

1. Sign in to [Secure Cloud](https://cp.appriver.com/) as an administrator.
2. Browse to **Service Administration** &gt; **Account Management** &gt; **User Integration** &gt; **Authentication**.

    ![Screenshot of the User Integration page with Authentication highlighted.](media/secure-cloud-user-integration-tutorial/navigate-authentication.png)
3. In the **Authentication Type** list, select **Microsoft Entra SSO**.

    ![Screenshot of the Authentication Type list with Microsoft Entra SSO highlighted.](media/secure-cloud-user-integration-tutorial/select-authentication-type.png)
4. Under **Configuration**, turn on **Enable Microsoft Entra Authentication**.

    ![Screenshot of the Configuration section with Enable Microsoft Entra Authentication turned on.](media/secure-cloud-user-integration-tutorial/enable-microsoft-entra-authentication.png)
5. Optionally, enable **Fallback User Password** during initial setup. This option provides an alternate sign-in method if Microsoft Entra authentication is unavailable.

    - If **Fallback User Password** is enabled, users can select **Sign in with Microsoft**, or sign in with their Secure Cloud credentials or LDAP credentials, if LDAP authentication is configured.
    - If **Fallback User Password** is disabled, users are redirected to Microsoft Entra ID after entering their username. Secure Cloud credentials and LDAP credentials aren't available as alternate sign-in methods.

    ![Screenshot of the Microsoft Entra SSO Settings section with Fallback User Password enabled.](media/secure-cloud-user-integration-tutorial/fallback-user-password.png)
6. Select **Save**.

## Step 2: Initiate Microsoft Entra sign-in

Start the sign-in flow from Secure Cloud.

1. Sign out of Secure Cloud, or use a different browser, and go to the [Secure Cloud sign-in page](https://account.appriver.com/).

    ![Screenshot of the Secure Cloud sign-in page.](media/secure-cloud-user-integration-tutorial/secure-cloud-sign-in.png)
2. Enter the username of a Secure Cloud account whose email address matches a Microsoft Entra account authorized to grant consent in your tenant, and then select **Continue**.

    ![Screenshot of the Secure Cloud sign-in page with Continue highlighted.](media/secure-cloud-user-integration-tutorial/secure-cloud-sign-in-continue.png)
3. Continue according to your **Fallback User Password** setting:

    - If it's disabled, you're redirected to Microsoft Entra ID automatically.
    - If it's enabled, select **Sign in with Microsoft** under **Use your organization's digital identity**.

    ![Screenshot of the Secure Cloud sign-in page with Sign in with Microsoft highlighted.](media/secure-cloud-user-integration-tutorial/secure-cloud-sign-in-with-microsoft.png)

## Step 3: Authenticate with Microsoft Entra ID

Secure Cloud redirects you to the Microsoft identity platform sign-in experience.

1. Enter your Microsoft Entra credentials.
2. Complete any required multifactor authentication prompts.
3. Continue to the consent screen.

If consent has already been granted, you might be signed in without another consent prompt. In that case, continue to Step 5.

## Step 4: Grant consent to the application

If consent hasn't already been granted, the **Permissions requested** page appears.

1. Review the requested permissions.

    ![Screenshot of the Permissions requested page.](media/secure-cloud-user-integration-tutorial/secure-cloud-user-integration-permissions-requested.png)
2. Optionally, select **Consent on behalf of your organization** if you're authorized to grant tenant-wide admin consent. This grants consent for users in the tenant so that they aren't prompted to grant the same consent individually.

    ![Screenshot of the Permissions requested page with Consent on behalf of your organization selected.](media/secure-cloud-user-integration-tutorial/secure-cloud-user-integration-permissions-requested-organization-consent.png)
3. Select **Accept**.

After consent is granted, Microsoft Entra ID creates the **Secure Cloud User Integration** enterprise application in your tenant.

Important

If organizational consent isn't granted, users might be prompted to consent individually during their first sign-in, depending on your tenant's consent policies.

For more information, see [Consent experience for applications in Microsoft Entra ID](../../identity-platform/application-consent-experience) and [Overview of user and admin consent](../enterprise-apps/user-admin-consent-overview).

## Step 5: Complete sign-in

After consent is granted, Microsoft Entra ID redirects you back to Secure Cloud. Secure Cloud validates the authentication response and signs you in with your Microsoft Entra account.

The enterprise application created during consent is used for subsequent SSO and provisioning configuration.

## Step 6: Verify enterprise application creation

Confirm that the initial sign-in and consent process created the application.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Search for **Secure Cloud User Integration** and confirm that the application appears in the list.

    ![Screenshot of the Enterprise applications list with Secure Cloud User Integration highlighted.](media/secure-cloud-user-integration-tutorial/secure-cloud-user-integration-listed.png)

## Test single sign-on

Verify that you can sign in to Secure Cloud with your Microsoft Entra account.

1. Sign out of Secure Cloud.
2. Return to [Secure Cloud](https://cp.appriver.com/).
3. Enter the username of the Secure Cloud account that matches your Microsoft Entra account, and then select **Continue**.
4. If **Fallback User Password** is enabled, select **Sign in with Microsoft** under **Use your organization's digital identity**. If it's disabled, you're redirected to Microsoft Entra ID automatically.
5. Authenticate with your Microsoft Entra account.

If authentication succeeds, you're redirected to the Secure Cloud portal and signed in without being prompted for a Secure Cloud password.

## Troubleshooting

Use the following checks if application creation, consent, or sign-in doesn't complete as expected.

### The enterprise application doesn't appear

The application is created only after an administrator completes the initial Microsoft Entra sign-in and consent process.

- Verify that the Microsoft Entra sign-in process completed successfully.
- Verify that you selected **Accept** on the consent page.
- Verify that your browser redirected you back to Secure Cloud.
- If needed, repeat the initial sign-in and consent process.

### Users can't grant consent

If users see a message that administrator approval is required:

- Check the tenant's consent settings.
- Contact a Microsoft Entra administrator authorized to grant the required consent.
- Have an authorized administrator review the requested permissions and grant consent on behalf of the organization.

For more information, see [Overview of user and admin consent](../enterprise-apps/user-admin-consent-overview).

### A user can't sign in

Verify the following settings:

- The user exists in Secure Cloud.
- The Secure Cloud user's email address matches the Microsoft Entra account.
- **Enable Microsoft Entra Authentication** is turned on in Secure Cloud.
- The sign-in path matches the configured **Fallback User Password** setting.