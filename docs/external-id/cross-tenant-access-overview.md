---
layout: Conceptual
title: Cross-tenant access overview - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/cross-tenant-access-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to manage cross-tenant access in Microsoft Entra External ID. Configure B2B collaboration and direct connect settings to control access and trust for external organizations.
ms.topic: overview
ms.date: 2025-03-28T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: b6138502-6a71-9671-fd88-312884ffb14c
document_version_independent_id: 1f3137c1-8ab1-e493-4dbe-49562aebe5dc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/cross-tenant-access-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/cross-tenant-access-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/cross-tenant-access-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 9fe7fa95-ccad-95de-76d9-6f1632e762c6
---

# Cross-tenant access overview - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra organizations can use External ID cross-tenant access settings to manage collaboration with other Microsoft Entra organizations and Microsoft Azure clouds through B2B collaboration and [B2B direct connect](cross-tenant-access-settings-b2b-direct-connect). The [cross-tenant access settings](cross-tenant-access-settings-b2b-collaboration) provide granular control over inbound and outbound access, allowing you to trust multifactor authentication (MFA) and device claims from other organizations.

This article covers cross-tenant access settings for managing B2B collaboration and B2B direct connect with external Microsoft Entra organizations, including across Microsoft clouds. Other settings are available for B2B collaboration with non-Microsoft Microsoft Entra identities (for example, social identities or non-IT managed external accounts). These [external collaboration settings](external-collaboration-settings-configure) include options for restricting guest user access, specifying who can invite guests, and allowing or blocking domains.

There are no limits to the number of organizations you can add in cross-tenant access settings.

## Manage external access with inbound and outbound settings

The external identities cross-tenant access settings manage how you collaborate with other Microsoft Entra organizations. These settings determine both the level of inbound access users in external Microsoft Entra organizations have to your resources, and the level of outbound access your users have to external organizations.

The following diagram shows the cross-tenant access inbound and outbound settings. The **Resource Microsoft Entra tenant** is the tenant containing the resources to be shared. For B2B collaboration, the resource tenant is the inviting tenant (for example, your corporate tenant, where you want to invite the external users). The **User's home Microsoft Entra tenant** is the tenant where the external users are managed.

![Screenshot of a diagram showing cross-tenant access settings for inbound and outbound collaboration.](media/cross-tenant-access-overview/cross-tenant-access-settings-overview.png)

By default, B2B collaboration with other Microsoft Entra organizations is enabled, and B2B direct connect is blocked. But the following comprehensive admin settings let you manage both of these features.

- **Outbound access settings** control whether your users can access resources in an external organization. You can apply these settings to everyone, or specify individual users, groups, and applications.
- **Inbound access settings** control whether users from external Microsoft Entra organizations can access resources in your organization. You can apply these settings to everyone, or specify individual users, groups, and applications.
- **Trust settings** (inbound) determine whether your Conditional Access policies trust the multifactor authentication (MFA), compliant device, and [Microsoft Entra hybrid joined device](../identity/devices/concept-hybrid-join) claims from an external organization if their users already satisfied these requirements in their home tenants. For example, when you configure your trust settings to trust MFA, your MFA policies are still applied to external users, but users who already completed MFA in their home tenants don't have to complete MFA again in your tenant.

## Default settings

The default cross-tenant access settings apply to all Microsoft Entra organizations external to your tenant, except organizations for which you configure custom settings. You can change your default settings, but the initial default settings for B2B collaboration and B2B direct connect are as follows:

- **B2B collaboration**: All your internal users are enabled for B2B collaboration by default. This setting means your users can invite external guests to access your resources and they can be invited to external organizations as guests. MFA and device claims from other Microsoft Entra organizations aren't trusted.
- **B2B direct connect**: No B2B direct connect trust relationships are established by default. Microsoft Entra ID blocks all inbound and outbound B2B direct connect capabilities for all external Microsoft Entra tenants.
- **Organizational settings**: No organizations are added to your Organizational settings by default. Therefore, all external Microsoft Entra organizations are enabled for B2B collaboration with your organization.
- **Cross-tenant sync**: No users from other tenants are synchronized into your tenant with cross-tenant synchronization.

