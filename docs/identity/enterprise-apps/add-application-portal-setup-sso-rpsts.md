---
layout: Conceptual
title: Enable single sign-on for an enterprise application with a relying party security token service - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/add-application-portal-setup-sso-rpsts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Enable single sign-on for an enterprise application that has a relying party security token service in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-02-01T00:00:00.0000000Z
ms.reviewer: ergreenl, mwahl
ms.custom: mode-other, enterprise-apps
locale: en-us
document_id: be89b0a9-7ecb-02b8-cd1d-8ed8600115a5
document_version_independent_id: be89b0a9-7ecb-02b8-cd1d-8ed8600115a5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/add-application-portal-setup-sso-rpsts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/add-application-portal-setup-sso-rpsts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/add-application-portal-setup-sso-rpsts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 95a2e6d7-221f-51f6-2f21-42e257e35f36
---

# Enable single sign-on for an enterprise application with a relying party security token service - Microsoft Entra ID | Microsoft Learn

In this article, you use the Microsoft Entra admin center to enable single sign-on (SSO) for an enterprise application which is dependent upon a relying party security token service (STS). The relying party STS supports the Security Assertion Markup Language (SAML), and can be integrated with Microsoft Entra as an enterprise application. After you configure SSO, your users can sign in to the application by using their Microsoft Entra credentials.

![Diagram showing the trust relationship between an application, a relying party STS, and Microsoft Entra ID as an identity provider.](media/add-application-portal-setup-sso-rpsts/saml-topology.png)

If your application will integrate directly with Microsoft Entra for single sign-on, and does not require a relying party Security Token Service (STS), then see the article [Enable single sign-on for an enterprise application](add-application-portal-setup-sso).

We recommend that you use a nonproduction environment to test the steps in this article, before configuring an application in a production tenant.

## Prerequisites

To configure SSO, you need:

- A relying party STS, such as Active Directory Federation Services (AD FS) or PingFederate, with HTTPS endpoints
    1. You'll need the entity identifier (entity ID) of the relying party STS. This must be unique across all relying party STS and applications configured in a Microsoft Entra tenant. There cannot be two applications in a single Microsoft Entra tenant with the same entity identifier. For example, if Active Directory Federation Services (AD FS) is the relying party STS, then the identifier may be a URL of the form `http://{hostname.domain}/adfs/services/trust`.
    2. You'll also need the assertion consumer service URL, or reply URL, of the relying party STS. This URL must be a `HTTPS` URL to securely transfer SAML tokens from Microsoft Entra to the relying party STS as part of single sign-on to an application. For example, if AD FS is the relying party STS, then the URL may be of the form `https://{hostname.domain}/adfs/ls/`.
- An application, which has already been integrated with that relying party STS
- One of the following roles in Microsoft Entra: Cloud Application Administrator, Application Administrator
- A test user in Microsoft Entra who can sign into the application

Note

This tutorial assumes that there is one Microsoft Entra tenant, one relying party STS, and one application connected to the relying party STS. This tutorial shows how to configure Microsoft Entra to use the entity identifier provided by the relying party STS to determine the appropriate enterprise application, to send a SAML token in a response. If you had more than one application connected to a single relying party STS, then Microsoft Entra wouldn't be able to distinguish between those two applications when issuing SAML tokens. Configuring different entity identifiers is outside the scope of this tutorial.

## Create an application in Microsoft Entra

First, create an enterprise application in Microsoft Entra, which enables Microsoft Entra to generate SAML tokens for the relying party STS to provide to the application.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. If you have already configured an application representing the relying party STS, then enter the name of the existing application in the search box, select the application from the search results, and continue at the next section.
4. Select **New application**.
5. Select **Create your own application**.
6. Type the name of the new application in the input name box, select **Integrate any other application you don't find in the gallery (Non-gallery)**, and select **Create**.

## Configure single sign-on in the application

