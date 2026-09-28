---
layout: Conceptual
title: Export Application Provisioning configuration and roll back to a known good state for disaster recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/export-import-provisioning-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to export your Application Provisioning configuration and roll back to a known good state for disaster recovery in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8951d68f-9904-c27f-4b8b-a5ccf7d4a8b7
document_version_independent_id: 28c5ae8d-f5ac-edc5-2807-1600bc76cf9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/export-import-provisioning-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/export-import-provisioning-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/export-import-provisioning-configuration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 796e3ed0-afa6-c0da-b002-60a0b91c1c6e
---

# Export Application Provisioning configuration and roll back to a known good state for disaster recovery in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to:

- Export and import your provisioning configuration from the Microsoft Entra admin center
- Export and import your provisioning configuration by using the Microsoft Graph API

## Export and import your provisioning configuration from the Microsoft Entra admin center

### Export your provisioning configuration

To export your configuration:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** and choose your application.
3. In the left navigation pane, select **Provisioning**. Under **Manage**, select **Attribute Mapping**. Select the **Advanced Options** dropdown, and then select **Edit schema**. The schema editor opens.
4. Select download in the command bar at the top of the page to download your schema.

### Disaster recovery - roll back to a known good state

Exporting and saving your configuration allows you to roll back to a previous version of your configuration. We recommend exporting your provisioning configuration and saving it for later use anytime you make a change to your attribute mappings or scoping filters. Open the JSON file that you downloaded, copy the entire contents. Next, replace the entire contents of the JSON payload in the schema editor, and then save. If there's an active provisioning cycle, it completes and the next cycle uses the updated schema. The next cycle is also an initial cycle, which reevaluates every user and group based on the new configuration.

Some things to consider when rolling back to a previous configuration:

- Users are evaluated again to determine if they should be in scope. If the scoping filters have changed, a user isn't in scope anymore because they're disabled. While the behavior is the desired in most cases, there are times where you may want to prevent it. To prevent the behavior, use the [skip out of scope deletions](skip-out-of-scope-deletions) functionality.
- Changing your provisioning configuration restarts the service and triggers an [initial cycle](how-provisioning-works#provisioning-cycles-initial-and-incremental).

## Export and import your provisioning configuration by using the Microsoft Graph API

You can use the Microsoft Graph API and the Microsoft Graph Explorer to export your User Provisioning attribute mappings and schema to a JSON file and import it back into Microsoft Entra ID. You can also use the steps captured here to create a backup of your provisioning configuration.

### Step 1: Retrieve your Provisioning App Service Principal ID (Object ID)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com), and navigate to the Properties section of your provisioning application. For example, if you want to export your *Workday to AD User Provisioning application* mapping navigate to the Properties section of that app.
2. In the Properties section of your provisioning app, copy the GUID value associated with the *Object ID* field. This value is also called the **ServicePrincipalId** of your App and it's used in Microsoft Graph Explorer operations.

    ![Workday App Service Principal ID](media/export-import-provisioning-configuration/wd_export_01.png)

### Step 2: Sign into Microsoft Graph Explorer

1. Launch [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)
2. Select the "Sign-In with Microsoft" button and sign-in as at least an [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator).

    ![Microsoft Graph Sign-in](media/export-import-provisioning-configuration/wd_export_02.png)
3. Upon successful sign-in, you see the user account details in the left-hand pane.

### Step 3: Retrieve the Provisioning Job ID of the Provisioning App

In the Microsoft Graph Explorer, run the following GET query replacing [servicePrincipalId] with the **ServicePrincipalId** extracted from the Step 1.

```http
   GET https://graph.microsoft.com/beta/servicePrincipals/[servicePrincipalId]/synchronization/jobs
```

You get a response as shown. Copy the `id` attribute present in the response. This value is the **ProvisioningJobId** and is used to retrieve the underlying schema metadata.

[![Provisioning Job ID](media/export-import-provisioning-configuration/wd_export_03.png)](media/export-import-provisioning-configuration/wd_export_03.png#lightbox)

### Step 4: Download the Provisioning Schema

In the Microsoft Graph Explorer, run the following GET query, replacing [servicePrincipalId] and [ProvisioningJobId] with the ServicePrincipalId and the ProvisioningJobId retrieved in the previous steps.

```http
   GET https://graph.microsoft.com/beta/servicePrincipals/[servicePrincipalId]/synchronization/jobs/[ProvisioningJobId]/schema
```

Copy the JSON object from the response and save it to a file to create a backup of the schema.

### Step 5: Import the Provisioning Schema

Caution

Perform this step only if you need to modify the schema for configuration that cannot be changed using the Microsoft Entra admin center or if you need to restore the configuration from a previously backed up file with valid and working schema.

In the Microsoft Graph Explorer, configure the following PUT query, replacing [servicePrincipalId] and [ProvisioningJobId] with the ServicePrincipalId and the ProvisioningJobId retrieved in the previous steps.

```http
    PUT https://graph.microsoft.com/beta/servicePrincipals/[servicePrincipalId]/synchronization/jobs/[ProvisioningJobId]/schema
```

In the "Request Body" tab, copy the contents of the JSON schema file.

[![Request Body](media/export-import-provisioning-configuration/wd_export_04.png)](media/export-import-provisioning-configuration/wd_export_04.png#lightbox)

In the "Request Headers" tab, add the Content-Type header attribute with value “application/json”

[![Request Headers](media/export-import-provisioning-configuration/wd_export_05.png)](media/export-import-provisioning-configuration/wd_export_05.png#lightbox)

Select **Run Query** to import the new schema.