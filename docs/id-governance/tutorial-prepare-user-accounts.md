---
layout: Conceptual
title: 'Tutorial: Preparing user accounts for Lifecycle workflows - Microsoft Entra ID Governance | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/tutorial-prepare-user-accounts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Tutorial for preparing user accounts for Lifecycle workflows.
ms.subservice: lifecycle-workflows
ms.topic: tutorial
ms.date: 2025-08-27T00:00:00.0000000Z
ms.reviewer: krbain
ms.custom: template-tutorial, no-azure-ad-ps-ref, sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: b7146d9e-ec99-3e82-1c60-07fb9d68219c
document_version_independent_id: 5ceb000f-6f3b-6672-3117-24f397262d79
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/tutorial-prepare-user-accounts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/tutorial-prepare-user-accounts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/tutorial-prepare-user-accounts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: e503d4bb-a4e0-b041-d70d-d00f1c7956b3
---

# Tutorial: Preparing user accounts for Lifecycle workflows - Microsoft Entra ID Governance | Microsoft Learn

For the on-boarding, and off-boarding, tutorials you need accounts for which the workflows are executed. This section helps you prepare these accounts, if you already have test accounts that meet the following requirements, you can proceed directly to the on-boarding and off-boarding tutorials. Two accounts are required for the on-boarding tutorials, one account for the new hire and another account that acts as the manager of the new hire. The new hire account must have the following attributes set:

- employeeHireDate must be set to today
- department must be set to sales
- manager attribute must be set, and the manager account should have a mailbox to receive an email

The off-boarding tutorials only require one account that has group and Teams memberships, but the account is deleted during the tutorial.

## Prerequisites

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

- A Microsoft Entra tenant
- An administrator account with appropriate permissions for the Microsoft Entra tenant. This account is used to create our users and workflows.

## Before you begin

In most cases, users are going to be provisioned to Microsoft Entra ID either from an on-premises solution (such as Microsoft Entra Connect or Cloud sync) or with an HR solution. These users have the attributes and values populated at the time of creation. Setting up the infrastructure to provision users is outside the scope of this tutorial. For information, see [Tutorial: Basic Active Directory environment](../identity/hybrid/cloud-sync/tutorial-basic-ad-azure) and [Tutorial: Integrate a single forest with a single Microsoft Entra tenant](../identity/hybrid/cloud-sync/tutorial-single-forest).

## Create users in Microsoft Entra ID

We use Graph Explorer to quickly create two users needed to execute the Lifecycle Workflows in the tutorials. One user represents our new employee and the second represents the new employee's manager.

You need to edit the POST and replace the &lt;your tenant name here&gt; portion with the name of your tenant. For example: $UPN\_manager = "bsimon@&lt;your tenant name here&gt;" to $UPN\_manager = "bsimon@contoso.onmicrosoft.com".

Note

Be aware that a workflow won't trigger when the employee hire date (Days from event) is prior to the workflow creation date. You must set an employeeHiredate in the future by design. The dates used in this tutorial are a snapshot in time. Therefore, you should change the dates accordingly to accommodate for this situation.

First we create our employee, Melva Prince.

1. Now navigate to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Sign-in to Graph Explorer with the User Administrator account for your tenant.
3. At the top, change **GET** to **POST** and add `https://graph.microsoft.com/v1.0/users/` to the box.
4. Copy the following code in to the **Request body**
5. Replace `<your tenant here>` in the following code with the value of your Microsoft Entra tenant.
6. Select **Run query**
7. Copy the ID that is returned in the results. This is used later to assign a manager.

```json
{
  "accountEnabled": true,
  "displayName": "Melva Prince",
  "mailNickname": "mprince",
  "department": "sales",
  "mail": "mprince@<your tenant name here>",
  "employeeHireDate": "2022-04-15T22:10:00Z",
  "userPrincipalName": "mprince@<your tenant name here>",
  "passwordProfile" : {
    "forceChangePasswordNextSignIn": true,
    "password": "<Generated Password>"
  }
}
```

