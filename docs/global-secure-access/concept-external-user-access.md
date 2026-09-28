---
layout: Conceptual
title: Learn about Global Secure Access external user access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-external-user-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how Global Secure Access enables secure external user access for partners through the Global Secure Access client and Azure Virtual Desktop.
ms.topic: concept-article
ms.date: 2026-04-09T00:00:00.0000000Z
ms.reviewer: cagautham
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 306c83bb-810c-fc0b-5b08-a708bec70460
document_version_independent_id: 306c83bb-810c-fc0b-5b08-a708bec70460
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-external-user-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-external-user-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-external-user-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/7814ca69-56be-4667-8a46-86327796c328
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/f15dfcd0-2664-48ba-bb88-f1f86eadbfd1
platformId: 022bca62-faca-5c23-43f7-fab3d5e71cbf
---

# Learn about Global Secure Access external user access - Global Secure Access | Microsoft Learn

Organizations often collaborate with external partners such as vendors and contractors. Traditional solutions for granting access to internal resources for external users typically lack visibility and granular security controls. Global Secure Access, built into Microsoft Entra, solves these challenges by using existing external user identities and providing advanced security features like Conditional Access, Continuous Access Evaluation, and cross-tenant trust. This approach enables secure, efficient management of external user access without duplicating accounts or requiring complex federation.

The External User access feature in Global Secure Access allows partners to use their own devices and identities to access company resources securely. It supports bring your own device (BYOD) scenarios, enforces per-app multifactor authentication, and offers seamless multitenant switching for partner users. Administrators benefit from single-pane management for identity, access, and network policies, reducing operational overhead while improving governance. Integrated logging and telemetry across identity and network layers provide full visibility into external user activity, ensuring a secure and streamlined experience for external collaboration.

## Enable external user access with the Global Secure Access client

Partners can enable the external user access feature with the Global Secure Access client, signed in to their home organization's Microsoft Entra ID account. The Global Secure Access client automatically discovers partner tenants where the user is an external user (guest or member) and offers the option to switch into the customer's tenant context. External users can access only assigned resources and only if they're included in the resource tenant's Private Access traffic forwarding profile. The client routes only traffic for the customer's private applications through the customer's Global Secure Access service.