These default settings apply to B2B collaboration with other Microsoft Entra tenants in your same Microsoft Azure cloud. In cross-cloud scenarios, default settings work a little differently. See Microsoft cloud settings later in this article.

## Organizational settings

You can configure organization-specific settings by adding an organization and modifying the inbound and outbound settings for that organization. Organizational settings take precedence over default settings.

- **B2B collaboration**: Use cross-tenant access settings to manage inbound and outbound B2B collaboration and scope access to specific users, groups, and applications. You can set a default configuration that applies to all external organizations, and then create individual, organization-specific settings as needed. Using cross-tenant access settings, you can also trust multifactor (MFA) and device claims (compliant claims and Microsoft Entra hybrid joined claims) from other Microsoft Entra organizations.

    Tip

    Consider excluding external users from the [Microsoft Entra ID Protection MFA registration policy](../id-protection/howto-identity-protection-configure-mfa-policy), if you're going to [trust MFA for external users](authentication-conditional-access#mfa-for-azure-ad-external-users). When both policies are present, external users aren't able to satisfy the requirements for access.
- **B2B direct connect**: For B2B direct connect, use organizational settings to set up a mutual trust relationship with another Microsoft Entra organization. Both your organization and the external organization need to mutually enable B2B direct connect by configuring inbound and outbound cross-tenant access settings.
- You can use **External collaboration settings** to limit who can invite external users, allow or block B2B specific domains, and set restrictions on guest user access to your directory.

### Automatic redemption setting

The automatic redemption setting is an inbound and outbound organizational trust setting to automatically redeem invitations. With this setting, users don't have to accept the consent prompt the first time they access the resource or target tenant. This setting is a checkbox with the name **Automatically redeem invitations with the tenant***tenant name*.

