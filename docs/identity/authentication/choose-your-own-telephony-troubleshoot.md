---
layout: Conceptual
title: Troubleshoot SMS and voice with your own telecom provider - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/choose-your-own-telephony-troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Trace CYOT SMS and voice requests with audit logs, sign-in logs, and Function App logs to identify issues and contact the right support team.
ms.topic: how-to
ms.date: 2026-10-30T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1012
ms.reviewer: xueca
locale: en-us
document_id: c6feb436-7002-6126-f9ac-a19f4deeb894
document_version_independent_id: c6feb436-7002-6126-f9ac-a19f4deeb894
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/choose-your-own-telephony-troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/choose-your-own-telephony-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/choose-your-own-telephony-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 1a61b24c-d1b3-96ac-ce83-038be39e309a
---

# Troubleshoot SMS and voice with your own telecom provider - Microsoft Entra ID | Microsoft Learn

Use this article to trace SMS and voice requests end to end with Choose Your Own Telephony Provider (CYOT), find where a request stopped, and contact the right team to resolve it: Microsoft support, your Azure team, or your telecom provider.

## How a CYOT request flows

Each request passes through four stages, and each stage is recorded in its own logs:

| Stage | What happens | Where to look |
| --- | --- | --- |
| 1. Microsoft Entra sends the request | Microsoft Entra requires an SMS or voice code and sends the request to your endpoint. | Microsoft Entra audit logs |
| 2. Your endpoint processes it | Your Function App receives the request and sends it to your telecom provider. | Function App logs |
| 3. Your provider delivers it | Your provider sends the SMS message or voice call to the user's phone. | Your provider's portal |
| 4. The user signs in | The user enters the code, and Microsoft Entra completes authentication. | Microsoft Entra sign-in logs |

## Find the request in audit logs

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a Reports Reader.
2. Go to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**, and select the **Directory** tab.
3. Set the **Date range**, and add these filters: **Service: Azure MFA** and **Category: Authentication**.
4. Leave **Activity** set to **All** so you see both successful and failed requests.

[![Screenshot of Audit logs filtered by Service Azure MFA and Category Authentication, showing CyotDeliverySucceeded and CyotDeliveryFailed activities.](media/choose-your-own-telephony-troubleshoot/audit-logs.png)](media/choose-your-own-telephony-troubleshoot/audit-logs.png#lightbox)

Select the request to open **Audit Log Details**, and note these values:

| Field | What it tells you |
| --- | --- |
| Activity Type | `CyotDeliverySucceeded` means your endpoint accepted the request. `CyotDeliveryFailed` means it didn't complete. |
| DeliveryMethod | `Cyot` for a live request through your provider. `CyotEvaluation` for an evaluation request. |
| Channel | `Sms` or `Voice`. |
| AuthenticationMethod | The method used, such as `OneWaySms` or `OneWayVoiceMobileOtp`. |
| Correlation ID | The identifier to share with support. |
| FailureReason | Why a failed request didn't complete. |

[![Screenshot of Audit Log Details for CyotDeliverySucceeded with DeliveryMethod Cyot and Channel Voice.](media/choose-your-own-telephony-troubleshoot/audit-log-details.png)](media/choose-your-own-telephony-troubleshoot/audit-log-details.png#lightbox)

## Check sign-in logs

Use sign-in logs to confirm whether the user completed authentication.

1. Go to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
2. Find the sign-in by user and time, and open it.
3. On **Authentication Details**, review the method, whether the step succeeded, and the result detail.

Sign-in logs show the method as **Text message** or **Voice**. To confirm that the request was sent through your provider, use audit logs.

## Check Function App logs

Use your Function App logs to see how your endpoint processed the request and what it returned to Microsoft Entra.

1. In the Azure portal, open the Function App created by setup.
2. Go to **Monitoring** &gt; **Application Insights**, and open the linked Application Insights resource.
3. Select **Logs**, and run the following query for the time of the attempt:

    ```kusto
     AppRequests
     | where TimeGenerated > ago(1h)
     | where Url has "/api/SendOtp"
     | project TimeGenerated, ResultCode, Success, DurationMs, OperationId
     | order by TimeGenerated desc
    ```

`ResultCode` shows what your Function App returned to Microsoft Entra. To see your provider's response for the same request, query `AppTraces` with its `OperationId`.

## Identify who can help

Use what you see in audit logs to find the right contact.

| What you see | What to check | Contact |
| --- | --- | --- |
| No CYOT activity in audit logs | Confirm the date range and filters, that the user is included in SMS or voice targeting, and that a new phone challenge was required. | Microsoft support |
| Only `CyotEvaluation` activity | The profile is in **Evaluation**. Switch to **Production** to route traffic through your provider. | No support needed |
| `CyotDeliveryFailed` with `EndpointClientError` | Your endpoint rejected the request. Check your Function App logs and authentication settings. | Your Azure team |
| `CyotDeliveryFailed` with `EndpointServerError` | Your endpoint returned an error or didn't respond in time. Check your Function App logs and your provider's status. | Your Azure team |
| `CyotDeliveryFailed` with `NonceMismatch` | Your endpoint's response didn't match what Microsoft Entra expects. Compare any customizations with the CYOT sample. | Your Azure team |
| `CyotDeliverySucceeded`, but the user didn't receive the code | Your endpoint accepted the request. Check your provider's delivery records. | Your telecom provider |
| The user received the code, but sign-in failed | Check the sign-in logs for an expired, reused, or incorrect code. | Microsoft support |
| Delivery blocked to certain countries/regions, fraud blocks, or unexpected charges | Review your provider's fraud, destination, and spending controls. | Your telecom provider |

Tip

When a request times out, check your provider's records before you try again. Your provider might have already accepted the original request.

## Contact support

| Contact | Covers | How to reach |
| --- | --- | --- |
| Microsoft support | Authentication method policy, Microsoft Entra authentication, and the request to your endpoint | [Get support for Microsoft Entra](/en-us/entra/fundamentals/how-to-get-support) |
| Your Azure team | Your Function App, its configuration, and Azure resources | Internal. For Azure platform issues, contact Azure support. |
| Your telecom provider | Provider account, delivery, fraud controls, and usage charges | Support details in the provider's [Microsoft Security Store](https://securitystore.microsoft.com/) listing |

### Information to include

- Tenant ID, channel (SMS or voice), and the UTC time of the attempt.
- The audit log **Correlation ID**, `DeliveryMethod`, and `FailureReason`.
- Your provider's transaction ID, if available.
- Any recent configuration changes.