1. In the **Manage** section of the left menu, select **Single sign-on** to open the **Single sign-on** pane for editing.
2. Select **SAML** to open the SSO configuration page.
3. In the **Basic SAML configuration** box, select **Edit**. The identifier and reply URL must be set before further SAML configuration changes can be made. ![Screenshot showing the required basic SAML configuration for single sign-on for an enterprise application.](media/add-application-portal-setup-sso-rpsts/basic-saml-configuration.png)
4. In the Basic SAML configuration page, under **Identifier (Entity ID)**, if there's no identifier listed, select **Add identifier**. Type the identifier for the application as provided by the relying party STS. For example, the identifier may be a URL of the form `http://{hostname.domain}/adfs/services/trust`.
5. In the Basic SAML configuration page, under **Reply URL (Assertion Consumer Service URL)**, select **Add reply URL**. Type the HTTPS URL of the relying party STS Assertion Consumer Service. For example, the URL may be of the form `https://{hostname.domain}/adfs/ls/`.
6. Optionally, configure the **sign on**, **relay state**, or **logout** URLs, if required by the relying party STS.
7. Select **Save**.

## Download metadata and certificates from Microsoft Entra

Your relying party STS may require the federation metadata from Microsoft Entra as the identity provider in order to complete the configuration. The federation metadata and associated certificates are provided in the **SAML Certificates** section of the **Basic SAML configuration** page. For more information, see [federation metadata](../../identity-platform/federation-metadata).

![Screenshot showing the SAML signing certificates and federation metadata download options for an enterprise application.](media/add-application-portal-setup-sso-rpsts/saml-certificates.png)

- If your relying party STS can download federation metadata from an Internet endpoint, then copy the value next to the **App Federation Metadata Url**.
- If your relying party STS requires a local XML file containing the federation metadata, then select **Download** next to **Federation Metadata XML**.
- If your relying party STS requires the certificate of the identity provider, then select **Download** next to either the **Certificate (Base64)** or **Certificate (Raw)**.
- If your relying party STS does not support federation metadata, then copy the **Login URL** and **MIcrosoft Entra Identifier** to configure your relying party STS. ![Screenshot showing the Microsoft Entra Login URL and identifier for an enterprise application.](media/add-application-portal-setup-sso-rpsts/saml-identifiers.png)

## Configure claims issued by Microsoft Entra

By default, only a few attributes from Microsoft Entra users are included in the SAML token Microsoft Entra sends to the relying party STS. You can add additional claims which your applications require, and change the attribute provided in the SAML name identifier. For more information on standard claims, see [SAML token claims reference](../../identity-platform/reference-saml-tokens).

1. In the **Attributes & Claims** box, select **Edit**.
2. To change which Entra ID attribute is sent as the value of the Name identifier, select the row **Unique User Identifier (Name ID)**. You can change the source attribute to another Microsoft Entra built-in or extension attribute. Then select **Save**.
3. To change which Entra ID attribute is sent as the value of a claim already configured, select the row in the **Additional claims** section.
4. To add a new claim, select **Add new claim**.
5. When complete, select **SAML-based Sign-on** to close this screen.

## Configure who can sign-in to the application

When testing the configuration, you should assign a designated test user to the application in Microsoft Entra, to validate that the user is able to sign on to the application via Microsoft Entra and the relying party STS.

1. In the **Manage** section of the left menu, select **Properties**.
2. Ensure that the value of **Enabled for users to sign-in** is set to **Yes**.
3. Ensure that the value of **Assignment required** is set to **Yes**.
4. If you made any changes, select **Save**.
5. In the **Manage** section of the left menu, select **Users and groups**.
6. Select **Add user/group**.
7. Select **None selected**.
8. In the search box, type the name of the test user, then pick the user and select **Select**.
9. Select **Assign** to assign the user to the default **User** role of the application.
10. In the **Security** section of the left menu, select **Conditional Access**.
11. Select **What if**.
12. Select **No user or service principal selected**, select **No user selected**, and select the user previously assigned to the application.
13. Select **Any cloud app**, and select the enterprise application.
14. Select **What if**. Validate that any policies that will apply allow the user to sign into the application.

## Configure Microsoft Entra as an identity provider in your relying party STS

Next, import the federation metadata into your relying party STS. The following steps are shown using AD FS, but another relying party STS could be used instead.

