---
layout: Conceptual
title: 'Tutorial: Per-app access segmentation - Microsoft Entra Private Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-private-access-app-segmentation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to transition from Quick Access to per-app segmentation by using Application Discovery to create enterprise applications with granular Conditional Access controls.
ms.topic: tutorial
ms.date: 2026-03-11T00:00:00.0000000Z
ms.subservice: entra-private-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: c8a1c9ca-a99a-d151-9e8f-125df5a0cb5b
document_version_independent_id: c8a1c9ca-a99a-d151-9e8f-125df5a0cb5b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-private-access-app-segmentation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-private-access-app-segmentation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-private-access-app-segmentation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 58dfeef4-c8ac-d8b5-8c78-123a8e71da95
---

# Tutorial: Per-app access segmentation - Microsoft Entra Private Access | Microsoft Learn

With Quick Access, you can quickly onboard to Private Access by publishing wide IP ranges and wildcard FQDNs, similar to traditional VPN solutions. However, for better security, you should transition from Quick Access to per-application segmentation. This approach allows you to set user assignments per application and target specific applications with Conditional Access policies, following the principle of least privilege.

This tutorial walks through using Application Discovery to identify which application segments users access through Quick Access. You then create enterprise applications either from the app discovery table or manually, assign users and groups, and configure Conditional Access policies for granular control.

In this tutorial, you learn how to:

- Review Application Discovery data to identify traffic patterns.
- Create an enterprise application from Application Discovery.
- Create an enterprise application manually.
- Assign users and groups to the enterprise application.
- Configure Conditional Access policies for granular control.
- Verify per-app access through the Global Secure Access client.

## Prerequisites

- One or more users have been accessing private resources through Quick Access for at least 10-15 minutes to generate discovery data.

## Key concepts

Tip

**From broad access to least privilege**

Application Discovery helps administrators see which applications users access through Quick Access. By identifying usage patterns, you can create private applications with precise segmentation, ensuring users only get the access they need.

This tutorial highlights the architectural turning point in Private Access adoption.

- **Quick Access** is broad and migration-friendly.
- **Per-app enterprise applications** are precise and security-focused.
- **Application Discovery** makes the transition easy by reporting exactly who (users, devices) has been accessing what (FQDNs, IP addresses, ports, protocols).

Why this is important:

- You reduce lateral movement risk by limiting app scope.
- You can apply Conditional Access to specific apps.
- You can migrate app segments in phases instead of a "big bang" cutover.

When an enterprise application network segment overlaps Quick Access, the enterprise application takes precedence for that resource. This enforces explicit assignment and prevents accidental overexposure.

## Kerberos SSO and Private Access

Though not in the scope of this tutorial, many organizations have Kerberos applications. At a high level, you enable Kerberos SSO by publishing your domain controllers (specific ports like 88 and 389) as an enterprise app and enabling private DNS resolution for domain controller discoverability. Once configured, clients can reach domain controllers to acquire Kerberos tickets. For more information, see [Configure Kerberos SSO](how-to-configure-kerberos-sso).

### Step 1: Review Application Discovery data

Application Discovery shows all application segments in Quick Access that users accessed via the Global Secure Access client in the last 30 days.

1. From the Microsoft Entra admin center, browse to **Global Secure Access** &gt; **Applications** &gt; **Application discovery**.
2. Review the list of discovered application segments.

    ![Screenshot showing the Application Discovery page with discovered application segments.](media/tutorial-private-access-app-segmentation/application-discovery-segments.png)
3. Select a **Destination FQDN** or **Destination IP** to view more details.
4. Review the **Usage** tab to see a graph of users, transactions, devices, or bytes over time.
5. Select the **Users** tab to see which users accessed the application segment.

Tip

Use the list of users to inform decisions about which users and groups to assign to the enterprise application once you create it.

### Step 2: Create an enterprise application from Application Discovery

Use Application Discovery to create a new enterprise application based on discovered application segments.

1. From the **Application discovery** list, select one or more application segments that correspond to an application you want to create (check the box next to the app).

    Note

    **Application segment examples:**

    - **Single segment application**: A file server like `filesrv.contoso.com`, TCP, 445.
    - **Multi-segment application**: Active Directory services spanning multiple ports and protocols on `dc1.contoso.com` and `dc2.contoso.com` (for example, configuring [Kerberos SSO for Private Access](how-to-configure-kerberos-sso)).
