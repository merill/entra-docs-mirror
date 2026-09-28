---
layout: Conceptual
title: Built-in policy definitions for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/policy-reference
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Lists Azure Policy built-in policy definitions for Microsoft Entra Domain Services. These built-in policy definitions provide common approaches to managing your Azure resources.
ms.date: 2023-09-19T00:00:00.0000000Z
ms.topic: reference
ms.custom: subject-policy-reference
locale: en-us
document_id: 19885147-060a-5c77-2e8c-34e64cbe4d2e
document_version_independent_id: d1c7f1b2-a2e4-1da3-0f3e-6ada72847bc1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/policy-reference.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/policy-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/policy-reference.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 210e6a57-ab2f-d42c-bdbc-1f81ddbc7278
---

# Built-in policy definitions for Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

This page is an index of [Azure Policy](/en-us/azure/governance/policy/overview) built-in policy definitions for Microsoft Entra Domain Services. For additional Azure Policy built-ins for other services, see [Azure Policy built-in definitions](/en-us/azure/governance/policy/samples/built-in-policies).

The name of each built-in policy definition links to the policy definition in the Microsoft Entra admin center. Use the link in the **Version** column to view the source on the [Azure Policy GitHub repo](https://github.com/Azure/azure-policy).

## Microsoft Entra Domain Services

| Name(Azure portal) | Description | Effect(s) | Version(GitHub) |
| --- | --- | --- | --- |
| [Microsoft Entra Domain Services managed domains should use TLS 1.2 only mode](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F3aa87b5a-7813-4b57-8a43-42dd9df5aaa7) | Use TLS 1.2 only mode for your managed domains. By default, Microsoft Entra Domain Services enables the use of ciphers such as NTLM v1 and TLS v1. These ciphers may be required for some legacy applications, but are considered weak and can be disabled if you don't need them. When TLS 1.2 only mode is enabled, any client making a request that is not using TLS 1.2 will fail. Learn more at [Harden a Microsoft Entra Domain Services managed domain](secure-your-domain). | Audit, Deny, Disabled | [1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Active%20Directory/AADDomainServices_TLS_Audit.json) |
| [Microsoft Entra ID should use private link to access Azure services](/en-us/training/modules/design-implement-private-access-to-azure-services/). | Azure Private Link lets you connect your virtual networks to Azure services without a public IP address at the source or destination. The Private Link platform handles the connectivity between the consumer and services over the Azure backbone network. By mapping private endpoints to Microsoft Entra ID, you can reduce data leakage risks. Learn more at: https://aka.ms/privateLinkforAzureADDocs. It should be only used from isolated VNETs to Azure services, with no access to the Internet or other services (M365). | AuditIfNotExists, Disabled | [1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Active%20Directory/PrivateLinkForAzureAD_PrivateLink_AINE.json) |
| [Configure Private Link for Microsoft Entra ID with private endpoints](https://ms.portal.azure.com/#view/Microsoft_Azure_Network/PrivateLinkCenterBlade/%7E/overview.Authorization%2FpolicyDefinitions%2Fb923afcf-4c3a-4ed6-8386-1ff64b68de47) | Private endpoints connect your virtual networks to Azure services without a public IP address at the source or destination. By mapping private endpoints to Microsoft Entra ID, you can reduce data leakage risks. Learn more at: https://aka.ms/privateLinkforAzureADDocs. It should be only used from isolated VNETs to Azure services, with no access to the Internet or other services (M365). | DeployIfNotExists, Disabled | [1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Azure%20Active%20Directory/PrivateLinkForAzureAD_PrivateEndpoint_DINE.json) |