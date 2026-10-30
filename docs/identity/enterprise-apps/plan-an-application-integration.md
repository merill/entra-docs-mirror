---
layout: Conceptual
title: Get started integrating Microsoft Entra ID with apps - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/plan-an-application-integration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: This article is a getting started guide for integrating Microsoft Entra ID with on-premises applications, and cloud applications.
ms.topic: concept-article
ms.date: 2024-12-05T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: enterprise-apps
locale: en-us
document_id: f70b403f-9f38-8148-6404-11763d5784ff
document_version_independent_id: 9c7a9956-c023-053e-6943-27d37b2260ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/plan-an-application-integration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/plan-an-application-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/plan-an-application-integration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6fdcd331-6df1-d5e5-66d2-a0907911c19c
---

# Get started integrating Microsoft Entra ID with apps - Microsoft Entra ID | Microsoft Learn

This article summarizes the process for integrating applications with Microsoft Entra ID. Each of the following sections contains a brief summary of a more detailed article so you can identify which parts of this getting started guide are relevant to you.

To download in-depth deployment plans, see Next steps.

## Take inventory

Before integrating applications with Microsoft Entra ID, it's important to know where you are and where you want to go. The following questions are intended to help you think about your Microsoft Entra application integration project.

### Application inventory

- Where are all of your applications? Who owns them?
- What kind of authentication do your applications require?
- Who needs access to which applications?
- Do you want to deploy a new application?
    - Will you build it in-house and deploy it on an Azure compute instance?
    - Will you use one that is available in the Azure Application Gallery?

### User and group inventory

- Where do your user accounts reside?
    - On-premises Active Directory
    - Microsoft Entra ID
    - Within a separate application database that you own
    - In unsanctioned applications
    - All of the listed options
- What permissions and role assignments do individual users currently have? Do you need to review their access or are you sure that your user access and role assignments are appropriate now?
- Are groups already established in your on-premises Active Directory?
    - How are your groups organized?
    - Who are the group members?
    - What permissions/role assignments do the groups currently have?
- Will you need to clean up user/group databases before integrating? (This is an important question. Garbage in, garbage out.)

### Access management inventory

- How do you currently manage user access to applications? Does that need to change? Have you considered other ways to manage access, such as with [Azure RBAC](/en-us/azure/role-based-access-control/role-assignments-portal) for example?
- Who needs access to what?

Maybe you don't have the answers to all of these questions up front but that's okay. This guide can help you answer some of those questions and make some informed decisions.

### Find unsanctioned cloud applications with Cloud Discovery

As mentioned the previous section, there might be applications that your organization manages until now. As part of the inventory process, it's possible to find unsanctioned cloud applications. See [Set up Cloud Discovery](/en-us/defender-cloud-apps/set-up-cloud-discovery).

## Integrating applications with Microsoft Entra ID

The following articles discuss the different ways applications integrate with Microsoft Entra ID, and provide some guidance.

- [Using applications in the Azure application gallery](what-is-single-sign-on)
- [Integrating SaaS applications tutorials list](../saas-apps/tutorial-list)

## Capabilities for apps not listed in the Microsoft Entra gallery

You can add any application that already exists in your organization, or any third-party application from a vendor who isn't already part of the Microsoft Entra gallery. Depending on your [license agreement](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing), the following capabilities are available:

- Self-service integration of any application that supports [Security Assertion Markup Language (SAML) 2.0](https://wikipedia.org/wiki/SAML_2.0) identity providers (SP-initiated or IdP-initiated)
- Self-service integration of any web application that has an HTML-based sign-in page using [password-based SSO](plan-sso-deployment#password-based-sso)
- Self-service connection of applications that use the [System for Cross-Domain Identity Management (SCIM) protocol for user provisioning](../app-provisioning/use-scim-to-provision-users-and-groups)
- Ability to add links to any application in the [Office 365 app launcher](https://support.microsoft.com/office/meet-the-microsoft-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) or [My Apps](https://myapplications.microsoft.com/)

If you're looking for developer guidance on how to integrate custom apps with Microsoft Entra ID, see [Authentication Scenarios for Microsoft Entra ID](../../identity-platform/authentication-vs-authorization). When you develop an app that uses a modern protocol like [OpenId Connect/OAuth](../../identity-platform/v2-protocols) to authenticate users, register it with the Microsoft identity platform. You can register by using the [App registrations](../../identity-platform/quickstart-register-app) experience in the Azure portal.

### Authentication Types

Each of your applications might have different authentication requirements. With Microsoft Entra ID, signing certificates can be used with applications that use SAML 2.0, WS-Federation, or OpenID Connect Protocols and Password Single Sign On. For more information about application authentication types, see [Managing certificates for federated single sign-on in Microsoft Entra ID](tutorial-manage-certificates-for-federated-single-sign-on) and [Password based single sign on](what-is-single-sign-on).

### Enabling SSO with Microsoft Entra application proxy

With Microsoft Entra application proxy, you can provide access to applications located inside your private network securely, from anywhere and on any device. After you install a private network connector within your environment, it can be easily configured with Microsoft Entra ID.

### Integrating custom applications

If you want to add your custom application to the Azure Application Gallery, see [Publish your app to the Microsoft Entra app gallery](v2-howto-app-gallery-listing).

## Managing access to applications

The following articles describe ways you can manage access to applications once they're integrated with Microsoft Entra ID using Microsoft Entra Connectors and Microsoft Entra ID.

- [Managing access to apps using Microsoft Entra ID](what-is-access-management)
- [Automating with Microsoft Entra Connectors](../app-provisioning/user-provisioning)
- [Assigning users to an application](assign-user-or-group-access-portal)
- [Assigning groups to an application](assign-user-or-group-access-portal)
- [Sharing accounts](../users/users-sharing-accounts)