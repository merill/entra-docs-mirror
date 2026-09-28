---
layout: Conceptual
title: Automated ServiceNow Ticket Creation with Microsoft Entra Entitlement Management Integration - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/entitlement-management-ticketed-provisioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This tutorial walks you through Ticketed provisioning via ServiceNow integration with entitlement management using custom extensions and Logic Apps.
ms.subservice: entitlement-management
ms.topic: tutorial
ms.date: 2026-02-02T00:00:00.0000000Z
ms.custom: template-tutorial, sfi-image-nochange
locale: en-us
document_id: f8107b1e-a5af-a03b-7aef-def51d9977df
document_version_independent_id: 9cf860b4-4a6e-3c2f-9b63-3962f4c040f6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/entitlement-management-ticketed-provisioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/entitlement-management-ticketed-provisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/entitlement-management-ticketed-provisioning.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5ca5d0ec-7921-4c50-ae9f-dd608d6ffc4c
---

# Automated ServiceNow Ticket Creation with Microsoft Entra Entitlement Management Integration - Microsoft Entra ID Governance | Microsoft Learn

Scenario: In this scenario you learn how to use custom extensibility, and a Logic App, to automatically generate ServiceNow tickets for manual provisioning of users who have received assignments and need access to apps.

In this tutorial, you learn:

- Adding a Logic App Workflow to an existing catalog.
- Adding a custom extension to a policy within an existing access package.
- Registering an application in Microsoft Entra ID for resuming Entitlement Management workflow
- Configuring ServiceNow for Automation Authentication.
- Requesting access to an access package as an end-user.
- Receiving access to the requested access package as an end-user.

## Prerequisites

