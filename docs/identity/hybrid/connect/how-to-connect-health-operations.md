---
layout: Conceptual
title: Microsoft Entra Connect Health operations - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-health-operations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes additional operations that can be performed after you have deployed Microsoft Entra Connect Health.
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2026-09-10T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: c0b95e24-8a5f-f136-5c14-fcc71c498c3b
document_version_independent_id: 5b12f1c9-e63a-5e1a-0818-ff94ddb8a156
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-health-operations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-health-operations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-health-operations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 78401489-f244-2bcc-50a5-610bb4e2843a
---

# Microsoft Entra Connect Health operations - Microsoft Entra ID | Microsoft Learn

This topic describes the various operations you can perform by using Microsoft Entra Connect Health.

## Enable email notifications

You can configure the Microsoft Entra Connect Health service to send email notifications when alerts indicate that your identity infrastructure isn't healthy. This occurs when an alert is generated, and when it is resolved.

Note

Email notifications are enabled by default.

### To enable Microsoft Entra Connect Health email notifications

1. Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), and then select **Sync errors**.
2. Select **Notification settings** on the command bar.
3. For **Get email notification for alerts**, select **Yes**.
4. Under **Recipients**, select **All global administrators** if you want all Global Administrators to receive notifications.
5. Under **Custom notification emails**, add any other email addresses that should receive notifications. Use **Remove email** to remove an address.
6. Select **Save**. Changes take effect only after you save them.

[![Screenshot of the Connect Health notification settings panel with callouts for enabling email, choosing recipients, and saving changes.](media/how-to-connect-health-operations/connect-health-notification-settings.png)](media/how-to-connect-health-operations/connect-health-notification-settings.png#lightbox)

Note

When there are issues processing synchronization requests in our backend service, this service sends a notification email with the details of the error to the administrative contact email address(es) of your tenant. We heard feedback from customers that in certain cases the volume of these messages is prohibitively large so we are changing the way we send these messages.

Instead of sending a message for every sync error every time it occurs we will send out a daily digest of all errors the backend service has returned. Sync error emails are sent once a day, based on the previous day's unresolved errors. So if the customer triggers an error, but resolves it fairly quickly, they will not get an email the following day. This enables customers to process these errors in a more efficient manner and reduces the number of duplicate error messages.

## Delete a server or service instance

Note

Microsoft Entra ID P1 or P2 license is required for the deletion steps.

In some instances, you might want to remove a server from being monitored. Here's what you need to know to remove a server from the Microsoft Entra Connect Health service.

When you're deleting a server, be aware of the following:

- This action stops collecting any further data from that server. This server is removed from the monitoring service. After this action, you aren't able to view new alerts, monitoring, or usage analytics data for this server.
- This action doesn't uninstall the Health Agent from your server. If you haven't uninstalled the Health Agent before performing this step, you might see errors related to the Health Agent on the server.
- This action doesn't delete the data already collected from this server. That data is deleted in accordance with the Azure data retention policy.
- After performing this action, if you want to start monitoring the same server again, you must uninstall and reinstall the Health Agent on this server.

The service overview separates the two deletion paths. Select a server to open its details before deleting only that server. Use **Delete** on the service-level command bar only when you intend to delete the entire monitored service instance.

[![Screenshot of the Connect Health service overview with callouts for selecting an individual server and using the service-level Delete action.](media/how-to-connect-health-operations/connect-health-delete-server-or-service.png)](media/how-to-connect-health-operations/connect-health-delete-server-or-service.png#lightbox)

### Delete a server from the Microsoft Entra Connect Health service

Note

Microsoft Entra ID P1 or P2 license is required for the deletion steps.

Microsoft Entra Connect Health for Active Directory Federation Services (AD FS) and Microsoft Entra Connect (Sync):

1. Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), select the applicable service type, and then select the service.
2. In the servers section, select the server that you want to remove. For AD FS, select **View all servers** first.
3. Select **Delete** on the command bar.
4. Confirm by typing the server name in the confirmation box.
5. Select **Delete**.

Microsoft Entra Connect Health for AD Domain Services:

1. Open the **Domain Controllers** dashboard.
2. Select the domain controller to be removed.
3. From the action bar, select **Delete Selected**.
4. Confirm the action to delete the server.
5. Select **Delete**.

### Delete a service instance from Microsoft Entra Connect Health service

In some instances, you might want to remove a service instance. Here's what you need to know to remove a service instance from the Microsoft Entra Connect Health service.

When you're deleting a service instance, be aware of the following:

- This action removes the current service instance from the monitoring service.
- This action doesn't uninstall or remove the Health Agent from any of the servers that were monitored as part of this service instance. If you haven't uninstalled the Health Agent before performing this step, you might see errors related to the Health Agent on the servers.
- All data from this service instance is deleted in accordance with the Azure data retention policy.
- After performing this action, if you want to start monitoring the service, uninstall and reinstall the Health Agent on all the servers. After performing this action, if you want to start monitoring the same server again, uninstall, reinstall, and register the Health Agent on that server.

#### To delete a service instance from the Microsoft Entra Connect Health service

1. Open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), and select the applicable service type.
2. Select the service identifier, such as the farm name, that you want to remove.
3. Select **Delete** on the command bar.
4. Confirm by typing the service name in the confirmation box, such as `sts.contoso.com`.
5. Select **Delete**.

