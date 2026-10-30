---
layout: Conceptual
title: First party app service principal reference table - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/reference-service-principal-table
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Reference table that maps application IDs to applications and their service principal usage from the sign-in logs.
ms.topic: reference
ms.date: 2025-05-06T00:00:00.0000000Z
ms.reviewer: egreenberg
locale: en-us
document_id: 73d3bc6a-9886-6cda-9db6-b46cf067da4e
document_version_independent_id: 73d3bc6a-9886-6cda-9db6-b46cf067da4e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/reference-service-principal-table.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/reference-service-principal-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/reference-service-principal-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 6a25b83b-c156-690f-0ca7-f0584b1a52a6
---

# First party app service principal reference table - Microsoft Entra ID | Microsoft Learn

The Microsoft service principal sign-in logs capture service-to-service authentication events for Microsoft services in your tenant. While not necessary for security investigations, the information can be useful for understanding how your services are interacting with each other.

## How to access the logs

These logs are only available by configuring diagnostic settings in Microsoft Entra to route the logs to an endpoint of your choice. For full guidance on this process, see [Configure diagnostic settings](howto-configure-diagnostic-settings).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Diagnostics**.
3. Adjust the filters accordingly.
4. Select **+ Add diagnostic setting**.
5. Select the **MicrosoftServicePrincipalSignInLogs**.
6. Select the destination and subscription from the dropdown menus that appear.
7. Select the **Save** button.

## Microsoft service principal sign-in logs

This table maps application IDs from the logs to the application name and a brief description of the application. This table is not exhaustive and will grow over time. Applications currently listed here illustrate the variety of applications that can be found in the logs.

Some application display names might include acronyms or abbreviations from previous application names. For example, some services still retain "AAD" (Azure Active Directory) in their display name, even though the service was rebranded to Microsoft Entra ID.

| Application display name | Application ID | Description |
| --- | --- | --- |
| AAD App Management | f0ae4899-d877-4d3c-ae25-679e38eea492 | Provides a single sign-on experience with access management to line of business applications, such as Salesforce or ServiceNow. |
| AAD Applications ARM RP | c8e14c19-0ae6-4966-bd07-17e5ffa8e4ce | Creates and manages first party and non-Microsoft apps in internal Microsoft Services and infrastructure tenants only.This app doesn't work outside of allowlisted tenants. |
| App Protection | c6e44401-4d0a-4542-ab22-ecd4c90d28d7 | Automatically disables applications based on user-defined and predefined policies.This app doesn't create app registrations or service principals in your tenant but can disable a service principal associated with a suspicious application. |
| Azure AD Application Proxy | 47ee738b-3f1a-4fc7-ab11-37e4822b007e | Provides ability to publish applications inside your private network and provides access to users outside your network.This app is used as part of workflows for both Microsoft Entra Private Access and Microsoft Entra Application Proxy. |
| Azure ESTS Service | fc03f97a-9db0-4627-a216-ec98ce54e018 | Standards compliant authentication service for Microsoft Entra. |
| Azure HDInsight Cluster API | fc03f97a-9db0-4627-a216-ec98ce54e018 | Big data analytics service that includes the Apache Hadoop and Apache Spark ecosystems, which enables the processing of massive amounts of data. |
| Azure Machine Learning | 0736f41a-0425-4b46-bdb5-1563eff02385 | Cloud service for accelerating and managing the machine learning project lifecycle. |
| Azure Security Insights | 98785600-1bb7-4fb9-b9fa-19afe2c8a360 | Cloud-native solution that provides Security Information and Event Management (SIEM) and Security Orchestration, Automation, and Response (SOAR) functionality. |
| Azure SQL Managed Instance to Azure AD Resource Provider | 913c6de4-2a4a-4a61-a9ce-945d2b2ce2e0 | Platform as a service (PaaS) that offers cloud-enhanced SQL Server within an isolated private virtual network environment. |
| Bot Framework Dev Portal | f3723d34-6ff5-4ceb-a148-d99dcd2511fc | Creates an app registration on behalf of the user when the Azure Bot Service (ABS) is asked to create a new app registration during the ABS resource creation process. |
| CPIM Service | bb2a2e3a-c5e7-4f0a-88e0-8e01fd3fc1f4 | The Customer and Partner Identity Management (CPIM) service provides a solution for customers to create user directories for external identities to authenticate to apps registered in their tenant.These external identity features can include social identity providers, such as Google or Facebook, self-service sign-up, and API connectors in the self-service sign-up flow. |
| Dynamics Lifecycle services | bb2a2e3a-c5e7-4f0a-88e0-8e01fd3fc1f4 | An Azure-based portal that provides a unifying, collaborative environment for customers and partners to manage the application lifecycle of their Microsoft Dynamics implementations. |
| Fabric Identity Management | c0be6b4c-212d-4ca9-8a35-fd260fe22342 | Creates and manages Fabric Workspace Identities. |
| MDATPNetworkScanAgent | 04687a56-4fc2-4e36-b274-b862fb649733 | Creates non-Microsoft apps within the customer tenant for each NetworkScan agent registered at customer sites. |
| Microsoft Rights Management Services | 00000012-0000-0000-c000-000000000000 | Also known as the Azure Rights Management Service, this app applies encryption via Purview labels and other encryption related tasks. |
| Microsoft Volume Licensing | 3ab9b3bc-762f-4d62-82f7-7e1d653ce29f | Commerce platform that supports the Microsoft Product and Services Agreement (MPSA), which is a transactional licensing agreement for commercial, government, and academic organizations with 250 or more users/devices. |
| Office 365 SharePoint Online | 00000003-0000-0ff1-ce00-000000000000 | This app represents the first-party instance of OneDrive and SharePoint apps. |
| Partner Customer Delegated Admin Migration | 39d63e7-7fa3-4b2b-94ea-ee256fdb8c2f | Granular Delegated Admin Privileges (GDAP) uses Extended Tools and Production (XTAP) to grant a partner's access to a customer tenant. |
| Power Virtual Agents Service9d8f559b-5984-46a4-902a-ad4271e83efa | 9d8f559b-5984-46a4-902a-ad4271e83efa9d8f559b-5984-46a4-902a-ad4271e83efa | Power Virtual Agents is the former name for Microsoft Copilot Studio. Both instances of this app allow the service to manage the applications and service principals created for each agent. |
| Storage Resource Provider | a6aa9161-5291-40bb-8c5c-923b567bee3b | Enables customers to manage storage accounts and keys programmatically. |
| SubstrateActionService | 06dd8193-75af-46d0-84bb-9b9bcaa89e8b | Assists non-Microsoft app developers to build customized MessageExtension apps like Poll and Survey for use in Microsoft Teams. |
| ZTNA Network Access Control Plane | 9d4afbbc-06a4-49e0-8005-4e5afd1d4fec | A feature of Global Secure Access, this app allows admins to control their network change's effect and try new features without affecting their onboarded environments. |