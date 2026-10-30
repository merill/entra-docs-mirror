---
layout: Conceptual
title: Connectors in the Microsoft Entra Connect Sync Service Manager UI' - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-service-manager-ui-connectors
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Understand the Connectors tab in the Service Manager for Microsoft Entra Connect Sync.
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: H1Hack27Feb2017, sfi-image-nochange
locale: en-us
document_id: 15003cb9-37ea-2c60-8a7b-492d11a17e29
document_version_independent_id: 23951bc8-220b-c0c3-1832-a9ce4f3492e1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sync-service-manager-ui-connectors.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sync-service-manager-ui-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sync-service-manager-ui-connectors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 0d4378ce-4840-b0e4-d0cb-40360016e2a0
---

# Connectors in the Microsoft Entra Connect Sync Service Manager UI' - Microsoft Entra ID | Microsoft Learn

![Screenshot that shows the Microsoft Entra Connect Sync Service Manager.](media/how-to-connect-sync-service-manager-ui-connectors/connectors.png)

The Connectors tab is used to manage all systems the sync engine is connected to.

## Connector actions

| Action | Comment |
| --- | --- |
| Create | Not supported. For connecting additional AD forests, use the configuration wizard. |
| Properties | Read-only. Connector properties for connectivity, domain and OU filtering and attribute selection and anchors. |
| Delete  (connector or connector space) | Not supported. For removing AD forests, reinstall the Microsoft Entra Connect product. |
| Configure Run Profiles | Read-only. Connector run profiles. |
| Run | Starts a one-off connector run profile. |
| Stop | Stops a connector run profile. |
| Export Connector | Read-only. Exports the connector configuration. |
| Import Connector | Not supported. |
| Update Connector | Not supported. |
| Refresh Schema | Not supported. Use the "Refresh directory schema" task in the configuration wizard which also updates sync rules. |
| Search Connector Space | Finds objects and shows object data across the Metaverse and other connected sources. |

Warning

Deleting a connector or connector space is **not supported** and can have serious consequences for your hybrid identity environment. Don't use these actions as a troubleshooting step.

### Configure Run Profiles

This option allows you to see the run profiles configured for a Connector.

![Screenshot that shows the &quot;Configure Run Profiles&quot; window with &quot;Delta Import&quot; selected.](media/how-to-connect-sync-service-manager-ui-connectors/configurerunprofiles.png)

### Search Connector Space

The search connector space action is useful to find objects and troubleshoot data issues.

![Screenshot that shows the &quot;Search Connector Space&quot; window.](media/how-to-connect-sync-service-manager-ui-connectors/cssearch.png)

Start by selecting a **scope**. You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).![Screenshot that shows the &quot;Scope&quot; drop-down menu.](media/how-to-connect-sync-service-manager-ui-connectors/cssearchscope.png) If you, for example, do a Sub-Tree search, you get all objects in one OU.![Screenshot that shows an example of a &quot;Sub-Tree&quot; search.](media/how-to-connect-sync-service-manager-ui-connectors/cssearchsubtree.png) From this grid you can select an object, select **properties**, and [follow it](tshoot-connect-object-not-syncing) from the source connector space, through the metaverse, and to the target connector space.

### Changing the AD DS account password

If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD. You may see the following:

- The import/export step for the AD connector fails with "no-start-credentials" error.
- Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”

To resolve the issue, update the AD DS user account using the following:

1. Start the Synchronization Service Manager (START → Synchronization Service). ![Sync Service Manager](media/how-to-connect-sync-service-manager-ui-connectors/startmenu.png)
2. Go to the **Connectors** tab.
3. Select the AD Connector which is configured to use the AD DS account.
4. Under Actions, select **Properties**.
5. In the pop-up dialog, select Connect to Active Directory Forest:
6. The Forest name indicates the corresponding on premises AD.
7. The User name indicates the AD DS account used for synchronization.
8. Enter the new password of the AD DS account in the Password textbox ![Microsoft Entra Connect Sync Encryption Key Utility](media/how-to-connect-sync-service-manager-ui-connectors/key6.png)
9. Select OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.