[![Diagram of external user access with Global Secure Access.](media/concept-external-user-access/client-agent.png)](media/concept-external-user-access/client-agent.png#lightbox)

### Prerequisites

To enable external user access with the Global Secure Access client, you must have:

- External users (guest or member) configured in the resource tenant. For more information, see the following articles:

    - [Quickstart: Add a external user and send an invitation](../external-id/b2b-quickstart-add-guest-users-portal)
    - [Understand and manage the properties of external users](../external-id/user-properties)
- The Global Secure Access client installed and running on the device connected to the home tenant. To install the Global Secure Access client, see [Install the Global Secure Access client for Microsoft Windows](how-to-install-windows-client).

    Tip

    The home tenant doesn't need to have a Global Secure Access license.
- Global Secure Access Private Access enabled on the resource tenant. Configure the Private Access traffic forwarding profile on the resource tenant and assign the profile to external user accounts.
- The resource tenant linked to an Azure subscription through Microsoft Entra External ID subscription linking. The administrator must link the subscription in the resource tenant so external users can access private resources and usage is billed correctly. For more information, see [Global Secure Access licensing for guest users](reference-licensing-guest-users#link-your-tenant-to-a-subscription).
- At least one private application configured and assigned to external user accounts.
- The external user access feature enabled on the client by setting the following registry key:`Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\Global Secure Access Client`

    | Value | Type | Data | Description |
    | --- | --- | --- | --- |
    | GuestAccessEnabled | REG\_DWORD | 0x1 | External user access is enabled on this device. |
    | GuestAccessEnabled | REG\_DWORD | 0x0 | External user access is disabled on this device. |

Administrators can use a Mobile Device Management (MDM) solution, such as [Microsoft Intune](/en-us/mem/intune/apps/apps-win32-app-management) or Group Policy, to set the registry values.

### Connect to the resource tenant

To enable external user access with the Global Secure Access client, follow these steps:

1. Launch the Global Secure Access client.
2. Switch the client to the resource tenant:
    1. Select the Global Secure Access client icon in the system tray.
    2. Select the User menu (profile picture) and select the resource tenant from the list. 
        Tip

        The home tenant doesn't need to have Global Secure Access configured for this step to work.
    3. Verify that you're connected to the resource tenant. When true, the Global Secure Access **Organization** displays the name of the resource tenant.![Screen shot of the Global Secure Access Status pane showing that the Organization is connected to the resource tenant.](media/concept-external-user-access/organization-resource-tenant.png)

All the Global Secure Access tunnels to the home tenant (such as Private Access, Internet Access, or Microsoft 365 tunnels) disconnect and a new Private Access tunnel is created to the resource tenant. You should be able to access private applications configured on the resource tenant.

### Switch back to the home tenant

1. Select the Global Secure Access client icon in the system tray.
2. Select the User menu (profile picture).
3. To switch back, select the home tenant from the list.

Switching back disconnects the Private Access tunnel from the resource tenant and connects the configured tunnels to the home tenant.

## Frequently asked questions (FAQ)

**Q: Are cross tenant signals like MFA and device compliance supported?** A: Yes, cross tenant signals work with the Global Secure Access external user access feature.

**Q: What is the license requirement for the home tenant?** A: The home tenant doesn't need a Global Secure Access license. The feature requires at least a Microsoft Entra free tenant.

**Q: Are both user types, Guest and Member, supported?** A: Yes. Cross Tenant Sync creates guest users as userType = Member by default, and this user type is supported.

**Q: Does the device need to be registered to the resource tenant?** A: No, device registration isn't required on the resource tenant for external user access to work.

**Q: Can I configure MFA on the resource tenant?** A: Yes, you can configure MFA on the user and on the applications.

**Q: Is tenant connection status is persisted on reboot?** A: Yes, the client retains the tenant connection after a reboot. Additionally, if the user has selected Disable Private Access, the tunnel’s disabled state will persist across reboots

**Q: Is this feature supported from a windows Entra registered device(BYOD)?** A: Yes, you can use a windows device which is registered to Entra for switching to resource tenant.

**Q: What is the definition of an External User?** A: The definition of an External User is provided in the [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/product/Glossary). Refer to the official Product Terms glossary and search for “External Users” for the most up‑to‑date definition.

## Traffic logs visibility

On the resource tenant, you can check if traffic originates from an external user. The traffic logs include the following fields for external user sessions:

- **Cross-tenant access type**: B2B collaboration
- **Home tenant ID**: The tenant ID of the external user's home organization

These fields help administrators identify and monitor external user traffic patterns in the resource tenant.

## Known limitations

- External user access doesn't support keeping the Internet Access, Microsoft 365, and Microsoft Entra tunnels to the home tenant.
- Switching an account to the resource tenant fails when the resource tenant is configured for required MFA in the cross-tenant configuration and the home tenant is configured with passwordless sign-in (PSI) on the authenticator app.
- On the resource tenant, inbound access settings to private application is not allowed on cross tenant settings.
- When a user switches tenants, existing active application connections like Remote Desktop Protocol (RDP) remain connected to the previous tenant.
- External user access in the resource tenant will fail if compliant network policies are enforced for private applications. External users must be excluded from these policies.
- When the client is already connected and the user is added to a new external tenant, the new tenant does not appear in the client UI. The client must be disabled and re-enabled for the new tenant to be shown.
- On the resource tenant, if the Private Access traffic profile is assigned after the client is connected, the client must be disabled and re-enabled for private traffic to take effect.

## Enable external user access for Azure Virtual Desktop and Windows 365

You can enable Global Secure Access on Windows 365 and Azure Virtual Desktop instances that support external identities to provide external user access. With this capability, external users—such as guests, partners, and contractors—from other organizations can securely access resources in your tenant (the resource tenant). As a resource tenant administrator, you can configure Private Access, Internet Access, and Microsoft 365 traffic policies for these third-party users, helping ensure secure and controlled access to your organization's resources.

[![Diagram showing an overview of external user access in Global Secure Access.](media/concept-external-user-access/guest-access-overview.png)](media/concept-external-user-access/guest-access-overview.png#lightbox)

Note

In this scenario, the virtual machine is domain joined to the resource tenant. The Global Secure Access client on the VM automatically authenticates the external user to the resource tenant based on the VM's domain membership, eliminating the need for manual tenant switching.

To enable external user access for Windows 365 or Azure Virtual Desktop (AVD) virtual machines (VM) with Global Secure Access, follow these steps:

1. Configure your Windows 365 or Azure Virtual Desktop VM instance to use external ID linking. For more information, see [Configure external ID linking](/en-us/azure/virtual-desktop/authentication#external-identity-preview).
2. Onboard your organization to Global Secure Access. For more information, see [onboarding instructions](/en-us/entra/global-secure-access/overview-what-is-global-secure-access#licensing-overview).
3. Set up one or more Global Secure Access traffic forwarding profiles and assign them to users with external IDs. For more information, see [Configure traffic forwarding profiles](/en-us/entra/global-secure-access/quickstart-access-admin-center) and [Assign users to profiles](/en-us/entra/external-id/what-is-b2b).
4. Install and configure the Global Secure Access client on the virtual machines. For more information, see [Installation guide for the Global Secure Access client](/en-us/entra/global-secure-access/how-to-install-windows-client).

Once configured, the Global Secure Access client automatically connects to the tenant associated with the VM instance by using the external ID.