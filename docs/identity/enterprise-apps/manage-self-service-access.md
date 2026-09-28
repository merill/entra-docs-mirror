---
layout: Conceptual
title: Enable self-service application assignment - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-self-service-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Enable self-service application access to allow users to find their own applications from their My Apps portal
ms.topic: how-to
ms.date: 2025-04-28T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.reviewer: ergreenl
ms.custom: enterprise-apps
locale: en-us
document_id: 580e9e5d-4685-f5d0-b272-97035861d97e
document_version_independent_id: 23e3c30a-e4e7-4387-2709-5979a415842d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/manage-self-service-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/manage-self-service-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/manage-self-service-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 836fa5eb-cb0b-682e-6597-07b27f57fe56
---

# Enable self-service application assignment - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to enable self-service application access using the Microsoft Entra admin center.

Before your users can self-discover applications from the [My Apps portal](myapps-overview), you need to enable **Self-service application access** for the applications. This functionality is available for applications that were added from the Microsoft Entra Gallery. It's also available for [Microsoft Entra application proxy](/en-us/entra/identity/app-proxy), or applications added using [user or admin consent](../../identity-platform/application-consent-experience).

Using this feature, you can:

- Let users self-discover applications from the My Apps portal without bothering the IT group.
- Add those users to a preconfigured group so you can see who requests access, remove access, and manage the roles assigned to them.
- Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.
- Optionally configure up to 10 individuals who might approve access to this application.
- Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s My Apps portal
- Optionally automate the assignment of self-service assigned users to an application role directly.

## Prerequisites

To enable self-service application access, you need:

- A Microsoft Entra user account. If you don't already have one, [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles: Cloud Application Administrator, or Application Administrator.
- A Microsoft Entra ID P1 or P2 license is required for users to request to join a self-service app and for owners to approve or deny requests. Without a Microsoft Entra ID P1 or P2 license, users can't add self-service apps.

## Enable self-service application access to allow users to find their own applications

Self-service application access is a great way to allow users to self-discover applications, and optionally allow the business group to approve access to those applications. For password single-sign on applications, you can also allow the business group to manage the credentials assigned to those users from their own My Apps portal.

To enable self-service application access to an application, undertake the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application from the search results.
4. In the left navigation menu, select **Self-service**.
5. To enable Self-service application access for this application, set **Allow users to request access to this application?** to **Yes.**
6. Next to **To which group should assigned users be added?**, select **Select group**. Choose a group, and then select **Select**. When a user's request is approved, they're added to this group. When viewing this group's membership, you're able to see who has access to the application through self-service access.

    Note

    This setting doesn't support groups synchronized from on-premises.
7. **Optional:** To require business approval before users are allowed access, set **Require approval before granting access to this application?** to **Yes**.
8. **Optional:** Next to **Who is allowed to approve access to this application?**, select **Select approvers** to specify the business approvers who are allowed to approve access to this application. Select up to ten individual business approvers, and then select **Select**.

    Note

    Groups aren't supported. You can select up to ten individual business approvers. If you specify multiple approvers, any single approver can approve an access request.
9. **Optional:** Next to **To which role should users be assigned in this application?**, select **Select Role** to assign self-service approved users to a role. Choose the role to which these users should be assigned, and then select **Select**. This option is for applications that expose roles.
10. Select the **Save** button at the top of the pane to finish.

Once you complete self-service application configuration, users can navigate to their My Apps portal, and select **Request new apps** to find the apps that are enabled with self-service access. Business approvers also see a notification in their My Apps portal. You can enable an email notifying them when a user requests access to an application that requires their approval.