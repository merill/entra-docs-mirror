---
layout: Conceptual
title: Considerations for specific personas in a phishing-resistant passwordless authentication deployment in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-plan-persona-phishing-resistant-passwordless-authentication
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Persona-specific guidance to deploy passwordless and phishing-resistant authentication for organizations that use Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-10-30T00:00:00.0000000Z
ms.reviewer: sipower
ms.collection: M365-identity-device-management
ms.custom: sfi-image-nochange
locale: en-us
document_id: 88135501-42a3-88cb-80cb-842f1a084d55
document_version_independent_id: 88135501-42a3-88cb-80cb-842f1a084d55
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-plan-persona-phishing-resistant-passwordless-authentication.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-plan-persona-phishing-resistant-passwordless-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-plan-persona-phishing-resistant-passwordless-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 819808c2-75a5-9317-7c94-ae1c8781868b
---

# Considerations for specific personas in a phishing-resistant passwordless authentication deployment in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Each persona has its own challenges and considerations that commonly come up during phishing-resistant passwordless deployments. As you identify which personas you need to accommodate, you should factor these considerations into your deployment project planning. The next sections provide specific guidance for each persona.

## Deployment for Admins and Highly regulated users

Admins and highly regulated users represent the most security-sensitive personas in your organization and require special consideration during phishing-resistant passwordless deployments. These users typically work with privileged access, handle sensitive data, or operate in environments with strict compliance requirements. While they prioritize security over convenience, successful deployment still requires careful planning to address their unique challenges.

### IT pros/DevOps workers

IT pros and DevOps workers are especially reliant on remote access and multiple user accounts, which is why they're considered different from information workers. Many of the challenges posed by phishing-resistant passwordless for IT pros are caused by their increased need for remote access to systems and ability to run automations.

![Diagram that shows examples of requirements for IT pro workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/it-pro-examples.png)

Understand the supported options for phishing-resistant with RDP especially for this persona.

Make sure to understand where users are using scripts that run in the user context and are therefore not using MFA today. Instruct your IT pros on the proper way to run automations using service principals and managed identities. You should also consider processes to allow IT pros and other professionals to request new service principals and get the proper permissions assigned to them.

- [What are managed identities for Azure resources?](../managed-identities-azure-resources/overview)
- [Securing service principals in Microsoft Entra ID](../../architecture/service-accounts-principal)

#### IT pros/DevOps worker deployment flow

Phases 1-3 of the deployment flow for IT pro/DevOps workers should typically follow the standard deployment flow as previously pictured for the user’s primary account. IT pros/DevOps workers often have secondary accounts that require different considerations. Adjust the methods used at each step as needed in your environment for the primary accounts:

![Diagram that shows deployment flow for IT pros/DevOps workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/it-pro-deployment.png)

1. Phase 1: Onboarding
    1. Microsoft Entra Verified ID service used to acquire a Temporary Access Pass
2. Phase 2: Portable credential registration
    1. Microsoft Authenticator app passkey (preferred)
    2. FIDO2 security key
3. Phase 3: Local credential registration
    1. Windows Hello for Business
    2. Platform SSO Secure Enclave Key

If your IT pro/DevOps workers have secondary accounts, you may need to handle those accounts differently. For example, for secondary accounts you may choose to use alternative portable credentials and forego local credentials on your computing devices entirely:

![Diagram that shows an alternative deployment flow for IT pros/DevOps workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/it-pro-secondary.png)

1. Phase 1: Onboarding
    1. Microsoft Entra Verified ID service used to acquire a Temporary Access Pass (preferred)
    2. Alternate process to provide TAPs for secondary accounts to the IT pro/DevOps worker
2. Phase 2: Portable credential registration
    1. Passkey in Microsoft Authenticator (preferred)
    2. FIDO2 security key
    3. Smart card
3. Phase 3: Portable credentials used rather than local credentials

### Highly regulated workers

Highly regulated workers pose more challenges than the average information worker because they may work on locked down devices, work in locked down environments, or have special regulatory requirements they must satisfy.

![Diagram that shows examples of requirements for highly regulated workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/regulated-worker-examples.png)

Highly regulated workers often use smart cards due to regulated environments already having heavy adoption of PKI and smart card infrastructure. However, consider when smart cards are desirable and required and when they can be balanced with more user-friendly options, such as Windows Hello for Business.

#### Highly regulated worker deployment flow without PKI

