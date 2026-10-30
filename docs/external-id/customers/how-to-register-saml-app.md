---
layout: Conceptual
title: Register a SAML app - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-register-saml-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to create and register a SAML app with External ID for customer identity and access management (CIAM). Choose your app type and get detailed steps.
ms.topic: how-to
ms.date: 2025-06-26T00:00:00.0000000Z
ms.custom: it-pro
locale: en-us
document_id: 82c8310d-7890-0fcf-00a3-1fd1ab3e7743
document_version_independent_id: 82c8310d-7890-0fcf-00a3-1fd1ab3e7743
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-register-saml-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-register-saml-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-register-saml-app.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1d1e0846-f516-a537-4492-f7ed618aaea9
---

# Register a SAML app - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

In external tenants, you can register applications that use the OpenID Connect (OIDC) or Security Assertion Markup Language (SAML) protocol for authentication and single sign-on. The [app registration](how-to-register-ciam-app) process is designed specifically for OIDC apps. But you can use the Enterprise applications feature to create and register your SAML app. This process generates a unique application ID (client ID) and adds your app to the App registrations, where you can view and manage its properties.

This article describes how to register your own SAML application in your external tenant by creating a *non-gallery* app in **Enterprise applications**.

## Prerequisites

- An Azure account that has an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra [external tenant](how-to-create-external-tenant-portal).
- [A sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers).

## Create and register a SAML app

1. Sign in to the Microsoft Entra admin center as at least an Application Administrator.
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu and switch to your external tenant from the **Directories** menu.
3. Go to **Identity** &gt; **Applications**&gt; **Enterprise applications**.
4. Select **New application**, and then select **Create your own application**.

    ![Screenshot of the Create your own application option in the Microsoft Entra Gallery.](media/how-to-register-saml-app/create-your-own-application.png)
5. On the **Create your own application** pane, enter a name for your app.
6. Select **Integrate any other application you don't find in the gallery (Non-gallery)**.
7. Select **Create**.
8. The app **Overview** page opens. In the left menu under **Manage**, select **Properties**. Switch the **Assignment required?** toggle to **No** so that users can use self-service sign-up, and then select **Save**.

    ![Screenshot of the Assignment required toggle.](media/how-to-register-saml-app/assignment-toggle-no.png)
9. In the left menu under **Manage**, select **Single sign-on**.
10. Under **Select a single sign-on method**, select **SAML**.

    ![Screenshot of the Single sign-on method tile.](media/how-to-register-saml-app/select-single-sign-on-method.png)
11. On the **SAML-based Sign-on** page, do one of the following:

    - Select **Upload metadata file**, browse to the file containing your metadata, and then select **Add**. Select **Save**.
    - Or, use the **Edit** pencil option to update each section, and then select **Save**.
12. At the third section under **SAML Certificates**, note that there's no **Download** button next to **Federation Metadata XML**. This button appears only in workforce tenants, not in external tenants. To download the metadata file in an external tenant, copy the link and paste it into your browser.

    ![Screenshot of the federation metadata xml link.](media/how-to-register-saml-app/federation-metadata-xml.png)
13. Select **Test**, and then select the **Test sign-in** button to see if single sign-on is working. This test verifies that your current admin account can sign in using the `https://login.microsoftonline.com` endpoint.

    ![Screenshot of the test single sign-on option.](media/how-to-register-saml-app/test-application.png)

    You can test external user sign-in with these steps:

    - [Create a sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers) if you haven't already.
    - [Add your SAML application to the user flow](how-to-user-flow-add-application).
    - Run your application.