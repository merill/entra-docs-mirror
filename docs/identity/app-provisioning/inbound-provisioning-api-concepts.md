---
layout: Conceptual
title: API-driven inbound provisioning concepts - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/inbound-provisioning-api-concepts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: An overview of API-driven inbound provisioning.
ms.topic: reference
ms.date: 2025-07-24T00:00:00.0000000Z
ms.reviewer: chmutali
locale: en-us
document_id: c59649a5-9bb8-c8be-34d4-c458fdf466f2
document_version_independent_id: 71da6c2b-ccbd-6278-34fc-59827dfac5a3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/inbound-provisioning-api-concepts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/inbound-provisioning-api-concepts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/inbound-provisioning-api-concepts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 1d6029c8-0c87-6ef5-1c7b-79ab45011f25
---

# API-driven inbound provisioning concepts - Microsoft Entra ID | Microsoft Learn

This document provides a conceptual overview of the Microsoft Entra API-driven inbound user provisioning.

## Introduction

Today enterprises have various authoritative systems of record. To establish end-to-end identity lifecycle, strengthen security posture and stay compliant with regulations, identity data in Microsoft Entra ID must be kept in sync with workforce data managed in these systems of record. The *system of record* could be an HR app, a payroll app, a spreadsheet, or SQL tables in a database hosted either on-premises or in the cloud.

With API-driven inbound provisioning, the Microsoft Entra provisioning service now supports integration with *any* system of record. Customers and partners can use *any* automation tool of their choice to retrieve workforce data from the system of record and ingest it into Microsoft Entra ID. The IT admin has full control on how the data is processed and transformed with attribute mappings. Once the workforce data is available in Microsoft Entra ID, the IT admin can configure appropriate joiner-mover-leaver business processes using [Lifecycle Workflows](../../id-governance/what-are-lifecycle-workflows).

## Supported scenarios

Several inbound user provisioning scenarios are enabled using API-driven inbound provisioning. This diagram demonstrates the most common scenarios.

