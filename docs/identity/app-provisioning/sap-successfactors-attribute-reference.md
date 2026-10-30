---
layout: Conceptual
title: SAP SuccessFactors attribute reference for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/sap-successfactors-attribute-reference
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn which attributes from SuccessFactors are supported by SuccessFactors-HR driven provisioning in Microsoft Entra ID.
ms.topic: reference
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: chmutali
ai-usage: ai-assisted
locale: en-us
document_id: 116f43c3-a550-71a8-3298-61029d64dd0f
document_version_independent_id: a87ba746-361f-7f51-3106-6f41ccf44aee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/sap-successfactors-attribute-reference.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/sap-successfactors-attribute-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/sap-successfactors-attribute-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: d5583a05-37dd-807c-f568-d0b06d59d58f
---

# SAP SuccessFactors attribute reference for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you'll find information on:

- SuccessFactors entities and attributes
- Default attribute mapping

## Supported SuccessFactors entities and attributes

The table below captures the list of SuccessFactors attributes included by default in the following two provisioning apps:

- [SuccessFactors to Active Directory User Provisioning](../saas-apps/sap-successfactors-inbound-provisioning-tutorial)
- [SuccessFactors to Microsoft Entra user provisioning](../saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial)

Please refer to the [SAP SuccessFactors integration reference](sap-successfactors-integration-reference#retrieving-more-attributes) to extend the schema for additional attributes.

| # | SuccessFactors Entity | SuccessFactors Attribute | Operation Type |
| --- | --- | --- | --- |
| 1 | PerPerson | personIdExternal | Read |
| 2 | PerPerson | personId | Read |
| 3 | PerPerson | perPersonUuid | Read |
| 4 | PerPersonal | displayName | Read |
| 5 | PerPersonal | firstName | Read |
| 6 | PerPersonal | gender | Read |
| 7 | PerPersonal | lastName | Read |
| 8 | PerPersonal | middleName | Read |
| 9 | PerPersonal | preferredName | Read |
| 10 | User | addressLine1 | Read |
| 11 | User | addressLine2 | Read |
| 12 | User | addressLIne3 | Read |
| 13 | User | businessPhone | Read |
| 14 | User | cellPhone | Read |
| 15 | User | city | Read |
| 16 | User | country | Read |
| 17 | User | custom01 | Read |
| 18 | User | custom02 | Read |
| 19 | User | custom03 | Read |
| 20 | User | custom04 | Read |
| 21 | User | custom05 | Read |
| 22 | User | custom06 | Read |
| 23 | User | custom07 | Read |
| 24 | User | custom08 | Read |
| 25 | User | custom09 | Read |
| 26 | User | custom10 | Read |
| 27 | User | custom11 | Read |
| 28 | User | custom12 | Read |
| 29 | User | custom13 | Read |
| 30 | User | custom14 | Read |
| 31 | User | empId | Read |
| 32 | User | homePhone | Read |
| 33 | User | jobFamily | Read |
| 34 | User | nickname | Read |
| 35 | User | state | Read |
| 36 | User | timeZone | Read |
| 37 | User | username | Read |
| 38 | User | zipCode | Read |
| 39 | PerPhone | areaCode | Read |
| 40 | PerPhone | countryCode | Read |
| 41 | PerPhone | extension | Read |
| 42 | PerPhone | phoneNumber | Read |
| 43 | PerPhone | phoneType | Read |
| 44 | PerEmail | emailAddress | Read, Write |
| 45 | PerEmail | emailType | Read |
| 46 | EmpEmployment | firstDateWorked | Read |
| 47 | EmpEmployment | lastDateWorked | Read |
| 48 | EmpEmployment | userId | Read |
| 49 | EmpEmployment | isContingentWorker | Read |
| 50 | EmpJob | countryOfCompany | Read |
| 51 | EmpJob | emplStatus | Read |
| 52 | EmpJob | endDate | Read |
| 53 | EmpJob | startDate | Read |
| 54 | EmpJob | jobTitle | Read |
| 55 | EmpJob | position | Read |
| 65 | EmpJob | customString13 | Read |
| 56 | EmpJob | managerId | Read |
| 57 | EmpJob.BusinessUnit | businessUnit | Read |
| 58 | EmpJob.BusinessUnit | businessUnitId | Read |
| 59 | EmpJob.Company | company | Read |
| 60 | EmpJob.Company | companyId | Read |
| 61 | EmpJob.Company.CountryOfRegistration | twoCharCountryCode | Read |
| 62 | EmpJob.CostCenter | costCenter | Read |
| 63 | EmpJob.CostCenter | costCenterId | Read |
| 64 | EmpJob.CostCenter | costCenterDescription | Read |
| 65 | EmpJob.Department | department | Read |
| 66 | EmpJob.Department | departmentId | Read |
| 67 | EmpJob.Division | division | Read |
| 68 | EmpJob.Division | divisionId | Read |
| 69 | EmpJob.JobCode | jobCode | Read |
| 70 | EmpJob.JobCode | jobCodeId | Read |
| 71 | EmpJob.Location | LocationName | Read |
| 72 | EmpJob.Location | officeLocationAddress | Read |
| 73 | EmpJob.Location | officeLocationCity | Read |
| 74 | EmpJob.Location | officeLocationCustomString4 | Read |
| 75 | EmpJob.Location | officeLocationZipCode | Read |
| 76 | EmpJob.PayGrade | payGrade | Read |
| 77 | EmpEmploymentTermination | activeEmploymentsCount | Read |
| 78 | EmpEmploymentTermination | latestTerminationDate | Read |

## Default attribute mapping

The table below provides the default attribute mapping between SuccessFactors attributes listed above and Active Directory / Microsoft Entra attributes. In the Microsoft Entra provisioning app "Mapping" blade, you can modify this default mapping to include attributes from the list above.

| # | SuccessFactors Entity | SuccessFactors Attribute | Default attribute mapping | Processing Remark |
| --- | --- | --- | --- | --- |
| 1 | PerPerson | personIdExternal | employeeId | Used as matching attribute |
| 2 | PerPerson | perPersonUuid | [Not mapped - used as source anchor] | During initial sync, the Provisioning Service links the personUuid to existing objectGuid. |
| 3 | PerPersonal | displayName | displayName | NA |
| 4 | PerPersonal | firstName | givenName | NA |
| 5 | PerPersonal | lastName | sn | NA |
| 6 | User | addressLine1 | streetAddress | NA |
| 7 | User | city | l | NA |
| 8 | User | country | co | NA |
| 9 | User | state | st | NA |
| 10 | User | username | samAccountName | NA |
| 11 | User | zipCode | postalCode | NA |
| 12 | PerEmail | emailAddress | mail | NA |
| 13 | EmpJob | jobTitle | title | NA |
| 14 | EmpJob | managerId | manager | NA |
| 15 | EmpJob.Company.CountryOfRegistration | twoCharCountryCode | c | NA |
| 16 | EmpJob.Department | department | department | NA |
| 17 | EmpJob.Division | division | company | NA |
| 18 | EmpJob.Location | officeLocationAddress | streetAddress | NA |
| 19 | EmpJob.Location | officeLocationZipCode | postalCode | NA |
| 20 | EmpEmploymentTermination | activeEmploymentsCount | accountEnabled | if activeEmploymentsCount=0, disable the account. |