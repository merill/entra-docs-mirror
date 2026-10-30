---
layout: Conceptual
title: Configure the role claim - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/enterprise-app-role-management
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure the role claim issued in the SAML token for enterprise applications in Microsoft Entra ID.
manager: pmwongera
ms.custom: 
ms.date: 2023-06-09T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: 46675c3e-f63e-dfaf-d380-88b0569ad45a
document_version_independent_id: 9e356f64-48ce-4b85-e8bd-788258b35ae0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/enterprise-app-role-management.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/enterprise-app-role-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/enterprise-app-role-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: b6fd6dab-0999-1954-e37c-8d29d44a16b2
---

# Configure the role claim - Microsoft identity platform | Microsoft Learn

You can customize the role claim in the access token that is received after an application is authorized. Use this feature if your application expects custom roles in the token. You can create as many roles as you need.

## Prerequisites

- A Microsoft Entra subscription with a configured tenant. For more information, see [Quickstart: Set up a tenant](quickstart-create-new-tenant).
- An enterprise application that has been added to the tenant. For more information, see [Quickstart: Add an enterprise application](../identity/enterprise-apps/add-application-portal).
- Single sign-on (SSO) configured for the application. For more information, see [Enable single sign-on for an enterprise application](../identity/enterprise-apps/add-application-portal-setup-sso).
- A user account that is assigned to the role. For more information, see [Quickstart: Create and assign a user account](../identity/enterprise-apps/add-application-portal-assign-users).

Note

This article explains how to create, update, or delete application roles on the service principal using APIs. To use the new user interface for App Roles, see [Add app roles to your application and receive them in the token](howto-add-app-roles-in-apps).

## Locate the enterprise application

Use the following steps to locate the enterprise application:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application from the search results.
4. After the application is selected, copy the object ID from the overview pane.

## Add roles

Use the Microsoft Graph Explorer to add roles to an enterprise application.

1. Open [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in another window and sign in using the administrator credentials for your tenant.

    Note

    The Cloud Application Administrator and Application Administrator role won't work in this scenario, use the Privileged Role Administrator.
2. Select **modify permissions**, select **Consent** for the `Application.ReadWrite.All` and the `Directory.ReadWrite.All` permissions in the list.
3. Replace `<objectID>` in the following request with the object ID that was previously recorded and then run the query:

    `https://graph.microsoft.com/v1.0/servicePrincipals/<objectID>`
4. An enterprise application is also referred to as a service principal. Record the **appRoles** property from the service principal object that was returned. The following example shows the typical appRoles property:

    ```json
    {
      "appRoles": [
        {
          "allowedMemberTypes": [
            "User"
          ],
          "description": "msiam_access",
          "displayName": "msiam_access",
          "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
          "isEnabled": true,
          "origin": "Application",
          "value": null
        }
      ]
    }
    ```
5. In Graph Explorer, change the method from **GET** to **PATCH**.
6. Copy the appRoles property that was previously recorded into the **Request body** pane of Graph Explorer, add the new role definition, and then select **Run Query** to execute the patch operation. A success message confirms the creation of the role. The following example shows the addition of an *Admin* role:

    ```json
    {
      "appRoles": [
        {
          "allowedMemberTypes": [
            "User"
          ],
          "description": "msiam_access",
          "displayName": "msiam_access",
          "id": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",
          "isEnabled": true,
          "origin": "Application",
          "value": null
        },
        {
          "allowedMemberTypes": [
            "User"
          ],
          "description": "Administrators Only",
          "displayName": "Admin",
          "id": "11bb11bb-cc22-dd33-ee44-55ff55ff55ff",
          "isEnabled": true,
          "origin": "ServicePrincipal",
          "value": "Administrator"
        }
      ]
    }
    ```

    You must include the `msiam_access` role object in addition to any new roles in the request body. Failure to include any existing roles in the request body removes them from the **appRoles** object. Also, you can add as many roles as your organization needs. The value of these roles is sent as the claim value in the SAML response. To generate the GUID values for the ID of new roles use the web tools, such as the [Online GUID / UUID Generator](https://www.guidgenerator.com/). The appRoles property in the response includes what was in the request body of the query.

## Edit attributes

Update the attributes to define the role claim that is included in the token.

1. Locate the application in the Microsoft Entra admin center, and then select **Single sign-on** in the left menu.
2. In the **Attributes & Claims** section, select **Edit**.
3. Select **Add new claim**.
4. In the **Name** box, type the attribute name. This example uses **Role Name** as the claim name.
5. Leave the **Namespace** box blank.
6. From the **Source attribute** list, select **user.assignedroles**.
7. Select **Save**. The new **Role Name** attribute should now appear in the **Attributes & Claims** section. The claim should now be included in the access token when signing into the application.

## Assign roles

After the service principal is patched with more roles, you can assign users to the respective roles.

1. Locate the application to which the role was added in the Microsoft Entra admin center.
2. Select **Users and groups** in the left menu and then select the user that you want to assign the new role.
3. Select **Edit assignment** at the top of the pane to change the role.
4. Select **None Selected**, select the role from the list, and then select **Select**.
5. Select **Assign** to assign the role to the user.

## Update roles

To update an existing role, perform the following steps:

1. Open [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Sign in to the Graph Explorer site as a Privileged Role Administrator.
3. Using the object ID for the application from the overview pane, replace `<objectID>` in the following request with it and then run the query:

    `https://graph.microsoft.com/v1.0/servicePrincipals/<objectID>`
4. Record the **appRoles** property from the service principal object that was returned.
5. In Graph Explorer, change the method from **GET** to **PATCH**.
6. Copy the appRoles property that was previously recorded into the **Request body** pane of Graph Explorer, add update the role definition, and then select **Run Query** to execute the patch operation.

## Delete roles

To delete an existing role, perform the following steps:

1. Open [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Sign in to the Graph Explorer site as a Privileged Role Administrator.
3. Using the object ID for the application from the overview pane in the Azure portal, replace `<objectID>` in the following request with it and then run the query:

    `https://graph.microsoft.com/v1.0/servicePrincipals/<objectID>`
4. Record the **appRoles** property from the service principal object that was returned.
5. In Graph Explorer, change the method from **GET** to **PATCH**.
6. Copy the appRoles property that was previously recorded into the **Request body** pane of Graph Explorer, set the **IsEnabled** value to **false** for the role that you want to delete, and then select **Run Query** to execute the patch operation. A role must be disabled before it can be deleted.
7. After the role is disabled, delete that role block from the **appRoles** section. Keep the method as **PATCH**, and select **Run Query** again.