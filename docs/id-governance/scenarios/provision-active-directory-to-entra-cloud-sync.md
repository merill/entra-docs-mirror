---
layout: Conceptual
title: Govern cloud users and groups with provisioning from on-premises and Entra Connect Cloud Sync | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/scenarios/provision-active-directory-to-entra-cloud-sync
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article a tutorial on how to provision users and groups using cloud sync.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: 
locale: en-us
document_id: a62a77b9-5a16-bf09-4e42-805cb8cf4107
document_version_independent_id: a62a77b9-5a16-bf09-4e42-805cb8cf4107
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/scenarios/provision-active-directory-to-entra-cloud-sync.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/scenarios/provision-active-directory-to-entra-cloud-sync
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/scenarios/provision-active-directory-to-entra-cloud-sync.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: a2b4e8a0-ec1c-7806-7b32-9e0c87de5b77
---

# Govern cloud users and groups with provisioning from on-premises and Entra Connect Cloud Sync | Microsoft Learn

**Scenario:** Manage cloud users and groups that are provisioned from Active Directory using Microsoft Entra cloud sync.

## Prerequisites

### In the Microsoft Entra admin center

- Microsoft recommends that organizations have two cloud-only emergency access accounts permanently assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role. These accounts are highly privileged and aren't assigned to specific individuals. The accounts are limited to emergency or "break glass" scenarios where normal accounts can't be used or all other administrators are accidentally locked out. These accounts should be created following the [emergency access account recommendations](/en-us/entra/identity/role-based-access-control/security-emergency-access).
- Add one or more [custom domain names](../../fundamentals/add-custom-domain) to your Microsoft Entra tenant. Your users can sign in with one of these domain names.

### In your on-premises environment

