---
layout: Conceptual
title: Cross-cloud settings - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/cross-cloud-settings
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Enable secure cross-cloud B2B collaboration between organizations in different sovereign (national) Microsoft Azure clouds by configuring Microsoft cloud settings.
ms.topic: how-to
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
ms.collection: M365-identity-device-management
ms.custom: it-pro, seo-july-2024, sfi-image-nochange
locale: en-us
document_id: 23465c7c-cda1-ca2f-e958-cbf835a2ba93
document_version_independent_id: 5f20559a-f258-bedf-786a-5b264bcfd6cf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/cross-cloud-settings.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/cross-cloud-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/cross-cloud-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: e4f67774-494b-5f64-0f55-5b26f640c27f
---

# Cross-cloud settings - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

When Microsoft Entra organizations in separate Microsoft Azure clouds need to collaborate, they can use Microsoft cloud settings to enable Microsoft Entra B2B collaboration with each other. B2B collaboration is available between the following global and sovereign Microsoft Azure clouds:

- Microsoft Azure commercial cloud and Microsoft Azure Government
- Microsoft Azure commercial cloud and Microsoft Azure operated by 21Vianet

Important

Both organizations must enable collaboration with each other, as described in this article. Then each organization can optionally modify their inbound and outbound access settings, as described in [Configure cross-tenant access settings for B2B collaboration](cross-tenant-access-settings-b2b-collaboration).

To enable collaboration between two organizations in different Microsoft clouds, an admin in each organization completes the following steps:

1. Configures their Microsoft cloud settings to enable collaboration with the partner's cloud.
2. Uses the partner's tenant ID to find and add the partner to their organizational settings.
3. Configures their inbound and outbound settings for the partner organization. The admin can either apply the default settings or configure specific settings for the partner.

After each organization completes these steps, Microsoft Entra B2B collaboration between the organizations is enabled.

Note

B2B direct connect is not supported for collaboration with Microsoft Entra tenants in a different Microsoft cloud.

## Before you begin

- **Obtain the partner's tenant ID.** To enable B2B collaboration with a partner's Microsoft Entra organization in another Microsoft Azure cloud, you need the partner's tenant ID. Using an organization's domain name for lookup isn't available in cross-cloud scenarios.
- **Decide on inbound and outbound access settings for the partner.** Selecting a cloud in your Microsoft cloud settings doesn't automatically enable B2B collaboration. Once you enable another Microsoft Azure cloud, all B2B collaboration is blocked by default for organizations in that cloud. You need to add the tenant you want to collaborate with to your Organizational settings. At that point, your default settings go into effect for that tenant only. You can allow the default settings to remain in effect. Or, you can modify the inbound and outbound settings for the organization.
- **Obtain any required object IDs or app IDs.** If you want to apply access settings to specific users, groups, or applications in the partner organization, you need to contact the organization for information before configuring your settings. Obtain their user object IDs, group object IDs, or application IDs (*client app IDs* or *resource app IDs*) so you can target your settings correctly.

Note

