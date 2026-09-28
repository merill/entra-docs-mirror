---
layout: Conceptual
title: SaaS App configuration guides for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/tutorial-list
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: celested
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Configure Microsoft Entra single sign-on integration with a variety of third-party software as a service application.
ms.topic: landing-page
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 20d4589b-e1a8-b9d0-76e6-4d3619100353
document_version_independent_id: b929de0a-4f82-8799-aadc-f7075e443310
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/tutorial-list.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/tutorial-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/tutorial-list.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
platformId: e505756e-4e3a-6795-9d99-dca4c561de0a
---

# SaaS App configuration guides for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

To help integrate your cloud-enabled [software as a service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) and on-premises applications with Microsoft Entra ID, we have developed a collection of articles that walk you through configuration.

For a list of all SaaS apps that have been preintegrated into Microsoft Entra ID, see the [Microsoft Entra Marketplace](https://marketplace.microsoft.com/marketplace/apps?product=entra-id-apps). For a list of applications that can be integrated with Microsoft Entra ID Governance, see [Microsoft Entra ID Governance integrations](../../id-governance/apps).

Microsoft Entra can be integrated with many other applications, using standards such as OpenID Connect, SAML, SCIM, SQL, and LDAP. If you're using an application that isn't listed, and it's a SaaS, then use the [application network portal](../enterprise-apps/v2-howto-app-gallery-listing) to request a [SCIM](../app-provisioning/use-scim-to-provision-users-and-groups) enabled application to be added to the gallery for automatic provisioning or a SAML / OIDC enabled application to be added to the gallery for SSO. For integration with other applications, see [integrating applications with Microsoft Entra ID](../../id-governance/identity-governance-applications-integrate).

## Quick links

Some of the popular integrations include the applications in the following table.

| Logo | Application article for single sign-on | Application article for user provisioning |
| --- | --- | --- |
| ![logo-Atlassian Cloud](media/tutorial-list/entra-saas-atlassian-cloud-tutorial.png) | [Atlassian Cloud](atlassian-cloud-tutorial) | [Atlassian Cloud - User Provisioning](atlassian-cloud-provisioning-tutorial) |
| ![logo-ServiceNow](media/tutorial-list/entra-saas-servicenow-tutorial.png) | [ServiceNow](servicenow-tutorial) | [ServiceNow - User Provisioning](servicenow-provisioning-tutorial) |
| ![logo-Slack](media/tutorial-list/entra-saas-slack-tutorial.png) | [Slack](slack-tutorial) | [Slack - User Provisioning](slack-provisioning-tutorial) |
| ![logo-SuccessFactors](media/tutorial-list/entra-saas-successfactors-tutorial.png) | [SuccessFactors](successfactors-tutorial) | [SuccessFactors - User Provisioning](sap-successfactors-inbound-provisioning-tutorial) |
| ![logo-Workday](media/tutorial-list/entra-saas-workday-tutorial.png) | [Workday](workday-tutorial) | [Workday - inbound provisioning](workday-inbound-tutorial) |

To find more articles for SaaS apps, use the table of contents on the left. The list is divided into single sign on and provisioning articles.

## Cloud provider integrations

Some of the popular integrations with infrastructure providers include those in the following table.

| Logo | Application article for single sign-on | Application article for user provisioning |
| --- | --- | --- |
| ![logo-Amazon Web Services (AWS) Console](media/tutorial-list/entra-saas-amazon-web-service-tutorial.png) | [Amazon Web Services (AWS) Console](amazon-web-service-tutorial) | [Amazon Web Services (AWS) Console - Role Provisioning](amazon-web-service-tutorial#configure-azure-ad-sso) |
| ![logo-Alibaba Cloud Service (Role based SSO)](media/tutorial-list/entra-saas-alibaba-tutorial.png) | [Alibaba Cloud Service (Role based SSO)](alibaba-cloud-service-role-based-sso-tutorial) |  |
| ![logo-Google Cloud Platform](media/tutorial-list/entra-saas-google-apps-tutorial.png) | [Google Cloud Platform](google-apps-tutorial) | [Google Cloud Platform - User Provisioning](g-suite-provisioning-tutorial) |
| ![logo-Salesforce](media/tutorial-list/entra-saas-salesforce-tutorial.png) | [Salesforce](salesforce-tutorial) | [Salesforce - User Provisioning](salesforce-provisioning-tutorial) |
| ![logo-SAP Cloud Identity Services](media/tutorial-list/entra-saas-sapboc-tutorial.png) | [SAP Cloud Identity Services](sap-hana-cloud-platform-identity-authentication-tutorial) | [SAP Cloud Identity Services - Provisioning](sap-cloud-platform-identity-authentication-provisioning-tutorial) |