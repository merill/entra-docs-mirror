---
layout: Conceptual
title: Fraud Protection Integration - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-integrate-fraud-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to configure Arkose Labs and Human fraud protection with Microsoft Entra External ID to block bot attacks and fake account creation during user sign-up flows.
zone_pivot_groups: fraud-protection-integration
ms.topic: how-to
ms.date: 2025-09-24T00:00:00.0000000Z
locale: en-us
document_id: 10d435c6-af9d-13e8-8d60-6756d5bbee8c
document_version_independent_id: 10d435c6-af9d-13e8-8d60-6756d5bbee8c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-integrate-fraud-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-integrate-fraud-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-integrate-fraud-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: a052eda7-ace6-787c-bfaf-d0eba4c8d94c
---

# Fraud Protection Integration - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Microsoft Entra External ID supports integration with third-party fraud protection providers, such as [Arkose Labs](https://www.arkoselabs.com/solutions/fake-account-creation/) and [HUMAN](https://www.humansecurity.com/), to help prevent fake account sign-ups and bot attacks. These providers offer comprehensive fraud protection solutions that enable organizations to detect and block automated attacks, such as bot-driven registrations, during the user sign-up process.

By integrating Arkose Labs, HUMAN, or both with Microsoft Entra External ID, you can leverage their advanced risk assessment capabilities to ensure that only legitimate users create accounts.

This article explains how to integrate fraud protection providers with Microsoft Entra External ID.

## About featured integrations

Arkose Labs and HUMAN Security are available as native integrations for sign-up protection through the Security Store. Microsoft developed and deployed these integrations in partnership with each provider to support bot detection and fake account prevention during user registration.

Native Security Store integrations are developed on a case-by-case basis through direct partnership with Microsoft's product engineering team. If you're a provider interested in integration opportunities with Microsoft Entra External ID, contact your Microsoft partner development representative.

::: zone pivot="arkose"

## How Arkose Labs works

When a user attempts to sign up, the Arkose Labs service evaluates the request and determines if it's likely to be fraudulent. If the request is flagged as suspicious, the user is presented with a challenge (like a CAPTCHA) to verify that they're human. If the user successfully completes the challenge, they can proceed with the sign-up process. Once this feature is enabled, you'll be able to view Arkose challenge metrics in the Arkose Labs dashboard. Additionally, you can fine-tune risk policies by coordinating with Arkose Labs support.

You can complete the integration in both the Microsoft Entra admin center and the Microsoft Graph API. This article provides instructions for the Microsoft Entra admin center.

## Prerequisites