1. In the claims provider trust list of your relying party STS, select **Add Claims Provider Trust**, and select **Start**.
2. Depending on whether you downloaded the federation metadata from Microsoft Entra, select **Import data about the the claims provider published online or on a local network**, or **Import data about the claims provider from a file**.
3. You may need to also provide the certificate of Microsoft Entra to the relying party STS.
4. When your configuration of Microsoft Entra as an identity provider is complete, confirm that:
    - The claims provider identifier is a URI of the form `https://sts.windows.net/{tenantid}`.
    - If using the Microsoft Entra ID global service, the endpoints for SAML single sign-on are URI of the form `https://login.microsoftonline.com/{tenantid}/saml2`. For national clouds, see [Microsoft Entra authentication & national clouds](../../identity-platform/authentication-national-cloud).
    - A certificate of Microsoft Entra is recognized by the relying party STS.
    - No encryption is configured.
    - The claims configured in Microsoft Entra are listed as available for claims rule mappings in your relying party STS. If you subsequently added additional claims, you may need to also add them to the configuration of the identity provider in your relying party STS.

## Configure claims rules in your relying party STS

Once the claims that Microsoft Entra will send as the identity provider are known to the relying party STS, you'll need to map or transform those claims into the claims required by your application. The following steps are shown using AD FS, but another relying party STS could be used instead.

1. In the claims provider trust list of your relying party STS, select the claims provider trust for Microsoft Entra, and select **Edit Claims Rules**.
2. For each claim provided by Microsoft Entra and required by your application, select **Add Rule**. In each rule, select [**Pass through or Filter an Incoming Claim**](/en-us/windows-server/identity/ad-fs/operations/create-a-rule-to-pass-through-or-filter-an-incoming-claim), or [**Transform an Incoming Claim**](/en-us/windows-server/identity/ad-fs/operations/create-a-rule-to-transform-an-incoming-claim), based on the requirements of your application.

## Test the single sign-on to your application

After the application is configured in Microsoft Entra and your relying party STS, users can sign into it by authenticating to Microsoft Entra, and having a token provided by Microsoft Entra transformed by your relying party STS into the form and claims required by your application.

This tutorial illustrates testing the sign-in flow using a web-based application which implements the relying party initiated single sign-on pattern. For more information, see [Single sign-on SAML protocol](../../identity-platform/single-sign-on-saml-protocol).

![Diagram showing the web browser redirects between an application, a relying party STS, and Microsoft Entra ID as an identity provider.](media/add-application-portal-setup-sso-rpsts/saml-redirects.png)

1. In a web browser private browsing session, connect to the application and initiate the login process. The application redirects the web browser to the relying party STS, and the relying party STS determines the identity providers which can provide appropriate claims.
2. In the relying party STS, if prompted, select the Microsoft Entra identity provider. The relying party STS redirects the web browser to the Microsoft Entra login endpoint, `https://login.microsoftonline.com` if using the Microsoft Entra ID global service.
3. Sign in to Microsoft Entra using the identity of the test user, previously configured in the step configure who can sign-in to the application. Microsoft Entra then locates the enterprise application based on the entity identifier, and redirect the web browser to the relying party STS reply URL endpoint, with the web browser transporting the SAML token.
4. The relying party STS validates the SAML token was issued by Microsoft Entra, then extract and transform the claims from the SAML token, and redirect the web browser to the application. Confirm that your application has received the required claims from Microsoft Entra via this process.

## Complete configuration

1. After testing the initial sign-on configuration, you'll need to ensure that your relying party STS stays up to date as new certificates are added to Microsoft Entra. Some relying party STS may have a built-in process to monitor the federation metadata of the identity provider.
2. This tutorial illustrated configuring single sign-in. Your relying party STS may also support SAML single sign-out. For more information on this capability, see [Single Sign-Out SAML Protocol](../../identity-platform/single-sign-out-saml-protocol).
3. You can remove the assignment of the test user to the application. You can use other features such as dynamic groups or entitlement management to assign users to the application. For more information, see [Quickstart: Create and assign a user account](add-application-portal-assign-users).