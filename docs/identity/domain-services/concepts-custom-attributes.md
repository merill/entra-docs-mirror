---
layout: Conceptual
title: Create and manage custom attributes for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/concepts-custom-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to create and manage custom attributes in a Domain Services managed domain.
ms.assetid: 1a14637e-b3d0-4fd9-ba7a-576b8df62ff2
ms.topic: how-to
ms.date: 2025-03-07T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: e037eaf2-95d5-e9b5-256e-07736e6c66db
document_version_independent_id: 2595ba88-a097-0949-6a5b-38c54f2303c7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/concepts-custom-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/concepts-custom-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/concepts-custom-attributes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 2fe709b4-2d1a-d9b9-3dcc-0b877df9bc7b
---

# Create and manage custom attributes for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

For various reasons, companies often can't modify code for legacy apps. For example, apps may use a custom attribute, such as a custom employee ID, and rely on that attribute for LDAP operations.

Microsoft Entra ID supports adding custom data to resources using [extensions](/en-us/graph/extensibility-overview). Microsoft Entra Domain Services can synchronize the following types of extensions from Microsoft Entra ID, so you can also use apps that depend on custom attributes with Domain Services:

- [onPremisesExtensionAttributes](/en-us/graph/extensibility-overview?tabs=http#extension-attributes) are a set of 15 attributes that can store extended user string attributes.
- [Directory extensions](/en-us/graph/extensibility-overview?tabs=http#directory-azure-ad-extensions) allow the schema extension of specific directory objects, such as users and groups, with strongly typed attributes through registration with an application in the tenant.

Both types of extensions can be configured by using Microsoft Entra Connect for users who are managed on-premises, or Microsoft Graph APIs for cloud-only users.

Note

The following types of extensions aren't supported for synchronization:

- Custom security attributes in Microsoft Entra ID
- Microsoft Graph schema extensions
- Microsoft Graph open extensions

## Requirements

The minimum SKU supported for custom attributes is the Enterprise SKU. If you use Standard, you need to [upgrade](change-sku) the managed domain to Enterprise or Premium. For more information, see [Microsoft Entra Domain Pricing](https://azure.microsoft.com/pricing/details/active-directory-ds/).

## How custom attributes work

After you create a managed domain, click **Custom Attributes** under **Settings** to enable attribute synchronization. Click **Save** to confirm the change.

![Screenshot of how to enable custom attributes.](media/concepts-custom-attributes/enable.png)

## Enable predefined attribute synchronization

Click **OnPremisesExtensionAttributes** to synchronize the attributes extensionAttribute1-15, also known as [Exchange custom attributes](/en-us/graph/api/resources/onpremisesextensionattributes).

## Synchronize Microsoft Entra directory extension attributes

These are the extended user or group attributes defined in your Microsoft Entra tenant.

Select **+ Add** to choose which custom attributes to synchronize. The list shows the available extension properties in your tenant. You can filter the list by using the search bar.

![Screenshot of how to add directory extension attributes.](media/concepts-custom-attributes/add.png)

If you don't see the directory extension you are looking for, enter the extension's associated application appId and click **Search** to load only that application's defined extension properties. This search helps when multiple applications define many extensions in your tenant.

Note

If you would like to see directory extensions synchronized by Microsoft Entra Connect, click **Enterprise App** and look for the Application ID of the **Tenant Schema Extension App**. For more information, see [Microsoft Entra Connect Sync: Directory extensions](/en-us/azure/active-directory/hybrid/connect/how-to-connect-sync-feature-directory-extensions#configuration-changes-in-azure-ad-made-by-the-wizard).

Click **Select**, and then **Save** to confirm the change.

![Screenshot of how to save directory extension attributes.](media/concepts-custom-attributes/select.png)

Domain Services back fills all synchronized users and groups with the onboarded custom attribute values. The custom attribute values gradually populate for objects that contain the directory extension in Microsoft Entra ID. During the backfill synchronization process, incremental changes in Microsoft Entra ID are paused, and the sync time depends on the size of the tenant.

To check the backfilling status, click **Domain Services Health** and verify the **Synchronization with Microsoft Entra ID** monitor has an updated timestamp within an hour since onboarding. Once updated, the backfill is complete.

## Reserved attributes for Active Directory Domain Services

The following attributes are reserved for Active Directory Domain Services in Windows Server. They can't be used for Microsoft Entra Domain Services.

| Name | Attribute |
| --- | --- |
| AccountDisabled | accountDisabled |
| AzureAdMailNickname | msDS-AzureADMailNickname |
| AadObjectId | msDS-aadObjectId |
| City | l |
| CommonName | cn |
| Company | company |
| Country | co |
| Department | department |
| Description | description |
| DisplayName | displayName |
| DistinguishedName | distinguishedName |
| EmployeeId | employeeId |
| ExchangeExtensions | extensionAttribute |
| ExchangeExtension1 | extensionAttribute1 |
| ExchangeExtension2 | extensionAttribute2 |
| ExchangeExtension3 | extensionAttribute3 |
| ExchangeExtension4 | extensionAttribute4 |
| ExchangeExtension5 | extensionAttribute5 |
| ExchangeExtension6 | extensionAttribute6 |
| ExchangeExtension7 | extensionAttribute7 |
| ExchangeExtension8 | extensionAttribute8 |
| ExchangeExtension9 | extensionAttribute9 |
| ExchangeExtension10 | extensionAttribute10 |
| ExchangeExtension11 | extensionAttribute11 |
| ExchangeExtension12 | extensionAttribute12 |
| ExchangeExtension13 | extensionAttribute13 |
| ExchangeExtension14 | extensionAttribute14 |
| ExchangeExtension15 | extensionAttribute15 |
| FacsimileTelephoneNumber | facsimileTelephoneNumber |
| GenerationSeq | msDS-generationSeq |
| GivenName | givenName |
| GroupType | groupType |
| LinkSeq | msDS-linkSeq |
| Mail | mail |
| Manager | manager |
| Member | member |
| MemberOf | memberOf |
| Mobile | mobile |
| ObjectClass | objectClass |
| ObjectGloballyUniqueIdentifier | objectGUID |
| Pager | pager |
| PhysicalDeliveryOfficeName | physicalDeliveryOfficeName |
| PostalCode | postalCode |
| PreferredLanguage | preferredLanguage |
| ProxyAddresses | proxyAddresses |
| PasswordLastSet | pwdLastSet |
| SamAccountName | sAMAccountName |
| SecurityDescriptor | nTSecurityDescriptor |
| SidHistory | sIDHistory |
| State | st |
| StreetAddress | streetAddress |
| Surname | sn |
| SupplementalCredentials | supplementalCredentials |
| TelephoneNumber | telephoneNumber |
| Title | title |
| UnicodePwd | unicodePwd |
| UserAccountControl | userAccountControl |
| UserPrincipalName | userPrincipalName |
| EscrowType | msDS-escrowType |
| EscrowOperation | msDS-escrowOperation |
| SourceAadObjectId | msDS-aadObjectId |
| TargetAadObjectId | msDS-targetAadObjectId |
| AadGraphLink | msDS-aadGraphLink |
| AadGraphDQLink | msDS-aadlink |
| EscrowCount | msDS-escrowCount |
| FirstSteadyStateTime | msDS-firstSteadyStateTime |
| LastSteadyStateTime | msDS-lastSteadyStateTime |
| QuarantineStartTime | msDS-quarantineStartTime |
| QuarantineSyncWaitPeriod | msDS-quarantineSyncWaitPeriod |
| SingleSyncRequests | msDS-singleSyncRequests |
| StringValues | msDS-stringValues |
| SyncRequestStatus | msDS-syncRequestStatus |
| SyncStatus | msDS-syncStatus |
| WhenChanged | whenChanged |
| DeletedObjectNumber | msDS-deletedObjectNumber |
| CustomAttributeState | msDS-customAttribute-state |
| CustomAttributeType | msDS-customAttribute-type |
| LegacyAadObjectId | msDS-AzureADObjectId |
| Name | name |
| Revision | revision |
| AdminDisplayName | adminDisplayName |
| AdminDescription | adminDescription |
| LdapDisplayName | lDAPDisplayName |
| AttributeId | attributeId |
| AttributeSyntax | attributeSyntax |
| OmSyntax | omSyntax |
| IsSingleValued | isSingleValued |
| MayContain | mayContain |
| SchemaUpdateNow | schemaUpdateNow |
| IsDefunct | isDefunct |