- An [external tenant](how-to-create-external-tenant-portal).
- A [registered application](/en-us/entra/identity-platform/quickstart-register-app) in the tenant.
- An account with at least an [Authentication Extensibility Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-extensibility-administrator) or [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) role in the external tenant.
- An Arkose Labs account. If you don’t have one, go to the [Security Store](https://securitystore.microsoft.com/solutions/arkoselabs1589934191756.arkose_securitystore) to create and purchase your account.
- The following configuration values from Arkose:
    - Public key (GUID format).
    - Private key (GUID format).
    - Client subdomain: use only the subdomain prefix (for example, "client-api"), not the full domain.
    - Verify subdomain: use only the subdomain prefix (for example, "verify-api"), not the full domain.

## Configure Arkose Labs in the Microsoft Entra admin center

To integrate Arkose Labs with Microsoft Entra External ID, you can use the Security Store wizard in Microsoft Entra admin center to create a fraud protection provider policy.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Extensibility Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-extensibility-administrator) or [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant from the **Directories + subscriptions** menu.
3. Browse to **Home** &gt; **Security Store** &gt; **Sign-up protection** to start the wizard.

    [![Screenshot showing the Sign-up protection page.](media/how-to-integrate-fraud-protection/configure-sign-up-protection.png)](media/how-to-integrate-fraud-protection/configure-sign-up-protection.png#lightbox)
4. Enter a name for the policy, such as *ArkosePolicy*.
5. Select the scenarios to apply the fraud protection policy to and select **Next**.

    ![Screenshot showing setting up a protection policy.](media/how-to-integrate-fraud-protection/policy-set-up.png)
6. In the **Choose a fraud protection provider for sign-up** step, select **Arkose Labs** as the provider and select **Next**.

    ![Screenshot showing selecting the Arkose Labs fraud protection provider.](media/how-to-integrate-fraud-protection/choose-fraud-protection-provider.png)
7. Create an Arkose Account. If you don’t have an account yet, create and purchase one in the [Security Store](https://securitystore.microsoft.com/solutions/arkoselabs1589934191756.arkose_securitystore). Then return here to complete the setup.

    [![Screenshot showing configuring the Arkose Labs provider.](media/how-to-integrate-fraud-protection/provider-configuration.png)](media/how-to-integrate-fraud-protection/provider-configuration.png#lightbox)
8. In the **Configure Arkose Labs for sign-up protection** step, either select an existing configuration or select the **Create new** configuration, and enter the configuration values you received from Arkose Labs:

    - **Public key**: Enter the public key (GUID format).
    - **Private key**: Enter the private key (GUID format).
    - **Client subdomain**: Enter only the subdomain prefix (for example, "client-api"), not the full domain.
    - **Verify subdomain**: Enter only the subdomain prefix (for example, "verify-api"), not the full domain.
9. Select **Next** to go to the next step.
10. Select the app you want to protect with Arkose Labs fraud protection. You can select one or more applications that you have registered in your external tenant.

    ![Screenshot showing selecting an application to protect.](media/how-to-integrate-fraud-protection/select-apps-to-protect.png)
11. Review the configuration and select **Create policy** to create the fraud protection policy.

    ![Screenshot showing creating a policy for Arkose Labs.](media/how-to-integrate-fraud-protection/create-policy.png)
12. Once you receive the confirmation that the policy was created successfully, select **Done** to finish the wizard.

Once the policy is created, it's applied to the selected applications. When a user attempts to sign up, the Arkose Labs service evaluates the request and determines if it's likely to be fraudulent. If the request is flagged as suspicious, the user is presented with a challenge (like a CAPTCHA) to verify that they're human. If the user successfully completes the challenge, they can proceed with the sign-up process.

## Edit the Arkose Labs configuration in the Microsoft Entra admin center

1. Browse to **Home** &gt; **Security Store** &gt; **Sign-up protection** to view the list of configurations.
2. Select the **Edit provider configurations** option to edit the Arkose Labs policy. If you want to edit the fraud protection policy, select the pencil icon.
3. In the **Configure Arkose Labs for sign-up protection** step, select the configuration you want to edit and select **Next**.
4. Select the app you want to protect with Arkose Labs fraud protection or remove the existing ones. You can select one or more applications that you have registered in your external tenant. Once you selected the app, select **Next**.
5. Select **Done** to finish the wizard.

## Configure Arkose Labs using Microsoft Graph API

Configure Arkose Labs fraud protection by using the Microsoft Graph API. This approach is useful if you want to automate the configuration or if you prefer using APIs over the Microsoft Entra admin center.

### Step 1: Sign in to the tenant

To configure Arkose Labs fraud protection, you need to sign in to your external tenant and consent to the required permissions.

1. Start [Microsoft Graph Explorer tool](https://aka.ms/ge).
2. Sign in to your external tenant: `https://developer.microsoft.com/en-us/graph/graph-explorer?tenant=<your-tenant-name.onmicrosoft.com>`.
3. Select your profile and then select **Consent to permissions**.
4. Consent to the following required permission.

    - `RiskPreventionProviders.ReadWrite.All`

### Step 2: Register Arkose Labs as a fraud protection provider

To register Arkose Labs as a fraud protection provider, you [create a fraudProtectionProvider policy](/en-us/graph/api/riskpreventioncontainer-post-fraudprotectionproviders) in your external tenant. This policy contains the Arkose configuration values that you received from Arkose Labs.

1. In the Microsoft Graph Explorer, select the **POST** method and enter the following URL:

    ```http
    https://graph.microsoft.com/beta/identity/riskPrevention/fraudProtectionProviders
    ```
2. In the **Request Body** section, enter the following JSON payload, replacing the placeholders with your Arkose configuration values:

    ```json
    {
        "@odata.type": "#microsoft.graph.arkoseFraudProtectionProvider",
        "displayName": "<your-arkose-configuration-name>",
        "publicKey": "<your-arkose-public-key>",
        "privateKey": "<your-arkose-private-key>",
        "clientSubDomain": "<your-client-api>",
        "verifySubDomain": "<your-verify-api>"
    }
    ```
3. Select **Run Query** to create the fraud protection provider.
4. If the request is successful, a **201 Created** response is returned. Copy the `id` value from the response for the next step.

### Step 3: Link Arkose protection to your application

In this step, you link the Arkose fraud protection provider to your application by creating a new [authenticationEventListener](/en-us/graph/api/identitycontainer-post-authenticationeventlisteners) that triggers the Arkose challenge during the sign-up flow. Make sure that you have the appId for the application where you want to enable fraud protection. Replace `<your-app-id>` with your application's ID, and replace `<id-from-previous-step>` with the Arkose provider ID from the previous step.

1. In the Microsoft Graph Explorer, select the **POST** method and enter the following URL:

    ```http
    https://graph.microsoft.com/beta/identity/authenticationEventListeners
    ```
2. In the **Request Body** section, enter the following JSON payload:

    ```json
    { 
      "@odata.type": "#microsoft.graph.onFraudProtectionLoadStartListener", 
      "conditions": { 
        "applications": { 
          "includeApplications": [ 
            { 
              "appId": "<your-app-id>" 
            } 
          ] 
        } 
      }, 
      "handler": { 
        "@odata.type": "#microsoft.graph.onFraudProtectionLoadStartExternalUsersAuthHandler", 
        "signUp": { 
          "@odata.type": "#microsoft.graph.fraudProtectionProviderConfiguration", 
          "fraudProtectionProvider": { 
            "@odata.type": "#microsoft.graph.arkoseFraudProtectionProvider", 
            "id": "<id-from-previous-step>" 
          } 
        } 
      } 
    }
    ```
3. Select **Run Query**.
4. If the request is successful, a **201 Created** response is returned. Test the sign-up flow in your application to verify that the Arkose challenge appears when a suspicious sign-up is detected.

### Troubleshooting tips

| Issue | Possible Cause | Resolution |
| --- | --- | --- |
| Challenge doesn't appear. | Event listener not linked to app. | Verify app ID and listener configuration. |
| Users blocked on challenge. | Strict Arkose thresholds. | Work with Arkose to adjust challenge behavior. |

::: zone-end

::: zone pivot="human"

## How HUMAN Security works

When a user initiates the sign-up process, it is critical to prevent automated bots and malicious actors from creating fraudulent accounts. To address this, Entra External ID supports integration with third-party fraud detection providers such as HUMAN Security. This integration enables real-time analysis of sign-up attempts, leveraging HUMAN Security’s advanced detection algorithms to identify and block suspicious activity before account creation is completed. The solution is natively integrated with Microsoft identity infrastructure, allowing for streamlined deployment and management. By implementing this approach, organizations can access detailed data and actionable insights to monitor sign-up flows, fine-tune detection thresholds, and respond proactively to emerging threats, thereby maintaining the integrity of their user base.

## Prerequisites

- An [external tenant](how-to-create-external-tenant-portal).
- A [registered application](/en-us/entra/identity-platform/quickstart-register-app) in the tenant.
- An account with at least an [Authentication Extensibility Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-extensibility-administrator) or [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) role in the external tenant.
- A HUMAN Security account. If you don’t have one, go to the [Security Store](https://securitystore.microsoft.com/solutions/human_security.human_sightline_fake_account_defense) to create and purchase your account.
- The following configuration values from HUMAN Security:
    - Application ID
    - Server token

You can find these values in the HUMAN Security admin console in the [application settings](https://docs.humansecurity.com/applications-and-accounts/docs/managing-applications#adding-server-tokens) page. If you're unsure about any value, contact HUMAN Security for assistance.

## Configure HUMAN Security in the Microsoft Entra admin center

To integrate HUMAN Security with Microsoft Entra External ID, you can use the Security Store wizard in Microsoft Entra admin center to create a fraud protection provider policy.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Extensibility Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#authentication-extensibility-administrator) or [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator).
2. If you have access to multiple tenants, use the **Settings** icon ![](media/common/admin-center-settings-icon.png) in the top menu to switch to the external tenant from the **Directories + subscriptions** menu.
3. Browse to **Home** &gt; **Security Store** &gt; **Sign-up protection** to start the wizard.

    [![Screenshot showing the Sign-up protection page.](media/how-to-integrate-fraud-protection/configure-sign-up-protection.png)](media/how-to-integrate-fraud-protection/configure-sign-up-protection.png#lightbox)
4. Enter a name for the policy, such as *HUMANPolicy*.
5. Select the scenarios to apply the fraud protection policy to and select **Next**.

    ![Screenshot showing setting up a protection policy.](media/how-to-integrate-fraud-protection/policy-set-up-human.png)
6. In the **Choose a fraud protection provider for sign-up** step, select **HUMAN Security** as the provider and select **Next**.

    ![Screenshot showing selecting the HUMAN Security fraud protection provider.](media/how-to-integrate-fraud-protection/choose-fraud-protection-provider-human.png)
7. Create a HUMAN Security account. If you don’t have an account yet, create and purchase one in the [Security Store](https://securitystore.microsoft.com/solutions/human_security.human_sightline_fake_account_defense). Then return here to complete the setup.

    [![Screenshot showing configuring the HUMAN Security fraud protection provider.](media/how-to-integrate-fraud-protection/provider-configuration-human.png)](media/how-to-integrate-fraud-protection/provider-configuration-human.png#lightbox)
8. In the **Configure HUMAN Security for sign-up protection** step, select the **Create new** configuration, and enter the configuration values you received from HUMAN Security:

    - **App Id**: Enter the Application ID from HUMAN Security.
    - **Server token**: Enter the Server token from HUMAN Security that you can find in the HUMAN Security admin console.
9. Or select an existing configuration if you have already set one up and select **Next**.
10. Select the app you want to protect with HUMAN Security fraud protection. You can select one or more applications that you have registered in your external tenant.

    ![Screenshot showing selecting an application to protect.](media/how-to-integrate-fraud-protection/select-apps-to-protect.png)
11. Review the configuration and select **Create policy** to create the fraud protection policy.
12. Once you receive the confirmation that the policy was created successfully, select **Done** to finish the wizard.

Once the policy is created, it's applied to the selected applications. When a user attempts to sign up, HUMAN Security evaluates the request in real-time to determine if it's likely to be fraudulent. If the request is flagged as suspicious, appropriate measures are taken to block the sign-up attempt, thereby preventing fake account registrations.

## Edit the HUMAN Security configuration in the Microsoft Entra admin center

1. Browse to **Home** &gt; **Security Store** &gt; **Sign-up protection** to view the list of configurations.
2. Select the **Edit provider configurations** option to edit the HUMAN Security policy. If you want to edit the fraud protection policy, select the pencil icon.
3. In the **Configure HUMAN Security for sign-up protection** step, select the configuration you want to edit and select **Next**.
4. Select the app you want to protect with HUMAN Security fraud protection or remove the existing ones. You can select one or more applications that you have registered in your external tenant. Once you selected the app, select **Next**.
5. Select **Done** to finish the wizard.

## Configure HUMAN Security using Microsoft Graph API

Configure HUMAN Security fraud protection by using the Microsoft Graph API. This approach is useful if you want to automate the configuration or if you prefer using APIs over the Microsoft Entra admin center.

### Step 1: Sign in to the tenant

To configure HUMAN Security fraud protection, you need to sign in to your external tenant and consent to the required permissions.

1. Start [Microsoft Graph Explorer tool](https://aka.ms/ge).
2. Sign in to your external tenant: `https://developer.microsoft.com/en-us/graph/graph-explorer?tenant=<your-tenant-name.onmicrosoft.com>`.
3. Select your profile and then select **Consent to permissions**.
4. Consent to the following required permission.

    - `RiskPreventionProviders.ReadWrite.All`

### Step 2: Register HUMAN Security as a fraud protection provider

To register HUMAN Security as a fraud protection provider, you [create a fraudProtectionProvider policy](/en-us/graph/api/riskpreventioncontainer-post-fraudprotectionproviders) in your external tenant. This policy contains the HUMAN Security configuration values that you've received while setting up your HUMAN Security account.

1. In the Microsoft Graph Explorer, select the **POST** method and enter the following URL:

    ```http
    https://graph.microsoft.com/beta/identity/riskPrevention/fraudProtectionProviders
    ```
2. In the **Request Body** section, enter the following JSON payload, replacing the placeholders with your HUMAN configuration values:

    ```json
    {
        "@odata.type": "#microsoft.graph.HUMANFraudProtectionProvider",
        "displayName": "<your-human-configuration-name>",
        "appId": "<your-human-appid>",  
        "serverToken": "<your-human-server-token>",
    }
    ```

The `displayName` is a display name for this specific HUMAN Security configuration, for example, "HUMAN Config 1". The `appId` is the Application ID from HUMAN Security, and the `serverToken` is the Server token from HUMAN Security that you can find in the HUMAN Security admin console. If you're unsure about any value, contact HUMAN Security for assistance.

1. Select **Run Query** to create the fraud protection provider.
2. If the request is successful, a **201 Created** response is returned. Copy the `id` value from the response for the next step.

### Step 3: Link HUMAN Security protection to your application

In this step, you link the HUMAN Security fraud protection provider to your application by creating a new [authenticationEventListener](/en-us/graph/api/identitycontainer-post-authenticationeventlisteners) to use the HUMAN Security fraud protection during the sign-up flow. Make sure that you have the appId for the application where you want to enable fraud protection. Replace `<your-app-id>` with your application's ID, and replace `<id-from-previous-step>` with the HUMAN Security provider ID from the previous step.

1. In the Microsoft Graph Explorer, select the **POST** method and enter the following URL:

    ```http
    https://graph.microsoft.com/beta/identity/authenticationEventListeners
    ```
2. In the **Request Body** section, enter the following JSON payload:

    ```json
    { 
      "@odata.type": "#microsoft.graph.onFraudProtectionLoadStartListener", 
      "conditions": { 
        "applications": { 
          "includeApplications": [ 
            { 
              "appId": "<your-app-id>" 
            } 
          ] 
        } 
      }, 
      "handler": { 
        "@odata.type": "#microsoft.graph.onFraudProtectionLoadStartExternalUsersAuthHandler", 
        "signUp": { 
          "@odata.type": "#microsoft.graph.fraudProtectionProviderConfiguration", 
          "fraudProtectionProvider": { 
            "@odata.type": "#microsoft.graph.HUMANFraudProtectionProvider", 
            "id": "<id-from-previous-step>" 
          } 
        } 
      } 
    }
    ```
3. Select **Run Query**.
4. If the request is successful, a **201 Created** response is returned. Test the sign-up flow in your application to verify that the HUMAN challenge appears when a suspicious sign-up is detected.

::: zone-end