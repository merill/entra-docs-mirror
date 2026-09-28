---
layout: Conceptual
title: Selective Password Hash Synchronization for Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-selective-password-hash-synchronization
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes how to set up and configure selective password hash synchronization to use with Microsoft Entra Connect.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 025a805d-412a-7426-f630-f5a0c963421f
document_version_independent_id: e20df137-677c-458e-50ac-c43a7129ad64
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-selective-password-hash-synchronization.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-selective-password-hash-synchronization
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-selective-password-hash-synchronization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 7ae3eaca-b399-0a8d-5f88-d44647279bf1
---

# Selective Password Hash Synchronization for Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

[Password hash synchronization](whatis-phs) is one of the sign-in methods used to accomplish hybrid identity. Microsoft Entra Connect synchronizes a hash, of the hash, of a user's password from an on-premises Active Directory instance to a cloud-based Microsoft Entra instance. By default, once it's set up, password hash synchronization occurs on all of the users you're synchronizing.

If you want to exclude a subset of users from synchronizing their password hash to Microsoft Entra ID, you can configure selective password hash synchronization using the guided steps in this article.

Important

Microsoft doesn't support modifying or operating Microsoft Entra Connect Sync outside of the configurations or actions that are formally documented. Any of these configurations or actions might result in an inconsistent or unsupported state of Microsoft Entra Connect Sync. As a result, Microsoft cannot guarantee the ability to provide efficient technical support for such deployments.

## Consider your implementation

To reduce the configuration administrative effort, you should first consider the number of user objects you wish to exclude from password hash synchronization. Verify the following scenarios, which are mutually exclusive, aligns with your requirements to select the right configuration option for you.

- If the number of users to **exclude** is **smaller** than the number of users to **include**, follow the steps in this section.
- If the number of users to **exclude** is **greater** than the number of users to **include**, follow the steps in this section.

Important

With either configuration option chosen, a required initial sync (Full Sync) to apply the changes, is performed automatically over the next sync cycle.

Important

Configuring selective password hash synchronization directly influences password writeback. Password changes or password resets that are initiated in Microsoft Entra ID write back to on-premises Active Directory only if the user is in scope for password hash synchronization.

Important

Selective password hash synchronization is supported in Microsoft Entra Connect 1.6.2.4 or later. If you're using a version lower than that, upgrade to the latest version.

### The adminDescription attribute

Both scenarios rely on setting the adminDescription attribute of users to a specific value. This allows the rules to be applied and is what makes selective PHS work.

| Scenario | adminDescription value |
| --- | --- |
| Excluded users is smaller than included users | PHSFiltered |
| Excluded users is larger than included users | PHSIncluded |

This attribute can be set either:

- using the Active Directory Users and Computers UI
- using `Set-ADUser` PowerShell cmdlet. For more information, see [Set-ADUser](/en-us/powershell/module/activedirectory/set-aduser).

### Disable the synchronization scheduler:

Before you start either scenario, you must disable the synchronization scheduler while making changes to the sync rules.

1. Start Windows PowerShell and enter.

    `Set-ADSyncScheduler -SyncCycleEnabled $false`
2. Confirm the scheduler is disabled by running the following cmdlet:

    `Get-ADSyncScheduler`

For more information on the scheduler, see [Microsoft Entra Connect Sync scheduler](how-to-connect-sync-feature-scheduler).

## Excluded users is smaller than included users

The following section describes how to enable selective password hash synchronization when the number of users to **exclude** is **smaller** than the number of users to **include**.

Important

Before you proceed, ensure the synchronization scheduler is disabled as previously described.

- Create an editable copy of the **In from AD – User AccountEnabled** with the option to **enable password hash sync un-selected** and define its scoping filter
- Create another editable copy of the default **In from AD – User AccountEnabled** with the option to **enable password hash sync selected** and define its scoping filter
- Re-enable the synchronization scheduler
- Set the attribute value, in active directory, that was defined as scoping attribute on the users you want to allow in password hash synchronization.

Important

The steps provided to configure selective password hash synchronization only affect user objects that have the attribute **adminDescription** populated in Active Directory with the value of **PHSFiltered**. If this attribute is not populated or the value is something other than **PHSFiltered** then these rules won't be applied to the user objects.

### Configure the necessary synchronization rules:

