---
layout: Conceptual
title: Set up SMS and voice - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-set-up-sms-voice-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Deploy your telecom integration, validate evaluation mode, and gradually roll out SMS and voice delivery by using CYOT APIs.
ms.topic: how-to
ms.date: 2026-10-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: eb745f6f-2f68-f2a0-f425-dffee61e8aef
document_version_independent_id: eb745f6f-2f68-f2a0-f425-dffee61e8aef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-set-up-sms-voice-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-set-up-sms-voice-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-set-up-sms-voice-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cdc80360-921e-4b45-947f-2719acf06f23
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/539badf0-028a-4e3e-bda6-770b2552b4d8
platformId: d1478d6e-e3fe-f3ee-72af-76324d2160dd
---

# Set up SMS and voice - Microsoft Entra ID | Microsoft Learn

Use Choose Your Own Telephony Provider (CYOT) to deliver SMS and voice authentication through your organization's telephony provider. With CYOT, you purchase a supported provider offer through [Microsoft Security Store](https://securitystore.microsoft.com/), deploy the integration in your Azure subscription, and configure Microsoft Entra to route SMS or voice authentication through your provider.

This article walks you through the end-to-end setup, including purchasing your provider offer, deploying the integration, configuring the authentication method policy, and testing the experience before moving to production.

## How the integration works

CYOT uses an Azure Function in your Azure subscription to connect Microsoft Entra with your telephony provider. The Azure Function processes SMS or voice requests from Microsoft Entra and sends them to your provider for delivery.

![Diagram of the CYOT integration connecting Microsoft Entra to a telephony provider through an Azure Function in your Azure subscription.](media/concept-phone-providers/telephony-provider-integration-diagram.jpeg)

## Prerequisites

Before you begin, prepare:

