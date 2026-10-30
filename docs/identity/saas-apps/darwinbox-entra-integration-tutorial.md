---
layout: Conceptual
title: Integrate Darwinbox HR With Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/darwinbox-entra-integration-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to integrate Darwinbox HR with Microsoft Entra ID to automate user provisioning, manage lifecycle workflows, and streamline HR-driven processes.
ms.topic: how-to
ms.date: 2025-06-19T00:00:00.0000000Z
ms.custom: ai-gen-description
ai-usage: ai-assisted
locale: en-us
document_id: 849d3009-8364-5050-ae8a-5cc1b224ec2c
document_version_independent_id: 849d3009-8364-5050-ae8a-5cc1b224ec2c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/darwinbox-entra-integration-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/darwinbox-entra-integration-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/darwinbox-entra-integration-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 409d6796-748c-c33b-610f-eda4c9771a01
---

# Integrate Darwinbox HR With Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The document provides a step-by-step guide for integrating Darwinbox with Microsoft Entra ID. The steps include establishing a connection, configuring attribute mapping, testing account provisioning, configuring account access rules, and monitoring provisioning. Use this integration to configure cloud-native users directly in Microsoft Entra ID. This integration allows IT admins to automate business processes using Microsoft Entra ID Governance Lifecycle Workflows.