1. Start the Synchronization Rules Editor and set the filters **Password Sync** to **On** and **Rule Type** to **Standard**. ![Start sync rules editor](media/how-to-connect-selective-password-hash-synchronization/exclude-1.png)
2. Select the rule **In from AD – User AccountEnabled** for the Active Directory forest Connector you want to configure selective password had hash synchronization on and select **Edit**. Select **Yes** in the next dialog box to create an editable copy of the original rule. ![Select rule](media/how-to-connect-selective-password-hash-synchronization/exclude-2.png)
3. The first rule disables password hash sync. Provide the following name to the new custom rule: **In from AD - User AccountEnabled - Filter Users from PHS**. Change the precedence value to a number lower than 100 (for example **90** or whichever is the lowest value available in your environment). Make sure the checkboxes **Enable Password Sync** and **Disabled** are unchecked. Select **Next**. ![Edit inbound](media/how-to-connect-selective-password-hash-synchronization/exclude-3.png)
4. In **Scoping filter**, select **Add clause**. Select **adminDescription** in the attribute column, **EQUAL** in the Operator column and enter **PHSFiltered** as the value. ![Scoping filter](media/how-to-connect-selective-password-hash-synchronization/exclude-4.png)
5. No further changes are required. **Join rules** and **Transformations** should be left with the default copied settings so you can select **Save** now. Select **OK** in the warning dialog box informing a full synchronization to be run on the next synchronization cycle of the connector. ![Save rule](media/how-to-connect-selective-password-hash-synchronization/exclude-5.png)
6. Next, create another custom rule with password hash synchronization enabled. Select again the default rule **In from AD – User AccountEnabled** for the Active Directory forest you want to configure selective password had synchronization on and select **Edit**. Select **yes** in the next dialog box to create an editable copy of the original rule. ![Custom rule](media/how-to-connect-selective-password-hash-synchronization/exclude-6.png)
7. Provide the following name to the new custom rule: **In from AD - User AccountEnabled - Users included for PHS**. Change the precedence value to a number lower than the rule previously created (in this example, that'll be **89**). Make sure the checkbox **Enable Password Sync** is checked and the **Disabled** checkbox is unchecked. Select **Next**.![Edit new rule](media/how-to-connect-selective-password-hash-synchronization/exclude-7.png)
8. In **Scoping filter**, select **Add clause**. Select **adminDescription** in the attribute column, **NOTEQUAL** in the Operator column and enter **PHSFiltered** as the value. ![Scope rule](media/how-to-connect-selective-password-hash-synchronization/exclude-8.png)
9. No further changes are required. **Join rules** and **Transformations** should be left with the default copied settings so you can select **Save** now. Select **OK** in the warning dialog box informing a full synchronization to be run on the next synchronization cycle of the connector. ![Join rules](media/how-to-connect-selective-password-hash-synchronization/exclude-9.png)
10. Confirm the rules creation. Remove the filters **Password Sync** **On** and **Rule Type** **Standard**. And you should see both new rules you just created. ![Confirm rules](media/how-to-connect-selective-password-hash-synchronization/exclude-10.png)

### Re-enable synchronization scheduler:

Once you completed the steps to configure the necessary synchronization rules, re-enable the synchronization scheduler with the following steps:

1. In Windows PowerShell run:

    `set-adsyncscheduler -synccycleenabled:$true`
2. Then confirm it has been successfully enabled by running:

    `get-adsyncscheduler`

For more information on the scheduler, see [Microsoft Entra Connect Sync scheduler](how-to-connect-sync-feature-scheduler).

### Edit users **adminDescription** attribute:

Once all configurations are complete, you need edit the attribute **adminDescription** for all users you wish to **exclude** from password hash synchronization in Active Directory and add the string used in the scoping filter: **PHSFiltered**.

![Edit attribute](media/how-to-connect-selective-password-hash-synchronization/exclude-11.png)

You can also use the following PowerShell command to edit a user's **adminDescription** attribute:

`set-adusermyuser-replace@{adminDescription="PHSFiltered"}`

## Excluded users is larger than included users

The following section describes how to enable selective password hash synchronization when the number of users to **exclude** is **larger** than the number of users to **include**.

Important

Before you proceed ensure the synchronization scheduler is disabled as outlined above.

The following is a summary of the actions to take :

- Create an editable copy of the **In from AD – User AccountEnabled** with the option to **enable password hash sync un-selected** and define its scoping filter
- Create another editable copy of the default **In from AD – User AccountEnabled** with the option to **enable password hash sync selected** and define its scoping filter
- Re-enable the synchronization scheduler
- Set the attribute value, in active directory, that was defined as scoping attribute on the users you want to allow in password hash synchronization.

Important

The steps provided to configure selective password hash synchronization only affect user objects that have the attribute **adminDescription** populated in Active Directory with the value of **PHSIncluded**. If this attribute is not populated or the value is something other than **PHSIncluded** then these rules aren't applied to the user objects.

### Configure the necessary synchronization rules:

1. Start the synchronization Rules Editor and set the filters **Password Sync** **On** and **Rule Type** **Standard**. ![Rule type](media/how-to-connect-selective-password-hash-synchronization/include-1.png)
2. Select the rule **In from AD – User AccountEnabled** for the Active Directory forest you want to configure selective password had synchronization on and select **Edit**. Select **yes** in the next dialog box to create an editable copy of the original rule. ![In from AD](media/how-to-connect-selective-password-hash-synchronization/include-2.png)
3. The first rule disables the password hash sync. Provide the following name to the new custom rule: **In from AD - User AccountEnabled - Filter Users from PHS**. Change the precedence value to a number lower than 100 (for example **90** or whichever is the lowest value available in your environment). Make sure the checkboxes **Enable Password Sync** and **Disabled** are unchecked. Select **Next**. ![Set precedence](media/how-to-connect-selective-password-hash-synchronization/include-3.png)
4. In **Scoping filter**, select **Add clause**. Select **adminDescription** in the attribute column, **NOTEQUAL** in the Operator column and enter **PHSIncluded** as the value. ![Add clause](media/how-to-connect-selective-password-hash-synchronization/include-4.png)
5. No further changes are required. **Join rules** and **Transformations** should be left with the default copied settings so you can select **Save** now. Select **OK** in the warning dialog box informing a full synchronization to be run on the next synchronization cycle of the connector. ![Transformation](media/how-to-connect-selective-password-hash-synchronization/include-5.png)
6. Next, create another custom rule with password hash synchronization enabled. Select again the default rule **In from AD – User AccountEnabled** for the Active Directory forest you want to configure selective password had synchronization on and select **Edit**. Select **yes** in the next dialog box to create an editable copy of the original rule. ![User AccountEnabled](media/how-to-connect-selective-password-hash-synchronization/include-6.png)
7. Provide the following name to the new custom rule: **In from AD - User AccountEnabled - Users included for PHS**. Change the precedence value to a number lower than the rule previously created (in this, example that'll be **89**). Make sure the checkbox **Enable Password Sync** is checked and the **Disabled** checkbox is unchecked. Select **Next**. ![Enable Password Sync](media/how-to-connect-selective-password-hash-synchronization/include-7.png)
8. In **Scoping filter**, select **Add clause**. Select **adminDescription** in the attribute column, **EQUAL** in the Operator column and enter **PHSIncluded** as the value. ![PHSIncluded](media/how-to-connect-selective-password-hash-synchronization/include-8.png)
9. No further changes are required. **Join rules** and **Transformations** should be left with the default copied settings so you can select **Save** now. Select **OK** in the warning dialog box informing a full synchronization to be run on the next synchronization cycle of the connector. ![Save now](media/how-to-connect-selective-password-hash-synchronization/include-9.png)
10. Confirm the rules creation. Remove the filters **Password Sync** **On** and **Rule Type** **Standard**. And you should see both new rules you just created. ![Sync on](media/how-to-connect-selective-password-hash-synchronization/include-10.png)

### Re-enable synchronization scheduler:

Once you completed the steps to configure the necessary synchronization rules, re-enable the synchronization scheduler with the following steps:

1. In Windows PowerShell, run:

    `set-adsyncscheduler-synccycleenabled$true`
2. Then confirm it has been successfully enabled by running:

    `get-adsyncscheduler`

For more information on the scheduler, see [Microsoft Entra Connect Sync scheduler](how-to-connect-sync-feature-scheduler).

### Edit users **adminDescription** attribute:

Once all configurations are complete, you need edit the attribute **adminDescription** for all users you wish to **include** for password hash synchronization in Active Directory and add the string used in the scoping filter: **PHSIncluded**.

![Edit attributes](media/how-to-connect-selective-password-hash-synchronization/include-11.png)

You can also use the following PowerShell command to edit a user's **adminDescription** attribute:

`Set-ADUser myuser -Replace @{adminDescription="PHSIncluded"}`