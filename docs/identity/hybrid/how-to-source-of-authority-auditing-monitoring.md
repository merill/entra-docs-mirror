---
layout: Conceptual
title: How to audit and monitor Group Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/how-to-source-of-authority-auditing-monitoring
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to audit and monitor Group Source of Authority (SOA) in Microsoft Entra ID.
ms.topic: concept-article
ms.subservice: hybrid-cloud-sync
ms.date: 2025-08-01T00:00:00.0000000Z
ms.reviewer: dhanyahk
locale: en-us
document_id: 41495551-618c-96f4-6051-7fdb23ef0a1d
document_version_independent_id: 41495551-618c-96f4-6051-7fdb23ef0a1d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/how-to-source-of-authority-auditing-monitoring.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/how-to-source-of-authority-auditing-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/how-to-source-of-authority-auditing-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: a07af2ee-8599-1cc3-1ee1-aa55a10b9aa5
---

# How to audit and monitor Group Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Admins can use **Audit Logs** in the Azure portal or the onPremisesSyncBehavior Microsoft Graph API to monitor and report SOA changes in their environment. They can also integrate SOA changes with third-party monitoring systems. For more information, see [onPremisesSyncBehavior](/en-us/graph/api/resources/onpremisessyncbehavior).

## How to use Audit Logs to see SOA changes

You can access Audit Logs in the Azure portal. They retain a record of SOA changes for the last 30 days.

1. Sign in to the [Azure portal](https://portal.azure.com) as at least a [Reports Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#reports-reader).
2. Select **Manage Microsoft Entra ID** &gt; **Monitoring** &gt; **Audit logs** or search for **audit logs** in the search bar.
3. Select activity as **Change Source of Authority from AD DS to cloud**.

    ![Screenshot of the Azure portal showing the Change Source of Authority from AD DS to cloud activity selection.](media/how-to-source-of-authority-auditing-monitoring/audit-logs.png)

## How to use Microsoft Graph API to create reports for SOA

You can use Microsoft Graph to report data such as:

- Report how many objects are SOA converted
- Filter data for converted groups
- Identify objects that were SOA converted and rolled back

### Filter and count converted objects

The [onPremisesSyncBehavior API](/en-us/graph/api/resources/onpremisessyncbehavior) helps you view the *isCloudManaged* property for a group. You can set the *isCloudManaged* property to `true` to convert the Group SOA.

You can also call the onPremisesSyncBehavior API to query how many groups converted their SOA to cloud-managed:

```https
GET groups/{ID}/onPremisesSyncBehavior?$select=id,isCloudManaged
```

You can use $search and $count to view all group objects with converted SOA. Before you can use $filter or $count, you need to set consistencyLevel = eventual in **Request headers** in Microsoft Graph Explorer:

```https
GET groups?$filter=onPremisesSyncBehavior/isCloudManaged eq true&$select=id,displayName,isCloudManaged&$count=true
```

## How to use Azure Monitor to create workbooks and reports using Log Analytics

You can integrate Audit Logs with Azure Monitoring and search the following events to get SOA operations:

- Event ID 6956 is logged if an object isn't synced to the cloud because the SOA of the object is cloud-managed.
- When SOA transfer is rolled back to on-premises, group provisioning to AD DS stops syncing changes without deleting the AD DS group. The AD DS group is also removed from the configuration scope. The AD DS group remains intact, and AD DS resumes control in the next sync cycle. You can verify in the **Audit Logs** that sync doesn't happen for this object because it's managed on-premises.

    [![Screenshot of Audit log details.](media/how-to-source-of-authority-auditing-monitoring/audit-log-details.png)](media/how-to-source-of-authority-auditing-monitoring/audit-log-details.png#lightbox)

For more information about how to create custom queries, see [Understand how provisioning integrates with Azure Monitor logs](/en-us/entra/identity/app-provisioning/application-provisioning-log-analytics).