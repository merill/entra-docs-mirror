---
layout: Conceptual
title: Create content policies for network content filtering - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-network-content-filtering
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Discover how to configure network content filtering with Global Secure Access to enforce data protection policies for files and text content in real time.
ms.topic: how-to
ms.date: 2026-06-30T00:00:00.0000000Z
ms.reviewer: absinh
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: bb976507-a008-e0aa-ba8f-21593ab09d32
document_version_independent_id: bb976507-a008-e0aa-ba8f-21593ab09d32
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-network-content-filtering.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-network-content-filtering
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-network-content-filtering.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cb8a1cfd-ba57-af6a-f350-78ffbbc4b706
---

# Create content policies for network content filtering - Global Secure Access | Microsoft Learn

Microsoft Entra Global Secure Access content policies provide real-time control over what users and agents share with generative AI applications, unmanaged cloud apps, and other internet destinations. These controls apply to content shared from managed endpoints through browsers, applications, add-ins, APIs, and more. **Basic content filtering** lets you block specific content types from being shared with selected destinations. **Scan with Purview** enables network data security by combining Microsoft Purview's data loss prevention (DLP) with identity-centric Global Secure Access policies. It inspects files and text for sensitive information and helps prevent data loss by blocking its sharing based on your *Purview DLP policies*. By combining content inspection with real-time user risk evaluation, you can enforce granular controls over sensitive data movement across the network without compromising user productivity or security posture.

### High-level architecture

