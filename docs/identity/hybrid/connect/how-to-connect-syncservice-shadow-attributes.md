---
layout: Conceptual
title: Microsoft Entra Connect Sync service shadow attributes - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-syncservice-shadow-attributes
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Describes how shadow attributes work in Microsoft Entra Connect Sync service.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 45995e13-c79a-56de-0b9a-44bfa1f2c58a
document_version_independent_id: 375a228f-819e-8de9-1c32-44a0e6a65fbc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-syncservice-shadow-attributes.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-syncservice-shadow-attributes
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-syncservice-shadow-attributes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8e01b5db-bcfa-8232-bd65-36c2c366612e
---

# Microsoft Entra Connect Sync service shadow attributes - Microsoft Entra ID | Microsoft Learn

Most attributes are represented the same way in Microsoft Entra ID as they are in your on-premises Active Directory. But some attributes have some special handling and the attribute value in Microsoft Entra ID might be different than what Microsoft Entra Connect synchronizes.

## Introducing shadow attributes

Some attributes have two representations in Microsoft Entra ID. Both the on-premises value and a calculated value are stored. These extra attributes are called shadow attributes. The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**. The sync engine in Microsoft Entra Connect and cloud sync exports the value to the shadow attribute and then Microsoft Entra ID processes this attribute to calculate the final value. The sync engine also imports values from the shadow attribute, so even if the final calculated value is different, from the sync engine perspective, it's able to confirm the original value that was exported. You can't see the shadow attributes using the [Microsoft Entra admin center](https://entra.microsoft.com) or with PowerShell, but understanding this concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.

To better understand the behavior, look at this example from Fabrikam:![Screenshot shows the Active Directory UPN Suffix for several examples with a corresponding Microsoft Entra Domain value of Not Added, Not Verified, and Verified.](media/how-to-connect-syncservice-shadow-attributes/domains.png) They have multiple UserPrincipalName (UPN) suffixes in their on-premises Active Directory, but only one is verified in Microsoft Entra ID.

### userPrincipalName

A user has the following attribute values in a nonverified domain:

| Attribute | Value |
| --- | --- |
| on-premises userPrincipalName | lee.sperry@fabrikam.com |
| Microsoft Entra shadowUserPrincipalName | lee.sperry@fabrikam.com |
| Microsoft Entra userPrincipalName | lee.sperry@fabrikam.onmicrosoft.com |

The userPrincipalName attribute is the value you see when using PowerShell.

Since the real on-premises attribute value is stored in Microsoft Entra ID, when you verify the fabrikam.com domain, Microsoft Entra ID updates the userPrincipalName attribute with the value from the shadowUserPrincipalName. You don't have to synchronize any changes from Microsoft Entra Connect or cloud sync for these values to be updated.

### proxyAddresses

The same process for only including verified domains also occurs for proxyAddresses, but with some extra logic. The check for verified domains only happens for mailbox users. A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.

For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear. It could look like this:

| Attribute | Value |
| --- | --- |
| on-premises proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com smtp:abbie.spencer@fabrikam.com smtp:abbie@fabrikamonline.com |
| Exchange Online proxyAddresses | SMTP:abbie.spencer@fabrikamonline.com smtp:abbie@fabrikamonline.com SIP:abbie.spencer@fabrikamonline.com |

In this case, **smtp:abbie.spencer@fabrikam.com** was removed since that domain isn't verified. But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam might not be using on-premises Lync/Skype for Business, but Microsoft Entra ID and Exchange Online prepare for it.

This logic for proxyAddresses is referred to as **ProxyCalc**. ProxyCalc is invoked with every change on a user when:

- The user gets a service plan assigned that includes Exchange Online even if the user wasn't licensed for an Exchange mailbox. For example, if the user is assigned the Office E3 SKU, but only SharePoint Online service is selected. This condition is true even if the user's mailbox is still on-premises.
- The attribute msExchRecipientTypeDetails have a value.
- You make a change to proxyAddresses or userPrincipalName.

ProxyCalc process sanitizes an address if ShadowProxyAddresses contains a nonverified domain and the user has one of the following properties configured.

- User is licensed with an EXO service type plan enabled (Excluding Microsoft Bookings, MyAnalytics, and Premium Encryption in Office 365)
- User has MSExchRemoteRecipientType set (not null)
- User is considered a shared resource

The user is considered a shared resource when its CloudMSExchRecipientDisplayType attribute has one of the following values:

| Object Display Type | Value (Decimal) |
| --- | --- |
| MailboxUser | 0 |
| PublicFolder | 2 |
| ConferenceRoomMailbox | 7 |
| EquipmentMailbox | 8 |
| ArbitrationMailbox | 10 |
| RoomList | 15 |
| TeamMailboxUser | 16 |
| GroupMailbox | 17 |
| SchedulingMailbox | 18 |
| ACLableMailboxUser | 1073741824 |
| ACLableTeamMailboxUser | 1073741840 |

Note

CloudMSExchRecipientDisplayType isn't visible from the Microsoft Entra ID side and can only be viewed using Exchange Online cmdlet [Get-Recipient](/en-us/powershell/module/exchange/get-recipient).

Example:

```PowerShell
  Get-Recipient admin | fl *type*
```

ProxyCalc might take some time to process a change on a user and isn't synchronous with the Microsoft Entra Connect export process.

Note

The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic. This topic is provided for you to understand the behavior and not document all internal logic.

### Quarantined attribute values

Shadow attributes are also used when there are duplicate attribute values. For more information, see [duplicate attribute resiliency](how-to-connect-syncservice-duplicate-attribute-resiliency).