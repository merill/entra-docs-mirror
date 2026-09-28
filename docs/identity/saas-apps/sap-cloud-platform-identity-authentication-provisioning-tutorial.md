---
layout: Conceptual
title: Configure SAP Cloud Identity Services for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sap-cloud-platform-identity-authentication-provisioning-tutorial
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
description: Learn how to configure Microsoft Entra ID to automatically provision and deprovision user accounts to SAP Cloud Identity Services.
ms.topic: how-to
ms.date: 2026-04-20T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8e8629d0-8a5c-64ba-46f2-f8caa51b9126
document_version_independent_id: 9eab5faf-da99-3fca-d7fd-a2814c72b136
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sap-cloud-platform-identity-authentication-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: msgraph
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sap-cloud-platform-identity-authentication-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sap-cloud-platform-identity-authentication-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7e5a7a74-c7a7-708c-ee45-4717faeff7cd
---

# Configure SAP Cloud Identity Services for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article demonstrates the steps for configuring provisioning from Microsoft Entra ID to SAP Cloud Identity Services. The goal is to set up Microsoft Entra ID to automatically provision and deprovision users to SAP Cloud Identity Services, so that those users can authenticate to SAP Cloud Identity Services and have access to other SAP workloads. SAP Cloud Identity Services supports provisioning from its local identity directory to other SAP applications as [target systems](https://help.sap.com/docs/identity-provisioning/identity-provisioning/target-systems).

Note

