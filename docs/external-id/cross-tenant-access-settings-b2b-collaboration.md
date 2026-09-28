---
layout: HowTo
title: Cross-tenant access settings - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/cross-tenant-access-settings-b2b-collaboration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to manage cross-tenant access settings for B2B collaboration and direct connect in Microsoft Entra External ID. Control inbound and outbound access, trust MFA, and device claims from other organizations.
ms.date: 2026-04-24T00:00:00.0000000Z
ms.topic: how-to
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom:
- it-pro
- ge-structured-content-pilot
- sfi-image-nochange
locale: en-us
document_id: 2c150664-0126-912e-699b-f97c64ee6b4d
document_version_independent_id: 3a89e05c-e28c-2097-c76d-52d2b9240b2a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/cross-tenant-access-settings-b2b-collaboration.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/cross-tenant-access-settings-b2b-collaboration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/cross-tenant-access-settings-b2b-collaboration.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: ee1383c2-a695-184c-3c08-0f53af0c1dc0
---

# Cross-tenant access settings - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Use External Identities cross-tenant access settings to manage how you collaborate with other Microsoft Entra organizations through B2B collaboration. These settings determine both the level of *inbound* access users in external Microsoft Entra organizations have to your resources, and the level of *outbound* access your users have to external organizations. They also let you trust multifactor authentication (MFA) and device claims ([compliant claims and Microsoft Entra hybrid joined claims](../identity/conditional-access/policy-alt-all-users-compliant-hybrid-or-mfa)) from other Microsoft Entra organizations. For details and planning considerations, see [Cross-tenant access in Microsoft Entra External ID](cross-tenant-access-overview).

**Collaboration across clouds:** Partner organizations in different Microsoft clouds can set up B2B collaboration with each other. First, both organizations must enable collaboration with each other as described in [Configure Microsoft cloud settings](cross-cloud-settings). Then each organization can optionally modify their inbound access settings and outbound access settings, as described below.

Important

