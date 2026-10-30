---
layout: Conceptual
title: What are access reviews? - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/access-reviews-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Using access reviews, you can control group membership and application access to meet governance, risk management, and compliance initiatives in your organization.
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: reference
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: mwahl
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 3a8a3416-ca49-e148-89ec-aa004914eaa5
document_version_independent_id: 6e6831f4-40ed-4058-5a6f-56cd3900460a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/access-reviews-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/access-reviews-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/access-reviews-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 141e61f0-5a16-9b4a-c595-f2e202167a33
---

# What are access reviews? - Microsoft Entra - Microsoft Entra ID Governance | Microsoft Learn

Access reviews in Microsoft Entra ID, part of Microsoft Entra, enable organizations to efficiently manage group memberships, access to enterprise applications, and role assignments. User access can be reviewed regularly to make sure only the right people have continued access.

Here's a video that provides a quick overview of access reviews:

## Why are access reviews important?

Microsoft Entra ID enables you to collaborate with users from inside your organization, and with external users. Users can join groups, invite guests, connect to cloud apps, and work remotely from either their work or personal devices. The convenience of using self-service has led to a need for better access management capabilities.

- As new employees join, how do you ensure they have the access they need to be productive?
- As people move teams or leave the company, how do you make sure that their old access is removed?
- Excessive access rights can lead to compromises.
- Excessive access rights can also lead to audit findings as they indicate a lack of control over access.
- You have to proactively engage with resource owners to ensure they regularly review who has access to their resources.

## When should you use access reviews?

- **Too many users in privileged roles:** It's a good idea to check how many users have administrative access, how many of them are Global Administrators, and if there are any invited guests or partners that haven't been removed after being assigned to do an administrative task. You can recertify the role assignment users in [Microsoft Entra roles](privileged-identity-management/pim-perform-roles-and-resource-roles-review?toc=/azure/active-directory/governance/toc.json) such as Global Administrators, or [Azure resources roles](privileged-identity-management/pim-perform-roles-and-resource-roles-review?toc=/azure/active-directory/governance/toc.json) such as User Access Administrator in the [Microsoft Entra Privileged Identity Management (PIM)](privileged-identity-management/pim-configure) experience.
- **When automation is not possible:** You can create rules for dynamic membership groups, security groups, or Microsoft 365 Groups, but what if the HR data isn't in Microsoft Entra ID or if users still need access after leaving the group to train their replacements? You can then create a review on that group to ensure those who still need access keeps access.
- **When a group is used for a new purpose:** If you have a group that is going to be synced to Microsoft Entra ID, or if you plan to enable the application Salesforce for everyone in the Sales team group, it would be useful to ask the group owner to review the dynamic membership group before it's used in a different risk context.
- **Business critical data access:** for certain resources, such as [business critical applications](identity-governance-applications-prepare), it might be required as part of compliance processes to ask people to regularly reconfirm and give a justification on why they need continued access.
- **To maintain a policy's exception list:** In an ideal world, all users would follow the access policies to secure access to your organization's resources. However, sometimes there are business cases that require you to make exceptions. As the IT admin, you can manage this task, avoid oversight of policy exceptions, and provide auditors with proof that these exceptions are reviewed regularly.
- **Ask group owners to confirm they still need guests in their groups:** Employee access might be automated with other identity and access management features such lifecycle workflows based on data from an HR source, but not invited guests. If a group gives guests access to business sensitive content, then it's the group owner's responsibility to confirm the guests still have a legitimate business need for access.
- **Have reviews recur periodically:** You can set up recurring access reviews of users at set frequencies such as weekly, monthly, quarterly or annually, and the reviewers are notified at the start of each review. Reviewers can approve or deny access with a friendly interface and with the help of smart recommendations.

Note

If you're ready to try access reviews, take a look at [Create an access review of groups or applications](create-access-review).

## Where do you create reviews?

Depending on what you want to review, you create your access review in access reviews, Microsoft Entra enterprise apps, PIM, or entitlement management.

| Access rights of users | Reviewers can be | Review created in | Reviewer experience |
| --- | --- | --- | --- |
| Security group membersOffice group members | Specified reviewersGroup ownersSelf-review | access reviewsMicrosoft Entra groups | Access panel |
| Assigned to a connected app | Specified reviewersSelf-review | access reviewsMicrosoft Entra enterprise apps | Access panel |
| Microsoft Entra role | Specified reviewersSelf-review | [PIM](privileged-identity-management/pim-create-roles-and-resource-roles-review?toc=/azure/active-directory/governance/toc.json) | Microsoft Entra admin center |
| Azure resource role | Specified reviewersSelf-review | [PIM](privileged-identity-management/pim-create-roles-and-resource-roles-review?toc=/azure/active-directory/governance/toc.json) | Microsoft Entra admin center |
| Access package assignments | Specified reviewersGroup membersSelf-review | entitlement management | Access panel |
| Access rights from custom data resources (preview) | Managers | access reviews | Access panel |

## License requirements

This feature requires Microsoft Entra ID Governance or Microsoft Entra Suite subscriptions, for your organization's users. Some capabilities, within this feature, may operate with a Microsoft Entra ID P2 subscription. For more information, see the articles of each capability for more details. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

Note

Creating a review on inactive users and with [user-to-group affiliation](review-recommendations-access-reviews#user-to-group-affiliation) recommendations, or an [access review of multiple resources together (preview)](catalog-access-reviews), requires a Microsoft Entra ID Governance license.