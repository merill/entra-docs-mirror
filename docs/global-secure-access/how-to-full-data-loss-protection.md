---
layout: Conceptual
title: Create a custom Data Loss Prevention profile with the Global Secure Access and Netskope integration - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-full-data-loss-protection
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to protect your organization with a custom Data Loss Prevention (DLP) profile powered by Netskope.
ms.topic: how-to
ms.date: 2025-11-07T00:00:00.0000000Z
ms.reviewer: abhijeetsinha
ai-usage: ai-assisted
locale: en-us
document_id: 3edfeaec-ad74-234c-529c-ffc59313ef3b
document_version_independent_id: 3edfeaec-ad74-234c-529c-ffc59313ef3b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-full-data-loss-protection.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-full-data-loss-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-full-data-loss-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 71836a18-5568-01bd-43a8-c1c51912c34c
---

# Create a custom Data Loss Prevention profile with the Global Secure Access and Netskope integration - Global Secure Access | Microsoft Learn

Microsoft Entra Internet Access with Global Secure Access integration with Netskope provides comprehensive Data Loss Prevention (DLP) capabilities to help protect your organization's sensitive data from leaks and unauthorized access. By using Netskope's advanced DLP features, you can create and enforce policies that monitor, control, and protect data across your network.

This guide provides step-by-step instructions to create custom DLP profiles using the Global Secure Access and Netskope integration.

## Prerequisites

To complete these steps, make sure you have the following prerequisites:

- All prerequisites listed in [Global Secure Access integration with Netskope's Advanced Threat Protection and Data Loss Prevention](concept-netskope-integration).
- An App Administrator role in Microsoft Entra ID to set up DLP integrations.
- Global Secure Access admins assigned to the app **Netskope GSA SAML SSO**. For more information, see [Manage user and group assignments to an application](../identity/enterprise-apps/assign-user-or-group-access-portal).

## Create a custom DLP profile

To create a custom DLP profile, follow these steps:

### Configure SAML SSO using Microsoft Graph API

To enable single sign-on (SSO) authentication between Global Secure Access and Netskope, you need to configure SAML SSO by running the following commands using Microsoft Graph API. Follow these steps:

1. Create a claims mapping policy.

    ```json
    POST https://graph.microsoft.com/v1.0/policies/claimsMappingPolicies 
    
    { 
    
      "definition": [ 
    
       "{\"ClaimsMappingPolicy\":{\"Version\":1,\"IncludeBasicClaimSet\":\"true\",\"ClaimsSchema\":[{\"Source\":\"user\",\"Id\":\"userprincipalname\",\"SamlClaimType\":\"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier\"},{\"Source\":\"user\",\"Id\":\"givenname\",\"SamlClaimType\":\"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname\"},{\"Source\":\"user\",\"Id\":\"displayname\",\"SamlClaimType\":\"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name\"},{\"Source\":\"user\",\"Id\":\"surname\",\"SamlClaimType\":\"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname\"},{\"Source\":\"user\",\"Id\":\"assignedroles\",\"SamlClaimType\":\"admin-role\"},{\"Source\":\"user\",\"Id\":\"mail\",\"SamlClaimType\":\"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress\"}]}}" 
    
      ], 
    
      "displayName": "Netskope SAML SSO Claims Policy" 
    
    } 
    ```
2. Copy the ID from the response.
3. Get the application ID.

    ```json
    GET https://graph.microsoft.com/v1.0/applications?$filter=displayName+eq+'Netskope+GSA+SAML+SSO'&$select=appId
    ```
4. Associate the claims mapping policy. Replace `<insert app id>` and `<insert claims mapping policy id>` with the respective values obtained from previous steps.

    ```json
    POST https://graph.microsoft.com/v1.0/servicePrincipals(appId='<insert app id>')/claimsMappingPolicies/$ref 
    
    { 
    
      "@odata.id": "https://graph.microsoft.com/v1.0/policies/claimsMappingPolicies/<insert claims mapping policy id>" 
    
    } 
    ```

### Create a DLP policy with a custom DLP profile

To create a DLP policy with a custom DLP profile, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Data Loss Prevention policies**.
3. Select **+ Create policy** and select a DLP profile.
4. Select the link to open the Netskope admin center.
5. In the Netskope admin center, [create a custom DLP profile](https://docs.netskope.com/en/create-a-custom-dlp-profile).
6. After creating the profile, return to the Microsoft Entra admin center.
7. The custom DLP profile automatically syncs and appears in the DLP profiles list.
8. Select the custom DLP profile and complete the policy creation workflow.

## Activate a Netskope offer

Netskope’s DLP offering is a value-added enhancement to Microsoft Entra Internet Access. For instructions on how to start a free trial or contact Netskope for a private offer, see [Activate a Netskope offer through the Global Secure Access marketplace](concept-netskope-integration#activate-a-netskope-offer-through-the-global-secure-access-marketplace).