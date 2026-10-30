---
layout: Conceptual
title: 'Microsoft Entra Connect Sync: Changing the default configuration - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-best-practices-changing-default-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Provides best practices for changing the default configuration of Microsoft Entra Connect Sync.
ms.assetid: 7638a031-1635-4942-94c3-fce8f09eed5e
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: d1f2fae0-4d53-903c-a991-31452f6d118d
document_version_independent_id: 4de41410-bbea-f24a-dbf8-74c519a63cc9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-best-practices-changing-default-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-best-practices-changing-default-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-best-practices-changing-default-configuration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d588f183-f3ea-b498-9d9b-bec62753725b
---

# Microsoft Entra Connect Sync: Changing the default configuration - Microsoft Entra ID | Microsoft Learn

The purpose of this topic is to describe supported and unsupported changes to Microsoft Entra Connect Sync.

The configuration Microsoft Entra Connect creates works “as is” for most environments that synchronize on-premises Active Directory with Microsoft Entra ID. However, in some cases, it's necessary to apply some changes to a configuration to satisfy a particular need or requirement.

## Changes to the service account

Microsoft Entra Connect Sync is running under a service account created by the installation wizard. This service account holds the encryption keys to the database used by sync. It's created with a 127 characters long password and the password is set to not expire.

Warning

If you change or reset the ADSync service account password, the Synchronization Service won't start correctly until you've abandoned the encryption key and reinitialized the ADSync service account password. To do this, see [Changing the ADSync service account password](how-to-connect-sync-change-serviceacct-pass).

## Changes to the scheduler

Starting with the releases from build 1.1 (February 2016) you can configure the [scheduler](how-to-connect-sync-feature-scheduler) to have a different sync cycle than the default 30 minutes.

## Changes to Synchronization Rules

The installation wizard provides a configuration that is supposed to work for the most common scenarios. In case you need to make changes to the configuration, then you must follow these rules to have a supported configuration.

Warning

If you make changes to the default sync rules then these changes are overwritten the next time Microsoft Entra Connect is updated, resulting in unexpected and likely unwanted synchronization results.

- You can [change attribute flows](how-to-connect-sync-change-the-configuration#other-common-attribute-flow-changes) if the default direct attribute flows are not suitable for your organization.
- If you want to [not flow an attribute](how-to-connect-sync-change-the-configuration#do-not-flow-an-attribute) and remove any existing attribute values in Microsoft Entra ID, then you need to create a rule for this scenario.
- Disable an unwanted Sync Rule rather than deleting it. A deleted rule is recreated during an upgrade.
- To change an out-of-box rule, you should make a copy of the original rule and disable the out-of-box rule. The Sync Rule Editor prompts and helps you.
- Export your custom synchronization rules using the Synchronization Rules Editor. The editor provides you with a PowerShell script you can use to easily recreate them in a disaster recovery scenario.

Warning

The out-of-box sync rules have a thumbprint. If you make a change to these rules, the thumbprint is no longer matching. You might have problems in the future when you try to apply a new release of Microsoft Entra Connect. Only make changes the way it's described in this article.

### Disable an unwanted Sync Rule

Don't delete an out-of-box sync rule. It's recreated during next upgrade.

In some cases, the installation wizard produces a configuration that isn't working for your topology. For example, if you have an account-resource forest topology but you've extended the schema in the account forest with the Exchange schema, then rules for Exchange are created for the account forest and the resource forest. In this case, you need to disable the Sync Rule for Exchange.

![Disabled sync rule](media/how-to-connect-sync-best-practices-changing-default-configuration/exchangedisabledrule.png)

In the prior picture, the installation wizard found an old Exchange 2003 schema in the account forest. This schema extension was added before the resource forest was introduced in Fabrikam's environment. To ensure no attributes from the old Exchange implementation are synchronized, the sync rule should be disabled as shown.

### Change an out-of-box rule

The only time you should change an out-of-box rule is when you need to change the join rule. If you need to change an attribute flow, then you should create a sync rule with higher precedence than the out-of-box rules. The only rule you practically need to clone is the rule **In from AD - User Join**. You can override all other rules with a higher precedence rule.

If you need to make changes to an out-of-box rule, then you should make a copy of the out-of-box rule and disable the original rule. Then make the changes to the cloned rule. The Sync Rule Editor is helping you with those steps. When you open an out-of-box rule, you're presented with this dialog box:![Warning out of box rule](media/how-to-connect-sync-best-practices-changing-default-configuration/warningoutofboxrule.png)

Select **Yes** to create a copy of the rule. The cloned rule is then opened.![Cloned rule](media/how-to-connect-sync-best-practices-changing-default-configuration/clonedrule.png)

On this cloned rule, make any necessary changes to scope, join, and transformations.