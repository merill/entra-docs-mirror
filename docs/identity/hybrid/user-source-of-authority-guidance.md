---
layout: Conceptual
title: Guidance for using user Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/user-source-of-authority-guidance
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: dougeby
description: Streamline user management with User Source of Authority (SOA) in Microsoft Entra ID. Minimize your AD footprint and ensure a smooth migration to the cloud.
ms.topic: concept-article
ms.subservice: hybrid-cloud-sync
ms.date: 2025-09-30T00:00:00.0000000Z
ms.reviewer: dhanyahk
locale: en-us
document_id: 3bf1a807-f6b1-ef15-0bbf-47461269a383
document_version_independent_id: 3bf1a807-f6b1-ef15-0bbf-47461269a383
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/user-source-of-authority-guidance.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/user-source-of-authority-guidance
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/user-source-of-authority-guidance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 26c38dff-8ba3-4c00-5012-7874cc00c480
---

# Guidance for using user Source of Authority (SOA) in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Managing user identities effectively is critical for organizations transitioning to the cloud. This article provides guidance on using user Source of Authority (SOA) to help transition users from on-premises to the cloud. How to minimize your Active Directory (AD) footprint after SOA transfer, adopt best practices for transitioning user management, and ensure a smooth migration of user management to the cloud are also covered in this article.

## Active Directory user management

One of the key scenarios for transferring SOA for users, is the ability to minimize your AD footprint. Once you complete the SOA transfer, users who no longer require access to Active Directory-specific resources can be disabled within AD, or deleted completely.

Note

If users still require access to on-premises resources after SOA transfer, then these attributes must be maintained manually using Microsoft Graph. For more information on these attributes, see: [Clear on-premises attributes for SOA transferred users](how-to-user-source-of-authority-configure#clear-on-premises-attributes-for-soa-transferred-users)

## Best practices

Follow these best practices to transition user management from on-premises to Microsoft Entra ID

### Move users to an OU

Using Active Directory management tools like Active Directory Users and Computers or the Active Directory module for PowerShell to modify AD objects with a changed Source of Authority (SOA) can lead to inconsistencies in their Microsoft Entra representation. Before you perform a SOA change, your organization should move those objects to a designated AD OU that signals that those objects should no longer be managed via AD tools. If the user who’s SOA you want to transfer is referenced in an on-premises managed group, then the user should remain in the sync scope. If you delete the on-premises user, then it's also removed from both the on-premises and Microsoft Entra group.

### Transition user management

Before shifting the SOA of users, ensure the sync cycle of the users is complete. Once complete, remove the users from the scope of the HR to AD, or MIM to AD configuration, and add them to your HR-&gt;Microsoft Entra ID configuration. If your organization uses Microsoft Identity Manager (MIM) with the Active Directory Management Agent (AD MA) to manage AD users and groups, you must update the sync logic to stop exporting changes to those objects via AD MA before making an SOA change. Instead of using the AD MA, you can have MIM update the objects in Microsoft Entra using the [MIM connector for Microsoft Graph](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-connector-graph) so that the changes made by MIM are first sent to Microsoft Entra, and then to Active Directory where needed. For more information, see: [Prepare your MIM setup](prepare-user-source-of-authority-environment#prepare-your-mim-setup). Stop making any changes directly to the user in AD. Once SOA is complete, begin management of users within the cloud.

### Users using LDAP applications

If you want to shift users using on-premises LDAP applications to the cloud, use [Microsoft Entra Domain services](../domain-services/overview) to shift the LDAP application to the cloud before transferring the SOA of users.

### Third-party federated authentication

If your organization uses a third-party federation authentication identity provider and plans to transfer the SOA of users, you must manage the Active Directory account manually and maintain the password using the third-party sync tool. If users are using federated authentication using [Active Directory Federation Service](/en-us/windows-server/identity/ad-fs/ad-fs-overview), then transferring SOA isn't supported.

### Devices

We recommend that customers migrate their devices to the cloud, and use a Microsoft Entra Joined Device setup in order to fully use user SOA capabilities. For groups, there’s no prerequisites around devices.