---
layout: Conceptual
title: Learn about Universal Conditional Access Through Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-universal-conditional-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn about how Microsoft Entra Internet Access and Microsoft Entra Private Access secures access to your resources through Conditional Access.
ms.topic: concept-article
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: smistry
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9791f5db-aef2-6570-c81a-1abfdee65422
document_version_independent_id: 7ed184bc-a0fc-44bd-78a3-33c465fdfe3a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-universal-conditional-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-universal-conditional-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-universal-conditional-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: e4c89696-106f-a9b7-cda0-3762ded2d483
---

# Learn about Universal Conditional Access Through Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

In addition to sending traffic to Global Secure Access, administrators can use Conditional Access policies to secure traffic profiles. They can mix and match controls as needed like requiring multifactor authentication, requiring a compliant device, or defining an acceptable sign-in risk. Applying these controls to network traffic not just cloud applications allows for universal Conditional Access.

Conditional Access on traffic profiles provides administrators with enormous control over their security posture. Administrators can enforce [Zero Trust principles](/en-us/security/zero-trust/) using policy to manage access to the network. Using traffic profiles allows consistent application of policy. For example, applications that don't support modern authentication can now be protected behind a traffic profile.

This functionality allows administrators to consistently enforce Conditional Access policy based on [traffic profiles](concept-traffic-forwarding), not just applications or actions. Administrators can target specific traffic profiles - the Microsoft traffic profile, private resources, and internet access with these policies. Users can access these configured endpoints or traffic profiles only when they satisfy the configured Conditional Access policies.

## Prerequisites

- Administrators who interact with **Global Secure Access**features must have one or more of the following role assignments depending on the tasks they're performing.
    - The [Global Secure Access Administrator role](/en-us/azure/active-directory/roles/permissions-reference) role to manage the Global Secure Access features.
    - The [Conditional Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#conditional-access-administrator) to create and interact with Conditional Access policies.
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

### Known tunnel authorization limitations

Both the Microsoft and Internet access forwarding profiles use Microsoft Entra ID Conditional Access policies to authorize access to their tunnels in the Global Secure Access Client. This means that you can Grant or Block access to the Microsoft traffic and Internet access forwarding profiles in Conditional Access. In some cases when authorization to a tunnel isn't granted, the recovery path to regain access to resources requires accessing destinations on either the Microsoft traffic or Internet access forwarding profile, locking a user out from accessing anything on their machine.

One example is if you block access to the Internet access target resource on noncompliant devices, you leave Microsoft Entra Internet Access users unable to bring their devices back to compliance. The way to mitigate this issue is bypassing [Network endpoints for Microsoft Intune](/en-us/mem/intune/fundamentals/intune-endpoints) and any other destinations accessed in [Custom compliance discovery scripts for Microsoft Intune](/en-us/mem/intune/protect/compliance-custom-script). You can perform this operation as part of custom bypass in the [Internet access forwarding profile](concept-traffic-forwarding).

### Other known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Conditional Access policies

With Conditional Access, you can enable access controls and security policies for the network traffic acquired by Microsoft Entra Internet Access and Microsoft Entra Private Access.

- Create a policy that targets all [Microsoft traffic](how-to-target-resource-microsoft-profile).
- Apply Conditional Access policies to your [Private Access apps](how-to-target-resource-private-access-apps), such as Quick Access.
- Enable [Global Secure Access source IP restoration](how-to-source-ip-restoration) so the source IP address is visible in the appropriate logs and reports.

## Internet Access flow diagram

The following example demonstrates how Microsoft Entra Internet Access works when you apply Universal Conditional Access policies to network traffic.

Note

Microsoft's Security Service Edge solution comprises three tunnels: Microsoft traffic, Internet Access, and Private Access. Universal Conditional Access applies to the Internet Access and Microsoft traffic tunnels. There isn't support to target the Private Access tunnel. You must individually target Private Access Enterprise Applications.

The following flow diagram illustrates Universal Conditional Access targeting internet resources and Microsoft apps with Global Secure Access.

[![Diagram shows flow for Universal Conditional Access when targeting internet resources with Global Secure Access and Microsoft apps with Global Secure Access.](media/concept-universal-conditional-access/internet-access-universal-conditional-access-inline.png)](media/concept-universal-conditional-access/internet-access-universal-conditional-access-expanded.png#lightbox)

| Step | Description |
| --- | --- |
| 1 | The Global Secure Access client attempts to connect to Microsoft's Security Service Edge solution. |
| 2 | The client redirects to Microsoft Entra ID for authentication and authorization. |
| 3 | The user and the device authenticate. Authentication happens seamlessly when the user has a valid Primary Refresh Token. |
| 4 | After the user and device authenticate, Universal Conditional Access policy enforcement occurs. Universal Conditional Access policies target the established Microsoft and internet tunnels between the Global Secure Access client and Microsoft Security Service Edge. |
| 5 | Microsoft Entra ID issues the access token for the Global Secure Access client. |
| 6 | The Global Secure Access client presents the access token to Microsoft Security Service Edge. The token validates. |
| 7 | Tunnels establish between the Global Secure Access client and Microsoft Security Service Edge. |
| 8 | Traffic starts being acquired and tunneled to the destination via the Microsoft and Internet Access tunnels. |

Note

Target Microsoft apps with Global Secure Access to protect the connection between the Microsoft Security Service Edge and the Global Secure Access client. To ensure that users can't bypass the Microsoft Security Service Edge service, create a Conditional Access policy that requires compliant network for your Microsoft 365 Enterprise applications.

## User experience

When users sign in to a machine with the Global Secure Access Client installed, configured, and running for the first time they're prompted to sign in. When users attempt to access a resource protected by a policy. Like the previous example, the policy is enforced and they're prompted to sign in if they haven't already. Looking at the system tray icon for the Global Secure Access Client you see a red circle indicating it's signed out or not running.

![Screenshot showing the pick an account window for the Global Secure Access Client.](media/how-to-target-resource-microsoft-profile/windows-client-pick-an-account.png)

When a user signs in the Global Secure Access Client has a green circle that you're signed in, and the client is running.

![Screenshot showing the Global Secure Access Client is signed in and running.](media/how-to-target-resource-microsoft-profile/global-secure-access-client-signed-in.png)