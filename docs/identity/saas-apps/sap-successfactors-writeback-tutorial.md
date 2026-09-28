---
layout: Conceptual
title: Configure SAP SuccessFactors writeback in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sap-successfactors-writeback-tutorial
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
description: Learn how to configure attribute write-back to SAP SuccessFactors from Microsoft Entra ID
ms.topic: how-to
ms.date: 2024-05-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: ed074cb3-7c71-0728-10d5-d1f991162e67
document_version_independent_id: 0ed1eddb-f8d2-172b-0cc5-ed5f94a9b1e6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sap-successfactors-writeback-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sap-successfactors-writeback-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sap-successfactors-writeback-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 78cfed86-f317-8994-4eeb-cca0336ecdc4
---

# Configure SAP SuccessFactors writeback in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show the steps to write-back attributes from Microsoft Entra ID to SAP SuccessFactors Employee Central.

## Overview

You can configure the SAP SuccessFactors Writeback app to write specific attributes from Microsoft Entra ID to SAP SuccessFactors Employee Central. The SuccessFactors writeback provisioning app supports assigning values to the following Employee Central attributes:

- Work Email
- Username
- Business phone number (including country code, area code, number, and extension)
- Business phone number primary flag
- Cell phone number (including country code, area code, number)
- Cell phone primary flag
- User custom01-custom15 attributes
- loginMethod attribute

Note

This app doesn't have any dependency on the SuccessFactors inbound user provisioning integration apps. You can configure it independent of [SuccessFactors to on-premises AD](sap-successfactors-inbound-provisioning-tutorial) provisioning app or [SuccessFactors to Microsoft Entra ID](sap-successfactors-inbound-provisioning-cloud-only-tutorial) provisioning app.

