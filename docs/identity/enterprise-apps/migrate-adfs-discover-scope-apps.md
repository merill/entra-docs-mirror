---
layout: Conceptual
title: 'Phase 1: Discover and scope apps - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-adfs-discover-scope-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: This article describes phase 1 of planning migration of applications from AD FS to Microsoft Entra ID
ms.topic: concept-article
ms.date: 2025-01-31T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
locale: en-us
document_id: 033f1403-d7df-5d39-0bbd-cea1288bc68f
document_version_independent_id: befecdb8-64be-43a6-2fc6-d82907e41c82
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migrate-adfs-discover-scope-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migrate-adfs-discover-scope-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migrate-adfs-discover-scope-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 5a7da6b6-7303-f9f2-26c7-d36afe23fc0c
---

# Phase 1: Discover and scope apps - Microsoft Entra ID | Microsoft Learn

Application discovery and analysis are a fundamental exercise to give you a good start. You may not know everything so be prepared to accommodate the unknown apps.

## Find your apps

The first decision in the migration process is which apps to migrate, which if any should remain, and which apps to deprecate. There's always an opportunity to deprecate the apps that you won't use in your organization. There are several ways to find apps in your organization. While discovering apps, ensure you include in-development and planned apps. Use Microsoft Entra ID for authentication in all future apps.

Discover applications using ADFS:

