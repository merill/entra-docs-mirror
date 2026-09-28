---
layout: Conceptual
title: Use partner driven integrations to provision accounts into all your applications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/partner-driven-integrations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Use partner driven integrations to provision accounts into all your applications.
ms.topic: overview
ms.date: 2025-07-24T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: 64da82a5-4e5b-28d4-d872-1b196a3394a7
document_version_independent_id: 721042bb-961d-d30a-c54c-4d208bfb046f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/partner-driven-integrations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/partner-driven-integrations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/partner-driven-integrations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 20508ca0-9c35-018d-6529-4603ae1a8b8b
---

# Use partner driven integrations to provision accounts into all your applications - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra provisioning service allows you to provision users and groups into both [SaaS](user-provisioning) and [on-premises](on-premises-scim-provisioning) applications. There are four integration paths:

**Option 1 - Microsoft Entra Application Gallery:** Popular third party applications, such as Dropbox, Snowflake, and Workplace by Facebook, are made available for customers through the Microsoft Entra application gallery. New applications can easily be onboarded to the gallery using the [application network portal](../enterprise-apps/v2-howto-app-gallery-listing).

**Option 2 - Implement a SCIM compliant API for your application:** If your line-of-business application supports the [SCIM](https://aka.ms/scimoverview) standard, it can easily be integrated with the [Microsoft Entra SCIM client](use-scim-to-provision-users-and-groups).

[![Diagram showing implementation of a SCIM compliant API for your application.](media/partner-driven-integrations/scim-compliant-api-1.png)](media/partner-driven-integrations/scim-compliant-api-1.png#lightbox)

**Option 3 - Use Microsoft Graph:** Many new applications use Microsoft Graph to retrieve users, groups, and other resources from Microsoft Entra ID. You can learn more about what scenarios to use [SCIM and Graph](scim-graph-scenarios) in.

**Option 4 - Use partner-driven connectors:** In cases where an application doesn't support SCIM, partners have built [custom ECMA connectors](on-premises-custom-connector) and SCIM gateways to integrate Microsoft Entra ID with numerous applications. **This document serves as a place for partners to attest to integrations that are compatible with Microsoft Entra ID, and for customers to discover these partner-driven integrations.** Custom ECMA connectors and SCIM gateways are built, maintained, and owned by the third-party vendor.

[![Diagram showing gateways between the Microsoft Entra SCIM client and target applications.](media/partner-driven-integrations/partner-driven-connectors-1.png)](media/partner-driven-integrations/partner-driven-connectors-1.png#lightbox)

## Available partner-driven integrations

The following descriptions and lists of applications are provided by the partners themselves. You can use the lists of applications supported to identify a partner that you may want to contact and learn more about.

### Aquera

#### Description

With 1,000+ customer deployments, Aquera delivers HR process and Identity Integration for Microsoft Active Directory (AD) and Microsoft Entra ID. Aquera automates user account provisioning and deprovisioning throughout the employee lifecycle to enable joiner, mover, leaver automation. Aquera’s prebuilt, out-of-the-box [HR Sync Connectors](https://azuremarketplace.microsoft.com/marketplace/apps/aquerainc1584125423571.hr-sync-for-microsoft-entra-id-azure-ad-by-aquera?tab=Overview) enable 50+ HR/HCM systems of record to automate HR-driven user and account inbound provisioning to AD and Microsoft Entra ID. Beyond HR systems of record, Aquera SCIM Gateway for Microsoft Entra ID provisions and deprovisions users, accounts, and groups (where available) to non-gallery apps through industry-standard System for Cross-domain Identity Management (SCIM). Since 2020, [Microsoft and Aquera have extended Microsoft Entra ID connectivity to hundreds of apps not found in the Microsoft Entra App Gallery](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/automate-user-provisioning-for-more-applications-with-our-new/ba-p/1751668).

The Aquera SCIM Gateway delivers out-of-the-box connectivity between Microsoft Entra ID and the provisioning target applications, directories, databases, devices, files, or 3rd-party identity providers (IDPs) for B2B partners, which aren't included in the [Microsoft Entra App Gallery](https://portal.azure.com/#view/Microsoft_AAD_IAM/AppGalleryBladeV2), or where Gallery apps do not support automatic provisioning. Microsoft + Aquera extend [Microsoft Entra ID to scale identity management](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-lifecycle-management-software) as user identities, roles, and entitlements change dynamically. The Aquera catalog of over 900 prebuilt connectors supports multiple integration methods including REST, SQL, LDAP, SOAP, and SCIM, and SCIM that isn't compatible with Microsoft Entra ID. Additionally, the connectors support web service APIs, admin console automation, SDKs, code libraries, files, and [Microsoft API-driven Inbound Provisioning](inbound-provisioning-api-concepts).

#### Contact Information

- Company website: https://www.aquera.com
- Azure Marketplace Listings: [https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=aquera&page=1](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=aquera&amp;page=1)
- AppSource Marketplace Listings: [https://appsource.microsoft.com/en-us/marketplace/apps?search=aquera&page=1](https://appsource.microsoft.com/en-us/marketplace/apps?search=aquera&amp;page=1)

#### Popular applications supported

- Human resources information systems applications: Over 40 including Oracle Cloud HCM, Dayforce, UKG Pro/Ready/Pro Workforce, ADP (all US and international versions), Workday, SAP HR, Greenhouse, iCIMS, SuccessFactors, HiBob, BambooHR, Paylocity, Paycor, PeopleSoft, Cornerstone, Lever
- Enterprise resource planning applications: Netsuite, Oracle Cloud ERP, Oracle EBS, SAP ERP Central Component (ECC), SAP S/4HANA, Sage Intacct, PeopleSoft ERP
- Electronic health record applications: Epic, Cerner, PointClickCare, MyAvatar, Homecare Homebase
- Student Information Systems: Ellucian Banner, PeopleSoft Campus Solutions
- Databases: Oracle, MySQL, SQLServer, MongoDB, PostgreSQL, AS/400 DB2, DB2, Snowflake, Redshift
- Directories and IDPs: AS/400, Resource Access Control Facility (RACF), ACF2, TopSecret, OpenLDAP, IDP Directories

### IDMWORKS

#### Description

We're Experts In Identity & Access Management and Data Center Management. The Microsoft Entra platform integrates with IDMWORKS IdentityForge (IDF) Gateway for user lifecycle management for Mainframe systems RACF, Top Secret, and ACF2, Midrange system AS/400, Healthcare applications EPIC and Cerner, Linux and Unix servers, Databases, and dozens of on-premises and cloud applications. IdentityForge provides a central, standardized integration engine and modern identity store that serves as a trusted source for all lifecycle management. The IDF Gateway for Microsoft Entra ID provides lifecycle management for import sources and provisioning target systems that aren't covered by the Microsoft Entra connector portfolio like Mainframe systems RACF, Top Secret, and ACF2, or Healthcare applications EPIC and Cerner. The IDF Gateway powers Microsoft Entra identity lifecycle management (LCM) to continuously synchronize user account information from Mainframe and Healthcare sources and to automate the account provisioning lifecycle use cases like create, read or import, update, deactivate, delete user accounts, and perform group management.

#### Contact information

- Company website: https://www.idmworks.com/
- Contact information: https://www.idmworks.com/contact/

#### Popular applications supported

Leading provider of Mainframe, Healthcare and ERP integrations. More can be found at https://www.idmworks.com/product/identityforge-connectors/

- IBM RACF
- CA Top Secret
- CA ACF2
- IBM i (AS/400)
- HP NonStop
- EPIC
- SAP ECC

### KloudIdentity

#### Description

KloudIdentity streamlines enterprise operations by simplifying the onboarding process of on-premises Line of Business (LOB) applications and facilitating outbound provisioning of users and groups through Microsoft Entra ID. It serves as a SCIM gateway, enabling non-SCIM compliant LOB applications to seamlessly integrate with Microsoft Entra ID. This application is founded upon a unique design paradigm known as the universal connector space, which offers a standardized platform for creating connectors for various LOB applications through a template-driven approach. This methodology significantly reduces lead time and costs associated with onboarding non-SCIM compliant LOB applications to Microsoft Entra ID for outbound provisioning.

Integration with LOB applications is primarily achieved through REST APIs, with support also extended to SOAP APIs and PowerShell scripts. Administrators can easily configure attribute mapping templates using a user-friendly web portal. Beyond graphical UI-driven attribute mapping, KloudIdentity offers a customizable policies-based approach, allowing for the configuration of highly tailored sequences of attribute mapping and payload generation.

Furthermore, KloudIdentity provides a Software Development Kit (SDK) to customize the standard connector platform, addressing complex and advanced integration scenarios. This SDK empowers users to make code modifications within the KloudIdentity framework safely and efficiently, enabling seamless integration of LOB applications for users and groups provisioning. The SCIM gateway can be deployed either as a cloud-based solution or within on-premises data centers, supporting a range of deployment options from conventional Internet Information Services (IIS) setups to Kubernetes orchestrated environments

#### Contact information

- Company website: https://www.kloudynet.com/
- Azure Marketplace Listing: https://azuremarketplace.microsoft.com/en-us/marketplace/consulting-services/kloudynettechnologiessdnbhd1588004273044.identity_implementation

#### Popular applications supported

KloudIdentity provides a universal connector platform; Hence any LOB application can be integrated with REST or SOAP APIs, PowerShell scripts, and SDK approach.

### Quorum Systems Identity DNA

#### Description

Identity DNA is Quorum’s purpose built platform designed to complement and enhance native Microsoft Entra ID Governance capabilities. The service acts as a System for Cross-domain Identity Management (SCIM) gateway, and it is deployed in customer's Azure environment and managed via CICD pipelines.

The Identity DNA platform is designed to handle complex integration scenarios while allowing customers to enhance end to end identity flow, achieving a better user experience and addressing key business and technical challenges.

The Identity DNA platform is able to connect to any application through a number of pre defined connections (REST API, SOAP API, Database, PowerShell, or CSV) to data sources either in the cloud or on-premises.

Identity DNA then converts that data to a System for Cross-domain Identity Management (SCIM) payload and delivers that to the Entra provisioning service. The Identity DNA platform allows for data between applications to be synced bidirectionally ensuring disparate systems identities are kept up to date with ease.

#### Contact information

- Company website: https://quorumsystems.com.au/
- AppSource Listing: Entra User ID Provisioning https://appsource.microsoft.com/en-us/marketplace/consulting-services/quorumsystemsptyltd1587621343059.entrauseridprovisioning

#### Popular applications supported

Identity DNA can be integrated with any line of business application that has REST or SOAP API's, Databases, PowerShell scripts, or even other directory services such as LDAP.

### Traxion SCIM Gateway

#### Description

At Traxion, we believe that industry-wide standardization plays a large role in the future of Identity and Access Management (IAM). We're determined to help our customers achieve their security goals by using best practices and common standards. System for Cross-domain Identity Management (SCIM) is such a standard.

Companies deploying an IGA system are challenged with how hard it can be to connect applications for synchronizing users, groups, and other data entities. The process of connecting and maintaining application integrations has proven to be a challenging, time-consuming, and costly process; not only for the companies deploying an IAM system but also for application vendors and integrators. It's especially tough when connecting an application that doesn't support a common standard such as SCIM 2.0. By using our SCIM Gateway we enable our customers to leverage the benefits of a standardized integration by reducing lead times and overall costs.

Our SCIM Gateway is an easy, secure, and standardized solution, that will enable you to synchronize all identity and access information with any non-natively SCIM supporting application.

Integrations include:

- AFAS Profit
- Splunk
- ATS
- Oracle ERP
- SAP SuccessFactors
- Tempus Resources
- Generic connectors (CSV, SQL)
- Develop your own connector using our [public SDK](https://www.nuget.org/packages/Traxion.Scim.Gateway.Connectors.Sdk)

#### Contact information

- Company website: https://www.traxion.com/products/iam-integration/scim-gateway/
- Contact information: https://www.traxion.com/contact/

### UNIFY Solutions

#### Description

UNIFY Solutions is a leading provider of Identity, Access, Security, and Governance solutions.

#### Contact information

- Company website: https://unifysolutions.net/identity/unifyconnect
- Contact information: https://unifysolutions.net/contact/

#### Popular applications supported

- Aurion People & Payroll
- Frontier Software chris21
- TechnologyOne HR
- Ascender HCM
- Fusion5 EmpowerHR
- SAP ERP Human Capital Management

### Custom connectors

Microsoft Entra ID includes connectivity to provision into applications that support protocols and interfaces including SCIM, SQL, LDAP, REST, SOAP, and PowerShell. For connectivity to applications that don't support one of those protocols and interfaces, customers and [partners](/en-us/archive/technet-wiki/1589.fim-2010-mim-2016-management-agents-from-partners) have custom Extensible Connectivity (ECMA) [connectors](/en-us/previous-versions/windows/desktop/forefront-2010/hh859557%28v=vs.100%29) for use with Microsoft Identity Manager (MIM) 2016. Community members have also built ECMA connectors, hosted on their blogs and in public source code repositories. These same ECMA2 connectors can be used to provision into apps with the Microsoft Entra provisioning agent and Extensible Connectivity (ECMA) Connector host, without needing to deploy MIM sync. For more information, see [provisioning with the custom connectors](on-premises-custom-connector).

If you have been using a custom connector with MIM, then you can [export the MIM connector configuration](on-premises-migrate-microsoft-identity-manager) and import it into Microsoft Entra.

## How-to add partner-driven integrations to this document

If you've built a SCIM Gateway and would like to add it to this list, follow these steps:

1. To understand the Microsoft Entra SCIM implementation, review the Microsoft Entra SCIM [documentation](use-scim-to-provision-users-and-groups).
2. Test compatibility between the Microsoft Entra SCIM client and your SCIM gateway.
3. Navigate to the following [github repository](https://github.com/MicrosoftDocs/entra-docs/blob/main/docs/includes/application-integration-partners.md).
4. To start making changes, select the pencil at the top of the article.
5. Make changes in the article using the Markdown language and create a pull request. Make sure to provide a description for the pull request.
6. An admin of the repository reviews and merges your changes so that others can view them.

## Guidelines

- Add any new partners in alphabetical order.
- Limit your entries to 500 words.
- Ensure that you provide contact information for customers to learn more.
- To avoid duplication, only include applications that don't already have out of the box provisioning connectors in the [Microsoft Entra application gallery](../saas-apps/tutorial-list).

## Disclaimer

For independent software vendors: The Microsoft Entra Application Gallery Terms & Conditions, excluding Sections 2–4, apply to this Partner-Driven Integrations Catalog (the “Integrations Catalog”). References to the “Gallery” shall be read as the “Integrations Catalog” and references to an “App” shall be read as “Integration”.

If you don't agree with these terms, don't submit your Integration for listing in the Integrations Catalog. If you submit an Integration to the Integrations Catalog, you agree that you or the entity you represent (“YOU” or “YOUR”) agree to these terms.

Microsoft reserves the right to accept or reject your proposed Integration in its sole discretion and reserves the right to determine the manner in which Apps are presented, promoted, or featured in this Integrations Catalog.