---
layout: Conceptual
title: Microsoft Entra directory extensions for provisioning to AD - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/custom-attribute-mapping-entra-to-active-directory
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: pmwongera
description: Learn how directory extensions for users and groups support provisioning from Microsoft Entra ID to Active Directory.
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, msecd-doc-authoring-1023
ms.topic: concept-article
ms.date: 2026-08-11T00:00:00.0000000Z
ms.subservice: hybrid-cloud-sync
ai-usage: ai-assisted
locale: en-us
document_id: 7869d0a9-7d19-2701-e0a5-c87cac340723
document_version_independent_id: 7869d0a9-7d19-2701-e0a5-c87cac340723
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/custom-attribute-mapping-entra-to-active-directory.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/custom-attribute-mapping-entra-to-active-directory
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/custom-attribute-mapping-entra-to-active-directory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: a528e04e-1d66-663e-266c-d5cf7059b24f
---

# Microsoft Entra directory extensions for provisioning to AD - Microsoft Entra ID | Microsoft Learn

You can use directory extensions to extend the schema of users and groups, and then use those attributes for scoping and attribute mapping. If you're looking for directory extensions when provisioning from Active Directory to Microsoft Entra ID, see [Cloud sync directory extensions and custom attribute mapping](custom-attribute-mapping).

Important

Directory extensions for Microsoft Entra Cloud Sync are supported only for applications with the identifier URI `api://<tenantId>/CloudSyncCustomExtensionsApp` and the [Tenant Schema Extension App](../connect/how-to-connect-sync-feature-directory-extensions#configuration-changes-in-azure-ad-made-by-the-wizard) created by Microsoft Entra Connect.

For step-by-step examples of extending the schema and then using directory extension attributes with cloud sync provisioning to Active Directory, see [Use directory extensions when provisioning to Active Directory](tutorial-directory-extension-group-provisioning). That article covers both users and groups.

## Ways to create directory extensions

You can create directory extensions in Microsoft Entra ID in several different ways. The following table provides links and additional information.

| Method | Description | URL |
| --- | --- | --- |
| Microsoft Graph | Create extensions using Microsoft Graph | [Create extensionProperty](/en-us/graph/api/application-post-extensionproperty?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true) |
| PowerShell | Create extensions using PowerShell | [New-MgApplicationExtensionProperty](/en-us/powershell/module/microsoft.graph.applications/new-mgapplicationextensionproperty) |
| Microsoft Entra Connect | Create extensions using Microsoft Entra Connect | [Create an extension attribute using Microsoft Entra Connect](../../app-provisioning/user-provisioning-sync-attributes-for-mapping#create-an-extension-attribute-using-azure-ad-connect) |