---
layout: Conceptual
title: 'Microsoft Entra Connect: Declarative Provisioning Expressions - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/concept-azure-ad-connect-sync-declarative-provisioning-expressions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Explains the declarative provisioning expressions.
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: d3b41058-8eb8-9a6f-ea35-2ac6c82eaa85
document_version_independent_id: 07adf124-3399-76a3-3f26-3a8a5e09393a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/concept-azure-ad-connect-sync-declarative-provisioning-expressions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/concept-azure-ad-connect-sync-declarative-provisioning-expressions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/concept-azure-ad-connect-sync-declarative-provisioning-expressions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
- https://authoring-docs-microsoft.poolparty.biz/devrel/8b896464-3b7d-4e1f-84b0-9bb45aeb5f64
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1d2d671-9549-46e8-918c-24349120dbf5
platformId: 36191fe7-7a0a-2ae2-e6d3-9db35ff6295f
---

# Microsoft Entra Connect: Declarative Provisioning Expressions - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Connect Sync builds on declarative provisioning first introduced in Forefront Identity Manager 2010. It allows you to implement your complete identity integration business logic without the need to write compiled code.

An essential part of declarative provisioning is the expression language used in attribute flows. The language used is a subset of Microsoft® Visual Basic® for Applications (VBA). This language is used in Microsoft Office and users with experience of VBScript will also recognize it. The Declarative Provisioning Expression Language is only using functions and isn't a structured language. There are no methods or statements. Functions are instead nested to express program flow.

For more information, see [Welcome to the Visual Basic for Applications language reference for Office 2013](/en-us/office/vba/api/overview/language-reference).

The attributes are strongly typed. A function only accepts attributes of the correct type. It's also case-sensitive. Both function names and attribute names must have proper casing or an error is thrown.

## Language definitions and Identifiers

- Functions have a name followed by arguments in brackets: FunctionName(argument 1, argument N).
- Attributes are identified by square brackets: [attributeName]
- Parameters are identified by percent signs: %ParameterName%
- String constants are surrounded by quotes: For example, "Contoso" (Note: must use straight quotes "" and not smart quotes “”)
- Numeric values are expressed without quotes and expected to be decimal. Hexadecimal values are prefixed with &H. For example, 98052, &HFF
- Boolean values are expressed with constants: True, False.
- Built-in constants and literals are expressed with only their name: NULL, CRLF, IgnoreThisFlow

### Functions

Declarative provisioning uses many functions to enable the possibility to transform attribute values. These functions can be nested so the result from one function is passed in to another function.

`Function1(Function2(Function3()))`

The complete list of functions can be found in the [function reference](reference-connect-sync-functions-reference).

### Parameters

A parameter is defined either by a Connector or by an administrator using PowerShell. Parameters usually contain values that are different from system to system, for example, the name of the domain the user is located in. These parameters can be used in attribute flows.

The Active Directory Connector provided the following parameters for inbound Synchronization Rules:

| Parameter Name | Comment |
| --- | --- |
| Domain.Netbios | Netbios format of the domain currently being imported, for example FABRIKAMSALES |
| Domain.FQDN | FQDN format of the domain currently being imported, for example sales.fabrikam.com |
| Domain.LDAP | LDAP format of the domain currently being imported, for example DC=sales,DC=fabrikam,DC=com |
| Forest.Netbios | Netbios format of the forest name currently being imported, for example FABRIKAMCORP |
| Forest.FQDN | FQDN format of the forest name currently being imported, for example fabrikam.com |
| Forest.LDAP | LDAP format of the forest name currently being imported, for example DC=fabrikam,DC=com |

The system provides the following parameter, which is used to get the identifier of the Connector currently running:`Connector.ID`

Here's an example that populates the metaverse attribute domain with the netbios name of the domain where the user is located:`domain` &lt;- `%Domain.Netbios%`

### Operators

The following operators can be used:

- **Comparison**: &lt;, &lt;=, &lt;&gt;, =, &gt;, &gt;=
- **Mathematics**: +, -, \*, -
- **String**: & (concatenate)
- **Logical**: && (and), || (or)
- **Evaluation order**: ( )

Operators are evaluated left to right and have the same evaluation priority. That is, the \* (multiplier) isn't evaluated before - (subtraction). 2\*(5+3) isn't the same as 2\*5+3. The brackets ( ) are used to change the evaluation order when left to right evaluation order isn't appropriate.

## Multi-valued attributes

The functions can operate on both single-valued and multi-valued attributes. For multi-valued attributes, the function operates over every value and applies the same function to every value.

For example:`Trim([proxyAddresses])` Do a Trim of every value in the proxyAddress attribute.`Word([proxyAddresses],1,"@") & "@contoso.com"` For every value with an @-sign, replace the domain with @contoso.com.`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])` Look for the SIP-address and remove it from the values.