Microsoft is beginning to move customers using cross-tenant access settings to a new storage model on August 30, 2023. You may notice an entry in your audit logs informing you that your cross-tenant access settings were updated as our automated task migrates your settings. For a brief window while the migration processes, you will be unable to make changes to your settings. If you are unable to make a change, you should wait a few moments and try the change again. Once the migration completes, [you will no longer be capped with 25kb of storage space](faq#how-many-organizations-can-i-add-in-cross-tenant-access-settings-) and there will be no more limits on the number of partners you can add.

## Prerequisites

Caution

Changing the default inbound or outbound settings to **Block access** could block existing business-critical access to apps in your organization or partner organizations. Be sure to use the tools described in [Cross-tenant access in Microsoft Entra External ID](cross-tenant-access-overview) and consult with your business stakeholders to identify the required access.

- Review the [Important considerations](cross-tenant-access-overview#important-considerations) section in the [cross-tenant access overview](cross-tenant-access-overview) before configuring your cross-tenant access settings.
- Use the tools and follow the recommendations in [Identify inbound and outbound sign-ins](cross-tenant-access-overview#identify-inbound-and-outbound-sign-ins) to understand which external Microsoft Entra organizations and resources users are currently accessing.
- Decide on the default level of access you want to apply to all external Microsoft Entra organizations.
- Identify any Microsoft Entra organizations that need customized settings so you can configure **Organizational settings** for them.
- If you want to apply access settings to specific users, groups, or applications in an external organization, you need to contact the organization for information before configuring your settings. Obtain their user object IDs, group object IDs, or application IDs (*client app IDs* or *resource app IDs*) so you can target your settings correctly.
- If you want to set up B2B collaboration with a partner organization in an external Microsoft Azure cloud, follow the steps in [Configure Microsoft cloud settings](cross-cloud-settings). An admin in the partner organization needs to do the same for your tenant.
- Both allow/block list and cross-tenant access settings are checked at the time of invitation. If a user's domain is on the allowlist, they can be invited, unless the domain is explicitly blocked in the cross-tenant access settings. If a user's domain is on the blocklist, they can't be invited regardless of the cross-tenant access settings. If a user isn't on either list, we check the cross-tenant access settings to determine whether they can be invited.

## Configure default settings

Default cross-tenant access settings apply to all external organizations for which you haven't created organization-specific customized settings. If you want to modify the Microsoft Entra ID-provided default settings, follow these steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**, then select **Cross-tenant access settings**.
3. Select the **Default settings** tab and review the summary page.

    ![Screenshot showing the Cross-tenant access settings Default settings tab.](media/cross-tenant-access-settings-b2b-collaboration/cross-tenant-defaults.png)
4. To change the settings, select the **Edit inbound defaults** link or the **Edit outbound defaults** link.

    ![Screenshot showing edit buttons for Default settings.](media/cross-tenant-access-settings-b2b-collaboration/cross-tenant-defaults-edit.png)
5. Modify the default settings by following the detailed steps in these sections:

    - Modify inbound access settings
    - Modify outbound access settings

## Add an organization

Follow these steps to configure customized settings for specific organizations.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**, then select **Organizational settings**.
3. Select **Add organization**.
4. On the **Add organization** pane, type the full domain name (or tenant ID) for the organization.

    ![Screenshot showing adding an organization.](media/cross-tenant-access-settings-b2b-collaboration/cross-tenant-add-organization.png)
5. Select the organization in the search results, and then select **Add**.
6. The organization appears in the **Organizational settings** list. At this point, all access settings for this organization are inherited from your default settings. To change the settings for this organization, select the **Inherited from default** link under the **Inbound access** or **Outbound access** column.

    ![Screenshot showing an organization added with default settings.](media/cross-tenant-access-settings-b2b-collaboration/org-specific-settings-inherited.png)
7. Modify the organization's settings by following the detailed steps in these sections:

    - Modify inbound access settings
    - Modify outbound access settings

## Modify inbound access settings

With inbound settings, you select which external users and groups are able to access the internal applications you choose. Whether you're configuring default settings or organization-specific settings, the steps for changing inbound cross-tenant access settings are the same. As described in this section, you navigate to either the **Default** tab or an organization on the **Organizational settings** tab, and then make your changes.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**.
3. Navigate to the settings you want to modify:

    - **Default settings**: To modify default inbound settings, select the **Default settings** tab, and then under **Inbound access settings**, select **Edit inbound defaults**.
    - **Organizational settings**: To modify settings for a specific organization, select the **Organizational settings** tab, find the organization in the list (or add one), and then select the link in the **Inbound access** column.
4. Follow the detailed steps for the inbound settings you want to change:

    - To change inbound B2B collaboration settings
    - To change inbound trust settings for accepting MFA and device claims

Note

If you are using the native sharing capabilities in Microsoft SharePoint and [Microsoft OneDrive with Microsoft Entra B2B integration](/en-us/sharepoint/sharepoint-azureb2b-integration) enabled, you must add the external domains to the [external collaboration settings](/en-us/entra/external-id/external-collaboration-settings-configure). Otherwise, invitations from these applications might fail, even if the external tenant has been added in the cross-tenant access settings.

### To change inbound B2B collaboration settings

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**, then select **Organizational settings**
3. Select the link in the **Inbound access** column and the **B2B collaboration** If you block access for all external users and groups, you also need to block access to all your internal applications.
4. If you're configuring inbound access settings for a specific organization, select an option:

    - **Default settings**: Select this option if you want the organization to use the default inbound settings (as configured on the **Default** settings If you block access for all external users and groups, you also need to block access to all your internal applications. If customized settings were already configured for this organization, you need to select **Yes** to confirm that you want all settings to be replaced by the default settings. Then select **Save**, and skip the rest of the steps in this procedure.
    - **Customize settings**: Select this option if you want to customize the settings to enforce for this organization instead of the default settings. Continue with the rest of the steps in this procedure.
5. Select **External users and groups**.
6. Under **Access status**, select one of the following:

    - **Allow access**: Allows the users and groups specified under **Applies to** to be invited for B2B collaboration.
    - **Block access**: Blocks the users and groups specified under **Applies to** from being invited to B2B collaboration.

    ![Screenshot showing selecting the user access status for B2B collaboration.](media/cross-tenant-access-settings-b2b-collaboration/generic-inbound-external-users-groups-access.png)
7. Under **Applies to**, select one of the following:

    - **All external users and groups**: Applies the action you chose under **Access status** to all users and groups from external Microsoft Entra organizations.
    - **Select external users and groups** (requires a Microsoft Entra ID P1 or P2 subscription): Lets you apply the action you chose under **Access status** to specific users and groups within the external organization.

    Note

    If you block access for all external users and groups, you also need to block access to all your internal applications (on the **Applications** tab). If you have configured cross-tenant synchronization, blocking access for all external users and groups can block cross-tenant sync.

    ![Screenshot showing selecting the target users and groups.](media/cross-tenant-access-settings-b2b-collaboration/generic-inbound-external-users-groups-target.png)
8. If you chose **Select external users and groups**, do the following for each user or group you want to add:

    - Select **Add external users and groups**.
    - In the **Add other users and groups** pane, in the search box, type the user object ID or group object ID you obtained from your partner organization.
    - In the menu next to the search box, choose either **user** or **group**.
    - Select **Add**.

    Note

    You can't target users or groups in inbound default settings.

    ![Screenshot showing adding users and groups.](media/cross-tenant-access-settings-b2b-collaboration/generic-inbound-external-users-groups-add-new.png)
9. When you're done adding users and groups, select **Submit**.

    ![Screenshot showing submitting users and groups.](media/cross-tenant-access-settings-b2b-collaboration/generic-inbound-external-users-groups-submit.png)
10. Select the **Applications** tab.
11. Under **Access status**, select one of the following:

    - **Allow access**: Allows the applications specified under **Applies to** to be accessed by B2B collaboration users.
    - **Block access**: Blocks the applications specified under **Applies to** from being accessed by B2B collaboration users.

    ![Screenshot showing applications access status.](media/cross-tenant-access-settings-b2b-collaboration/generic-inbound-applications-access.png)
12. Under **Applies to**, select one of the following:

    - **All applications**: Applies the action you chose under **Access status** to all of your applications.
    - **Select applications** (requires a Microsoft Entra ID P1 or P2 subscription): Lets you apply the action you chose under **Access status** to specific applications in your organization.

    Note

    If you block access to all applications, you also need to block access for all external users and groups (on the **External users and groups** tab).

    ![Screenshot showing target applications.](media/cross-tenant-access-settings-b2b-collaboration/generic-inbound-applications-target.png)
13. If you chose **Select applications**, do the following for each application you want to add:

    - Select **Add Microsoft applications** or **Add other applications**.
    - In the **Select** pane, type the application name or the application ID (either the *client app ID* or the *resource app ID*) in the search box. Then select the application in the search results. Repeat for each application you want to add.
    - When you're done selecting applications, choose **Select**.

    ![Screenshot showing selecting applications.](media/cross-tenant-access-settings-b2b-collaboration/generic-inbound-applications-add.png)
14. Select **Save**.

### Considerations for allowing Microsoft applications

If you want to configure **Cross-tenant access settings** to allow only a designated set of applications, consider adding the Microsoft applications shown in the following table. For example, if you configure an allowlist and only allow SharePoint Online, the user can't access My Apps or register for MFA in the resource tenant. To ensure a smooth end user experience, include the following applications in your inbound and outbound collaboration settings.

| Application | Resource ID | Available in portal | Details |
| --- | --- | --- | --- |
| My Apps | 2793995e-0a7d-40d7-bd35-6968ba142197 | Yes | Default landing page after redeemed invitation. Defines access to `myapplications.microsoft.com`. |
| Microsoft App Access Panel | 0000000c-0000-0000-c000-000000000000 | No | Used in some late-bound calls when loading certain pages within My Sign ins. For example, the Security Info blade or the Organizations switcher. |
| My Profile | 8c59ead7-d703-4a27-9e55-c96a0054c8d2 | Yes | Defines access to `myaccount.microsoft.com` including My Groups and My Access portals. Some tabs within My Profile require the other apps listed here in order to work. |
| My Sign ins | 19db86c3-b2b9-44cc-b339-36da233a3be2 | No | Defines access to `mysignins.microsoft.com` including access to Security Info. Allow this app if you require users to register for and use MFA in the resource tenant (for example, MFA isn't trusted from the home tenant). |

Some of the applications in the previous table don't allow selection from the Microsoft Entra admin center. To allow them, add them with Microsoft Graph API as shown in the following example:

```json
PATCH https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/partners/<insert partner’s tenant id> 
{ 
    "b2bCollaborationInbound": { 
        "applications": { 
            "accessType": "allowed", 
            "targets": [ 
                { 
                    "target": "2793995e-0a7d-40d7-bd35-6968ba142197", 
                    "targetType": "application" 
                }, 
                { 
                    "target": "0000000c-0000-0000-c000-000000000000", 
                    "targetType": "application" 
                }, 
                { 
                    "target": "8c59ead7-d703-4a27-9e55-c96a0054c8d2", 
                    "targetType": "application" 
                }, 
                { 
                    "target": "19db86c3-b2b9-44cc-b339-36da233a3be2", 
                    "targetType": "application" 
                } 
            ] 
        } 
    } 
}
```

Note

Be sure to include any additional applications you want to allow in the PATCH request as this will overwrite any previously configured applications. Applications that are already configured can be retrieved manually from the portal or by running a GET request on the partner policy. For example, `GET https://graph.microsoft.com/v1.0/policies/crossTenantAccessPolicy/partners/<insert partner's tenant id>`

Note

Applications added via Microsoft Graph API that do not map to an application available in the Microsoft Entra admin center will be displayed as the app ID.

You can't add the Microsoft Admin Portals app to the inbound and outbound cross-tenant access settings in the Microsoft Entra admin center. To allow external access to Microsoft admin portals, use the Microsoft Graph API to individually add the following apps that are part of the Microsoft Admin Portals app group:

- Azure portal (c44b4083-3bb0-49c1-b47d-974e53cbdf3c)
- Microsoft Entra admin center (c44b4083-3bb0-49c1-b47d-974e53cbdf3c)
- Microsoft 365 Defender Portal (80ccca67-54bd-44ab-8625-4b79c4dc7775)
- Microsoft Intune Admin Center (80ccca67-54bd-44ab-8625-4b79c4dc7775)
- Microsoft Purview portal (80ccca67-54bd-44ab-8625-4b79c4dc7775)

### Configure redemption order

To customize the order of identity providers that your guest users can use to sign in when they accept your invitation, follow these steps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**.
3. On the **Default settings** tab, under **Inbound access settings**, select **Edit inbound defaults**.
4. On the **B2B collaboration** tab, select the **Redemption order** tab.
5. Move the identity providers up or down to change the order in which your guest users can sign in when they accept your invitation. You can also reset the redemption order to the default settings here.

    [![Screenshot showing the redemption order tab.](media/cross-tenant-access-overview/redemption-order-tab-entra.png)](media/cross-tenant-access-overview/redemption-order-tab-entra.png#lightbox)
6. Select **Save**.

You can also customize the redemption order via the Microsoft Graph API.

1. Open the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Sign in as at least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) to your resource tenant.
3. Run the following query to get the current redemption order:

```http
GET https://graph.microsoft.com/beta/policies/crossTenantAccessPolicy/default
```

1. In this example, we'll move the SAML/WS-Fed IdP federation to the top of the redemption order above Microsoft Entra identity provider. Patch the same URI with this request body:

```http
{
  "invitationRedemptionIdentityProviderConfiguration":
  {
  "primaryIdentityProviderPrecedenceOrder": ["ExternalFederation ","AzureActiveDirectory"],
  "fallbackIdentityProvider": "defaultConfiguredIdp "
  }
}
```

1. To verify the changes run the GET query again.
2. To reset the redemption order to the default settings, run the following query:

```http
    {
    "invitationRedemptionIdentityProviderConfiguration": {
    "primaryIdentityProviderPrecedenceOrder": [
    "azureActiveDirectory",
    "externalFederation",
    "socialIdentityProviders"
    ],
    "fallbackIdentityProvider": "defaultConfiguredIdp"
    }
    }
```

### SAML/WS-Fed federation (Direct federation) for Microsoft Entra ID verified domains

You can now add your enlisted Microsoft Entra ID verified domain to set up the direct federation relationship. First you need to set up the Direct federation configuration in the [admin center](direct-federation) or via the [API](/en-us/graph/api/resources/samlorwsfedexternaldomainfederation). Make sure that the domain isn't verified in the same tenant. Once the configuration is set up, you can customize the redemption order. The SAML/WS-Fed IdP is added to the redemption order as the last entry. You can move it up in the redemption order to set it above Microsoft Entra identity provider.

### Prevent your B2B users from redeeming an invite using Microsoft accounts

To prevent your B2B guest users from redeeming their invite using their existing Microsoft accounts or creating a new one to accept the invitation, follow the steps below.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator)
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**.
3. On the **Default settings** tab, under **Inbound access settings**, select **Edit inbound defaults**.
4. On the **B2B collaboration** tab, select the **Redemption order** tab.
5. Under **Fallback identity providers** disable Microsoft service account (MSA).

    [![Screenshot of the fallback identity providers option.](media/cross-tenant-access-overview/fallback-idp.png)](media/cross-tenant-access-overview/fallback-idp.png#lightbox)
6. Select **Save**.

You need to have at least one fallback identity provider enabled at any given time. If you want to disable Microsoft accounts, you have to enable email one-time passcode. You can't disable both fallback identity providers. Any existing guest users signed in with Microsoft accounts continue using it during subsequent sign-ins. You need to [reset their redemption status](reset-redemption-status) for this setting to apply.

### To change inbound trust settings for MFA and device claims

1. Select the **Trust settings** tab.
2. (This step applies to **Organizational settings** only.) If you're configuring settings for an organization, select one of the following:

    - **Default settings**: The organization uses the settings configured on the **Default** settings tab. If customized settings were already configured for this organization, select **Yes** to confirm that you want all settings to be replaced by the default settings. Then select **Save**, and skip the rest of the steps in this procedure.
    - **Customize settings**: You can customize the settings to enforce for this organization instead of the default settings. Continue with the rest of the steps in this procedure.
3. Select one or more of the following options:

    - **Trust multifactor authentication from Microsoft Entra tenants**: Select this checkbox to allow your Conditional Access policies to trust MFA claims from external organizations. During authentication, Microsoft Entra ID checks a user's credentials for a claim that the user completed MFA. If not, an MFA challenge is initiated in the user's home tenant. This setting isn't applied if an external user signs in using [granular delegated admin privileges (GDAP)](/en-us/partner-center/customers/gdap-introduction), such as used by a technician at a Cloud Service Provider that administers services in your tenant. When an external user signs in using GDAP, MFA is always required in the user's home tenant, and always trusted in the resource tenant. MFA registration of a GDAP user isn't supported outside of the user's home tenant. If your organization has a requirement to disallow access to service provider technicians based on MFA in the user's home tenant, you can remove the GDAP relationship in [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home#/partners).
    - **Trust compliant devices**: Allows your Conditional Access policies to trust [compliant device claims](../identity/conditional-access/policy-all-users-device-compliance) from an external organization when their users access your resources.
    - **Trust Microsoft Entra hybrid joined devices**: Allows your Conditional Access policies to trust Microsoft Entra hybrid joined device claims from an external organization when their users access your resources.

    ![Screenshot showing trust settings.](media/cross-tenant-access-settings-b2b-collaboration/inbound-trust-settings.png)
4. (This step applies to **Organizational settings** only.) Review the **Automatic redemption** option:

    - **Automatically redeem invitations with the tenant** &lt;tenant&gt;: Check this setting if you want to automatically redeem invitations. If so, users from the specified tenant won't have to accept the consent prompt the first time they access this tenant using cross-tenant synchronization, B2B collaboration, or B2B direct connect. This setting only suppresses the consent prompt if the specified tenant also checks this setting for outbound access.

    ![Screenshot that shows the inbound Automatic redemption check box.](../media/external-identities/inbound-consent-prompt-setting.png)
5. Select **Save**.

### Allow users to sync into this tenant

If you select **Inbound access** of the added organization, you see the **Cross-tenant sync** tab and the **Allow users sync into this tenant** check box. Cross-tenant synchronization is a one-way synchronization service in Microsoft Entra ID that automates creating, updating, and deleting B2B collaboration users across tenants in an organization. For more information, see [Configure cross-tenant synchronization](../identity/multi-tenant-organizations/cross-tenant-synchronization-configure) and the [Multitenant organizations documentation](../identity/multi-tenant-organizations/).

[![Screenshot that shows the Cross-tenant sync tab with the Allow users sync into this tenant check box.](media/cross-tenant-access-settings-b2b-collaboration/cross-tenant-sync-tab.png)](media/cross-tenant-access-settings-b2b-collaboration/cross-tenant-sync-tab.png#lightbox)

## Modify outbound access settings

With outbound settings, you select which of your users and groups are able to access the external applications you choose. Whether you're configuring default settings or organization-specific settings, the steps for changing outbound cross-tenant access settings are the same. As described in this section, you navigate to either the **Default** tab or an organization on the **Organizational settings** tab, and then make your changes.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**.
3. Navigate to the settings you want to modify:

    - To modify default outbound settings, select the **Default settings** tab, and then under **Outbound access settings**, select **Edit outbound defaults**.
    - To modify settings for a specific organization, select the **Organizational settings** tab, find the organization in the list (or add one) and then select the link in the **Outbound access** column.
4. Select the **B2B collaboration** tab.
5. (This step applies to **Organizational settings** only.) If you're configuring settings for an organization, select an option:

    - **Default settings**: The organization uses the settings configured on the **Default** settings tab. If customized settings were already configured for this organization, you need to select **Yes** to confirm that you want all settings to be replaced by the default settings. Then select **Save**, and skip the rest of the steps in this procedure.
    - **Customize settings**: You can customize the settings to enforce for this organization instead of the default settings. Continue with the rest of the steps in this procedure.
6. Select **Users and groups**.
7. Under **Access status**, select one of the following:

    - **Allow access**: Allows your users and groups specified under **Applies to** to be invited to external organizations for B2B collaboration.
    - **Block access**: Blocks your users and groups specified under **Applies to** from being invited to B2B collaboration. If you block access for all users and groups, this also blocks all external applications from being accessed via B2B collaboration.

    ![Screenshot showing users and groups access status for b2b collaboration.](media/cross-tenant-access-settings-b2b-collaboration/generic-outbound-external-users-groups-access.png)
8. Under **Applies to**, select one of the following:

    - **All &lt;your organization&gt; users**: Applies the action you chose under **Access status** to all your users and groups.
    - **Select &lt;your organization&gt; users and groups** (requires a Microsoft Entra ID P1 or P2 subscription): Lets you apply the action you chose under **Access status** to specific users and groups.

    Note

    If you block access for all of your users and groups, you also need to block access to all external applications (on the **External applications** tab).

    ![Screenshot showing selecting the target users for b2b collaboration.](media/cross-tenant-access-settings-b2b-collaboration/generic-outbound-external-users-groups-target.png)
9. If you chose **Select &lt;your organization&gt; users and groups**, do the following for each user or group you want to add:

    - Select **Add &lt;your organization&gt; users and groups**.
    - In the **Select** pane, type the user name or group name in the search box.
    - Select the user or group in the search results.
    - When you're done selecting the users and groups you want to add, choose **Select**.

    Note

    When targeting your users and groups, you won't be able to select users who have configured [SMS-based authentication](../identity/authentication/howto-authentication-sms-signin). This is because users who have a "federated credential" on their user object are blocked to prevent external users from being added to outbound access settings. As a workaround, you can use the [Microsoft Graph API](/en-us/graph/api/resources/crosstenantaccesspolicy-overview) to add the user's object ID directly or target a group the user belongs to.
10. Select the **External applications** tab.
11. Under **Access status**, select one of the following:

    - **Allow access**: Allows the external applications specified under **Applies to** to be accessed by your users via B2B collaboration.
    - **Block access**: Blocks the external applications specified under **Applies to** from being accessed by your users via B2B collaboration.

    ![Screenshot showing applications access status for b2b collaboration.](media/cross-tenant-access-settings-b2b-collaboration/generic-outbound-applications-access.png)
12. Under **Applies to**, select one of the following:

    - **All external applications**: Applies the action you chose under **Access status** to all external applications.
    - **Select external applications**: Applies the action you chose under **Access status** to all external applications.

    Note

    If you block access to all external applications, you also need to block access for all of your users and groups (on the **Users and groups** tab).

    ![Screenshot showing application targets for b2b collaboration.](media/cross-tenant-access-settings-b2b-collaboration/generic-outbound-applications-target.png)
13. If you chose **Select external applications**, do the following for each application you want to add:

    - Select **Add Microsoft applications** or **Add other applications**.
    - In the search box, type the application name or the application ID (either the *client app ID* or the *resource app ID*). Then select the application in the search results. Repeat for each application you want to add.
    - When you're done selecting applications, choose **Select**.

    ![Screenshot showing selecting applications for b2b collaboration.](media/cross-tenant-access-settings-b2b-collaboration/outbound-b2b-collaboration-add-apps.png)
14. Select **Save**.

### To change outbound trust settings

(This section applies to **Organizational settings** only.)

1. Select the **Trust settings** tab.
2. Review the **Automatic redemption** option:

    - **Automatically redeem invitations with the tenant** &lt;tenant&gt;: Check this setting if you want to automatically redeem invitations. If so, users from this tenant don't have to accept the consent prompt the first time they access the specified tenant using cross-tenant synchronization, B2B collaboration, or B2B direct connect. This setting only suppresses the consent prompt if the specified tenant also checks this setting for inbound access.

        ![Screenshot that shows the outbound Automatic redemption check box.](../media/external-identities/outbound-consent-prompt-setting.png)
3. Select **Save**.

## Remove an organization

When you remove an organization from your Organizational settings, the default cross-tenant access settings go into effect for that organization.

Note

If the organization is a cloud service provider for your organization (the isServiceProvider property in the Microsoft Graph [partner-specific configuration](/en-us/graph/api/resources/crosstenantaccesspolicyconfigurationpartner) is true), you won't be able to remove the organization.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**.
3. Select the **Organizational settings** tab.
4. Find the organization in the list, and then select the trash can icon on that row.