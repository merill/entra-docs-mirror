---
layout: Conceptual
title: Troubleshoot user update issues with HR provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/hr-user-update-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to troubleshoot user update issues with HR provisioning
ms.topic: troubleshooting
ai-usage: ai-assisted
ms.date: 2026-08-20T00:00:00.0000000Z
ms.reviewer: chmutali
locale: en-us
document_id: aaac29de-7f44-3c89-6710-a60850950247
document_version_independent_id: b8fc05c3-9734-3813-5e08-d38fa96d7e4a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/hr-user-update-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/hr-user-update-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/hr-user-update-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 0f8c876b-558b-23c1-11fd-2c18d81663ed
---

# Troubleshoot user update issues with HR provisioning - Microsoft Entra ID | Microsoft Learn

## Null and empty values not processed as expected

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning
- SAP SuccessFactors to on-premises Active Directory user provisioning
- SAP SuccessFactors to Microsoft Entra user provisioning

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You successfully configured the inbound provisioning app. The HR app returns a null or empty value, but the target attribute isn't cleared, or the operation fails with the error message: `InvalidAttributeSyntax-LdapErr: The syntax is invalid. The parameter is incorrect. Error in attribute conversion operation, data 0, v3839`. |
| **Cause** | Attribute value clearing is disabled by default. The provisioning service clears a target attribute only when **Flow null values** is enabled for both the source attribute and target mapping. Without both settings, the null or empty value might be ignored or passed to a target that doesn't accept an empty string. |
| **Resolution** | Check the provisioning logs to confirm the value returned by the HR connector. Then configure the source attribute and target mapping based on the intended behavior. |

**Recommended resolutions**

Let's say the Workday attribute `BusinessTitle`, which maps to the Active Directory attribute `jobTitle`, can be null or empty.

