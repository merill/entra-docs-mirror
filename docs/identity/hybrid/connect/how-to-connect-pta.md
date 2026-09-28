---
layout: Conceptual
title: 'Microsoft Entra Connect: Pass-through Authentication - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-pta
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article describes Microsoft Entra pass-through authentication and how it allows Microsoft Entra sign-ins by validating users' passwords against on-premises Active Directory.
keywords: what is Azure AD Connect Pass-through Authentication, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 2ac3db0d-38f4-5605-dd9a-2a7583ef1af9
document_version_independent_id: 1a15f8e7-c9f8-8367-ee03-7694d916deea
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-pta.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-pta
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-pta.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: fc82786e-382f-22e6-1045-ee7642631107
---

# Microsoft Entra Connect: Pass-through Authentication - Microsoft Entra ID | Microsoft Learn

## What is Microsoft Entra pass-through authentication?

Microsoft Entra pass-through authentication allows your users to sign in to both on-premises and cloud-based applications using the same passwords. This feature provides your users a better experience - one less password to remember, and reduces IT helpdesk costs because your users are less likely to forget how to sign in. When users sign in using Microsoft Entra ID, this feature validates users' passwords directly against your on-premises Active Directory.

This feature is an alternative to [Microsoft Entra password hash synchronization](how-to-connect-password-hash-synchronization), which provides the same benefit of cloud authentication to organizations. However, certain organizations wanting to enforce their on-premises Active Directory security and password policies, can choose to use Pass-through Authentication instead. Review [this guide](choose-ad-authn) for a comparison of the various Microsoft Entra sign-in methods and how to choose the right sign-in method for your organization.

![Microsoft Entra pass-through authentication](media/how-to-connect-pta/pta1.png)

You can combine Pass-through Authentication with the [Seamless single sign-on](how-to-connect-sso) feature. If you have Windows 10 or later machines, use [Microsoft Entra hybrid join (AADJ)](../../devices/how-to-hybrid-join). This way, when your users are accessing applications on their corporate machines inside your corporate network, they don't need to type in their passwords to sign in.

## Key benefits of using Microsoft Entra pass-through authentication

- *Great user experience*
    - Users use the same passwords to sign into both on-premises and cloud-based applications.
    - Users spend less time talking to the IT helpdesk resolving password-related issues.
    - Users can complete [self-service password management](../../authentication/concept-sspr-howitworks) tasks in the cloud.
- *Easy to deploy & administer*
    - No need for complex on-premises deployments or network configuration.
    - Needs just a lightweight agent to be installed on-premises.
    - No management overhead. The agent automatically receives improvements and bug fixes.
- *Secure*
    - On-premises passwords are never stored in the cloud in any form.
    - Protects your user accounts by working seamlessly with [Microsoft Entra Conditional Access policies](../../conditional-access/overview), including Multi-Factor Authentication (MFA), [blocking legacy authentication](../../conditional-access/concept-conditional-access-conditions) and by [filtering out brute force password attacks](../../authentication/howto-password-smart-lockout).
    - The agent only makes outbound connections from within your network. Therefore, there is no requirement to install the agent in a perimeter network, also known as a DMZ.
    - The communication between an agent and Microsoft Entra ID is secured using certificate-based authentication. These certificates are automatically renewed every few months by Microsoft Entra ID.
- *Highly available*
    - Additional agents can be installed on multiple on-premises servers to provide high availability of sign-in requests.

## Feature highlights

- Supports user sign-in into all web browser-based applications and into Microsoft Office client applications that use [modern authentication](https://aka.ms/modernauthga).
- Sign-in usernames can be either the on-premises default username (`userPrincipalName`) or another attribute configured in Microsoft Entra Connect (known as `Alternate ID`).
- The feature works seamlessly with [Conditional Access](../../conditional-access/overview) features such as Multi-Factor Authentication (MFA) to help secure your users.
- Integrated with cloud-based [self-service password management](../../authentication/concept-sspr-howitworks), including password writeback to on-premises Active Directory and password protection by banning commonly used passwords.
- Multi-forest environments are supported if there are forest trusts between your AD forests and if name suffix routing is correctly configured.
- It is a free feature, and you don't need any paid editions of Microsoft Entra ID to use it.
- It can be enabled via [Microsoft Entra Connect](../whatis-hybrid-identity).
- It uses a lightweight on-premises agent that listens for and responds to password validation requests.
- Installing multiple agents provides high availability of sign-in requests.
- It [protects](../../authentication/howto-password-smart-lockout) your on-premises accounts against brute force password attacks in the cloud.

## Privacy considerations

When a pass-through sign-in attempt from Tenant A (for example, Contoso) to Tenant B (for example, Fabrikam) fails, Microsoft Entra ID publishes the sign-in log to both tenants. For failed attempts, Microsoft Entra ID doesn't expose personally identifiable information (PII) to Tenant B, because the user in Tenant A never consented to share their identity with Tenant B. In these cases, attributes like the user principal name (UPN) are replaced with unresolved GUIDs.

If the sign-in succeeds and the user enters Tenant B as a guest with resource access, they become a B2B guest user. Microsoft Entra ID then surfaces their identity information to Tenant B.