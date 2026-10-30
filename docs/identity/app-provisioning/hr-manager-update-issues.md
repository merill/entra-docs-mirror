---
layout: Conceptual
title: Troubleshoot manager update issues with HR provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/hr-manager-update-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: This article provides potential issues and resolutions that show you how to troubleshoot manager update issues with HR provisioning
ms.date: 2025-03-04T00:00:00.0000000Z
ms.topic: troubleshooting
ms.reviewer: chmutali
locale: en-us
document_id: 48e8805a-4f45-62bd-b87d-e32dcffdeebf
document_version_independent_id: 52deee82-b3ba-2dbc-097e-1e3c51d8b98f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/hr-manager-update-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/hr-manager-update-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/hr-manager-update-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 28039f8c-c5ae-2521-ec29-76cee3f9501a
---

# Troubleshoot manager update issues with HR provisioning - Microsoft Entra ID | Microsoft Learn

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning
- SAP SuccessFactors to on-premises Active Directory user provisioning
- SAP SuccessFactors to Microsoft Entra user provisioning

## Understanding how manager reference resolution works

The Microsoft Entra provisioning service automatically updates manager information so that the user-manager relationship in Microsoft Entra ID is always in sync with your HR data. It uses a process called *manager reference resolution* to accurately update the *manager* attribute. Before going into the process details, it's important to understand how manager information is stored in Microsoft Entra ID and on-premises Active Directory.

- In **on-premises Active Directory**, the *manager* attribute stores the *distinguishedName (dn)* of the manager's account in AD.
- In **Microsoft Entra ID**, the *manager* attribute is a DirectoryObject navigation property in Microsoft Entra ID. When you view the user record in the Microsoft Entra admin center, it shows the *displayName* of the manager record in Microsoft Entra ID.

The *manager reference resolution* is a two-step process:

- Step 1: Link the manager's HR source record with the manager's target account record using a pair of attributes referred to as *source anchor* and *target anchor*.
- Step 2: Use the manager reference attributes defined in the schema to update the manager attribute in the target in the required format.

The default anchor attributes and reference attributes for each app are:

| App Name | Anchor attribute | Reference attribute in user profile |
| --- | --- | --- |
| Workday | WID | ManagerReference (which points to the WID of the manager record) |
| SAP SuccessFactors | personIdExternal | manager (which points to the personIdExternal of the manager record) |
| On-premises Active Directory | objectGUID | manager (which points to DN of the manager record) |
| Microsoft Entra ID | objectId | manager (which points to the manager's Microsoft Entra ID record) |

## Prerequisites for successful manager update

In order for *manager reference resolution* to work successfully, the following prerequisites should be met:

- Your provisioning app should be configured to use the default source and target anchors as listed in the anchor attributes table. Don't change the metadata properties (data type, API expression) associated with these anchor and reference attributes.
- The API expressions (XPATH for Workday and JSONPath for SuccessFactors) associated with the manager attribute resolve to a valid non-null value.
    - Workday ManagerReference default XPATH API expression: `wd:Worker/wd:Worker_Data/wd:Management_Chain_Data/wd:Worker_Supervisory_Management_Chain_Data[position()=1]/wd:Management_Chain_Data[last()=position()]/wd:Manager_Reference/wd:ID[@wd:type='WID']/text()`
    - SuccessFactors manager default JSONPath API expression: `$.employmentNav.results[0].userNav.manager.empInfo.personIdExternal`
- The manager record must also be in scope of the provisioning job.
- The provisioning app should process the manager record prior to processing the user record.

Note

The *manager* attribute mapping must be a direct mapping and can't include more than one source attribute. Using expression mappings to perform conditional assignment of manager attribute is not supported. For example, implementing logic such as “if user is active then assign manager1, else assign manager2” isn't supported.

## Provision-on-demand doesn't update manager attribute

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You successfully configured the inbound provisioning app. You're testing sync with provision-on-demand. It doesn't update the manager attribute and you get an error message *"Invalid value"*. |
| **Cause** | Your provisioning job isn't meeting one of the prerequisites for successful manager update |
| **Resolution** | \* If you changed the default manager attribute mapping, restore the default mapping.  \* Ensure that the manager record is in scope and the manager API expression resolves to a valid value.  \* Run provision-on-demand for the manager's record first and then run provision-on-demand for the user's record. |

## Full sync doesn't update manager attribute

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You successfully configured the inbound provisioning app. You're using a scoping filter to process only certain HR records. You observe that the manager resolution isn't happening for some users. |
| **Cause** | If you are using scoping filters, most likely the manager record isn't in scope. |
| **Resolution** | Update the scoping filter to add the manager record in scope |