Refer to the [Writeback scenarios section](../app-provisioning/sap-successfactors-integration-reference#writeback-scenarios) of the SAP SuccessFactors integration reference guide for more details on the supported scenarios, known issues and limitations.

### Who is this user provisioning solution best suited for?

This SuccessFactors Writeback user provisioning solution is ideally suited for:

- Organizations using Microsoft 365 that desire to write-back authoritative attributes managed by IT (such as email address, phone, username) back to SuccessFactors Employee Central.

## Configuring SuccessFactors for the integration

All SuccessFactors provisioning connectors require credentials of a SuccessFactors account with the right permissions to invoke the Employee Central OData APIs. The following procedure describes how to create the service account in SuccessFactors and grant the required permissions.

- Create/identify API user account in SuccessFactors
- Create an API permissions role
- Create a Permission Group for the API user
- Grant Permission Role to the Permission Group

### Create/identify API user account in SuccessFactors

Work with your SuccessFactors admin team or implementation partner to create or identify a user account in SuccessFactors to invoke the OData APIs. The username and password credentials of this account are required when configuring the provisioning apps in Microsoft Entra ID.

### Create an API permissions role

Perform the following steps to create an API permissions role in SuccessFactors:

1. Log in to SAP SuccessFactors with a user account that has access to the Admin Center.
2. Search for *Manage Permission Roles*, then select **Manage Permission Roles** from the search results.

    ![Manage Permission Roles](media/sap-successfactors-inbound-provisioning/manage-permission-roles.png)
3. From the Permission Role List, select **Create New**.

![Create New Permission Role](media/sap-successfactors-inbound-provisioning/create-new-permission-role-1.png)
4. Add a **Role Name** and **Description** for the new permission role. The name and description should indicate that the role is for API usage permissions.
5. Under Permission settings, select **Permission...**, then scroll down the permission list and select **Manage Integration Tools**. Check the box for **Allow Admin to Access to OData API through Basic Authentication**.

![Manage integration tools](media/sap-successfactors-inbound-provisioning/manage-integration-tools.png)
6. Scroll down in the same box and select **Employee Central API**. Add permissions as shown below to read using ODATA API and edit using ODATA API. Select the edit option if you plan to use the same account for the write-back to SuccessFactors scenario.

![Read write permissions](media/sap-successfactors-inbound-provisioning/odata-read-write-perm.png)
7. Select **Done**. Select **Save Changes**.

### Create a Permission Group for the API user

Perform the following steps to create a permission group for the API user:

1. In the SuccessFactors Admin Center, search for *Manage Permission Groups*, then select **Manage Permission Groups** from the search results.

![Manage permission groups](media/sap-successfactors-inbound-provisioning/manage-permission-groups.png)
2. From the Manage Permission Groups window, select **Create New**.

![Add new group](media/sap-successfactors-inbound-provisioning/create-new-group.png)
3. Add a Group Name for the new group. The group name should indicate that the group is for API users.

![Permission group name](media/sap-successfactors-inbound-provisioning/permission-group-name.png)
4. Add members to the group. For example, you could select **Username** from the People Pool drop-down menu and then enter the username of the API account that's used for the integration.

![Add group members](media/sap-successfactors-inbound-provisioning/add-group-members.png)
5. Select **Done** to finish creating the Permission Group.

### Grant Permission Role to the Permission Group

Perform the following steps to grant the permission role to the permission group:

1. In SuccessFactors Admin Center, search for *Manage Permission Roles*, then select **Manage Permission Roles** from the search results.
2. From the **Permission Role List**, select the role that you created for API usage permissions.
3. Under **Grant this role to...**, select **Add...** Button.
4. Select **Permission Group...** from the drop-down menu, then select **Select...** to open the Groups window to search and select the group created above.
5. Review the Permission Role grant to the Permission Group.
6. Select **Save Changes**.

## Preparing for SuccessFactors Writeback

The SuccessFactors Writeback provisioning app uses certain *code* values for setting email and phone numbers in Employee Central. These *code* values are set as constant values in the attribute-mapping table and are different for each SuccessFactors instance. The following procedure explains how to capture these *code* values for use in the attribute-mapping table.

Note

Please involve your SuccessFactors Admin to complete the steps in this section.

### Identify Email and Phone Number picklist names

In SAP SuccessFactors, a *picklist* is a configurable set of options from which a user can make a selection. The different types of email and phone number (such as business, personal, and other) are represented using a picklist. The following procedure identifies the picklists configured in your SuccessFactors tenant to store email and phone number values.

1. In SuccessFactors Admin Center, search for *Manage business configuration*.

![Manage business configuration](media/sap-successfactors-inbound-provisioning/manage-business-config.png)
2. Under **HRIS Elements**, select **emailInfo** and select the *Details* for the **email-type** field.

![Get email info](media/sap-successfactors-inbound-provisioning/get-email-info.png)
3. On the **email-type** details page, note down the name of the picklist associated with this field. By default, it's **ecEmailType**. However it may be different in your tenant.

![Identify email picklist](media/sap-successfactors-inbound-provisioning/identify-email-picklist.png)
4. Under **HRIS Elements**, select **phoneInfo** and select the *Details* for the **phone-type** field.

![Get phone info](media/sap-successfactors-inbound-provisioning/get-phone-info.png)
5. On the **phone-type** details page, note down the name of the picklist associated with this field. By default, it's **ecPhoneType**. However it may be different in your tenant.

![Identify phone picklist](media/sap-successfactors-inbound-provisioning/identify-phone-picklist.png)

### Retrieve constant value for emailType

Perform the following steps to retrieve the constant value for emailType:

1. In SuccessFactors Admin Center, search and open *Picklist Center*.
2. Use the name of the email picklist captured in Identify Email and Phone Number picklist names (such as ecEmailType) to find the email picklist.

![Find email type picklist](media/sap-successfactors-inbound-provisioning/find-email-type-picklist.png)
3. Open the active email picklist.

![Open active email type picklist](media/sap-successfactors-inbound-provisioning/open-active-email-type-picklist.png)
4. On the email type picklist page, select the *Business* email type.

![Select business email type](media/sap-successfactors-inbound-provisioning/select-business-email-type.png)
5. Note down the **Option ID** associated with the *Business* email. This is the code that we use with *emailType* in the attribute-mapping table.

![Get email type code](media/sap-successfactors-inbound-provisioning/get-email-type-code.png)

    Note

    Drop the comma character when you copy over the value. For example, if the **Option ID** value is *8,448*, then set the *emailType* in Microsoft Entra ID to the constant number *8448* (without the comma character).

### Retrieve constant value for phoneType

Perform the following steps to retrieve the constant value for phoneType:

1. In SuccessFactors Admin Center, search and open *Picklist Center*.
2. Use the name of the phone picklist captured in Identify Email and Phone Number picklist names to find the phone picklist.

![Find phone type picklist](media/sap-successfactors-inbound-provisioning/find-phone-type-picklist.png)
3. Open the active phone picklist.

![Open active phone type picklist](media/sap-successfactors-inbound-provisioning/open-active-phone-type-picklist.png)
4. On the phone type picklist page, review the different phone types listed under **Picklist Values**.

![Review phone types](media/sap-successfactors-inbound-provisioning/review-phone-types.png)
5. Note down the **Option ID** associated with the *Business* phone. This is the code that we use with *businessPhoneType* in the attribute-mapping table.

![Get business phone code](media/sap-successfactors-inbound-provisioning/get-business-phone-code.png)
6. Note down the **Option ID** associated with the *Cell* phone. This is the code that we use with *cellPhoneType* in the attribute-mapping table.

![Get cell phone code](media/sap-successfactors-inbound-provisioning/get-cell-phone-code.png)

    Note

    Drop the comma character when you copy over the value. For example, if the **Option ID** value is *10,606*, then set the *cellPhoneType* in Microsoft Entra ID to the constant number *10606* (without the comma character).

## Configuring SuccessFactors Writeback App

To configure the SuccessFactors Writeback app, complete the following procedures:

- Add the provisioning connector app and configure connectivity to SuccessFactors
- Configure attribute mappings
- Enable and launch user provisioning

### Part 1: Add the provisioning connector app and configure connectivity to SuccessFactors

**To configure SuccessFactors Writeback:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. Search for **SuccessFactors Writeback**, and add that app from the gallery.
4. After the app is added and the app details screen is shown, select **Provisioning**
5. Change the **Provisioning** **Mode** to **Automatic**
6. Complete the **Admin Credentials** section as follows:

    - **Admin Username** – Enter the username of the SuccessFactors API user account, with the company ID appended. It has the format: **username@companyID**
    - **Admin password –** Enter the password of the SuccessFactors API user account.
    - **Tenant URL –** Enter the name of the SuccessFactors OData API services endpoint. Only enter the host name of server without http or https. This value should look like: `api4.successfactors.com`.
    - **Notification Email –** Enter your email address, and check the "send email if failure occurs" checkbox.

    Note

    The Microsoft Entra provisioning service sends email notification if the provisioning job goes into a [provisioning quarantine](../app-provisioning/application-provisioning-quarantine-status) state.

    - Select the **Test Connection** button. If the connection test succeeds, select the **Save** button at the top. If it fails, double-check that the SuccessFactors credentials and URL are valid.
    - Once the credentials are saved successfully, the **Mappings** section displays the default mapping. Refresh the page, if the attribute mappings aren't visible.

### Part 2: Configure attribute mappings

Configure how user data flows from Microsoft Entra ID to SAP SuccessFactors by defining attribute mappings.

1. On the Provisioning tab under **Mappings**, select **Provision Microsoft Entra users**.
2. In the **Source Object Scope** field, you can select which sets of users in Microsoft Entra ID should be considered for write-back, by defining a set of attribute-based filters. The default scope is **all users in Microsoft Entra ID**.

    Tip

    When you're configuring the provisioning app for the first time, you need to test and verify your attribute mappings and expressions to make sure that it's giving you the desired result. Microsoft recommends using the scoping filters under **Source Object Scope** to test your mappings with a few test users from Microsoft Entra ID. Once you have verified that the mappings work, then you can either remove the filter or gradually expand it to include more users.
3. The **Target Object Actions** field only supports the **Update** operation.
4. In the mapping table under **Attribute mappings** section, you can map the following Microsoft Entra attributes to SuccessFactors. The table below provides guidance on how to map the write-back attributes.

    | # | Microsoft Entra attribute | SuccessFactors Attribute | Remarks |
    | --- | --- | --- | --- |
    | 1 | employeeId | personIdExternal | By default, this attribute is the matching identifier. Instead of employeeId you can use any other Microsoft Entra attribute that may store the value equal to personIdExternal in SuccessFactors. |
    | 2 | mail | email | Map email attribute source. For testing purposes, you can map userPrincipalName to email. |
    | 3 | 8448 | emailType | This constant value is the SuccessFactors ID value associated with business email. Update this value to match your SuccessFactors environment. See the section Retrieve constant value for emailType for steps to set this value. |
    | 4 | true | emailIsPrimary | Use this attribute to set business email as primary in SuccessFactors. If business email isn't primary, set this flag to false. |
    | 5 | userPrincipalName | [custom01 – custom15] | Using **Add New Mapping**, you can optionally write userPrincipalName or any Microsoft Entra attribute to a custom attribute available in the SuccessFactors User object. |
    | 6 | On Prem SamAccountName | username | Using **Add New Mapping**, you can optionally map on-premises samAccountName to SuccessFactors username attribute. Use [Microsoft Entra Connect Sync: Directory extensions](../hybrid/connect/how-to-connect-sync-feature-directory-extensions) to sync samAccountName to Microsoft Entra ID. This appears in the source drop down as *extension\_yourTenantGUID\_samAccountName* |
    | 7 | SSO | loginMethod | If SuccessFactors tenant is setup for partial SSO, then using Add New Mapping, you can optionally set loginMethod to a constant value of "SSO" or "PWD". |
    | 8 | telephoneNumber | businessPhoneNumber | Use this mapping to flow *telephoneNumber* from Microsoft Entra ID to SuccessFactors business / work phone number. |
    | 9 | 10605 | businessPhoneType | This constant value is the SuccessFactors ID value associated with business phone. Update this value to match your SuccessFactors environment. See the section Retrieve constant value for phoneType for steps to set this value. |
    | 10 | true | businessPhoneIsPrimary | Use this attribute to set the primary flag for business phone number. Valid values are true or false. |
    | 11 | mobile | cellPhoneNumber | Use this mapping to flow *telephoneNumber* from Microsoft Entra ID to SuccessFactors business / work phone number. |
    | 12 | 10606 | cellPhoneType | This constant value is the SuccessFactors ID value associated with cell phone. Update this value to match your SuccessFactors environment. See the section Retrieve constant value for phoneType for steps to set this value. |
    | 13 | false | cellPhoneIsPrimary | Use this attribute to set the primary flag for cell phone number. Valid values are true or false. |
    | 14 | [extensionAttribute1-15] | userId | Use this mapping to ensure that the active record in SuccessFactors is updated when there are multiple employment records for the same user. For more details refer to [Enabling writeback with UserID](../app-provisioning/sap-successfactors-integration-reference#enabling-writeback-with-userid) |
5. Validate and review your attribute mappings.
6. Select **Save** to save the mappings. Next, update the JSON Path API expressions to use the phoneType codes in your SuccessFactors instance.
7. Select **Show advanced options**.
8. Select **Edit attribute list for SuccessFactors**.

    Note

    If the **Edit attribute list for SuccessFactors** option doesn't show in the Entra admin center, use the URL *https://portal.azure.com/?Microsoft_AAD_IAM_forceSchemaEditorEnabled=true* to access the page.
9. The **API expression** column in this view displays the JSON Path expressions used by the connector.
10. Update the JSON Path expressions for business phone and cell phone to use the ID value (*businessPhoneType* and *cellPhoneType*) corresponding to your environment.

![Phone JSON Path change](media/sap-successfactors-inbound-provisioning/phone-json-path-change.png)
11. Select **Save** to save the mappings.

## Enable and launch user provisioning

Once the SuccessFactors provisioning app configurations are complete, you can turn on the provisioning service.

Tip

By default when you turn on the provisioning service, it initiates provisioning operations for all users in scope. If there are errors in the mapping or data issues, then the provisioning job might fail and go into the quarantine state. To avoid this, as a best practice, we recommend configuring **Source Object Scope** filter and testing your attribute mappings with a few test users before launching the full sync for all users. Once you have verified that the mappings work and are giving you the desired results, then you can either remove the filter or gradually expand it to include more users.

1. In the **Provisioning** tab, set the **Provisioning Status** to **On**.
2. Select **Scope**. You can select from one of the following options:

    - **Sync all users and groups**: Select this option if you plan to write back mapped attributes of all users from Microsoft Entra ID to SuccessFactors, subject to the scoping rules defined under **Mappings** &gt; **Source Object Scope**.
    - **Sync only assigned users and groups**: Select this option if you plan to write back mapped attributes of only users that you have assigned to this application in the **Application** &gt; **Manage** &gt; **Users and groups** menu option. These users are also subject to the scoping rules defined under **Mappings** &gt; **Source Object Scope**.

![Select Writeback scope](media/sap-successfactors-inbound-provisioning/select-writeback-scope.png)

    Note

    SuccessFactors Writeback provisioning apps created after 12-Oct-2022 support the "group assignment" feature. If you created the app prior to 12-Oct-2022, it only has "user assignment" support. To use the "group assignment" feature, create a new instance of the SuccessFactors Writeback application and move your existing mapping configurations to this app.
3. Select **Save**.
4. This operation starts the initial sync, which can take a variable number of hours depending on how many users are in the Microsoft Entra tenant and the scope defined for the operation. You can check the progress bar to the track the progress of the sync cycle.
5. At any time, check the **Provisioning logs** tab in the Entra admin center to see what actions the provisioning service has performed. The provisioning logs lists all individual sync events performed by the provisioning service.
6. Once the initial sync is completed, it writes an audit summary report in the **Provisioning** tab, as shown below.

![Provisioning progress bar](media/sap-successfactors-inbound-provisioning/prov-progress-bar-stats.png)