If you don't plan to use certificates, smart cards, and PKI, then the highly regulated worker deployment closely mirrors the information worker deployment. For more information, see Information workers.

#### Highly regulated worker deployment flow with PKI

If you plan to use certificates, smart cards, and PKI, then the deployment flow for highly regulated workers typically differs from the information worker setup flow in key places. There's an increased need to identify if local authentication methods are viable for some users. Similarly, you need to identify if there are some users who need portable-only credentials, such as smart cards, that can work without internet connections. Depending on your needs, you may adjust the deployment flow further, and tailor it to the various user personas identified in your environment. Adjust the methods used at each step as needed in your environment:

![Diagram that shows deployment flow for highly regulated workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/regulated-worker-deployment.png)

1. Phase 1: Onboarding
    1. Microsoft Entra Verified ID service used to acquire a Temporary Access Pass (preferred)
    2. Smart card registration on behalf of the user, following an identity proofing process
2. Phase 2: Portable credential registration
    1. Smart card (preferred)
    2. FIDO2 security key
    3. Passkey in Microsoft Authenticator
3. Phase 3 (Optional): Local credential registration
    1. Optional: Windows Hello for Business
    2. Optional: Microsoft Entra passkey on Windows
    3. Optional: Platform SSO Secure Enclave Key

Note

It's always recommended that users have at least two credentials registered. This ensures the user has a backup credential available if something happens to their other credentials. For highly regulated workers, it's recommended that you deploy passkeys or Windows Hello for Business in addition to any smart cards you deploy.

## Deployment for non-admin users

Deployment for non admins users requires proper communication and support. This commonly involves convincing users to install certain apps on their phones, distributing security keys where users won’t use apps, addressing concerns about biometrics, and developing processes for helping users recover from partial or total loss of their credentials.

### Information workers

Information workers typically have the simplest requirements and are the easiest to begin your phishing-resistant passwordless deployment with. However, there are still some issues that frequently arise when deploying for these users. Common examples include:

![Diagram that shows examples of requirements for information workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/information-worker-examples.png)

#### Information worker deployment flow

Steps 1-3 of the deployment flow for information workers should typically follow the standard deployment flow, as shown in the following image. Adjust the methods used at each step as needed in your environment:

![Diagram that shows deployment flow for information workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/information-worker-deployment.png)

1. Onboarding
    1. Microsoft Entra Verified ID service used to acquire a Temporary Access Pass
2. Portable credential registration
    1. Synced passkey (preferred)
    2. Passkey in Microsoft Authenticator
    3. FIDO2 security key
3. Local credential registration
    1. Windows Hello for Business
    2. Microsoft Entra passkey on Windows
    3. Platform SSO Secure Enclave Key

### Frontline workers

Frontline workers often have more complicated requirements due to increased needs for the portability of their credentials and limitations on which devices they can carry in retail or manufacturing settings. Synced passkey is a great option for frontline workers. In scenarios where synced passkeys can't be used, security keys and smart cards are other phishing-resistant options.

![Diagram that shows examples of requirements for frontline workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/frontline-worker-examples.png)

#### Frontline worker deployment flow

Steps 1-3 of the deployment flow for frontline workers should typically follow a modified flow that emphasizes portable credentials. Many frontline workers may not have a permanent computing device, and they never need a local credential on a Windows or Mac workstation. Instead, they largely rely on portable credentials that they can take with them from device to device. Adjust the methods used at each step as needed in your environment:

![Diagram that shows deployment flow for frontline workers.](media/how-to-deploy-phishing-resistant-passwordless-authentication/frontline-worker-deployment.png)

1. Phase 1: Onboarding
    1. FIDO2 security key on-behalf-of registration (preferred)
    2. Microsoft Entra Verified ID service used to acquire a Temporary Access Pass
2. Phase 2: Portable credential registration
    1. Synced passkey (preferred)
    2. FIDO2 security key
    3. Passkey in Microsoft Authenticator
    4. Smart card
3. Phase 3 (Optional): Local credential registration
    1. Optional: Windows Hello for Business
    2. Optional: Microsoft Entra passkey on Windows
    3. Optional: Platform SSO Secure Enclave Key

## General considerations

When dealing with concerns about biometrics, make sure that you understand how technologies like Windows Hello for Business handle biometrics. The biometric data is stored only locally on the device and can't be converted back into raw biometric data even if stolen. For more information, see [Windows Hello for Business Biometric data storage](/en-us/windows/security/identity-protection/hello-for-business/how-it-works#biometric-data-storage).