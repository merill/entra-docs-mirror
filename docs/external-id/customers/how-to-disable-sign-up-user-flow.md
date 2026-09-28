---
layout: Conceptual
title: Disable sign-up in a sign-up and sign-in user flow - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-disable-sign-up-user-flow
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Disable sign-up in your user flow with Microsoft Graph API. Prevent new registrations and allow only sign-in for your external users.
ms.topic: how-to
ms.date: 2025-06-30T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024, sfi-image-nochange
locale: en-us
document_id: 269ae9dc-4f96-ddab-8181-f120a2235d08
document_version_independent_id: 269ae9dc-4f96-ddab-8181-f120a2235d08
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-disable-sign-up-user-flow.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-disable-sign-up-user-flow
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-disable-sign-up-user-flow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 6dad1df7-83e5-0f7b-b806-ffc8c07c88a9
---

# Disable sign-up in a sign-up and sign-in user flow - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

To restrict access so that only existing external users can sign in, you can disable the sign-up option in your sign-up and sign-in user flow. This article shows you how to use the Microsoft Graph API to update your user flow settings, preventing new registrations while allowing sign-in for current users.

You use the [Update authenticationEventsFlow API in Microsoft Graph](/en-us/graph/api/authenticationeventsflow-update) to update the **onInteractiveAuthFlowStart** property &gt; **isSignUpAllowed** property to `false`.

## Prerequisites

- **A sign-up and sign-in user flow**: Before you begin, [create the user flow](how-to-user-flow-sign-up-sign-in-customers) that you want to associate with your application.
- **Application registration**: In your external tenant, [register your application](/en-us/entra/identity-platform/quickstart-register-app).

## Disable sign-up flow

To disable sign-up flow, you need to know the ID of the user flow whose sign-up you want to disable. You can't read the user flow ID from the Microsoft Entra admin center, but you can retrieve it via Microsoft Graph API if you know the app associated with it.

Follow these steps to disable the sign-up flow:

1. Read the application ID associated with the user flow:

    1. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
    2. From the list, select your user flow.
    3. In the left menu, under **Use**, select **Applications**.
    4. From the list, under **Application (client) ID** column, copy the Application (client) ID.
2. Identify the ID of the user flow whose sign-up you want to disable. To do so, [List the user flow associated with the specific application](/en-us/graph/api/identitycontainer-list-authenticationeventsflows#example-4-list-user-flow-associated-with-specific-application-id). This Microsoft Graph API endpoint requires you to know the application ID you obtained from the previous step.
3. [Update your user flow](/en-us/graph/api/authenticationeventsflow-update) to disable sign-up.

    **Example**:

    ```http
    PATCH https://graph.microsoft.com/beta/identity/authenticationEventsFlows/{user-flow-id} 
    ```

    **Request body**

    ```json
        {    
            "@odata.type": "#microsoft.graph.externalUsersSelfServiceSignUpEventsFlow",    
            "onInteractiveAuthFlowStart": {    
                "@odata.type": "#microsoft.graph.onInteractiveAuthFlowStartExternalUsersSelfServiceSignUp",    
                "isSignUpAllowed": false    
          }    
        }
    ```

    Replace `{user-flow-id}` with the user flow ID that you obtained in the previous step. Notice the `isSignUpAllowed` parameter is set to *false*. To re-enable sign-up, make a call to the Microsoft Graph API endpoint, but set the `isSignUpAllowed` parameter to *true*.