- A Microsoft Entra user account with an active Azure subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following least privileged roles: Cloud Application Administrator, Application Administrator, or owner of the service principal.
- A [ServiceNow instance](https://www.servicenow.com/) of Rome or higher
- SSO integration with ServiceNow. If this isn't already configured, see:[Tutorial: Microsoft Entra single sign-on (SSO) integration with ServiceNow](../identity/saas-apps/servicenow-tutorial) before continuing.

Note

It's recommended to use a least privilege role when completing these steps.

## Adding Logic App Workflow to an existing Catalog for Entitlement Management

To add a Logic App workflow to an existing catalog use the ARM template for the Logic App creation here:

.

[![Screenshot of Logic App ARM template.](media/entitlement-management-servicenow-integration/logic-app-arm-template.png)](media/entitlement-management-servicenow-integration/logic-app-arm-template.png#lightbox)

Provide the resource group details, along with the Catalog ID to associate the Logic App with and select purchase. For more information on how to create a new catalog, see: [Create and manage a catalog of resources in entitlement management](entitlement-management-catalog-create).

After a catalog is created, you'd add a Logic App workflow by doing the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and Resource group owner.
2. In the left menu, select **Catalogs**.
3. Select the catalog for which you want to add a custom extension and then in the left menu, select **Custom Extensions**.
4. In the header navigation bar, select **Add a Custom Extension**.
5. In the **Basics** tab, enter the name of the custom extension and a description of the workflow. These fields show up in the **Custom Extensions** tab of the Catalog. [![Screenshot of creating a custom extension for entitlement management.](media/entitlement-management-servicenow-integration/entitlement-management-create-custom-extension.png)](media/entitlement-management-servicenow-integration/entitlement-management-create-custom-extension.png#lightbox)
6. Select the **Extension Type** as “**Request workflow**” to correspond with the policy stage of the access package requested being created. [![Screenshot of entitlement management custom extension behavior actions tab.](media/entitlement-management-servicenow-integration/entitlement-management-custom-extension-behavior.png)](media/entitlement-management-servicenow-integration/entitlement-management-custom-extension-behavior.png#lightbox)
7. Select **Launch and wait** in the **Extension Configuration** which will pause the associated access package action until after the Logic App linked to the extension completes its task, and a resume action is sent by the admin to continue the process. For more information on this process, see: [Configuring custom extensions that pause entitlement management processes](entitlement-management-logic-apps-integration#configuring-custom-extensions-that-pause-entitlement-management-processes).
8. In the **Details** tab, choose No in the "*Create new logic App*" field as the Logic App was created in the previous steps. However, you need to provide the Azure subscription and resource group details, along with the Logic App name. [![Screenshot of the entitlement management custom extension details tab.](media/entitlement-management-servicenow-integration/entitlement-management-custom-extension-details.png)](media/entitlement-management-servicenow-integration/entitlement-management-custom-extension-details.png#lightbox)
9. In **Review and Create**, review the summary of your custom extension and make sure the details for your Logic App call-out are correct. Then select **Create**.
10. Once created, the Logic App is able to be accessed under **Logic App** next to the custom extension on the custom extensions page. You're able to call on this in access package policies. ![Screenshot of custom extension list.](media/entitlement-management-servicenow-integration/custom-extension-list.png)

Tip

To learn more about custom extension feature that pauses entitlement management processes, see: [Configuring custom extensions that pause entitlement management processes](entitlement-management-logic-apps-integration#configuring-custom-extensions-that-pause-entitlement-management-processes).

## Adding Custom Extension to a policy in an existing Access Package

After setting up custom extensibility in the catalog, administrators can create an access package with a policy to trigger the custom extension when the request has been approved. This enables them to define specific access requirements and tailor the access review process to meet their organization's needs.

1. In the Microsoft Entra portal as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator), select **Access packages**.

    Tip

    Other least privilege roles that can complete this task include the Catalog owner and Access package manager.
2. Select the access package you want to add a custom extension (Logic App) to from the list of access packages that have already been created.
3. Change to the policy tab, select the policy, and select **Edit**.
4. In the policy settings, go to the **Custom Extensions** tab.
5. In the menu below **Stage**, select the access package event you wish to use as trigger for this custom extension (Logic App). For our scenario, to trigger the custom extension Logic App workflow when access package has been approved, select **Request is approved**.

    Note

    To create a ServiceNow ticket for an expired assignment that had permission granted previously, add a new stage for "*Assignment is removed*", and then select the LogicApp.
6. In the menu below Custom Extension, select the custom extension (Logic App) you created in the above steps to add to this access package. The action you select executes when the event selected in the *when* field occurs.
7. Select **Update** to add it to an existing access package's policy. [![Screenshot of custom extension details for an access package.](media/entitlement-management-servicenow-integration/entitlement-management-access-package-extension.png)](media/entitlement-management-servicenow-integration/entitlement-management-access-package-extension.png#lightbox)

Note

Select **New access package** if you want to create a new access package. For more information about how to create an access package, see: [Create a new access package in entitlement management](entitlement-management-access-package-create). For more information about how to edit an existing access package, see: [Change request settings for an access package in Microsoft Entra entitlement management](entitlement-management-access-package-request-policy#open-and-edit-an-existing-policys-request-settings).

## Register an application with secrets in the Microsoft Entra admin center

With Azure, you're able to use [Azure Key Vault](/en-us/azure/key-vault/secrets/about-secrets) to store application secrets such as passwords. To register an application with secrets within the Microsoft Entra admin center, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Under Manage, select App registrations &gt; New registration.
4. Enter a display Name for your application.
5. Select "Accounts in this organizational directory only" in supported account type.
6. Select Register.

After registering your application, you must add a client secret by following these steps:

1. Browse to **Entra ID** &gt; **App registrations**.
2. select your application.
3. Select Certificates & secrets &gt; Client secrets &gt; New client secret.
4. Add a description for your client secret.
5. Select an expiration for the secret or specify a custom lifetime.
6. Select Add.

Note

To find more detailed information on registering an application, see: [Quickstart: Register an app in the Microsoft identity platform](../identity-platform/quickstart-register-app):

To authorize the created application to call the [MS Graph resume API](/en-us/graph/api/accesspackageassignmentrequest-resume) you'd do the following steps:

1. Navigate to the Microsoft Entra admin center [Identity Governance - Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_ERM/DashboardBlade/%7E/elmEntitlement)
2. In the left menu, select **Catalogs**.
3. Select the catalog for which you have added the custom extension.
4. Select “Roles and administrators” menu and select “+ Add access package assignment manager”.
5. In the Select members dialog box, search for the application created by name or application Identifier. Select the application and choose the *“Select”* button.

Tip

You can find more detailed information on delegation and roles on Microsoft’s official documentation located here: [Delegation and roles in entitlement management](entitlement-management-delegate).

## Configuring ServiceNow for Automation Authentication

At this point it's time to configure ServiceNow for resuming the entitlement management workflow after the ServiceNow ticket closure:

1. Register a Microsoft Entra application in the ServiceNow Application Registry by following these steps:
    1. Sign in to ServiceNow and navigate to the Application Registry.
    2. Select “*New*” and then select “**Connect to a third party OAuth Provider**”.
    3. Provide a name for the application, and select Client Credentials in the Default Grant type.
    4. Enter the Client Name, ID, Client Secret, Authorization URL, Token URL that were generated when you registered the Microsoft Entra application in the Microsoft Entra admin center.
    5. Submit the application. [![Screenshot of the application registry within ServiceNow.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-application-registry.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-application-registry.png#lightbox)
2. Create a System Web Service REST API message by following these steps:
    1. Go to the REST API Messages section under System Web Services.
    2. Select the "New" button to create a new REST API message.
    3. Fill in all the required fields, which include providing the Endpoint URL: `https://learn.microsoft.com/en-us/graph/api/accesspackageassignmentrequest-resume?view=graph-rest-1.0&tabs=http`
    4. For the required header: Content Type: `application/json`
    5. For Authentication, select OAuth2.0 and choose the OAuth profile that was created during the app registration process.
    6. Select the "*Submit*" button to save the changes.
    7. Go back to the REST API Messages section under System Web Services.
    8. Select Http Request and then select "*New*". Enter a name, and select "POST" as the Http method.
    9. In the Http request, add the content for the Http query parameters using the following API Schema:

        ```http
        {
        "data": {
            "@odata.type": "#microsoft.graph.accessPackageAssignmentRequestCallbackData",
            "customExtensionStageInstanceDetail": "Resuming-Assignment for user",
            "customExtensionStageInstanceId": "${StageInstanceId}",
            "stage": "${Stage}"
                  },
                  "source": "ServiceNow",
                    "type": "microsoft.graph.accessPackageCustomExtensionStage.${Stage}"
                    }
        ```
    10. Select "*Submit*" to save the changes. [![Screenshot of resume call selection within ServiceNow.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-resume-call.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-resume-call.png#lightbox)

        [![Screenshot of the http request within ServiceNow.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-request-call.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-request-call.png#lightbox)
3. Modify the request table schema: To modify the request table schema, make changes to the three tables shown in the following image: [![Screenshot of the request table schema within ServiceNow.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-request-table-schema.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-request-table-schema.png#lightbox)Add the four column label and type as string:
    - AccessPackageAssignmentRequestId
    - AccessPackageAssignmentStage
    - StageInstanceId
    - EntraUserObjectId
4. To automate workflow with Flow Designer, you'd do the following steps:
    1. Sign in to ServiceNow and go to Flow Designer.
    2. Select the “*New*” button and create a new action.
    3. Add an action to invoke the System Web Service REST API message that was created in the previous step. [![Screenshot of flow designer script to resume entitlement management process within ServiceNow.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer.png#lightbox) Script for the action: (Update the script with the Column labels created in previous step): 

        ```
        (function execute(inputs, outputs) {
            gs.info("AccessPackageAssignmentRequestId: " + inputs['accesspkgassignmentrequestid']);
            gs.info("StageInstanceId: " + inputs['customextensionstageinstanceid'] );
            gs.info("Stage: " + inputs['assignmentstage']);
            var r = new sn_ws.RESTMessageV2('Resume ELM WorkFlow', 'RESUME');
            r.setStringParameterNoEscape('AccessPackageAssignmentRequestId', inputs['accesspkgassignmentrequestid']);
            r.setStringParameterNoEscape('StageInstanceId', inputs['customextensionstageinstanceid'] );
            r.setStringParameterNoEscape('Stage', inputs['assignmentstage']);
            var response = r.execute();
            var responseBody = response.getBody();
            var httpStatus = response.getStatusCode();
            var requestBody =  r.getRequestBody();
            gs.info("requestBody: " + requestBody);
            gs.info("responseBody: " + responseBody);
            gs.info("httpStatus: " + httpStatus);
            })(inputs, outputs); 
        ```
    4. Save the Action
    5. Select the "*New*" button to create a new flow.
    6. Enter flow name, select Run as – System User and select submit.
5. To create triggers within ServiceNow, you'd follow these steps:
    1. Select "*Add Trigger*" and then select "*updated*" trigger and run the trigger for every update.
    2. Add a filter condition by updating the condition as shown in the following image: [![Screenshot of ServiceNow call entitlement management resume API](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-call-elm-assignment.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-call-elm-assignment.png#lightbox)
    3. Select done.
    4. Select add an action [![Screenshot of flow diagram trigger.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer-trigger.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer-trigger.png#lightbox)
    5. Select the Action and then select the action created in the previous step. [![Screenshot of flow designer actions selection.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer-actions.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer-actions.png#lightbox)
    6. Drag and drop the newly created columns from the request record to the appropriate action parameters.
    7. Select “Done”, “Save” and then “Activate”. [![Screenshot of save and activate within flow designer.](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer-save.png)](media/entitlement-management-servicenow-integration/entitlement-management-servicenow-flow-designer-save.png#lightbox)

## Requesting access to an access package as an end-user

When an end user requests access to an access package, the request is sent to the appropriate approver. Once the approver grants approval, Entitlement Management calls the Logic App. The Logic app then calls ServiceNow to create a new request/ticket and Entitlement Management awaits a callback from ServiceNow.

[![Screenshot of requesting an access package.](media/entitlement-management-servicenow-integration/entitlement-management-request-access-package.png)](media/entitlement-management-servicenow-integration/entitlement-management-request-access-package.png#lightbox)

## Receiving access to the requested access package as an end-user

The IT Support team works on the previous ticket created to do necessary provisions, and close the ServiceNow ticket. When the ticket is closed, ServiceNow triggers a call to resume the Entitlement Management workflow. Once the request is completed, the requestor receives a notification from entitlement management that the request has been fulfilled. This streamlined workflow ensures that access requests are fulfilled efficiently, and users are notified promptly.

[![Screenshot of My Access request history.](media/entitlement-management-servicenow-integration/entitlement-management-myaccess-request-history.png)](media/entitlement-management-servicenow-integration/entitlement-management-myaccess-request-history.png#lightbox)

Note

The end user sees "assignment failed" in the MyAccess portal if the ticket isn't closed within 14 days.