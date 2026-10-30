---
layout: Conceptual
title: Configure Transport Layer Security Inspection Policies - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-transport-layer-security
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure a Transport Layer Security inspection policy and assign it to users in your organization.
ms.topic: how-to
ms.reviewer: teresayao
ms.date: 2026-08-28T00:00:00.0000000Z
locale: en-us
document_id: 6f217ae5-d8dc-2e54-9922-2b09d3180636
document_version_independent_id: 6f217ae5-d8dc-2e54-9922-2b09d3180636
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-transport-layer-security.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-transport-layer-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-transport-layer-security.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: dfb49189-0304-9a1e-c015-8ae1c6cdd64f
---

# Configure Transport Layer Security Inspection Policies - Global Secure Access | Microsoft Learn

Transport Layer Security (TLS) inspection in Microsoft Entra Internet Access lets you decrypt and inspect encrypted traffic at service edge locations. This feature lets Global Secure Access apply advanced security controls like threat detection, content filtering, and granular access policies. These access policies help protect against threats that might be hidden in encrypted communications. This article explains how to create a context-aware Transport Layer Security inspection policy and assign it to users in your organization.

## Prerequisites

To complete the steps in this process, you must have the following prerequisites in place:

- An active, enabled certificate authority. Configure either a [Microsoft-managed certificate](how-to-transport-layer-security-settings-managed-certificate) or [your own certificate](how-to-transport-layer-security-settings).
- Test devices or virtual machines running Windows that are either Microsoft Entra joined or hybrid joined to your organization's Microsoft Entra ID.
- A trial license for Microsoft Entra Internet Access.
- [Global Secure Access prerequisites](how-to-configure-web-content-filtering)

## Create a context-aware TLS inspection policy

To create a context-aware Transport Layer Security inspection policy and assign it to users in your organization, complete the following steps:

### Step 1: Global Secure Access admin: create a TLS inspection policy

To create a TLS inspection policy:

1. In the Microsoft Entra admin center, go to **Secure** &gt; **TLS inspection policies** &gt; **Create policy**. ![Screenshot of the Create a TLS inspection policy screen open to the Basics tab.](media/how-to-transport-layer-security/create-tls-inspection-policy.png) The **Default action** specifies what to do if no rules match. The default setting is **Inspect**.
2. Select **Next** &gt; **Add rule**. On the **Rules** page, you can define a custom rule by specifying an **FQDN** or selecting a **Web category**. ![Screenshot of the Create a TLS inspection policy screen open to the Rules tab.](media/how-to-transport-layer-security/add-rule.png)
3. To complete the policy configuration, go to **Save** &gt; **Next** &gt; **Submit**. Note a system rule has been auto created to exclude destinations that do not work with TLS inspection. An editable recommended bypass rule is automatically created to exclude Education, Finance, Government, and Health & Medicine categories.
4. To review rules, including the auto-created rules, select a policy and then go to **Edit** &gt; **Rules**. ![Screenshot of the Edit a TLS inspection policy screen open to the Rules tab.](media/how-to-transport-layer-security/edit-policy-rules.png)

### Step 2: Global Secure Access admin: link the TLS inspection policy to a security profile

Link the TLS inspection policy to a security profile.

Before you enable TLS inspection on user traffic, make sure your organization has established and communicated TLS policy to end users. This step helps maintain transparency and supports compliance with privacy and consent requirements.

You can link the TLS policy to a security profile in two ways:

#### Option 1: Link the TLS policy to the baseline profile for all users

With this method, the baseline profile policy is evaluated last and applies to all user traffic.

1. In the Microsoft Entra admin center, navigate to **Secure** &gt; **Security profiles**.
2. Switch to the **Baseline profile** tab.
3. Select **Edit profile**.
4. In the **Link policies** view, select **+ Link a policy** &gt; **Existing TLS inspection policy**.
5. In the Link a TLS inspection policy view, choose a TLS policy and assign it a priority.
6. Select **Add**.![Screenshot of the Edit Baseline profile screen showing a list of policy names and their priorities.](media/how-to-transport-layer-security/security-profile-baseline.png)

#### Option 2: Link the TLS policy to a security profile for specific users or groups

Alternatively, add a TLS policy to a security profile and link it to a [Conditional Access policy](how-to-configure-web-content-filtering#create-and-link-conditional-access-policy) for a specific user or group. ![Screenshot of the new Conditional Access policy form with all fields completed with sample information.](media/how-to-transport-layer-security/conditional-access-group-assignment.png)

### Step 4: Test the configuration

Ensure your devices trust the root certificate used to break and inspect TLS traffic. You can use Intune to [deploy the trusted certificate](/en-us/intune/intune-service/protect/certificates-trusted-root#to-create-a-trusted-certificate-profile) to your managed Windows devices.

To test the configuration:

1. Make sure the end user device has the root certificate installed in the Trusted Root Certification Authorities folder. ![Screenshot of the Trusted Root Certification Authorities folder.](media/how-to-transport-layer-security/trusted-store.png)
2. Set up the Global Secure Access client:

    - Disable secure DNS and built-in DNS.
    - Block QUIC traffic from your device. QUIC isn't supported in Microsoft Entra Internet Access. Most websites support fallback to TCP when QUIC can't be established. For an improved user experience, deploy a Windows Firewall rule that blocks outbound UDP 443: `New-NetFirewallRule -DisplayName "Block QUIC" -Direction Outbound -Action Block -Protocol UDP -RemotePort 443`.
    - Make sure Internet Access Traffic Forwarding is enabled.
3. Open a browser on a client device and test various websites. Inspect the certificate information and confirm the Global Secure Access certificate. ![Screenshot of the Certificate Viewer with the Global Secure Access certificate highlighted.](media/how-to-transport-layer-security/certificate-viewer.png)

## Disable TLS inspection

To disable TLS inspection:

1. Remove the policy link from the security profile:
    1. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**.
    2. Switch to the **Baseline profile** tab.
    3. Select **Edit profile**.
    4. Select the **Link policies** view.
    5. Select the **Delete** icon for the policy you're disabling.
    6. Select **Delete** to confirm.
2. Remove the TLS inspection policy:
    1. Browse to **Global Secure Access** &gt; **Secure** &gt; **TLS inspection policies**.
    2. Select **Actions**.
    3. Select **Delete**.
3. Remove the TLS inspection policy certificate:
    1. Switch to the **TLS inspection settings** tab.
    2. Select **Actions**.
    3. Select **Delete**.