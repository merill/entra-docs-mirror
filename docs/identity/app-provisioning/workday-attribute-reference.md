---
layout: Conceptual
title: Workday attribute reference for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/workday-attribute-reference
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn which attributes that you can fetch from Workday using XPATH queries in Microsoft Entra ID.
ms.topic: reference
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
locale: en-us
document_id: 27710bf3-6226-4d04-cd85-3bdd1fb44d3d
document_version_independent_id: b1ef7b4e-b539-4ff3-4c25-454d7e8c6836
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/workday-attribute-reference.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/workday-attribute-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/workday-attribute-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c175ef6a-1430-ec69-e587-377fa9989aa1
---

# Workday attribute reference for Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This section provides a list of attributes that you can fetch from Workday using XPATH queries. Based on the Workday Web Services API version, you plan to use, refer to the appropriate section.

## XPATH values for Workday Web Services (WWS) API v21.1

The table below captures the list of Workday attributes and corresponding XPATH expressions that are shipped out of the box with the Workday inbound provisioning app connector. These XPATH values are used *if no version information is specified in the connection URL or if the version is set to v21.1*.

![Screenshot of Workday no version info](../../includes/governance/media/workday-inbound-tutorial/workday-url-no-version-info.png)

| # | Workday Attribute Name | Workday XPATH API expression |
| --- | --- | --- |
| 1 | Active | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Active/text() |
| 2 | AddressLine2Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_2']/text() |
| 3 | AddressLine3Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_3']/text() |
| 4 | AddressLine4Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_4']/text() |
| 5 | AddressLine5Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_5']/text() |
| 6 | AddressLine6Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_6']/text() |
| 7 | AddressLine7Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_7']/text() |
| 8 | AddressLine8Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_8']/text() |
| 9 | AddressLine9Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_9']/text() |
| 10 | AddressLineData | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data/text() |
| 11 | BusinessTitle | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Title/text() |
| 12 | Company | wd:Worker/wd:Worker\_Data/wd:Organization\_Data/wd:Worker\_Organization\_Data[translate(string(wd:Organization\_Data/wd:Organization\_Type\_Reference/wd:ID[@wd:type='Organization\_Type\_ID']),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='COMPANY']/wd:Organization\_Reference/@wd:Descriptor |
| 13 | ContingentWorkerID | wd:Worker/wd:Worker\_Reference/wd:ID[@wd:type='Contingent\_Worker\_ID']/text() |
| 14 | CountryReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/wd:ID[@wd:type='ISO\_3166-1\_Alpha-3\_Code']/text() |
| 15 | CountryReferenceFriendly | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/@wd:Descriptor |
| 16 | CountryReferenceNumeric | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/wd:ID[@wd:type='ISO\_3166-1\_Numeric-3\_Code']/text() |
| 17 | CountryReferenceTwoLetter | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/wd:ID[@wd:type='ISO\_3166-1\_Alpha-2\_Code']/text() |
| 18 | CountryRegionReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Region\_Reference/@wd:Descriptor |
| 19 | EmailAddress | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Email\_Address\_Data[translate(string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='WORK']/wd:Email\_Address/text() |
| 20 | EmployeeID | wd:Worker/wd:Worker\_Reference/wd:ID[@wd:type='Employee\_ID']/text() |
| 21 | FacilityLocation | wd:Worker/wd:Worker\_Data/wd:Organization\_Data/wd:Worker\_Organization\_Data[translate(string(wd:Organization\_Data/wd:Organization\_Type\_Reference/wd:ID[@wd:type='Organization\_Type\_ID']),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='FACILITY']/wd:Organization\_Reference/@wd:Descriptor |
| 22 | Fax | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[translate(string(wd:Phone\_Device\_Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='FAX' and translate(string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='WORK']/@wd:Formatted\_Phone |
| 23 | FirstName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Legal\_Name\_Data/wd:Name\_Detail\_Data/wd:First\_Name/text() |
| 24 | JobClassificationID | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Job\_Classification\_Summary\_Data/wd:Job\_Classification\_Reference/wd:ID[@wd:type='Job\_Classification\_Reference\_ID']/text() |
| 25 | JobFamilyID | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Job\_Profile\_Summary\_Data/wd:Job\_Family\_Reference/wd:ID[@wd:type='Job\_Family\_ID']/text() |
| 26 | LastName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Legal\_Name\_Data/wd:Name\_Detail\_Data/wd:Last\_Name/text() |
| 27 | LeaveAbsenceType | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Leave\_Status\_Data[wd:On\_Leave='1']/wd:Leave\_of\_Absence\_Type\_Reference/wd:ID[@wd:type='Leave\_of\_Absence\_Type\_ID']/text() |
| 28 | LocalReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Local\_Reference/wd:ID[@wd:type='Locale\_ID']/text() |
| 29 | LocationIdentifier | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Location\_Reference/wd:ID[@wd:type='Location\_ID']/text() |
| 30 | ManagerReference | wd:Worker/wd:Worker\_Data/wd:Management\_Chain\_Data/wd:Worker\_Supervisory\_Management\_Chain\_Data[position()=1]/wd:Management\_Chain\_Data[last()=position()]/wd:Manager\_Reference/wd:ID[@wd:type='WID']/text() |
| 31 | MiddleName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Legal\_Name\_Data/wd:Name\_Detail\_Data/wd:Middle\_Name/text() |
| 32 | Mobile | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[translate(string(wd:Phone\_Device\_Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='MOBILE' and translate(string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='WORK']/@wd:Formatted\_Phone |
| 33 | Municipality | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Municipality/text() |
| 34 | PositionID | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Position\_ID/text() |
| 35 | PositionTitle | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Position\_Title/text() |
| 36 | PostalCode | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Postal\_Code/text() |
| 37 | PreferredFirstName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/wd:First\_Name/text() |
| 38 | PreferredLastName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/wd:Last\_Name/text() |
| 39 | PreferredMiddleName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/wd:Middle\_Name/text() |
| 40 | PreferredNameData | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/@wd:Formatted\_Name |
| 41 | PrimaryWorkTelephone | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[wd:Usage\_Data/wd:Type\_Data/@wd:Primary='1' and translate(string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='WORK']/@wd:Formatted\_Phone |
| 42 | StatusAcademisTenureDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Academic\_Tenure\_Date/text() |
| 43 | StatusActiveStatusDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Active\_Status\_Date/text() |
| 44 | StatusBenefitsServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Benefits\_Service\_Date/text() |
| 45 | StatusCompanyServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Company\_Service\_Date/text() |
| 46 | StatusContinuousFirstDayOfWork | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:First\_Day\_of\_Work/text() |
| 47 | StatusContinuousServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Continuous\_Service\_Date/text() |
| 48 | StatusDateEnteredWorkforce | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Date\_Entered\_Workforce/text() |
| 49 | StatusDaysUnemployed | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Days\_Unemployed/text() |
| 50 | StatusEndEmploymentDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:End\_Employment\_Date/text() |
| 51 | StatusExpectedRetirementDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Expected\_Retirement\_Date/text() |
| 52 | StatusHireDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Hire\_Date/text() |
| 53 | StatusMonthsContinuousPriorEmployment | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Months\_Continuous\_Prior\_Employment/text() |
| 54 | StatusNotEligibleForHire | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Not\_Eligible\_For\_Hire/text() |
| 55 | StatusNotEligibleForRehire | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Not\_Eligible\_for\_Rehire/text() |
| 56 | StatusOriginalHireDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Original\_Hire\_Date/text() |
| 57 | StatusProbationEndDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Probation\_End\_Date/text() |
| 58 | StatusProbationStartDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Probation\_Start\_Date/text() |
| 59 | StatusRegrettableTermination | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Regrettable\_Termination/text() |
| 60 | StatusRehire | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Rehire/text() |
| 61 | StatusResignationDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Resignation\_Date/text() |
| 62 | StatusRetired | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Retired/text() |
| 63 | StatusRetirementDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Retirement\_Date/text() |
| 64 | StatusRetirementEligibilityDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Retirement\_Eligibility\_Date/text() |
| 65 | StatusSeniorityDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Seniority\_Date/text() |
| 66 | StatusSeveranceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Severance\_Date/text() |
| 67 | StatusTerminated | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Terminated/text() |
| 68 | StatusTerminationDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Termination\_Date/text() |
| 69 | StatusTerminationInvoluntary | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Termination\_Involuntary/text() |
| 70 | StatusTerminationLastDayOfWork | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Termination\_Last\_Day\_of\_Work/text() |
| 71 | StatusTimeOffServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Time\_Off\_Service\_Date/text() |
| 72 | StatusVestingDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Vesting\_Date/text() |
| 73 | SupervisoryOrganization | wd:Worker/wd:Worker\_Data/wd:Organization\_Data/wd:Worker\_Organization\_Data/wd:Organization\_Data[translate(string(wd:Organization\_Type\_Reference/wd:ID[@wd:type='Organization\_Type\_ID']),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='SUPERVISORY']/wd:Organization\_Name/text() |
| 74 | Telephone | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[translate(string(wd:Phone\_Device\_Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='TELEPHONE' and translate(string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/@wd:Descriptor),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='WORK']/@wd:Formatted\_Phone |
| 75 | TransactionLogData | wd:Worker/wd:Worker\_Data/wd:Transaction\_Log\_Entry\_Data/wd:Transaction\_Log\_Entry |
| 76 | UserID | wd:Worker/wd:Worker\_Data/wd:User\_ID/text() |
| 77 | WID | wd:Worker/wd:Worker\_Reference/wd:ID[@wd:type='WID']/text() |
| 78 | WorkerID | wd:Worker/wd:Worker\_Data/wd:Worker\_ID/text() |
| 79 | WorkerType | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Worker\_Type\_Reference/@wd:Descriptor |
| 80 | WorkSpaceReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Position\_Data/wd:Work\_Space\_\_Reference/@wd:Descriptor |

## XPATH values for Workday Web Services (WWS) API v30+

If you are using WWS API v30.0 or above in the connection URL as shown below:

![Screenshot of Workday version info](../../includes/governance/media/workday-inbound-tutorial/workday-url-version-info.png)

...then before turning on the provisioning job, please update the **XPATH API expressions** under **Attribute Mapping -&gt; Advanced Options -&gt; Edit attribute list for Workday** to use the values listed in the table.

To configure additional XPATHs, refer to the section [Tutorial: Managing your configuration](../saas-apps/workday-inbound-tutorial#managing-your-configuration).

| # | Workday Attribute Name | Workday XPATH API expression |
| --- | --- | --- |
| 1 | Active | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Active/text() |
| 2 | AddressLine2Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_2']/text() |
| 3 | AddressLine3Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_3']/text() |
| 4 | AddressLine4Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_4']/text() |
| 5 | AddressLine5Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_5']/text() |
| 6 | AddressLine6Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_6']/text() |
| 7 | AddressLine7Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_7']/text() |
| 8 | AddressLine8Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_8']/text() |
| 9 | AddressLine9Data | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data[@wd:Type='ADDRESS\_LINE\_9']/text() |
| 10 | AddressLineData | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Address\_Line\_Data/text() |
| 11 | BusinessTitle | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Title/text() |
| 12 | Company | wd:Worker/wd:Worker\_Data/wd:Organization\_Data/wd:Worker\_Organization\_Data[translate(string(wd:Organization\_Data/wd:Organization\_Type\_Reference/wd:ID[@wd:type='Organization\_Type\_ID']),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='COMPANY']/wd:Organization\_Data/wd:Organization\_Name/text() |
| 13 | ContingentWorkerID | wd:Worker/wd:Worker\_Reference/wd:ID[@wd:type='Contingent\_Worker\_ID']/text() |
| 14 | CountryReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/wd:ID[@wd:type='ISO\_3166-1\_Alpha-3\_Code']/text() |
| 15 | CountryReferenceFriendly | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/@wd:Descriptor |
| 16 | CountryReferenceNumeric | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/wd:ID[@wd:type='ISO\_3166-1\_Numeric-3\_Code']/text() |
| 17 | CountryReferenceTwoLetter | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Reference/wd:ID[@wd:type='ISO\_3166-1\_Alpha-2\_Code']/text() |
| 18 | CountryRegionReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Country\_Region\_Descriptor/text() |
| 19 | EmailAddress | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Email\_Address\_Data[wd:Usage\_Data/@wd:Public='1' and string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/wd:ID[@wd:type='Communication\_Usage\_Type\_ID'])='WORK']/wd:Email\_Address/text() |
| 20 | EmployeeID | wd:Worker/wd:Worker\_Reference/wd:ID[@wd:type='Employee\_ID']/text() |
| 21 | FacilityLocation | wd:Worker/wd:Worker\_Data/wd:Organization\_Data/wd:Worker\_Organization\_Data/wd:Organization\_Data[translate(string(wd:Organization\_Type\_Reference/wd:ID[@wd:type='Organization\_Type\_ID']),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='LOCATION\_HIERARCHY']/wd:Organization\_Name/text() |
| 22 | Fax | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[wd:Usage\_Data/@wd:Public='1' and string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/wd:ID[@wd:type='Communication\_Usage\_Type\_ID'])='WORK' and string(wd:Phone\_Device\_Type\_Reference/wd:ID[@wd:type='Phone\_Device\_Type\_ID'])='Fax']/@wd:Workday\_Traditional\_Formatted\_Phone |
| 23 | FirstName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Legal\_Name\_Data/wd:Name\_Detail\_Data/wd:First\_Name/text() |
| 24 | JobClassificationID | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Job\_Classification\_Summary\_Data/wd:Job\_Classification\_Reference/wd:ID[@wd:type='Job\_Classification\_Reference\_ID']/text() |
| 25 | JobFamilyID | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Job\_Profile\_Summary\_Data/wd:Job\_Family\_Reference/wd:ID[@wd:type='Job\_Family\_ID']/text() |
| 26 | LastName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Legal\_Name\_Data/wd:Name\_Detail\_Data/wd:Last\_Name/text() |
| 27 | LeaveAbsenceType | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Leave\_Status\_Data[wd:On\_Leave='1']/wd:Leave\_of\_Absence\_Type\_Reference/wd:ID[@wd:type='Leave\_of\_Absence\_Type\_ID']/text() |
| 28 | LocalReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Local\_Reference/wd:ID[@wd:type='Locale\_ID']/text() |
| 29 | LocationIdentifier | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Location\_Reference/wd:ID[@wd:type='Location\_ID']/text() |
| 30 | ManagerReference | wd:Worker/wd:Worker\_Data/wd:Management\_Chain\_Data/wd:Worker\_Supervisory\_Management\_Chain\_Data[position()=1]/wd:Management\_Chain\_Data[last()=position()]/wd:Manager\_Reference/wd:ID[@wd:type='WID']/text() |
| 31 | MiddleName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Legal\_Name\_Data/wd:Name\_Detail\_Data/wd:Middle\_Name/text() |
| 32 | Mobile | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[wd:Usage\_Data/@wd:Public='1' and string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/wd:ID[@wd:type='Communication\_Usage\_Type\_ID'])='WORK' and string(wd:Phone\_Device\_Type\_Reference/wd:ID[@wd:type='Phone\_Device\_Type\_ID'])='Mobile']/@wd:Workday\_Traditional\_Formatted\_Phone |
| 33 | Municipality | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Municipality/text() |
| 34 | PositionID | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Position\_ID/text() |
| 35 | PositionTitle | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Position\_Title/text() |
| 36 | PostalCode | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Business\_Site\_Summary\_Data/wd:Address\_Data/wd:Postal\_Code/text() |
| 37 | PreferredFirstName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/wd:First\_Name/text() |
| 38 | PreferredLastName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/wd:Last\_Name/text() |
| 39 | PreferredMiddleName | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/wd:Middle\_Name/text() |
| 40 | PreferredNameData | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Name\_Data/wd:Preferred\_Name\_Data/wd:Name\_Detail\_Data/@wd:Formatted\_Name |
| 41 | PrimaryWorkTelephone | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[wd:Usage\_Data/@wd:Public='1' and string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/wd:ID[@wd:type='Communication\_Usage\_Type\_ID'])='WORK' and string(wd:Phone\_Device\_Type\_Reference/wd:ID[@wd:type='Phone\_Device\_Type\_ID'])='Landline']/@wd:Workday\_Traditional\_Formatted\_Phone |
| 42 | StatusAcademisTenureDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Academic\_Tenure\_Date/text() |
| 43 | StatusActiveStatusDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Active\_Status\_Date/text() |
| 44 | StatusBenefitsServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Benefits\_Service\_Date/text() |
| 45 | StatusCompanyServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Company\_Service\_Date/text() |
| 46 | StatusContinuousFirstDayOfWork | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:First\_Day\_of\_Work/text() |
| 47 | StatusContinuousServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Continuous\_Service\_Date/text() |
| 48 | StatusDateEnteredWorkforce | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Date\_Entered\_Workforce/text() |
| 49 | StatusDaysUnemployed | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Days\_Unemployed/text() |
| 50 | StatusEndEmploymentDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:End\_Employment\_Date/text() |
| 51 | StatusExpectedRetirementDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Expected\_Retirement\_Date/text() |
| 52 | StatusHireDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Hire\_Date/text() |
| 53 | StatusMonthsContinuousPriorEmployment | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Months\_Continuous\_Prior\_Employment/text() |
| 54 | StatusNotEligibleForHire | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Not\_Eligible\_For\_Hire/text() |
| 55 | StatusNotEligibleForRehire | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Not\_Eligible\_for\_Rehire/text() |
| 56 | StatusOriginalHireDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Original\_Hire\_Date/text() |
| 57 | StatusProbationEndDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Probation\_End\_Date/text() |
| 58 | StatusProbationStartDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Probation\_Start\_Date/text() |
| 59 | StatusRegrettableTermination | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Regrettable\_Termination/text() |
| 60 | StatusRehire | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Rehire/text() |
| 61 | StatusResignationDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Resignation\_Date/text() |
| 62 | StatusRetired | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Retired/text() |
| 63 | StatusRetirementDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Retirement\_Date/text() |
| 64 | StatusRetirementEligibilityDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Retirement\_Eligibility\_Date/text() |
| 65 | StatusSeniorityDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Seniority\_Date/text() |
| 66 | StatusSeveranceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Severance\_Date/text() |
| 67 | StatusTerminated | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Terminated/text() |
| 68 | StatusTerminationDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Termination\_Date/text() |
| 69 | StatusTerminationInvoluntary | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Termination\_Involuntary/text() |
| 70 | StatusTerminationLastDayOfWork | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Termination\_Last\_Day\_of\_Work/text() |
| 71 | StatusTimeOffServiceDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Time\_Off\_Service\_Date/text() |
| 72 | StatusVestingDate | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Vesting\_Date/text() |
| 73 | SupervisoryOrganization | wd:Worker/wd:Worker\_Data/wd:Organization\_Data/wd:Worker\_Organization\_Data/wd:Organization\_Data[translate(string(wd:Organization\_Type\_Reference/wd:ID[@wd:type='Organization\_Type\_ID']),'abcdefghijklmnopqrstuvwxyz','ABCDEFGHIJKLMNOPQRSTUVWXYZ')='SUPERVISORY']/wd:Organization\_Name/text() |
| 74 | Telephone | wd:Worker/wd:Worker\_Data/wd:Personal\_Data/wd:Contact\_Data/wd:Phone\_Data[wd:Usage\_Data/@wd:Public='1' and string(wd:Usage\_Data/wd:Type\_Data/wd:Type\_Reference/wd:ID[@wd:type='Communication\_Usage\_Type\_ID'])='WORK' and string(wd:Phone\_Device\_Type\_Reference/wd:ID[@wd:type='Phone\_Device\_Type\_ID'])='Landline']/@wd:Workday\_Traditional\_Formatted\_Phone |
| 75 | TransactionLogData | wd:Worker/wd:Worker\_Data/wd:Transaction\_Log\_Entry\_Data/wd:Transaction\_Log\_Entry |
| 76 | UserID | wd:Worker/wd:Worker\_Data/wd:User\_ID/text() |
| 77 | WID | wd:Worker/wd:Worker\_Reference/wd:ID[@wd:type='WID']/text() |
| 78 | WorkerID | wd:Worker/wd:Worker\_Data/wd:Worker\_ID/text() |
| 79 | WorkerType | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Worker\_Type\_Reference[wd:ID/@wd:type="Contingent\_Worker\_Type\_ID" or wd:ID/@wd:type="Employee\_Type\_ID"]/@wd:Descriptor |
| 80 | WorkSpaceReference | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Work\_Space\_\_Reference/@wd:Descriptor |

## Custom XPATH values

The table below provides a list of other commonly used custom XPATH API expressions when provisioning workers from Workday to Active Directory or Microsoft Entra ID. Please test the XPATH API expressions provided here with your version of Workday referring to the instructions captured in the section [Tutorial: Managing your configuration](../saas-apps/workday-inbound-tutorial#managing-your-configuration).

To add more attributes to the XPATH table for the benefit of customers implementing this integration, please leave a comment below or directly [contribute](/en-us/contribute/) to the article.

| # | Workday Attribute Name | Workday API version | Workday XPATH API expression |
| --- | --- | --- | --- |
| 1 | Universal ID | v30.0+ | wd:Worker/wd:Worker\_Data/wd:Universal\_ID/text() |
| 2 | User Name | v30.0+ | wd:Worker/wd:Worker\_Data/wd:User\_Account\_Data/wd:User\_Name/text() |
| 3 | Management Level ID | v30.0+ | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Job\_Data[@wd:Primary\_Job=1]/wd:Position\_Data/wd:Job\_Profile\_Summary\_Data/wd:Management\_Level\_Reference/wd:ID[@wd:type="Management\_Level\_ID"]/text() |
| 4 | Hire Rescinded | v30.0+ | wd:Worker/wd:Worker\_Data/wd:Employment\_Data/wd:Worker\_Status\_Data/wd:Hire\_Rescinded/text() |
| 5 | Assigned Provisioning Group | v21.1+ | wd:Worker/wd:Worker\_Data/wd:Account\_Provisioning\_Data/wd:Provisioning\_Group\_Assignment\_Data[wd:Status='Assigned']/wd:Provisioning\_Group/text() |

## Supported XPATH functions

Given below is the list of XPATH functions supported by [Microsoft .NET XPATH library](/en-us/previous-versions/dotnet/netframework-4.0/ms256138%28v=vs.100%29) that you can use while creating your XPATH API expression.

- name
- last
- position
- string
- substring
- concat
- substring-after
- starts-with
- string-length
- contains
- translate
- normalize-space
- substring-before
- boolean
- true
- not
- false
- number
- ceiling
- sum
- round
- floor