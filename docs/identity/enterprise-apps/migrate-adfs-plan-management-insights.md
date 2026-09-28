---
layout: Conceptual
title: 'Phase 4: Plan management and insights - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-adfs-plan-management-insights
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: This article describes phase 4 of planning migration of applications from AD FS to Microsoft Entra ID
ms.topic: concept-article
ms.date: 2023-05-30T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
locale: en-us
document_id: ed13d781-503b-50a2-d8b6-d8178b266db3
document_version_independent_id: fea95bd1-feb8-4f72-7844-4ae8c235fe76
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migrate-adfs-plan-management-insights.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migrate-adfs-plan-management-insights
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migrate-adfs-plan-management-insights.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 5962d4d5-a718-dfdb-851b-47c03f10ac41
---

# Phase 4: Plan management and insights - Microsoft Entra ID | Microsoft Learn

Once apps are migrated, you must ensure that:

- Users can securely access and manage
- You can gain the appropriate insights into usage and app health

We recommend taking the following actions as appropriate to your organization.

## Manage your users’ app access

Once you've migrated the apps, consider applying the following suggestions to enrich your user’s experience:

- Make apps discoverable by publishing them to the [Microsoft MyApplications portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510#download-and-install-the-my-apps-secure-sign-in-extension).
- Add [app collections](access-panel-collections) so users can locate application based on business function.
- Add their own application bookmarks to the [MyApplications portal](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510#download-and-install-the-my-apps-secure-sign-in-extension).
- Enable [self-service application access](manage-self-service-access) to an app and **let users add apps that you curate**.
- Optionally [hide applications from end-users](hide-application-from-user-portal).
- Users can go to [Office.com](https://www.office.com) to **search for their apps and have their most-recently-used apps appear** for them right from where they do work.
- Users can download the MyApps secure sign-in extension in Chrome, or Microsoft Edge so they can launch applications directly from their browser without having to first navigate to MyApplications.
- Users can access the MyApps portal with Intune-managed browser on their [iOS 7.0](hide-application-from-user-portal) or later or [Android](hide-application-from-user-portal) devices.

    - For **Android devices**, from the [Google play store](https://play.google.com/store/apps/details?id=com.microsoft.intune)
    - For **Apple devices**, from the [Apple App Store](https://apps.apple.com/us/app/intune-company-portal/id719171358).

## Secure app access

Microsoft Entra ID provides a centralized access location to manage your migrated apps. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) and enable the following capabilities:

- **Secure user access to apps.** Enable [Conditional Access policies](../conditional-access/overview) to secure user access to applications based on device state, location, and more.
- **Automatic provisioning.** Set up [automatic provisioning of users](../app-provisioning/user-provisioning) with various third-party SaaS apps that users need to access. In addition to creating user identities, it includes the maintenance and removal of user identities as status or roles change.
- **Delegate user access** **management**. As appropriate, enable self-service application access to your apps and *assign a business approver to approve access to those apps*. Use [Self-Service Group Management](../users/groups-self-service-management)for groups assigned to collections of apps.
- **Delegate admin access** using **Directory Role** to assign an admin role (such as Application Administrator, Cloud Application Administrator, or Application Developer) to your user.
- **Add applications to Access Packages** to provide governance and attestation.

## Audit and gain insights of your apps

You can also use the [Microsoft Entra admin center](https://entra.microsoft.com) to audit all your apps from a centralized location,

- **Audit your app** using **Enterprise Applications, Audit**, or access the same information from the [Microsoft Entra reporting API](../monitoring-health/howto-configure-prerequisites-for-reporting-api) to integrate into your favorite tools.
- **View the permissions for an app** using **Enterprise Applications, Permissions** for apps using OAuth/OpenID Connect.
- **Get sign-in insights** using **Enterprise Applications, Sign-Ins**. Access the same information from the [Microsoft Entra reporting API.](../monitoring-health/howto-configure-prerequisites-for-reporting-api)
- **Visualize your app’s usage** from the [Microsoft Entra ID Power BI content pack](../monitoring-health/howto-use-workbooks)

## Exit criteria

You're successful in this phase when you:

- Provide secure app access to your users
- Manage to audit and gain insights of the migrated apps

## Do even more with deployment plans

Deployment plans walk you through the business value, planning, implementation steps, and management of Microsoft Entra solutions, including app migration scenarios. They bring together everything that you need to start deploying and getting value out of Microsoft Entra capabilities. The deployment guides include content such as Microsoft recommended best practices, end-user communications, planning guides, implementation steps, test cases, and more.

Many [deployment plans](../../architecture/deployment-plans) are available for your use, and we’re always making more!

## Contact support

Visit the following support links to create or track support ticket and monitor health.

- **Azure Support:** You can call [Microsoft Support](https://azure.microsoft.com/support) and open a ticket for any Azure Identity deployment issue depending on your Enterprise Agreement with Microsoft.
- **FastTrack**: If you've purchased Enterprise Mobility and Security (EMS) or Microsoft Entra ID P1 or P2 licenses, you're eligible to receive deployment assistance from the [FastTrack program.](/en-us/microsoft-365/fasttrack/introduction)
- **Engage the Product Engineering team:** If you're working on a major customer deployment with millions of users, you're entitled to support from the Microsoft account team or your Cloud Solutions Architect. Based on the project’s deployment complexity, you can work directly with the [Azure Identity Product Engineering team.](https://portal.azure.com/#blade/Microsoft_Azure_Marketplace/MarketplaceOffersBlade/selectedMenuItemId/solutionProviders)