For detailed guidance on how to integrate your Darwinbox environment, reference the Darwinbox guide [here](https://help.darwinbox.com/r/Integration-Templates/Darwinbox-Microsoft-Entra-ID-Connector).

Follow these high-level steps for configuring the app integration with Microsoft Entra ID in the Darwinbox Portal.

## Create single-tenant app registration

In this step, you'll create a single-tenant application in Microsoft Entra ID and assign it the required permissions. This allows Darwinbox to use the application's client credentials to create a provisioning job and securely send user data to your Microsoft Entra ID tenant.

Go to the Microsoft Entra admin center, select **App Registrations**, and then select **New registration**. Create a single-tenant app as shown below.

[![Screenshot of Microsoft Entra ID Register an application page.](media/darwinbox-entra-integration-tutorial/entra-darwinbox-register.png)](media/darwinbox-entra-integration-tutorial/entra-darwinbox-register.png#lightbox)

Add the following three Microsoft Graph application permissions to let Darwinbox create the provisioning job: `Application.ReadWrite.OwnedBy`, send user data `SyncrhonizationData-User.Upload.OwnedBy`, and review the provisioning logs `ProvisioningLog.Read.All`.

[![Screenshot of Microsoft Entra ID Darwinbox Sync page for API permissions.](media/darwinbox-entra-integration-tutorial/entra-darwinbox-sync.png)](media/darwinbox-entra-integration-tutorial/entra-darwinbox-sync.png#lightbox)

Create a client secret and provide the credentials to Darwinbox as specified in their guide.

## Configure connectors in Darwinbox Studio

1. Open Darwinbox studio and navigate to **Connector Library**.
2. Search for **Microsoft**. Install the **Microsoft** parent app connector and the **Microsoft Entra** child app connector.

[![Screenshot of the Darwinbox Studio.](media/darwinbox-entra-integration-tutorial/darwinbox-studio.png)](media/darwinbox-entra-integration-tutorial/darwinbox-studio.png#lightbox)

1. Open the **Microsoft** app and configure connection parameters obtained from step 1. Provide **Client ID**, **Client Secret** and **OAuth Token endpoint** details. The connectivity information specified here is used by Darwinbox to create a provisioning app in your Microsoft Entra ID tenant.[![Screenshot of Creating a connection for Microsoft.](media/darwinbox-entra-integration-tutorial/microsoft-app-connectivity.png)](media/darwinbox-entra-integration-tutorial/microsoft-app-connectivity.png#lightbox)
2. Manually trigger the recipe task **Configure application and Job in Microsoft Entra SCIM**. This creates the API-driven provisioning job that Darwinbox uses to send user information.[![Screenshot of configuring the application and job in Entra.](media/darwinbox-entra-integration-tutorial/configure-app-and-job-entra.png)](media/darwinbox-entra-integration-tutorial/configure-app-and-job-entra.png#lightbox)
3. In Microsoft Entra admin center, browse to **Enterprise Applications**and open the provisioning app created by Darwinbox.
    1. Copy the **Service Principal Id/Object ID** from the Overview blade.
    2. Open the Provisioning blade of this app, and go to the Overview section’s **View technical information**.
    3. Copy the **Provisioning Job ID**.
4. In Darwinbox Studio, open the **Microsoft Entra** app and configure connection details, specifically entering the **ServicePrincipalID** and **Provisioning Job ID**.[![Screenshot of editing a connection for Microsoft Entra.](media/darwinbox-entra-integration-tutorial/edit-microsoft-entra-app-connectivity.png)](media/darwinbox-entra-integration-tutorial/edit-microsoft-entra-app-connectivity.png#lightbox)

## Configure attribute mapping in Darwinbox and Entra ID

### Map Darwinbox attributes to Entra ID SCIM attributes

Refer to the Darwinbox integration guide and create the following three CSV files that will be used as input in the Darwinbox recipes.

- CSV file that maps Darwinbox attributes to Entra ID SCIM attributes. This file is used as input in the Darwinbox recipes.

    [![Screenshot of example CSV file for Darwinbox to Entra keys.](media/darwinbox-entra-integration-tutorial/darwinbox-key-entra-key.png)](media/darwinbox-entra-integration-tutorial/darwinbox-key-entra-key.png#lightbox)
- CSV file that instructs which domain should be used for email ID creation based on either group company name or department.
- CSV file that instructs how groups and licenses should be assigned (Optional).

### Add Darwinbox custom attributes to Entra provisioning job

Refer to the steps documented [here](../app-provisioning/inbound-provisioning-api-custom-attributes#step-1---extend-the-provisioning-app-schema) to introduce the following custom Darwinbox SCIM attributes in the Entra provisioning job.

- urn:ietf:params:scim:schemas:extension:Darwinbox:1.0:User:UsageLocation
- urn:ietf:params:scim:schemas:extension:Darwinbox:1.0:User:EmployeeType
- urn:ietf:params:scim:schemas:extension:Darwinbox:1.0:User:HireDate
- urn:ietf:params:scim:schemas:extension:Darwinbox:1.0:User:TerminationDate

Review and update the Microsoft Entra ID API-driven provisioning job attribute mapping. Ensure that your mapping includes `employeeHireDate` and `employeeLeaveDateTime` attributes so you can configure Joiner-Mover-Leaver Lifecycle Workflows.[![Screenshot of the Attribute Mapping screen.](media/darwinbox-entra-integration-tutorial/entra-attribute-mapping.png)](media/darwinbox-entra-integration-tutorial/entra-attribute-mapping.png#lightbox)

### Set up Darwinbox automations for user provisioning

Once you’ve configured the connector, Darwinbox has multiple recipes in place to manage the Joiner-Mover-Leaver lifecycle of your employees.

[![Screenshot of Darwinbox's featured recipes for Microsoft Entra.](media/darwinbox-entra-integration-tutorial/darwinbox-connector-library-recipes.png)](media/darwinbox-entra-integration-tutorial/darwinbox-connector-library-recipes.png#lightbox)

Configure the recipes based on your needs to enable the creation, updating, and deletion of user accounts in your Microsoft Entra ID tenant.

### Monitor provisioning

To monitor the status of your provisioning events, go to the provisioning logs or use the provisioning workbook.

- [User provisioning logs in Microsoft Entra ID](../monitoring-health/concept-provisioning-logs)
- [How to analyze the Microsoft Entra provisioning logs](../monitoring-health/howto-analyze-provisioning-logs)

### Manage Joiner-Mover-Leaver lifecycle workflows

Extend your HR-driven provisioning process to automate business processes and security controls for new hires, employment changes, and termination. With [Microsoft Entra ID Governance Lifecycle Workflows](../../id-governance/what-are-lifecycle-workflows), configure Joiner-Mover-Leaver workflows such as the following:

- “X” days before the new hire joins, send an email to the manager, add the user to groups, and generate a temporary access pass for first-time login.
- When there's a change in the user’s department, job title, or group membership, launch a custom task.
- On the last day of work, send an email to the manager, and remove the user from groups and license assignments.
- “X” days after termination, delete user from Microsoft Entra ID.