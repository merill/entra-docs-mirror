---
layout: Conceptual
title: Group Writeback for Microsoft 365 Groups - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-group-writeback-enable
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes how to enable group writeback in Microsoft Entra Connect by using PowerShell and a wizard.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 67966556-c772-3c22-0a6e-2f7b82a5760e
document_version_independent_id: 11b7ae96-925c-27ae-43e7-34a75ac9e90e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-group-writeback-enable.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-group-writeback-enable
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-group-writeback-enable.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 995ccbd1-8133-ca0f-367b-1f1f64862bfb
---

# Group Writeback for Microsoft 365 Groups - Microsoft Entra ID | Microsoft Learn

Important

The preview of Group Writeback v2 in Microsoft Entra Connect Sync is deprecated and no longer supported.

You can use Microsoft Entra Cloud Sync to provision cloud security groups to on-premises Active Directory Domain Services (AD DS).

If you use Group Writeback v2 in Microsoft Entra Connect Sync, you should move your sync client to Microsoft Entra Cloud Sync. To check if you're eligible to move to Microsoft Entra Cloud Sync, use the user synchronization wizard.

If you can't use Microsoft Cloud Sync as recommended by the wizard, you can run Microsoft Entra Cloud Sync side-by-side with Microsoft Entra Connect Sync. In that case, you might run Microsoft Entra Cloud Sync only to provision cloud security groups to on-premises AD DS.

If you provision Microsoft 365 groups to AD DS, you can keep using Group Writeback v1.

Group writeback is a feature that you can use to write cloud groups back to your on-premises Active Directory instance by using Microsoft Entra Connect Sync. Group writeback V2 using Microsoft Entra Connect was deprecated. Group writeback V1 using Microsoft Entra Connect still functions, and you should use it if you're synchronizing Microsoft 365 groups. This version of group writeback is being replaced with [Microsoft Entra Cloud Sync group provisioning to Active Directory](../group-writeback-cloud-sync). The V1 functionality continues to work until Microsoft Entra Cloud Sync supports synchronizing Microsoft 365 groups.

This article provides information and walks you through how to enable group writeback V1.

Important

This article describes how to enable group writeback V1 with Microsoft Entra Connect Sync. Only customers who provision Microsoft 365 groups to Active Directory should use it.

## Prerequisites and information

To enable group writeback, you must have:

- Microsoft Entra Premium licenses for your tenant.
- A hybrid deployment configured between your Exchange on-premises organization and Microsoft 365 and verify that it's functioning correctly.
- A supported version of Exchange installed on-premises.
- Single sign-on configured by using Microsoft Entra Connect.

Consider the following information when you use group writeback V1 with Microsoft Entra Connect Sync:

- Microsoft 365 groups with up to 250,000 members can be written back to on-premises.
- If you don't want to write back all existing Microsoft 365 groups to Active Directory, make changes to group writeback default behavior before you perform the steps in this article to enable the feature. For more information, see Modify Microsoft 365 groups.

## Enable group writeback

To enable group writeback, follow these steps:

