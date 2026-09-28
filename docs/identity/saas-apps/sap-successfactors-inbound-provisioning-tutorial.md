---
layout: Conceptual
title: Configure SuccessFactors inbound provisioning in AD and Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sap-successfactors-inbound-provisioning-tutorial
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
description: Learn how to configure inbound provisioning from SuccessFactors
ms.topic: how-to
ms.date: 2024-05-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 90fd487d-65b9-917b-4687-650b34dc4d81
document_version_independent_id: 27a18d45-66ab-bc71-d928-93f93fb190dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sap-successfactors-inbound-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sap-successfactors-inbound-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sap-successfactors-inbound-provisioning-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 263f8d78-cac3-0d96-6751-7040334bfe3e
---

# Configure SuccessFactors inbound provisioning in AD and Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to show the steps you need to perform to provision users from SuccessFactors Employee Central into Active Directory (AD) and Microsoft Entra ID, with optional write-back of email address to SuccessFactors.

Note

Use this article if the users you want to provision from SuccessFactors need an on-premises AD account and optionally a Microsoft Entra account. If the users from SuccessFactors only need Microsoft Entra account (cloud-only users), then please refer to the article on [configure SAP SuccessFactors to Microsoft Entra ID](sap-successfactors-inbound-provisioning-cloud-only-tutorial) user provisioning.

The following video provides a quick overview of the steps involved when planning your provisioning integration with SAP SuccessFactors.

## Overview

