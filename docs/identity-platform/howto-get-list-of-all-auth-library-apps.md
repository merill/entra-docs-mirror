---
layout: Conceptual
title: 'How to: Get a complete list of all apps using Active Directory Authentication Library (ADAL) in your tenant - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-get-list-of-all-auth-library-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this how-to guide, you get a complete list of all apps that are using ADAL in your tenant.
manager: pmwongera
ms.date: 2024-05-01T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 78002fb8-97c4-a4d0-a753-c5beda889457
document_version_independent_id: 5bad7377-c352-10f6-7748-a6eed9ee6a37
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-get-list-of-all-auth-library-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-get-list-of-all-auth-library-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-get-list-of-all-auth-library-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 54a6bac2-11d9-5312-f315-679e9f201197
---

# How to: Get a complete list of all apps using Active Directory Authentication Library (ADAL) in your tenant - Microsoft identity platform | Microsoft Learn

This article provides guidance on how to use Azure Monitor workbooks to obtain a list of all apps that use ADAL in your tenant.

Azure Active Directory Authentication Library (ADAL) has been deprecated. We strongly recommend migrating to the Microsoft Authentication Library (MSAL), which replaces ADAL. Microsoft **no longer releases new features and security fixes on ADAL**. Applications using ADAL won't be able to utilize the latest security features, leaving them vulnerable to future security threats. If you have existing applications that use ADAL, be sure to [migrate them to MSAL](msal-migration).

## Sign-ins workbook

Workbooks are a set of queries that collect and visualize information that is available in Microsoft Entra logs. [Learn more about the sign-in logs schema here](../identity/monitoring-health/reference-azure-monitor-sign-ins-log-schema).

The Sign-ins Workbook in the Microsoft Entra admin center consolidates logs from various types of sign-in events, including interactive, non-interactive, and service principal sign-ins. This aggregation offers detailed insights into the usage of ADAL applications across your tenant to help you fully understand and manage migration of your ADAL applications.

Below, we provide comprehensive instructions on accessing the workbook and subsequently demonstrate effective ways for visualizing the list of applications.

## Step 1: Send Microsoft Entra sign-in events to Azure Monitor

Microsoft Entra ID doesn't send sign-in events to Azure Monitor by default, which the Sign-ins Workbook in Azure Monitor requires.

Configure AD to send sign-in events to Azure Monitor by following the steps in [Integrate your Microsoft Entra sign-in and audit logs with Azure Monitor](../identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs). In the **Diagnostic settings** configuration step, select the **SignInLogs** check box.

No sign-in event that occurred *before* you configure Microsoft Entra ID to send the events to Azure Monitor will appear in the Sign-ins workbook.

## Step 2: Access Sign-ins workbook in the Microsoft Entra admin center

Once you integrate your Microsoft Entra sign-in and audit logs with Azure Monitor as specified in the Azure Monitor integration, access the sign-ins workbook:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Workbooks**.
3. In the **Usage** section, open the **Sign-ins** workbook.

![Screenshot of the Microsoft Entra admin center workbooks interface highlighting the sign-ins workbook.](media/howto-get-list-of-all-auth-library-apps/sign-in-workbook.png)

## Step 3: Identify apps that use ADAL

The table at the bottom of the Sign-ins workbook page lists ADAL apps active in last 30 days. You can also export a list of these apps by selecting the download button. Update these apps to use MSAL.

![Screenshot of sign-ins workbook displaying active apps that use Active Directory Authentication Library.](media/howto-get-list-of-all-auth-library-apps/active-apps-using-adal.png)

If there are no apps using ADAL, this section of workbook displays a view as shown:

![Screenshot of sign-ins workbook when no app is using Active Directory Authentication Library.](media/howto-get-list-of-all-auth-library-apps/no-active-apps-using-adal.png)

The following section of the workbook shows all the apps sign-in data. This includes total number of apps and sign-in activities including location and device.

![Screenshot of sign-ins workbook showing detailed sign-in information for your apps.](media/howto-get-list-of-all-auth-library-apps/all-apps-sign-in-data.png)

## Step 4: Dive deep to analyze application usage and authentication data

To thoroughly assess the impact of ADAL applications within your tenant, it's crucial to analyze more detailed data beyond mere identification.

- **Application Id**: Unique identifier for each application.
- **App Display Name**: The name of the application, which helps in easily identifying the app across the organization.
- **SigninCount**: Number of sign-ins per application.
- **ADAL Version**: Specific version of ADAL used by the application.
- **IP Address**: Displays the client's IP address from which the sign-in attempt originated.
- **Location**: Provides the city, state, country/region and from where the sign-in request was made.
- **Sign-in by Device**: Shares the details of the OS of the device including the specific version.

To access this enhanced data view, apply custom filters and queries within the workbook. This information not only aids in identifying critical applications but also helps in planning the migration strategy by prioritizing applications based on their usage and exposure level.

## Step 5: Update your ADAL application

Once you've identified the applications using ADAL, proceed with updating them to MSAL. The migration process varies based on the type of application you are working with. Follow the guidelines provided below for each application type.

**Single-page app (SPA)**

- [ADAL.js to MSAL.js](msal-compare-msal-js-and-adal-js)

**Web app**

- [ADAL Node to MSAL Node](msal-node-migration)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)

**Web API**

- [ADAL Java to MSAL Java](/en-us/entra/msal/java/advanced/migrate-adal-msal-java)
- [ADAL Python to MSAL Python](/en-us/entra/msal/python/advanced/migrate-python-adal-msal)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)

**Desktop app**

- [ADAL Java to MSAL Java](/en-us/entra/msal/java/advanced/migrate-adal-msal-java)
- [ADAL Python to MSAL Python](/en-us/entra/msal/python/advanced/migrate-python-adal-msal)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)

**Mobile app**

- [ADAL.Android to MSAL.Android](migrate-android-adal-msal)
- [ADAL.iOS to MSAL.iOS](/en-us/entra/msal/objc/migrate-objc-adal-msal)

**Service / daemon app**

- [ADAL Python to MSAL Python](/en-us/entra/msal/python/advanced/migrate-python-adal-msal)
- [ADAL.NET to MSAL.NET](/en-us/entra/msal/dotnet/how-to/msal-net-migration)
- [ADAL Node to MSAL Node](msal-node-migration)
- [ADAL Java to MSAL Java](/en-us/entra/msal/java/advanced/migrate-adal-msal-java)

## Step 6: Monitor to validate successful migration

With the detailed data from Step 4, you can effectively prioritize and manage the migration process of your applications to MSAL. Here’s how you can use this data to investigate sign-in scenarios and ensure a smooth transition:

- **Prioritization**: Applications with a high `SigninCount` and older `ADAL Version` should be prioritized as they represent higher usage and potentially higher risk. Migrate these applications first to minimize the most significant risks to your organization.
- **Security Analysis**: Use the `IP Address` to detect sign-in patterns. For example, if sign-ins request is made from a user or an organization owned service to identify the source of the call.
- **Compatibility Checks**: Before migrating, assess the `ADAL Version` used by the application. Some versions might have known issues with specific MSAL features. Understanding these nuances will help in planning a migration that minimizes functionality disruptions.
- **Testing Scenarios**: After updating to MSAL, monitor to compare pre-and post-migration behavior. This comparison helps verify that the migration was successful and that the application behaves as expected in the new environment.

By leveraging the detailed data from the Sign-ins workbook, your organization can strategically plan and execute the migration from ADAL to MSAL, ensuring minimal disruption and maintaining robust security protocols.