- To clear the existing target value, [enable attribute value clearing](clear-attribute-values) for both the source attribute and target mapping.
- To replace a null or empty value with a nonblank fallback value, use the [Switch](functions-for-customizing-application-data#switch) function. For example, `Switch([BusinessTitle],[BusinessTitle],"","N/A")`.
- To preserve the existing target value, use the [IgnoreFlowIfNullOrEmpty](functions-for-customizing-application-data#ignoreflowifnullorempty) function. For example, `IgnoreFlowIfNullOrEmpty([BusinessTitle])`.

## Some Workday attribute updates are missing

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You successfully configured the Workday inbound provisioning app and successfully connected to the Workday tenant URL. You're observing that there's a delay in the flow of certain attribute updates from Workday or in some cases, the attributes changes from Workday aren't flowing through as expected during incremental sync. |
| **Cause** | During incremental sync, the provisioning app queries Workday transaction log for changes to the primary Worker entity and only changes tracked by Workday's transaction log are processed.  If changes to a Workday attribute in your setup aren't tracked in Workday's transaction log, then Microsoft Entra ID doesn't fetch that change. For example: the *LocalReference* Workday attribute is part of the default attribute mapping and it has XPATH `wd:Worker/wd:Worker_Data/wd:Employment_Data/wd:Position_Data/wd:Business_Site_Summary_Data/wd:Local_Reference/wd:ID[@wd:type='Locale_ID']/text()`. This attribute is part of the entity *Business\_Site\_Summary\_Data*. A change in the value of this attribute in Workday doesn't show up in the Workday transaction log. Thus during incremental sync, the new value of this attribute shows up only if an attribute associated with the primary Worker entity also changes during the sync interval. |
| **Resolution** | If you notice this behavior frequently, where changes to certain Workday attributes aren't flowing through, we recommend periodically running a weekly or monthly full sync. |

## Attribute isn't found

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning
- Workday to on-premises Active Directory user provisioning
- SAP SuccessFactors to on-premises Active Directory user provisioning
- API-driven provisioning to on-premises Active Directory

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You receive the error code: `HybridSynchronizationActiveDirectoryCannotFindAttribute` |
| **Cause** | The attribute name wasn't found in the Active Directory schema: attribute. |
| **Resolution** | If the attribute was recently added to Active Directory, restart the provisioning agent, as it caches the schema at startup. |

## User match with extensionAttribute not working

**Applies to:**

- Workday to Microsoft Entra user provisioning
- SAP SuccessFactors to Microsoft Entra user provisioning

| Troubleshooting | Details |
| --- | --- |
| **Issue** | Let's say you're using *extensionAttribute3* in Microsoft Entra ID to store the employee ID and you map it to Workday *WorkerID* or SuccessFactors *personIdExternal* attribute for user matching. With this configuration, the matching step in provisioning process fails. This issue impacts both user creation and updates. |
| **Cause** | The Microsoft Entra ID *OnPremisesExtensionAttributes* (`extensionAttributes1-15`) can't be used as a matching attribute because the `$filter` parameter of **Azure AD Graph API** doesn't [support filtering by extensionAttributes](/en-us/previous-versions/azure/ad/graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#filter). |
| **Resolution** | Don't use Microsoft Entra ID *OnPremisesExtensionAttributes* (`extensionAttributes1-15`) in the matching attribute pair. Use employeeID. |

## Updates to Microsoft Entra ID *mail* attribute not supported

**Applies to:**

- Workday to Microsoft Entra user provisioning
- SAP SuccessFactors to Microsoft Entra user provisioning
- API-driven provisioning to Microsoft Entra ID

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You configured *mail* attribute provisioning from your HR system to Microsoft Entra ID. Any update to the mail attribute isn't working even though the provisioning logs display a record for the mail attribute. |
| **Cause** | The provisioning connector to Microsoft Entra does not support setting the *mail* attribute during user provisioning as this attribute is managed by Microsoft Exchange online. |
| **Resolution** | After creating the user, assigning the Exchange Online license to the user automatically sets the user principal name as the email address. To update the mail attribute, use the Exchange Online portal or PowerShell. |

## Provisioning Last Day of Work field from Workday

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning

| Troubleshooting | Details |
| --- | --- |
| **Issue** | You configured attribute mapping for Workday 'Last Day of Work' (`StatusTerminationLastDayOfWork`) attribute in the provisioning app. However, the 'Last Day of Work' update only happens after the termination date is effective, whereas you’d like to fetch this 'Last Day of Work' before the termination date. |
| **Cause** | In Workday, the 'Last Day of Work' field gets set on the worker profile only after the termination date is effective. Hence, the Workday provisioning connector is unable to get this date in advance before the termination date. |
| **Resolution** | In Workday create a provisioning group called 'Workers past Last Day of Work'. Add automation in Workday to assign users to this group when a worker’s last day of work is reached. In the Microsoft Entra provisioning job, add a Workday XPATH attribute to fetch this group assignment. |

- Example:``LastDayOfWorkWorkers =  wd:Worker/wd:Worker_Data/wd:Account_Provisioning_Data/wd:Provisioning_Group_Assignment_Data[wd:Status='Assigned' and wd:Provisioning_Group=" Workers past Last Day of Work"]/wd:Provisioning_Group/text()``

Use this field in the attribute mapping logic for the accountDisabled flag.

- Example:``Switch([LastDayOfWorkWorkers], Switch([Active], , "1", "False", "0", "True"), 'Workers past Last Day of Work', "True")``

## Workday termination processing delay

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning

| Troubleshooting | Details |
| --- | --- |
| **Issue** | During incremental sync, there may be a delay of 12-18 hours in processing the termination event for workers located in the Asia Pacific and Australia/New Zealand regions. |
| **Cause** | The Workday Integration System User (ISU) accounts always retrieve data based on the Pacific time zone. The connector currently doesn't implement specialized query to process termination records specific to a time zone. |
| **Resolution** | Use the termination lookahead query feature. For setup and configuration steps, see [Configure Workday termination lookahead query](configure-workday-termination-lookahead). |

## SuccessFactors termination processing delay

**Applies to:**

- SuccessFactors to on-premises Active Directory user provisioning
- SuccessFactors to Microsoft Entra ID user provisioning

| Troubleshooting | Details |
| --- | --- |
| **Issue** | In certain scenarios, there might be delays in propagation of terminated employment status as an "account disable" operation. This isn't due to a lack of user-disable capability in Microsoft Entra, but rather how real-time identity lifecycle changes are detected during HR-driven provisioning. |
| **Cause** | Microsoft Entra's provisioning service operates as a stateless change-detection system. It relies on the source system (for example, SAP SuccessFactors) to emit a time-based change event—such as a termination becoming effective—at the point when the change should take effect. Provisioning cycles then detect and act on those events during incremental sync. In scenarios where termination is effective *as of the current day*, SuccessFactors might not emit an incremental change event at the exact time the user's employment status changes (for example, at end of business day). As a result, Microsoft Entra provisioning doesn't receive a detectable change during its polling cycle and the "disable" action might be delayed until a subsequent update occurs in the source system. |
| **Resolution** | To support deterministic, policy-driven offboarding, use [Microsoft Entra ID Governance Lifecycle Workflows](../../id-governance/what-are-lifecycle-workflows). This model is based on state, rather than time-based events. [Synchronize the employee's `endDate`](../../id-governance/how-to-lifecycle-workflow-sync-attributes) from SuccessFactors into Microsoft Entra (for example, via the `employeeLeaveDateTime` attribute). Organizations can then trigger automated offboarding workflows directly from directory state—ensuring accounts are disabled exactly when the employment end date is reached, independent of incremental change detection in the HR system. |

This approach enables:

- Timely and predictable user offboarding.
- Policy-based automation aligned to HR intent.
- Reduced reliance on custom scripts or manual intervention.
- Centralized lifecycle governance across hybrid and cloud identities.

[Lifecycle Workflows](../../id-governance/what-are-lifecycle-workflows) are part of Microsoft Entra ID Governance and are designed specifically for enforcing joiner-mover-leaver policies based on authoritative identity state in the directory.

## Redundant updates for certain attribute types

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning
- SAP SuccessFactors to on-premises Active Directory user provisioning
- SAP SuccessFactors to Microsoft Entra user provisioning
- API-driven provisioning to on-premises Active Directory
- API-driven provisioning to Microsoft Entra ID

| Troubleshooting | Details |
| --- | --- |
| **Issue** | Provisioning logs show repeated update operations for certain attributes, even when there are no meaningful changes in source data. This behavior is commonly observed with multi-valued attributes, custom security attributes, and derived account status attributes such as `accountEnabled` or `accountDisabled`. |
| **Cause** | For certain attribute types, the provisioning engine evaluates values at runtime instead of performing a stable comparison with the previously provisioned state. Because of this runtime evaluation model, these attributes might be reprocessed or written again during sync cycles, which can generate redundant update entries in provisioning logs. |
| **Resolution** | No resolution is currently available. This behavior is a known limitation. |