---
layout: FAQ
title: Microsoft Entra Connect Health FAQ - Azure - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/reference-connect-health-faq
summary: >
  <p>This article includes answers to frequently asked questions (FAQs) about Microsoft Entra Connect Health. These FAQs cover questions about how to use the service, which includes the billing model, capabilities, limitations, and support.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: mwongerapk
description: This FAQ answers questions about Microsoft Entra Connect Health. This FAQ covers questions about using the service, including the billing model, capabilities, limitations, and support.
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.subservice: hybrid-connect
ms.tgt_pltfrm: na
ms.custom:
- no-azure-ad-ps-ref
- sfi-ga-nochange
- msecd-doc-authoring-1012
ms.topic: faq
ms.date: 2026-05-15T00:00:00.0000000Z
locale: en-us
document_id: 982a752e-1900-0483-d4d2-1a4f5ba314cf
document_version_independent_id: f45f07cc-d53d-07fc-61f9-21915eda76fd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/reference-connect-health-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/reference-connect-health-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/reference-connect-health-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 334c8b11-853c-1774-3259-3dfca9cd22ad
---

# Microsoft Entra Connect Health FAQ - Azure - Microsoft Entra ID | Microsoft Learn

This article includes answers to frequently asked questions (FAQs) about Microsoft Entra Connect Health. These FAQs cover questions about how to use the service, which includes the billing model, capabilities, limitations, and support.

## General questions

### I manage multiple Microsoft Entra directories. How do I switch to the one that has Microsoft Entra ID P1 or P2?

To switch between different Microsoft Entra tenants, select the currently signed-in **User Name** on the upper-right corner, and then choose the appropriate account. If the account isn't listed here, select **Sign out.** Next, use the Global Administrator credentials of the directory that has Microsoft Entra ID P1 or P2 (P1 or P2) enabled to sign in.

### What version of identity roles are supported by Microsoft Entra Connect Health?

The following table lists the roles and supported operating system versions.

| Role | Operating system / Version |
| --- | --- |
| Active Directory Federation Services (AD FS) | Windows Server 2016, 2019, 2022, or 2025 |
| Microsoft Entra Connect | [Version 2.5.79.0 or higher](reference-connect-version-history) |
| Active Directory Domain Services (AD DS) | Windows Server 2016, 2019, 2022, or 2025 |

Windows Server Core installations aren't supported.

The features provided by the service may differ based on the role and the operating system. All of the features may not be available, for all operating system versions. See the feature descriptions for details.

### How many licenses do I need to monitor my infrastructure?

- The first Connect Health Agent requires at least one Microsoft Entra P1 or P2 license.
- Each additional registered agent requires 25 more Microsoft Entra P1 or P2 licenses.
- Agent count is equivalent to the total number of agents that are registered across all monitored roles (AD FS, Microsoft Entra Connect, and/or AD DS).
- Microsoft Entra Connect Health licensing doesn't require you to assign the license to specific users. You only need the requisite number of valid licenses.

