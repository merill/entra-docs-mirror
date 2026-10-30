---
layout: Landing
title: Application management documentation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/
summary: Microsoft Entra ID is an Identity and Access Management (IAM) system. It provides a single place to store information about digital identities. You can configure your software applications to use Microsoft Entra ID as the place where user information is stored.
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Microsoft Entra ID is an Identity and Access Management (IAM) system. It provides a single place to store information about digital identities. You can configure your software applications to use Microsoft Entra ID as the place where user information is stored.
ms.topic: landing-page
ms.date: 2025-03-31T00:00:00.0000000Z
locale: en-us
document_id: a418ca56-1f80-aec7-8230-4e3f3faa8f2f
document_version_independent_id: 019faa6c-44ce-75f4-d18f-9c2d479d0673
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/index.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: landing
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/index.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0e86bc8f-665f-4a47-4ba6-2a1e01594d8a
---

# Application management documentation

Microsoft Entra ID is an Identity and Access Management (IAM) system. It provides a single place to store information about digital identities. You can configure your software applications to use Microsoft Entra ID as the place where user information is stored.

## Fundamentals

### Overview

- [What is application management?](what-is-application-management)

### Concept

- [What type of apps does Microsoft Entra support?](../../identity-platform/v2-app-types)
- [What is single sign-on?](what-is-single-sign-on)

## Develop an app

### Concept

- [Authentication and authorization concepts](../../identity-platform/authentication-vs-authorization)

### How-To Guide

- [Build an app using Microsoft identities or social accounts](../../identity-platform/v2-overview)

## Integrate an app with the tenant

### How-To Guide

- [Get started with app integration](plan-an-application-integration)
- [Add a preintegrated cloud application](add-application-portal)
- [Register your app](../../identity-platform/quickstart-register-app)
- [Migrate AD FS apps to Microsoft Entra ID](migrate-adfs-apps-stages)

## Configure an app

### How-To Guide

- [Configure app properties](add-application-portal-configure)
- [Assign users and groups](assign-user-or-group-access-portal)
- [Provision an app](../../id-governance/what-is-provisioning)
- [Configure My Apps](myapps-overview)

### Reference

- [Manage applications using Microsoft Graph API](/en-us/graph/api/resources/applications-api-overview?view=graph-rest-1.0)

## Secure an app

### How-To Guide

- [Set up Conditional Access](../conditional-access/concept-conditional-access-cloud-apps)
- [Set up multifactor authentication](../authentication/howto-mfa-getstarted)
- [Manage certificates](tutorial-manage-certificates-for-federated-single-sign-on)
- [Set up tenant restrictions](tenant-restrictions)
- [Configure token encryption](howto-saml-token-encryption)
- [Use Defender for Cloud Apps](cloud-app-security)
- [Act on overprivileged and suspicious app](manage-application-permissions)

## Manage app access

### Overview

- [Identity governance](../../id-governance/identity-governance-overview)
- [User and admin consent](user-admin-consent-overview)

### How-To Guide

- [Assign roles](../../identity-platform/howto-add-app-roles-in-apps)
- [Configure user consent](configure-user-consent)
- [Configure admin consent](configure-admin-consent-workflow)
- [Configure permissions classification](configure-permission-classifications)
- [Manage entitlement](../../id-governance/entitlement-management-scenarios)

## Maintain an app

### How-To Guide

- [View, search, sort, filter list of apps in a tenant](view-applications-portal)
- [Troubleshoot sign-in errors](../monitoring-health/howto-troubleshoot-sign-in-errors)
- [Disable user sign-in for an app](disable-user-sign-in-portal)
- [Remove user access to an app](methods-for-removing-user-access)
- [Delete an app](delete-application-portal)

## Monitor an app

### Concept

- [Sign in logs](../monitoring-health/concept-sign-ins)
- [Usage and insights report](../monitoring-health/concept-usage-insights-report)
- [Audit logs](../monitoring-health/concept-audit-logs)
- [Provisioning logs](../monitoring-health/concept-provisioning-logs)

### How-To Guide

- [Access activity logs](../monitoring-health/howto-access-activity-logs)
- [Download logs](../monitoring-health/howto-download-logs)
- [Set up access reviews](../../id-governance/deploy-access-reviews)
- [Assign owners](assign-app-owners)

## Remote access to on-premises apps

### Concept

- [Application proxy](/en-us/entra/identity/app-proxy)

### How-To Guide

- [Plan application proxy deployment](../app-proxy/conceptual-deployment-plan)
- [Set up connectors](../../global-secure-access/concept-connectors)
- [Configure single sign-on](../app-proxy/how-to-configure-sso)
- [Publish native client applications](../app-proxy/application-proxy-configure-native-client-application)
- [Publish claims-aware applications](../app-proxy/application-proxy-configure-for-claims-aware-applications)