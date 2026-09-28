---
layout: Conceptual
title: Sign-ins using legacy authentication workbook - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/workbook-legacy-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to use the sign-ins using legacy authentication workbook in Microsoft Entra ID to identify apps using legacy methods.
ms.topic: how-to
ms.date: 2024-11-04T00:00:00.0000000Z
ms.reviewer: besiler
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2c76c44d-8bb2-d2a7-bea6-db63ee586a02
document_version_independent_id: 40c1af47-ce2c-6e30-caf7-3c7773fd6f49
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/workbook-legacy-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/workbook-legacy-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/workbook-legacy-authentication.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1e4853b2-ee38-fd86-e43e-8d56492adfc2
---

# Sign-ins using legacy authentication workbook - Microsoft Entra ID | Microsoft Learn

Have you ever wondered how you can determine whether it's safe to turn off legacy authentication in your tenant? The sign-ins using legacy authentication workbook helps you to answer this question.

This article gives you an overview of the **Sign-ins using legacy authentication** workbook.

## Prerequisites

To use Azure Workbooks for Microsoft Entra ID, you need:

- A Microsoft Entra tenant with a [Premium P1 license](../../fundamentals/get-started-premium)
- A Log Analytics workspace *and* access to that workspace
- The appropriate roles for Azure Monitor *and* Microsoft Entra ID

### Log Analytics workspace

You must create a [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace)*before* you can use Microsoft Entra Workbooks. several factors determine access to Log Analytics workspaces. You need the right roles for the workspace *and* the resources sending the data.

For more information, see [Manage access to Log Analytics workspaces](/en-us/azure/azure-monitor/logs/manage-access).

### Azure Monitor roles

Azure Monitor provides [two built-in roles](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader) for viewing monitoring data and editing monitoring settings. Azure role-based access control (RBAC) also provides two Log Analytics built-in roles that grant similar access.

- **View**:

    - Monitoring Reader
    - Log Analytics Reader
- **View and modify settings**:

    - Monitoring Contributor
    - Log Analytics Contributor

### Microsoft Entra roles

Read only access allows you to view Microsoft Entra ID log data inside a workbook, query data from Log Analytics, or read logs in the Microsoft Entra admin center. Update access adds the ability to create and edit diagnostic settings to send Microsoft Entra data to a Log Analytics workspace.

- **Read**:

    - Reports Reader
    - Security Reader
    - Global Reader
- **Update**:

    - Security Administrator

For more information on Microsoft Entra built-in roles, see [Microsoft Entra built-in roles](../role-based-access-control/permissions-reference).

For more information on the Log Analytics RBAC roles, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles#log-analytics-contributor).

## Description

![Screenshot of workbook thumbnail.](media/workbook-legacy-authentication/sign-ins-legacy-auth.png)

Microsoft Entra ID supports several of the most widely used authentication and authorization protocols including legacy authentication. Legacy authentication refers to basic authentication, which was once a widely used industry-standard method for passing user name and password information through a client to an identity provider.

Examples of applications that commonly or only use legacy authentication are:

- Microsoft Office 2013 or older.
- Apps using legacy auth with mail protocols like POP, IMAP, and SMTP AUTH.

Single-factor authentication (for example, username and password) doesn’t provide the required level of protection for today’s computing environments. Passwords are bad as they're easy to guess and humans are bad at choosing good passwords.

Unfortunately, legacy authentication:

- Doesn't support multifactor authentication (MFA) or other strong authentication methods.
- Makes it impossible for your organization to move to passwordless authentication.

To improve the security of your Microsoft Entra tenant and experience of your users, you should disable legacy authentication. However, important user experiences in your tenant might depend on legacy authentication. Before shutting off legacy authentication, you might want to find those cases so you can migrate them to more secure authentication.

The **Sign-ins using legacy authentication** workbook lets you see all legacy authentication sign-ins in your environment. This workbook helps you find and migrate critical workflows to more secure authentication methods before you shut off legacy authentication.

## How to access the workbook

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using the appropriate combination of roles.
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
3. Select the **Sign-ins using legacy authentication** workbook from the **Usage** section.

## Workbook sections

With this workbook, you can distinguish between interactive and non-interactive sign-ins. This workbook highlights which legacy authentication protocols are used throughout your tenant.

The data collection consists of three steps:

1. Select a legacy authentication protocol, and then select an application to filter by users accessing that application.
2. Select a user to see all their legacy authentication sign-ins to the selected app.
3. View all legacy authentication sign-ins for the user to understand how legacy authentication is being used.

## Filters

This workbook supports multiple filters:

- Time range (up to 90 days)
- User principal name
- Application
- Status of the sign-in (success or failure)

![Filter options](media/workbook-legacy-authentication/filter-options.png)

## Best practices

- For guidance on blocking legacy authentication in your environment, see [Block legacy authentication to Microsoft Entra ID with Conditional Access](../conditional-access/policy-block-legacy-authentication).
- Many email protocols that once relied on legacy authentication now support more secure modern authentication methods. If you see legacy email authentication protocols in this workbook, consider migrating to modern authentication for email instead. For more information, see [Deprecation of Basic authentication in Exchange Online](/en-us/exchange/clients-and-mobile-in-exchange-online/deprecation-of-basic-authentication-exchange-online).
- Some clients can use both legacy authentication or modern authentication depending on client configuration. If you see “modern mobile/desktop client” or “browser” for a client in the Microsoft Entra logs, it's using modern authentication. If it has a specific client or protocol name, such as “Exchange ActiveSync,” it's using legacy authentication to connect to Microsoft Entra ID. The client types in Conditional Access, and the Microsoft Entra reporting page in the Microsoft Entra admin center demarcate modern authentication clients and legacy authentication clients for you, and only legacy authentication is captured in this workbook.
- To learn more about identity protection, see [What is identity protection](../../id-protection/overview-identity-protection).
- For more information about Microsoft Entra workbooks, see [How to use Microsoft Entra workbooks](howto-use-workbooks).