1. Open the **Microsoft Entra Connect** wizard, select **Configure**, and then select **Next**.
2. Select **Customize synchronization options** and then select **Next**.
3. On the **Connect to Azure AD** page, enter your credentials. Select **Next**.
4. On the **Optional features** page, verify that the options you previously configured are still selected.
5. Select **Group writeback** and then select **Next**.
6. On the **Group Writeback** page, select an Active Directory organizational unit to store objects that are synced from Microsoft 365 to your on-premises organization. Then select **Next**.
7. To make it easier to find groups being written back from Microsoft Entra ID to Active Directory, select the **Writeback group Distinguished Name with cloud Display Name** option:

    - Default format: `CN=Group_3a5c3221-c465-48c0-95b8-e9305786a271, OU=WritebackContainer, DC=domain, DC=com`
    - New format: `CN=Administrators_e9305786a271, OU=WritebackContainer, DC=domain, DC=com`

    When you configure group writeback, a checkbox appears at the bottom of the configuration window. Select it to enable this feature.

    Groups that are written back from Microsoft Entra ID to Active Directory have a source of authority in the cloud. Any changes made on-premises to groups that are written back from Microsoft Entra ID are overwritten in the next sync cycle.

    [![Screenshot that shows selecting the Writeback group Distinguished Name with cloud Display Name option.](media/how-to-connect-group-writeback/optional-group-writeback-1.png)](media/how-to-connect-group-writeback/optional-group-writeback-1.png#lightbox)
8. On the **Ready to configure** page, select **Configure**.
9. When the wizard is complete, on the **Configuration complete** page, select **Exit**.
10. Open Windows PowerShell as an administrator on the Microsoft Entra Connect server, and run the following commands:

    ```powershell
    $AzureADConnectSWritebackAccountDN = <MSOL_ account DN>
    Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdSyncConfig\AdSyncConfig.psm1"
    
    # To grant the <MSOL_account> permission to all domains in the forest:
    Set-ADSyncUnifiedGroupWritebackPermissions -ADConnectorAccountDN $AzureADConnectSWritebackAccountDN
    
    # To grant the <MSOL_account> permission to specific OU (eg. the OU chosen to writeback Office 365 Groups to):
    $GroupWritebackOU = <DN of OU where groups are to be written back to>
    Set-ADSyncUnifiedGroupWritebackPermissions -ADConnectorAccountDN $AzureADConnectSWritebackAccountDN -ADObjectDN $GroupWritebackOU
    ```

For more information on how to configure Microsoft 365 groups, see [Configure Microsoft 365 groups with on-premises Exchange hybrid](/en-us/exchange/hybrid-deployment/set-up-microsoft-365-groups#enable-group-writeback-in-azure-ad-connect).

## Disable group writeback

To disable group writeback, follow these steps:

1. Open the **Microsoft Entra Connect** wizard and go to the **Additional tasks** page. Select the **Customize synchronization options** task and select **Next**.
2. On the **Optional features** page, clear the **Group writeback** checkbox. A warning states that you are about to delete groups. Select **Yes**.

    When you disable group writeback, any groups that were previously created with this feature are deleted from your local Active Directory instance on the next sync cycle.

    ![Screenshot that shows the Group writeback checkbox to clear.](media/how-to-connect-group-writeback/group-1.png)
3. Select **Next**.
4. Select **Configure**.

Disabling group writeback sets the `Full Import` and `Full Synchronization` flags to `true` on the Microsoft Entra Connector. The rule changes propagate through on the next sync cycle and delete the groups that were previously written back to Active Directory.

## Modify default behavior for Microsoft 365 groups

The following sections provide guidance on how to modify the default behavior for Microsoft 365 groups.

### Write back Microsoft 365 groups with up to 250,000 members

Because the default synchronization rule that limits the group size is created when group writeback is enabled, you must complete the following steps after you enable group writeback:

1. On your Microsoft Entra Connect server, open a PowerShell prompt as an administrator.
2. Disable the [Microsoft Entra Connect Sync scheduler](how-to-connect-sync-feature-scheduler):

    ```PowerShell
    Set-ADSyncScheduler -SyncCycleEnabled $false 
    ```
3. Open the [Synchronization Rules Editor](how-to-connect-create-custom-sync-rule).
4. Set the direction to **Outbound**.
5. Locate and disable the **Out to AD – Group Writeback Member Limit** synchronization rule.
6. Enable the Microsoft Entra Connect Sync scheduler:

    ```PowerShell
    Set-ADSyncScheduler -SyncCycleEnabled $true 
    ```

Disabling the synchronization rule sets the flag for full synchronization to `true` on the Microsoft Entra Connector. This change causes the rule changes to propagate through on the next sync cycle.