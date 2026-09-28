---
layout: Conceptual
title: Prepare Your Environment for User SOA - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/prepare-user-source-of-authority-environment
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn the steps to prepare your environment to use Source of Authority (SOA) for users.
ms.topic: how-to
ms.subservice: hybrid-cloud-sync
ms.date: 2025-08-14T00:00:00.0000000Z
ms.reviewer: dhanyahk
locale: en-us
document_id: 51de996f-1edc-bf9a-9501-06f73bed928f
document_version_independent_id: 51de996f-1edc-bf9a-9501-06f73bed928f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/prepare-user-source-of-authority-environment.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/prepare-user-source-of-authority-environment
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/prepare-user-source-of-authority-environment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c5bda514-898e-755f-2f47-6c05f4bbecc4
---

# Prepare Your Environment for User SOA - Microsoft Entra ID | Microsoft Learn

Once you decide that you want to minimize your on-premises footprint by using Source of Authority for users, you must prepare your Active Directory environment based on how users are configured. How you choose to prepare your environment is based on many factors. For other things to consider, see: [Prerequisites for Transferring User SOA](user-source-of-authority-overview#prerequisites-for-transferring-user-soa) and [Guidance for using User Source of Authority (SOA)](user-source-of-authority-guidance).

The flow for preparing for user SOA is as follows:

![Screenshot of steps to prepare for source of authority.](media/prepare-user-source-of-authority-environment/prepare-source-of-authority-overview.png)

This article walks you through what needs to be completed to prepare Microsoft Exchange, HR integration, and Microsoft Identity Manager environments before switching user SOA.

## Confirm your AD objects are ready to have their SOA changed

Before transferring the SOA of users, retrieve the objects from your Active Directory domain and check that they’re ready to be transferred by confirming the following information:

- Confirm that the objects are already synchronized to Microsoft Entra. Administrative objects, or objects excluded from synchronization, can’t have their SOA changed.
- Confirm that all attributes you have, or plan to modify, on those users are being synched to Microsoft Entra and are visible as either directory attributes, or as *directory schema extensions*: `/graph/api/resources/extensionproperty` in Microsoft Graph.
- Confirm there are no reference-valued attributes populated on those user objects in Active Directory other than the user's manager's attribute, and Active Directory backlinks such as `memberof`. Other reference-valued attributes aren't supported for SOA transfer.
- Confirm that the value of the manager and member attributes, if set, must be references to users in the same Active Directory domain and that they're synchronized to Microsoft Entra. They can’t refer to other object types, or to objects that aren’t synchronized from this domain to Microsoft Entra.
- Confirm that there are no attributes on the objects that are updated by another Microsoft on-premises technology, other than Active Directory Domain Services (AD DS) itself. For example, don’t change the SOA of a user whose `userCertificate` attribute is maintained by [Active Directory Certificate Services](/en-us/windows-server/identity/ad-cs/active-directory-certificate-services-overview).

## Update Active Directory

If you’re planning to only change the SOA for some Active Directory users, and all your users are currently in a single OU using Kerberos applications that don’t use LDAP, we recommend that you create a new AD DS OU for these objects. Having them in a separate OU will enable you to avoid inadvertently making updates to them in Active Directory after the SOA change. Users, whose SOA isn’t changing, can continue to be managed using Active Directory Users and Computers, Active Directory Module for PowerShell, or other Active Directory management tools. After creating an OU, move the objects to that OU. For more information, see: [Move-ADObject](/en-us/powershell/module/activedirectory/move-adobject?view=windowsserver2025-ps&amp;preserve-view=true).

## Prepare your Microsoft Exchange setup

In case you have Exchange Hybrid setup with Microsoft 365 Exchange Online, prepare your Exchange Server and Exchange Online as per the following guidance before switching the SOA of your user accounts. If you're running an Exchange Hybrid configuration, ensure all your mailboxes are migrated to Exchange Online before you switch the SOA for any users to the cloud. After mailbox migration of all users, these users can be managed in Microsoft 365, and you can safely switch SOA of users to cloud. With SOA switched, you disable Exchange Hybrid by completing following steps:

1. Point the MX and Autodiscover DNS records to Exchange Online instead of Exchange Server.
2. Remove the Service Connection Point (SCP) values on Exchange servers. This step ensures that no SCPs are returned, and the Outlook clients use the DNS method for Autodiscover.
3. (Optional) To secure your environment, remove the inbound and outbound connectors created by the Hybrid Configuration Wizard used for mail flow between Exchange Server and Exchange online.
4. (Optional) To secure your environment, remove the organization relationship, Fed Trust, and oauth trust set up between Exchange Server and Exchange Online by HCW.
5. Stop writing to on-premises Exchange for the object and sync the object to cloud to ensure EXO has the latest changes from on-premises.

For more information on disabling Exchange Hybrid, see: see: [Manage recipients in Exchange Hybrid environments using Management tools](/en-us/Exchange/manage-hybrid-exchange-recipients-with-management-tools).

## Shift the configuration of users in provisioning from the HR system

The next step in setting up SOA is to determine your provisioning strategy for your HR system. In the pre-SOA world, users from your HR system are first provisioned in on-premises Active Directory and then synced to Microsoft Entra ID using Microsoft Entra Connect Sync or Cloud Sync. If you’re using Microsoft Entra provisioning service, you have most likely configured one of the following apps: Workday to AD user provisioning, SAP SuccessFactors to AD user provisioning or API-driven provisioning to AD. The following diagram depicts the data flow in this configuration.

![Screenshot of HR system before transferring source of authority.](media/prepare-user-source-of-authority-environment/before-conversion.png)

To update this configuration, first identify employees from your HR system who can be provisioned into Microsoft Entra ID directly, and are no longer needed in Active Directory. You can take a phased approach to identify such employees using grouping constructs available in HR, for example: transferring SOA of users by department, cost center, or location. Then update your Microsoft Entra provisioning configuration as described in the following section:

### Update your HR provisioning configuration

Once you identify the employees for SOA conversion, follow these steps:

1. Stop the “*HR to on-premises Active Directory*” provisioning job.
2. For users eligible for SOA conversion, switch the SOA of the users from on-premises Active Directory to Entra ID.
3. Create a new “*HR to Microsoft Entra ID*” provisioning application to provision users from your HR system to Entra ID. Use scoping filters to restrict this app to only handle SOA converted users. For example: In the first phase, if you’re converting SOA only for users in the “Finance” department, then set the scoping filter as department EQUALS “Finance”. Expand the scoping filter in future phases to include more users.
4. Start the new “*HR to Microsoft Entra ID*” provisioning job.
5. Update the configuration of your “HR to on-premises Active Directory” provisioning app to exclude the SOA converted users from syncing to AD. Ensure that the skip out of scope deletions flag is set on the provisioning job. Continuing with the example above, you can exclude “Finance” department users from syncing to AD by setting the filter department NOT EQUALS “Finance”.
6. Restart the “*HR to on-premises Active Directory*” provisioning job.
7. Update the configuration of your Entra Connect Sync / Cloud Sync app to exclude the SOA converted users from syncing to Entra ID using a similar scoping filter.

The following diagram depicts the new SOA-aware provisioning configuration:

![Screenshot of HR system source of authority after conversion.](media/prepare-user-source-of-authority-environment/after-conversion.png)

## Prepare your MIM setup

For customers using Microsoft Identity Manager(MIM), you can update the sync rules in MIM to determine which objects continue to be provisioned into Active Directory, and which ones are provisioned into Microsoft Entra ID.

![Screenshot of MIM Set up for SOA.](media/prepare-user-source-of-authority-environment/prepare-identity-setup.png)

To prepare your MIM setup for user SOA, do the following steps:

1. Select the attributes that will be the unique identifiers for users that are the same in both Active Directory and Microsoft Entra.
2. Add the [Microsoft Identity Manager connector for Microsoft Graph](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-connector-graph) to MIM sync, configure a join of the existing Active Directory users brought in from this connector.
3. Check the precedence settings on the user.
4. Perform a full import from Microsoft Entra using the Microsoft Graph connector.
5. Confirm that all the users planned for the SOA conversion are joined between the metaverse and the Microsoft Graph connector.
6. Update the management system for those users (for example, MIM Portal and Service) to add a label to user objects for which the SOA is changing to Microsoft Entra ID.
7. Update the sync rules so that you’re no longer syncing those labeled user objects from MIM to Active Directory, but instead synching to the Microsoft Graph connector.
8. Keep the sync rules deactivated until the SOA transfer is complete.
9. After the SOA transfer, resync users. Confirm there are no exports pending to the AD MA for users whose SOA changed, only to the Microsoft Graph connector.
10. Add to your run profile schedules a run of exporting changes from MIM to Microsoft Entra ID using the Microsoft Graph connector.
11. If you’re no longer exporting any changes to other users in Active Directory, then remove the export to AD run profile from your run profile schedules.

Once these steps are completed, your MIM-synced hybrid environment should follow this diagram: ![Screenshot of a diagram of an environment that's ready to use user SOA.](media/prepare-user-source-of-authority-environment/identity-ready-for-source-of-authority.png)

## Sequence of steps for using SOA

Once your environment is prepped for transferring user SOA, the sequence for transferring SOA is as follows:

1. Identify the users and/or groups for whom you’re going to Switch the source of authority (SOA) to Microsoft Entra ID. Ensure these users and groups are currently being synced using Microsoft Entra Connect Sync or Microsoft Entra Cloud Sync.

    Note

    Switch SOA of groups before switching SOA of users.
2. Remove these users from the App-&gt; AD provisioning configuration (for example, Workday to AD or MIM to AD etc.) so they no longer sync into AD.
3. Wait for the sync cycle to complete and make sure the object data is the same between AD and Microsoft Entra ID.
4. Stop making any changes to these users and/or groups in AD directly.
5. Switch the SOA of the users and/or groups.
6. Confirm that the users and/or groups can now be managed from the cloud by following these steps.

    1. Go to the Microsoft Entra admin center and find the user/group you switched SOA of and see if they’re a cloud object and can be edited (or)
    2. Run this script to check if the “DirSync” and “isCloudManaged” attribute it set to cloud.
    3. Check the events listed in the Audit log to see whether the SOA status has changed.
7. Continue to keep the users and/or groups in scope for Connect/Cloud Sync. This is needed if these objects have references to groups, devices, and contacts managed in AD.
8. Change the direction of provisioning for users you stopped syncing in order to ensure these user changes are provisioned directly into Microsoft Entra ID from the corresponding HR systems.

    1. Create a new provisioning configuration to provision the users no longer synced from equivalent cloud app system to Microsoft Entra ID using Provisioning API.
    2. Start provisioning the same users from the cloud system (HR or other apps) into Microsoft Entra directly.
    3. At this point, SOA transfer is complete, and the identities have started flowing from the cloud system to Microsoft Entra ID, and Microsoft Entra ID is the source of authority.