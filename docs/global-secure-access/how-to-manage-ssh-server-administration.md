---
layout: Conceptual
title: Use SSH to administer servers with Microsoft Entra Private Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-manage-ssh-server-administration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn to configure and establish a Secure Shell (SSH) connection using Microsoft Entra Private Access for enhanced security.
ms.topic: how-to
ms.date: 2025-05-12T00:00:00.0000000Z
ms.reviewer: jricketts
ai-usage: human-only
locale: en-us
document_id: b320665f-5c17-b840-1273-c017aa88f1eb
document_version_independent_id: b320665f-5c17-b840-1273-c017aa88f1eb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-manage-ssh-server-administration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-manage-ssh-server-administration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-manage-ssh-server-administration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 19957046-2ca6-a36c-1472-db7791864bc3
---

# Use SSH to administer servers with Microsoft Entra Private Access - Global Secure Access | Microsoft Learn

Secure Shell (SSH) is widely recognized across the IT industry as a critical service for system administrators. It provides a secure and encrypted method to access and manage remote systems over unsecured networks. IT administrators rely on SSH to perform essential tasks securely, including the configuration, deployment, and maintenance of servers and applications in an organization’s infrastructure.

In this guide and [in this video](https://youtu.be/lpgl08z7dzE), you learn how to configure and establish an SSH connection using Microsoft Entra Private Access to enhance security in your remote access workflows.

## Establish SSH connections with Microsoft Entra Private Access

Microsoft Entra Private Access enhances the security and efficiency of SSH management traffic by providing a secure, identity-centric Zero Trust Network Access (ZTNA) solution by allowing IT administrators to establish SSH connections to remote servers securely.

![Diagram of an SSH connection using Private Access.](media/how-to-manage-ssh-server-administration/ssh-service.png)

## Prerequisites

Ensure you meet the following prerequisites.

- **Licensing** - Learn about licensing for [Microsoft Global Secure Access](overview-what-is-global-secure-access)
    - Learn more about [Microsoft Entra plans and pricing](https://aka.ms/azureadlicense)
    - See, [Global Secure Access client for Windows](how-to-install-windows-client)
- **A remote server with SSH** enabled
- **Microsoft Global Secure Access private network connector**with network connectivity to the resource
    - Learn how to [configure connectors](how-to-configure-connectors)
- **A device with the Global Secure Access client**
- **Private Access profile**enabled
    - See [Global Secure Access traffic forwarding profiles](concept-traffic-forwarding)
- **[Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference)**for administrators
    - Learn about [built-in roles](reference-role-based-permissions)

## Configure SSH traffic acquisition and secure with Conditional Access policies

To create the Enterprise Application:

1. In [Microsoft Entra admin center](https://entra.microsoft.com), browse to **Global Secure Access**.
2. Select **Applications**, then select **Enterprise application**.
3. Select **New application**.
4. Type a name for the SSH enterprise application.
5. The **Create application segment** panel appears.
6. To application segments to acquire SSH traffic, select **Destination type** and add the IPs or subnets that provide a connection to your remote server.
7. Configure **Port** to acquire traffic destined for port **22**.
8. For **Protocol**, select **TCP**.
9. Select **Save**.

Assign users and groups to the application. Only users assigned to the enterprise application will have the ability to connect to it over the designated application segment(s).

1. In the Microsoft Entra admin center, browse to **Global Secure Access**.
2. Select **Applications**, then select **Enterprise application**.
3. Select the SSE enterprise application you created and then select **Users and groups**.
4. Add users and groups that require access.
5. If desired, create [Microsoft Entra Conditional Access](../identity/conditional-access/overview) policy to increase application security. For more information, see [Apply Conditional Access policies to Private Access apps](how-to-target-resource-private-access-apps).
6. Confirm you can access the SSH services from the client device.

### Configuration checklist

Use the following checklist to help confirm configuration.

- Ensure the server is running and accessible by the SSH port.
- Confirm the correct host firewall configuration.
    - Find guidance in [OpenSSH Server configuration for Windows](/en-us/windows-server/administration/OpenSSH/openssh-server-configuration).
- Confirm the application segment has downloaded to the Global Secure Access client.
    - Right-click the **Global Secure Access** client icon in the Windows taskbar.
    - Select **Advanced Diagnostics** &gt; **Forwarding profile** &gt; **Private Access**.
    - Verify the application appears in the access profile.

## Connection failure

If the connection fails, use the following checklist.

- Verify the server IP address and port number.
- Confirm the SSH port is allowed from a Private Connector server.
- Isolate firewall rules that might block SSH traffic.
- Validate the Global Secure Access client captures traffic.
- Verify users are assigned to the application.