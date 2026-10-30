---
layout: Conceptual
title: 'Tutorial: Configure Web Content Filtering with the Baseline Profile - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-internet-access-web-content-filtering
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to create a web content filtering policy and assign it to the baseline security profile in Microsoft Entra Internet Access.
ms.topic: tutorial
ms.date: 2026-03-07T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4654523a-e46b-8792-2586-7a83283ee621
document_version_independent_id: 4654523a-e46b-8792-2586-7a83283ee621
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-internet-access-web-content-filtering.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-internet-access-web-content-filtering
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-internet-access-web-content-filtering.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 61d3ec6b-e898-6e39-d4d4-5a3b263be6e3
---

# Tutorial: Configure Web Content Filtering with the Baseline Profile - Global Secure Access | Microsoft Learn

Microsoft Entra Internet Access provides web content filtering to control access to websites based on their fully qualified domain names (FQDNs) or web categories such as gambling, social media, or malware. Policies are assigned to security profiles, which can then be applied to all users via the baseline profile or to specific users via Conditional Access. This layered approach allows organizations to enforce broad protections while still enabling granular exceptions for specific groups.

In this tutorial, you learn how to:

- Create a web content filtering policy that blocks gambling websites and a specific domain.
- Link the filtering policy to the baseline security profile.
- Validate that blocked websites can't be accessed.
- View blocked traffic in the traffic log.

## Key concepts

Security profiles are containers that hold one or more filtering policies. They're delivered through user-aware Microsoft Entra Conditional Access policies. For example, to block all AI websites except `m365.cloud.microsoft` (Enterprise Copilot) for a specific group of users:

```Example
"Security Profile for Sales Department"   <---- the security profile
    Allow m365.cloud.microsoft at priority 100      <---- higher priority filtering policy (evaluated first)
    Block Artificial Intelligence at priority 200   <---- lower priority filtering policy
```

- **Policy priority**: Determines the order of evaluation:

    - **100 = highest priority**: Evaluated first.
    - **65,000 = lowest priority**: Evaluated last.
    - **Traditional firewall logic**: Lower numbers = higher precedence.
    - **Best practice:** Add spacing of about 100 between priorities for future flexibility.
- **Multi-profile processing**: When multiple Conditional Access policies match a user's traffic, *all matching security profiles are processed* in priority order of the security profiles themselves.
- **Baseline security profile**: This profile has special behavior:

    - It applies to *all Internet Access traffic* routed through the service.
    - It doesn't require linking to a Conditional Access policy.
    - It acts as a *catch-all policy* at the lowest priority (65,000).
    - It always executes, even when a Conditional Access policy matches another security profile.

### Example scenario

```Example
User "Angie" matches a Conditional Access policy → Custom Security Profile (priority 100)
   ↓
All policies in Custom Security Profile are evaluated
   ↓
Baseline Profile (priority 65,000) ALSO executes ← Always runs as catch-all
```

You can create organization-wide protections in the baseline profile while still allowing higher-priority custom profiles to create exceptions for specific groups. Higher-priority security profiles still take precedence over the baseline security profile if there are conflicting rules between the two profiles.

## Objective

In this tutorial, you create a web content filtering policy that blocks access to gambling websites and the Bing search engine. You assign the policy to the baseline security profile and verify that the websites are blocked as expected.

### Step 1: Create a web filtering policy

Configure a web content filtering policy that blocks gambling websites and Bing.

1. In the **Microsoft Entra admin center**, go to **Global Secure Access** &gt; **Secure** &gt; **Web content filtering policies** &gt; **Create policy**.
2. Provide the following details:
    - **Name**: Enter **Baseline Blocked Websites**.
    - **Description**: Add a description.
    - **Action**: Select **Block**.
3. Select **Next**.
4. On **Policy Rules**, select **Add Rule**.
5. In the **Add Rule**dialog, provide the following details:
    - **Name**: Enter **Block Gambling**.
    - **Destination type:** Select **webCategory**.
    - **Search**: Search for and select **Gambling**.
6. Select **Add**.
7. Select **Add Rule** again.
8. In the **Add Rule**dialog, provide the following details:
    - **Name**: Enter **Block Bing**.
    - **Destination type**: Select **fqdn**.
    - **Destination**: Select **www.bing.com,bing.com**.
9. Select **Add**.
10. Select **Next**.
11. Select **Create policy**.

This tutorial configures only FQDN and `webCategory` web content filtering. URL filtering requires TLS inspection. Both TLS inspection and URL filtering are covered in later tutorials.

### Step 2: Link the web content filtering policy to the baseline security profile

Note

The baseline security profile applies to any internet traffic tunneled through GSA. It has the lowest priority (65000), which means any other security profile that targets a specific set of users or groups takes precedence over the baseline profile.

1. In the **Microsoft Entra admin center**, go to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**.
2. Select the **Baseline profile** tab.
3. Select the **Link policies** page.
4. Select **Link a policy**, and then select **Existing web filtering policy**.
    - In the **Link a policy** dialog, under **Policy name**, select **Baseline Blocked Websites**.
    - **Priority**: Select **100**.
    - **State**: Select **Enabled**.
5. Select **Add**.
6. On **Link policies**, confirm that **Baseline Blocked Websites** is listed.

### Step 3: Validate that Bing and gambling websites are blocked

1. Sign in to the device with the Global Secure Access (GSA) client.
2. Open a browser and attempt to go to `www.bing.com` and `www.gambling.com`.

    It can take up to 20 minutes for the policy to apply to your client device.
3. Verify that the webpages don't load.

    ![Screenshot that shows connection reset.](media/tutorial-internet-access-web-content-filtering/connection-reset-error.png)

You received this error message because you didn't enable Transport Layer Security (TLS) inspection, which provides a customizable block message and unlocks more security capabilities. You see a more user-friendly error message in the TLS inspection tutorial.

### Step 4: View activity in the traffic log

1. In the Microsoft Entra admin center, select **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**. If needed, select **Add filter**. Filter on **User principal name**, which contains **testuser**, and set **Action** to **Block**.
2. Review the entries for your target websites that show traffic as blocked. There might be a delay of up to 20 minutes for entries to appear in the log.

## What you learned

In this exercise, you accomplished the following tasks:

- **Created a web content filtering policy:** You defined rules by using both FQDN-based blocking (specific domains) and category-based blocking (gambling as a web category).
- **Understood the baseline profile:** You learned that the baseline profile applies to all internet traffic tunneled through GSA, which makes it ideal for organization-wide protections.
- **Linked policies to security profiles:** You learned that policies must be linked to a security profile. Security profiles must be linked to Conditional Access policies to be assigned to users and take effect. The baseline security profile (used in this tutorial) doesn't require Conditional Access and applies to all internet traffic.
- **Observed the "connection reset" error:** You learned that without TLS inspection, GSA can only drop the connection, which results in a generic browser error rather than a helpful message.

### Deep dive: Why did the "connection reset" error appear?

When TLS inspection isn't enabled, security service edge (SSE) can see:

- The destination IP address.
- The server name indication in the TLS handshake, which reveals the FQDN, like `www.bing.com`.

But it can't see:

- The full URL path, like `www.google.com/images` or `www.google.com/maps`.
- The HTTP request/response content.

Because the SSE can't inject content into an encrypted stream, it can only terminate the connection. The result is a "connection reset" error. In the next tutorial, you enable TLS inspection to unlock richer capabilities, including custom block pages.