[![Screenshot of POST create Melva in graph explorer.](media/tutorial-lifecycle-workflows/graph-post-user.png)](media/tutorial-lifecycle-workflows/graph-post-user.png#lightbox)

Next, we create Britta Simon. This account is used as our manager.

1. Still in [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Make sure the top is still set to **POST** and `https://graph.microsoft.com/v1.0/users/` is in the box.
3. Copy the following code in to the **Request body**
4. Replace `<your tenant here>` in the following code with the value of your Microsoft Entra tenant.
5. Select **Run query**
6. Copy the ID that is returned in the results. This ID is used later to assign a manager. 

    ```json
    {
      "accountEnabled": true,
      "displayName": "Britta Simon",
      "mailNickname": "bsimon",
      "department": "sales",
      "mail": "bsimon@<your tenant name here>",
      "employeeHireDate": "2021-01-15T22:10:00Z",
      "userPrincipalName": "bsimon@<your tenant name here>",
      "passwordProfile" : {
        "forceChangePasswordNextSignIn": true,
        "password": "<Generated Password>"
      }
    }
    ```

Note

You need to change the &lt;your tenant name here&gt; section of the code to match your Microsoft Entra tenant.

As an alternative, the following PowerShell script can also be used to quickly create two users needed to execute a lifecycle workflow. One user represents our new employee and the second represents the new employee's manager.

Important

The following PowerShell script is provided to quickly create the two users required for this tutorial. These users can also be created in the Microsoft Entra admin center.

In order to create this step, save the following PowerShell script to a location on a machine that has access to Azure.

Next, you need to edit the script and replace the &lt;your tenant name here&gt; portion with the name of your tenant. For example: $UPN\_manager = "bsimon@&lt;your tenant name here&gt;" to $UPN\_manager = "bsimon@contoso.onmicrosoft.com".

You need to do perform this action for both $UPN\_employee and $UPN\_manager

After editing the script, save it and follow these steps:

1. Open a Windows PowerShell command prompt, with Administrative privileges, from a machine that has access to the Microsoft Entra admin center.
2. Navigate to the saved PowerShell script location and run it.
3. If prompted select **Yes to all** when installing the PowerShell module.
4. When prompted, sign in to the Microsoft Entra admin center with a Global Administrator for your tenant.

```powershell
#
# DISCLAIMER:
# Copyright (c) Microsoft Corporation. All rights reserved. This 
# script is made available to you without any express, implied or 
# statutory warranty, not even the implied warranty of 
# merchantability or fitness for a particular purpose, or the 
# warranty of title or non-infringement. The entire risk of the 
# use or the results from the use of this script remains with you.
#
#
#
#
#Declare variables

$Displayname_employee = "Melva Prince"
$UPN_employee = "mprince<your tenant name here>"
$Name_employee = "mprince"
$Password_employee = "Pass1w0rd"
$EmployeeHireDate_employee = "04/10/2022"
$Department_employee = "Sales"
$Displayname_manager = "Britta Simon"
$Name_manager = "bsimon"
$Password_manager = "Pass1w0rd"
$Department = "Sales"
$UPN_manager = "bsimon@<your tenant name here>"

Install-Module -Name Microsoft.Graph
Connect-MgGraph -Confirm

$PasswordProfile = @{
  Password = "$Password_manager"
  }

New-MgUser -DisplayName $Displayname_manager -PasswordProfile $PasswordProfile -UserPrincipalName $UPN_manager -AccountEnabled $true -MailNickName $Name_manager -Department $Department

$PasswordProfile = @{
  Password = "$Password_employee"
  }

New-MgUser -DisplayName $Displayname_employee -PasswordProfile $PasswordProfile -UserPrincipalName $UPN_employee -AccountEnabled $true -MailNickName $Name_employee -Department $Department
```

Once your user or users are successfully created in Microsoft Entra ID, you can proceed to follow the Lifecycle workflow tutorials for your workflow creation.

## Other steps for prehire scenario

There are some other steps that you should be aware of when testing either the [On-boarding users to your organization using Lifecycle workflows with the Microsoft Entra admin center](tutorial-onboard-custom-workflow-portal) tutorial or the [On-boarding users to your organization using Lifecycle workflows with Microsoft Graph](/en-us/graph/tutorial-lifecycle-workflows-onboard-custom-workflow) tutorial.

### Edit the users attributes using the Microsoft Entra admin center

Some of the attributes required for the prehire onboarding tutorial are exposed through the Microsoft Entra admin center and can be set there.

These attributes are:

| Attribute | Description | Set on |
| --- | --- | --- |
| mail | Used to notify manager of the new employees temporary access pass | Manager |
| manager | This attribute that is used by the lifecycle workflow | Employee |

For the tutorial, the **mail** attribute only needs to be set on the manager account and the **manager** attribute set on the employee account. Use the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to &gt; **Entra ID** &gt; **Users**.
3. Select **Melva Prince**.
4. At the top, select **Edit**.
5. Under manager, select **Change** and Select **Britta Simon**.
6. At the top, select **Save**.
7. Go back to users and select **Britta Simon**.
8. At the top, select **Edit**.
9. Under **Email**, enter a valid email address.
10. Select **Save**.

### Edit employeeHireDate

The employeeHireDate attribute is new to Microsoft Entra ID. It isn't exposed through the UI and must be updated using Graph. To edit this attribute, we can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).

Note

Be aware that a workflow won't trigger when the employee hire date (Days from event) is prior to the workflow creation date. You must set an `employeeHireDate` in the future by design. The dates used in this tutorial are a snapshot in time. Therefore, you should change the dates accordingly to accommodate for this situation.

In order to do this, we must get the object ID for our user Melva Prince.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to &gt; **Entra ID** &gt; **Users**.
3. Select **Melva Prince**.
4. Select the copy sign next to the **Object ID**.
5. Now navigate to [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
6. Sign-in to Graph Explorer with the Global Administrator account for your tenant.
7. At the top, change **GET** to **PATCH** and add `https://graph.microsoft.com/v1.0/users/<id>` to the box. Replace `<id>` with the value we copied before.
8. Copy the following in to the **Request body** and select **Run query**

    ```Example
    {
    "employeeHireDate": "2022-04-15T22:10:00Z"
    }
    ```

    [![Screenshot of the PATCH employeeHireDate.](media/tutorial-lifecycle-workflows/update-1.png)](media/tutorial-lifecycle-workflows/update-1.png#lightbox)
9. Verify the change by changing **PATCH** back to **GET** and **v1.0** to **beta**. Select **Run query**. You should see the attributes for Melva set.[![Screenshot of the GET employeeHireDate.](media/tutorial-lifecycle-workflows/update-3.png)](media/tutorial-lifecycle-workflows/update-3.png#lightbox)

### Edit the manager attribute on the employee account

The manager attribute is used for email notification tasks. It emails the manager a temporary password for the new employee. Use the following steps to ensure your Microsoft Entra users have a value for the manager attribute.

1. Still in [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Make sure the top is still set to **PUT** and `https://graph.microsoft.com/v1.0/users/<id>/manager/$ref` is in the box. Change `<id>` to the ID of Melva Prince.
3. Copy the following code into the **Request body**
4. Replace `<managerid>` in the following code with the value of Britta Simons ID.
5. Select **Run query**

    ```Example
    {
      "@odata.id": "https://graph.microsoft.com/v1.0/users/<managerid>"
    }
    ```

    [![Screenshot of Adding a manager in Graph explorer.](media/tutorial-lifecycle-workflows/graph-add-manager.png)](media/tutorial-lifecycle-workflows/graph-add-manager.png#lightbox)
6. Now, we can verify that the manager is set correctly by changing the **PUT** to **GET**.
7. Make sure `https://graph.microsoft.com/v1.0/users/<id>/manager/` is in the box. The `<id>` is still that of Melva Prince.
8. Select **Run query**. You should see Britta Simon returned in the Response.

    [![Screenshot of getting a manager in Graph explorer.](media/tutorial-lifecycle-workflows/graph-get-manager.png)](media/tutorial-lifecycle-workflows/graph-get-manager.png#lightbox)

For more information about updating manager information for a user in Graph API, see [assign manager](/en-us/graph/api/user-post-manager?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) documentation. You can also set this attribute in the Azure Admin center. For more information, see [add or change profile information](../fundamentals/how-to-manage-user-profile-info?context=azure/active-directory/users-groups-roles/context/ugr-context).

### Enabling the Temporary Access Pass (TAP)

A Temporary Access Pass is a time-limited pass issued by an admin that satisfies strong authentication requirements.

In this scenario, we use this feature of Microsoft Entra ID to generate a temporary access pass for our new employee. It's mailed to the employee's manager.

To use this feature, it must be enabled on our Microsoft Entra tenant. To enable this feature, use the following steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Authentication Policy Administrator](../identity/role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Temporary Access Pass**
3. Select **Yes** to enable the policy and add Britta Simon and select which users have the policy applied, and any **General** settings.

## Consideration for leaver scenario

There's an extra step that you should be aware of when testing the tutorials for either the Off-boarding users from your organization using Lifecycle workflows with the Microsoft Entra admin center tutorial, or with Microsoft Graph.

### Set up user with groups and Teams with team membership

A user with groups and Teams memberships is required before you begin the tutorials for the leaver scenario.