[![Diagram showing API workflow scenarios.](media/inbound-provisioning-api-concepts/api-workflow-scenarios.png)](media/inbound-provisioning-api-concepts/api-workflow-scenarios.png#lightbox)

### Scenario 1: Enable IT teams to import HR data extracts using any automation tool

Flat files, CSV files and SQL staging tables are commonly used in enterprise integration scenarios. Employee, contractor, and vendor information are periodically exported into one of these formats and an automation tool is used to sync this data with enterprise identity directories. With API-driven inbound provisioning, IT teams can use any automation tool of their choice (example: PowerShell scripts or Azure Logic Apps) to modernize and simplify this integration.

### Scenario 2: Enable ISVs to build direct integration with Microsoft Entra ID

With API-driven inbound provisioning, HR ISVs can ship native synchronization experiences so that changes in the HR system automatically flow into Microsoft Entra ID and connected on-premises Active Directory domains. For example, an HR app or student information systems app can send data to Microsoft Entra ID as soon as a transaction is complete or as end-of-day bulk update.

### Scenario 3: Enable system integrators to build more connectors to systems of record

Partners can build custom HR connectors to meet different integration requirements around data flow from systems of record to Microsoft Entra ID.

In all of the above scenarios, integration is simplified as the Microsoft Entra provisioning service takes over the responsibility of performing identity profile comparison, restricting the data sync to scoping logic configured by the IT admin, and executing rule-based attribute flow and transformation managed in the Microsoft Entra admin center.

## End-to-end flow

[![Diagram of the end-to-end workflow of inbound provisioning.](media/inbound-provisioning-api-concepts/end-to-end-workflow.png)](media/inbound-provisioning-api-concepts/end-to-end-workflow.png#lightbox)

### Steps of the workflow

1. IT Admin configures [an API-driven inbound user provisioning app](inbound-provisioning-api-configure-app) from the Microsoft Entra Enterprise App gallery.
2. IT Admin [grants access permissions](inbound-provisioning-api-grant-access) and provides endpoint access details to the API developer/partner/system integrator.
3. The API developer/partner/system integrator builds an API client to send authoritative identity data to Microsoft Entra ID.
4. The API client reads identity data from the authoritative source.
5. The API client sends a POST request to provisioning [/bulkUpload](/en-us/graph/api/synchronization-synchronizationjob-post-bulkupload) API endpoint associated with the provisioning app. 
    Note

    The API client doesn't need to perform any comparisons between the source attributes and the target attribute values to determine what operation (create/update/enable/disable) to invoke. This is automatically handled by the provisioning service. The API client simply uploads the identity data read from the source system by packaging it as bulk request using SCIM schema constructs.
6. If successful, an `Accepted 202 Status` is returned.
7. The Microsoft Entra provisioning service processes the data received, applies the attribute mapping rules, and completes user provisioning.
8. Depending on the provisioning app that's configured, the user is provisioned either into on-premises Active Directory (for hybrid users) or Microsoft Entra ID (for cloud-only users).
9. The API Client then queries the provisioning logs API endpoint for the status of each record sent.
10. If the processing of any record fails, the API client can check the error details and include records corresponding to the failed operations in the next bulk request (step 5).
11. At any time, the IT Admin can check the status of the provisioning job and view events in the provisioning logs.

### Key features of API-driven inbound user provisioning

- Available as a provisioning app that exposes an *asynchronous* Microsoft Graph provisioning [/bulkUpload](/en-us/graph/api/synchronization-synchronizationjob-post-bulkupload) API endpoint accessed using valid OAuth token.
- Tenant admins must grant API clients interacting with this provisioning app the Graph permissions `SynchronizationData-User.Upload`, `SynchronizationData-User.Upload.OwnedBy` (for ISVs), and `ProvisioningLog.Read.All`.
- The Graph API endpoint accepts valid bulk request payloads using SCIM schema constructs.
- With SCIM schema extensions, you can send any attribute in the bulk request payload.
- You can configure provisioning to [clear attribute values (Preview)](clear-attribute-values) when the request payload includes null or empty values.
- Include a complete user record in every bulk request, for both full and delta sync. When [clear attribute values (Preview)](clear-attribute-values) is enabled, null or empty values for mapped attributes will clear the corresponding values in the target system. The clearing can also happen if you omit an attribute for which null flow is enabled. An incomplete payload might therefore unintentionally clear existing attribute values. Use an explicit JSON `null` or empty string to perform deterministic clearing.
- The `/bulkUpload`API endpoint enforces the following throttling limits:
    - There is a limit of 40 API calls within any 5-second window. If this threshold is exceeded, the service returns an HTTP 429 (Too Many Requests) response. To avoid throttling, implement pacing logic in the client to space out requests - such as adding delays or rate-limit handling between submissions.
    - There is a tenant-level limit of 2,000 API calls per 24-hour period under the Entra ID P1/P2 license, and 6,000 API calls under the Entra ID Governance license. Exceeding these limits results in an HTTP 429 (Too Many Requests) response. To stay within the quota, ensure that your SCIM bulk payloads are optimized to include up to 50 operations per API call.
- Each API endpoint is associated with a specific provisioning app in Microsoft Entra ID. You can integrate multiple data sources by creating a provisioning app for each data source.
- Incoming bulk request payloads are processed in near real-time.
- Admins can check provisioning progress by viewing the [provisioning logs](../monitoring-health/concept-provisioning-logs).
- API clients can track progress by querying [provisioning logs API](/en-us/graph/api/resources/provisioningobjectsummary).

### License requirements

This feature is available with Microsoft Entra ID P1, P2, and Microsoft Entra ID Governance licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals.](https://go.microsoft.com/fwlink/?linkid=2262973)

### API usage guidance

The `/bulkUpload` API endpoint expands the number of ways that you can manage users in Microsoft Entra ID. To help you determine if the `/bulkUpload` API endpoint is right for your integration scenario, refer to this table that compares it with other API-based integration options.

| Use Case Scenario to API mapping | User creation API | HR inbound bulk API | User invitation API | Direct assignment API |
| --- | --- | --- | --- | --- |
| *When your identity creation scenario is...* | Ad-hoc user creation in Microsoft Entra ID for a user not associated with any worker in an HR source | Sourcing employee records from an authoritative HR source, and you want those employees to have "member" accounts in Microsoft Entra ID or on-premises Active Directory | Ad-hoc guest user creation in Microsoft Entra ID, for sharing purposes, where the guest has unique access rights | Access assignment for existing users, and (preview) guest creation in Microsoft Entra ID, to give the new guest standardized access |
| *...use the API...* | [Create user](https://go.microsoft.com/fwlink/?linkid=2261811) | [Perform bulkUpload](https://go.microsoft.com/fwlink/?linkid=2261471). | [Create invitation](https://go.microsoft.com/fwlink/?linkid=2261635) | [Create accessPackageAssignmentRequest](/en-us/graph/api/entitlementmanagement-post-assignmentrequests?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) |
| *The resulting user is first created in...* | Microsoft Entra ID | On-premises Active Directory or Microsoft Entra ID | Microsoft Entra ID | Microsoft Entra ID |
| *The resulting user authenticates to...* | Microsoft Entra ID, with the password you supply | On-premises Active Directory of Microsoft Entra ID, with a [Temporary Access Pass provided by Entra Lifecycle workflows](https://go.microsoft.com/fwlink/?linkid=2261542) | Home tenant or other identity provider | Home tenant or other identity provider |
| *Subsequent updates to the user can be done via* | Graph API or Microsoft Entra admin center | Graph API or HR inbound bulk API or Microsoft Entra admin center | Graph API or Microsoft Entra admin center | Graph API or Microsoft Entra admin center |
| *The lifecycle of user when their employment starts, is determined by...* | Manual processes | [Entra onboarding Lifecycle workflows](../../id-governance/tutorial-onboard-custom-workflow-portal) that trigger based on the `employeeHireDate` attribute | Entitlement management | [Automatic assignment](../../id-governance/entitlement-management-access-package-auto-assignment-policy) using Entitlement management access packages |
| *The lifecycle of user when their employment is terminated is determined by...* | Manual processes | [Entra offboarding lifecycle workflows](../../id-governance/tutorial-scheduled-leaver-portal) that trigger based on the `employeeLeaveDateTime` attribute | Access reviews | Entitlement management when the user loses their last access package assignment, they're removed |

### Recommended learning path

| # | Learning objective | Guidance |
| --- | --- | --- |
| 1. | You want to learn more about the inbound provisioning API specs. | Refer to [/bulkUpload](/en-us/graph/api/synchronization-synchronizationjob-post-bulkupload) API spec document. |
| 2. | You want to get more familiar with the API-driven provisioning concepts, scenarios and limitations. | Refer to [Frequently asked questions about API-driven inbound provisioning](inbound-provisioning-api-faqs). |
| 3. | As an *Admin user*, you want to quickly test the inbound provisioning API. | \* Create [API-driven inbound provisioning app](inbound-provisioning-api-configure-app) \* [Test API using Graph Explorer](inbound-provisioning-api-graph-explorer) |
| 4. | With a service account or managed identity, you want to quickly test the inbound provisioning API. | \* Create [API-driven inbound provisioning app](inbound-provisioning-api-configure-app) \* Grant [API permissions](inbound-provisioning-api-grant-access) \* [Test API using cURL](inbound-provisioning-api-curl-tutorial) |
| 5. | You want to extend the API-driven provisioning app to process more custom attributes. | Refer to the tutorial [Extend API-driven provisioning to sync custom attributes](inbound-provisioning-api-custom-attributes) |
| 6. | You want to clear existing target attributes when the source no longer has a value. | Refer to [Clear attribute values (Preview)](clear-attribute-values). |
| 7. | You want to automate data upload from your system of record to the inbound provisioning API endpoint. | Refer to the tutorials  \* [Quick start with PowerShell](inbound-provisioning-api-powershell) \* [Quick start with Azure Logic Apps](inbound-provisioning-api-logic-apps) |
| 8. | You want to troubleshoot inbound provisioning API issues. | Refer to the [Troubleshooting guide](inbound-provisioning-api-issues). |

### External learning resources

The following content, created by our partners and Microsoft MVPs, offers extra guidance on how to deploy and configure API-driven provisioning for various integration scenarios.

- Video tutorials

    - John Savill explains [how API-driven provisioning works](https://www.youtube.com/watch?v=olkOYEyJB1o)
    - Microsoft MVP Nick Ross explains [how to configure API-driven provisioning](https://www.youtube.com/watch?v=4FLEroQ8zmQ)
    - Microsoft MVP Nick Ross explains [how to source HR data from an Excel file in SharePoint using Power Automate and API-driven provisioning](https://www.youtube.com/watch?v=QN6SsamvS9c)
    - Microsoft partner [IdentityXP 4-part series on API-driven provisioning](https://www.youtube.com/watch?v=7ZPDnhwKz_w)
- Blog posts, presentations, and other useful links

    - Microsoft MVP Christian Frohn explains how to [use API-driven provisioning with Azure SQL database as source of truth](https://www.christianfrohn.dk/2024/05/15/using-api-driven-user-provisioning-with-an-azure-sql-database-as-source-of-truth/)
    - Microsoft MVP Pim Jacob's article explaining [how to perform Bamboo HR API-driven provisioning to on-premises Active Directory](https://identity-man.eu/2023/10/25/using-the-brand-new-entra-inbound-provisioning-api-for-identity-lifecycle-management/)
    - Microsoft MVP Pim Jacob's presentation on [how to configure the joiner and leaver process using API-driven provisioning and lifecycle workflows](https://github.com/IdentityMan/presentations/blob/main/DutchMicrosoftSecurityMeetup/Dutch%20SecMeetup%20-%20Securing%20Joiner%20&amp;%20Leaver%20process%20with%20Inbound%20Provisioning%20and%20LCW.pdf)
    - Microsoft MVP Marius Solbakken's article explaining [how to source Excel data using PowerShell script and API-driven provisioning](https://goodworkaround.com/2023/08/01/testing-out-the-entra-id-inbound-provisioning-api/)
    - Suryendu Bhattacharyya's article on [how to invoke API-driving provisioning using custom GitHub Action](https://suryendub.github.io/2023-11-25-github-action-for-inbound-api-provisioning/)
    - Microsoft MVP Jan Vidar Elven's [Bicep template for API-driven provisioning](https://github.com/JanVidarElven/ExpertsLiveEurope2023/tree/main/EntraIDGovernance/Elven%20Inbound%20Provisioning%20API)