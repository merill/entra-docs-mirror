---
layout: Conceptual
title: Install the Microsoft Entra provisioning agent - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-install
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Learn how to install the Microsoft Entra provisioning agent and how to configure it in the Microsoft Entra admin center.
ms.topic: how-to
ms.date: 2025-09-18T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ms.custom: sfi-ga-nochange
locale: en-us
document_id: e4692b48-2a40-3a4f-bd2c-5ccc8efc2f62
document_version_independent_id: e869ea03-68be-9de8-4219-18a4e5e7005e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-install.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-install
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-install.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5c61e4da-6f47-4a0e-572f-7d513ed4ae80
---

# Install the Microsoft Entra provisioning agent - Microsoft Entra ID | Microsoft Learn

This article walks you through the installation process for the Microsoft Entra provisioning agent and how to initially configure it in the Microsoft Entra admin center.

Important

The following installation instructions assume that you've met all the [prerequisites](how-to-prerequisites).

Note

This article deals with installing the provisioning agent by using the wizard. For information about installing the Microsoft Entra provisioning agent by using a CLI, see [Install the Microsoft Entra provisioning agent by using a CLI and PowerShell](how-to-install-pshell).

For more information and an example, view the following video:

## Group Managed Service Accounts

A group Managed Service Account (gMSA) is a managed domain account that provides automatic password management, simplified service principal name (SPN) management, and the ability to delegate the management to other administrators. A gMSA also extends this functionality over multiple servers. Microsoft Entra Cloud Sync supports and recommends the use of a gMSA for running the agent. For more information, see [Group Managed Service Accounts](how-to-prerequisites#group-managed-service-accounts).

### Update an existing agent to use the gMSA

To update an existing agent to use the Group Managed Service Account created during installation, upgrade the agent service to the latest version by running *AADConnectProvisioningAgent.msi*. Now run through the installation wizard again and provide the credentials to create the account when you're prompted to do so.

## Install the agent

Note

By default, the Microsoft Entra provisioning agent is installed in the default Azure environment.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. On the left pane, select **Entra Connect**, and then select **Cloud Sync**.

    [![Screenshot that shows the Get started screen.](../../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png)](../../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png#lightbox)
3. On the left pane, select **Agents**.
4. Select **Download on-premises agent**, and then select **Accept terms & download**.

    [![Screenshot that shows downloading the agent.](../../../includes/media/entra-cloud-sync-how-to-install/new-ux-2.png)](../../../includes/media/entra-cloud-sync-how-to-install/new-ux-2.png#lightbox)
5. After you download the Microsoft Entra Connect Provisioning Agent Package, run the *AADConnectProvisioningAgentSetup.exe* installation file from your downloads folder.
6. On the screen that opens, select the **I agree to the license terms and conditions** checkbox, and then select **Install**.

    [![Screenshot that shows the Microsoft Entra Provisioning Agent Package licensing terms.](../../../includes/media/entra-cloud-sync-how-to-install/agree-license-terms.png)](../../../includes/media/entra-cloud-sync-how-to-install/agree-license-terms.png#lightbox)
7. After the installation finishes, the configuration wizard opens. Select **Next** to start the configuration.

    [![Screenshot that shows the welcome screen.](../../../includes/media/entra-cloud-sync-how-to-install/welcome.png)](../../../includes/media/entra-cloud-sync-how-to-install/welcome.png#lightbox)
8. Sign in with an account with at least the [Hybrid Identity administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator) role. If you have Internet Explorer enhanced security enabled, it blocks the sign-in. If so, close the installation, [disable Internet Explorer enhanced security](/en-us/troubleshoot/developer/browsers/security-privacy/enhanced-security-configuration-faq), and restart the Microsoft Entra Provisioning Agent Package installation.

    [![Screenshot that shows the Connect Microsoft Entra ID screen.](../../../includes/media/entra-cloud-sync-how-to-install/username.png)](../../../includes/media/entra-cloud-sync-how-to-install/username.png#lightbox)
9. On the **Configure Service Account** screen, select a group Managed Service Account (gMSA). This account is used to run the agent service. If a managed service account is already configured in your domain by another agent and you're installing a second agent, select **Create gMSA**. The system detects the existing account and adds the required permissions for the new agent to use the gMSA account. When you're prompted, choose one of two options:

    - **Create gMSA**: Let the agent create the **provAgentgMSA$** managed service account for you. The group managed service account (for example, `CONTOSO\provAgentgMSA$`) is created in the same Active Directory domain where the host server joined. To use this option, enter the Active Directory domain administrator credentials (recommended).
    - **Use custom gMSA**: Provide the name of the managed service account that you manually created for this task.

    [![Screenshot that shows how to configure the group Managed Service Account.](../../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configure-service-account.png)](../../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configure-service-account.png#lightbox)
10. To continue, select **Next**.
11. On the **Connect Active Directory** screen, if your domain name appears under **Configured domains**, skip to the next step. Otherwise, enter your Active Directory domain name, and select **Add directory**.

    [![Screenshot that shows configured domains.](../../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configured-domains.png)](../../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configured-domains.png#lightbox)
12. Sign in with your Active Directory domain administrator account. The domain administrator account shouldn't have an expired password. If the password is expired or changes during the agent installation, reconfigure the agent with the new credentials. This operation adds your on-premises directory. Select **OK**, and then select **Next** to continue.
13. Select **Next** to continue.
14. On the **Configuration complete** screen, select **Confirm**. This operation registers and restarts the agent.

    [![Screenshot that shows the finish screen.](../../../includes/media/entra-cloud-sync-how-to-install/finish.png)](../../../includes/media/entra-cloud-sync-how-to-install/finish.png#lightbox)
15. After the operation finishes, you see a notification that your agent configuration was successfully verified. Select **Exit**. If you still get the initial screen, select **Close**.

## Verify the agent installation

Agent verification occurs in the Azure portal and on the local server that runs the agent.

### Verify the agent in the Azure portal

To verify that Microsoft Entra ID registers the agent, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Select **Entra Connect**, and then select **Cloud Sync**.

    [![Screenshot that shows the Get started screen.](../../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png)](../../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png#lightbox)
3. On the **Cloud Sync** page, click **Agents** to see the agents that you installed. Verify that the agent appears and that the status is **active**.

### Verify the agent on the local server

To verify that the agent is running, follow these steps:

1. Sign in to the server with an administrator account.
2. Go to **Services**. You can also use *Start/Run/Services.msc* to get to it.
3. Under **Services**, make sure that **Microsoft Azure AD Connect Agent Updater** and **Microsoft Azure AD Connect Provisioning Agent** are present and that the status is **Running**.

    [![Screenshot that shows the Windows services.](../../../includes/media/entra-cloud-sync-how-to-verify-installation/windows-services.png)](../../../includes/media/entra-cloud-sync-how-to-verify-installation/windows-services.png#lightbox)

### Verify the provisioning agent version

To verify the version of the agent that's running, follow these steps:

1. Go to *C:\Program Files\Microsoft Azure AD Connect Provisioning Agent*.
2. Right-click *AADConnectProvisioningAgent.exe* and select **Properties**.
3. Select the **Details** tab. The version number appears next to the product version.

Important

After you've installed the agent, you must configure and enable it before it will start synchronizing users. To configure a new agent, see [Create a new configuration for Microsoft Entra Cloud Sync](how-to-configure).

## Enable password writeback in cloud sync

You can enable password writeback in SSPR directly in the portal or through PowerShell.

### Enable password writeback in the portal

To use *password writeback* and enable the self-service password reset (SSPR) service to detect the cloud sync agent, using the portal, complete the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Password reset** &gt; **On-premises integration**.
3. Check the option for **Enable password write back for synced users** .
4. (optional) If Microsoft Entra Connect provisioning agents are detected, you can additionally check the option for **Write back passwords with Microsoft Entra Cloud Sync**.
5. Check the option for **Allow users to unlock accounts without resetting their password** to *Yes*.
6. When ready, select **Save**.

### Using PowerShell

To use *password writeback* and enable the self-service password reset (SSPR) service to detect the cloud sync agent, use the `Set-AADCloudSyncPasswordWritebackConfiguration` cmdlet and the tenant’s Global Administrator credentials:

```
 Import-Module "C:\\Program Files\\Microsoft Azure AD Connect Provisioning Agent\\Microsoft.CloudSync.Powershell.dll" 
 Set-AADCloudSyncPasswordWritebackConfiguration -Enable $true -Credential $(Get-Credential)
```

For more information about using password writeback with Microsoft Entra Cloud Sync, see [Tutorial: Enable cloud sync self-service password reset writeback to an on-premises environment](../../authentication/tutorial-enable-cloud-sync-sspr-writeback).

## Password hash synchronization and FIPS with cloud sync

If your server has been locked down according to the Federal Information Processing Standard (FIPS), MD5 (message-digest algorithm 5) is disabled.

To enable MD5 for password hash synchronization, do the following:

1. Go to %programfiles%\Microsoft Azure AD Connect Provisioning Agent.
2. Open *AADConnectProvisioningAgent.exe.config*.
3. Go to the configuration/runtime node at the top of the file.
4. Add the `<enforceFIPSPolicy enabled="false"/>` node.
5. Save your changes.

For reference, your code should look like the following snippet:

```xml
<configuration>
   <runtime>
      <enforceFIPSPolicy enabled="false"/>
   </runtime>
</configuration>
```

For information about security and FIPS, see [Microsoft Entra password hash sync, encryption, and FIPS compliance](https://techcommunity.microsoft.com/t5/microsoft-entra-azure-ad-blog/aad-password-sync-encryption-and-fips-compliance/ba-p/243709).