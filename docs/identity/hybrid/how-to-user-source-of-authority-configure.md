---
layout: Conceptual
title: Configure user Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/how-to-user-source-of-authority-configure
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to transfer user management from Active Directory Domain Services (AD DS) to Microsoft Entra ID by using user Source of Authority (SOA).
ms.subservice: hybrid-cloud-sync
ms.topic: how-to
ms.date: 2026-04-15T00:00:00.0000000Z
ms.reviewer: dhanyahk
ai-usage: ai-assisted
locale: en-us
document_id: b71baecb-d131-4706-917a-402af587d9e4
document_version_independent_id: b71baecb-d131-4706-917a-402af587d9e4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/how-to-user-source-of-authority-configure.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/how-to-user-source-of-authority-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/how-to-user-source-of-authority-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 8e0d67b2-824b-8727-69db-4bbe391e051b
---

# Configure user Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article explains the prerequisites and steps to configure both User, and Contact, Source of Authority (SOA). This article also explains how to revert changes, and current feature limitations. For a full overview for User SOA, see [Embrace cloud-first posture: Transfer User Source of Authority to the cloud](user-source-of-authority-overview).

## Prerequisites

| Requirement | Description |
| --- | --- |
| **Roles** | [Hybrid Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-administrator) is required to call the Microsoft Graph APIs to read and update SOA of users.[Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) or [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) is required to grant user consent to the required permissions to Microsoft Graph Explorer or the app used to call the Microsoft Graph APIs. |
| **Permissions** | For apps calling into the `onPremisesSyncBehavior` Microsoft Graph API, the `User-OnPremisesSyncBehavior.ReadWrite.All` permission scope needs to be granted. For more information, see [how to consent to this permission](how-to-user-source-of-authority-configure#consent-permission-to-apps) using the Microsoft Entra Admin Center. |
| **License needed** | Microsoft Entra Free license. |
| **Connect Sync client** | Minimum version is [2.5.76.0](/en-us/entra/identity/hybrid/connect/reference-connect-version-history#25760). To use Contact SOA, version [2.5.79.0](connect/reference-connect-version-history#25790). |
| **Cloud Sync client** | Minimum version is [1.1.1370.0](/en-us/entra/identity/hybrid/cloud-sync/reference-version-history#1113700) |

## Setup

You need to set up Connect Sync client and the Microsoft Entra Provisioning agent.

### Connect sync client

1. Download the latest version of the Connect Sync build.
2. Verify the Connect Sync build is successfully installed. Go to **Programs** in Control Panel and confirm that the version of Microsoft Entra Connect Sync is [2.5.76.0](/en-us/entra/identity/hybrid/connect/reference-connect-version-history#25760).

### Cloud sync client

Download the Microsoft Entra Provisioning agent with build version [1.1.1370.0](/en-us/entra/identity/hybrid/cloud-sync/reference-version-history#1113700) or later.

1. Follow the [instructions to download the Cloud Sync client](/en-us/entra/identity/hybrid/cloud-sync/reference-version-history#download-link).
2. Learn how to [identify the agent's current version](/en-us/azure/active-directory/hybrid/cloud-sync/how-to-automatic-upgrade).
3. Follow the [instructions to configure provisioning from AD DS to Microsoft Entra ID](/en-us/entra/identity/hybrid/cloud-sync/how-to-configure).

## Consent permission to apps

You can consent permission in the Microsoft Entra admin center. This highly privileged operation requires the Application Administrator or Cloud Application Administrator role. You can also grant consent by using PowerShell. For more information, see [Grant consent on behalf of a single user](/en-us/entra/identity/enterprise-apps/grant-consent-single-user?pivots=ms-graph).

### Custom apps

Follow these steps to grant `User-OnPremisesSyncBehavior.ReadWrite.All` permission to the corresponding app. For more information about how to add new permissions to your app registration and grant consent, see [Update an app's requested permissions in Microsoft Entra ID](/en-us/entra/identity-platform/howto-update-permissions).

Note

To transfer SOA of a Contact, the required permission is `Contacts-OnPremisesSyncBehavior.ReadWrite.All`.

### Use Microsoft Entra admin center to consent permission to apps

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) or a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Enterprise Apps** &gt; ***App name***.
3. Select **Permissions** &gt; **Grant admin consent for *tenant name***.
4. Sign in again as an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator) or a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
5. Review the list of permissions that require your consent, and select **Accept**.
6. You can see the list of permissions that you granted:

![Screenshot of how to validate a permission is granted.](media/how-to-user-source-of-authority-configure/permission.png)

### Grant permission to Graph Explorer

1. Open [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and sign in as an [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) or [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Select the profile icon, and select **Consent to permissions**.
3. Search for User-OnPremisesSyncBehavior, and select **Consent** for the permission. ![screenshot of graph permissions.](media/how-to-user-source-of-authority-configure/graph-permissions.png)

## Transfer SOA for a test user

Note

You're also able to transfer contact SOA using the `https://graph.microsoft.com/v1.0/contacts` API endpoint.

Follow these steps to transfer the SOA for a test user:

1. Create a user within AD. You can also use an existing user that is synced to Microsoft Entra ID by using Connect Sync.
2. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
3. Verify that the user appears in the Microsoft Entra admin center as a synced user.
4. Use Microsoft Graph API to transfer the SOA of the user object (*isCloudManaged*=true). Open [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and sign in with an appropriate user role, such as user admin.
5. Let's check the existing SOA status. We didn’t update the SOA yet, so the *isCloudManaged* attribute value should be false. Replace the *{ID}* in the following examples with the object ID of your user. For more information about this API, see [Get onPremisesSyncBehavior](/en-us/graph/api/onpremisessyncbehavior-get). /graph/api/onpremisessyncbehavior-update

    ```https
    GET https://graph.microsoft.com/v1.0/users/{ID}/onPremisesSyncBehavior?$select=isCloudManaged
    ```

    ![Screenshot of GET call to verify user properties.](media/how-to-user-source-of-authority-configure/cloud-managed.png)
6. Confirm that the synced user is read-only. Because the user is managed on-premises, any write attempts to the user in the cloud fail. The error message differs for mail-enabled users, but updates still aren't allowed.

    Note

    If this API fails with 403, use the **Modify permissions** tab to grant consent to the required User.ReadWrite.All permission.

    ```https
    PATCH https://graph.microsoft.com/v1.0/users/{ID}/
       {
         "DisplayName": "User Name Updated"
       }   
    ```

    ![Screenshot of an attempt to update a user to verify it's read-only.](media/how-to-user-source-of-authority-configure/try-update.png)
7. Search the Microsoft Entra admin center for the user. Verify that all user fields are greyed out, and that source is Windows Server AD DS.
8. Now you can update the SOA of the user to be cloud-managed. Run the following operation in Microsoft Graph Explorer for the user object you want to transfer to the cloud. For more information about this API, see [Update onPremisesSyncBehavior](/en-us/graph/api/onpremisessyncbehavior-update).

    ```https
    PATCH https://graph.microsoft.com/v1.0/users/{ID}/onPremisesSyncBehavior
       {
         "isCloudManaged": true
       }   
    ```

    ![Screenshot of PATCH operation to update user properties.](media/how-to-user-source-of-authority-configure/switch.png)
9. To validate the change, call GET to verify *isCloudManaged* is true.

    ```https
    GET https://graph.microsoft.com/v1.0/users/{ID}/onPremisesSyncBehavior?$select=isCloudManaged
    ```

    ![Screenshot of how to use Microsoft Graph Explorer to get the SOA value of a user.](media/how-to-user-source-of-authority-configure/get-user.png)
10. Confirm the change in the Audit Logs. To access Audit Logs in the Azure portal, open **Manage Microsoft Entra ID** &gt; **Monitoring** &gt; **Audit Logs**, or search for *audit logs*. Select **Change Source of Authority from AD to cloud** as the activity.
11. Check that the user can be updated in the cloud.

    ```https
    PATCH https://graph.microsoft.com/v1.0/users/{ID}/
       {
         "DisplayName": "Update User Name"
       }   
    ```

    ![Screenshot of a retry to change user properties.](media/how-to-user-source-of-authority-configure/retry-update.png)
12. Open Microsoft Entra admin center and confirm that the user **On-premises sync enabled** property is **Yes**.

## Connect Sync client

1. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
2. To look at the user object with transferred SOA, in the **Synchronization Service Manager**, go to **Connectors**:

    ![Screenshot of Connectors.](media/how-to-user-source-of-authority-configure/connectors.png)
3. Right-click **Active Directory Domain Services Connector**. Search for the user by the relative domain name (RDN) setting "CN=&lt;UserName&gt;":

    ![Screenshot of how to search for RDN.](media/how-to-user-source-of-authority-configure/search.png)
4. Double-click the searched entry, and select **Lineage** &gt; **Metaverse Object Properties**.

    ![Screenshot of how to view lineage.](media/how-to-user-source-of-authority-configure/lineage.png)
5. Select **Connectors** and double-click the **Microsoft Entra ID object** with "CN={&lt;Alphanumeric Characters&gt;}".
6. You can see that the **blockOnPremisesSync** property is set to true on the Microsoft Entra ID object. This property value means that any changes made in the corresponding AD DS object don't flow to the Microsoft Entra ID object:

    ![Screenshot of how to block data flow.](media/how-to-user-source-of-authority-configure/block.png)
7. Let’s update the on-premises user object. We change the user name from *TestUserF1* to *TestUserF1.1*:

    ![Screenshot of how to change the object name.](media/how-to-user-source-of-authority-configure/change-name.png)
8. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
9. Open Event viewer and filter the Application log for event ID 6956. This event ID is reserved to inform the customers that the object isn't synced to the cloud because the SOA of the object is in the cloud.

    ![Screenshot of event ID 6956.](media/how-to-user-source-of-authority-configure/event-6956.png)

### Status of attributes after you transfer SOA

The following table explains the status for *isCloudManaged* and *onPremisesSyncEnabled* attributes after you transfer the SOA of an object.

| Admin step | isCloudManaged value | onPremisesSyncEnabled value | Description |
| --- | --- | --- | --- |
| Admin syncs an object from AD DS to Microsoft Entra ID | `false` | `true` | When an object is originally synchronized to Microsoft Entra ID, the *onPremisesSyncEnabled* attribute is set to `true` and *isCloudManaged* is set to `false`. |
| Admin transfers the source of authority (SOA) of the object to the cloud | `true` | `null` | After an admin transfers the SOA of an object to the cloud, the *isCloudManaged* attribute becomes set to `true` and the *onPremisesSyncEnabled* attribute value is set to `null`. |
| Admin rolls back the SOA operation | `false` | `null` | If an admin transfers the SOA back to AD, the *isCloudManaged* is set to `false` and *onPremisesSyncEnabled* is set to `null` until the sync client takes over the object. |
| Admin creates a cloud native object in Microsoft Entra ID | `false` | `null` | If an admin creates a new cloud-native object in Microsoft Entra ID, *isCloudManaged* is set to `false` and *onPremisesSyncEnabled* is set to `null`. |
| Admin creates a cloud native object in Microsoft Entra ID | `false` | `null` | If an admin creates a new cloud-native object in Microsoft Entra ID, *isCloudManaged* is set to `false` and *onPremisesSyncEnabled* is set to `null`. |

## Roll back SOA update

Important

Make sure that the users that you roll back have no cloud references. Remove cloud users from SOA transferred groups, and remove these groups from access packages before you roll back the users to AD DS. The sync client takes over the object in the next sync cycle.

Follow these steps to roll back the SOA update and revert the SOA to on-premises:

1. Disable the `blockCloudObjectTakeoverThroughHardMatchEnabled` feature flag. This flag blocks switching source of authority from cloud to on-premises by default. Issue the following request to Microsoft Graph to disable it:

    ```http
    PATCH https://graph.microsoft.com/beta/directory/onPremisesSynchronization/{id}
    {
        "features": {
            "blockCloudObjectTakeoverThroughHardMatchEnabled": false
        }
    }
    ```

    Replace `{id}` with the on-premises directory synchronization configuration ID for your tenant.
2. Run the following operation to roll back the SOA and revert to on-premises management.

    ```https
    PATCH https://graph.microsoft.com/v1.0/users/{ID}/onPremisesSyncBehavior
       {
         "isCloudManaged": false
       }   
    ```

    ![Screenshot of API call to revert SOA.](media/how-to-user-source-of-authority-configure/rollback.png)

Note

The change of *isCloudManaged* to `false` allows an AD DS object that's in scope for sync to be taken over by Connect Sync the next time it runs. Until the next time Connect Sync runs, the object can be edited in the cloud. The rollback of SOA is finished only after *both* the API call and the next scheduled or forced run of Connect Sync are complete.

### Validate the change in the audit logs

Select activity as **Undo changes to Source of Authority from AD DS to cloud**:

![Screenshot of Undo Changes in Audit Logs.](media/how-to-user-source-of-authority-configure/audit-undo-changes.png)

## Validate in Connect Sync client

1. Run the following command to start Connect Sync:

    ```powershell
    Start-ADSyncSyncCycle
    ```
2. Open the object in the **Synchronization Server Manager** (details are in the Connect Sync Client section). You can see the state of the Microsoft Entra ID connector object is **Awaiting Export Confirmation** and *blockOnPremisesSync* = false, which means the object SOA is taken over by the on-premises again.

    ![Screenshot of an object awaiting export.](media/how-to-user-source-of-authority-configure/await-export.png)

Important

After the rollback is complete and Connect Sync takes over the object, re-enable the `blockCloudObjectTakeoverThroughHardMatchEnabled` feature flag to maintain protection against unintended cloud object takeover:

```http
PATCH https://graph.microsoft.com/beta/directory/onPremisesSynchronization/{id}
{
    "features": {
        "blockCloudObjectTakeoverThroughHardMatchEnabled": true
    }
}
```

## Clear on-premises attributes for SOA transferred users

The following are the list of on-premises [properties](/en-us/graph/api/resources/user#properties) present on the cloud user object that are used for accessing on-premises resources:

- onPremisesDistinguishedName
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesSecurityIdentifier
- onPremisesUserPrincipalName

If Admins want to access on-premises resources after transfer of SOA, you must [manually maintain these attributes using Microsoft Graph](/en-us/graph/api/resources/user), and not delete, these attributes.

## Scope a user for SOA operations within an Administrative Unit

To scope a user for Source of Authority operations within an Administrative Unit, do the following steps:

1. Create a unit to use as the scope for the user. For steps on creating a unit, see: [Create an administrative unit](../role-based-access-control/admin-units-manage#create-an-administrative-unit).
2. Add the user as a Hybrid Identity Administrator within the scope. [![Screenshot of assigning a hybrid admin role to an Administrative unit scope.](media/how-to-user-source-of-authority-configure/assign-scope-role.png)](media/how-to-user-source-of-authority-configure/assign-scope-role.png#lightbox)
3. Add users to the unit. For information on this, see: [Add users, groups, or devices to an administrative unit](../role-based-access-control/admin-units-members-add).
4. Transfer the SOA of users within the scope of the unit. For a guide on transferring the SOA of users, see: [Transfer SOA for a test user](how-to-user-source-of-authority-configure#transfer-soa-for-a-test-user).

## Configure Contact SOA

You're also able to transfer the SOA of contacts of users using the examples provided in this article. Contacts are items in Outlook where you can organize and save information about the people and organizations you communicate with. The following examples are of how you would transfer the SOA of contacts.

Note

To transfer SOA of a Contact, the required permission is `Contacts-OnPremisesSyncBehavior.ReadWrite.All`.

To confirm the contact SOA is cloud managed, you run the following API call:

```https
GET https://graph.microsoft.com/v1.0/contacts/{ID}/onPremisesSyncBehavior?$select=isCloudManaged
```

To update the cloud-managed contact, you can make the following API call:

```https
   PATCH https://graph.microsoft.com/v1.0/contacts/{ID}/
      {
        "DisplayName": "Contact Name Updated"
      }   
```