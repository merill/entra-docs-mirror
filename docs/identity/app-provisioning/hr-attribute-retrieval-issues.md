---
layout: Conceptual
title: Troubleshoot attribute retrieval issues with HR provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/hr-attribute-retrieval-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to troubleshoot attribute retrieval issues with HR provisioning
ms.topic: troubleshooting
ms.workload: identity
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: chmutali
locale: en-us
document_id: ccc92694-5444-27ec-5f33-06313b96447f
document_version_independent_id: bf92482e-7d9a-5c97-1cc1-aa10113ba417
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/hr-attribute-retrieval-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/hr-attribute-retrieval-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/hr-attribute-retrieval-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: ded10b36-c70d-e548-e43b-7bbcb4666017
---

# Troubleshoot attribute retrieval issues with HR provisioning - Microsoft Entra ID | Microsoft Learn

## Issue fetching Workday attributes

| **Applies to** |
| --- |
| \* Workday to on-premises Active Directory user provisioning  \* Workday to Microsoft Entra user provisioning |
| **Issue Description** |
| You configured the Workday inbound provisioning app and successfully connected to the Workday tenant URL. You ran a test sync and you observed that the provisioning app isn't retrieving certain attributes from Workday. Only some attributes are read and provisioned to the target. |
| **Probable Cause** |
| By default, the Workday provisioning app ships with attribute mapping and XPATH definitions that work with Workday Web Services (WWS) v21.1. When configuring connectivity to Workday in the provisioning app, if you explicitly specified the WWS API version (example: `https://wd3-impl-services1.workday.com/ccx/service/contoso4/Human_Resources/v34.0`), then you may run into this issue, because of the mismatch between WWS API version and the XPATH definitions. |
| **Resolution Options** |
| \* *Option 1*: Remove the WWS API version information from the URL and use the default WWS API version v21.1  \* *Option 2*: Manually update the XPATH API expressions so it's compatible with your preferred WWS API version. Update the **XPATH API expressions** under **Attribute Mapping -&gt; Advanced Options -&gt; Edit attribute list for Workday** referring to the section [Workday attribute reference](workday-attribute-reference#xpath-values-for-workday-web-services-wws-api-v30) |

## Issue fetching Workday calculated fields

| **Applies to** |
| --- |
| \* Workday to on-premises Active Directory user provisioning  \* Workday to Microsoft Entra user provisioning |
| **Issue Description** |
| You configured the Workday inbound provisioning app and successfully connected to the Workday tenant URL. You have an integration system configured in Workday and you have configured XPATHs that point to attributes in the Workday Integration System. However, the Microsoft Entra provisioning app isn't fetching values associated with these integration system attributes or calculated fields. |
| **Cause** |
| This is a known limitation. The Workday provisioning app currently doesn't support fetching calculated fields/integration system attributes using the *Field\_And\_Parameter\_Criteria\_Data* Get\_Workers request filter. This capability is also known as an Integration Field Override. |
| **Resolution Options** |
| Consider a workaround of either using Workday Provisioning groups or the Workday Custom ID field. |

**Suggested workarounds**

- **Option 1: Using Workday Provisioning Groups**: Check if the calculated field value can be represented as a provisioning group in Workday. Using the same logic that is used for the calculated field, your Workday Admin may be able to assign a Provisioning Group to the user. Reference Workday doc that requires Workday login: [Set Up Account Provisioning Groups](https://doc.workday.com/reader/3DMnG%7E27o049IYFWETFtTQ/keT9jI30zCzj4Nu9pJfGeQ). Once configured, this Provisioning Group assignment can be [retrieved in the provisioning job](workday-integration-reference#example-3-retrieving-provisioning-group-assignments) and used in attribute mappings and scoping filter.
- **Option 2: Using Workday Custom IDs**: Check if the calculated field value can be represented as a Custom ID on the Worker Profile. Use `Maintain Custom ID Type` task in Workday to define a new type and populate values in this custom ID. Make sure the [Workday ISU account used for the integration](../saas-apps/workday-inbound-tutorial#configuring-domain-security-policy-permissions) has domain security permission for `Person Data: ID Information`.
    - Example 1: Let's say you have a calculated field called Payroll ID. You can define "External\_Payroll\_ID" as a custom ID in Workday and retrieve it using an XPATH that uses "Custom\_ID\_Type\_ID" as the selecting mechanism: `wd:Worker/wd:Worker_Data/wd:Personal_Data/wd:Identification_Data/wd:Custom_ID/wd:Custom_ID_Data[string(wd:ID_Type_Reference/wd:ID[@wd:type='Custom_ID_Type_ID']='External_Payroll_ID']/wd:ID/text()`
    - Example 2: Let's say you have a calculated field called Badge ID. You can define "Badge ID" as a custom ID in Workday and retrieve the "Descriptor" attribute corresponding to it with an XPATH that uses "wd:ID\_Type\_Reference/@wd:Descriptor" as the selecting mechanism: `wd:Worker/wd:Worker_Data/wd:Personal_Data/wd:Identification_Data/wd:Custom_ID[string(wd:Custom_ID_Data/wd:ID_Type_Reference/@wd:Descriptor)='BADGE ID']/wd:Custom_ID_Reference/@wd:Descriptor`