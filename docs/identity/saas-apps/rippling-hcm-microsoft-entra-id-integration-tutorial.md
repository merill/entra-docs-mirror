---
layout: Conceptual
title: Configure Rippling Human Capital Management (HCM) for user provisioning in Active Directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/rippling-hcm-microsoft-entra-id-integration-tutorial
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
description: Integrating Rippling Human Capital Management (HCM) with Microsoft Entra ID/Active Directory.
ms.topic: how-to
ms.date: 2025-06-18T00:00:00.0000000Z
locale: en-us
document_id: 27f5b934-b80c-495e-3a21-a0f8c8d6738b
document_version_independent_id: 27f5b934-b80c-495e-3a21-a0f8c8d6738b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/rippling-hcm-microsoft-entra-id-integration-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/rippling-hcm-microsoft-entra-id-integration-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/rippling-hcm-microsoft-entra-id-integration-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 4bf24315-1ef2-5d84-715e-f0b4eab2ff2a
---

# Configure Rippling Human Capital Management (HCM) for user provisioning in Active Directory - Microsoft Entra ID | Microsoft Learn

The document provides a step-by-step guide for integrating Rippling HCM with Microsoft Entra ID/Active Directory. The steps include establishing a connection, configuring attribute mapping, testing account provisioning, configuring account access rules, and monitoring provisioning. This integration allows IT admins to automate business processes using Microsoft Entra ID Governance Lifecycle Workflows.

For detailed guidance on how to integrate your Rippling HCM environment, reference the Rippling guide [here](https://app.rippling.com/sign-in/id). Select the **Help docs** link next to the application name.

Here are the high-level steps for configuring the app integration with Microsoft Entra ID/Active Directory in the [Rippling App Shop](https://www.rippling.com/app-shop/app/microsoftactivedirectory):

Note

The steps and screenshots listed below depict experiences built in the Rippling app and highlight the depth and flexibility of the integration.

## Step 1 – Establish connection

In this step, the IT admin provides consent to Rippling to create an API-driven provisioning app in their Microsoft Entra ID tenant. The IT admin also provides details of the Active Directory domain and organizational unit container to use for new user creations.

## Step 2 – Configure attribute mapping

The app integration has a default mapping of Rippling user fields to Active Directory attributes. The IT admin can customize this attribute mapping and select which user fields from Rippling flow downstream to on-premises Active Directory. To use Microsoft Entra ID Governance Lifecycle Workflows with this integration, ensure that the fields **user start date** and **termination date** are present in the attribute mapping.

[![Screenshot showing Rippling attribute mapping.](media/rippling-hcm-microsoft-entra-id-integration-tutorial/microsoft-entra-id-attributes.png)](media/rippling-hcm-microsoft-entra-id-integration-tutorial/microsoft-entra-id-attributes.png#lightbox)

## Step 3 – Test account provisioning

In this step, the IT admin can test the attribute mapping and verify account creation or update using a test user profile.

[![Screenshot of verification of account creation window.](media/rippling-hcm-microsoft-entra-id-integration-tutorial/rippling-test-account-creation.png)](media/rippling-hcm-microsoft-entra-id-integration-tutorial/rippling-test-account-creation.png#lightbox)

## Step 4 – Configure account access rules

In this step, the IT admin configures account provisioning rules for Active Directory. Using the options in this step, the IT admin can enforce business policies around account creation and revocation.

[![Screenshot of Rippling account access rules and settings.](media/rippling-hcm-microsoft-entra-id-integration-tutorial/rippling-account-access-rules.png)](media/rippling-hcm-microsoft-entra-id-integration-tutorial/rippling-account-access-rules.png#lightbox)

## Step 5 – Monitor provisioning

In this step, the IT admin can monitor the actions performed by Rippling and review the API calls from the **Action history** tab. The data shown here corresponds to information retrieved from Microsoft Entra ID provisioning logs.

[![Screenshot of API action history tab.](media/rippling-hcm-microsoft-entra-id-integration-tutorial/api-logs-action-history.png)](media/rippling-hcm-microsoft-entra-id-integration-tutorial/api-logs-action-history.png#lightbox)

Using the above steps, once employee data from Rippling is available in Microsoft Entra ID, the IT admin can configure Microsoft Entra ID Governance Lifecycle Workflows to automate the Joiner-Mover-Leaver business processes.