2. Select **Add to new application**.

    ![Screenshot showing how to add discovered segments to a new application.](media/tutorial-private-access-app-segmentation/application-discovery-add-to-app.png)
3. In the **Create Global Secure Access application** screen:

    - Enter a **Name** for the application.
    - Select the appropriate **Connector Group**.
    - Assign users or groups to the application.
4. Select **Save**.

Note

You can optionally check the box **Import users and groups from Quick Access application**. This option imports all users and groups assigned to the Quick Access app and assigns them to the new enterprise app. If you leave this unchecked, the application is created with no users or groups assigned. The admin must assign users as an extra step.

![Screenshot showing the option to import users and groups from Quick Access.](media/tutorial-private-access-app-segmentation/application-discovery-import-users.png)

Note

Discovered application segments persist in the Application Discovery table until a user signs in to the new enterprise application and accesses the resource.

### Step 3: Create an enterprise application manually

You can also create an enterprise application manually without using Application Discovery.

#### Step 3.1: Create an enterprise application

1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
2. Select **New application**.
3. Enter a **Name** for the application (for example, "Internal Web Portal").
4. Select a **Connector group** from the dropdown menu.
5. Select **Add application segment**.
6. Select a **Destination type**.
7. Enter the **Ports** (separate multiple ports with commas, use hyphens for ranges, for example, `80, 443, 8080-8090`).
8. Select the **Protocol** (TCP, UDP, or both).
9. Select **Apply**, then select **Save**.

Note

When an enterprise application's segment overlaps with Quick Access, the enterprise application takes precedence—including its assignment scope. For example, if Quick Access is assigned to the entire organization with a full network range, but an admin creates an enterprise application segment targeting a specific IP or port and assigns it only to an admin group, users not assigned to that enterprise application lose access, even though they're assigned to Quick Access which has an overlapping network segment.

#### Step 3.2: Assign users and groups

You must grant access to the enterprise application by assigning users or groups.

1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
2. Search for and select your application.
3. Select **Users and groups** from the side menu.
4. Select **Add user/group**.
5. Search for and select the users or groups who need access.
6. Select **Assign**.

### Step 4: Configure Conditional Access policies

Conditional Access policies for per-app access are configured at the application level.

1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Enterprise applications**.
2. Select your application.
3. Select **Conditional Access** from the side menu.
4. Select **New policy**.
5. Configure the policy:
    - **Name**: Enter a descriptive name (for example, "Require MFA for Internal Portal").
    - **Users**: Select the users or groups or `All users`.
    - **Target resources**: Select the Private Access Enterprise application you created.
    - **Conditions**: Configure as needed (for example, device platforms, locations).
    - **Grant**: Select controls like **Require multifactor authentication** or **Require device to be marked as compliant**.
    - **Session (optional):** If you want an interactive MFA prompt and don't want MFA satisfied by the claim in the token, you can configure a **Sign-in frequency**.
6. Set **Enable policy** to **On**.
7. Select **Create**.

For more information, see [Apply Conditional Access policies to Private Access apps](how-to-target-resource-private-access-apps).

### Step 5: Verify per-app access

1. On your test device, right-click the **Global Secure Access** icon in the system tray.
2. Select **Advanced diagnostics**.
3. Select the **Traffic** tab, then select **Start collecting**.
4. Attempt to access the private application you configured.
5. Verify you can access the application successfully.
6. Verify the Conditional Access policy is applied.
7. Review the network traffic capture in **Advanced diagnostics** to confirm traffic is being tunneled through **Global Secure Access** (**Action** = **Tunnel**).

## What you learned

In this exercise, you accomplished the following:

- **Used Application Discovery for segmentation planning** - Identified real traffic patterns before publishing apps.
- **Created per-app enterprise applications** - Created enterprise applications for internal resources with explicit network segments.
- **Controlled access through app assignments and Conditional Access** - Enforced per-app assignment and applied identity-driven Conditional Access policy to specific on-premises applications.
- **Validated tunneled app behavior** - Confirmed that segmented resources are properly acquired and tunneled by the **Global Secure Access client**.

This is where Private Access shifts from VPN replacement to Zero Trust access control. In the next tutorial, you optimize user experience by allowing eligible app traffic to stay local when users are on trusted corporate networks.