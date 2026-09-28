---
layout: Conceptual
title: Overview of the Microsoft Entra application gallery - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/overview-application-gallery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Explore the Microsoft Entra application gallery for seamless SaaS integration with preconfigured SSO and user provisioning. Enhance cloud app deployment.
ms.topic: overview
ms.date: 2026-01-05T00:00:00.0000000Z
ms.reviewer: ergreenl
ms.custom: enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 55052925-0511-c3b4-6f64-90123abff3f6
document_version_independent_id: a9fae159-bcac-cd52-8551-186c7f1fe762
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/overview-application-gallery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/overview-application-gallery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/overview-application-gallery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 8f864b4f-339d-152e-5763-8e0705bdb859
---

# Overview of the Microsoft Entra application gallery - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra application gallery is a collection of software as a service (SaaS) [applications](../../identity-platform/app-objects-and-service-principals) that are preintegrated with Microsoft Entra ID. The collection contains thousands of applications that make it easy to deploy and configure [single sign-on (SSO)](../../identity-platform/single-sign-on-saml-protocol) and [automated user provisioning](../app-provisioning/user-provisioning).

To find the gallery when signed into your tenant, browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications** &gt; **New application**.

The applications available from the gallery follow the SaaS model that allows users to connect to and use cloud-based applications over the Internet. Common examples are email, calendaring, and office tools (such as Microsoft Office 365).

The following are benefits of using applications available in the gallery:

- Users find the best possible SSO experience for the application.
- Configuration of the application is simple and minimal.
- A quick search finds the needed application.
- Free, Basic, and Premium Microsoft Entra users can all use the application.
- Users can easily find [step-by-step configuration tutorials](../saas-apps/tutorial-list) that are available for onboarding gallery applications.
- Organizations can assess application security through calculated risk scores that evaluate over 90 risk factors across security, compliance, legal, and general categories.

## Applications in the gallery

The gallery contains thousands of applications that are preintegrated into Microsoft Entra ID. When using the gallery, you choose from using applications from specific cloud platforms, featured applications, or you search for the application that you want to use.

### Search for applications

If you don’t find the application that you're looking for in the featured applications, you can search for a specific application by name.

![Screenshot showing the search options on the Microsoft Entra application gallery pane in the Microsoft Entra admin center.](media/overview-application-gallery/search-applications.png)

When searching for an application, you can also specify specific filters, such as single sign-on options, automated provisioning, and categories.

- **Single sign-on options** – You can search for applications that support these SSO options: SAML, OpenID Connect (OIDC), Password, or Linked. For more information about these options, see [Plan a single sign-on deployment in Microsoft Entra ID](plan-sso-deployment).
- **User account management** – The only option available is [automated provisioning](../app-provisioning/user-provisioning).
- **Categories** – When an application is added to the gallery it can be classified in a specific category. Many categories are available such as **Business management**, **Collaboration**, or **Education**.
- **Risk Score** – View applications by their calculated security risk score from 1 (highest risk) to 10 (lowest risk). This score helps identify applications that meet your organization's security requirements.
- **Security Risk Factors** – Search for applications that meet specific security measures such as multifactor authentication, admin audit trail, user audit trail, and other security standards that protect data used by the application.
- **Compliance Risk Factors** – Narrow results to applications with compliance standards and certifications such as SOC 2, ISO 27001, HIPAA, and other regulatory requirements that ensure the application meets industry best practices.

Note

In an [external tenant](/en-us/entra/external-id/customers/overview-customers-ciam), enterprise applications are supported, but the application gallery catalog isn't available. To find and add enterprise applications in the external tenant, select **New application** &gt; **Create your own application**, then type the name of the app in the search bar and select it from the list once it appears.

### Cloud platforms

Applications that are specific to major cloud platforms, such as AWS, Google, or Oracle can be found by selecting the appropriate platform.

![Screenshot showing the cloud application options on the Microsoft Entra application gallery pane in the Microsoft Entra admin center.](media/overview-application-gallery/cloud-applications.png)

### On-premises applications

There are five ways on-premises applications can be connected to Microsoft Entra ID. One is using Microsoft Entra application proxy for single sign-on. If your application supports single-sign on via SAML or Kerberos, then from the on-premises section of the Microsoft Entra gallery, you can undertake the following tasks:

- Configure Application Proxy to enable remote access to an on-premises application.
- Use the documentation to learn more about how to use Application Proxy to secure remote access to on-premises applications.
- Manage any private network connectors that you created.

![Screenshot showing the on-premises application options on the Microsoft Entra application gallery pane in the Microsoft Entra admin center.](media/overview-application-gallery/on-premises-applications.png)

If your application uses Kerberos and also requires group memberships, you can populate Windows Server AD groups from corresponding groups in Microsoft Entra ID. For more information, see [Group writeback with Microsoft Entra Cloud Sync](../hybrid/group-writeback-cloud-sync).

The second is using the provisioning agent to provision to an on-premises application that has its own user store and doesn't rely upon Windows Server AD. You can configure provisioning to [on-premises applications that support SCIM](../app-provisioning/on-premises-scim-provisioning), that use [SQL databases](../app-provisioning/on-premises-sql-connector-configure), that use an [LDAP directory](../app-provisioning/on-premises-ldap-connector-configure), or support a [SOAP or REST provisioning API](../app-provisioning/on-premises-web-services-connector).

The third is using Microsoft Entra Private Access, by configuring a Global Secure Access app for per-app connections. For more information, see [Learn about Microsoft Entra Private Access](/en-us/entra/global-secure-access/concept-private-access).

