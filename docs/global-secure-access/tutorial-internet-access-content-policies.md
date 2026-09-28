---
layout: Conceptual
title: 'Tutorial: Configure Content Policies - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-internet-access-content-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure content policies in Global Secure Access to block file uploads and downloads to unauthorized destinations.
ms.topic: tutorial
ms.date: 2026-04-16T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 44e30010-907b-a4a1-5fb9-9c8e426a39e9
document_version_independent_id: 44e30010-907b-a4a1-5fb9-9c8e426a39e9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-internet-access-content-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-internet-access-content-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-internet-access-content-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
platformId: e7e40d7c-76ae-9143-86bb-92104d1a7054
---

# Tutorial: Configure Content Policies - Global Secure Access | Microsoft Learn

Network content filtering in Microsoft Entra Internet Access allows administrators to use content policies to prevent the transport of specific file types over the network. This feature helps protect sensitive data by blocking uploads and downloads of certain file formats (such as .doc, .docx, .pdf, and .zip) to and from web applications like ChatGPT, Gmail, and file-sharing apps. It can also use Microsoft Purview to scan files and apply network-level policies based on document sensitivity labels.

In this tutorial, you learn how to:

- Create a content policy to block specific file types from being uploaded.
- Link the content policy to a security profile.
- Verify that file upload blocking works as expected.

## Key concepts

### Why are content policies critical?

Content policies address a key data exfiltration vector, which is users who intentionally or accidentally upload sensitive files to unauthorized destinations.

| Threat scenario | Example | Content policy solution |
| --- | --- | --- |
| Shadow AI data leakage | Employee pastes confidential contract into ChatGPT. | Block document uploads to `*.oaiusercontent.com`. |
| Personal email exfiltration | Employee emails customer database to personal Gmail. | Block uploads to `mail.google.com`. |
| Unauthorized cloud storage | Employee syncs work files to personal Dropbox. | Block uploads to `*.dropbox.com`. |
| Insider threat | Malicious employee downloads sensitive files before leaving. | Block downloads of specific file types. |

### How content policies work with TLS inspection

```
User attempts upload     GSA client      SSE with TLS inspection     Destination
         │                    │                     │                      │
         │  Upload file.pdf   │                     │                      │
         ├───────────────────>│                     │                      │
         │                    │  Tunnel traffic     │                      │
         │                    ├────────────────────>│                      │
         │                    │                     │  Decrypt & inspect   │
         │                    │                     │  ┌───────────────┐   │
         │                    │                     │  │ File type: PDF│   │
         │                    │                     │  │ Action: Upload│   │
         │                    │                     │  │ Dest: chatgpt │   │
         │                    │                     │  │ → BLOCK       │   │
         │                    │                     │  └───────────────┘   │
         │    Block message   │                     │                      │
         │<───────────────────┤                     │                      │
```

Content policies require Transport Layer Security (TLS) inspection to be enabled. Security service edge (SSE) can't detect file types within encrypted uploads unless the traffic is decrypted.

## Sample walkthrough videos

The following video demonstrates how to configure a content policy.

## Step 1: Create a content policy

1. From the Microsoft Entra admin center, browse to **Global Secure Access** &gt; **Secure** &gt; **Content policies**.
2. Select **Create policy**.
3. Enter a name and description for the policy. Select **Next**.
4. Select **Add rule**.
5. Enter the following information:

    - **Rule name:** Enter **Block uploads to ChatGPT and Gmail**.
    - **Description:** Enter a description (optional).
    - **Priority:** Select **120**.
    - **Status:** Select **Enabled**.
    - **Action:** Select **Block**.
    - **Activities:** Select the checkbox for **Upload**.
    - **Content types:** Select the checkboxes for **Word (97-2003)**, **Word Document**, and **PDF**.
6. Select **Add destination**, select **FQDN**, and then enter the following fully qualified domain names (FQDNs):

    - `*.oaiusercontent.com`
    - `mail.google.com`
    - `clients6.google.com`
    - `*.clients6.google.com`
7. Select **Add**.
8. Select **Add destination**, and then select **URL** and enter the following URLs:

    - `https://chatgpt.com/backend-api/files`
    - `https://chatgpt.com/backend-api/files/process_upload_stream`

    ![Screenshot that shows the content policy rule configuration.](media/tutorial-internet-access-content-policies/content-policy-configuration.png)

    Note

    Apps might use multiple URLs and FQDNs under the hood when you interact with them. In this example, ChatGPT uses `*.oaiusercontent.com` and Gmail uses `mail.google.com`. If you aren't seeing content policies applied, check with dev tools to confirm which URLs and FQDNs the app is using.
9. Select **Save**.
10. Select **Next**, and then select **Create**.

## Step 2: Link the policy to a security profile

1. After the policy is created, browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**.
2. Select the existing security profile from a previous tutorial.
3. Go to the **Link policies** pane.
4. Select **Link a policy**, and then select **Existing Content policy**.
5. Choose the content policy that you created and select **Add**.

Note

Verify that the security profile is assigned to a Microsoft Entra Conditional Access policy.

## Step 3: Verify file upload and download blocking

1. On your test device, open a browser, go to `www.chatgpt.com`, and sign in with an account of your choice.
2. Attempt to upload a PDF or Word document to ChatGPT, and verify that the upload fails.
3. Go to `mail.google.com`, and sign in with a Google account.
4. Attempt to upload a PDF or Word document to Gmail, and verify that the upload fails.

    ![Screenshot that shows a blocked file upload attempt.](media/tutorial-internet-access-content-policies/file-upload-blocked.png)

## Known limitations

Refer to [official documentation](/en-us/entra/global-secure-access/how-to-network-content-filtering#known-limitations) for the list of known limitations.

## What you learned

In this tutorial, you accomplished the following tasks:

- **Created a content policy to prevent data exfiltration:** You blocked specific document types from being uploaded to AI tools and personal email, which addresses a key data loss vector.
- **Understood FQDN discovery for apps:** You learned that web applications often use multiple back-end URLs, like `*.oaiusercontent.com` for ChatGPT.
- **Linked content policies to security profiles:** You learned that content policies follow the same security profile model, which you can use to target specific users via Conditional Access.
- **Combined multiple security controls:** You saw in this tutorial how content policies work alongside web content filtering, TLS inspection, and threat intelligence as part of a comprehensive security strategy.

### Identify application FQDNs

When you configure content policies, you need to know the actual FQDNs that are used by applications.

To discover the FQDNs, select **F12** to open the browser developer tools:

1. Open the **Network** tab.
2. Upload a file to the target app.
3. Look for `POST` requests with file content.

Use the application discovery feature to identify which apps are being used, and then create targeted content policies:

```
1. Discover shadow AI apps.
        ↓
2. Assess risk scores.
        ↓
3. Decide to block entirely or allow with content restrictions.
        ↓
4. Create content policy if allowing with restrictions.
```

### Best practices

- Start by blocking uploads to high-risk AI apps (or all AI apps with authorized exceptions).
- Consider blocking both uploads and downloads for maximum protection.
- Test policies with a pilot group before broad deployment.
- Communicate changes to users to avoid confusion.