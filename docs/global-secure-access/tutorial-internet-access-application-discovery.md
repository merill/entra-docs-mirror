---
layout: Conceptual
title: 'Tutorial: Discover applications and shadow IT - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/tutorial-internet-access-application-discovery
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to use application usage analytics in Global Secure Access to discover shadow IT and generative AI applications.
ms.topic: tutorial
ms.date: 2026-03-07T00:00:00.0000000Z
ms.subservice: entra-internet-access
ms.reviewer: jebley
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: cce723ca-4b01-c57d-9870-5c01ee47608d
document_version_independent_id: cce723ca-4b01-c57d-9870-5c01ee47608d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/tutorial-internet-access-application-discovery.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/tutorial-internet-access-application-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/tutorial-internet-access-application-discovery.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: e5a974e1-cc8c-090d-8868-18903bb33590
---

# Tutorial: Discover applications and shadow IT - Global Secure Access | Microsoft Learn

Application usage analytics gives IT admins actionable insights into their organization's app use by analyzing traffic patterns, data usage, and which users access which applications. Admins can use these analytics to identify shadow IT, generative AI apps, and potential security or compliance risks. Usage analytics helps organizations increase visibility, improve their security posture, and optimize app use across their environment.

In this tutorial, you learn how to:

- Generate internet network traffic to populate analytics data.
- Review cloud application analytics and usage insights.
- Identify generative AI applications and shadow IT in your organization.

## Key concepts

### What is shadow IT?

*Shadow IT* refers to applications and services that are used by employees without the IT department's knowledge or approval. This use creates risk such as the following examples.

| Risk category | Examples | Why it matters |
| --- | --- | --- |
| Data loss | Uploading files to personal cloud storage | Sensitive data leaves corporate control. |
| Compliance | Using apps that don't meet regulatory requirements | Health Insurance Portability and Accountability Act (HIPAA) and Sarbanes-Oxley Act violations. |
| Security | Using apps with poor security practices | Credential theft and malware delivery. |
| Licensing | Duplicating tools across teams | Wasted IT budget. |

#### Shadow AI: The new frontier

*Shadow AI* is the unauthorized use of AI tools by employees without approval or security clearance. Generative AI tools (ChatGPT, Claude, Gemini, and others) present unique challenges:

- Employees might paste sensitive data into prompts.
- Confidential information might be used to train AI models.
- Organizations lose visibility into AI-assisted decisions.
- AI is susceptible to prompt injection and jailbreaking.

#### Risk scores explained

Microsoft evaluates each discovered application and assigns a risk score based on:

- **General factors:** Popularity, data sovereignty, and company information availability.
- **Security factors:** Encryption, multifactor authentication support, audit logs, and penetration testing.
- **Compliance factors:** SOC 2, ISO 27001, and HIPAA certification.
- **Legal factors:** Data ownership, Microsoft Software License Terms, and data retention policies.

## Sample walkthrough videos

The following video demonstrates how to identify shadow AI with application discovery.

## Step 1: Generate internet traffic

For this exercise to produce useful data, open a browser on your test device (with the Global Secure Access client installed) and go to several of your favorite websites. *Be sure to browse to some AI websites* too. Some examples of AI websites include:

- `copilot.microsoft.com`
- `chatgpt.com`
- `claude.ai`
- `ai.google`

## Step 2: Review cloud application analytics

### View summarized information

1. From the Microsoft Entra admin center, browse to **Global Secure Access** &gt; **Applications** &gt; **Insights & Analytics**.
2. Review the information that appears on the widgets.

    The dashboard displays three key widgets.

    | Widget | Description |
    | --- | --- |
    | Application count | Shows total cloud applications, total private applications, and newly discovered segments. |
    | Application usage distribution | Shows usage by type (cloud versus private), aggregated by transactions, bytes sent, or bytes received. |
    | Application usage trend | Shows usage over time, aggregated by transactions, users, devices, or bytes. |

    ![Screenshot that shows the application discovery dashboard widgets.](media/tutorial-internet-access-application-discovery/application-discovery-dashboard.png)

### Investigate discovered applications

Cloud application analytics give admins visibility into the cloud applications that their organization uses, including generative AI applications. These insights help identify shadow IT and assess security and compliance risks.

1. Review the list of discovered cloud applications with the following details:

    - **Name**
    - **Categories**
    - **Risk score**
    - **Users**
    - **Sent bytes**
    - **Received bytes**
2. Optionally, select the column titles to reorder the lists. You can see the apps with the lowest risk score, the apps with the highest user counts, and more.

    ![Screenshot that shows the list of discovered cloud applications.](media/tutorial-internet-access-application-discovery/application-discovery-list.png)

### View app details and risk factors

1. Select the **Name** link for an application.
2. The Microsoft Entra App Gallery opens and shows:
    - **Overall Risk Score**.
    - **General**, **Security**, **Compliance**, and **Legal** tabs, which show risk factor details.

## Step 3: Identify generative AI applications

Cloud application analytics can help you identify generative AI applications that are used in your organization. Analytics can help you to assess and manage potential risks.

1. Browse to **Global Secure Access** &gt; **Applications** &gt; **Insights & Analytics** &gt; **Cloud Applications**.
2. Enable the **Generative AI apps and tools** toggle.

    ![Screenshot that shows the generative AI apps filter toggle.](media/tutorial-internet-access-application-discovery/application-discovery-generative-ai.png)
3. Review the filtered list that shows only generative AI applications accessed by users.
4. Evaluate each application's risk score and usage patterns.

## What you learned

In this tutorial, you accomplished the following tasks:

- **Discovered shadow IT in your organization:** You now have visibility into cloud applications that are being used, even apps that aren't sanctioned by IT.
- **Identified shadow AI applications:** You can use the generative AI filter to help you quickly find AI tools that might pose data leakage risks.
- **Understood application risk scoring:** You can prioritize remediation efforts based on risk scores across general, security, compliance, and legal factors.
- **Analyzed usage patterns:** You can see which apps have the most users, data transfer, or transactions to understand true business impact.

### From discovery to action

After you discover shadow IT or shadow AI, you can take actions to mitigate risks.

```
┌────────────────┐     ┌────────────────┐     ┌────────────────┐
│    Discover    │ →→→ │     Assess     │ →→→ │      Act       │
├────────────────┤     ├────────────────┤     ├────────────────┤
│ • View all     │     │ • Review risk  │     │ • Sanction app.│
│   discovered   │     │   scores.      │     │ • Block app.   │
│   apps.        │     │ • Check        │     │ • Apply file   │
│ • Filter by    │     │   compliance.  │     │   controls.    │
│   AI apps.     │     │ • Review user  │     │ • Monitor      │
│ • Sort by      │     │   count.       │     │   ongoing.     │
│   usage.       │     │ • Analyze data │     │ • Add to app   │
│                │     │    transfer.   │     │   governance.  │
└────────────────┘     └────────────────┘     └────────────────┘
```

#### Integration points

- Export data to Microsoft Defender for Cloud Apps for deeper investigation.
- Use discovered apps to inform web content filtering policies.
- Combine with content policies to prevent data upload to risky apps.
- Feed insights into security awareness training programs.