1. Identify a domain-joined host server running Windows Server 2016 or greater with minimum of 4-GB RAM and .NET 4.7.1+ runtime
2. If there's a firewall between your servers and Microsoft Entra ID, configure the following items:

    - Ensure that agents can make *outbound* requests to Microsoft Entra ID over the following ports:

        | Port number | How it's used |
        | --- | --- |
        | **80** | Downloads the certificate revocation lists (CRLs) while validating the TLS/SSL certificate |
        | **443** | Handles all outbound communication with the service |
        | **8080** (optional) | Agents report their status every 10 minutes over port 8080, if port 443 is unavailable. This status is displayed on the portal. |

        If your firewall enforces rules according to the originating users, open these ports for traffic from Windows services that run as a network service.
    - If your firewall or proxy allows you to specify safe suffixes, then add connections to **\*.msappproxy.net** and **\*.servicebus.windows.net**. If not, allow access to the [Azure datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated weekly.
    - Your agents need access to **login.windows.net** and **login.microsoftonline.com** for initial registration. Open your firewall for those URLs as well.
    - For certificate validation, unblock the following URLs: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80**, and **www.microsoft.com:80**. Since these URLs are used for certificate validation with other Microsoft products, you may already have these URLs unblocked.

## Install the Microsoft Entra provisioning agent

If you're using the [Basic AD and Azure environment](../../identity/hybrid/cloud-sync/tutorial-basic-ad-azure) tutorial, it would be DC1. To install the agent, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../identity/role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. On the left pane, select **Entra Connect**, and then select **Cloud Sync**.

    [![Screenshot that shows the Get started screen.](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png)](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png#lightbox)
3. On the left pane, select **Agents**.
4. Select **Download on-premises agent**, and then select **Accept terms & download**.

    [![Screenshot that shows downloading the agent.](../../includes/media/entra-cloud-sync-how-to-install/new-ux-2.png)](../../includes/media/entra-cloud-sync-how-to-install/new-ux-2.png#lightbox)
5. After you download the Microsoft Entra Connect Provisioning Agent Package, run the *AADConnectProvisioningAgentSetup.exe* installation file from your downloads folder.
6. On the screen that opens, select the **I agree to the license terms and conditions** checkbox, and then select **Install**.

    [![Screenshot that shows the Microsoft Entra Provisioning Agent Package licensing terms.](../../includes/media/entra-cloud-sync-how-to-install/agree-license-terms.png)](../../includes/media/entra-cloud-sync-how-to-install/agree-license-terms.png#lightbox)
7. After the installation finishes, the configuration wizard opens. Select **Next** to start the configuration.

    [![Screenshot that shows the welcome screen.](../../includes/media/entra-cloud-sync-how-to-install/welcome.png)](../../includes/media/entra-cloud-sync-how-to-install/welcome.png#lightbox)
8. Sign in with an account with at least the [Hybrid Identity administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator) role. If you have Internet Explorer enhanced security enabled, it blocks the sign-in. If so, close the installation, [disable Internet Explorer enhanced security](/en-us/troubleshoot/developer/browsers/security-privacy/enhanced-security-configuration-faq), and restart the Microsoft Entra Provisioning Agent Package installation.

    [![Screenshot that shows the Connect Microsoft Entra ID screen.](../../includes/media/entra-cloud-sync-how-to-install/username.png)](../../includes/media/entra-cloud-sync-how-to-install/username.png#lightbox)
9. On the **Configure Service Account** screen, select a group Managed Service Account (gMSA). This account is used to run the agent service. If a managed service account is already configured in your domain by another agent and you're installing a second agent, select **Create gMSA**. The system detects the existing account and adds the required permissions for the new agent to use the gMSA account. When you're prompted, choose one of two options:

    - **Create gMSA**: Let the agent create the **provAgentgMSA$** managed service account for you. The group managed service account (for example, `CONTOSO\provAgentgMSA$`) is created in the same Active Directory domain where the host server joined. To use this option, enter the Active Directory domain administrator credentials (recommended).
    - **Use custom gMSA**: Provide the name of the managed service account that you manually created for this task.

    [![Screenshot that shows how to configure the group Managed Service Account.](../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configure-service-account.png)](../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configure-service-account.png#lightbox)
10. To continue, select **Next**.
11. On the **Connect Active Directory** screen, if your domain name appears under **Configured domains**, skip to the next step. Otherwise, enter your Active Directory domain name, and select **Add directory**.

    [![Screenshot that shows configured domains.](../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configured-domains.png)](../../includes/media/entra-cloud-sync-how-to-install/cloud-sync-configured-domains.png#lightbox)
12. Sign in with your Active Directory domain administrator account. The domain administrator account shouldn't have an expired password. If the password is expired or changes during the agent installation, reconfigure the agent with the new credentials. This operation adds your on-premises directory. Select **OK**, and then select **Next** to continue.
13. Select **Next** to continue.
14. On the **Configuration complete** screen, select **Confirm**. This operation registers and restarts the agent.

    [![Screenshot that shows the finish screen.](../../includes/media/entra-cloud-sync-how-to-install/finish.png)](../../includes/media/entra-cloud-sync-how-to-install/finish.png#lightbox)
15. After the operation finishes, you see a notification that your agent configuration was successfully verified. Select **Exit**. If you still get the initial screen, select **Close**.

## Verify agent installation

Agent verification occurs in the Azure portal and on the local server that runs the agent.

### Verify the agent in the Azure portal

To verify that Microsoft Entra ID registers the agent, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../identity/role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Select **Entra Connect**, and then select **Cloud Sync**.

    [![Screenshot that shows the Get started screen.](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png)](../../includes/media/entra-cloud-sync-how-to-install/new-ux-1.png#lightbox)
3. On the **Cloud Sync** page, click **Agents** to see the agents that you installed. Verify that the agent appears and that the status is **active**.

### Verify the agent on the local server

To verify that the agent is running, follow these steps:

1. Sign in to the server with an administrator account.
2. Go to **Services**. You can also use *Start/Run/Services.msc* to get to it.
3. Under **Services**, make sure that **Microsoft Azure AD Connect Agent Updater** and **Microsoft Azure AD Connect Provisioning Agent** are present and that the status is **Running**.

    [![Screenshot that shows the Windows services.](../../includes/media/entra-cloud-sync-how-to-verify-installation/windows-services.png)](../../includes/media/entra-cloud-sync-how-to-verify-installation/windows-services.png#lightbox)

### Verify the provisioning agent version

To verify the version of the agent that's running, follow these steps:

1. Go to *C:\Program Files\Microsoft Azure AD Connect Provisioning Agent*.
2. Right-click *AADConnectProvisioningAgent.exe* and select **Properties**.
3. Select the **Details** tab. The version number appears next to the product version.

## Configure Microsoft Entra Cloud Sync

Use the following steps to configure and start the provisioning:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../identity/role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot that shows the Microsoft Entra Connect Cloud Sync home page.](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png)](../../includes/media/cloud-sync-sign-in/cloud-sync-configurations.png#lightbox)

1. Select **New configuration** &gt; **AD to Microsoft Entra ID sync**.
2. Choose the domain that you want to sync, and select **Create**.

For more information about how to configure Microsoft Entra Cloud Sync, see [Provision Active Directory to Microsoft Entra ID](/en-us/entra/identity/hybrid/cloud-sync/how-to-configure).

## Verify users are created and synchronization is occurring

You'll now verify that the users that you had in your on-premises directory that are in scope of synchronization have been synchronized and now exist in your Microsoft Entra tenant. The sync operation may take a few hours to complete. To verify users are synchronized, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../identity/role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Verify that you see the new users in your tenant

## Test signing in with one of your users

1. Browse to https://myapps.microsoft.com
2. Sign in with a user account that was created in your tenant. You'll need to sign in using the following format: (user@domain.onmicrosoft.com). Use the same password that the user uses to sign in on-premises.

![Screenshot that shows the my apps portal with a signed in users.](../../includes/governance/media/tutorial-single-forest/verify-1.png)

You've now successfully configured a hybrid identity environment using Microsoft Entra Cloud Sync.