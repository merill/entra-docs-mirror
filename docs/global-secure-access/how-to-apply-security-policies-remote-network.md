---
layout: Conceptual
title: Apply security policies to remote network traffic - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-apply-security-policies-remote-network
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to apply security policies like web content filtering, threat intelligence, and cloud firewall to remote network traffic in Global Secure Access.
ms.topic: how-to
ms.date: 2026-03-13T00:00:00.0000000Z
ms.reviewer: abhijeetsinha
ai-usage: ai-assisted
locale: en-us
document_id: f7d3d384-b525-9cb4-e766-ba3228f441b5
document_version_independent_id: f7d3d384-b525-9cb4-e766-ba3228f441b5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-apply-security-policies-remote-network.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-apply-security-policies-remote-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-apply-security-policies-remote-network.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 1f29139b-cf85-896e-e30c-065d5e8a1e0b
---

# Apply security policies to remote network traffic - Global Secure Access | Microsoft Learn

## Overview

Global Secure Access enables you to apply comprehensive security policies to remote network traffic, providing consistent protection across your entire network perimeter. By leveraging the baseline security profile, you can enforce tenant-wide security controls on all remote networks without requiring Conditional Access policies.

This article explains how to configure and apply security policies to protect traffic from remote networks such as branch offices, retail locations, and other remote sites.

## Prerequisites

To apply security policies to remote network traffic, you must have:

- A **Global Secure Access Administrator** role in Microsoft Entra ID.
- Remote networks configured and connected to Global Secure Access. For more information, see [How to create a remote network](how-to-create-remote-networks).
- At least one security policy created (such as web content filtering, threat intelligence, TLS inspection, cloud firewall).
- The product requires licensing. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

### Known limitations

For detailed information about known issues and limitations, see [Known limitations for Global Secure Access](reference-current-known-limitations).

## Understanding the baseline security profile

The baseline security profile is a special tenant-wide security profile that applies to all traffic routed through Global Secure Access, including both client-based and remote network traffic. Unlike user-specific security profiles that require Conditional Access policies, the baseline profile enforces policies at the tenant level by default.

Key characteristics of the baseline profile:

- **Automatic enforcement**: Applies to all traffic without requiring Conditional Access policy configuration.
- **Tenant-wide coverage**: Enforces policies on all remote network traffic automatically.
- **Lowest priority**: Operates at priority 65,000 in the policy stack, allowing user-specific profiles to override when needed.

For more information on security profile concepts, see [Understand Microsoft Entra Internet Access](concept-internet-access).

# [Microsoft Entra admin center](#tab/microsoft-entra-admin-center)
Follow these steps to apply security policies to remote network traffic using the baseline profile.

### Step 1: Create or select a security policy

If you haven't already created a security policy, create one first:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/azure/active-directory/roles/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Secure**and select the type of policy you want to create, such as:
    - **Web content filtering policy**
    - **Threat intelligence policies**
    - **TLS inspection policies**
    - **Cloud firewall policies**
3. Select **Create policy** and configure your policy rules.
4. Save the policy.

### Step 2: Link the policy to the baseline profile

1. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles** &gt; **Baseline profile**.
2. Select **Edit profile**.
3. In the **Link policies** view, select **Link a policy** &gt; **Existing policy**.
4. Choose the policy type (such as web content filtering, threat intelligence, TLS inspection, or cloud firewall).
5. Select the policy you want to apply and assign it a priority.
6. Select **Add**.
7. Select **Save**.

    [![Screenshot of the baseline profile page showing how to link a security policy to the baseline profile.](media/how-to-apply-security-policies-remote-network/baseline-profile-link-policy.png)](media/how-to-apply-security-policies-remote-network/baseline-profile-link-policy.png#lightbox)

Note

The baseline security profile automatically applies to all traffic routed through Global Secure Access, including remote network traffic. No Conditional Access policy configuration is required.

# [Microsoft Graph API](#tab/microsoft-graph-api)
You can configure the baseline profile programmatically using Microsoft Graph network access APIs. For a complete tutorial on configuring Internet Access policies with Microsoft Graph, see [Configure Microsoft Entra Internet Access using Microsoft Graph APIs](/en-us/graph/tutorial-entra-internet-access).

### Prerequisites for API access

- Delegated permissions: **NetworkAccess.Read.All** and **NetworkAccess.ReadWrite.All**.
- An API client such as [Graph Explorer](https://aka.ms/ge).
- **Global Secure Access Administrator** role.

### Step 1: Retrieve the baseline profile ID

Get the ID of the baseline security profile.

#### Request

```http
GET https://graph.microsoft.com/beta/networkaccess/filteringProfiles
```

#### Response

```json
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#networkaccess/filteringProfiles",
  "value": [
    {
      "id": "00001111-aaaa-2222-bbbb-3333cccc4444",
      "name": "Baseline Profile",
      "description": "Default baseline security profile",
      "priority": 65000,
      "state": "enabled",
      "version": "1.0.0",
      "createdDateTime": "2024-01-01T00:00:00Z",
      "lastModifiedDateTime": "2024-01-01T00:00:00Z"
    }
  ]
}
```

### Step 2: Create a security policy

Create the security policy you want to apply. This example creates a web content filtering policy.

#### Request

```http
POST https://graph.microsoft.com/beta/networkaccess/filteringPolicies
Content-type: application/json

{
  "name": "Block Social Media for Remote Networks",
  "policyRules": [
    {
      "@odata.type": "#microsoft.graph.networkaccess.webCategoryFilteringRule",
      "name": "Block Social Media",
      "ruleType": "webCategory",
      "destinations": [
        {
          "@odata.type": "#microsoft.graph.networkaccess.webCategory",
          "name": "SocialNetworking"
        }
      ]
    }
  ],
  "action": "block"
}
```

#### Response

```json
{
  "id": "cccccccc-2222-3333-4444-dddddddddddd",
  "name": "Block Social Media for Remote Networks",
  "description": null,
  "version": "1.0.0",
  "lastModifiedDateTime": "2024-02-11T18:10:28Z",
  "createdDateTime": "2024-02-11T18:10:27Z",
  "action": "block"
}
```

### Step 3: Link the policy to the baseline profile

Link your security policy to the baseline profile.

#### Request

```http
POST https://graph.microsoft.com/beta/networkaccess/filteringProfiles/{baseline-profile-id}/policies
Content-type: application/json

{
  "priority": 100,
  "state": "enabled",
  "@odata.type": "#microsoft.graph.networkaccess.filteringPolicyLink",
  "loggingState": "enabled",
  "policy": {
    "id": "cccccccc-2222-3333-4444-dddddddddddd",
    "@odata.type": "#microsoft.graph.networkaccess.filteringPolicy"
  }
}
```

#### Response

```json
{
  "id": "dddddddd-9999-0000-1111-eeeeeeeeeeee",
  "priority": 100,
  "state": "enabled",
  "version": "1.0.0",
  "loggingState": "enabled",
  "lastModifiedDateTime": "2024-02-11T18:31:32Z",
  "createdDateTime": "2024-02-11T18:31:32Z",
  "policy": {
    "@odata.type": "#microsoft.graph.networkaccess.filteringPolicy",
    "id": "cccccccc-2222-3333-4444-dddddddddddd",
    "name": "Block Social Media for Remote Networks",
    "description": null,
    "version": "1.0.0",
    "action": "block"
  }
}
```

---

## Verify policy enforcement

After configuring security policies for remote networks, verify that they're being enforced:

1. Browse to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
2. Filter the logs by traffic from your remote networks by applying the **DeviceCategory** filter.
3. Verify that blocked traffic shows the appropriate action and policy information.
4. Check that allowed traffic flows through as expected.

Note

Configuration changes to the baseline profile typically take effect within a few minutes. Monitor traffic logs to confirm policy enforcement.

## Policy priority and interaction

When both the baseline profile and user-specific security profiles are configured:

- User-specific profiles (linked to Conditional Access policies) are evaluated first and have higher priority.
- The baseline profile operates at the lowest priority (65,000) and provides a fallback policy.
- Policies within a profile are evaluated based on their assigned priority numbers (100 is highest priority).
- Once a policy matches and takes action (block/allow), policy evaluation stops.

This design allows you to:

- Apply broad tenant-wide policies via the baseline profile.
- Override baseline policies for specific users or groups using Conditional Access-linked profiles. User awareness is possible only through the Global Secure Access client. Non-client traffic coming through remote networks goes through the baseline profile.
- Ensure consistent protection for all remote network traffic while maintaining flexibility for exceptions.