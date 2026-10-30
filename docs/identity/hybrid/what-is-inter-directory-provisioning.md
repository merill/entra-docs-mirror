---
layout: Conceptual
title: What is inter-directory provisioning with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/what-is-inter-directory-provisioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Describes overview of identity inter-directory provisioning.
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: e1ec78e2-e021-2e44-b0d2-d44fd2183b35
document_version_independent_id: 6508a127-7832-c56c-5dca-51d82e08df49
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/what-is-inter-directory-provisioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/what-is-inter-directory-provisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/what-is-inter-directory-provisioning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 40e6cf2d-04ba-2be6-197e-52f3eb3bf521
---

# What is inter-directory provisioning with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn

A directory is a shared information infrastructure and is used for locating, managing, administering, and organizing items and network resources. Examples of applications that use directory services are Microsoft Active Directory and Microsoft Entra ID. Identities help directory systems make determinations such as who has access to what, and who is allowed to use specific resources.

Inter-directory provisioning is provisioning an identity between two different directory services systems. The most common scenario for inter-directory provisioning is when a user already in Active Directory is provisioned into Microsoft Entra ID. This provisioning can be accomplished by agents such as Microsoft Entra Connect Sync or Microsoft Entra Connect cloud provisioning.

Inter-directory provisioning allows us to create [hybrid identity](whatis-hybrid-identity) environments.

## What types of inter-directory provisioning does Microsoft Entra ID support

Microsoft Entra ID currently supports three methods for accomplishing inter-directory provisioning. These methods are:

- [Microsoft Entra Cloud Sync](cloud-sync/what-is-cloud-sync) -a new Microsoft agent designed to meet and accomplish your hybrid identity goals. It provides a light-weight inter -directory provisioning experience between Active Directory and Microsoft Entra ID and is configured via the portal.
- [Microsoft Entra Connect](connect/whatis-azure-ad-connect) - the Microsoft tool designed to meet and accomplish your hybrid identity, including inter-directory provisioning from Active Directory to Microsoft Entra ID.
- [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) - Microsoft's on-premises identity and access management solution that helps you manage the users, credentials, policies, and access within your organization. Additionally, MIM provides advanced inter-directory provisioning to achieve hybrid identity environments for Active Directory, Microsoft Entra ID, and other directories.

### Key benefits

This capability of inter-directory provisioning offers the following significant business benefits:

- [Password hash synchronization](connect/whatis-phs) - A sign-in method that synchronizes a hash of a users on-premises AD password with Microsoft Entra ID.
- [Pass-through authentication](connect/how-to-connect-pta) - A sign-in method that allows users to use the same password on-premises and in the cloud, but doesn't require the additional infrastructure of a federated environment.
- [Federation integration](connect/how-to-connect-fed-whatis) - can be used to configure a hybrid environment using an on-premises AD FS infrastructure. It also provides AD FS management capabilities such as certificate renewal and more AD FS server deployments.
- [Synchronization](connect/how-to-connect-sync-whatis) - Responsible for creating users, groups, and other objects. Also for making sure identity information for your on-premises users and groups is matching the cloud. This synchronization also includes password hashes.
- [Health Monitoring](connect/whatis-azure-ad-connect) - can provide robust monitoring and provide a central location in the [Microsoft Entra admin center](https://entra.microsoft.com) to view this activity.

### Common scenarios

For a list of common hybrid synchronization scenarios, see [Common scenarios](common-scenarios).