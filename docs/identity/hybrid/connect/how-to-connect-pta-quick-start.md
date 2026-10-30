---
layout: Conceptual
title: Microsoft Entra pass-through authentication - Quickstart - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta-quick-start
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes how to get started with Microsoft Entra pass-through authentication.
keywords: Azure AD Connect Pass-through Authentication, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-09-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 368a128e-0809-a15a-40e7-8682081bba5b
document_version_independent_id: e395f83d-56b3-87cb-5a83-0790a36368ca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-pta-quick-start.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-pta-quick-start
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-pta-quick-start.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0e136136-ee2e-15a6-bd81-1e4e9023b1a9
---

# Microsoft Entra pass-through authentication - Quickstart - Microsoft Entra ID | Microsoft Learn

## Deploy Microsoft Entra pass-through authentication

Microsoft Entra pass-through authentication allows your users to sign in to both on-premises and cloud-based applications by using the same passwords. Pass-through Authentication signs users in by validating their passwords directly against on-premises Active Directory.

Important

If you're migrating from AD FS (or other federation technologies) to Pass-through Authentication, view [Resources for migrating applications to Microsoft Entra ID](../../enterprise-apps/migration-resources).

Note

If you're deploying Pass Through Authentication with the Azure Government cloud, view [Hybrid Identity Considerations for Azure Government](reference-connect-government-cloud).

Follow these instructions to deploy Pass-through Authentication on your tenant:

## Step 1: Check the prerequisites

Ensure that the following prerequisites are in place.

Important

From a security standpoint, administrators should treat the server running the PTA agent as if it were a domain controller. The PTA agent servers should be hardened along the same lines as outlined in [Securing Domain Controllers Against Attack](/en-us/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack)

### In the Microsoft Entra admin center

1. Create a cloud-only Hybrid Identity Administrator account or a Hybrid Identity Administrator account on your Microsoft Entra tenant. This way, you can manage the configuration of your tenant should your on-premises services fail or become unavailable. Learn about [adding a cloud-only Hybrid Identity Administrator account](../../../fundamentals/how-to-create-delete-users). Completing this step is critical to ensure that you don't get locked out of your tenant.
2. Add one or more [custom domain names](../../../fundamentals/add-custom-domain) to your Microsoft Entra tenant. Your users can sign in with one of these domain names.

### In your on-premises environment

