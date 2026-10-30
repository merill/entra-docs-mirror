---
layout: Conceptual
title: Configure API-driven inbound provisioning app - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/inbound-provisioning-api-configure-app
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to configure API-driven inbound provisioning app.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: cmmdesai
ms.custom: sfi-image-nochange
locale: en-us
document_id: e947f34f-6e1f-199d-df18-061e4aed6980
document_version_independent_id: 80ecf3b7-3470-ed5c-c769-779a24fe3305
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/inbound-provisioning-api-configure-app.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/inbound-provisioning-api-configure-app
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/inbound-provisioning-api-configure-app.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: dcc2e2b8-408d-4e72-a12f-8461b82e4861
---

# Configure API-driven inbound provisioning app - Microsoft Entra ID | Microsoft Learn

## Introduction

This tutorial describes how to configure [API-driven inbound user provisioning](inbound-provisioning-api-concepts).

This feature is available only when you configure the following Enterprise Gallery apps:

- API-driven inbound user provisioning to Microsoft Entra ID
- API-driven inbound user provisioning to on-premises AD

## Prerequisites

To complete the steps in this tutorial, you need access to Microsoft Entra admin center with the following roles:

- [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) (if you're configuring inbound user provisioning to Microsoft Entra ID) OR
- [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) + [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator) (if you're configuring inbound user provisioning to on-premises Active Directory)

If you're configuring inbound user provisioning to on-premises Active Directory, you need access to a Windows Server where you can install the provisioning agent for connecting to your Active Directory domain controller.

## Create your API-driven provisioning app

1. Log in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](https://go.microsoft.com/fwlink/?linkid=2247823).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Click on **New application** to create a new provisioning application. [![Screenshot of Microsoft Entra admin center.](media/inbound-provisioning-api-configure-app/provisioning-entra-admin-center.png)](media/inbound-provisioning-api-configure-app/provisioning-entra-admin-center.png#lightbox)
4. Enter **API-driven** in the search field, then select the application for your setup:

    - **API-driven provisioning to on-premises Active Directory**: Select this app if you're provisioning hybrid identities (identities that need both on-premises AD and Microsoft Entra account) from your system of record. Once these accounts are provisioned in on-premises AD, they are automatically synchronized to your Microsoft Entra tenant using Microsoft Entra Connect Sync or Microsoft Entra Connect cloud sync.
    - **API-driven provisioning to Microsoft Entra ID**: Select this app if you're provisioning cloud-only identities (identities that don't require on-premises AD accounts and only need Microsoft Entra account) from your system of record.

    [![Screenshot of API-driven provisioning apps.](media/inbound-provisioning-api-configure-app/api-driven-inbound-provisioning-apps.png)](media/inbound-provisioning-api-configure-app/api-driven-inbound-provisioning-apps.png#lightbox)
5. In the **Name** field, rename the application to meet your naming requirements, then click **Create**.

    [![Screenshot of create app.](media/inbound-provisioning-api-configure-app/provisioning-create-inbound-provisioning-app.png)](media/inbound-provisioning-api-configure-app/provisioning-create-inbound-provisioning-app.png#lightbox)

    Note

    If you plan to ingest data from multiple sources, each with their own sync rules, you can create multiple apps and give each app a descriptive name, such as `Provision-Employees-From-CSV-to-AD` or `Provision-Contractors-From-SQL-to-AD`.
6. Once the application creation is successful, go to the Provisioning blade and click on **Get started**. [![Screenshot of Get started button.](media/inbound-provisioning-api-configure-app/provisioning-overview-get-started.png)](media/inbound-provisioning-api-configure-app/provisioning-overview-get-started.png#lightbox)
7. Switch the Provisioning Mode from Manual to **Automatic**.

Depending on the app you selected, use one of the following sections to complete your setup:

- Configure API-driven inbound provisioning to on-premises AD
- Configure API-driven inbound provisioning to Microsoft Entra ID

## Configure API-driven inbound provisioning to on-premises AD

1. After setting the Provisioning Mode to **Automatic**, click on **Save** to create the initial configuration of the provisioning job.
2. Click on the information banner about the Microsoft Entra provisioning Agent.
3. Click **Accept terms & download** to download the Microsoft Entra provisioning Agent.
4. Refer to the steps documented here to [install and configure the provisioning agent.](https://go.microsoft.com/fwlink/?linkid=2241216). This step registers your on-premises Active Directory domains with your Microsoft Entra tenant.
5. Once the agent registration is successful, select your domain in the drop-down **Active Directory domain** and specify the distinguished name of the OU where new user accounts are created by default. 
    Note

    If your AD domain is not visible in the **Active Directory Domain** dropdown list, reload the provisioning app in the browser. Click on **View on-premises agents for your domain** to ensure that your agent status is healthy.
6. Click on **Test connection** to ensure that Microsoft Entra ID can connect to the provisioning agent.
7. Click on **Save** to save your changes.
8. Once the save operation is successful, you'll see two more expansion panels – one for **Mappings** and one for **Settings**. Before proceeding to the next step, provide a valid notification email ID and save the configuration again. 
    Note

    Providing the **Notification Email** in **Settings** is mandatory. If the Notification Email is left empty, then the provisioning goes into quarantine when you start the execution.
9. Click on hyperlink in the **Mappings** expansion panel to view the default attribute mappings. 
    Note

    The default configuration in the **Attribute Mappings** page maps SCIM Core User and Enterprise User attributes to on-premises AD attributes. We recommend using the default mappings to get started and customizing these mappings later as you get more familiar with the overall data flow.
10. Complete the configuration by following steps in the section Start accepting provisioning requests.

## Configure API-driven inbound provisioning to Microsoft Entra ID

1. After setting the Provisioning Mode to **Automatic**, click on **Save** to create the initial configuration of the provisioning job.
2. Once the save operation is successful, you will see two more expansion panels – one for **Mappings** and one for **Settings**. Before proceeding to the next step, make sure you provide a valid notification email ID and Save the configuration once more.

    Note

    Providing the **Notification Email** in **Settings** is mandatory. If the Notification Email is left empty, then the provisioning goes into quarantine when you start the execution.
3. Click on hyperlink in the **Mappings** expansion panel to view the default attribute mappings.

    Note

    The default configuration in the **Attribute Mappings** page maps SCIM Core User and Enterprise User attributes to on-premises AD attributes. We recommend using the default mappings to get started and customizing these mappings later as you get more familiar with the overall data flow.
4. Complete the configuration by following steps in the section Start accepting provisioning requests.

## Start accepting provisioning requests

1. Open the provisioning application's **Provisioning** &gt; **Overview** page.
2. On this page, you can take the following actions:
    - **Start provisioning** control button – Click on this button to place the provisioning job in **listen mode** to process inbound bulk upload request payloads.
    - **Stop provisioning** control button – Use this option to pause/stop the provisioning job.
    - **Restart provisioning** control button – Use this option to purge any existing request payloads pending processing and start a new provisioning cycle.
    - **Edit provisioning** control button – Use this option to edit the job settings, attribute mappings and to customize the provisioning schema.
    - **Provision on demand** control button – This feature is not supported for API-driven inbound provisioning.
    - **Provisioning API Endpoint** URL text – Copy the HTTPS URL value shown and save it in a Notepad or OneNote for use later with the API client.
3. Expand the **Statistics to date** &gt; **View technical information** panel and copy the **Provisioning API Endpoint** URL. Share this URL with your API developer after [granting access permission](inbound-provisioning-api-grant-access) to invoke the API.