[![Diagram showing the architecture of network content filtering with Global Secure Access and Microsoft Purview.](media/how-to-network-content-filtering/network-content-filtering-architecture.png)](media/how-to-network-content-filtering/network-content-filtering-architecture.png#lightbox)

This article explains how to create a content policy to filter internet traffic flowing through Global Secure Access.

Note

Basic content policy detects the file MIME type and text type in payload and enforces the **Allow** or **Block** action in Global Secure Access. Microsoft Purview is only involved when you choose **Scan with Purview**.

Caution

Use the **Block** action for HTML or JSON text types with caution. Web requests and responses commonly use HTML or JSON payloads, so blocking these text types can unintentionally block normal web and API traffic, including GET, POST, and PUT operations.

## Supported scenarios

Network content filtering supports the following key scenarios and outcomes for HTTP/S traffic:

- **Basic content filtering** is modeled in Content rule with action = **Allow** or **Block**. It lets you allow or block upload or download of files based on supported file MIME types. The same can be done for supported text types as well. This does not need Purview.
- **Scan with Purview** is modeled in Content rule with action = **Scan with purview**. Using this, you can audit and block selected file and text content based on:
    - Microsoft Purview sensitivity labels
    - Sensitive content in files or text
    - The user's risk level
- When you use **Scan with Purview**, you can generate Data Loss Prevention (DLP) admin alerts for rule matches.

## Prerequisites

To use the content policy feature, you need the following prerequisites:

- A valid Microsoft Entra tenant.
- Licensing for the product. For details, see the licensing section of [What is Global Secure Access](overview-what-is-global-secure-access). If needed, you can [purchase licenses or get trial licenses](https://aka.ms/azureadlicense).

    - A valid Microsoft Entra Internet Access license.
    - A valid Microsoft Purview license, required for **Scan with Purview** inspection.
    - You can use basic content filtering without a Purview license.
- A user with the [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role in Microsoft Entra ID to configure Global Secure Access settings.
- A [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator) role to configure Conditional Access policies.
- The Global Secure Access client requires a device (or virtual machine) that is either Microsoft Entra ID joined or Microsoft Entra ID Hybrid joined.
- To use **web categories** as a content policy destination, you must also configure any [web content filtering policy](how-to-configure-web-content-filtering).
- User Datagram Protocol (UDP) traffic (that is, QUIC) isn't supported. Most websites support fallback to Transmission Control Protocol (TCP) when QUIC can't be established. For an improved user experience, you can deploy a Windows Firewall rule that blocks outbound UDP 443:

    ```powershell
    New-NetFirewallRule -DisplayName "Block QUIC" -Direction Outbound -Action Block -Protocol UDP -RemotePort 443
    ```

## Initial configuration

To configure content policies, complete the following initial setup steps:

1. [Enable the Internet Access traffic forwarding profile](how-to-manage-internet-access-profile#enable-the-internet-access-traffic-forwarding-profile) and ensure correct user assignments.
2. [Configure the Transport Layer Security (TLS) inspection](how-to-transport-layer-security) policy.
3. Install and configure the Global Secure Access client:
    1. Install the Global Secure Access client on Windows or macOS. 
        Important

        Before you continue, test and ensure your client's internet traffic is routed through Global Secure Access. To verify the client configuration, see the steps in the following section.
    2. Select the **Global Secure Access** icon and select the Troubleshooting tab.
    3. Under **Advanced Diagnostics**, select **Run tool**.
    4. In the Global Secure Access Advanced Diagnostics window, select the **Forwarding Profile** tab.
    5. Verify that **Internet Access** rules are present in the **Rules** section. This configuration might take up to 15 minutes to apply to clients after enabling the Internet Access traffic profile in the Microsoft Entra admin center. [![Screenshot of the Global Secure Access Advanced Diagnostics window on the Forwarding Profile tab, showing Internet Access rules in the Rules section.](media/how-to-network-content-filtering/internet-access-rules.png)](media/how-to-network-content-filtering/internet-access-rules.png#lightbox)
4. Confirm access to web applications you plan for content policies.

## Configure a content policy

To configure a content policy in Global Secure Access, complete the following steps:

1. Create a content policy.
2. Link the content policy to a security profile.
3. Configure a Conditional Access policy.

### Create a content policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Content policies**. [![Screenshot of the Content policies page in the Microsoft Entra admin center showing the Create policy button.](media/how-to-network-content-filtering/content-policies-create.png)](media/how-to-network-content-filtering/content-policies-create.png#lightbox)
3. Select **+ Create Policy**. Pick the options that fit your needs.
4. On the **Basics**tab:
    1. Enter the policy **Name**.
    2. Enter the policy **Description**.
    3. Select **Next**. [![Screenshot of the Basics tab for a new content policy showing the Policy name and Description fields.](media/how-to-network-content-filtering/content-policy-basics-tab.png)](media/how-to-network-content-filtering/content-policy-basics-tab.png#lightbox)
5. On the **Rules**tab:
    1. Add a new rule.
    2. Enter the **Rule name**, **Description**, **Priority**, and **Status** as appropriate.
    3. Select the appropriate option for the **Action**menu:
        - To configure a basic content filtering, select **Allow** or **Block**.
        - To use data policies configured in Microsoft Purview, select **Scan with Purview**. [![Screenshot of the content rule screen with the Action menu expanded and the Scan with Purview option selected.](media/how-to-network-content-filtering/scan-with-purview.png)](media/how-to-network-content-filtering/scan-with-purview.png#lightbox)
    4. For **Matching conditions**, select the appropriate **Activities** and **Content types**.
        - For basic **content filtering**, select the file content types to allow or block.
            - (Optional) You can choose text type as well, but exercise caution as you should not end up blocking HTML or JSON text type that blocks your web traffic.
        - For **Scan with Purview**, select the file content types and text content types that you want Microsoft Purview to inspect. File content type selection is optional for text-only scenarios. [![Screenshot of the Add Content Rule page showing the Matching conditions section with Activities set to Upload, and the Content types dropdown expanded with PDF selected.](media/how-to-network-content-filtering/content-rule-content-types.png)](media/how-to-network-content-filtering/content-rule-content-types.png#lightbox)
    5. (Optional) Configure the **Session type** condition to scope the rule by traffic origin. Select **Agent** to match traffic classified as AI agent traffic. Traffic that is not classified as agent traffic is treated as **User** traffic. If not configured, the rule applies to all traffic.
    6. Select **+ Add destination**and configure the destinations.
        - For application-specific control, you can add the exact URLs and related FQDNs that the app uses. Use browser developer tools or network traffic analysis to identify the endpoints used during file upload, text submission, or other protected traffic.
        - You can also select web categories as a destination. If you select web categories, you must also configure a [web content filtering policy](how-to-configure-web-content-filtering).
6. Select **Next**.
7. On the **Review** tab, review your settings. [![Screenshot of the Review tab showing a summary of the content policy settings including policy name, description, and number of rules before creation.](media/how-to-network-content-filtering/content-policy-review-tab.png)](media/how-to-network-content-filtering/content-policy-review-tab.png#lightbox)
8. Select **Create** to create the policy.

Important

If you choose the **Scan with Purview** action in a content policy rule, you must also configure a corresponding DLP policy in Microsoft Purview that targets inline web traffic. Without a matching Purview DLP policy, the content policy can't inspect selected file or text content or enforce audit or block decisions. See Configure a Purview DLP policy for network data security for step-by-step guidance and Example: Block sensitive text sent through Gmail for a concrete scenario.

### Link the content policy to a security profile

1. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**.
2. Select the security profile you want to modify.
3. Switch to the **Link policies** view.
4. Configure the link content policy:
    1. Select **+ Link a policy** &gt; **Existing Content policy**.
    2. From the **Policy name** menu, select the content policy you created.
    3. Keep the default values for **State**.
    4. Select **Add**.
5. Close the security profile.

### Configure a Conditional Access policy

To enforce the Global Secure Access security profile, create a Conditional Access policy with the following configuration:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Identity** &gt; **Protection** &gt; **Conditional Access**.
3. Select **+ Create new policy**.
4. Name the policy.
5. Select the users and groups to apply the policy to.
6. Set the **Target resources** to **All internet resources with Global Secure Access**.
7. Configure the **Network**, **Conditions**, and **Grant** sections according to your needs.
8. Under **Session**, select **Use Global Secure Access Security Profile** and select the security profile you created.
9. To create the policy, select **Create**.

For more information, see [Create and link a Conditional Access policy](how-to-configure-web-content-filtering#create-and-link-conditional-access-policy).

The content policy is successfully configured.

## Configure a Purview DLP policy for network data security

If you selected the **Scan with Purview** action in your content policy, you must configure a corresponding data loss prevention (DLP) policy in Microsoft Purview. The DLP policy defines how Purview classifies and acts on file and text content that Global Secure Access routes for inspection.

Note

If you don't see **Data loss prevention** in Microsoft Purview, your account might not have the required permissions or your tenant might not have the required licensing. You need a role such as **DLP Compliance Management** or **Information Protection Admin**, and a Microsoft 365 E5/A5 subscription or a Microsoft Purview DLP add-on. For more information, see [Permissions in the Microsoft Purview portal](/en-us/purview/purview-permissions).

### Create a DLP policy for network data security

1. Sign in to the [Microsoft Purview portal](https://purview.microsoft.com).
2. Select **Data loss prevention** &gt; **Policies** &gt; **+ Create policy**.
3. Select **Inline web traffic**.
4. Select **Custom** from the **Categories** list and then select **Custom policy** from the **Regulations** list.
5. Select **Next**.
6. Enter a policy name and description, then select **Next**.
7. Configure the cloud apps to monitor:
    1. Select **+ Add cloud apps**.
    2. On the **Adaptive app scopes** tab, choose the app categories you want to protect against (for example, **All unmanaged AI apps**).
    3. Select **Add**.
8. Select **Next**.
9. On the **Choose where to enforce the policy** page, ensure **Network and non-Microsoft secure browsers** is enabled, then select **Next**.
10. Select **Create or customize advanced DLP rules** and select **Next**.
11. Select **+ Create rule**and configure the rule:
    1. Enter a **Name** and optional description.
    2. Under **Conditions**, select **+ Add condition** &gt; **Content contains**.
    3. Add the **sensitive information types** or **sensitivity labels** that match your organization's data protection requirements.
    4. Under **Actions**, select **+ Add an action** &gt; **Restrict browser and network activities**.
    5. Select the actions that match your content policy scenario and set each action to **Audit** or **Block**as appropriate:
        - **Text sent to or shared with cloud or AI apps**
        - **Text received from cloud or AI apps**
        - **File uploaded to or shared with cloud or AI apps**
        - **File downloaded from cloud or AI apps**
    6. Configure **Incident reports** and alert settings as needed.
    7. Select **Save**.
12. Review the rule, ensure its status is **On**, and select **Next**.
13. On the **Policy mode** page, choose **Turn the policy on immediately** or run in simulation mode first to test.
14. Select **Next**, review the policy, and select **Submit**.

Note

The actions you select in the Purview DLP rule should match the content types and activities you selected in the Global Secure Access content policy. For text inspection scenarios, include the applicable text actions in the Purview DLP rule.

For a detailed walkthrough with example configurations, see [Use Network Data Security to help prevent sharing sensitive information with unmanaged AI](/en-us/purview/dlp-create-policy-ai-network-data-security).

## Test the network content filtering with Purview

Test the configuration by attempting to upload or download files, or send text content, that matches the content policy conditions. Verify that the policy settings audit or block the actions.

### Example: Block sensitive text sent through Gmail

This example walks through an end-to-end test scenario that blocks text containing sensitive data, such as credit card numbers or Social Security numbers, from being sent in a Gmail message body.

#### Step 1: Configure the content policy destination

When you create or edit your content policy rule, configure the following settings:

- **Action**: Select **Scan with Purview**.
- **Activities**: Select **Upload**.
- **Text content types**: Select the text content types that you want Microsoft Purview to inspect.
- **Destination**: Add `mail.google.com` as an FQDN.

For text-only scenarios, you don't need to select a file content type.

#### Step 2: Configure a Purview DLP policy

If you select **Scan with Purview** as the content policy action, you must also configure a corresponding Microsoft Purview DLP policy to inspect the text content and make the audit or block decision.

1. In the [Microsoft Purview portal](https://purview.microsoft.com), create an **Inline web traffic** DLP policy.
2. On the **Choose where to enforce the policy** page, ensure **Network and non-Microsoft secure browsers** is enabled.
3. Configure the DLP rule to detect the sensitive information types you want to block, such as credit card numbers or Social Security numbers.
4. Under **Actions**, select **Restrict browser and network activities**.
5. Select **Text sent to or shared with cloud or AI apps** and set the action to **Block**.
6. Configure incident reports and alert settings as needed.
7. Save and apply the policy.

#### Step 3: Validate the policy

1. On a managed device with the Global Secure Access client installed, open a browser and go to [Gmail](https://mail.google.com).
2. Create a message that contains sensitive data, such as sample credit card numbers or Social Security numbers.
3. Attempt to send the message.
4. Verify that the message is blocked.
5. To confirm the block, check the traffic logs in the Microsoft Entra admin center under **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
6. Review the corresponding alert or activity details in Microsoft Purview.

### Example: Block sensitive PDF uploads to ChatGPT

This example walks through an end-to-end test scenario that blocks a PDF file containing sensitive data (such as credit card numbers or Social Security numbers) from being uploaded to ChatGPT.

#### Step 1: Configure the content policy destinations

When you create or edit your content policy rule, don't add only `chatgpt.com`. Add the specific URLs and FQDNs that match ChatGPT file upload traffic:

- `https://chatgpt.com/backend-api/files` (add as URL)
- `https://chatgpt.com/backend-api/files/process_upload_stream` (add as URL)
- `*.oaiusercontent.com` (add as FQDN)

For **Content types**, select **PDF** and other file types you want to inspect.

Tip

Web applications often use multiple URLs and FQDNs under the hood. Use browser developer tools or network traffic analysis to identify the correct upload endpoints for your target destination. For ChatGPT, the URLs listed here are the endpoints used for file upload operations.

#### Step 2: Configure a Purview DLP policy (for Scan with Purview action)

If you select **Scan with Purview** as the content policy action, you must also configure a corresponding Microsoft Purview DLP policy to inspect the file content and make the audit or block decision.

1. Sign in to the [Microsoft Purview portal](https://purview.microsoft.com).
2. Follow the steps in [Use Network Data Security to help prevent sharing sensitive information with unmanaged AI](/en-us/purview/dlp-create-policy-ai-network-data-security#steps-to-create-policy)to create a new DLP policy.
    1. In the **Cloud apps** step, search for and add **ChatGPT**.
    2. Configure the DLP rule to detect the sensitive information types you want to block (for example, credit card numbers or Social Security numbers).
    3. Set the rule action to **Block**.
3. Save and apply the policy.

For more information about Purview DLP policies for network traffic, see [Learn about Microsoft Purview Network Data Security](/en-us/purview/dlp-network-data-security-learn).

Note

Global Secure Access forwards matching upload traffic to Microsoft Purview for content inspection. Purview evaluates the content against your DLP policy and returns a decision based on your DLP rule action. Global Secure Access then enforces the result.

#### Step 3: Validate the policy

1. On a managed device with the Global Secure Access client installed, open a browser and go to [ChatGPT](https://chatgpt.com).
2. Prepare a test PDF file that contains sensitive data, such as sample credit card numbers or Social Security numbers. You can use a [sample file from dlptest.com](https://dlptest.com/sample-data.pdf).
3. In ChatGPT, attempt to upload the test PDF file.
4. Verify that the upload is blocked. ChatGPT displays an error message because Global Secure Access prevented the file transfer.
5. To confirm the block, check the traffic logs in the Microsoft Entra admin center under **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.
6. If you use **Scan with Purview**, also review the matching alert or activity details in Microsoft Purview. For more information, see [Get started with the data loss prevention Alerts dashboard](/en-us/purview/dlp-alerts-dashboard-get-started) and [Get started with activity explorer](/en-us/purview/data-classification-activity-explorer).

## Known limitations

### Known internet access limitations

For more information, see [Current known limitations](/en-us/reference-current-known-limitations.md#internet-access-limitations)

### Known GSA network content filtering limitations

- Network content filtering is supported with the Internet access profile only
- When using web categories as destinations within Content rules, you must have a web filtering policy in place applied to one or more web categories (allow or block).
- When using wildcards (\*) in Content rule destinations, they cannot be used for top-level domains (TLD) or second-level domains (SLD). For example, \*.contoso.com is supported, however *.com and contoso.* are not supported.
- File detection is limited to files transferred as request/response bodies unencoded and with multipart encoding. Certain file transfer methods may prevent inspection, such as if an application encodes a file within a JSON, or the file is broken up into multiple encrypted requests.
- WebSocket traffic bypasses file-type filtering in Content policy rules. Text content type is still evaluated within web sockets.
- Requests are subject to API rate limiting based on usage. When limits are exceeded, traffic is automatically blocked (fail-closed).

### Known Purview DLP limitations

- The maximum supported content size for **Scan with Purview** is 3 MB for both file and text content types.
- OCR is not yet supported for traffic sent to Purview.
- Scan with Purview only applies to traffic associated with an Entra user identity. Traffic that cannot be mapped to an Entra user identity is not sent to Purview for inspection.
- In scenarios where Purview inspection is unable to complete, such as a payload that is too large to inspect, or an internal error, the traffic is allowed (fail-open). Transactions that have skipped inspection can be identified in Traffic logs using **PurviewStatus** field.

## Monitoring and logging

### Review Global Secure Access traffic logs

To view traffic logs:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader).
2. Select **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.

### Review Microsoft Purview investigation data

If you use **Scan with Purview**, review the corresponding investigation data in Microsoft Purview:

1. Sign in to the [Microsoft Purview portal](https://purview.microsoft.com).
2. To review DLP alerts and their associated events, go to **Data loss prevention** &gt; **Alerts**. For more information, see [Get started with the data loss prevention Alerts dashboard](/en-us/purview/dlp-alerts-dashboard-get-started).
3. To investigate matching activities, open **Activity explorer** and filter for **Network DLP activities** or the policy, user, or app you want to review. For more information, see [Get started with activity explorer](/en-us/purview/data-classification-activity-explorer).

Note

Purview alerts and Activity explorer apply only when you use **Scan with Purview**. If you use basic content policy with **Allow** or **Block** actions, review the Global Secure Access traffic logs instead.