Licensing information is also found on the [Microsoft Entra pricing page](https://aka.ms/aadpricing).

Example:

| Registered agents | Licenses needed | Example monitoring configuration |
| --- | --- | --- |
| 1 | 1 | 1 Microsoft Entra Connect server |
| 2 | 26 | 1 Microsoft Entra Connect server and 1 domain controller |
| 3 | 51 | 1 Active Directory Federation Services (AD FS) server, 1 AD FS proxy, and 1 domain controller |
| 4 | 76 | 1 AD FS server, 1 AD FS proxy, and 2 domain controllers |
| 5 | 101 | 1 Microsoft Entra Connect server, 1 AD FS server, 1 AD FS proxy, and 2 domain controllers |

## Installation questions

### Does my agent installation get updated automatically when there's a new version of the agent?

Yes, all agents are updated automatically when there's a new version of the agent.

### Can I opt out or disable automatic upgrade of the agent?

No, automatic upgrade is mandatory. If you don't want the agent to be upgraded when a new version is released, you should uninstall the agent.

### What is the impact of installing the Microsoft Entra Connect Health Agent on individual servers?

The impact of installing the Microsoft Entra Connect Health Agent, AD FS, web application proxy servers, Microsoft Entra Connect (sync) servers, and domain controllers is minimal with respect to the CPU, memory consumption, network bandwidth, and storage.

The following numbers are an approximation:

- CPU consumption: ~1-5% increase.
- Memory consumption: Up to 10 % of the total system memory.

Note

If the agent can't communicate with Azure, the agent stores the data locally for a defined maximum limit. The agent overwrites the “cached” data on a “least recently serviced” basis.

- Local buffer storage for Microsoft Entra Connect Health Agents: ~20 MB.
- For AD FS servers, we recommend that you provision a disk space of 1,024 MB (1 GB) for the AD FS audit channel for Microsoft Entra Connect Health Agents to process all the audit data before it's overwritten.

### Will I have to reboot my servers during the installation of the Microsoft Entra Connect Health Agents?

No. The installation of the agents won't require you to reboot the server. However, installation of some prerequisite steps might require a reboot of the server.

For example, installation of .NET 4.6.2 Framework may require a server reboot.

### Does Microsoft Entra Connect Health work through a pass-through HTTP proxy?

Yes. For ongoing operations, you can configure the Health Agent to use an HTTP proxy to forward outbound HTTP requests. Read more about [configuring HTTP Proxy for Health Agents](how-to-connect-health-agent-install#configure-azure-ad-connect-health-agents-to-use-http-proxy).

If you need to configure a proxy during agent registration, you might need to modify your Internet Explorer Proxy settings beforehand.

1. Open Internet Explorer &gt; **Settings** &gt; **Internet Options** &gt; **Connections** &gt; **LAN Settings**.
2. Select **Use a Proxy Server for your LAN**.
3. Select **Advanced** if you have different proxy ports for HTTP and HTTPS/Secure.

### Does Microsoft Entra Connect Health support Basic authentication when connecting to HTTP proxies?

No. A mechanism to specify an arbitrary user name and password for Basic authentication isn't currently supported.

### What firewall ports do I need to open for the Microsoft Entra Connect Health Agent to work?

See the [prerequisites section](how-to-connect-health-agent-install#prerequisites) for the list of firewall ports and other connectivity requirements.

### Why do I see two servers with the same name in the Microsoft Entra Connect Health portal?

When you remove an agent from a server, the server isn't automatically removed from the Microsoft Entra Connect Health portal. If you manually remove an agent from a server or remove the server itself, you need to manually delete the server entry from the Microsoft Entra Connect Health portal. To delete monitored servers from Microsoft Entra Connect Health, you must have either Microsoft Entra Global Administrator account permissions or the Contributor role in Azure role-based access control.

You might reimage a server or create a new server with the same details (such as machine name). If you didn't remove the already registered server from the Microsoft Entra Connect Health portal, and you installed the agent on the new server, you might see two entries with the same name.

In this case, manually delete the entry that belongs to the older server. The data for this server should be out of date.

### Can I install the Microsoft Entra Connect Health agent on Windows Server Core?

No. Installation on Server Core isn't supported.

### After installing Microsoft Entra Connect Sync, with an account that has the Hybrid Administrator role, why is the Connect Health for Sync Agent disabled in services?

In order to install the Connect Health for Sync Agent, you need to be a Global Administrator. To activate the agent, you need to reinstall the agent using a Global Administrator account.

## Health Agent registration and data freshness

### What are common reasons for the Health Agent registration failures and how do I troubleshoot issues?

The health agent can fail to register due to the following possible reasons:

- The agent can't communicate with the required endpoints because a firewall is blocking traffic. This issue is common on web application proxy servers. Make sure that you allowed outbound communication to the required endpoints and ports. See the [prerequisites section](how-to-connect-health-agent-install#prerequisites) for details.
- Outbound communication is subjected to a TLS inspection by the network layer. This causes the certificate that the agent uses to be replaced by the inspection server/entity, and the steps to complete the agent registration fail.
- The user can't perform the registration of the agent. Global Administrators can by default. You can use [Azure role-based access control (Azure RBAC)](how-to-connect-health-operations#manage-access-with-azure-rbac) to delegate access to other users.

### I'm getting alerted that "Health Service data isn't up to date." How do I troubleshoot the issue?

Microsoft Entra Connect Health generates the alert when it doesn't receive all the data points from the server in the last two hours. [Read more](how-to-connect-health-data-freshness).

## Operations questions

### Do I need to enable auditing on the web application proxy servers?

No, auditing doesn't need to be enabled on the web application proxy servers.

### How do Microsoft Entra Connect Health Alerts get resolved?

Microsoft Entra Connect Health alerts get resolved on a success condition. Microsoft Entra Connect Health Agents detect and report the success conditions to the service periodically. For a few alerts, the suppression is time-based. In other words, if the same error condition isn't observed within 72 hours from alert generation, the alert is automatically resolved.

### I'm getting alerted that "Test Authentication Request (Synthetic Transaction) failed to obtain a token." How do I troubleshoot the issue?

Microsoft Entra Connect Health for AD FS generates this alert when the Health Agent installed on an AD FS server fails to obtain a token as part of a synthetic transaction initiated by the Health Agent. The Health agent uses the local system context and attempts to get a token for a self relying party. This behavior is a catch-all test to ensure that AD FS is in a state of issuing tokens.

Most often this test fails because the Health Agent is unable to resolve the AD FS farm name. This state can happen if the AD FS servers are behind a network load balancers and the request gets initiated from a node that's behind the load balancer (as opposed to a regular client that is in front of the load balancer). This issue can be fixed by updating the "hosts" file located under `C:\Windows\System32\drivers\etc` to include the IP address of the AD FS server or a loopback IP address (`127.0.0.1`) for the AD FS farm name (such as `sts.contoso.com`). Adding the host file short-circuits the network call, thus allowing the Health Agent to get the token.

### I got an email indicating my machines are NOT patched for the recent ransomware attacks. Why did I receive this email?

Microsoft Entra Connect Health service scanned all the machines it monitors to ensure the required patches were installed. The email was sent to the tenant administrators if at least one machine didn't have the critical patches. The following logic was used to make this determination.

1. Find all the hotfixes installed on the machine.
2. Check if at least one of the HotFixes from the defined list is present.
3. If Yes, the machine is protected. If Not, the machine is at risk for the attack.

You can use the following PowerShell script to perform this check manually. It implements the above logic.

```powershell
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks the computer it's run on if any of the listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```

### Why are my AD FS audits not being generated?

Please use the PowerShell cmdlet *Get-AdfsProperties -AuditLevel* to ensure audit logs aren't in disabled state. Read more about [AD FS audit logs](/en-us/windows-server/identity/ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server#auditing-levels-in-ad-fs-for-windows-server-2016). Notice if there are audit settings pushed to the AD FS server, any changes with auditpol.exe are overwritten (event if Application Generated isn't configured). In this case, set the local security policy to log Application Generated failures and success.

### When will the agent certificate be automatically renewed before expiration?

The agent certification is automatically renewed **six months** before its expiration date. If it isn't renewed, ensure the network connection of the agent is stable. Restart the agent services or update to the latest version may also solve the issue.

### Is it safe to remove PKS certificates from servers running the Microsoft Entra Connect Health agent?

Yes. PKS certificates are no longer used by the Microsoft Entra Connect Health agent and are safe to remove.

Legacy versions of the agent installed certificates named after the server they ran on. Current versions of the agent don't use these certificates, but they're left in place after upgrade. Because the certificates remain in the local certificate store, expiry monitoring tools can raise false alerts as they approach their expiration date.

You can safely delete these certificates from the local certificate store on the agent server to stop the false alerts. Removing them doesn't affect the operation of the agent.

## Related links

- [Microsoft Entra Connect Health](whatis-azure-ad-connect)
- [Microsoft Entra Connect Health Agent installation](how-to-connect-health-agent-install)
- [Microsoft Entra Connect Health operations](how-to-connect-health-operations)
- [Using Microsoft Entra Connect Health with AD FS](how-to-connect-health-adfs)
- [Using Microsoft Entra Connect Health for sync](how-to-connect-health-sync)
- [Using Microsoft Entra Connect Health with AD DS](how-to-connect-health-adds)
- [Microsoft Entra Connect Health version history](reference-connect-health-version-history)