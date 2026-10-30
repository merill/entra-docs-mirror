---
layout: Conceptual
title: Allow or block invitations - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/allow-deny-list
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how an administrator creates a list to allow or block B2B collaboration with specific domains by using the Microsoft Entra admin center.
ms.topic: how-to
ms.date: 2026-04-24T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 9e4ee507-3d48-d93b-8f6c-59279b1c0eda
document_version_independent_id: 60683a55-6e81-0e9e-f8fe-2e1ff37c262e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/allow-deny-list.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/allow-deny-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/allow-deny-list.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 11b9d940-ec54-a065-88ab-c28743c0f8df
---

# Allow or block invitations - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Use an allow list or block list to control which organizations can receive B2B collaboration invitations. For example, to block personal email domains, add domains like Gmail.com and Outlook.com to a block list. To allow invitations only to partner organizations, add domains such as Contoso.com, Fabrikam.com, and Litware.com to an allow list.

This article explains how to configure an allow list or block list for B2B collaboration.

- In the portal by configuring collaboration restrictions in your organization's [External collaboration settings](external-collaboration-settings-configure)

## Important considerations

- You can create either an allow list or a block list. You can't set up both types of lists. By default, whatever domains aren't in the allow list are on the block list, and vice versa.
- You can create only one policy per organization. You can update the policy to include more domains, or you can delete the policy to create a new one.
- The number of domains you can add to an allow list or block list is limited only by the size of the policy. This limit applies to the number of characters, so you can have a greater number of shorter domains or fewer longer domains. The maximum size of the entire policy is 25 KB (25,000 characters), which includes the allow list or block list and any other parameters configured for other features. For example, if your domain entries average 15 characters each, you can add approximately 1,600 domains to the policy.
- This list works independently from OneDrive and SharePoint Online allow/block lists. If you want to restrict individual file sharing in SharePoint Online, you need to set up an allow or block list for OneDrive and SharePoint Online. For more information, see [Restrict sharing of SharePoint and OneDrive content by domain](https://support.office.com/article/restricted-domains-sharing-in-sharepoint-online-and-onedrive-for-business-5d7589cd-0997-4a00-a2ba-2320ec49c4e9).
- The list doesn't apply to external users who already redeemed the invitation. The list will be enforced after the list is set up. If a user invitation is in a pending state, and you set a policy that blocks their domain, the user's attempt to redeem the invitation fails.
- Both allow/block list and cross-tenant access settings are checked at the time of invitation.

## Set the allow or block list policy in the portal

By default, the **Allow invitations to be sent to any domain (most inclusive)** setting is enabled. In this case, you can invite B2B users from any organization.

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

### Add a block list

This is the most common scenario, where your organization wants to work with almost any organization but wants to prevent users from specific domains from being invited as B2B users.

To add a block list:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **Collaboration restrictions**, select **Deny invitations to the specified domains**.
4. Under **Target domains**, enter the name of one of the domains that you want to block. For multiple domains, enter each domain on a new line. For example:

    ![Screenshot showing the option to deny with added domains.](media/allow-deny-list/deny-list-settings.png)
5. When you're done, select **Save**.

After you save the policy, invitations to blocked domains fail and the inviter sees a blocked-domain message.

### Add an allow list

This is a more restrictive configuration. Only domains in the allow list can receive invitations.

If you want to use an allow list, take time to fully evaluate your business needs. If you make this policy too restrictive, users might send documents over email or use other unsanctioned ways to collaborate.

To add an allow list:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **External collaboration settings**.
3. Under **Collaboration restrictions**, select **Allow invitations only to the specified domains (most restrictive)**.
4. Under **Target domains**, enter the name of one of the domains that you want to allow. For multiple domains, enter each domain on a new line. For example:

    ![Screenshot showing the allow option with added domains.](media/allow-deny-list/allow-list-settings.png)
5. When you're done, select **Save**.

After you save the policy, invitations to domains not in the allow list fail, and the inviter sees a blocked-domain message.

### Switch from allow list to block list and vice versa

Switching from one policy to another discards the existing policy configuration. Make sure to back up details of your configuration before you perform the switch.