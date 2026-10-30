---
layout: Conceptual
title: Known issues for provisioning in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/known-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn about known issues when you work with automated application provisioning or cross-tenant synchronization in Microsoft Entra ID.
ms.topic: troubleshooting
ms.date: 2026-03-31T00:00:00.0000000Z
ms.reviewer: arvinh
zone_pivot_groups: app-provisioning-cross-tenant-synchronization
locale: en-us
document_id: a2382361-1699-3beb-574e-0879c87f7442
document_version_independent_id: 97f40a33-983d-f927-beb5-cb03aa3f82dd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/known-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/known-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/known-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
platformId: 3f175e5e-1b46-6bef-4584-7a77806abf2a
---

# Known issues for provisioning in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article discusses known issues to be aware of when you work with app provisioning or cross-tenant synchronization. To provide feedback about the application provisioning service on UserVoice, see [Microsoft Entra application provision UserVoice](https://aka.ms/appprovisioningfeaturerequest). We watch UserVoice closely so that we can improve the service.

Note

This article isn't a comprehensive list of known issues. If you know of an issue that isn't listed, provide feedback at the bottom of the page.

::: zone pivot="cross-tenant-synchronization"

## Cross-tenant synchronization

### Unsupported synchronization scenarios

- Synchronizing groups, devices, and contacts into another tenant
- Synchronizing photos across tenants
- Synchronizing contacts and converting contacts to B2B users
- Synchronizing meeting rooms across tenants

### Updating exchange attributes such as proxyAddresses and HiddenFromAddressListEnabled

Cross-tenant synchronization can manage user properties in Entra. It does not directly manage exchange attributes. For example:

