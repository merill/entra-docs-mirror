---
layout: Conceptual
title: Secure hybrid access with Microsoft Entra ID and Silverfort - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/silverfort-integration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: In this tutorial, learn how to integrate Silverfort with Microsoft Entra ID for secure hybrid access (SHA).
ms.topic: how-to
ms.date: 2024-04-18T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
ms.custom: not-enterprise-apps
locale: en-us
document_id: 4403c77a-5404-0c18-30f2-36c92bdc0ef9
document_version_independent_id: 096b7fd9-0a5e-c96b-1345-2a42285705ba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/silverfort-integration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/silverfort-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/silverfort-integration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c8ab6525-71f8-4e1b-0d9b-64d1a68e1d84
---

# Secure hybrid access with Microsoft Entra ID and Silverfort - Microsoft Entra ID | Microsoft Learn

[Silverfort](https://www.silverfort.com/) uses agent-less and proxy-less technology to connect your assets on-premises and in the cloud to Microsoft Entra ID. This solution enables organizations to apply identity protection, visibility, and user experience across environments in Microsoft Entra ID. It enables universal risk-based monitoring and assessment of authentication activity for on-premises and cloud environments, and helps to prevent threats.

In this tutorial, learn how to integrate your on-premises Silverfort implementation with Microsoft Entra ID.

Learn more:

- [Microsoft Entra hybrid joined devices](../devices/concept-hybrid-join)
- [Silverfort bridging to Microsoft Entra ID](https://www.silverfort.com/resources/solution-brief/silverfort-bridging-to-entra-id/)

Silverfort connects assets with Microsoft Entra ID. These bridged assets appear as regular applications in Microsoft Entra ID and can be protected with [Conditional Access](../conditional-access/overview), single-sign-on (SSO), multifactor authentication, auditing and more. Use Silverfort to connect assets including:

- Legacy and homegrown applications
- Remote desktop and Secure Shell (SSH)
- Command-line tools and other admin access
- File shares and databases
- Infrastructure and industrial systems

Silverfort integrates corporate assets and third-party Identity and Access Management (IAM) platforms, which includes Active Directory Federation Services (AD FS), and Remote Authentication Dial-In User Service (RADIUS) in Microsoft Entra ID. The scenario includes hybrid and multicloud environments.

Use this tutorial to configure and test the Silverfort Microsoft Entra ID bridge in your Microsoft Entra tenant to communicate with your Silverfort implementation. After configuration, you can create Silverfort authentication policies that bridge authentication requests from identity sources to Microsoft Entra ID for SSO. After an application is bridged, you can manage it in Microsoft Entra ID.

## Silverfort with Microsoft Entra authentication architecture

The following diagram shows the authentication architecture orchestrated by Silverfort, in a hybrid environment.

![Diagram the architecture diagram](media/silverfort-integration/silverfort-architecture-diagram.png)

### User flow

1. Users send authentication request to the original identity provider (IdP) through protocols such as Kerberos, SAML, NTLM, OIDC, and LDAPs
2. Responses are routed as-is to Silverfort for validation to check authentication state
3. Silverfort provides visibility, discovery, and a bridge to Microsoft Entra ID
4. If the application is bridged, the authentication decision passes to Microsoft Entra ID. Microsoft Entra ID evaluates Conditional Access policies and validates authentication.
5. The authentication state response goes as-is from Silverfort to the IdP
6. IdP grants or denies access to the resource
7. Users are notified if access request is granted or denied

## Prerequisites

You need Silverfort deployed in your tenant or infrastructure to perform this tutorial. To deploy Silverfort in your tenant or infrastructure, go to silverfort.com [Silverfort](https://www.silverfort.com/) to install the Silverfort desktop app on your workstations.

Set up Silverfort Microsoft Entra Adapter in your Microsoft Entra tenant:

- An Azure account with an active subscription
    - You can create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- One of the following roles in your Azure account:
    - Cloud Application Administrator
    - Application Administrator
    - Service Principal Owner
- The Silverfort Microsoft Entra Adapter application in the Microsoft Entra application gallery is preconfigured to support SSO. From the gallery, add the Silverfort Microsoft Entra Adapter to your tenant as an Enterprise application.

## Configure Silverfort and create a policy

1. From a browser, sign in to the Silverfort admin console.
2. In the main menu, navigate to **Settings** and then scroll to **Microsoft Entra ID Bridge Connector** in the General section.
3. Confirm your tenant ID, and then select **Authorize**.
4. Select **Save Changes**.
5. On the **Permissions requested** dialog, select **Accept**.
6. A Registration Completed message appears in a new tab. Close this tab.

    ![image shows registration completed](media/silverfort-integration/registration-completed.png)
7. On the **Settings** page, select **Save Changes**.
8. Sign in to your Microsoft Entra account. In the left pane, select **Enterprise applications**. The **Silverfort Microsoft Entra Adapter** application appears as registered.
9. In the Silverfort admin console, navigate to the **Policies** page and select **Create Policy**. The **New Policy** dialog appears.
10. Enter a **Policy Name**, the application name to be created in Azure. For example, if you're adding multiple servers or applications for this policy, name it to reflect the resources covered by the policy. In the example, we create a policy for the SL-APP1 server.

![image shows define policy](media/silverfort-integration/define-policy.png)

1. Select the **Auth Type**, and **Protocol**.
2. In the **Users and Groups** field, select the **Edit** icon to configure users affected by the policy. These users' authentication bridges to Microsoft Entra ID.

![image shows user and groups](media/silverfort-integration/user-groups.png)

1. Search and select users, groups, or Organization Units (OUs).

![image shows search users](media/silverfort-integration/search-users.png)

1. Selected users appear in the **SELECTED** box.

![image shows selected user](media/silverfort-integration/select-user.png)

1. Select the **Source** for which the policy applies. In this example, **All Devices** is selected.

    ![image shows source](media/silverfort-integration/source.png)
2. Set the **Destination** to SL-App1. Optional: You can select the **edit** button to change or add more resources, or groups of resources.

    ![image shows destination](media/silverfort-integration/destination.png)
3. For Action, select **Entra ID BRIDGE**.
4. Select **Save**. You're prompted to turn on the policy.
5. In the Entra ID Bridge section, the policy appears on the Policies page.
6. Return to the Microsoft Entra account, and navigate to **Enterprise applications**. The new Silverfort application appears. You can include this application in Conditional Access policies.

Learn more: [Tutorial: Secure user sign-in events with Microsoft Entra multifactor authentication](../authentication/tutorial-enable-azure-mfa?bc=/azure/active-directory/conditional-access/breadcrumb/toc.json&amp;toc=/azure/active-directory/conditional-access/toc.json#create-a-conditional-access-policy).