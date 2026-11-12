---
layout: Conceptual
title: Set up SMS and voice with your own telephony provider in the Microsoft Entra admin center - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/choose-your-own-telephony-set-up
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Use the Microsoft Entra admin center to set up your telephony integration, validate evaluation mode, and gradually roll out SMS and voice delivery.
ms.topic: how-to
ms.date: 2026-10-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: eb745f6f-2f68-f2a0-f425-dffee61e8aef
document_version_independent_id: eb745f6f-2f68-f2a0-f425-dffee61e8aef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/choose-your-own-telephony-set-up.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/choose-your-own-telephony-set-up
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/choose-your-own-telephony-set-up.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: d1478d6e-e3fe-f3ee-72af-76324d2160dd
---

# Set up SMS and voice with your own telephony provider in the Microsoft Entra admin center - Microsoft Entra ID | Microsoft Learn

Use Choose Your Own Telephony Provider (CYOT) to deliver SMS and voice authentication through your organization's telephony provider. With CYOT, you purchase a supported provider offer through [Microsoft Security Store](https://securitystore.microsoft.com/), deploy the integration in your Azure subscription, and configure Microsoft Entra to route SMS or voice authentication through your provider.

This article walks you through the end-to-end setup in the Microsoft Entra admin center, including purchasing your provider offer, deploying the integration, configuring the authentication method policy, and testing the experience before moving to production.

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
| Create the application during deployment | Permission to register applications in the customer tenant. | Lets setup create the application that securely connects Microsoft Entra to your integration. |
| Deploy Azure resources | Subscription Owner, or Contributor + Role Based Access Control Administrator at the required scope. | Lets setup deploy the integration in your subscription. |
| Grant directory access during deployment | Privileged Role Administrator. | Lets setup grant the directory permissions that Microsoft Entra needs to route requests to your integration. |
| Configure authentication method profiles | Authentication Policy Administrator. | Allows you to review existing SMS or voice settings and configure the integration in the Microsoft Entra admin center. |

Important

Before you begin, confirm that your Microsoft Entra policies allow the setup script to create the application and credentials it needs. If you use app management policies for credentials, multitenant apps, or custom Application ID URIs, review them with your Microsoft Entra administrator.