- ProxyAddresses is a [read-only property in Microsoft Graph](https://go.microsoft.com/fwlink/?linkid=2272551). It can be included as a source attribute in your mappings, but cannot be set as a target attribute.
- Cross-tenant synchronization can update the ShowInAddressList attribute in Entra, but it cannot directly update HiddenFromAddressListEnabled in Exchange.
- TargetAddress, which maps to the ExternalEmailAddress property in Microsoft Exchange Online, isn't available as an attribute you can choose. If you need to change this attribute, you have to do it manually over the required object.

### SMS sign-in enabled users are skipped

An external user from the source (home) tenant can't be provisioned into another tenant. Internal guest users from the source tenant can't be provisioned into another tenant. Only internal member users from the source tenant can be provisioned into the target tenant. For more information, see [Properties of a Microsoft Entra B2B collaboration user](../../external-id/user-properties).

In addition, users that are enabled for SMS sign-in cannot be synchronized through cross-tenant synchronization.

### Updating the showInAddressList property fails

For existing B2B collaboration users, the showInAddressList attribute is updated as long as the B2B collaboration user doesn't have a mailbox enabled in the target tenant. If the mailbox is enabled in the target tenant, use the [Set-MailUser](/en-us/powershell/module/exchange/set-mailuser) PowerShell cmdlet to set the HiddenFromAddressListsEnabled property to a value of $false.

`Set-MailUser [GuestUserUPN] -HiddenFromAddressListsEnabled:$false`

Where [GuestUserUPN] is the calculated UserPrincipalName. Example:

`Set-MailUser guestuser1_contoso.com#EXT#@fabrikam.onmicrosoft.com -HiddenFromAddressListsEnabled:$false`

For more information, see [About the Exchange Online PowerShell module](/en-us/powershell/exchange/exchange-online-powershell-v2).

### Mail attribute is not updated

If the user in the target tenant is assigned an exchange license, cross-tenant synchronization will not be able to update the mail attribute. To work around this, remove the exchange license for the user, update the mail attribute, and assign the license to the user again.

### Configuring synchronization from target tenant

Configuring synchronization from the target tenant isn't supported. All configurations must be done in the source tenant. The target administrator is able to turn off cross-tenant synchronization at any time.

### Two users in the source tenant matched with the same user in the target tenant

When two users in the source tenant have the same mail, and they both need to be created in the target tenant, one user is created in the target and linked to the two users in the source. Ensure that the mail attribute is not shared among users in the source tenant. In addition, please ensure that the mail of the user in the source tenant is from a verified domain. The external user will not be created successfully if the mail is from an unverified domain.

### Usage of Microsoft Entra B2B collaboration for cross-tenant access

- B2B users are unable to manage certain Microsoft 365 services in remote tenants (such as Exchange Online), as there's no directory picker.
- To learn about Azure Virtual Desktop support for B2B users, see [Prerequisites for Azure Virtual Desktop](/en-us/azure/virtual-desktop/prerequisites?tabs=portal).
- For the latest status on Power BI support for external member users, see [Distribute Power BI content to external guest users with Microsoft Entra B2B](/en-us/fabric/enterprise/powerbi/service-admin-entra-b2b)

::: zone-end

## Authorization

#### Unable to change provisioning mode back to manual

On configuring provisioning for the first time, you'll notice that the provisioning mode has switched from manual to automatic. You can't change it back to manual. But you can turn off provisioning through the UI. Turning off provisioning in the UI effectively does the same as setting the dropdown to manual.

## Attribute mappings

#### Attribute SamAccountName or userType not available as a source attribute

The attributes **SamAccountName** and **userType** aren't available as source attributes. You can instead use a directory extension attribute as a workaround. To learn more, see [Missing source attribute](user-provisioning-sync-attributes-for-mapping).

#### Source attribute dropdown missing for schema extension

Extensions to your schema can sometimes be missing from the source attribute dropdown in the UI. Go into the advanced settings of your attribute mappings and manually add the attributes. To learn more, see [Customize attribute mappings](customize-application-attributes).

#### Null attribute can't be provisioned

Microsoft Entra ID currently can't provision null attributes. If an attribute is null on the user object, it is skipped.

#### Special characters are not supported on joining properties

Microsoft Entra ID currently can't perform filter queries on values containing special characters. Therefore a provisioning attempt on a resource (user or group) with a special character on filter attributes fails. An example is, a group with a special character on the name can be created on Microsoft Entra ID but can't be synced to a target system.

#### Maximum characters for attribute-mapping expressions

Attribute-mapping expressions can have a maximum of 10,000 characters.

#### Unsupported scoping filters

The **appRoleAssignments**, **userType**, **manager**, and **date-type** attributes (for example, StatusHireDate, startDate, endDate, StatusTerminationDate, accountExpires) aren't supported as scoping filters.

::: zone pivot="cross-tenant-synchronization"

#### OtherMails should not be included in your attribute mappings as a target attribute

The otherMails property is automatically computed in the target tenant. Changes to the user object made directly in the target tenant could result in the otherMails property being updated and override the value set by cross-tenant synchronization. As a result, otherMails should not be included in your cross-tenant synchronization attribute mappings as a target attribute.

::: zone-end

#### Multivalue directory extensions

Multivalue directory extensions can't be used in attribute mappings or scoping filters.

#### SCIM multi-valued addresses, emails and phone numbers

SCIM multi-valued attributes in `addresses`, `emails` and `phoneNumbers` are currently processed only for supported `type` values. Attribute mappings that reference `addresses[type eq "home"]`, `addresses[type eq "any-other-value"]`, `emails[type eq "home"]` or `phoneNumbers[type eq "home"]` aren't processed. Only `addresses[type eq "work"]`, `emails[type eq "work"]` and `phoneNumbers[type eq "work"]` are processed. All other types are skipped.

## Service issues

#### Unsupported scenarios

- Provisioning passwords isn't supported.
- Provisioning nested groups beyond the first level is not supported.
- Provisioning is not supported for B2C tenants, including into or out of the tenant.
- Inbound provisioning using System for Cross‑domain Identity Management (SCIM) is not supported. Use Microsoft Graph and [Microsoft Graph batch](/en-us/graph/json-batching) instead.
- Not all provisioning apps are available in all clouds.

::: zone pivot="app-provisioning"

#### Automatic provisioning isn't available on my OIDC-based application

If you create an app registration, the corresponding service principal in enterprise apps won't be enabled for automatic user provisioning. You'll need to either request the app be added to the gallery, if intended for use by multiple organizations, or create a second non-gallery app for provisioning.

#### Manager isn't provisioned

If a user and their manager are both in scope for provisioning, the service provisions the user and then updates the manager. If on day one the user is in scope and the manager is out of scope, we'll provision the user without the manager reference. When the manager comes into scope, the manager reference won't be updated until you restart provisioning and cause the service to reevaluate all the users again.

#### Gallery application doesn't support provisioning in US Government or 21Vianet (China) clouds

The non-gallery / custom application and ecma connector are available for provisioning in the US Government / 21Vianet (China) clouds. A limited number of gallery applications are available in these environments.

::: zone-end

#### The provisioning interval is fixed

The [time](application-provisioning-when-will-provisioning-finish-specific-user#how-long-will-it-take-to-provision-users) between provisioning cycles is currently not configurable.

#### Changes not moving from target app to Microsoft Entra ID

The app provisioning service isn't aware of changes made in external apps. So, no action is taken to roll back. The app provisioning service relies on changes made in Microsoft Entra ID.

#### Switching from Sync All to Sync Assigned not working

After you change scope from **Sync All** to **Sync Assigned**, make sure to also perform a restart to ensure that the change takes effect. You can do the restart from the UI.

#### Provisioning cycle continues until completion

When you set provisioning to `enabled = off` or select **Stop**, the current provisioning cycle continues running until completion. The service stops executing any future cycles until you turn provisioning on again.

#### Member of group not provisioned

When a group is in scope and a member is out of scope, the group will be provisioned. The out-of-scope user won't be provisioned. If the member comes back into scope, the service won't immediately detect the change. Restarting provisioning addresses the issue. Periodically restart the service to ensure that all users are properly provisioned.

#### Global Reader

The Global Reader role is unable to read the provisioning configuration. Create a custom role with the `microsoft.directory/applications/synchronization/standard/read` permission in order to read the provisioning configuration from the Microsoft Entra admin center.

#### Microsoft Azure Government Cloud

Credentials, including the secret token, notification email, and SSO certificate notification emails together have a 1KB limit in the Microsoft Azure Government Cloud.

::: zone pivot="app-provisioning"

## On-premises application provisioning

This is a current list of known limitations with the Microsoft Entra ECMA Connector Host and on-premises application provisioning.

### SQL Connector connectivity

The SQL Connector expects the DSN file to be encoded in UTF-8. Other encodings might not be read correctly and result in the error "Data source name not found and no default driver specified."

### Application and directories

The following applications and directories aren't yet supported.

#### Active Directory Domain Services (user or group writeback from Microsoft Entra ID by using the on-premises provisioning preview)

- When a user is managed by Microsoft Entra Connect, the source of authority is on-premises Active Directory Domain Services. So, user attributes can't be changed in Microsoft Entra ID. This preview doesn't change the source of authority for users managed by Microsoft Entra Connect.
- Attempting to use Microsoft Entra Connect and the on-premises provisioning to provision groups or users into Active Directory Domain Services can lead to creation of a loop, where Microsoft Entra Connect can overwrite a change that was made by the provisioning service in the cloud. Microsoft is working on a dedicated capability for group or user writeback. Upvote the UserVoice feedback on [this website](https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789/) to track the status of the preview. Alternatively, you can use [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) for user or group writeback from Microsoft Entra ID to Active Directory.

#### Microsoft Entra ID

By using on-premises provisioning, you can take a user already in Microsoft Entra ID and provision them into a third-party application. *You can't bring a user into the directory from a third-party application.* Customers will need to rely on our native HR integrations, Microsoft Entra Connect, Microsoft Identity Manager, or Microsoft Graph, to bring users into the directory.

### Attributes and objects

The following attributes and objects aren't supported:

- Multivalued attributes.
- Reference attributes (for example, manager).
- Groups.
- Complex anchors (for example, ObjectTypeName+UserName).
- Attributes that have characters such as "." or "["
- Binary attributes.
- On-premises applications are sometimes not federated with Microsoft Entra ID and require local passwords. The on-premises provisioning preview doesn't support password synchronization. Provisioning initial one-time passwords is supported. Ensure that you're using the [Redact](functions-for-customizing-application-data#redact) function to redact the passwords from the logs. In the SQL and LDAP connectors, the passwords aren't exported on the initial call to the application, but rather a second call with set password.

#### SSL certificates

The Microsoft Entra ECMA Connector Host currently requires either an SSL certificate to be trusted by Azure or the provisioning agent to be used. The certificate subject must match the host name the Microsoft Entra ECMA Connector Host is installed on.

#### Anchor attributes

The Microsoft Entra ECMA Connector Host currently doesn't support anchor attribute changes (renames) or target systems, which require multiple attributes to form an anchor.

#### Attribute discovery and mapping

The attributes that the target application supports are discovered and surfaced in the Microsoft Entra admin center in **Attribute Mappings**. Newly added attributes will continue to be discovered. If an attribute type has changed, for example, string to Boolean, and the attribute is part of the mappings, the type won't change automatically in the Microsoft Entra admin center. Customers will need to go into advanced settings in mappings and manually update the attribute type.

#### Provisioning agent

- The agent doesn't currently support auto update for the on-premises application provisioning scenario. We're actively working to close this gap and ensure that auto update is enabled by default and required for all customers.
- The same provisioning agent can't be used for on-premises app provisioning and cloud sync / HR- driven provisioning.

::: zone-end