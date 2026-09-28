---
layout: Conceptual
title: Convert local guest accounts to Microsoft Entra B2B guest accounts - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/10-secure-local-guest
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn to convert local guests into Microsoft Entra B2B guest accounts by identifying apps and local guest accounts, migration, and more.
ms.reviewer: gasinh
ms.date: 2023-02-23T00:00:00.0000000Z
ms.topic: how-to
ms.subservice: architecture
locale: en-us
document_id: d2181d1f-ec6c-0596-dd7d-d8382b15018c
document_version_independent_id: df180f38-f6e0-d289-c566-0a5d24d568f6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/10-secure-local-guest.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/10-secure-local-guest
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/10-secure-local-guest.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d8ba7153-5a34-aaa0-abfc-8bf2e607a17e
---

# Convert local guest accounts to Microsoft Entra B2B guest accounts - Microsoft Entra | Microsoft Learn

With Microsoft Entra ID (Microsoft Entra B2B), external users collaborate with their identities. Although organizations can issue local usernames and passwords to external users, this approach isn't recommended. Microsoft Entra B2B has improved security, lower cost, and less complexity, compared to creating local accounts. In addition, if your organization issues local credentials that external users manage, you can use Microsoft Entra B2B instead. Use the guidance in this document to make the transition.

Learn more: [Plan a Microsoft Entra B2B collaboration deployment](secure-external-access-resources)

## Before you begin

This article is number 10 in a series of 10 articles. We recommend you review the articles in order. Go to the **Next steps** section to see the entire series.

## Identify external-facing applications

Before migrating local accounts to Microsoft Entra B2B, confirm the applications and workloads external users can access. For example, for applications hosted on-premises, validate the application is integrated with Microsoft Entra ID. On-premises applications are a good reason to create local accounts.

Learn more: [Grant B2B users in Microsoft Entra ID access to your on-premises applications](../external-id/hybrid-cloud-to-on-premises)

We recommend that external-facing applications have single sign-on (SSO) and provisioning integrated with Microsoft Entra ID for the best end user experience.

## Identify local guest accounts

Identify the accounts to be migrated to Microsoft Entra B2B. External identities in Active Directory are identifiable with an attribute-value pair. For example, making ExtensionAttribute15 = `External` for external users. If these users are set up with Microsoft Entra Connect Sync or Microsoft Entra Connect cloud sync, configure synced external users to have the `UserType` attributes set to `Guest`. If the users are set up as cloud-only accounts, you can modify user attributes. Primarily, identify users to convert to B2B.

## Map local guest accounts to external identities

Identify user identities or external emails. Confirm that the local account (v-lakshmi@contoso.com) is a user with the home identity and email address: lakshmi@fabrikam.com. To identify home identities:

- The external user's sponsor provides the information
- The external user provides the information
- Refer to an internal database, if the information is known and stored

After mapping external local accounts to identities, add external identities or email to the user.mail attribute on local accounts.

## End user communications

Notify external users about migration timing. Communicate expectations, for instance when external users must stop using a current password to enable authentication by home and corporate credentials. Communications can include email campaigns and announcements.

## Migrate local guest accounts to Microsoft Entra B2B

After local accounts have user.mail attributes populated with the external identity and email, convert local accounts to Microsoft Entra B2B by inviting the local account. You can use PowerShell or the Microsoft Graph API.

Learn more: [Invite internal users to B2B collaboration](../external-id/invite-internal-users)

## Post-migration considerations

After you verify external authentication is working, complete the transition:

- Transition external user local accounts to Microsoft Entra B2B and stop creating local accounts
    - Invite external users in Microsoft Entra ID
- Change or randomize local account passwords to phase out legacy authentication
    - This action ensures authentication and user lifecycle is connected to the external user home identity
    - For on-premises accounts, coordinate with your directory services team to disable local credentials.

Important

During conversion, both local and external credentials work simultaneously. This dual authentication period is necessary because external authentication isn't available until invitation acceptance.