The fourth is to use the application's own connector. If you have [`SAP S/4HANA On-premise`](https://help.sap.com/docs/identity-provisioning/identity-provisioning/target-sap-s-4hana-on-premise), then provision users from Microsoft Entra ID to SAP Cloud Identity Directory. SAP Cloud Identity Services then provisions the users that are in the SAP Cloud Identity Directory into the downstream SAP applications, such as `SAP S/4HANA On-Premise`, through the SAP cloud connector. For more information, see [plan deploying Microsoft Entra for user provisioning with SAP source and target apps](../app-provisioning/plan-sap-user-source-and-target).

The fifth is to use a third party integration technology. In cases where an application doesn't support standards such as SCIM, partners have custom ECMA connectors and SCIM gateways to integrate Microsoft Entra ID with more applications, including on-premises applications. For more information, see the list of [available partner-driven integrations](../app-provisioning/partner-driven-integrations#available-partner-driven-integrations).

### Featured applications

A collection of featured applications is listed by default when you open the Microsoft Entra gallery. Each application is marked with a symbol to enable you to identify whether it supports federated SSO or automated provisioning.

![Screenshot showing the featured applications on the Microsoft Entra application gallery pane in the Microsoft Entra admin center.](media/overview-application-gallery/featured-applications.png)

- **Federated SSO** - When you set up [SSO](what-is-single-sign-on) to work between multiple identity providers, it results to federation. An SSO implementation based on federation protocols improves security, reliability, user experiences, and implementation. Some applications implement federated SSO as SAML-based or as OIDC-based. For SAML applications, when you select create, the application is added to your tenant. For OIDC applications, the administrator must first sign up or sign-in to the application's website to add the application to Microsoft Entra ID.
- **Provisioning** - Microsoft Entra ID to SaaS [application provisioning](../app-provisioning/user-provisioning) refers to automatically creating user identities and roles in the SaaS applications that users need access to.

Note

Linked Sign-on gallery applications will have a grayed out 'Create' button. The Linked Sign-on URL is provided to be used in the create your own application option.

The **Create** button might appear disabled for certain gallery apps by design. This occurs in two scenarios: First, for linked-based SSO applications. These templates are link-only and don't support creating a new app or service principal in Microsoft Entra ID. They redirect users to an external URL managed by the service provider. Because no Microsoft Entra object is created, the button is intentionally unavailable.

Second, when the app already exists in your tenant, as gallery applications are limited to one instance per tenant. In both cases, a disabled **Create** button is expected behavior.

## Understanding application risk scores

Microsoft Defender for Cloud Apps assigns risk scores to SaaS applications in the gallery to help organizations evaluate security posture and make informed adoption decisions. Access to risk score information requires either [Microsoft Entra Suite](/en-us/entra/fundamentals/licensing) or [Microsoft Entra Internet Access](/en-us/entra/global-secure-access/concept-internet-access) licenses.

Each application is scored from 1 to 10, where 1 indicates highest risk and 10 indicates lowest risk. Scores are calculated using a weighted average across four risk categories:

- **General**: Company stability, domain age, and popularity
- **Security**: Encryption methods, multi-factor authentication, and audit trails
- **Compliance**: Standards like SOC 2, ISO 27001, HIPAA, and PCI
- **Legal**: Data protection policies and regulatory compliance

The scoring model evaluates more than 90 risk factors derived from publicly available data, vendor disclosures, and observed security practices.

This risk assessment capability helps IT administrators identify potential security vulnerabilities and make data-driven decisions when selecting applications for their organization.

Application owners can request updates to risk scores by navigating to the gallery -&gt; Selecting the app that needs an update -&gt; Scrolling to the specific risk factor that needs an update -&gt; Selecting the feedback symbol on the right side of the risk factor name -&gt; Completing the **Give feedback to Microsoft** form with options like score update request, outdated app data, or suggesting new risk factors -&gt; providing detailed information about the requested changes and submitting the request.

Note

Feedback submitted through this process is sent to Microsoft Defender for Cloud Apps, which reviews and makes any necessary updates to application risk scores and data.

![Screenshot showing application risk score details with feedback options for individual risk factors.](media/overview-application-gallery/app-risk-score-details.png)

For detailed information about risk scoring methodology and how to request score updates on Microsoft Defender for Cloud Apps, see [Find your cloud app and calculate risk scores](/en-us/defender-cloud-apps/risk-score). You can also programmatically access application templates and their risk scores using the [List applicationTemplates API](/en-us/graph/api/applicationtemplate-list).

## Create your own application

When you select the **Create your own application** link near the top of the pane, you see a new pane that lists the following choices:

- **Register an application to integrate with Microsoft Entra ID (App you're developing)** – This choice is meant for developers who want to work on the integration of their application that uses OpenID Connect with Microsoft Entra ID. This choice doesn't provide an opportunity to publish your application to the gallery. It's only for development purposes to work on integration. For more information, see [Set up OIDC-based single sign-on for an application](add-application-portal-setup-oidc-sso).
- **Configure Application Proxy for secure remote access to an on-premises application** – This choice is meant for an administrator to enable SSO and secure remote access for web applications hosted on-premises by connecting with Application Proxy. For more information, see [What is Microsoft Entra Application Proxy?](../app-proxy/overview-what-is-app-proxy).

## Request an app to be added to the gallery

After you successfully integrate an application with Microsoft Entra ID and thoroughly tested it, you file a request for it to be added to the gallery. Publishing an application to the gallery from the portal isn't supported but there's a process that you can follow to request it to be added. For more information about publishing to the gallery, select [Request new gallery application](v2-howto-app-gallery-listing).