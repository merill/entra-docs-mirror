---
layout: Conceptual
title: 'Troubleshoot the Global Secure Access Client: Disabled by Your Organization - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-disabled
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: This document provides troubleshooting guidance for the Global Secure Access client when it shows the "disabled by your organization" error message.
ms.topic: troubleshooting
ms.date: 2026-03-23T00:00:00.0000000Z
ms.reviewer: lirazbarak
locale: en-us
document_id: a98fffa7-f06b-a90c-585c-d3a8be870834
document_version_independent_id: a98fffa7-f06b-a90c-585c-d3a8be870834
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-global-secure-access-client-disabled.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-global-secure-access-client-disabled
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-global-secure-access-client-disabled.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: ef819867-98d3-71c4-4cd7-06aa05e795f5
---

# Troubleshoot the Global Secure Access Client: Disabled by Your Organization - Global Secure Access | Microsoft Learn

This document provides troubleshooting guidance for the Global Secure Access client. It explores how to resolve the **Global Secure Access client - disabled by your organization** error message.

| Icon | Message | Description |
| --- | --- | --- |
| ![](media/troubleshoot-global-secure-access-client-disabled/global-secure-access-client-icon-warning.png) | Global Secure Access - disabled by your organization | Your organization disabled the client (that is, all traffic forwarding profiles are disabled). |

The **Global Secure Access client - disabled by your organization** error message appears when the Global Secure Access client is deliberately deactivated by your organization's administrator.![Screenshot of the warning message, Global Secure Access - disabled by your organization.](media/troubleshoot-global-secure-access-client-disabled/warning-message.png)

The warning message also appears when the client receives an empty policy (that is, no traffic forwarding profiles from Microsoft, Private Access, or Internet Access). The empty policy happens in the following cases:

1. All traffic forwarding profiles are disabled in the portal.
2. Some traffic forwarding profiles are enabled, but the user isn't assigned to any of them (in the **User and group assignments** section of each profile).
3. The user didn't sign in to Windows with a Microsoft Entra user.
4. Authentication to get the policy requires user interaction (such as if multifactor authentication (MFA) or terms of use (ToU) are enabled).

In cases **3** and **4**, only traffic profiles that are assigned to the entire tenant (**Assign to all users** in the user and group assignment section is set to **Yes**) take effect. Traffic profiles assigned to specific users and groups aren't applied since the user identity isn't used to get the policy. In these cases, only the device identity is available to the policy service.

To view the Global Secure Access traffic profile configuration:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Navigate to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**.[![Screenshot of the Traffic forwarding profiles screen.](media/troubleshoot-global-secure-access-client-disabled/traffic-forwarding.png)](media/troubleshoot-global-secure-access-client-disabled/traffic-forwarding-expanded.png#lightbox)

## Troubleshooting steps

1. View the available traffic forwarding profiles. At least one traffic forwarding profile must be enabled. Verify that the user is assigned to the enabled traffic forwarding profile. Users in your organization who sign in to Windows with a non-Microsoft Entra ID, such as local user or Active Directory Domain Services (AD DS) user not synced to Microsoft Entra, receive only the traffic forwarding profiles assigned to all users in the tenant. ![Screenshot of the User and group assignments screen with the Assign to all users toggle set to Yes.](media/troubleshoot-global-secure-access-client-disabled/user-group-assignments-yes.png)
2. Ensure that both the device and the user are successfully authenticated to Microsoft Entra and receive a valid token.

    1. Check that the device is joined to Microsoft Entra and signed in to Windows with a Microsoft Entra user.
    2. Run the command `dsregcmd /status` and check the **AzureAdPrt** field.![Screenshot of the command line, showing the AzureAdPrt status of YES.](media/troubleshoot-global-secure-access-client-disabled/token-state.png)
3. Check if a Conditional Access policy is blocking the user. Network blocks can arise from Conditional Access settings, an unmanaged or noncompliant device, or unfulfilled MFA or ToU policies. To confirm that the Global Secure Access Client authenticated successfully to the policy service, check the list of non-interactive user sign-ins.![Screenshot of the Sign-in logs screen, showing the list of non-interactive user sign-ins.](media/troubleshoot-global-secure-access-client-disabled/sign-in-logs.png)

Note

To get the policy, the Global Secure Access client uses a non-interactive, silent authentication.

1. If you assign the traffic forwarding profile to specific users and groups, ensure that users signed in to Windows are either assigned to the profile or are a direct member of an assigned group.![Screenshot of the User and group assignments screen with the Assign to all users toggle set to No.](media/troubleshoot-global-secure-access-client-disabled/user-group-assignments.png)

Note

Traffic profiles are fetched on behalf of the Microsoft Entra user logged into Windows, not the user logged into the client. Multiple users logging into the same device simultaneously isn't supported. Nested group memberships aren't supported. Each user must be a direct member of the group assigned to the profile.

1. Ensure the Global Secure Access client can reach the policy service in the cloud by checking that the **Policy service hostname resolved by DNS** and the **Policy server is reachable** health check tests pass. ![Screenshot of the Advanced diagnostics Health check tab, with Policy service hostname resolved and Policy server is reachable tests highlighted.](media/troubleshoot-global-secure-access-client-disabled/hostname-resolved.png)