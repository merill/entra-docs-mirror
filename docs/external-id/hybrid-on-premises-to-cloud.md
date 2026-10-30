---
layout: Conceptual
title: Sync local partner accounts to cloud as B2B users - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/hybrid-on-premises-to-cloud
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Give locally managed external partners access to both local and cloud resources using the same credentials with Microsoft Entra B2B collaboration.
ms.topic: how-to
ms.date: 2026-04-24T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 57db217b-bfef-ec10-3a7d-72169cc4acb0
document_version_independent_id: e054a542-1597-2f4f-d802-3a6d7de84a9d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/hybrid-on-premises-to-cloud.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/hybrid-on-premises-to-cloud
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/hybrid-on-premises-to-cloud.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 28d138a0-d869-fd85-380e-243bc2ee8c87
---

# Sync local partner accounts to cloud as B2B users - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Before Microsoft Entra ID, organizations with on-premises identity systems have managed partner accounts in their on-premises directory. In such an organization, when you start to move apps to Microsoft Entra ID, you want to make sure your partners can access the resources they need. It shouldn't matter whether the resources are on-premises or in the cloud. Also, you want your partner users to be able to use the same sign-in credentials for both on-premises and Microsoft Entra resources.

If you create accounts for your external partners in your on-premises directory (for example, you create an account with a sign-in name of "msullivan" for an external user named Maria Sullivan in your partners.contoso.com domain), you can now sync these accounts to the cloud. Specifically, you can use [Microsoft Entra Connect](../identity/hybrid/connect/whatis-azure-ad-connect) to sync partner accounts to the cloud, which creates a user account with UserType = Guest. This configuration enables partner users to access cloud resources by using the same credentials as their local accounts, without giving them more access than they need. For more information about converting local guest accounts, see [Convert local guest accounts to Microsoft Entra B2B guest accounts](../architecture/10-secure-local-guest).

Note

See also [Invite internal users to B2B collaboration](invite-internal-users). With this feature, you can invite internal guest users to use B2B collaboration, regardless of whether you've synced their accounts from your on-premises directory to the cloud. Once the user accepts the invitation, they can use their own identities and credentials to sign in to the resources you want them to access. You won't need to maintain passwords or manage account lifecycles.

## Identify unique attributes for UserType

Before you enable synchronization of the UserType attribute, you must first decide how to derive the UserType attribute from on-premises Active Directory. In other words, what parameters in your on-premises environment are unique to your external collaborators? Determine a parameter that distinguishes these external collaborators from members of your own organization.

The two common approaches to defining the parameter are:

- Designate an unused on-premises Active Directory attribute (for example, extensionAttribute1) to use as the source attribute.
- Alternatively, derive the value for UserType attribute from other properties. For example, you want to synchronize all users as Guest if their on-premises Active Directory UserPrincipalName attribute ends with the domain *@partners.contoso.com*.

For detailed attribute requirements, see [Enable synchronization of UserType](../identity/hybrid/connect/how-to-connect-sync-change-the-configuration#enable-synchronization-of-usertype).

## Configure Microsoft Entra Connect to sync users to the cloud

After you identify the unique attribute, you can configure Microsoft Entra Connect to sync these users to the cloud, which creates a user account with UserType = Guest. From an authorization point of view, these users are indistinguishable from B2B users created through the Microsoft Entra B2B collaboration invitation process.

For implementation instructions, see [Enable synchronization of UserType](../identity/hybrid/connect/how-to-connect-sync-change-the-configuration#enable-synchronization-of-usertype).