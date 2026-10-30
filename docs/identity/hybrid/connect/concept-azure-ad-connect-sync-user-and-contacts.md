---
layout: Conceptual
title: 'Microsoft Entra Connect Sync: Understanding Users, Groups, and Contacts - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/concept-azure-ad-connect-sync-user-and-contacts
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Explains users, groups, and contacts in Microsoft Entra Connect Sync.
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 517b623e-4449-1fe4-2b57-cd30af3faec5
document_version_independent_id: 4383ed6c-413f-c25a-5ab3-016ab7c12363
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/concept-azure-ad-connect-sync-user-and-contacts.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/concept-azure-ad-connect-sync-user-and-contacts
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/concept-azure-ad-connect-sync-user-and-contacts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 4fe1213b-22ec-85f4-2306-0ca9bff3c719
---

# Microsoft Entra Connect Sync: Understanding Users, Groups, and Contacts - Microsoft Entra ID | Microsoft Learn

There are several different reasons why you would have multiple Active Directory forests and there are several different deployment topologies. Common models include an account-resource deployment and GAL sync’ed forests after a merger & acquisition. But even if there are pure models, hybrid models are common as well. The default configuration in Microsoft Entra Connect Sync doesn't assume any particular model. However, depending on how user matching was selected in the installation guide, different behaviors can be observed.

In this article, we go through how the default configuration behaves in certain topologies. We go through the configuration and the Synchronization Rules Editor can be used to look at the configuration.

There are a few general rules the configuration assumes:

- Regardless of which order we import from the source Active Directories, the end result should always be the same.
- An active account contributes sign-in information, including **userPrincipalName** and **sourceAnchor**.
- A disabled account contributes userPrincipalName and sourceAnchor, unless it's a linked mailbox, if there's no active account to be found.
- An account with a linked mailbox is never be used for userPrincipalName and sourceAnchor. It's assumed that an active account will be found later.
- A contact object might be provisioned to Microsoft Entra ID as a contact or as a user. You don’t really know until all source Active Directory forests are processed.

## Groups

Note

Keep in mind that when you add a user from another forest to the group, there is an anchor created in the Active Directory where the groups exists inside a specific OU. This anchor is a Foreign security principal and is stored inside the OU ‘ForeignSecurityPrincipals’. If you don't synchronize this OU the users are removed from the group membership.

Important points to be aware of when synchronizing groups from Active Directory to Microsoft Entra ID:

- Microsoft Entra Connect excludes built-in security groups from directory synchronization.
- Microsoft Entra Connect doesn't support synchronizing [Primary Group memberships](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771489%28v=ws.11%29) to Microsoft Entra ID.
- Microsoft Entra Connect doesn't support synchronizing [Dynamic Distribution Group memberships](/en-us/exchange/recipients/dynamic-distribution-groups/dynamic-distribution-groups) to Microsoft Entra ID.
- To synchronize an Active Directory group to Microsoft Entra ID as a mail-enabled group:

    - If the group's *proxyAddress* attribute is empty, its *mail* attribute must have a value
    - If the group's *proxyAddress* attribute is non-empty, it must contain at least one SMTP proxy address value. Here are some examples:

        - An Active Directory group whose proxyAddress attribute has value *{"X500:/0=contoso.com/ou=users/cn=testgroup"}* won't be mail-enabled in Microsoft Entra ID. It doesn't have an SMTP address.
        - An Active Directory group whose proxyAddress attribute has values *{"X500:/0=contoso.com/ou=users/cn=testgroup","SMTP:johndoe@contoso.com"}* will be mail-enabled in Microsoft Entra ID.
        - An Active Directory group whose proxyAddress attribute has values *{"X500:/0=contoso.com/ou=users/cn=testgroup", "smtp:johndoe@contoso.com"}* will also be mail-enabled in Microsoft Entra ID.

## Contacts

Having contacts representing a user in a different forest is common after a merger & acquisition where a GALSync solution is bridging two or more Exchange forests. The contact object is always joining from the connector space to the metaverse using the mail attribute. If there's already a contact object or user object with the same mail address, the objects are joined together. This is configured in the rule **In from AD – Contact Join**. There's also a rule named **In from AD – Contact Common** with an attribute flow to the metaverse attribute **sourceObjectType** with the constant **Contact**. This rule has low precedence so if any user object is joined to the same metaverse object, then the rule **In from AD – User Common** contributes the value User to this attribute. With this rule, this attribute has the value Contact if no user is joined and the value User if at least one user is found.

For provisioning an object to Microsoft Entra ID, the outbound rule **Out to Microsoft Entra ID – Contact Join** creates a contact object if the metaverse attribute **sourceObjectType** is set to **Contact**. If this attribute is set to **User**, then the rule **Out to Microsoft Entra ID – User Join** creates a user object instead. It's possible that an object is promoted from Contact to User when more source Active Directories are imported and synchronized.

For example, in a GALSync topology we find contact objects for everyone in the second forest when we import the first forest. This stages new contact objects in the Microsoft Entra Connector. When we later import and synchronize the second forest, we find the real users and join them to the existing metaverse objects. We'll then delete the contact object in Microsoft Entra ID and create a new user object instead.

If you have a topology where users are represented as contacts, make sure you select to match users on the mail attribute in the installation guide. If you select another option, then you have an order-dependent configuration. Contact objects always join on the mail attribute, but user objects only join on the mail attribute if this option was selected in the installation guide. You could then end up with two different objects in the metaverse with the same mail attribute if the contact object was imported before the user object. During export to Microsoft Entra ID, an error is shown. This behavior is by design and would indicate bad data or that the topology wasn't correctly identified during the installation.

## Disabled accounts

Disabled accounts are synchronized as well to Microsoft Entra ID. Disabled accounts are common to represent resources in Exchange, for example conference rooms. The exception is users with a linked mailbox; as previously mentioned, these never provision an account to Microsoft Entra ID.

The assumption is that if a disabled user account is found, then we won't find another active account later. The object is provisioned to Microsoft Entra ID with the userPrincipalName and sourceAnchor found. In case another active account join to the same metaverse object, then its userPrincipalName and sourceAnchor are used.

## Changing sourceAnchor

When an object is exported to Microsoft Entra ID, then it's not allowed to change the sourceAnchor anymore. When the object is exported the metaverse attribute **cloudSourceAnchor** is set with the **sourceAnchor** value accepted by Microsoft Entra ID. If **sourceAnchor** is changed and not match **cloudSourceAnchor**, the rule **Out to Microsoft Entra ID – User Join** throws the error **sourceAnchor attribute has changed**. In this case, the configuration or data must be corrected so the same sourceAnchor is present in the metaverse again before the object can be synchronized again.