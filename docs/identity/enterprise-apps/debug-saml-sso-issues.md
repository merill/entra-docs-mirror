---
layout: Conceptual
title: Debug SAML-based single sign-on to applications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/debug-saml-sso-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Debug SAML-based single sign-on to applications in Microsoft Entra ID.
ms.reviewer: alamaral
ms.topic: troubleshooting
ms.date: 2025-06-20T00:00:00.0000000Z
ms.custom: enterprise-apps, sfi-image-nochange
locale: en-us
document_id: ba6c47fe-8ee0-cf71-9582-9404f400aeb9
document_version_independent_id: 384c74ce-0bb4-9e96-3c7f-6d5a67243a2b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/debug-saml-sso-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/debug-saml-sso-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/debug-saml-sso-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2d07d985-3b14-c959-8e98-a23ee14775b4
---

# Debug SAML-based single sign-on to applications - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to find and fix [single sign-on](what-is-single-sign-on) issues for applications in Microsoft Entra ID that use SAML-based single sign-on.

## Before you begin

We recommend installing the [My Apps Secure Sign-in Extension](https://support.microsoft.com/account-billing/troubleshoot-problems-with-the-my-apps-portal-d228da80-fcb7-479c-b960-a1e2535cbdff#im-having-trouble-installing-the-my-apps-secure-sign-in-extension). This browser extension makes it easy to gather the SAML request and SAML response information that you need to resolve issues with single sign-on. In case you can't install the extension, this article shows you how to resolve issues both with and without the extension installed.

To download and install the My Apps Secure Sign-in Extension, use one of the following links.

- [Chrome](https://go.microsoft.com/fwlink/?linkid=866367)
- [Microsoft Edge](https://microsoftedge.microsoft.com/addons/detail/my-apps-secure-signin-ex/gaaceiggkkiffbfdpmfapegoiohkiipl)

## Test SAML-based single sign-on

To test SAML-based single sign-on between Microsoft Entra ID and a target application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. From the list of enterprise applications, select the application for which you want to test single sign-on, and then from the options on the left, select **Single sign-on**.
4. On the **Select a single sign-on method** pane, select **SAML**.
5. To open the SAML-based single sign-on testing experience, go to **Test single sign-on** (step 5). If the **Test** button is greyed out, you need to fill out and save the required attributes first in the **Basic SAML Configuration** section.
6. In the **Test single sign-on** page, use your corporate credentials to sign in to the target application. You can sign in as the current user or as a different user. If you sign in as a different user, a prompt asks you to authenticate.

    ![Screenshot showing the test SAML SSO page](media/debug-saml-sso-issues/test-single-sign-on.png)

If you're able to sign in, the test is successful. In this case, Microsoft Entra ID issued a SAML response token to the application. The application used the SAML token to successfully sign you in.

If you have an error on the company sign-in page or the application's page, use one of the next sections to resolve the error.

## Resolve a sign-in error on your company sign-in page

When you try to sign in, you might see an error on your company sign-in page that's similar to the following example.

![Example showing an error in the company sign-in page](media/debug-saml-sso-issues/error.png)

To debug this error, you need the error message and the SAML request. The My Apps Secure Sign-in Extension automatically gathers this information and displays resolution guidance on Microsoft Entra ID.

### To resolve the sign-in error with the My Apps Secure Sign-in Extension installed

1. When an error occurs, the extension redirects you back to the Microsoft Entra ID **Test single sign-on** page.
2. On the **Test single sign-on** page, select **Download the SAML request**.
3. You should see specific resolution guidance based on the error and the values in the SAML request.
4. You see a **Fix it** button to automatically update the configuration in Microsoft Entra ID to resolve the issue. If you don't see this button, then the sign-in issue isn't due to a misconfiguration on Microsoft Entra ID.

If no resolution is provided for the sign-in error, we suggest that you use the feedback textbox to inform us.

### To resolve the error without installing the My Apps Secure Sign-in Extension

1. Copy the error message at the bottom right corner of the page. The error message includes:
    - A CorrelationID and Timestamp. These values are important when you create a support case with Microsoft because they help the engineers to identify your problem and provide an accurate resolution to your issue.
    - A statement identifying the root cause of the problem.
2. Go back to Microsoft Entra ID and find the **Test single sign-on** page.
3. In the text box above **Get resolution guidance**, paste the error message.
4. Select **Get resolution guidance** to display steps for resolving the issue. The guidance might require information from the SAML request or SAML response. If you're not using the My Apps Secure Sign-in Extension, you might need a tool such as [Fiddler](https://www.telerik.com/fiddler) to retrieve the SAML request and response.
5. Verify that the destination in the SAML request corresponds to the SAML Single Sign-on Service URL obtained from Microsoft Entra ID.
6. Verify the issuer in the SAML request is the same identifier configured for the application in Microsoft Entra ID. Microsoft Entra ID uses the issuer to find an application in your directory.
7. Verify AssertionConsumerServiceURL is where the application expects to receive the SAML token from Microsoft Entra ID. You can configure this value in Microsoft Entra ID, but it's not mandatory if it's part of the SAML request.

## Resolve a sign-in error on the application page

You might sign in successfully and then see an error on the application's page. This error occurs when Microsoft Entra ID issued a token to the application, but the application doesn't accept the response.

To resolve the error, follow these steps, or watch this [short video about how to use Microsoft Entra ID to troubleshoot SAML SSO](https://www.youtube.com/watch?v=poQCJK0WPUk&amp;list=PLLasX02E8BPBm1xNMRdvP6GtA6otQUqp0&amp;index=8):

1. If the application is in the Microsoft Entra Gallery, verify that you followed all the steps for integrating the application with Microsoft Entra ID. To find the integration instructions for your application, see the [list of SaaS application integration tutorials](../saas-apps/tutorial-list).
2. Retrieve the SAML response.

    - If the My Apps Secure Sign-in extension is installed, from the **Test single sign-on** page, select **download the SAML response**.
    - If the extension isn't installed, use a tool such as [Fiddler](https://www.telerik.com/fiddler) to retrieve the SAML response.
3. Notice these elements in the SAML response token:

    - User unique identifier of NameID value and format
    - Claims issued in the token
    - Certificate used to sign the token.

        For more information on the SAML response, see [Single Sign-on SAML protocol](../../identity-platform/single-sign-on-saml-protocol).
4. Now that you're done reviewing the SAML response, see [Error on an application's page after signing in](application-sign-in-problem-application-error) for guidance on how to resolve the problem.
5. If you're still not able to sign in successfully, you can ask the application vendor what is missing from the SAML response.