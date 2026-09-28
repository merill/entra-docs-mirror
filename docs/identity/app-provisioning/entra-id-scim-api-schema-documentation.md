---
layout: Conceptual
title: Microsoft Entra ID SCIM API schema documentation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/entra-id-scim-api-schema-documentation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: pmwongera
description: This article provides a reference for SCIM schema attributes, including core user and group attributes, enterprise extensions, and Microsoft Entra-specific extensions, along with their mappings to Microsoft Entra ID properties.
ms.topic: how-to
ms.date: 2026-09-04T00:00:00.0000000Z
ms.reviewer: chmutali
ai-usage: ai-assisted
locale: en-us
document_id: 26ff5117-a197-bf13-8968-dcd5c0c33dd1
document_version_independent_id: 26ff5117-a197-bf13-8968-dcd5c0c33dd1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/entra-id-scim-api-schema-documentation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/entra-id-scim-api-schema-documentation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/entra-id-scim-api-schema-documentation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f219f1f3-b320-b9b0-b874-55c525ab1c28
---

# Microsoft Entra ID SCIM API schema documentation - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID SCIM API supports standard SCIM schema elements and Microsoft Entra ID specific extensions. The SCIM schema is published at the endpoint https://graph.microsoft.com/rp/scim/schemas This article describes how SCIM schema attributes map to Microsoft Entra ID [user properties](/en-us/graph/api/resources/user#properties) and [group properties](/en-us/graph/api/resources/group#properties).

Note

Attribute value constraints enforced by Microsoft Entra ID also apply to the corresponding SCIM attribute.

## User - Core

