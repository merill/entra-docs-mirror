---
layout: Conceptual
title: Enable Microsoft Entra Password Writeback - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-enable-sspr-writeback
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: In this tutorial, you learn how to enable Microsoft Entra self-service password reset writeback using Microsoft Entra Connect to synchronize changes back to an on-premises Active Directory Domain Services environment.
ms.topic: tutorial
ms.date: 2026-05-27T00:00:00.0000000Z
ms.reviewer: tilarso
ms.custom: msecd-doc-authoring-106
adobe-target: true
locale: en-us
document_id: 115ae83a-95dd-5643-bc88-f5447ebb2b99
document_version_independent_id: 7462ce84-0a9f-4bfd-7eba-c00928d77865
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/tutorial-enable-sspr-writeback.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/tutorial-enable-sspr-writeback
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/tutorial-enable-sspr-writeback.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7540c817-89a9-d5f5-47ca-4efa303c6da2
---

# Enable Microsoft Entra Password Writeback - Microsoft Entra ID | Microsoft Learn

With Microsoft Entra self-service password reset (SSPR), users can update their passwords or unlock their accounts using a web browser. We recommend this video on [How to enable and configure SSPR in Entra ID](https://www.youtube.com/watch?v=rA8TvhNcCvQ). In a hybrid environment where Microsoft Entra ID is connected to an on-premises Active Directory Domain Services (AD DS) environment, passwords can be different between the two directories.

You can use password writeback to synchronize password changes in Microsoft Entra back to your on-premises AD DS environment. Microsoft Entra Connect provides a secure mechanism to send these password changes back to an existing on-premises directory from Microsoft Entra ID.

Important

This tutorial shows administrators how to enable self-service password reset back to an on-premises environment. If you're an end user already registered for self-service password reset and need to get back into your account, go to https://aka.ms/sspr.

If your IT team hasn't enabled the ability to reset your own password, reach out to your helpdesk for additional assistance.

In this tutorial, you learn how to:

- Configure the required permissions for password writeback
- Enable the password writeback option in Microsoft Entra Connect
- Enable password writeback in Microsoft Entra SSPR

## Prerequisites

To complete this tutorial, you need the following resources and privileges:

- A working Microsoft Entra tenant with at least a Microsoft Entra ID P1 or trial license enabled.
    - If needed, [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - For more information, see [Licensing requirements for Microsoft Entra SSPR](concept-sspr-licensing).
- An account with [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
- Microsoft Entra ID configured for self-service password reset.
    - If needed, [complete the previous tutorial to enable Microsoft Entra SSPR](tutorial-enable-sspr).
- An existing on-premises AD DS environment configured with a current version of Microsoft Entra Connect.
    - If needed, configure Microsoft Entra Connect using the [Express](../hybrid/connect/how-to-connect-install-express) or [Custom](../hybrid/connect/how-to-connect-install-custom) settings.
    - To use password writeback, domain controllers can run any supported version of Windows Server.

## Configure account permissions for Microsoft Entra Connect

Microsoft Entra Connect lets you synchronize users, groups, and credential between an on-premises AD DS environment and Microsoft Entra ID. You typically install Microsoft Entra Connect on a Windows Server 2016 or later computer that's joined to the on-premises AD DS domain.

To correctly work with SSPR writeback, the account specified in Microsoft Entra Connect must have the appropriate permissions and options set. If you're not sure which account is currently in use, open Microsoft Entra Connect and select the **View current configuration** option. The account to which you need to add permissions is listed under **Synchronized Directories**. The following permissions and options must be set on the account:

- **Reset password**
- **Change password**
- **Write permissions** on `lockoutTime`
- **Write permissions** on `pwdLastSet`
- **Extended rights** for **Unexpire Password** on the root object of *each domain* in that forest, if not already set.

If you don't assign these permissions, writeback might appear to be configured correctly, but users encounter errors when they manage their on-premises passwords from the cloud. When setting **Unexpire Password** permissions in Active Directory, you must apply it to **This object and all descendant objects**, **This object only**, or **All descendant objects**; otherwise, the **Unexpire Password** permission isn't displayed.

Tip

If passwords for some user accounts aren't written back to the on-premises directory, make sure that inheritance isn't disabled for the account in the on-prem AD DS environment. Write permissions for passwords must be applied to descendant objects for the feature to work correctly.

To set up the appropriate permissions for password writeback to occur, complete the following steps:

1. In your on-premises AD DS environment, open **Active Directory Users and Computers** with an account that has the appropriate domain administrator permissions.
2. From the **View** menu, make sure that **Advanced features** are turned on.
3. In the left panel, right-click the object that represents the root of the domain and select **Properties** &gt; **Security** &gt; **Advanced**.
4. From the **Permissions** tab, select **Add**.
5. For **Principal**, select the account that permissions should be applied to (the account Microsoft Entra Connect uses).
6. In the **Applies to** drop-down list, select **Descendant User objects**.
7. Under **Permissions**, select the box for **Reset password**.
8. Under **Properties**, select the boxes for the following options. Scroll through the list to find these options, which might already be set by default:

- **Write lockoutTime**
- **Write pwdLastSet**

    [![Set the appropriate permissions in Active Users and Computers for the account that Microsoft Entra Connect uses.](media/tutorial-enable-sspr-writeback/set-ad-ds-permissions-cropped.png)](media/tutorial-enable-sspr-writeback/set-ad-ds-permissions.png#lightbox)

1. When ready, select **Apply / OK** to apply the changes.
2. From the **Permissions** tab, select **Add**.
3. For **Principal**, select the account that permissions should be applied to (the account Microsoft Entra Connect uses).
4. In the **Applies to** drop-down list, select **This object and all descendant objects**
5. Under **Permissions**, select the box for the following option:
    - **Unexpire Password**
6. When ready, select **Apply / OK** to apply the changes and exit any open dialog boxes.

When you update permissions, it might take up to an hour or more for these permissions to replicate to all the objects in your directory.

Password policies in the on-premises AD DS environment may prevent password resets from being correctly processed. For password writeback to work most efficiently, the group policy for **Minimum password age** must be set to **0**. You can find this setting under **Computer Configuration &gt; Policies &gt; Windows Settings &gt; Security Settings &gt; Account Policies** within `gpmc.msc`.

If you update the group policy, wait for the updated policy to replicate or use the `gpupdate /force` command.

Note

If you need to allow users to change or reset passwords more than once per day, you must set **Minimum password age** to **0**. Password writeback will work after on-premises password policies are successfully evaluated.

## Enable password writeback in Microsoft Entra Connect

One of the configuration options in Microsoft Entra Connect is for password writeback. When this option is enabled, password change events cause Microsoft Entra Connect to synchronize the updated credentials back to the on-premises AD DS environment.

To enable SSPR writeback, first enable the writeback option in Microsoft Entra Connect. From your Microsoft Entra Connect server, complete the following steps:

1. Sign in to your Microsoft Entra Connect server and start the **Microsoft Entra Connect** configuration wizard.
2. On the **Welcome** page, select **Configure**.
3. On the **Additional tasks** page, select **Customize synchronization options**, then select **Next**.
4. On the **Connect to Microsoft Entra ID** page, enter a Hybrid Administrator credential for your Azure tenant, then select **Next**.
5. On the **Connect directories** and **Domain/OU** filtering pages, select **Next**.
6. On the **Optional features** page, select the box next to **Password writeback** and select **Next**.
7. On the **Directory extensions** page, select **Next**.
8. On the **Ready to configure** page, select **Configure** and wait for the process to finish.
9. When you see the configuration finish, select **Exit**.

Note

Updating `PasswordWritebackEnabled` from [OnPremDirectorySynchronization service features](../hybrid/connect/how-to-connect-syncservice-features) isn't supported because this feature flag isn't in use.

## Enable password writeback for SSPR

With password writeback enabled in Microsoft Entra Connect, you can now configure Microsoft Entra SSPR for writeback. You can configure SSPR to writeback through Microsoft Entra Connect Sync agents and Microsoft Entra Connect provisioning agents (cloud sync). When you enable SSPR to use password writeback, users who change or reset their password have that updated password synchronized back to the on-premises AD DS environment as well.

To enable password writeback in SSPR, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Password reset**, then choose **On-premises integration**.
3. Check the option for **Write back passwords to your on-premises directory**.
4. (optional) If Microsoft Entra Connect provisioning agents are detected, you can additionally check the option for **Write back passwords with Microsoft Entra Connect cloud sync**.
5. Set the option for **Allow users to unlock accounts without resetting their password** to **Yes**.
6. When ready, select **Save**.

## Clean up resources

If you no longer want to use the SSPR writeback functionality you have configured as part of this tutorial, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Password reset**, then choose **On-premises integration**.
3. Uncheck the option for **Write back passwords to your on-premises directory**.
4. Uncheck the option for **Write back passwords with Microsoft Entra Connect cloud sync**.
5. Uncheck the option for **Allow users to unlock accounts without resetting their password**.
6. When ready, select **Save**.

If you no longer want to use the Microsoft Entra Connect cloud sync for SSPR writeback functionality but want to continue using Microsoft Entra Connect Sync agent for writebacks complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Password reset**, then choose **On-premises integration**.
3. Uncheck the option for **Write back passwords with Microsoft Entra Connect cloud sync**.
4. When ready, select **Save**.

If you no longer want to use any password functionality, complete the following steps from your Microsoft Entra Connect server:

1. Sign in to your Microsoft Entra Connect server and start the **Microsoft Entra Connect** configuration wizard.
2. On the **Welcome** page, select **Configure**.
3. On the **Additional tasks** page, select **Customize synchronization options**, then select **Next**.
4. On the **Connect to Microsoft Entra ID** page, enter a Hybrid Administrator credential, then select **Next**.
5. On the **Connect directories** and **Domain/OU** filtering pages, select **Next**.
6. On the **Optional features** page, deselect the box next to **Password writeback** and select **Next**.
7. On the **Ready to configure** page, select **Configure** and wait for the process to finish.
8. When you see the configuration finish, select **Exit**.

Important

Enabling password writeback for the first time might trigger password change events 656 and 657, even if a password change hasn't occurred. This is because all password hashes are resynchronized after a password hash synchronization cycle runs.