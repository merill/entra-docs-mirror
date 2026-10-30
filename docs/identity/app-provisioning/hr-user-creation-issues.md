---
layout: Conceptual
title: Troubleshoot user creation issues with HR provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/hr-user-creation-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to troubleshoot user creation issues with HR provisioning
ms.topic: troubleshooting
ms.date: 2026-08-20T00:00:00.0000000Z
ms.reviewer: chmutali
ai-usage: ai-assisted
locale: en-us
document_id: 105208c8-512c-37a7-55b8-9fef3e1b8eb4
document_version_independent_id: e2061c62-7321-59d7-be5e-35b1297069d9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/hr-user-creation-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/hr-user-creation-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/hr-user-creation-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cf601d5e-e785-8d8e-5db1-35dc4a7394eb
---

# Troubleshoot user creation issues with HR provisioning - Microsoft Entra ID | Microsoft Learn

## Null and empty values during user creation

**Applies to:**

- Workday to on-premises Active Directory user provisioning
- Workday to Microsoft Entra user provisioning
- SAP SuccessFactors to on-premises Active Directory user provisioning
- SAP SuccessFactors to Microsoft Entra user provisioning

| Troubleshooting | Details |
| --- | --- |
| **Issue** | The HR app returns a null or empty value during user creation, and the resulting target value doesn't match the intended behavior. For provisioning to on-premises Active Directory, the create operation might fail with the error message: `InvalidAttributeSyntax-LdapErr: The syntax is invalid. The parameter is incorrect. Error in attribute conversion operation, data 0, v3839`. |
| **Cause** | Attribute value clearing is disabled by default. If null value flow isn't enabled for both the source attribute and target mapping, the provisioning service might ignore the source value or pass an empty string to the target. The on-premises Active Directory connector can't set an empty string and returns the LDAP error. |
| **Resolution** | Check the provisioning logs and identify the source and target attributes associated with the null or empty value. Then configure the mapping based on whether the target attribute should remain empty, receive a fallback value, or ignore the source value. |

**Recommended resolutions**

Let's say the Workday attribute `BusinessTitle`, which maps to the Active Directory attribute `jobTitle`, can be null or empty.

- To leave the optional target attribute empty during creation and clear it during future updates, [enable attribute value clearing](clear-attribute-values) for both the source attribute and target mapping. If you configure **Default value if null**, the provisioning service uses that value during creation only.
- To populate a required target attribute with a nonblank fallback value, use the [Switch](functions-for-customizing-application-data#switch) function. For example, `Switch([BusinessTitle],[BusinessTitle],"","N/A")`.
- To ignore the null or empty source value instead of clearing the target attribute, use the [IgnoreFlowIfNullOrEmpty](functions-for-customizing-application-data#ignoreflowifnullorempty) function. For example, `IgnoreFlowIfNullOrEmpty([BusinessTitle])`.