| SCIM Attribute | Microsoft Entra ID Attribute | Notes / Restrictions |
| --- | --- | --- |
| active | accountEnabled |  |
| addresses[type eq "work"].country/region | country/region | Only one *addresses* value is allowed, and it requires a type of "work". |
| addresses[type eq "work"].locality | city |  |
| addresses[type eq "work"].postalCode | postalCode |  |
| addresses[type eq "work"].region | state |  |
| addresses[type eq "work"].streetAddress | streetAddress |  |
| displayName | displayName |  |
| emails[type eq "other"].value | otherMails | A list of email addresses associated with the user that may not be linked to their Exchange Online recipient object, such as a personal email address. |
| emails[type eq "proxyAddress"].value | proxyAddresses - only for values that start with SMTP: (case-insensitive) | A read-only list of email addresses. This attribute is currently implemented as type "work" and primary equal to false. |
| emails[type eq "work" and primary eq true].value | mail | Only one value of type "work" and primary *true* is allowed. |
| externalId | crossDomainData.scim.v2.externalId | This attribute is persisted in the Graph entity `crossDomainData`. |
| groups.value | *See notes* | Read only. The user’s group memberships. This attribute is never returned in the JSON body of a user and is only usable for filter queries. |
| ims[type eq "work"].value | imAddresses |  |
| name.familyName | surname |  |
| name.givenName | givenName |  |
| password | *See notes* | Required for users with a userName value containing a domain name that is managed (nonfederated). Write only (can't be read). Can only be set on user creation, can't be used to update a user’s password. |
| phoneNumbers[type eq "fax"].value | faxNumber | Only one value of this type is allowed. |
| phoneNumbers[type eq "mobile"].value | mobilePhone | Only one value of this type is allowed. |
| phoneNumbers[type eq "work"].value | businessPhones | Only one value of this type is allowed. |
| preferredLanguage | preferredLanguage | Only allows a single language value and doesn't accept a ranked preference list. |
| title | jobTitle |  |
| userName | userPrincipalName |  |
| userType | employeeType |  |

## User - Enterprise Extension

Attributes in this table are part of namespace `urn:ietf:params:scim:schemas:extension:enterprise:2.0:User`.

| SCIM Attribute | Microsoft Entra ID Attribute |
| --- | --- |
| costCenter | employeeOrgData.costCenter |
| department | department |
| division | employeeOrgData.division |
| employeeNumber | employeeId |
| manager.value | manager |
| organization | companyName |

## User - Microsoft Entra Extension

Attributes in this table are part of namespace `urn:ietf:params:scim:schemas:extension:Microsoft:Entra:2.0:User`.

| SCIM Attribute | Microsoft Entra ID Attribute |
| --- | --- |
| creationType | creationType |
| employeeHireDate | employeeHireDate |
| employeeLeaveDateTime | employeeLeaveDateTime |
| lastPasswordChangeDateTime | lastPasswordChangeDateTime |
| mailNickname | mailNickname |
| officeLocation | officeLocation |
| onPremisesDistinguishedName | onPremisesDistinguishedName |
| onPremisesDomainName | onPremisesDomainName |
| onPremisesExtensionAttributes.extensionAttribute1 | extensionAttribute1 |
| onPremisesExtensionAttributes.extensionAttribute10 | extensionAttribute10 |
| onPremisesExtensionAttributes.extensionAttribute11 | extensionAttribute11 |
| onPremisesExtensionAttributes.extensionAttribute12 | extensionAttribute12 |
| onPremisesExtensionAttributes.extensionAttribute13 | extensionAttribute13 |
| onPremisesExtensionAttributes.extensionAttribute14 | extensionAttribute14 |
| onPremisesExtensionAttributes.extensionAttribute15 | extensionAttribute15 |
| onPremisesExtensionAttributes.extensionAttribute2 | extensionAttribute2 |
| onPremisesExtensionAttributes.extensionAttribute3 | extensionAttribute3 |
| onPremisesExtensionAttributes.extensionAttribute4 | extensionAttribute4 |
| onPremisesExtensionAttributes.extensionAttribute5 | extensionAttribute5 |
| onPremisesExtensionAttributes.extensionAttribute6 | extensionAttribute6 |
| onPremisesExtensionAttributes.extensionAttribute7 | extensionAttribute7 |
| onPremisesExtensionAttributes.extensionAttribute8 | extensionAttribute8 |
| onPremisesExtensionAttributes.extensionAttribute9 | extensionAttribute9 |
| onPremisesImmutableId | onPremisesImmutableId |
| onPremisesSAMAccountName | onPremisesSAMAccountName |
| onPremisesSecurityIdentifier | onPremisesSecurityIdentifier |
| onPremisesSyncEnabled | onPremisesSyncEnabled |
| onPremisesUserPrincipalName | onPremisesUserPrincipalName |
| ownedGroups.value | ownedObjects (groups only) |
| passwordForceChangeOnNextSignIn | passwordProfile.forceChangePasswordNextSignIn |
| passwordForceChangeOnNextSignInWithMFA | passwordProfile.forceChangePasswordNextSignInWithMFA |
| preferredDataLocation | preferredDataLocation |
| proxyAddresses | proxyAddresses (all values) |
| usageLocation | usageLocation |
| userType | userType |

Note

`urn:ietf:params:scim:schemas:extension:Microsoft:Entra:2.0:User:ownedGroups` is a read-only, multi-valued complex attribute. Its `value` sub attribute contains a group ID. The attribute has a `returned` value of `never`, so it isn't included in user response bodies. You can use the fully qualified `urn:ietf:params:scim:schemas:extension:Microsoft:Entra:2.0:User:ownedGroups.value` path as a filter target to find users who own a specific group.

Note

The Microsoft Entra extension namespace doesn't include Microsoft Entra ID Directory Extensions of the form `extension_{appId-without-hyphens}_{extensionProperty-name}`. The SCIM APIs don't support retrieving these attributes on the user profile.

## Group – Core

| SCIM Attribute | Microsoft Entra ID Attribute | Notes / Restrictions |
| --- | --- | --- |
| displayName | displayName |  |
| members.value | *See Notes column* | Read only. The group’s members. This attribute is never returned in the JSON body of a group and is only usable for filter queries. |

## Group – Microsoft Entra Extension

Attributes in this table are part of namespace `urn:ietf:params:scim:schemas:extension:Microsoft:Entra:2.0:Group`.

| SCIM Attribute | Microsoft Entra ID Attribute |
| --- | --- |
| description | description |
| expirationDateTime | expirationDateTime |
| groupTypes | groupTypes |
| mailEnabled | mailEnabled |
| mailNickname | mailNickname |
| onPremisesSAMAccountName | onPremisesSAMAccountName |
| onPremisesSecurityIdentifier | onPremisesSecurityIdentifier |
| onPremisesSyncEnabled | onPremisesSyncEnabled |
| owners.value | owners |
| proxyAddresses | proxyAddresses (all values) |
| securityEnabled | securityEnabled |
| securityIdentifier | securityIdentifier |

Note

`urn:ietf:params:scim:schemas:extension:Microsoft:Entra:2.0:Group:owners` is a read-only, multi-valued complex attribute. Its `value` sub attribute contains a user ID. The attribute has a `returned` value of `never`, so it isn't included in group response bodies. You can use the fully qualified `urn:ietf:params:scim:schemas:extension:Microsoft:Entra:2.0:Group:owners.value` path as a filter target to find groups owned by a specific user.

## Custom Security Attributes namespace

If you have Custom Security Attributes defined in your Microsoft Entra ID tenant, then use this namespace `urn:ietf:params:scim:schemas:extension:Microsoft:Entra:2.0:CustomSecurityAttributes` in your SCIM requests.