The [Microsoft Entra user provisioning service](../app-provisioning/user-provisioning) integrates with the [SuccessFactors Employee Central](https://www.successfactors.com/products-services/core-hr-payroll/employee-central.html) in order to manage the identity life cycle of users.

The SuccessFactors user provisioning workflows supported by the Microsoft Entra user provisioning service enable automation of the following human resources and identity lifecycle management scenarios:

- **Hiring new employees** - When a new employee is added to SuccessFactors, a user account is automatically created in Active Directory, Microsoft Entra ID, and optionally Microsoft 365 and [other SaaS applications supported by Microsoft Entra ID](../app-provisioning/user-provisioning), with write-back of the email address to SuccessFactors.
- **Employee attribute and profile updates** - When an employee record is updated in SuccessFactors (such as their name, title, or manager), their user account is automatically updated in Active Directory, Microsoft Entra ID, and optionally Microsoft 365 and [other SaaS applications supported by Microsoft Entra ID](../app-provisioning/user-provisioning).
- **Employee terminations** - When an employee is terminated in SuccessFactors, their user account is automatically disabled in Active Directory, Microsoft Entra ID, and optionally Microsoft 365 and [other SaaS applications supported by Microsoft Entra ID](../app-provisioning/user-provisioning).
- **Employee rehires** - When an employee is rehired in SuccessFactors, their old account can be automatically reactivated or re-provisioned (depending on your preference) to Active Directory, Microsoft Entra ID, and optionally Microsoft 365 and [other SaaS applications supported by Microsoft Entra ID](../app-provisioning/user-provisioning).

### Who is this user provisioning solution best suited for?

This SuccessFactors to Active Directory user provisioning solution is ideally suited for:

- Organizations that desire a pre-built, cloud-based solution for SuccessFactors user provisioning, including organizations that are populating SuccessFactors from SAP HCM using SAP Integration Suite
- Organizations that's [deploying Microsoft Entra for user provisioning with SAP source and target apps](../app-provisioning/plan-sap-user-source-and-target), using Microsoft Entra to set up identities for workers so they can sign in to one or more SAP applications, such as SAP ECC or SAP S/4HANA, and optionally non-SAP applications
- Organizations that require direct user provisioning from SuccessFactors to Active Directory so that users can access Windows Server Active Directory-integrated applications and Microsoft Entra ID integrated applications
- Organizations that require users to be provisioned using data obtained from the [SuccessFactors Employee Central (EC)](https://www.successfactors.com/products-services/core-hr-payroll/employee-central.html)
- Organizations that require joining, moving, and leaving users to be synced to one or more Active Directory Forests, Domains, and OUs based only on change information detected in [SuccessFactors Employee Central (EC)](https://www.successfactors.com/products-services/core-hr-payroll/employee-central.html)
- Organizations using Microsoft 365 for email

## Solution Architecture

This section describes the end-to-end user provisioning solution architecture for common hybrid environments. There are two related flows:

- **Authoritative HR Data Flow – from SuccessFactors to on-premises Active Directory:** In this flow worker events (such as New Hires, Transfers, Terminations) first occur in the cloud SuccessFactors Employee Central and then the event data flows into on-premises Active Directory through Microsoft Entra ID and the Provisioning Agent. Depending on the event, it may lead to create/update/enable/disable operations in AD.
- **Email Writeback Flow – from on-premises Active Directory to SuccessFactors:** Once the account creation is complete in Active Directory, it's synced with Microsoft Entra ID through Microsoft Entra Connect Sync and email attribute can be written back to SuccessFactors.

    ![Overview](media/sap-successfactors-inbound-provisioning/sf2ad-overview.png)

### End-to-end user data flow

1. The HR team performs worker transactions (Joiners/Movers/Leavers or New Hires/Transfers/Terminations) in SuccessFactors Employee Central.
2. The Microsoft Entra provisioning service runs scheduled synchronizations of identities from SuccessFactors EC and identifies changes that need to be processed for sync with on-premises Active Directory.
3. The Microsoft Entra provisioning service invokes the on-premises Microsoft Entra Connect Provisioning Agent with a request payload containing AD account create/update/enable/disable operations.
4. The Microsoft Entra Connect Provisioning Agent uses a service account to add/update AD account data.
5. The Microsoft Entra Connect Sync engine runs delta sync to pull updates in AD.
6. The Active Directory updates are synced with Microsoft Entra ID.
7. If the [SuccessFactors Writeback app](sap-successfactors-writeback-tutorial) is configured, it writes back email attribute to SuccessFactors, based on the matching attribute used.

## Planning your deployment

Configuring Cloud HR driven user provisioning from SuccessFactors to AD requires considerable planning covering different aspects such as:

- Setup of the Microsoft Entra Connect provisioning agent
- Number of SuccessFactors to AD user provisioning apps to deploy
- Matching ID, Attribute mapping, transformation and scoping filters

Please refer to the [cloud HR deployment plan](../app-provisioning/plan-cloud-hr-provision) for comprehensive guidelines around these topics. Please refer to the [SAP SuccessFactors integration reference](../app-provisioning/sap-successfactors-integration-reference) to learn about the supported entities, processing details and how to customize the integration for different HR scenarios.

## Configuring SuccessFactors for the integration

A common requirement of all the SuccessFactors provisioning connectors is that they require credentials of a SuccessFactors account with the right permissions to invoke the SuccessFactors OData APIs. This section describes steps to create the service account in SuccessFactors and grant appropriate permissions.

- Create/identify API user account in SuccessFactors
- Create an API permissions role
- Create a Permission Group for the API user
- Grant Permission Role to the Permission Group

### Create/identify API user account in SuccessFactors

Work with your SuccessFactors admin team or implementation partner to create or identify a user account in SuccessFactors to invoke the OData APIs. The username and password credentials of this account are required when configuring the provisioning apps in Microsoft Entra ID.

### Create an API permissions role

1. Log in to SAP SuccessFactors with a user account that has access to the Admin Center.
2. Search for *Manage Permission Roles*, then select **Manage Permission Roles** from the search results. ![Manage Permission Roles](media/sap-successfactors-inbound-provisioning/manage-permission-roles.png)
3. From the Permission Role List, select **Create New**.

![Create New Permission Role](media/sap-successfactors-inbound-provisioning/create-new-permission-role-1.png)
4. Add a **Role Name** and **Description** for the new permission role. The name and description should indicate that the role is for API usage permissions.
5. Under Permission settings, select **Permission...**, then scroll down the permission list and select **Manage Integration Tools**. Check the box for **Allow Admin to Access to OData API through Basic Authentication**.

![Manage integration tools](media/sap-successfactors-inbound-provisioning/manage-integration-tools.png)
6. Scroll down in the same box and select **Employee Central API**. Add permissions as shown below to read using ODATA API and edit using ODATA API. Select the edit option if you plan to use the same account for the Writeback to SuccessFactors scenario.

![Read write permissions](media/sap-successfactors-inbound-provisioning/odata-read-write-perm.png)
7. In the same permissions box, go to **User Permissions -&gt; Employee Data** and review the attributes that the service account can read from the SuccessFactors tenant. For example, to retrieve the *Username* attribute from SuccessFactors, ensure that "View" permission is granted for this attribute. Similarly review each attribute for view permission.

![Employee data permissions](media/sap-successfactors-inbound-provisioning/review-employee-data-permissions.png)

    Note

    For the complete list of attributes retrieved by this provisioning app, please refer to [SuccessFactors Attribute Reference](../app-provisioning/sap-successfactors-attribute-reference)
8. Select **Done**. Select **Save Changes**.

### Create a Permission Group for the API user

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

1. In SuccessFactors Admin Center, search for *Manage Permission Roles*, then select **Manage Permission Roles** from the search results.
2. From the **Permission Role List**, select the role that you created for API usage permissions.
3. Under **Grant this role to...**, select the **Add...** button.
4. Select **Permission Group...** from the drop-down menu, then select **Select...** to open the Groups window to search and select the group created above.
5. Review the Permission Role grant to the Permission Group.
6. Select **Save Changes**.

## Configuring user provisioning from SuccessFactors to Active Directory

This section provides steps for user account provisioning from SuccessFactors to each Active Directory domain within the scope of your integration.

- Add the provisioning connector app and download the Provisioning Agent
- Install and configure on-premises Provisioning Agent(s)
- Configure connectivity to SuccessFactors and Active Directory
- Configure attribute mappings
- Enable and launch user provisioning

### Part 1: Add the provisioning connector app and download the Provisioning Agent

**To configure SuccessFactors to Active Directory provisioning:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. Search for **SuccessFactors to Active Directory User Provisioning**, and add that app from the gallery.
4. After the app is added and the app details screen is shown, select **Provisioning**
5. Change the **Provisioning** **Mode** to **Automatic**
6. Select the information banner displayed to download the Provisioning Agent.

![Screenshot of provisioning agent informational.](../../includes/governance/media/workday-inbound-tutorial/pa-download-agent.png)

### Part 2: Install and configure on-premises Provisioning Agent(s)

To provision to Active Directory on-premises, the Provisioning agent must be installed on a domain-joined server that has network access to the desired Active Directory domain(s).

Transfer the downloaded agent installer to the server host and follow the steps listed [in the install agent section](/en-us/azure/active-directory/cloud-sync/how-to-install) to complete the agent configuration.

### Part 3: In the provisioning app, configure connectivity to SuccessFactors and Active Directory

In this step, we establish connectivity with SuccessFactors and Active Directory.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; SuccessFactors to Active Directory User Provisioning App created in Part 1
3. Complete the **Admin Credentials** section as follows:

    - **Admin Username** – Enter the username of the SuccessFactors API user account, with the company ID appended. It has the format: **username@companyID**
    - **Admin password –** Enter the password of the SuccessFactors API user account.
    - **Tenant URL –** Enter the name of the SuccessFactors OData API services endpoint. Only enter the host name of server without http or https. This value should look like: **&lt;api-server-name&gt;.successfactors.com**.
    - **Active Directory Forest -** The "Name" of your Active Directory domain, as registered with the agent. Use the dropdown to select the target domain for provisioning. This value is typically a string like: *contoso.com*
    - **Active Directory Container -** Enter the container DN where the agent should create user accounts by default. Example: *OU=Users,DC=contoso,DC=com*

        Note

        This setting only comes into play for user account creations if the *parentDistinguishedName* attribute isn't configured in the attribute mappings. This setting isn't used for user search or update operations. The entire domain sub tree falls in the scope of the search operation.
    - **Notification Email –** Enter your email address, and check the "send email if failure occurs" checkbox.

        Note

        The Microsoft Entra provisioning service sends email notification if the provisioning job goes into a [quarantine](../app-provisioning/application-provisioning-quarantine-status) state.
    - Select the **Test Connection** button. If the connection test succeeds, select the **Save** button at the top. If it fails, double-check that the SuccessFactors credentials and the AD credentials configured on the agent setup are valid.
    - Once the credentials are saved successfully, the **Mappings** section displays the default mapping **Synchronize SuccessFactors Users to On Premises Active Directory**

### Part 4: Configure attribute mappings

In this section, you configure how user data flows from SuccessFactors to Active Directory.

1. On the Provisioning tab under **Mappings**, select **Synchronize SuccessFactors Users to On Premises Active Directory**.
2. In the **Source Object Scope** field, you can select which sets of users in SuccessFactors should be in scope for provisioning to AD, by defining a set of attribute-based filters. The default scope is **all users in SuccessFactors**. Example filters:

    - Example: Scope to users with personIdExternal between 1000000 and 2000000 (excluding 2000000)

        - Attribute: personIdExternal
        - Operator: REGEX Match
        - Value: (1[0-9][0-9][0-9][0-9][0-9][0-9])
    - Example: Only employees and not contingent workers

        - Attribute: EmployeeID
        - Operator: IS NOT NULL

    Tip

    When you're configuring the provisioning app for the first time, you need to test and verify your attribute mappings and expressions to make sure that it's giving you the desired result. Microsoft recommends using the scoping filters under **Source Object Scope** to test your mappings with a few test users from SuccessFactors. Once you have verified that the mappings work, then you can either remove the filter or gradually expand it to include more users.

Caution

The default behavior of the provisioning engine is to disable/delete users that go out of scope. This may not be desirable in your SuccessFactors to AD integration. To override this default behavior refer to the article [Skip deletion of user accounts that go out of scope](../app-provisioning/skip-out-of-scope-deletions)
3. In the **Target Object Actions** field, you can globally filter what actions are performed on Active Directory. **Create** and **Update** are most common.
4. In the **Attribute mappings** section, you can define how individual SuccessFactors attributes map to Active Directory attributes.

    Note

    For the complete list of SuccessFactors attribute supported by the application, please refer to [SuccessFactors Attribute Reference](../app-provisioning/sap-successfactors-attribute-reference)
5. Select an existing attribute mapping to update it, or select **Add new mapping** at the bottom of the screen to add new mappings. An individual attribute mapping supports these properties:

    - **Mapping Type**

        - **Direct** – Writes the value of the SuccessFactors attribute to the AD attribute, with no changes
        - **Constant** - Write a static, constant string value to the AD attribute
        - **Expression** – Allows you to write a custom value to the AD attribute, based on one or more SuccessFactors attributes. [For more info, see this article on expressions](../app-provisioning/functions-for-customizing-application-data).
    - **Source attribute** - The user attribute from SuccessFactors
    - **Default value** – Optional. If the source attribute has an empty value, the mapping will write this value instead. Most common configuration is to leave this blank.
    - **Target attribute** – The user attribute in Active Directory.
    - **Match objects using this attribute** – Whether or not this mapping should be used to uniquely identify users between SuccessFactors and Active Directory. This value is typically set on the Worker ID field for SuccessFactors, which is typically mapped to one of the Employee ID attributes in Active Directory.
    - **Matching precedence** – Multiple matching attributes can be set. When there are multiple, they are evaluated in the order defined by this field. As soon as a match is found, no further matching attributes are evaluated.
    - **Apply this mapping**

        - **Always** – Apply this mapping on both user creation and update actions
        - **Only during creation** - Apply this mapping only on user creation actions
6. To save your mappings, select **Save** at the top of the Attribute-Mapping section.

Once your attribute mapping configuration is complete, you can test provisioning for a single user using [on-demand provisioning](../app-provisioning/provision-on-demand) and then enable and launch the user provisioning service.

## Enable and launch user provisioning

Once the SuccessFactors provisioning app configurations are complete and you have verified provisioning for a single user with [on-demand provisioning](../app-provisioning/provision-on-demand), you can turn on the provisioning service.

Tip

By default when you turn on the provisioning service, it initiates provisioning operations for all users in scope. If there are errors in the mapping or SuccessFactors data issues, then the provisioning job might fail and go into the quarantine state. To avoid this, as a best practice, we recommend configuring **Source Object Scope** filter and testing your attribute mappings with a few test users using [on-demand provisioning](../app-provisioning/provision-on-demand) before launching the full sync for all users. Once you have verified that the mappings work and are giving you the desired results, then you can either remove the filter or gradually expand it to include more users.

1. Go to the **Provisioning** blade and select **Start provisioning**.
2. This operation starts the initial sync, which can take a variable number of hours depending on how many users are in the SuccessFactors tenant. You can check the progress bar to the track the progress of the sync cycle.
3. At any time, check the **Provisioning** tab in the Entra admin center to see what actions the provisioning service has performed. The provisioning logs lists all individual sync events performed by the provisioning service, such as which users are being read out of SuccessFactors and then subsequently added or updated to Active Directory.
4. Once the initial sync is completed, it writes an audit summary report in the **Provisioning** tab, as shown below.

![Provisioning progress bar](media/sap-successfactors-inbound-provisioning/prov-progress-bar-stats.png)