1. Identify a server that runs Windows Server 2025, Windows Server 2022, Windows Server 2019, or Windows Server 2016 to run Microsoft Entra Connect. If not enabled already, [enable TLS 1.2 on the server](how-to-connect-install-prerequisites#enable-tls-12-for-azure-ad-connect). Add the server to the same Active Directory forest as the users whose passwords you need to validate. It should be noted that installation of Pass-Through Authentication agent on Windows Server Core versions isn't supported.
2. Install the [latest version of Microsoft Entra Connect](https://www.microsoft.com/download/details.aspx?id=47594) on the server identified in the preceding step. If you already have Microsoft Entra Connect running, ensure that the version is supported.

    Note

    Microsoft Entra Connect versions 1.1.557.0, 1.1.558.0, 1.1.561.0, and 1.1.614.0 have a problem related to password hash synchronization. If you *don't* intend to use password hash synchronization in conjunction with Pass-through Authentication, read the [Microsoft Entra Connect release notes](reference-connect-version-history).
3. Identify another server that runs Windows Server 2025, Windows Server 2022, Windows Server 2019, or Windows Server 2016 with TLS 1.2 enabled where you can run standalone Authentication Agents. These additional servers are needed to ensure the high availability of requests to sign in. Add the servers to the same Active Directory forest as the users whose passwords you need to validate.

    Important

    In production environments, we recommend that you have a minimum of 3 Authentication Agents running on your tenant. There's a system limit of 40 Authentication Agents per tenant. And as best practice, treat all servers running Authentication Agents as Tier 0 systems (see [reference](/en-us/windows-server/identity/securing-privileged-access/securing-privileged-access-reference-material)).
4. If there's a firewall between your servers and Microsoft Entra ID, configure the following items:

    - Ensure that Authentication Agents can make *outbound* requests to Microsoft Entra ID over the following ports:

        | Port number | How it's used |
        | --- | --- |
        | **80** | Downloads the certificate revocation lists (CRLs) while validating the TLS/SSL certificate |
        | **443** | Handles all outbound communication with the service |
        | **8080** (optional) | Authentication Agents report their status every 10 minutes over port 8080, if port 443 is unavailable. This status is displayed on the [Microsoft Entra admin center](https://entra.microsoft.com). Port 8080 is *not* used for user sign-ins. |

        If your firewall enforces rules according to the originating users, open these ports for traffic from Windows services that run as a network service.
    - If your firewall or proxy lets you add DNS entries to an allowlist, add connections to **\*.msappproxy.net** and **\*.servicebus.windows.net**. If not, allow access to the [Azure datacenter IP ranges](https://www.microsoft.com/en-us/download/details.aspx?id=56519), which are updated weekly.
    - Avoid all forms of inline inspection and Termination on outbound TLS communications between Azure Passthrough Agent and Azure Endpoint.
    - If you have an outgoing HTTP proxy, make sure this URL, autologon.microsoftazuread-sso.com, is on the allowed list. You should specify this URL explicitly since wildcard may not be accepted.
    - Your Authentication Agents need access to **login.windows.net** and **login.microsoftonline.com** for initial registration. Open your firewall for those URLs as well.
    - For certificate validation, unblock the following URLs: **crl3.digicert.com:80**, **crl4.digicert.com:80**, **ocsp.digicert.com:80**, **www.d-trust.net:80**, **root-c3-ca2-2009.ocsp.d-trust.net:80**, **crl.microsoft.com:80**, **oneocsp.microsoft.com:80**, and **ocsp.msocsp.com:80**. Since these URLs are used for certificate validation with other Microsoft products, you may already have these URLs unblocked.

### Azure Government cloud prerequisite

Prior to enabling Pass-through Authentication through Microsoft Entra Connect with Step 2, download the latest release of the PTA agent from the [Microsoft Entra admin center](https://entra.microsoft.com). You need to ensure that your agent is versions **1.5.1742.0.** or later. To verify your agent see [Upgrade authentication agents](how-to-connect-pta-upgrade-preview-authentication-agents)

After downloading the latest release of the agent, proceed with the below instructions to configure Pass-Through Authentication through Microsoft Entra Connect.

## Step 2: Enable the feature

Enable Pass-through Authentication through [Microsoft Entra Connect](../whatis-hybrid-identity).

Important

You can enable Pass-through Authentication on the Microsoft Entra Connect primary or staging server. It's highly recommended that you enable it from the primary server. If you're setting up a Microsoft Entra Connect staging server in the future, you **must** continue to choose Pass-through Authentication as the sign-in option; choosing another option will **disable** Pass-through Authentication on the tenant and override the setting in the primary server.

If you're installing Microsoft Entra Connect for the first time, choose the [custom installation path](how-to-connect-install-custom). At the **User sign-in** page, choose **Pass-through Authentication** as the **Sign On method**. On successful completion, a Pass-through Authentication Agent is installed on the same server as Microsoft Entra Connect. In addition, the Pass-through Authentication feature is enabled on your tenant.

![Microsoft Entra Connect: User sign-in](media/how-to-connect-pta-quick-start/sso3.png)

If you have already installed Microsoft Entra Connect by using the [express installation](how-to-connect-install-express) or the [custom installation](how-to-connect-install-custom) path, select the **Change user sign-in** task on Microsoft Entra Connect, and then select **Next**. Then select **Pass-through Authentication** as the sign-in method. On successful completion, a Pass-through Authentication Agent is installed on the same server as Microsoft Entra Connect and the feature is enabled on your tenant.

![Microsoft Entra Connect: Change user sign-in](media/how-to-connect-pta-quick-start/changeusersignin.png)

Important

Pass-through Authentication is a tenant-level feature. Turning it on affects the sign-in for users across *all* the managed domains in your tenant. If you're switching from Active Directory Federation Services (AD FS) to Pass-through Authentication, you should wait at least 12 hours before shutting down your AD FS infrastructure. This wait time is to ensure that users can keep signing in to Exchange ActiveSync during the transition. For more help on migrating from AD FS to Pass-through Authentication, check out our deployment plans published [here](../../enterprise-apps/migration-resources).

## Step 3: Test the feature

Follow these instructions to verify that you have enabled Pass-through Authentication correctly:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the Hybrid Identity Administrator credentials for your tenant.
2. Select **Microsoft Entra ID**.
3. Select **Microsoft Entra Connect**.
4. Verify that the **Pass-through authentication** feature appears as **Enabled**.
5. Select **Pass-through authentication**. The **Pass-through authentication** pane lists the servers where your Authentication Agents are installed.

    ![Screenshot shows Microsoft Entra admin center: Microsoft Entra Connect pane.](media/how-to-connect-pta-quick-start/azure-ad-connect-blade.png)

    ![Screenshot shows Microsoft Entra admin center: Pass-through Authentication pane.](media/how-to-connect-pta-quick-start/pta-server-list.png)

At this stage, users from all the managed domains in your tenant can sign in by using Pass-through Authentication. However, users from federated domains continue to sign in by using AD FS or another federation provider that you have previously configured. If you convert a domain from federated to managed, all users from that domain automatically start signing in by using Pass-through Authentication. The Pass-through Authentication feature doesn't affect cloud-only users.

## Step 4: Ensure high availability

If you plan to deploy Pass-through Authentication in a production environment, you should install additional standalone Authentication Agents. Install these Authentication Agent(s) on server(s) *other* than the one running Microsoft Entra Connect. This setup provides you with high availability for user sign-in requests.

Important

In production environments, we recommend that you have a minimum of 3 Authentication Agents running on your tenant. There's a system limit of 40 Authentication Agents per tenant. And as best practice, treat all servers running Authentication Agents as Tier 0 systems (see [reference](/en-us/windows-server/identity/securing-privileged-access/securing-privileged-access-reference-material)).

Installing multiple Pass-through Authentication Agents ensures high availability, but not deterministic load balancing between the Authentication Agents. To determine how many Authentication Agents you need for your tenant, consider the peak and average load of sign-in requests that you expect to see on your tenant. As a benchmark, a single Authentication Agent can handle 300 to 400 authentications per second on a standard 4-core CPU, 16-GB RAM server.

To estimate network traffic, use the following sizing guidance:

- Each request has a payload size of (0.5K + 1K \* num\_of\_agents) bytes, that is, data from Microsoft Entra ID to the Authentication Agent. Here, "num\_of\_agents" indicates the number of Authentication Agents registered on your tenant.
- Each response has a payload size of 1K bytes, that is, data from the Authentication Agent to Microsoft Entra ID.

For most customers, three Authentication Agents in total are sufficient for high availability and capacity. You should install Authentication Agents close to your domain controllers to improve sign-in latency.

To begin, follow these instructions to download the Authentication Agent software:

1. To download the latest version of the Authentication Agent (version 1.5.193.0 or later), sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with your tenant's Hybrid Identity Administrator credentials.
2. Select **Microsoft Entra ID**.
3. Select **Microsoft Entra Connect**, select **Connect Sync** and then **Pass-through authentication**, and next select **Download**.
4. Select the **Accept terms and download** button.

    [![Screenshot shows Microsoft Entra admin center: Download Authentication Agent button.](media/how-to-connect-pta-quick-start/download-agent.png)](media/how-to-connect-pta-quick-start/download-agent.png#lightbox)

Note

You can also directly [download the Authentication Agent software](https://aka.ms/getauthagent). Review and accept the Authentication Agent's [Terms of Service](https://aka.ms/authagenteula)*before* installing it.

There are two ways to deploy a standalone Authentication Agent:

First, you can do it interactively by just running the downloaded Authentication Agent executable and providing your tenant's Hybrid Identity Administrator credentials when prompted.

Second, you can create and run an unattended deployment script. This is useful when you want to deploy multiple Authentication Agents at once, or install Authentication Agents on Windows servers that don't have user interface enabled, or that you can't access with Remote Desktop. Here are the instructions on how to use this approach:

1. Run the following command to install an Authentication Agent: `AADConnectAuthAgentSetup.exe REGISTERCONNECTOR="false" /q`.
2. You can register the Authentication Agent with our service via PowerShell. Create a PowerShell Credentials object `$cred` that contains a Hybrid Identity Administrator username and password for your tenant. Run the following command, replacing `<username>` and `<password>`:

```powershell
$User = "<username>"
$PlainPassword = '<password>'
$SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $User, $SecurePassword
```

1. Go to **C:\Program Files\Microsoft Azure AD Connect Authentication Agent** and run the following script using the `$cred` object that you created:

```powershell
RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft Azure AD Connect Authentication Agent\Modules\" -moduleName "PassthroughAuthPSModule" -Authenticationmode Credentials -Usercredentials $cred -Feature PassthroughAuthentication
```

Important

If an Authentication Agent is installed on a Virtual Machine, you can't clone the Virtual Machine to set up another Authentication Agent. This method is **unsupported**.

## Step 5: Configure Smart Lockout capability

Smart Lockout assists in locking out bad actors who are trying to guess your users’ passwords or using brute-force methods to get in. By configuring Smart Lockout settings in Microsoft Entra ID and / or appropriate lockout settings in on-premises Active Directory, attacks can be filtered out before they reach Active Directory. Read [this article](../../authentication/howto-password-smart-lockout) to learn more on how to configure Smart Lockout settings on your tenant to protect your user accounts.