Users from another Microsoft cloud must be invited using their user principal name (UPN). [Email as sign-in](../identity/authentication/howto-authentication-use-email-signin#b2b-guest-user-sign-in-with-an-email-address) is not currently supported when collaborating with users from another Microsoft cloud.

## Enable the cloud in your Microsoft cloud settings

In your Microsoft cloud settings, enable the Microsoft Azure cloud you want to collaborate with.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**, then select **Microsoft cloud settings**.
3. Select the checkboxes next to the external Microsoft Azure clouds you want to enable.

    ![Microsoft cloud settings page with external cloud options selected.](media/cross-cloud-settings/cross-cloud-settings.png)

    The **Cross-cloud synchronization settings** checkbox applies to synchronization across clouds. For more information, see [Configure cross-cloud synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure?pivots=cross-cloud-synchronization).

Note

Selecting a cloud doesn't automatically enable B2B collaboration with organizations in that cloud. You'll need to add the organization you want to collaborate with, as described in the next section.

## Add the tenant to your organizational settings

Follow these steps to add the tenant you want to collaborate with to your Organizational settings.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**, then select **Organizational settings**.
3. Select **Add organization**.
4. On the **Add organization** pane, type the tenant ID for the organization (cross-cloud lookup by domain name isn't currently available).

    ![Add organization pane with a cross-cloud tenant ID entered.](media/cross-cloud-settings/cross-tenant-add-organization.png)
5. Select the organization in the search results, and then select **Add**.
6. The organization appears in the **Organizational settings** list. At this point, all access settings for this organization are inherited from your default settings.

    ![Organizational settings list showing an added organization inheriting default access settings.](media/cross-cloud-settings/org-specific-settings-inherited.png)
7. If you want to change the cross-tenant access settings for this organization, select the **Inherited from default** link under the **Inbound access** or **Outbound access** column. Then follow the detailed steps in these sections:

    - [Modify inbound access settings](cross-tenant-access-settings-b2b-collaboration#modify-inbound-access-settings)
    - [Modify outbound access settings](cross-tenant-access-settings-b2b-collaboration#modify-outbound-access-settings)

## Sign-in endpoints

After you enable collaboration with an organization from a different Microsoft cloud, cross-cloud Microsoft Entra guest users can now sign in to your multitenant or Microsoft first-party apps by using a [common endpoint](redemption-experience#redemption-process-and-sign-in-through-a-common-endpoint) (in other words, a general app URL that doesn't include your tenant context). During the sign-in process, the guest user chooses **Sign-in options**, and then selects **Sign in to an organization**. The user then types the name of your organization and continues signing in using their Microsoft Entra credentials.

Cross-cloud Microsoft Entra guest users can also use application endpoints that include your tenant information, for example:

- `https://myapps.microsoft.com/?tenantid=<your tenant ID>`
- `https://myapps.microsoft.com/<your verified domain>.onmicrosoft.com`
- `https://contoso.sharepoint.com/sites/testsite`

You can also give cross-cloud Microsoft Entra guest users a direct link to an application or resource by including your tenant information, for example `https://myapps.microsoft.com/signin/X/<application ID>?tenantId=<your tenant ID>`.

## Supported scenarios with cross-cloud Microsoft Entra guest users

The following scenarios are supported when collaborating with an organization from a different Microsoft cloud:

- Use B2B collaboration to invite a user in the partner tenant to access resources in your organization, including web line-of-business apps, SaaS apps, and SharePoint Online sites, documents, and files.
- Use B2B collaboration to [share Power BI content to a user in the partner tenant](/en-us/fabric/enterprise/powerbi/service-admin-entra-b2b).
- Apply Conditional Access policies to the B2B collaboration user and opt to trust multifactor authentication or device claims (compliant claims and Microsoft Entra hybrid joined claims) from the user’s home tenant.

Note

Enabling the [SharePoint and OneDrive integration with Microsoft Entra B2B](/en-us/sharepoint/sharepoint-azureb2b-integration) will provide the best experience for inviting users from another Microsoft cloud within SharePoint and OneDrive.

## Known behavior with cross-cloud B2B authentication

For cross-cloud B2B guest users, the `login_hint` is populated from the guest object's mail attribute rather than the user's home UPN. This behavior exists because cross-cloud and same-cloud B2B scenarios have different identity boundaries and data availability. In same-cloud B2B scenarios, the service can access the user's home identity information within the same cloud ecosystem and can therefore resolve and use the home sign-in identifier when needed.

In cross-cloud B2B scenarios, however, the resource tenant stores only the guest's immutable home-cloud identifier (PUID) and invited email address. Because the home UPN doesn't persist on the guest object and isn't available when the initial authentication redirect is generated, the `login_hint` is populated from the guest's mail attribute by design. Organizations that require a seamless SSO experience should ensure that the guest user's mail attribute in the resource tenant matches the user's UPN in their home tenant. Because the login\_hint is populated from the guest's mail attribute, any mismatch between the guest mail value and the home tenant UPN can prevent the home tenant from correctly identifying the user for SSO, resulting in additional sign-in prompts, failed account resolution, or a degraded authentication experience.