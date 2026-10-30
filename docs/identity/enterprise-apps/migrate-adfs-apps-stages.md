---
layout: Conceptual
title: Understand the stages of migrating application authentication from AD FS to Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-adfs-apps-stages
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Migrating application authentication from AD FS to Microsoft Entra ID in four stages. Plan your move, test configurations, and secure apps.
ms.topic: concept-article
ms.date: 2025-04-29T00:00:00.0000000Z
ms.reviewer: alamaral
ms.custom: not-enterprise-apps
locale: en-us
document_id: 8883103a-3647-e991-3688-fe849871e151
document_version_independent_id: d53a9aff-3992-afbc-eab1-e77286611c41
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migrate-adfs-apps-stages.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migrate-adfs-apps-stages
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migrate-adfs-apps-stages.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 65dca3f5-a668-f91f-c7e8-7a34e9dfcae6
---

# Understand the stages of migrating application authentication from AD FS to Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID offers a universal identity platform that provides your people, partners, and customers a single identity to access applications and collaborate from any platform and device. Microsoft Entra ID has a full suite of identity management capabilities. Standardizing your application authentication and authorization to Microsoft Entra ID provides these benefits.

## Types of apps to migrate

Your applications might use modern or legacy protocols for authentication. When you plan your migration to Microsoft Entra ID, consider migrating the apps that use modern authentication protocols (such as SAML and OpenID Connect) first.

These apps can be reconfigured to authenticate with Microsoft Entra ID either via a built-in connector from the Azure App Gallery. They can also be reconfigured by registering the custom application in Microsoft Entra ID.

Apps that use older protocols can be integrated using [Application Proxy](../app-proxy/overview-what-is-app-proxy) or any of our [Secure Hybrid Access (SHA) partners](secure-hybrid-access-integrations).

For more information, see:

- [Using Microsoft Entra application proxy to publish on-premises apps for remote users](../app-proxy/overview-what-is-app-proxy).
- [What is application management?](what-is-application-management)
- [AD FS application activity report to migrate applications to Microsoft Entra ID](migrate-adfs-application-activity).
- [Monitor AD FS using Microsoft Entra Connect Health](../hybrid/connect/how-to-connect-health-adfs).

## The migration process

During the process of moving your app authentication to Microsoft Entra ID, test your apps and configuration. We recommend that you continue to use existing test environments for migration testing before you move to the production environment. If a test environment isn't currently available, you can set one up using [Azure App Service](https://azure.microsoft.com/services/app-service/) or [Azure Virtual Machines](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn), depending on the architecture of the application.

You might choose to set up a separate test Microsoft Entra tenant on which to develop your app configurations.

Your migration process might look like this:

### Stage 1 – Current state: The production app authenticates with AD FS

![Diagram showing migration stage 1.](media/migrate-adfs-apps-stages/stage-1.png)

### Stage 2 – (Optional) Point a test instance of the app to the test Microsoft Entra tenant

Update the configuration to point your test instance of the app to a test Microsoft Entra tenant, and make any required changes. The app can be tested with users in the test Microsoft Entra tenant. During the development process, you can use tools such as [Fiddler](https://www.telerik.com/fiddler) to compare and verify requests and responses.

If it isn't feasible to set up a separate test tenant, skip this stage and point a test instance of the app to your production Microsoft Entra tenant as described in Stage 3 below.

![Diagram showing migration stage 2.](media/migrate-adfs-apps-stages/stage-2.png)

### Stage 3 – Point a test instance of the app to the production Microsoft Entra tenant

Update the configuration to point your test instance of the app to your production Microsoft Entra tenant. You can now test with users in your production tenant. If necessary, review the section of this article on transitioning users.

![Diagram showing migration stage 3.](media/migrate-adfs-apps-stages/stage-3.png)

### Stage 4 – Point the production app to the production Microsoft Entra tenant

Update the configuration of your production app to point to your production Microsoft Entra tenant.

![Diagram showing migration stage 4.](media/migrate-adfs-apps-stages/stage-4.png)

Apps that authenticate with AD FS can use Active Directory groups for permissions. Use [Microsoft Entra Connect Sync](../hybrid/connect/how-to-connect-sync-whatis) to sync identity data between your on-premises environment and Microsoft Entra ID before you begin migration. Verify those groups and membership before migration so that you can grant access to the same users when the application is migrated.

## Line of business apps

Your line-of-business apps are apps that your organization developed or apps that are a standard packaged product.

Line-of-business apps that use OAuth 2.0, OpenID Connect, or WS-Federation can be integrated with Microsoft Entra ID as [app registrations](../../identity-platform/quickstart-register-app). Integrate custom apps that use SAML 2.0 or WS-Federation as [non-gallery applications](add-application-portal) on the enterprise applications page in the [Microsoft Entra admin center](https://entra.microsoft.com/#home).