This article describes a connector built in the Microsoft Entra user provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning). SAP Cloud Identity Services also has its own separate connector to read users and groups from Microsoft Entra ID. For more information, see [SAP Cloud Identity Services - Identity Provisioning - Microsoft Entra ID as a source system](https://help.sap.com/docs/identity-provisioning/identity-provisioning/microsoft-azure-active-directory).

Note

A new version of the SAP Cloud Identity Services connector is Generally Available and is now the default for the SAP Cloud Identity Services listing in the Microsoft Entra app gallery. This current version of the connector features the following changes:

- Updated to the SCIM 2.0 standard
- Support for group provisioning and deprovisioning to SAP Cloud Identity Services
- Support for custom extension attributes
- Support for the [OAuth 2.0 Client Credentials grant](../../identity-platform/v2-oauth2-client-creds-grant-flow)

Important

If [integrating with SAP IAG](../../id-governance/entitlement-management-sap-integration), map Microsoft Entra ObjectId to username by selecting *EDIT* in the username line and set the Source and Target attribute as:

- Source Attribute: objectId
- Target Attribute: userName

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [An SAP Cloud Identity Services tenant](https://www.sap.com/products/cloud-platform.html)
- A user account in SAP Cloud Identity Services with Admin permissions.
- A Microsoft Entra ID P1 license is required to use group provisioning capabilities.

Note

This integration is also available to use from the Microsoft Entra US Government Cloud environment. You can find this application in the Microsoft Entra US Government Cloud Application Gallery and configure it in the same way as you do from the public cloud environment.

If you don't yet have users in Microsoft Entra ID, then start with the article [plan deploying Microsoft Entra for user provisioning with SAP source and target apps](../app-provisioning/plan-sap-user-source-and-target). That article illustrates how to connect Microsoft Entra with authoritative sources for the list of workers in an organization, such as SAP SuccessFactors. It also shows you how to use Microsoft Entra to set up identities for those workers, so they can sign in to one or more SAP applications, such as SAP ECC or SAP S/4HANA.

If you're configuring provisioning into SAP Cloud Identity Services in a production environment, where you are governing access to SAP workloads using Microsoft Entra ID Governance, then review the [prerequisites before configuring Microsoft Entra ID for identity governance](../../id-governance/identity-governance-applications-prepare#prerequisites-before-configuring-microsoft-entra-id-and-microsoft-entra-id-governance-for-identity-governance) before proceeding.

## Set up SAP Cloud Identity Services for provisioning

In this article, you add an admin system in SAP Cloud Identity Services and then configure Microsoft Entra.

![Screenshot of the architecture of SSO and provisioning flow between SAP applications, SAP Cloud Identity Services and Microsoft Entra.](media/sap-cloud-platform-identity-authentication-provisioning-tutorial/architecture.png)

1. Sign in to your SAP Cloud Identity Services Admin Console, `https://<tenantID>.accounts.ondemand.com/admin` or `https://<tenantID>.trial-accounts.ondemand.com/admin` if a trial. Navigate to **Users & Authorizations &gt; Administrators**.

    ![Screenshot of the SAP Cloud Identity Services Admin Console.](media/sap-cloud-platform-identity-authentication-provisioning-tutorial/admin-console.png)
2. Press the **+Add** button on the left hand panel in order to add a new administrator to the list. Choose **Add System** and enter the name of the system.

    Note

    The administrator identity in SAP Cloud Identity Services must be of type **System**. An administrator user isn't able to authenticate to the SAP SCIM API when provisioning. SAP Cloud Identity Services doesn't allow the name of a system to be changed after it's created.
3. Under Configure Authorizations, switch on the toggle button against **Manage Users**. Then select **Save** to create the system.

    ![Screenshot of the SAP Cloud Identity Services Add SCIM.](media/sap-cloud-platform-identity-authentication-provisioning-tutorial/configuration-auth.png)
4. After the administrator system is created, add a new secret to that system.
5. Copy the **Client ID** and **Client Secret** that's generated by SAP. These values are entered in the Admin Username and Admin Password fields respectively. Enter these values in the Provisioning tab of your SAP Cloud Identity Services application, which you set up in the next section.
6. SAP Cloud Identity Services may have mappings to one or more SAP applications as target systems. Check if there are any attributes on the users that those SAP applications require to be provisioned through SAP Cloud Identity Services. This article assumes SAP Cloud Identity Services and downstream target systems require two attributes, `userName` and `emails[type eq "work"].value`. If your SAP target systems require other attributes, and those aren't part of your Microsoft Entra ID user schema, then you may need to configure [synching extension attributes](../app-provisioning/user-provisioning-sync-attributes-for-mapping).

## Add SAP Cloud Identity Services from the gallery

Before configuring Microsoft Entra ID to have automatic user provisioning into SAP Cloud Identity Services, you need to add SAP Cloud Identity Services from the Microsoft Entra application gallery to your tenant's list of enterprise applications. You can do this step in the Microsoft Entra admin center, or via the Graph API.

If SAP Cloud Identity Services is already configured for single-sign on from Microsoft Entra using SAML, and an application is already present in your Microsoft Entra list of enterprise applications, then continue at Configure automatic user provisioning to SAP Cloud Identity Services.

Note

If you have previously configured an application registration for OpenID Connect integration, then you will not be able to configure provisioning for that application registration. Instead, create a separate enterprise application for provisioning.

### Adding SAP Cloud Identity Services using the Microsoft Entra admin center

**To add SAP Cloud Identity Services from the Microsoft Entra application gallery using the Microsoft Entra admin center, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. To add the app from the gallery, type **SAP Cloud Identity Services** in the search box.
4. Select **SAP Cloud Identity Services** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.
5. Continue to Configure automatic user provisioning to SAP Cloud Identity Services to configure provisioning.

### Adding SAP Cloud Identity Services using Microsoft Graph

You can create an application and service principal by following the steps in [Configure provisioning with the Microsoft Graph API](../app-provisioning/application-provisioning-configuration-api).

First, retrieve the gallery application template identifier for `SAP Cloud Identity Services`.

```msgraph
GET https://graph.microsoft.com/v1.0/applicationTemplates?$filter=displayName eq 'SAP Cloud Identity Services'
```

Extract the `id` of the application template from the response. Then, create the gallery application and service principal.

```msgraph
POST https://graph.microsoft.com/v1.0/applicationTemplates/{applicationTemplateId}/instantiate
Content-type: application/json

{
  "displayName": "SAP Cloud Identity Services"
}
```

The response will contain the new application and service principal objects.

Next, retrieve the template for provisioning configuration, using the `id` of the service principal just created.

```msgraph
GET https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/templates
```

To enable provisioning, you'll need to create a job. Use the following request to create a provisioning job. Use the `id` from the previous step as the `templateId` when specifying the template to be used for the job.

```msgraph
POST https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs
Content-type: application/json

{
    "templateId": "sapcloudidentityservices"
}
```

As described in Configure automatic user provisioning to SAP Cloud Identity Services, you can then further configure the [provisioning job and template schema](/en-us/graph/api/synchronization-synchronizationschema-update?view=graph-rest-1.0&amp;preserve-view=true) associated with the service principal. Then, [authorize access](../app-provisioning/application-provisioning-configuration-api#step-3-authorize-access) for Microsoft Entra to authenticate to SAP Cloud Identity Services, and then [start the provisioning job](../app-provisioning/application-provisioning-configuration-api#step-4-start-the-provisioning-job).

## Configure automatic user provisioning to SAP Cloud Identity Services

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and groups in SAP Cloud Identity Services based on user and group assignments to an application in Microsoft Entra ID.

### Configure automatic user provisioning in Microsoft Entra ID

To configure automatic user provisioning for SAP Cloud Identity Services in Microsoft Entra ID, perform the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select the application, **SAP Cloud Identity Services**.

    ![Screenshot of the SAP Cloud Identity Services link in the Applications list.](common/all-applications.png)
4. Select the **Properties** tab.
5. Verify that the **Assignment required?** option is set to **Yes**. If it's set to **No**, all users in your directory, including external identities, can access the application, and you can't review access to the application.
6. Select the **Provisioning** tab.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
7. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
8. In the **Tenant URL** field, input your SAP Cloud Identity Services Tenant URL and Secret Token. Select **Test Connection** to ensure Microsoft Entra ID can connect to SAP Cloud Identity Services. If the connection fails, ensure your SAP Cloud Identity Services account has the required admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-connection.png)
9. Select **Create** to create your configuration.
10. Select **Properties** in the **Overview** page.
11. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning properties page showing notification and deletion settings.](common/provisioning-properties.png)
12. Select **Attribute Mapping** in the left panel and select users.
13. Review the user and group attributes that are synchronized from Microsoft Entra ID to SAP Cloud Identity Services in the **Attribute Mapping** section. If you don't see the attributes in your SAP Cloud Identity Services available as a target for mapping, then select **Show advanced options** and select **Edit attribute list for SAP Cloud Platform Identity Authentication Service** to [edit the list of supported attributes](../app-provisioning/customize-application-attributes#editing-the-list-of-supported-attributes). Add the attributes of your SAP Cloud Identity Services tenant.
14. Review and record the source and target attributes selected as **Matching** properties, mappings that have a **Matching precedence**, as these attributes are used to match the users and groups in SAP Cloud Identity Services for the Microsoft Entra provisioning service to determine whether to create a new user/group or update an existing user/group. For more information on matching, see [matching users in the source and target systems](../app-provisioning/customize-application-attributes#matching-users-in-the-source-and-target--systems). In a subsequent step, you ensure that any users already in SAP Cloud Identity Services have the attributes selected as **Matching** properties populated, to prevent duplicate users from being created.
15. Confirm that there's an attribute mapping for `IsSoftDeleted`, or a function containing `IsSoftDeleted`, mapped to an attribute of the application. When a user is unassigned from the application, soft-deleted in Microsoft Entra ID, or blocked from sign-in, the Microsoft Entra provisioning service will update the attribute mapped to `isSoftDeleted`. If no attribute is mapped, users who later are unassigned from the application role will continue to exist in the application's data store.
16. Add any additional mappings that your SAP Cloud Identity Services, or downstream target SAP systems, require.
17. Select the **Save** button to commit any changes.

    | User Attribute | Type | Supported for filtering | Required by SAP Cloud Identity Services |
    | --- | --- | --- | --- |
    | `userName` | String | ✓ | ✓ |
    | `emails[type eq "work"].value` | String |  | ✓ |
    | `active` | Boolean |  |  |
    | `displayName` | String |  |  |
    | `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager` | Reference |  |  |
    | `addresses[type eq "work"].country` | String |  |  |
    | `addresses[type eq "work"].locality` | String |  |  |
    | `addresses[type eq "work"].postalCode` | String |  |  |
    | `addresses[type eq "work"].region` | String |  |  |
    | `addresses[type eq "work"].streetAddress` | String |  |  |
    | `name.givenName` | String |  |  |
    | `name.familyName` | String |  |  |
    | `name.honorificPrefix` | String |  |  |
    | `phoneNumbers[type eq "fax"].value` | String |  |  |
    | `phoneNumbers[type eq "mobile"].value` | String |  |  |
    | `phoneNumbers[type eq "work"].value` | String |  |  |
    | `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:costCenter` | String |  |  |
    | `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department` | String |  |  |
    | `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division` | String |  |  |
    | `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber` | String |  |  |
    | `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization` | String |  |  |
    | `locale` | String |  |  |
    | `timezone` | String |  |  |
    | `userType` | String |  |  |
    | `company` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute1` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute2` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute3` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute4` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute5` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute6` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute7` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute8` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute9` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:User:attributes:customAttribute10` | String |  |  |
    | `sendMail` | String |  |  |
    | `mailVerified` | String |  |  |

    | Group Attribute | Type | Supported for filtering | Required by SAP Cloud Identity Services |
    | --- | --- | --- | --- |
    | `id` | String | ✓ | ✓ |
    | `externalId` | String |  |  |
    | `displayName` | String |  | ✓ |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:Group:name` | String |  |  |
    | `urn:sap:cloud:scim:schemas:extension:custom:2.0:Group:description` | String |  |  |
    | `members` | Reference |  | ✓ |
18. To configure scoping filters, refer to the instructions in [Define conditional rules for provisioning user accounts](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

    ![Screenshot of Saving Provisioning Configuration.](common/provisioning-configuration-save.png)
19. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
20. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Provision a new test user from Microsoft Entra ID to SAP Cloud Identity Services

It's recommended that a single new Microsoft Entra test user is assigned to SAP Cloud Identity Services to test the automatic user provisioning configuration.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) and a User Administrator.
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**.
4. Type in the **User principal name** and **Display Name** of the new test user. The user principal name must be unique and not the same of any current or previous Microsoft Entra user or SAP Cloud Identity Services user. Select **Review + create** and **Create**.
5. Once the test user is created, browse to **Entra ID** &gt; **Enterprise apps**.
6. Select the SAP Cloud Identity Services application.
7. Select **Users and groups** and then select **Add user/group**.
8. In the **Users and groups** , select **None Selected**, and in text box, type the user principal name of the test user.
9. Select **Select**, and then **Assign**.
10. Select **Provisioning** and then select **Provision on demand**.
11. In the **Select a user or group** text box, type the user principal name of the test user.
12. Select **Provision**.
13. Wait for the provisioning to complete. If successful, you see the message `Modified attributes (successful)`.

You can also optionally verify what the Microsoft Entra provisioning service will provision when a user goes out of scope of the application.

1. Select **Users and groups**.
2. Select the test user, then select **Remove**.
3. After the test user is removed, select **Provisioning** and then select **Provision on demand**.
4. In the **Select a user or group** text box, type the user principal name of the test user just de-assigned.
5. Select **Provision**.
6. Wait for the provisioning to complete.

Finally, you can remove the test user from Microsoft Entra ID.

1. Browse to **Entra ID** &gt; **Users**.
2. Select the test user, select **Delete**, and select **OK**. This action soft-deletes the test user from Microsoft Entra ID.

You can also then remove the test user from SAP Cloud Identity Services.

## Identify existing users in your application and assign them to the enterprise application

Microsoft Entra can discover the existing users in your application and simplify getting them assigned to the enterprise application. Click on the [discover identities](../app-provisioning/how-to-account-discovery) button in the provisioning overview page. Once the report is generated, you will have a view of all the users in your application, which users in the application match with a Microsoft Entra ID user, which users are already assigned to the enterprise application in Microsoft Entra ID, and which users in the application are not matched with a Microsoft Entra ID user. You can then run a simple PowerShell script to assign the discovered users to the application:

1. [Download the Assign-CorrelatedUsers PowerShell script](https://aka.ms/AssignCorrelatedUsersPowerShell).
2. Preview which users would receive application role assignments without making changes by running the script in dry-run mode:

    ```powershell
    .\Assign-CorrelatedUsers.ps1 -ServicePrincipalId "7A22..." -DryRun
    ```
3. After reviewing the dry-run output, run the script without `-DryRun` to create the actual application role assignments for the matched users:

    ```powershell
    .\Assign-CorrelatedUsers.ps1 -ServicePrincipalId "7A22..."
    ```
4. Wait one minute for changes to propagate within Microsoft Entra ID.

The discovery functionality requires [Entra ID Governance](../../id-governance/licensing-fundamentals) licenses. Organizations without the necessary licenses can still follow the steps below to identify existing users in SAP CLout Identity Services and assign them to the enterprise application in Microsoft Entra.

## Ensure existing SAP Cloud Identity Services users have the necessary matching attributes

Before assigning non-test users to the SAP Cloud Identity Services application in Microsoft Entra ID, you should ensure that any users already in SAP Cloud Identity Services that represent the same people as the users in Microsoft Entra ID, have the mapping attributes populated in SAP Cloud Identity services.

In the provisioning mapping, the attributes selected as **Matching** properties are used to match the user accounts in Microsoft Entra ID with the user accounts in SAP Cloud Identity Services. If there is a user in Microsoft Entra ID with no match in SAP Cloud Identity Services, then the Microsoft Entra provisioning service will attempt to create a new user. If there is a user in Microsoft Entra ID and a match in SAP Cloud Identity Services, then the Microsoft Entra provisioning service will update that SAP Cloud Identity Services user. For this reason, you should ensure that any users already in SAP Cloud Identity Services have the attributes selected as **Matching** properties populated, otherwise duplicate users may be created. If you need to change the matching attribute in your Microsoft Entra application attribute mapping, see [matching users in the source and target systems](../app-provisioning/customize-application-attributes#matching-users-in-the-source-and-target--systems).

1. Sign in to your SAP Cloud Identity Services Admin Console, `https://<tenantID>.accounts.ondemand.com/admin` or `https://<tenantID>.trial-accounts.ondemand.com/admin` if a trial.
2. Navigate to **Users & Authorizations &gt; Export Users**.
3. Select all attributes required for matching Microsoft Entra users with those in SAP. These attributes include the `SCIM ID`, `userName`, `emails`, and other attributes you may be using in your SAP systems as identifiers.
4. Select **Export** and wait for the browser to download the CSV file.
5. Open a PowerShell window.
6. Type the following script into an editor. In line one, if you selected a different matching attribute other than `userName`, change the value of the `sapScimUserNameField` variable to the name of the SAP Cloud Identity Services attribute. In line two, change the argument to the filename of the exported CSV file from `Users-exported-from-sap.csv` to the name of your downloaded file.

    ```powershell
    $sapScimUserNameField = "userName"
    $existingSapUsers = import-csv -Path ".\Users-exported-from-sap.csv" -Encoding UTF8
    $count = 0
    $warn = 0
    foreach ($u in $existingSapUsers) {
     $id = $u.id
     if (($null -eq $id) -or ($id.length -eq 0)) {
         write-error "Exported CSV file doesn't contain the ID attribute of SAP Cloud Identity Services users."
         throw "ID attribute not available, re-export"
         return
     }
     $count++
     $userName = $u.$sapScimUserNameField
     if (($null -eq $userName) -or ($userName.length -eq 0)) {
         write-warning "SAP Cloud Identity Services user $id doesn't have a $sapScimUserNameField attribute populated"
         $warn++
     }
    }
    write-output "$warn of $count users in SAP Cloud Identity Services did not have the $sapScimUserNameFIeld attribute populated."
    ```
7. Run the script. When the script completes, if there were one or more users that were lacking the required matching attribute, then look up those users in the exported CSV file or in the SAP Cloud Identity Services Admin Console. If those users are also present in Microsoft Entra, then you need to first update the SAP Cloud Identity Services representation of those users so that they have the matching attribute populated.
8. Once you have updated the attributes of those users in SAP Cloud Identity Services, then re-export the users from SAP Cloud Identity Services, as described in steps 2-5, and PowerShell steps in this section, to confirm no users in SAP Cloud Identity Services are lacking the matching attributes that would prevent provisioning to those users.

Now that you have a list of all the users obtained from SAP Cloud Identity Services, you match those users from the application's data store, with users already in Microsoft Entra ID, to determine which users should be in scope for provisioning.

### Retrieve the IDs of the users in Microsoft Entra ID

This section shows how to interact with Microsoft Entra ID by using [Microsoft Graph PowerShell](https://www.powershellgallery.com/packages/Microsoft.Graph) cmdlets.

The first time your organization uses these cmdlets for this scenario, you need to be in a Global Administrator role to allow Microsoft Graph PowerShell to be used in your tenant. Subsequent interactions can use a lower-privileged role, such as:

- User Administrator, if you anticipate creating new users.
- Application Administrator or [Identity Governance Administrator](../role-based-access-control/permissions-reference#identity-governance-administrator), if you're just managing application role assignments.

1. Open PowerShell.
2. If you don't have the [Microsoft Graph PowerShell modules](https://www.powershellgallery.com/packages/Microsoft.Graph) already installed, install the `Microsoft.Graph.Users` module and others by using this command:

    ```powershell
    Install-Module Microsoft.Graph
    ```

    If you already have the modules installed, ensure that you're using a recent version:

    ```powershell
    Update-Module microsoft.graph.users,microsoft.graph.identity.governance,microsoft.graph.applications
    ```
3. Connect to Microsoft Entra ID:

    ```powershell
    $msg = Connect-MgGraph -ContextScope Process -Scopes "User.ReadWrite.All,Application.ReadWrite.All,AppRoleAssignment.ReadWrite.All,EntitlementManagement.ReadWrite.All"
    ```
4. If this is the first time you have used this command, you may need to consent to allow the Microsoft Graph Command Line tools to have these permissions.
5. Read the list of users obtained from the application's data store into the PowerShell session. If the list of users was in a CSV file, you can use the PowerShell cmdlet `Import-Csv` and provide the name of the file from the previous section as an argument.

    For example, if the file obtained from SAP Cloud Identity Services is named *Users-exported-from-sap.csv* and is located in the current directory, enter this command.

    ```powershell
    $filename = ".\Users-exported-from-sap.csv"
    $dbusers = Import-Csv -Path $filename -Encoding UTF8
    ```

    For another example if you are using a database or directory, if the file is named *users.csv* and located in the current directory, enter this command:

    ```powershell
    $filename = ".\users.csv"
    $dbusers = Import-Csv -Path $filename -Encoding UTF8
    ```
6. Choose the column of the *users.csv* file that will match with an attribute of a user in Microsoft Entra ID.

    If you are using SAP Cloud Identity Services, then the default mapping is the SAP SCIM attribute `userName` with the Microsoft Entra ID attribute `userPrincipalName`:

    ```powershell
    $db_match_column_name = "userName"
    $azuread_match_attr_name = "userPrincipalName"
    ```

    For another example if you are using a database or directory, you might have users in a database where the value in the column named `EMail` is the same value as in the Microsoft Entra attribute `userPrincipalName`:

    ```powershell
    $db_match_column_name = "EMail"
    $azuread_match_attr_name = "userPrincipalName"
    ```
7. Retrieve the IDs of those users in Microsoft Entra ID.

    The following PowerShell script uses the `$dbusers`, `$db_match_column_name`, and `$azuread_match_attr_name` values specified earlier. It will query Microsoft Entra ID to locate a user that has an attribute with a matching value for each record in the source file. If there are many users in the file obtained from the source SAP Cloud Identity Services, database, or directory, this script might take several minutes to finish. If you don't have an attribute in Microsoft Entra ID that has the value, and need to use a `contains` or other filter expression, then you will need to customize this script and that in step 11 below to use a different filter expression.

    ```powershell
    $dbu_not_queried_list = @()
    $dbu_not_matched_list = @()
    $dbu_match_ambiguous_list = @()
    $dbu_query_failed_list = @()
    $azuread_match_id_list = @()
    $azuread_not_enabled_list = @()
    $dbu_values = @()
    $dbu_duplicate_list = @()
    
    foreach ($dbu in $dbusers) { 
       if ($null -ne $dbu.$db_match_column_name -and $dbu.$db_match_column_name.Length -gt 0) { 
          $val = $dbu.$db_match_column_name
          $escval = $val -replace "'","''"
          if ($dbu_values -contains $escval) { $dbu_duplicate_list += $dbu; continue } else { $dbu_values += $escval }
          $filter = $azuread_match_attr_name + " eq '" + $escval + "'"
          try {
             $ul = @(Get-MgUser -Filter $filter -All -Property Id,accountEnabled -ErrorAction Stop)
             if ($ul.length -eq 0) { $dbu_not_matched_list += $dbu; } elseif ($ul.length -gt 1) {$dbu_match_ambiguous_list += $dbu } else {
                $id = $ul[0].id; 
                $azuread_match_id_list += $id;
                if ($ul[0].accountEnabled -eq $false) {$azuread_not_enabled_list += $id }
             } 
          } catch { $dbu_query_failed_list += $dbu } 
        } else { $dbu_not_queried_list += $dbu }
    }
    
    ```
8. View the results of the previous queries. See if any of the users in SAP Cloud Identity Services, the database, or directory couldn't be located in Microsoft Entra ID, because of errors or missing matches.

    The following PowerShell script will display the counts of records that weren't located:

    ```powershell
    $dbu_not_queried_count = $dbu_not_queried_list.Count
    if ($dbu_not_queried_count -ne 0) {
      Write-Error "Unable to query for $dbu_not_queried_count records as rows lacked values for $db_match_column_name."
    }
    $dbu_duplicate_count = $dbu_duplicate_list.Count
    if ($dbu_duplicate_count -ne 0) {
      Write-Error "Unable to locate Microsoft Entra ID users for $dbu_duplicate_count rows as multiple rows have the same value"
    }
    $dbu_not_matched_count = $dbu_not_matched_list.Count
    if ($dbu_not_matched_count -ne 0) {
      Write-Error "Unable to locate $dbu_not_matched_count records in Microsoft Entra ID by querying for $db_match_column_name values in $azuread_match_attr_name."
    }
    $dbu_match_ambiguous_count = $dbu_match_ambiguous_list.Count
    if ($dbu_match_ambiguous_count -ne 0) {
      Write-Error "Unable to locate $dbu_match_ambiguous_count records in Microsoft Entra ID as attribute match ambiguous."
    }
    $dbu_query_failed_count = $dbu_query_failed_list.Count
    if ($dbu_query_failed_count -ne 0) {
      Write-Error "Unable to locate $dbu_query_failed_count records in Microsoft Entra ID as queries returned errors."
    }
    $azuread_not_enabled_count = $azuread_not_enabled_list.Count
    if ($azuread_not_enabled_count -ne 0) {
     Write-Error "$azuread_not_enabled_count users in Microsoft Entra ID are blocked from sign-in."
    }
    if ($dbu_not_queried_count -ne 0 -or $dbu_duplicate_count -ne 0 -or $dbu_not_matched_count -ne 0 -or $dbu_match_ambiguous_count -ne 0 -or $dbu_query_failed_count -ne 0 -or $azuread_not_enabled_count) {
     Write-Output "You will need to resolve those issues before access of all existing users can be reviewed."
    }
    $azuread_match_count = $azuread_match_id_list.Count
    Write-Output "Users corresponding to $azuread_match_count records were located in Microsoft Entra ID." 
    ```
9. When the script finishes, it will indicate an error if any records from the data source weren't located in Microsoft Entra ID. If not all the records for users from the application's data store could be located as users in Microsoft Entra ID, you'll need to investigate which records didn't match and why.

    For example, someone's email address and userPrincipalName might have been changed in Microsoft Entra ID without their corresponding `mail` property being updated in the application's data source. Or, the user might have already left the organization but is still in the application's data source. Or there might be a vendor or super-admin account in the application's data source that does not correspond to any specific person in Microsoft Entra ID.
10. If there were users who couldn't be located in Microsoft Entra ID, or weren't active and able to sign in, but you want to have their access reviewed or their attributes updated in SAP Cloud Identity Services, the database, or directory, you'll need to update the application, the matching rule, or update or create Microsoft Entra users for them. For more information on which change to make, see [manage mappings and user accounts in applications that did not match to users in Microsoft Entra ID](../app-provisioning/application-provisioning-application-unmatched-users).

    If you choose the option of creating users in Microsoft Entra ID, you can create users in bulk by using either:

    - A CSV file, as described in [Bulk create users in the Microsoft Entra admin center](../users/users-bulk-add)
    - The [New-MgUser](/en-us/powershell/module/microsoft.graph.users/new-mguser?view=graph-powershell-1.0#examples&amp;preserve-view=true) cmdlet

    Ensure that these new users are populated with the attributes required for Microsoft Entra ID to later match them to the existing users in the application, and the attributes required by Microsoft Entra ID, including `userPrincipalName`, `mailNickname` and `displayName`. The `userPrincipalName` must be unique among all the users in the directory.

    For example, you might have users in a database where the value in the column named `EMail` is the value you want to use as the Microsoft Entra user principal Name, the value in the column `Alias` contains the Microsoft Entra ID mail nickname, and the value in the column `Full name` contains the user's display name:

    ```powershell
    $db_display_name_column_name = "Full name"
    $db_user_principal_name_column_name = "Email"
    $db_mail_nickname_column_name = "Alias"
    ```

    Then you can use this script to create Microsoft Entra users for those in SAP Cloud Identity Services, the database, or directory that didn't match with users in Microsoft Entra ID. Note that you may need to modify this script to add additional Microsoft Entra attributes needed in your organization, or if the `$azuread_match_attr_name` is neither `mailNickname` nor `userPrincipalName`, in order to supply that Microsoft Entra attribute.

    ```powershell
    $dbu_missing_columns_list = @()
    $dbu_creation_failed_list = @()
    foreach ($dbu in $dbu_not_matched_list) {
       if (($null -ne $dbu.$db_display_name_column_name -and $dbu.$db_display_name_column_name.Length -gt 0) -and
           ($null -ne $dbu.$db_user_principal_name_column_name -and $dbu.$db_user_principal_name_column_name.Length -gt 0) -and
           ($null -ne $dbu.$db_mail_nickname_column_name -and $dbu.$db_mail_nickname_column_name.Length -gt 0)) {
          $params = @{
             accountEnabled = $false
             displayName = $dbu.$db_display_name_column_name
             mailNickname = $dbu.$db_mail_nickname_column_name
             userPrincipalName = $dbu.$db_user_principal_name_column_name
             passwordProfile = @{
               Password = -join (((48..90) + (96..122)) * 16 | Get-Random -Count 16 | % {[char]$_})
             }
          }
          try {
            New-MgUser -BodyParameter $params
          } catch { $dbu_creation_failed_list += $dbu; throw }
       } else {
          $dbu_missing_columns_list += $dbu
       }
    }
    ```
11. After you add any missing users to Microsoft Entra ID, run the script from step 7 again. Then run the script from step 8. Check that no errors are reported.

    ```powershell
    $dbu_not_queried_list = @()
    $dbu_not_matched_list = @()
    $dbu_match_ambiguous_list = @()
    $dbu_query_failed_list = @()
    $azuread_match_id_list = @()
    $azuread_not_enabled_list = @()
    $dbu_values = @()
    $dbu_duplicate_list = @()
    
    foreach ($dbu in $dbusers) { 
       if ($null -ne $dbu.$db_match_column_name -and $dbu.$db_match_column_name.Length -gt 0) { 
          $val = $dbu.$db_match_column_name
          $escval = $val -replace "'","''"
          if ($dbu_values -contains $escval) { $dbu_duplicate_list += $dbu; continue } else { $dbu_values += $escval }
          $filter = $azuread_match_attr_name + " eq '" + $escval + "'"
          try {
             $ul = @(Get-MgUser -Filter $filter -All -Property Id,accountEnabled -ErrorAction Stop)
             if ($ul.length -eq 0) { $dbu_not_matched_list += $dbu; } elseif ($ul.length -gt 1) {$dbu_match_ambiguous_list += $dbu } else {
                $id = $ul[0].id; 
                $azuread_match_id_list += $id;
                if ($ul[0].accountEnabled -eq $false) {$azuread_not_enabled_list += $id }
             } 
          } catch { $dbu_query_failed_list += $dbu } 
        } else { $dbu_not_queried_list += $dbu }
    }
    
    $dbu_not_queried_count = $dbu_not_queried_list.Count
    if ($dbu_not_queried_count -ne 0) {
      Write-Error "Unable to query for $dbu_not_queried_count records as rows lacked values for $db_match_column_name."
    }
    $dbu_duplicate_count = $dbu_duplicate_list.Count
    if ($dbu_duplicate_count -ne 0) {
      Write-Error "Unable to locate Microsoft Entra ID users for $dbu_duplicate_count rows as multiple rows have the same value"
    }
    $dbu_not_matched_count = $dbu_not_matched_list.Count
    if ($dbu_not_matched_count -ne 0) {
      Write-Error "Unable to locate $dbu_not_matched_count records in Microsoft Entra ID by querying for $db_match_column_name values in $azuread_match_attr_name."
    }
    $dbu_match_ambiguous_count = $dbu_match_ambiguous_list.Count
    if ($dbu_match_ambiguous_count -ne 0) {
      Write-Error "Unable to locate $dbu_match_ambiguous_count records in Microsoft Entra ID as attribute match ambiguous."
    }
    $dbu_query_failed_count = $dbu_query_failed_list.Count
    if ($dbu_query_failed_count -ne 0) {
      Write-Error "Unable to locate $dbu_query_failed_count records in Microsoft Entra ID as queries returned errors."
    }
    $azuread_not_enabled_count = $azuread_not_enabled_list.Count
    if ($azuread_not_enabled_count -ne 0) {
     Write-Warning "$azuread_not_enabled_count users in Microsoft Entra ID are blocked from sign-in."
    }
    if ($dbu_not_queried_count -ne 0 -or $dbu_duplicate_count -ne 0 -or $dbu_not_matched_count -ne 0 -or $dbu_match_ambiguous_count -ne 0 -or $dbu_query_failed_count -ne 0 -or $azuread_not_enabled_count -ne 0) {
     Write-Output "You will need to resolve those issues before access of all existing users can be reviewed."
    }
    $azuread_match_count = $azuread_match_id_list.Count
    Write-Output "Users corresponding to $azuread_match_count records were located in Microsoft Entra ID." 
    ```

## Ensure existing Microsoft Entra users have the necessary attributes

Before enabling automatic user provisioning, you must decide which users in Microsoft Entra ID need access to SAP Cloud Identity Services, and then you need to check to make sure that those users have the necessary attributes in Microsoft Entra ID, and those attributes are mapped to the expected schema of SAP Cloud Identity Services.

- By default, the value of the Microsoft Entra user `userPrincipalName` attribute is mapped to both the `userName` and `emails[type eq "work"].value` attributes of SAP Cloud Identity Services. If user's email addresses are different from their user principal names, then you may need to change this mapping.
- SAP Cloud Identity Services may ignore values of the `postalCode` attribute if the format of Company ZIP/postal code doesn't match the company country or region.
- By default, the Microsoft Entra attribute `country` is mapped to the SAP Cloud Identity Services `addresses[type eq "work"].country` field. If the values of the `country` attribute are not two character ISO 3166 country codes, then creation of those users in SAP Cloud Identity Services may fail. For more information, see [countries.properties](https://help.sap.com/docs/cloud-identity-services/cloud-identity-services/change-master-data-texts-rest-api#countries-properties).
- By default, the Microsoft Entra attribute `department` is mapped to the SAP Cloud Identity Services `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department` attribute. If Microsoft Entra users have values of the `department` attribute, those values must match those departments already configured in SAP Cloud Identity Services, otherwise creation, or update, of the user will fail. For more information, see [departments.properties](https://help.sap.com/docs/cloud-identity-services/cloud-identity-services/change-master-data-texts-rest-api#departments-properties). If the `department` values in your Microsoft Entra users aren't consistent with those in your SAP environment, then either update the department values in Microsoft Entra, update the allowed department values in SAP Cloud Identity Services, or remove the mapping, prior to assigning users.
- SAP Cloud Identity Services's SCIM endpoint requires certain attributes to be of specific format. For more information about these attributes and their specific format, see [SAP Cloud Identity Services SCIM API attribute details](https://help.sap.com/viewer/6d6d63354d1242d185ab4830fc04feb1/Cloud/en-US/b10fc6a9a37c488a82ce7489b1fab64c.html#).

## Assign users to the SAP Cloud Identity Services application in Microsoft Entra ID

Microsoft Entra ID uses a concept called *assignments* to determine which users should receive access to selected apps. In the context of automatic user provisioning, if the Settings value of **Scope** is **Sync only assigned users and groups**, then only the users and groups that have been assigned to an application role of that application in Microsoft Entra ID are synchronized with SAP Cloud Identity Services. When assigning a user to SAP Cloud Identity Services, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning. Currently the only available role for SAP Cloud Identity Services is **User**.

If provisioning has already been enabled for the application, check that the application provisioning isn't in [quarantine](../app-provisioning/application-provisioning-quarantine-status) before assigning more users to the application. Resolve any issues that are causing the quarantine, before you proceed.

### Check for users who are present in SAP Cloud Identity Services and aren't already assigned to the application in Microsoft Entra ID

The previous steps have evaluated whether the users in SAP Cloud Identity Services also exist as users in Microsoft Entra ID. However, they might not all currently be assigned to the application's roles in Microsoft Entra ID. So the next steps are to see which users don't have assignments to application roles.

1. Using PowerShell, look up the service principal ID for the application's service principal.

    For example, if the enterprise application is named `SAP Cloud Identity Services`, enter the following commands:

    ```powershell
    $azuread_app_name = "SAP Cloud Identity Services"
    $azuread_sp_filter = "displayName eq '" + ($azuread_app_name -replace "'","''") + "'"
    $azuread_sp = Get-MgServicePrincipal -Filter $azuread_sp_filter -All
    ```
2. Retrieve the users who currently have assignments to the application in Microsoft Entra ID.

    This builds upon the `$azuread_sp` variable set in the previous command.

    ```powershell
    $azuread_existing_assignments = @(Get-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $azuread_sp.Id -All)
    ```
3. Compare the list of user IDs of the users already in both SAP Cloud Identity Services and Microsoft Entra ID to those users currently assigned to the application in Microsoft Entra ID. This script builds upon the `$azuread_match_id_list` variable set in the previous sections:

    ```powershell
    $azuread_not_in_role_list = @()
    foreach ($id in $azuread_match_id_list) {
       $found = $false
       foreach ($existing in $azuread_existing_assignments) {
          if ($existing.principalId -eq $id) {
             $found = $true; break;
          }
       }
       if ($found -eq $false) { $azuread_not_in_role_list += $id }
    }
    $azuread_not_in_role_count = $azuread_not_in_role_list.Count
    Write-Output "$azuread_not_in_role_count users in the application's data store aren't assigned to the application roles."
    ```

    If zero users are *not* assigned to application roles, indicating that all users *are* assigned to application roles, that result indicates that there were no users in common across Microsoft Entra ID and SAP Cloud Identity Services, so no changes are needed. However, if one or more users already in SAP Cloud Identity Services aren't currently assigned to the application roles, you need to continue the procedure and add them to one of the application's roles.
4. Retrieve the `User` app role ID from the service principal so you can assign the matched users to the correct role:

    ```powershell
    $azuread_app_role_name = "User"
    $azuread_app_role_id = ($azuread_sp.AppRoles | where-object {$_.AllowedMemberTypes -contains "User" -and $_.DisplayName -eq "User"}).Id
    if ($null -eq $azuread_app_role_id) { write-error "role $azuread_app_role_name not located in application manifest"}
    ```
5. Create application role assignments for users who are already present in SAP Cloud Identity Services and Microsoft Entra, and don't currently have role assignments to the application:

    ```powershell
    foreach ($u in $azuread_not_in_role_list) {
       $res = New-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $azuread_sp.Id -AppRoleId $azuread_app_role_id -PrincipalId $u -ResourceId $azuread_sp.Id
    }
    ```
6. Wait one minute for changes to propagate within Microsoft Entra ID.
7. On the next Microsoft Entra provisioning cycle, the Microsoft Entra provisioning service will compare the representation of those users assigned to the application, with the representation in SAP Cloud Identity Services, and update SAP Cloud Identity Services users to have the attributes from Microsoft Entra ID.

### Assign remaining users and monitor initial sync

Once the testing is complete, a user is successfully provisioned to SAP Cloud Identity Services, and any existing SAP Cloud Identity Services users are assigned to the application role, you can assign any additional authorized users to the SAP Cloud Identity Services application by following one of the instructions here:

- You can [assign each individual user to the application](../enterprise-apps/assign-user-or-group-access-portal) in the Microsoft Entra admin center,
- You can assign individual users to the application via PowerShell cmdlet `New-MgServicePrincipalAppRoleAssignedTo` as shown in the previous section, or
- if your organization has a license for Microsoft Entra ID Governance, you can also [deploy entitlement management policies for automating access assignment](../../id-governance/identity-governance-applications-deploy#deploy-entitlement-management-policies-for-automating-access-assignment).

Once users are assigned to the application role and are in scope for provisioning, then the Microsoft Entra provisioning service will provision them to SAP Cloud Identity Services. Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 40 minutes as long as the Microsoft Entra provisioning service is running.

If you don't see users being provisioned, review the steps in the [troubleshooting guide for no users being provisioned](../app-provisioning/application-provisioning-config-problem-no-users-provisioned). Then, check the provisioning log through the [provisioning logs in Microsoft Entra](../monitoring-health/concept-provisioning-logs) or [Graph APIs](../app-provisioning/application-provisioning-configuration-api#monitor-provisioning-events-using-the-provisioning-logs). Filter the log to the status **Failure**. If there are failures with an ErrorCode of **DuplicateTargetEntries**, this indicates an ambiguity in your provisioning matching rules, and you need to update the Microsoft Entra users or the mappings that are used for matching to ensure each Microsoft Entra user matches one application user. Then filter the log to the action **Create** and status **Skipped**. If users were skipped with the SkipReason code of **NotEffectivelyEntitled**, this may indicate that the user accounts in Microsoft Entra ID weren't matched because the user account status was **Disabled**.

## Configure single-sign on

You may also choose to enable SAML-based single sign-on for SAP Cloud Identity Services, following the instructions provided in [SAP Cloud Identity Services single sign-on tutorial](sap-hana-cloud-platform-identity-authentication-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

## Monitor provisioning

You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity report, which describes all actions performed by the Microsoft Entra provisioning service on SAP Cloud Identity Services. You can also monitor the provisioning project via the Microsoft [Graph APIs](../app-provisioning/application-provisioning-configuration-api#monitor-the-provisioning-job-status).

For more information on how to read the Microsoft Entra provisioning logs, see [Reporting on automatic user account provisioning](../app-provisioning/check-status-user-account-provisioning).

## Maintain application role assignments

As users that are in assigned to the application are updated in Microsoft Entra ID, those changes are automatically provisioned to SAP Cloud Identity Services.

If you have Microsoft Entra ID Governance, you can automate changes to the application role assignments for SAP Cloud Identity Services in Microsoft Entra ID, to add or remove assignments as people join the organization, or leave or change roles.

- You can [perform a one-time or recurring access review of the application role assignments](../../id-governance/access-reviews-application-preparation).
- You can [create an entitlement management access package for this application](../../id-governance/entitlement-management-access-package-create-app). You can have policies for users to be assigned access, either when they request, [directly assigned by an administrator](../../id-governance/entitlement-management-access-package-assignments#directly-assign-an-identity), [using an automatic assignment policy](../../id-governance/entitlement-management-access-package-auto-assignment-policy), or through [lifecycle workflows](../../id-governance/entitlement-management-scenarios#administrator-assign-employees-access-from-lifecycle-workflows).

## Update an SAP Cloud Identity Services application to use the SAP Cloud Identity Services SCIM 2.0 endpoint

In September 2025, Microsoft released a SCIM 2.0 connector for SAP Cloud Identity Services that added support for group provisioning and deprovisioning to SAP Cloud Identity Services, custom extension attributes, and the OAuth 2.0 Client Credentials grant.

Completing the below steps will allow customers that were already previously using the SAP Cloud Identity Services connector to switch from the SCIM 1.0 endpoint to the SCIM 2.0 endpoint.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID &gt; Enterprise Apps &gt; SAP Cloud Identity Services**.
3. In the **Properties** section, copy the Object ID.

    ![Screenshot of where to copy Object ID in the Properties blade of the SAP Cloud Identity Services connector.](media/sap-cloud-platform-identity-authentication-provisioning-tutorial/object-id.png)
4. In a new web browser window, go to [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and sign in as the administrator for the Microsoft Entra tenant where your app is added.
5. Check to make sure the account being used has the correct permissions. The permission "Directory.ReadWrite.All" is required to make this change.

    ![Screenshot of the Permissions screen in Graph Explorer, where the admin is selecting the option to provide consent for the Directory.ReadWrite.All permission.](media/sap-cloud-platform-identity-authentication-provisioning-tutorial/graph-permissions.png)
6. Using the Object ID selected from the app previously, list the existing synchronization jobs for the service principal:

```http
GET https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/
```

1. Taking the "ID" value from the response body of the `GET` request from previous example, delete the existing synchronization job so you can recreate it with the SCIM 2.0 template. Replace "[job-id]" with the ID value from the `GET` request. The value should have the format of "sapcloudidentityservices.xxxxxxxxxxxxxxx.xxxxxxxxxxxxxxx":

```http
DELETE https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/[job-id]
```

1. In the Microsoft Graph Explorer, create a new provisioning job using the SAP Cloud Identity Services SCIM 2.0 template. Replace "[object-id]" with the service principal ID (object ID) copied from the third step.

```http
POST https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs { "templateId": "sapcloudidentityservices" }
```

1. Return to the first web browser window and select the **Provisioning** tab for your application. Your configuration is reset. You can confirm the upgrade is successful by confirming the Job ID starts with "sapcloudidentityservices".
2. Update the tenant URL in the **Admin credentials** section to the following: `https://<tenantID>.accounts.ondemand.com/scim`, or `https://<tenantid>.trial-accounts.ondemand.com/service/scim` if a trial.
3. Restore any previous changes you made to the application (Authentication details, Scoping filters, Custom attribute mappings) and re-enable provisioning.

Note

Failure to restore the previous settings might result in attributes (name.formatted for example) updating in SAP Cloud Identity Services unexpectedly. Be sure to check the configuration before enabling provisioning.

## Changelog

The following changes have been made to this connector:

- 9/30/2025 – Released to General Availability a new version of the SAP Cloud Identity Services connector that uses a SCIM 2.0 endpoint. The new version supports group provisioning and deprovisioning to SAP Cloud Identity Services, custom extension attributes, and the OAuth 2.0 Client Credentials grant.