- **Use Microsoft Entra Connect Health for ADFS**: If you have a Microsoft Entra ID P1 or P2 license, we recommend deploying [Microsoft Entra Connect Health](../hybrid/connect/how-to-connect-health-adfs) to analyze the app usage in your on-premises environment. You can use the [ADFS application report](migrate-adfs-application-activity) to discover ADFS applications that can be migrated and evaluate the readiness of the application to be migrated.
- If you don’t have Microsoft Entra ID P1 or P2 licenses, we recommend using the ADFS to Microsoft Entra app migration tools based on [PowerShell](https://github.com/AzureAD/Deployment-Plans/tree/master/ADFS%20to%20AzureAD%20App%20Migration). Refer to [solution guide](migrate-adfs-apps-stages):

Note

This video covers both phase 1 and 2 of the migration process.

## Using other identity providers (IdPs)

If you're using other identity providers, you can use the following approaches to discover applications:

- If you’re currently using Okta, refer to our [Okta to Microsoft Entra migration guide](migrate-applications-from-okta).
- If you're currently using Ping Federate, then consider using the [Ping Administrative API](https://docs.pingidentity.com/pingfederate/latest/developers_reference_guide/pf_admin_api.html)
- If the applications are integrated with Active Directory, search for service principals or service accounts that may be used for applications.

## Using cloud discovery tools

In the cloud environment, you need rich visibility, control over data travel, and sophisticated analytics to find and combat cyber threats across all your cloud services. You can gather your cloud app inventory using the following tools:

- **Cloud Access Security Broker (CASB**) – A [CASB](/en-us/defender-cloud-apps/) typically works alongside your firewall to provide visibility into your employees’ cloud application usage and helps you protect your corporate data from cybersecurity threats. The CASB report can help you determine the most used apps in your organization, and the early targets to migrate to Microsoft Entra ID.
- **Cloud Discovery** - By configuring [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps), you gain visibility into the cloud app usage, and can discover unsanctioned or Shadow IT apps.
- **Azure Hosted Applications**- For apps connected to Azure infrastructure, you can use the APIs and tools on those systems to begin to take an inventory of hosted apps. In the Azure environment:
    - Use the [Get-AzWebApp](/en-us/powershell/module/Az.websites/get-Azwebapp) cmdlet to get information about your Azure Web Apps.
    - Query Microsoft Entra ID looking for [Applications](/en-us/previous-versions/azure/ad/graph/api/entity-and-complex-type-reference#application-entity) and [Service Principals](/en-us/previous-versions/azure/ad/graph/api/entity-and-complex-type-reference#serviceprincipal-entity).

## Manual discovery process

Once you've taken the automated approaches described in this article, you have a good handle on your applications. However, you might consider doing the following to ensure you have good coverage across all user access areas:

- Contact the various business owners in your organization to find the applications in use in your organization.
- Run an HTTP inspection tool on your proxy server, or analyze proxy logs, to see where traffic is commonly routed.
- Review weblogs from popular company portal sites to see what links users access the most.
- Reach out to executives or other key business members to ensure that you've covered the business-critical apps.

## Type of apps to migrate

Once you find your apps, you identify these types of apps in your organization:

- Apps that use modern authentication protocols such as [Security Assertion Markup Language (SAML)](../../architecture/auth-saml) or [OpenID Connect (OIDC)](../../architecture/auth-oidc).
- Apps that use legacy authentication such as [Kerberos](https://techcommunity.microsoft.com/t5/itops-talk-blog/deep-dive-how-azure-ad-kerberos-works/ba-p/3070889) or NT LAN Manager (NTLM) that you choose to modernize.
- Apps that use legacy authentication protocols that you choose NOT to modernize
- New Line of Business (LoB) apps

### Apps that use modern authentication already

The already modernized apps are the most likely to be moved to Microsoft Entra ID. These apps already use modern authentication protocols such as SAML or OIDC and can be reconfigured to authenticate with Microsoft Entra ID.

We recommend you search and add applications from the [Microsoft Entra app gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps). If you don’t find them in the gallery, you can still onboard a custom application.

### Legacy apps that you choose to modernize

For legacy apps that you want to modernize, moving to Microsoft Entra ID for core authentication and authorization unlocks all the power and data-richness that the [Microsoft Graph](https://developer.microsoft.com/graph/gallery/?filterBy=Samples,SDKs) and [Intelligent Security Graph](https://www.microsoft.com/security/operations/intelligence?rtc=1) have to offer.

We recommend updating the authentication stack code for these applications from the legacy protocol (such as Windows-Integrated Authentication, Kerberos, HTTP Headers-based authentication) to a modern protocol (such as SAML or OpenID Connect).

### Legacy apps that you choose NOT to modernize

For certain apps using legacy authentication protocols, sometimes modernizing their authentication isn't the right thing to do for business reasons. These include the following types of apps:

- Apps kept on-premises for compliance or control reasons.
- Apps connected to an on-premises identity or federation provider that you don't want to change.
- Apps developed using on-premises authentication standards that you have no plans to move

Microsoft Entra ID can bring great benefits to these legacy apps. You can enable modern Microsoft Entra security and governance features like [Multi-Factor Authentication](../authentication/concept-mfa-howitworks), [Conditional Access](../conditional-access/overview), [Microsoft Entra ID Protection](../../id-protection/), [Delegated Application Access](manage-self-service-access), and [Access Reviews](../../id-governance/manage-user-access-with-access-reviews#create-and-perform-an-access-review) against these apps without touching the app at all!

- Start by extending these apps into the cloud with [Microsoft Entra application proxy](/en-us/entra/identity/app-proxy).
- Or explore using on of our [Secure Hybrid Access (SHA) partner integrations](secure-hybrid-access) that you might have deployed already.

### New Line of Business (LoB) apps

You usually develop LoB apps for your organization’s in-house use. If you have new apps in the pipeline, we recommend using the [Microsoft identity platform](../../identity-platform/v2-overview) to implement OIDC.

## Apps to deprecate

Apps without clear owners and clear maintenance and monitoring present a security risk for your organization. Consider deprecating applications when:

- Their **functionality is highly redundant** with other systems
- There's **no business owner**
- There's clearly **no usage**

We recommend that you **do not deprecate high impact, business-critical applications**. In those cases, work with business owners to determine the right strategy.

## Exit criteria

You're successful in this phase with:

- A good understanding of the applications in scope for migration, those that require modernization, those that should stay as-is, or those you've marked for deprecation.