- A Microsoft Entra workforce tenant.
- An Azure subscription with a valid payment method to host the integration and subscribe to your provider. See [Security Store purchasing prerequisites](/en-us/security/store/customers/how-to-purchase-a-saas-solution-and-deploy-a-linked-solution#prerequisites).
- [Azure Cloud Shell](/en-us/azure/cloud-shell/overview) in PowerShell mode (recommended), or PowerShell 7.0+ with Azure CLI 2.61+ for integration deployment.
- A test user with a phone number registered for SMS or voice authentication.

## Required permissions

Use accounts with the following permissions:

| Task | Required access | Why it's needed |
| --- | --- | --- |
| Create the application | Permission to register applications in the customer tenant | Lets setup create the application that securely connects Microsoft Entra to your integration. |
| Deploy Azure resources | Subscription Owner, or Contributor + Role Based Access Control Administrator at the required scope | Lets setup deploy the integration in your subscription. |
| Grant directory access during deployment | Privileged Role Administrator | Lets setup grant the directory permissions that Microsoft Entra needs to route requests to your integration. |
| Read authentication method policy | Delegated `Policy.Read.AuthenticationMethod` permission and a supported role, such as Authentication Policy Administrator | Allows setup to read the existing SMS or voice authentication method configuration. |
| Update authentication method policy | Authentication Policy Administrator and delegated `Policy.ReadWrite.AuthenticationMethod` permission | Allows setup to configure the SMS or voice authentication method to use the integration. |

Important

Before you begin, confirm that your Microsoft Entra policies allow the setup script to create the application and credentials it needs. If you use app management policies for credentials, multitenant apps, or custom Application ID URIs, review them with your Microsoft Entra administrator.

## Step 1: Purchase and activate your telecom provider

1. Purchase your provider's offer from [Microsoft Security Store](https://securitystore.microsoft.com/). For detailed purchasing instructions, see [Purchase and deploy a SaaS solution from Security Store](/en-us/security/store/customers/how-to-purchase-a-saas-solution-and-deploy-a-linked-solution).
2. After you **Place Order**, select **Configure Account Now** and follow your provider's registration instructions.
3. Keep this page available and continue to step 2. You'll complete registration in step 3 with the application ID from the deployment summary.

## Step 2: Deploy the integration

Use Azure Cloud Shell in PowerShell mode to run the setup script for the telecom provider you select.

### What the setup script does

The setup script deploys everything needed to connect Microsoft Entra ID to your telecom provider, so you don't have to create Azure resources by hand. It walks you through a few choices, then shows the full deployment plan. Nothing is created until you approve it.

After you approve, the script creates the Microsoft Entra application, deploys and secures the Azure resources, and applies your provider's configuration. Deployment usually takes a few minutes.

### Costs

Important

The integration runs on Azure resources in your subscription, billed based on your configuration and usage. To plan your budget, see [Estimate telecom-provider and Azure hosting costs](phone-providers-faq#how-much-does-choose-your-own-telephony-provider-cost) before you deploy.

### Run the setup script

1. Sign in to the Azure portal and select the **Cloud Shell** icon (**&gt;\_**) in the top toolbar. You can also go directly to https://shell.azure.com.
2. Select **PowerShell**. If Cloud Shell opens in Bash, select **Switch to PowerShell** in the toolbar.
3. If this is your first time, select **No storage account required**, choose your subscription, and then select **Apply**.
4. Download and review the [setup script](https://github.com/Azure-Samples/ExternalPhoneProvider-AzureFunction-Sample/blob/main/setup/Setup-Epp.ps1):

    ```powershell
    Invoke-WebRequest -Uri 'https://raw.githubusercontent.com/Azure-Samples/ExternalPhoneProvider-AzureFunction-Sample/main/setup/Setup-Epp.ps1' `
        -OutFile '.\Setup-Epp.ps1'
    ```
5. Run the script.

    ```powershell
    .\Setup-Epp.ps1
    ```
6. Follow the prompts to select the customer tenant, hosting subscription, Azure region, telecom provider, runtime, and hosting plan, then approve the deployment plan.
7. Save the deployment summary, including its tenant ID, endpoint URL, and **Application (client) ID**. You need these values to complete provider registration and configure your profile.

Important

Copy these values before you leave the Cloud Shell window. Cloud Shell sessions are temporary and can end when you navigate away, and the output isn't saved.

## Step 3: Complete telecom provider registration

After deployment completes, return to your telecom provider's registration page to complete the provider setup.

1. Provide the **Application (client) ID** from your Microsoft Entra application when requested by your telecom provider.
2. Complete any additional registration steps required by the provider.
3. In [Microsoft Security Store](https://securitystore.microsoft.com/), go to **Management** &gt; **My Solutions** and confirm that the **Subscription status** is '**Subscribed**' before continuing.

Important

Complete the telecom provider registration before configuring Microsoft Entra to send authentication traffic through the provider.

## Step 4: Update the authentication method policy

Configure each channel with the endpoint URL and application client ID from the deployment summary. Start in evaluation mode, validate the integration, and then gradually move delivery to your telecom provider.

Warning

CYOT updates your existing SMS or voice authentication method policy, so any change also applies to current SMS and voice users. Before you update the policy, save the full JSON response from Read the current policy. In production, keep your existing `includeTargets` unchanged, and use evaluation mode and `migrationPercentage` to roll out gradually. Test targeting changes in a test tenant.

### Read the current policy

Use [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read and update the policy. Confirm that you're signed in to the tenant whose ID matches the Tenant ID in the deployment summary.

Use these request URLs for the corresponding channel:

| Channel | Request URL |
| --- | --- |
| SMS | `https://graph.microsoft.com/beta/policies/authenticationMethodsPolicy/authenticationMethodConfigurations/Sms` |
| Voice | `https://graph.microsoft.com/beta/policies/authenticationMethodsPolicy/authenticationMethodConfigurations/Voice` |

1. Set the request method to **GET** and enter the corresponding channel's request URL.
2. Open **Modify permissions** and consent to `Policy.Read.AuthenticationMethod`.
3. Select **Run query** and save the complete JSON response as a record of the existing policy.
4. Repeat for the other channel if you're configuring both SMS and voice.

Important

When you prepare the updated policy, use the saved response to preserve your existing `includeTargets` and other intended authentication method settings.

### Configure CYOT settings

Configure these properties:

| Property | Value |
| --- | --- |
| `telecomProviderSettings.url` | Endpoint URL from the deployment summary. |
| `telecomProviderSettings.appId` | Integration application client ID. |
| `telecomProviderSettings.isEvaluationModeEnabled` | Set to `true` for evaluation mode or `false` to enable telecom provider delivery. |
| `telecomProviderSettings.migrationPercentage` | Percentage of eligible authentication requests sampled during evaluation, or routed to your telecom provider when evaluation mode is disabled. |
| `includeTargets` | Preserve the existing production configuration. These targets are shared with the existing SMS or voice authentication method policy. |

### Start in evaluation mode

Start in evaluation mode to validate the integration before moving authentication delivery to your telecom provider.

Use `migrationPercentage` to set the evaluation sampling percentage.

1. Use the tested SMS or voice JSON example provided below in **Request body**.
2. Replace the endpoint URL and application client ID with the values for your deployment.
3. Set `isEvaluationModeEnabled` to `true`.
4. For production tenants, preserve the existing `includeTargets` from your saved policy configuration. Do not replace existing production targeting for CYOT testing.
5. Open **Modify permissions**, consent to `Policy.ReadWrite.AuthenticationMethod`, and send the **PATCH** request to the corresponding channel's URL.
6. Read the policy again with **GET** and verify the endpoint URL, application client ID, evaluation-mode setting, migration percentage, and existing targets.
7. Complete the evaluation-mode tests in step 5.

Important

The JSON examples below contain the tested configuration values. Before using an example, replace the endpoint URL and application client ID with the values for your deployment.

For evaluation mode, set `isEvaluationModeEnabled` to `true`. In a production tenant, preserve the `includeTargets` from your existing SMS or voice policy. Use a test tenant if you want to validate CYOT with different target users or groups.

For SMS:

```json
{
  "@odata.type": "#microsoft.graph.smsAuthenticationMethodConfiguration",
  "state": "enabled",
  "telecomProviderSettings": {
    "url": "<YOUR-ENDPOINT-URL>",
    "appId": "<YOUR-APPLICATION-CLIENT-ID>",
    "isEvaluationModeEnabled": false,
    "migrationPercentage": 100
  }
}
```

For Voice:

```json
{
  "@odata.type": "#microsoft.graph.voiceAuthenticationMethodConfiguration",
  "state": "enabled",
  "includeTargets": [
    {
      "verificationMode": "voiceOneTimePasscode"
    }
  ],
  "telecomProviderSettings": {
    "url": "<YOUR-ENDPOINT-URL>",
    "appId": "<YOUR-APPLICATION-CLIENT-ID>",
    "isEvaluationModeEnabled": false,
    "migrationPercentage": 100
  }
}
```

### Move to production mode

After evaluation succeeds:

1. Set `telecomProviderSettings.isEvaluationModeEnabled` to `false`.
2. Set `telecomProviderSettings.migrationPercentage` to your initial traffic percentage.
3. Keep the existing production `includeTargets` unchanged.
4. Submit the policy update.
5. Read the configuration again and verify the endpoint URL, application client ID, evaluation mode, migration percentage, and targets.
6. Test telecom provider delivery before increasing traffic.

### Increase traffic gradually

1. Keep `isEvaluationModeEnabled` set to `false`.
2. Increase `migrationPercentage` in increments until you reach `100`.
3. Keep the endpoint URL, application client ID, and existing `includeTargets` unchanged while changing the migration percentage.
4. Validate authentication and telecom provider delivery after each change.
5. Increase the percentage after each stage validates successfully. To investigate an issue, hold at the current percentage and see [Monitor and troubleshoot](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider).

Important

When each stage validates successfully, continue to 100 percent without delay. Completing your rollout early helps ensure uninterrupted authentication for your users. For dates, see [Passkeys by default and retirement of Microsoft-provided SMS and voice authentication](concept-sms-voice-retirement).

## Step 5: Test the integration

Use a test user with a phone number registered for SMS or voice.

### Test in Evaluation

1. In an InPrivate browser session, sign in as the test user and complete an SMS or voice authentication.
2. In the Azure portal, go to your **Function App** &gt; **SendOtp** &gt; **Invocations** and open the latest transaction. In **Invocation details**, confirm **Evaluation request completed** with HTTP `200`.
3. In the Microsoft Entra admin center, go to **Monitoring & health** &gt; **Audit logs** and filter by **Service: Azure MFA**. Open the latest entry and confirm **DeliveryMethod** is `CyotEvaluation`.

### Test provider delivery

After evaluation succeeds, set `isEvaluationModeEnabled` to `false` and configure your initial `migrationPercentage`.

1. In a new InPrivate browser session, sign in as the test user. Confirm the SMS or voice code arrives and authentication completes.
2. In the Azure portal, go to your **Function App** &gt; **Invocations** and open the latest transaction. In **Invocation details**, confirm the request completed with HTTP `200`.
3. In the Microsoft Entra admin center, go to **Audit logs** and filter by **Service: Azure MFA**. Open the latest entry and confirm **Delivery Method** is `Cyot`.
4. In your provider's portal, confirm the message was delivered.

At a partial percentage, only some requests route through your provider, so make a few attempts. If something doesn't look right, see [Monitor and troubleshoot your own telephony provider](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider).

## Troubleshooting

To diagnose integration issues, use the troubleshooting guide to identify whether the issue is with the Microsoft Entra configuration, Azure Function, telecom provider, or authentication flow.

See [Monitor and troubleshoot your own telephony provider](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider) for diagnostic steps, logs, common issues, and remediation guidance.