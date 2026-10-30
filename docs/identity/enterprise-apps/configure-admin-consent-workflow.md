---
layout: Conceptual
title: Configure the admin consent workflow - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-admin-consent-workflow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to configure a way for end users to request access to applications that require admin consent.
ms.topic: how-to
ms.date: 2024-12-29T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.collection: M365-identity-device-management
ms.custom: enterprise-apps, sfi-ga-blocked
locale: en-us
document_id: f6e93be2-bad4-bae7-91bc-d4122dad86fd
document_version_independent_id: caf48884-743b-8f83-58a0-a92c3940fbba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/configure-admin-consent-workflow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/configure-admin-consent-workflow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/configure-admin-consent-workflow.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 798b5a48-f962-cfd6-3f8a-baade79208d8
---

# Configure the admin consent workflow - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to configure the admin consent workflow to enable users to request access to applications that require admin consent. You enable the ability to make requests by using an admin consent workflow. For more information on consenting to applications, see [User and admin consent](user-admin-consent-overview).

The admin consent workflow gives admins a secure way to grant access to applications that require admin approval. When a user tries to access an application but is unable to provide consent, they can send a request for admin approval. The request is sent via email to admins who are designated as reviewers. A reviewer takes action on the request, and the user is notified of the action.

To approve requests, a reviewer must have the [permissions required](grant-admin-consent#prerequisites) to grant admin consent for the application requested. Simply designating them as a reviewer doesn't elevate their privileges.

## Prerequisites

To configure the admin consent workflow, you need:

- An Azure account. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- You must be a Global Administrator to turn on the admin consent workflow.

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

## Enable the admin consent workflow

To enable the admin consent workflow and choose reviewers:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Consent and permissions** &gt; **Admin consent settings**.
3. Under **Admin consent requests**, select **Yes** for **Users can request admin consent to apps they are unable to consent to** .

    ![Screenshot of configure admin consent workflow settings.](media/configure-admin-consent-workflow/enable-admin-consent-workflow.png)
4. Configure the following settings:

    - **Who can review admin consent requests** - Select users, groups, or roles that are designated as reviewers for admin consent requests. Reviewers can view, block, or deny admin consent requests, but only Global Administrators can approve admin consent requests for apps requesting for Microsoft Graph app roles (application permissions). People designated as reviewers can view incoming requests in the **My Pending** tab after they're set as reviewers. Any new reviewers aren't able to act on existing or expired admin consent requests.
    - **Selected users will receive email notifications for requests** - Enable or disable email notifications to the reviewers when a request is made. If this option is disabled, email notifications to the requesters when a request is made and reviewed are also disabled.
    - **Selected users will receive request expiration reminders** - Enable or disable reminder email notifications to the reviewers when a request is about to expire. The first about-to-expire reminder email is likely sent out in the middle of the configured "Consent request expires after (days)." For example, if you configure the consent request to expire in three days, the first reminder email is sent out on the second day, and the last expiration email is sent out almost immediately the consent request expires.
    - **Consent request expires after (days)** - Specify how long requests stay valid.
5. Select **Save**. It can take up to an hour for the workflow to become enabled.

Note

You can add or remove reviewers for this workflow by modifying the **Who can review admin consent requests** list. A current limitation of this feature is that a reviewer retains the ability to review requests that were made while they were designated as a reviewer and will receive expiration reminder emails for those requests after they're removed from the reviewers list. Additionally, new reviewers won't be assigned to requests that were created before they were set as a reviewer.

## Configure the admin consent workflow using Microsoft Graph

To configure the admin consent workflow programmatically, use the [Update adminConsentRequestPolicy](/en-us/graph/api/adminconsentrequestpolicy-update) API in Microsoft Graph.