[![Screenshot that shows the checkbox for inbound automatic redemption.](../media/external-identities/inbound-consent-prompt-setting.png)](../media/external-identities/inbound-consent-prompt-setting.png#lightbox)

### How does the setting work in various scenarios?

The automatic redemption setting applies to cross-tenant synchronization, B2B collaboration, and B2B direct connect in the following situations:

- When users are created in a target tenant through cross-tenant synchronization.
- When users are added to a resource tenant through B2B collaboration.
- When users access resources in a resource tenant by using B2B direct connect.

The following table shows how this setting works when you enable it for these scenarios.

| Item | Cross-tenant synchronization | B2B collaboration | B2B direct connect |
| --- | --- | --- | --- |
| Automatic redemption setting | Required | Optional | Optional |
| Users receive a [B2B collaboration invitation email](invitation-email-elements) | No | No | Not applicable |
| Users must accept a [consent prompt](redemption-experience#consent-experience-for-the-guest) | No | No | No |
| Users receive a [B2B collaboration notification email](redemption-experience#automatic-redemption-process-setting) | No | Yes | Not applicable |

This setting doesn't affect application consent experiences. For more information, see [Consent experience for applications in Microsoft Entra ID](../identity-platform/application-consent-experience).

This setting is supported for organizations across different Microsoft cloud environments, such as Azure commercial and Azure Government. For more information, see [Configure cross-tenant synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure?pivots=cross-cloud-synchronization).

### When is the consent prompt suppressed?

The automatic redemption setting suppresses the consent prompt and invitation email only if you select this setting for both the home/source tenant (outbound) and resource/target tenant (inbound).

![Diagram that shows the automatic redemption setting for both outbound and inbound.](../media/automatic-redemption-include/automatic-redemption-setting.png)

The following table shows the consent prompt behavior for source tenant users when the automatic redemption setting is selected for various combinations of cross-tenant access settings.

| Home/source tenant | Resource/target tenant | Consent prompt behaviorfor source tenant users |
| --- | --- | --- |
| **Outbound** | **Inbound** |  |
| ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | Suppressed |
| ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | Not suppressed |
| ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | Not suppressed |
| ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | Not suppressed |
| **Inbound** | **Outbound** |  |
| ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | Not suppressed |
| ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | Not suppressed |
| ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | ![Icon for check mark.](../media/automatic-redemption-include/icon-check-mark.png) | Not suppressed |
| ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | ![Icon for clear check mark.](../media/automatic-redemption-include/icon-check-mark-clear.png) | Not suppressed |

To configure this setting using Microsoft Graph, see the [Update crossTenantAccessPolicyConfigurationPartner](/en-us/graph/api/crosstenantaccesspolicyconfigurationpartner-update) API. For information about building your own onboarding experience, see [B2B collaboration invitation manager](external-identities-overview#azure-ad-microsoft-graph-api-for-b2b-collaboration).

For more information, see [Configure cross-tenant synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure), [Configure cross-tenant access settings for B2B collaboration](cross-tenant-access-settings-b2b-collaboration), and [Configure cross-tenant access settings for B2B direct connect](cross-tenant-access-settings-b2b-direct-connect).

### Configurable redemption

With configurable redemption, you can customize the order of identity providers that your guest users can sign in with when they accept your invitation. You can enable the feature and specify the redemption order under the **Redemption order** tab.

[![Screenshot of the Redemption order tab.](media/cross-tenant-access-overview/redemption-order-tab-entra.png)](media/cross-tenant-access-overview/redemption-order-tab-entra.png#lightbox)

When a guest user selects the **Accept invitation** link in an invitation email, Microsoft Entra ID automatically redeems the invitation based on the [default redemption order](redemption-experience#invitation-redemption-flow). When you change the identity provider order under the new Redemption order tab, the new order overrides the default redemption order.

You find both primary identity providers and fallback identity providers under the **Redemption order** tab.

Primary identity providers are the ones that have federations with other sources of authentication. Fallback identity providers are the ones that are used, when a user doesn't match a primary identity provider.

Fallback identity providers can be either Microsoft account (MSA), email one-time passcode, or both. You can't disable both fallback identity providers, but you can disable all primary identity providers and only use fallback identity providers for redemption options.

When using this feature, consider the following known limitations:

- If a Microsoft Entra ID user who has an existing single sign-on (SSO) session is authenticating using email one-time passcode (OTP), they need to choose **Use another account** and reenter their username to trigger the OTP flow. Otherwise the user gets an error indicating their account doesn’t exist in the resource tenant.
- When a user has the same email in both their Microsoft Entra ID and Microsoft accounts, they're prompted to choose between using their Microsoft Entra ID or their Microsoft account even after the admin disables the Microsoft account as a redemption method. Choosing Microsoft account as a redemption option is allowed, even if the method is disabled.

### Direct federation for Microsoft Entra ID verified domains

SAML/WS-Fed identity provider federation (Direct federation) is now supported for Microsoft Entra ID verified domains. This feature allows you to set up a Direct federation with an external identity provider for a domain that is verified in another Microsoft Entra tenant

Note

Ensure that the domain isn't verified in the same tenant in which you're trying to set up the Direct federation configuration. Once you've set up a Direct federation, you can configure the tenant’s redemption preference and move SAML/WS-Fed identity provider over Microsoft Entra ID through the new configurable redemption cross-tenant access settings.

When the guest user redeems the invite, they see a traditional consent screen and are redirected to the My Apps page. In the resource tenant, the profile for this direct federation user shows that the invite is successfully redeemed, with external federation listed as the issuer.

[![Screenshot of the direct federation provider under user identities.](media/cross-tenant-access-overview/external-federation-provider.png)](media/cross-tenant-access-overview/external-federation-provider.png#lightbox)

### Prevent your B2B users from redeeming an invite using Microsoft accounts

You can now prevent your B2B guest users from using Microsoft accounts to redeem invitations. Instead, they use a one-time passcode sent to their email as the fallback identity provider. They're not allowed to use an existing Microsoft account to redeem invitations, nor are they prompted to create a new one. You can enable this feature in your redemption order settings by turning off Microsoft accounts in the fallback identity provider options.

[![Screenshot of the fallback identity providers option.](media/cross-tenant-access-overview/fallback-idp.png)](media/cross-tenant-access-overview/fallback-idp.png#lightbox)

You must always have at least one fallback identity provider active. So, if you decide to disable Microsoft accounts, you need to enable the email one-time passcode option. Existing guest users who already sign in with Microsoft accounts continue to do so for future sign-ins. To apply the new settings to them, you need to [reset their redemption status](reset-redemption-status).

### Cross-tenant synchronization settings

The cross-tenant synchronization settings are inbound-only organizational settings to allow the administrator of a source tenant to synchronize users and groups into a target tenant. These settings are checkboxes with the names **Allow user synchronization into this tenant** and **Allow group synchronization into this tenant** that are specified in the target tenant. These settings don't affect B2B invitations created through other processes such as [manual invitation](add-users-administrator) or [Microsoft Entra entitlement management](../id-governance/entitlement-management-external-users).

[![Screenshot that shows the tab for cross-tenant synchronization with the checkboxes for synchronizing users and groups into a target tenant.](../media/external-identities/access-settings-users-sync.png)](../media/external-identities/access-settings-users-sync.png#lightbox)

To configure these settings using Microsoft Graph, see the [Update crossTenantIdentitySyncPolicyPartner](/en-us/graph/api/crosstenantidentitysyncpolicypartner-update) API. For more information, see [Configure cross-tenant synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure).

## Tenant restrictions

With **Tenant Restrictions** settings, you can control the types of external accounts your users can use on the devices you manage, including:

- Accounts your users created in unknown tenants.
- Accounts that external organizations gave to your users so they can access that organization's resources.

Configure your tenant restrictions to disallow these types of external accounts and use B2B collaboration instead. B2B collaboration gives you the ability to:

- Use Conditional Access and force multifactor authentication for B2B collaboration users.
- Manage inbound and outbound access.
- Terminate sessions and credentials when a B2B collaboration user's employment status changes or their credentials are breached.
- Use sign-in logs to view details about the B2B collaboration user.

Tenant restrictions are independent of other cross-tenant access settings, so any inbound, outbound, or trust settings you configure don't affect tenant restrictions. For details about configuring tenant restrictions, see [Set up tenant restrictions V2](tenant-restrictions-v2).

## Microsoft cloud settings

Microsoft cloud settings let you collaborate with organizations from different Microsoft Azure clouds. With Microsoft cloud settings, you can establish mutual B2B collaboration between the following clouds:

- Microsoft Azure commercial cloud and Microsoft Azure Government, which includes the Office GCC-High and DoD clouds
- Microsoft Azure commercial cloud and Microsoft Azure operated by 21Vianet (operated by 21Vianet)

Note

B2B direct connect isn't supported for collaboration with Microsoft Entra tenants in a different Microsoft cloud.

For more information, see the [Configure Microsoft cloud settings for B2B collaboration](cross-cloud-settings) article.

[Cross-cloud synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-overview) settings allows you to manage the lifecycle of users across tenants in your organization from different Microsoft clouds. After you enable cross-tenant synchronization settings, you can start synchronizing user data from that cloud.

## Important considerations

Important

Changing the default inbound or outbound settings to block access could block existing business-critical access to apps in your organization or partner organizations. Be sure to use the tools described in this article and consult with your business stakeholders to identify the required access.

- To configure cross-tenant access settings in the Azure portal, you need an account with at least [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator), or a custom role.
- To configure trust settings or apply access settings to specific users, groups, or applications, you need a Microsoft Entra ID P1 license. The license is required on the tenant that you configure. For B2B direct connect, where mutual trust relationship with another Microsoft Entra organization is required, you need a Microsoft Entra ID P1 license in both tenants.
- Cross-tenant access settings are used to manage B2B collaboration and B2B direct connect with other Microsoft Entra organizations. For B2B collaboration with non-Microsoft Microsoft Entra identities (for example, social identities or non-IT managed external accounts), use [external collaboration settings](external-collaboration-settings-configure). External collaboration settings include B2B collaboration options for restricting guest user access, specifying who can invite guests, and allowing or blocking domains.
- To apply access settings to specific users, groups, or applications in an external organization, you need to contact the organization for information before configuring your settings. Obtain their user object IDs, group object IDs, or application IDs (*client app IDs* or *resource app IDs*) so you can target your settings correctly.

    Tip

    You might be able to find the application IDs for apps in external organizations by checking your sign-in logs. See the Identify inbound and outbound sign-ins section.
- The access settings you configure for users and groups must match the access settings for applications. Conflicting settings aren't allowed, and warning messages appear if you try to configure them.

    - **Example 1**: If you block inbound access for all external users and groups, access to all your applications must also be blocked.
    - **Example 2**: If you allow outbound access for all your users (or specific users or groups), you're prevented from blocking all access to external applications; access to at least one application must be allowed.
- If you want to allow B2B direct connect with an external organization and your Conditional Access policies require MFA, you must configure your trust settings to accept MFA claims from the external organization.
- If you block access to all apps by default, users are unable to read emails encrypted with Microsoft Rights Management Service, also known as Office 365 Message Encryption (OME). To avoid this issue, configure your outbound settings to allow your users to access this app ID: 00000012-0000-0000-c000-000000000000. If you allow only this application, access to all other apps is blocked by default.
- Conditional Access policies that require MFA or Terms of Use (ToU) can prevent users from completing MFA registration or ToU consent. To avoid this issue, configure outbound settings (home tenant) and inbound settings (resource tenant) to let users access app ID 0000000c-0000-0000-c000-000000000000 (Microsoft App Access Panel) for MFA registration and app ID d52792f4-ba38-424d-8140-ada5b883f293 (Microsoft Entra Terms of Use) for ToU. The configuration of the outbound settings can be achieved via the Microsoft Entra admin center by selecting 'Add other applications' and providing the app ID. Due to a current user interface (UI) limitation, the configuration of the inbound settings must be performed via [Microsoft Graph APIs](/en-us/graph/api/resources/crosstenantaccesspolicy-overview).

## Custom roles for managing cross-tenant access settings

You can create custom roles to manage cross-tenant access settings. Learn more about the recommended custom roles [here](reference-cross-tenant-custom-roles).

## Protect cross-tenant access administrative actions

Any actions that modify cross-tenant access settings are considered protected actions and can be additionally protected with Conditional Access policies. For more information about configuration steps, see [protected actions](../identity/role-based-access-control/protected-actions-overview).

## Identify inbound and outbound sign-ins

Several tools are available to help you identify the access your users and partners need before you set inbound and outbound access settings. To ensure you don’t remove access that your users and partners need, you should examine current sign-in behavior. Taking this preliminary step helps prevent loss of desired access for your end users and partner users. However, in some cases these logs are only retained for 30 days, so we strongly recommend you speak with your business stakeholders to ensure required access isn't lost.

| Tool | Method |
| --- | --- |
| PowerShell script for cross-tenant sign-in activity | To review user sign-in activity associated with external organizations, use the [cross-tenant user sign-in activity](https://www.powershellgallery.com/packages/MSIdentityTools/2.0.1/Content/Get-MSIDCrossTenantAccessActivity.ps1) PowerShell script from the [MSIdentityTools](https://www.powershellgallery.com/packages/MSIdentityTools). |
| PowerShell script for sign-in logs | To determine your users' access to external Microsoft Entra organizations, use the [Get-MgAuditLogSignIn](/en-us/powershell/module/microsoft.graph.reports/get-mgauditlogsignin) cmdlet. |
| Azure Monitor | If your organization subscribes to the Azure Monitor service, use the [Cross-tenant access activity workbook](../identity/monitoring-health/workbook-cross-tenant-access-activity). |
| Security Information and Event Management (SIEM) systems | If your organization exports sign-in logs to a Security Information and Event Management (SIEM) system, you can retrieve the required information from your SIEM system. |

## Identify changes to cross-tenant access settings

The Microsoft Entra audit logs capture all activity around cross-tenant access setting changes and activity. To audit changes to your cross-tenant access settings, use the **category** of ***CrossTenantAccessSettings*** to filter all activity to show changes to cross-tenant access settings.

[![Screenshot of the audit logs for cross-tenant access settings.](media/cross-tenant-access-overview/cross-tenant-access-settings-audit-logs.png)](media/cross-tenant-access-overview/cross-tenant-access-settings-audit-logs.png#lightbox)