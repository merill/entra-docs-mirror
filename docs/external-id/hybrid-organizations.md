---
layout: Conceptual
title: B2B collaboration for hybrid organizations - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/hybrid-organizations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Give partners access to both on-premises and cloud resources with Microsoft Entra B2B collaboration.
ms.topic: concept-article
ms.date: 2024-10-21T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: ff4624ff-f7d8-076c-119d-a49d9a4c1aa5
document_version_independent_id: 28a8a57c-5e98-e105-b4c2-856cf0b18107
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/hybrid-organizations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/hybrid-organizations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/hybrid-organizations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b97a02ff-2b5c-0561-7ec6-6ec0b57aa0e0
---

# B2B collaboration for hybrid organizations - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra B2B collaboration makes it easy for you to give your external partners access to apps and resources in your organization. This is true even in a hybrid configuration where you have both on-premises and cloud-based resources. It doesn’t matter if you currently manage external partner accounts locally in your on-premises identity system, or if you manage the external accounts in the cloud as Microsoft Entra B2B users. You can now grant these users access to resources in either location, using the same sign-in credentials for both environments.

## Grant B2B users in Microsoft Entra ID access to your on-premises apps

If your organization uses Microsoft Entra B2B collaboration capabilities to invite guest users from partner organizations to your Microsoft Entra ID, you can now provide these B2B users access to on-premises apps.

For apps that use SAML-based authentication, you can make these apps available to B2B users through the Azure portal, using Microsoft Entra application proxy for authentication.

For apps that use integrated Windows authentication (IWA) with Kerberos constrained delegation (KCD), you also use Microsoft Entra ID Proxy for authentication. However, for authorization to work, a user object is required in the on-premises Windows Server Active Directory. There are two methods you can use to create local user objects that represent your B2B guest users.

- You can use Microsoft Identity Manager (MIM) 2016 SP1 and the MIM management agent for Microsoft Graph.
- You can use a PowerShell script. (This solution doesn't require MIM.)

For details about how to implement these solutions, see [Grant Microsoft Entra B2B users access to your on-premises applications](hybrid-cloud-to-on-premises).

## Grant locally managed partner accounts access to cloud resources

Before Microsoft Entra ID, organizations with on-premises identity systems have traditionally managed partner accounts in their on-premises directory. If you’re such an organization, you want to make sure that your partners continue to have access as you move your apps and other resources to the cloud. Ideally, you want these users to use the same set of credentials to access both cloud and on-premises resources.

We now offer methods where you can use Microsoft Entra Connect to sync these local accounts to the cloud as "guest users," where the accounts behave just like Microsoft Entra B2B users.

To help protect your company data, you can control access to just the right resources, and configure authorization policies that treat these guest users differently from your employees.

For implementation details, see [Grant locally managed partner accounts access to cloud resources using Microsoft Entra B2B collaboration](hybrid-on-premises-to-cloud).