## Step 1: Purchase and activate your telephony provider

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an Authentication Policy Administrator.
2. Go to **Entra ID** &gt; **Authentication methods** &gt; **Policies** and select **Add telecom profile**. The **Set up an SMS or voice provider** page guides you through subscription, integration, and profile setup.

    [![Redacted screenshot of the Set up an SMS or voice provider page and its three setup tasks.](media/choose-your-own-telephony-set-up/setup-overview.png)](media/choose-your-own-telephony-set-up/setup-overview.png#lightbox)
3. Select **Subscribe to an SMS or voice provider** and choose a supported telephony provider. Use **Get solution** to open its offer in [Microsoft Security Store](https://securitystore.microsoft.com/), or select an existing subscription with **Select details**. See [Available telephony providers](concept-phone-providers#available-telephony-providers).

    [![Redacted screenshot of the telephony provider selection pane. Demo pricing and offer details are obscured.](media/choose-your-own-telephony-set-up/subscribe-telecom-provider.png)](media/choose-your-own-telephony-set-up/subscribe-telecom-provider.png#lightbox)
4. Purchase your provider's offer. For detailed purchasing instructions, see [Purchase and deploy a SaaS solution from Security Store](/en-us/security/store/customers/how-to-purchase-a-saas-solution-and-deploy-a-linked-solution).
5. After you **Place Order**, select **Configure Account Now** and follow your provider's registration instructions.
6. Keep your provider's registration page open, but leave the **Application (client) ID** field blank. The setup script creates this ID in step 2.
7. Return to the Microsoft Entra setup page and continue to step 2.

Important

Don't enter any other ID in the provider's **Application (client) ID** field, such as your tenant ID, subscription ID, or an existing app's ID. Use only the **Application (client) ID** from the step 2 deployment summary.

## Step 2: Deploy the integration

On **Set up an SMS or voice provider**, select **Set up the provider integration**. Select the Azure hosting subscription and review the telephony provider configuration populated in the pane.

[![Redacted screenshot of the provider integration pane with subscription selection, Function App setup, registration guidance, and Verify.](media/choose-your-own-telephony-set-up/integration-setup.png)](media/choose-your-own-telephony-set-up/integration-setup.png#lightbox)

### What the setup script does

The setup script deploys everything needed to connect Microsoft Entra ID to your telephony provider, so you don't have to create Azure resources by hand. It walks you through a few choices, then shows the full deployment plan. Nothing is created until you approve it.

After you approve, the script creates the Microsoft Entra application, deploys and secures the Azure resources, and applies your provider's configuration. Deployment usually takes a few minutes.

### Costs

Important

The integration runs on Azure resources in your subscription, billed based on your configuration and usage. To plan your budget, see [Estimate telephony-provider and Azure hosting costs](phone-providers-faq#how-much-does-choose-your-own-telephony-provider-cost) before you deploy.

### Run the setup script

1. Select **View setup script on GitHub** in the integration pane and review the setup instructions.
2. Sign in to the Azure portal and select the **Cloud Shell** icon (**&gt;\_**) in the top toolbar. You can also go directly to https://shell.azure.com.
3. Select **PowerShell**. If Cloud Shell opens in Bash, select **Switch to PowerShell** in the toolbar.
4. If this is your first time, select **No storage account required**, choose your subscription, and then select **Apply**.
5. Download the setup script:

    ```powershell
    Invoke-WebRequest -Uri 'https://raw.githubusercontent.com/Azure-Samples/ExternalPhoneProvider-AzureFunction-Sample/main/setup/Setup-Epp.ps1' `
        -OutFile '.\Setup-Epp.ps1'
    ```
6. Run the script.

    ```powershell
    .\Setup-Epp.ps1
    ```
7. Follow the prompts to select the customer tenant, hosting subscription, Azure region, telephony provider, runtime, and hosting plan. Use the configuration shown in the integration pane and approve the deployment plan.

    Tip

    **Choose region and plan for performance.** Deploy the Function App in the Azure region closest to your tenant's Microsoft Entra region. For low latency, use the Flex Consumption plan with one always-ready instance to avoid cold starts.
8. Save the deployment summary, including its tenant ID, endpoint URL, and **Application (client) ID**. You need these values to complete provider registration and configure your profile.

Important

Copy these values before you leave the Cloud Shell window. Cloud Shell sessions are temporary and can end when you navigate away, and the output isn't saved.

## Step 3: Complete telephony provider registration

After deployment completes, return to your telephony provider's registration page to complete the provider setup.

1. Provide the **Application (client) ID** created by the setup script when requested by your telephony provider.
2. Complete any additional registration steps required by the provider.
3. In [Microsoft Security Store](https://securitystore.microsoft.com/), go to **Management** &gt; **My Solutions** and confirm that the **Subscription status** is '**Subscribed**' before continuing.
4. Return to **Set up the provider integration** in the Microsoft Entra admin center and select **Verify** to check the telephony provider subscription.

## Step 4: Update the authentication method policy

Create a profile for each intended channel. The wizard carries over the current channel's targets and populates the endpoint and application ID when you select the deployed Function App. Start in **Evaluation**, validate the integration, and then gradually move delivery to your telephony provider.

Warning

**Target users** are shared with your existing SMS or voice policy, so any change here also affects users who sign in with SMS or voice today. Keep the current selections during rollout, and use a test tenant to try different users or groups.

### Configure CYOT settings

1. On **Set up an SMS or voice provider**, select **Create an SMS or voice profile**.
2. On **Delivery channel**, select **SMS** or **Voice call**, then select **Next**. Each profile configures one delivery channel.

    [![Redacted screenshot of the Delivery channel step with SMS and Voice call options.](media/choose-your-own-telephony-set-up/delivery-channel.png)](media/choose-your-own-telephony-set-up/delivery-channel.png#lightbox)
3. On **Target users**, review the targets carried over from the built-in channel configuration. Preserve the existing production **Include** and **Exclude** selections, then select **Next**.

    [![Redacted screenshot of Target users with the carried-over targeting notice and included group values obscured.](media/choose-your-own-telephony-set-up/target-users.png)](media/choose-your-own-telephony-set-up/target-users.png#lightbox)

### Start in evaluation mode

1. On **Profile plan**, select **Evaluation**. Review the **Evaluation sampling percentage**, then select **Next**.

    [![Redacted screenshot of the Evaluation plan, Microsoft-managed delivery explanation, and evaluation sampling control.](media/choose-your-own-telephony-set-up/evaluation-plan.png)](media/choose-your-own-telephony-set-up/evaluation-plan.png#lightbox)
2. On **Function App**, select the Function App deployed for the channel's integration. The wizard populates its **Function App URL** and **App ID**, along with subscription and resource details. Compare the endpoint and application client ID with the deployment summary, then select **Next**.

    [![Redacted screenshot of Function App selection and automatically populated endpoint, application, subscription, and resource details.](media/choose-your-own-telephony-set-up/select-function-app.png)](media/choose-your-own-telephony-set-up/select-function-app.png#lightbox)
3. On **Review and finalize**, confirm the delivery channel, existing targets, **Evaluation** plan, and selected Function App, then select **Create profile**.

    Note

    Changes to the authentication method policy can take up to an hour to take effect. Wait before you start testing.
4. Complete the evaluation-mode tests in step 5.

Saving applies the selected plan and targets to the channel. In **Evaluation**, Microsoft-managed telephony continues delivering authentication messages while the integration processes validation requests. Repeat profile configuration for each channel you intend to support.

### Move to production mode

After evaluation succeeds:

1. Open the saved SMS or voice profile from **Authentication methods** &gt; **Policies** and return to its **Profile plan** settings.
2. Select **Production** and set **Traffic routed through provider percentage** to your initial traffic percentage.

    [![Redacted screenshot of the Production plan and Traffic routed through provider percentage control.](media/choose-your-own-telephony-set-up/production-plan.png)](media/choose-your-own-telephony-set-up/production-plan.png#lightbox)
3. Keep the existing production targets and selected Function App unchanged.
4. Review and save the profile changes. Confirm the saved plan, percentage, endpoint, application ID, and targets.
5. Test telephony provider delivery before increasing traffic.

### Increase traffic gradually

1. Keep the profile in **Production**.
2. Increase **Traffic routed through provider percentage** in increments until you reach `100`.
3. Keep the endpoint URL, application client ID, and existing production targets unchanged while updating the traffic percentage.
4. Validate authentication and telephony provider delivery after every percentage change.
5. Increase the percentage after each stage validates successfully. To investigate an issue, hold at the current percentage and see [Monitor and troubleshoot](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider).

Important

When each stage validates successfully, continue to 100 percent without delay. Completing your rollout early helps ensure uninterrupted authentication for your users. For dates, see [Passkeys by default and retirement of Microsoft-provided SMS and voice authentication](concept-sms-voice-retirement).

## Step 5: Test the integration

Use a test user with a phone number registered for SMS or voice.

### Test in Evaluation

1. In an InPrivate browser session, sign in as the test user and complete an SMS or voice authentication.
2. In the Azure portal, go to your **Function App** → **Functions** → **SendOtp** → **Invocations** and open the latest transaction. In **Invocation details**, confirm **Evaluation request completed** with HTTP `200`.
3. In the Microsoft Entra admin center, go to **Monitoring & health** &gt; **Audit logs** and filter by **Service: Azure MFA**. Open the latest entry and confirm **DeliveryMethod** is `CyotEvaluation`.

### Test provider delivery

After evaluation succeeds, switch to **Production** and set your initial traffic percentage.

1. In a new InPrivate browser session, sign in as the test user. Confirm the SMS or voice code arrives and authentication completes.
2. In the Azure portal, go to your **Function App** → **Functions** → **SendOtp** → **Invocations** and open the latest transaction. In **Invocation details**, confirm the request completed with HTTP `200`.
3. In the Microsoft Entra admin center, go to **Audit logs** and filter by **Service: Azure MFA**. Open the latest entry and confirm **Delivery Method** is `Cyot`.
4. In your provider's portal, confirm the message was delivered.

At a partial percentage, only some requests route through your provider, so make a few attempts. If something doesn't look right, see [Monitor and troubleshoot your own telephony provider](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider).

## Troubleshooting

To diagnose integration issues, use the troubleshooting guide to identify whether the issue is with the Microsoft Entra configuration, Azure Function, telephony provider, or authentication flow.

See [Monitor and troubleshoot your own telephony provider](choose-your-own-telephony-troubleshoot#monitor-and-troubleshoot-your-own-telephony-provider) for diagnostic steps, logs, common issues, and remediation guidance.