## Manage access with Azure RBAC

[Azure role-based access control (Azure RBAC)](../../role-based-access-control/permissions-reference) for Microsoft Entra Connect Health provides access to users and groups other than Hybrid Identity Administrators. Azure RBAC assigns roles to the intended users and groups, and provides a mechanism to limit the Hybrid Identity Administrators within your directory.

### Roles

Microsoft Entra Connect Health supports the following built-in roles:

| Role | Permissions |
| --- | --- |
| Owner | Owners can *manage access* (for example, assign a role to a user or group), *view all information* (for example, view alerts) from the portal, and *change settings* (for example, email notifications) within Microsoft Entra Connect Health. By default, Microsoft Entra Hybrid Identity Administrators are assigned this role, and this can't be changed. |
| Contributor | Contributors can *view all information* (for example, view alerts) from the portal, and *change settings* (for example, email notifications) within Microsoft Entra Connect Health. |
| Reader | Readers can *view all information* (for example, view alerts) from the portal within Microsoft Entra Connect Health. |

All other roles (such as User Access Administrators or DevTest Labs Users) have no impact to access within Microsoft Entra Connect Health, even if the roles are available in the portal experience.

### Access scope

Microsoft Entra Connect Health supports managing access at two levels:

- **All service instances**: This is the recommended path in most cases. It controls access for all service instances (for example, an AD FS farm) across all role types that are being monitored by Microsoft Entra Connect Health.
- **Service instance**: In some cases, you might need to segregate access based on role types or by a service instance. In this case, you can manage access at the service instance level.

Permission is granted if an end user has access either at the directory or service instance level.

### Allow users or groups access to Microsoft Entra Connect Health

The following steps show how to allow access.

#### Step 1: Select the appropriate access scope

To allow a user access at the *all service instances* level, open [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth), and then select **Role based access control (IAM)**.

To manage access for an individual service instance, open the service and select **Access Control** where available.

The IAM page lets you check existing access, review role assignments and roles, or create an assignment at the selected Connect Health scope.

[![Screenshot of the Connect Health role-based access control page with callouts for adding an assignment, reviewing role information, and granting access at the current scope.](media/how-to-connect-health-operations/connect-health-role-based-access-control.png)](media/how-to-connect-health-operations/connect-health-role-based-access-control.png#lightbox)

#### Step 2: Add users and groups, and assign roles

1. Select **Add**, and then select **Add role assignment**.
2. Select a role, such as **Owner**, **Contributor**, or **Reader**.
3. Search for and select one or more users or groups.
4. Confirm the role assignment.
5. After the assignment is complete, the users and groups appear in the role assignments list.

Now the listed users and groups have access, according to their assigned roles.

Note

- Global Administrators always have full access to all the operations, but Global Administrator accounts aren't present in the preceding list.
- The Invite Users feature isn't supported within Microsoft Entra Connect Health.

#### Step 3: Share the Connect Health location

After you assign permissions, share the [Microsoft Entra Connect Health](https://aka.ms/aadconnecthealth) link with the users or groups.

### Remove users or groups

To remove access, select the user or group in the role assignments list, and then select **Remove**.