---
layout: Conceptual
title: Skip deletion of out of scope users in Microsoft Entra Application Provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/skip-out-of-scope-deletions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to override the default behavior of deprovisioning out of scope users in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5ed55ea3-4271-367f-4cdb-2a8f7a38823a
document_version_independent_id: a795bdbb-ae07-87a6-71e4-681370f51d1a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/skip-out-of-scope-deletions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/skip-out-of-scope-deletions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/skip-out-of-scope-deletions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 83f2a329-6da0-0493-4b0c-21cfbe2a8ed6
---

# Skip deletion of out of scope users in Microsoft Entra Application Provisioning - Microsoft Entra ID | Microsoft Learn

By default, the Microsoft Entra provisioning engine soft deletes or disables users that go out of scope. However, for certain scenarios like Workday to AD User Inbound Provisioning, this behavior may not be the expected and you may want to override this default behavior.

This article describes how to use the Microsoft Graph API and the Microsoft Graph API explorer to set the flag ***SkipOutOfScopeDeletions*** that controls the processing of accounts that go out of scope.

- If ***SkipOutOfScopeDeletions*** is set to 0 (false), accounts that go out of scope are disabled in the target.
- If ***SkipOutOfScopeDeletions*** is set to 1 (true), accounts that go out of scope aren't disabled in the target. This flag is set at the *Provisioning App* level and can be configured using the Graph API.

Because this configuration is widely used with the *Workday to Active Directory user provisioning* app, the following steps include screenshots of the Workday application. However, the configuration can also be used with *all other apps*, such as ServiceNow, Salesforce, and Dropbox. To successfully complete this procedure, you must have first set up app provisioning for the app. Each app has its own configuration article. For example, to configure the Workday application, see [Tutorial: Configure Workday to Microsoft Entra user provisioning](../saas-apps/workday-inbound-cloud-only-tutorial). SkipOutOfScopeDeletions doesn't work for cross-tenant synchronization.

## Step 1: Retrieve your Provisioning App Service Principal ID (Object ID)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select your application and go to Properties section of your provisioning app. In this example, we're using Workday.
4. Copy the GUID value in the *Object ID* field. This value is also called the **ServicePrincipalId** of your app and it's used in Graph Explorer operations.

## Step 2: Sign into Microsoft Graph Explorer

1. Launch [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)
2. Select the "Sign-In with Microsoft" button and sign-in as a user with at least the [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) role.

    ![Screenshot of Microsoft Graph Explorer Sign-in.](media/skip-out-of-scope-deletions/wd_export_02.png)
3. Upon successful sign-in, the user account details appear in the left-hand pane.
4. Select the **Modify permissions** tab and consent to the `Synchronization.ReadWrite.All` permission. This permission is required for the Graph API queries in the following steps.

## Step 3: Get existing app credentials and connectivity details

In the Microsoft Graph Explorer, run the following GET query replacing [servicePrincipalId] with the **ServicePrincipalId** extracted from the Step 1.

```http
   GET https://graph.microsoft.com/beta/servicePrincipals/[servicePrincipalId]/synchronization/secrets
```

![Screenshot of GET job query.](media/skip-out-of-scope-deletions/skip-03.png)

Copy the Response into a text file. It looks like the JSON text shown, with values highlighted in yellow specific to your deployment. Add the lines highlighted in green to the end and update the Workday connection password highlighted in blue.

![Screenshot of GET job response.](media/skip-out-of-scope-deletions/skip-04.png)

Here's the JSON block to add to the mapping.

```json
{
  "key": "SkipOutOfScopeDeletions",
  "value": "True"
}
```

## Step 4: Update the secrets endpoint with the SkipOutOfScopeDeletions flag

In the Graph Explorer, run the command to update the secrets endpoint with the ***SkipOutOfScopeDeletions*** flag.

In the URL, replace [servicePrincipalId] with the **ServicePrincipalId** extracted from the Step 1.

```http
   PUT https://graph.microsoft.com/beta/servicePrincipals/[servicePrincipalId]/synchronization/secrets
```

Copy the updated text from Step 3 into the "Request Body".

![Screenshot of PUT request.](media/skip-out-of-scope-deletions/skip-05.png)

Select “Run Query”.

You should get the output as "Success – Status Code 204". If you receive an error, you may need to check that your account has Read/Write permissions for ServicePrincipalEndpoint. You can find this permission by clicking on the *Modify permissions* tab in Graph Explorer.

![Screenshot of PUT response.](media/skip-out-of-scope-deletions/skip-06.png)

## Step 5: Verify that out of scope users don’t get disabled

You can test this flag results in expected behavior by updating your scoping rules to skip a specific user. In the example, we're excluding the employee with ID 21173 (who was earlier in scope) by adding a new scoping rule:

![Screenshot that shows the &quot;Add Scoping Filter&quot; section with an example user highlighted.](media/skip-out-of-scope-deletions/skip-07.png)

In the next provisioning cycle, the Microsoft Entra provisioning service identifies that the user 21173 is out of scope. If the `SkipOutOfScopeDeletions` property is enabled, then the synchronization rule for that user displays a message.