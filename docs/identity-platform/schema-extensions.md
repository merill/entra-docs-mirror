---
layout: Conceptual
title: Directory extension attributes in claims - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/schema-extensions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Describes directory extension attributes that are used for sending user data to applications in token claims.
manager: pmwongera
ms.custom: 
ms.date: 2023-05-26T00:00:00.0000000Z
ms.reviewer: ludwignick, alamaral
ms.topic: concept-article
locale: en-us
document_id: bcfe59aa-9ba1-caef-d015-b6fd6f09ba30
document_version_independent_id: 41c5e5f6-7bf7-852c-fe48-b04c131639d7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/schema-extensions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/schema-extensions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/schema-extensions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 37212d1b-b994-5e1a-d2f5-9c32dc4fa5ec
---

# Directory extension attributes in claims - Microsoft identity platform | Microsoft Learn

Directory extension attributes provide a way to store more data on directory objects such as users. Only extension attributes on user objects can be used for emitting claims to applications. This article describes how to use directory extension attributes for sending user data to applications in token claims.

Note

Microsoft Graph provides three other extension mechanisms to customize Graph objects. These are the extension attributes 1-15, open extensions, and schema extensions. See the [Microsoft Graph documentation](/en-us/graph/extensibility-overview) for details. Data stored on Microsoft Graph objects using open and schema extensions aren't available as sources for claims in tokens.

Directory extension attributes are always associated with an application in the tenant. The name of the directory attribute includes the *appId* of the application in its name.

The identifier for a directory extension attribute is of the form `extension_xxxxxxxxx_AttributeName`. Where `xxxxxxxxx` is the *appId* of the application the extension was defined for, with only characters 0-9 and A-Z.

## Register and use directory extensions

Register directory extension attributes in one of the following ways:

- Configure Microsoft Entra Connect to create them and to sync data into them from on-premises. See [Microsoft Entra Connect Sync Directory Extensions](../identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions).
- Use Microsoft Graph to register, set the values of, and read from [directory extensions](/en-us/graph/extensibility-overview#directory-azure-ad-extensions). [PowerShell cmdlets](/en-us/powershell/azure/active-directory/using-extension-attributes-sample) are also available.

### Emit claims with data from Microsoft Entra Connect

Directory extension attributes created and synced using Microsoft Entra Connect are always associated with the application ID used by Microsoft Entra Connect. These attributes can be used as a source for claims both by configuring them as claims in **Enterprise Applications** configuration in the Portal. After a directory extension attribute is created using AD Connect, it's displayed in the SAML SSO claims configuration.

### Emit claims using Graph or PowerShell

If a directory extension attribute is registered for using Microsoft Graph or PowerShell, the application can be configured to receive data in that attribute when the user signs in. The application can be configured to receive data in directory extensions that are registered on the application using [optional claims](optional-claims) that can be set in the application manifest.

Multi-tenant applications can then register directory extension attributes for their own use. When the application is provisioned into a tenant, the associated directory extensions become available and consumed for users in that tenant. After the directory extension is available, it can be used to store and retrieve data using Microsoft Graph. The directory extension can also map to claims in tokens the Microsoft identity platform emits to applications.

If an application needs to send claims with data from an extension attribute that's registered on a different application, a [claims mapping policy](saml-claims-customization) must be used to map the extension attribute to the claim.

A common pattern for managing directory extension attributes is to register an application specifically for all the directory extensions that you need. When you use this type of application, all the extensions have the same appID in their name.

For example, the following code shows a claims-mapping policy to emit a single claim from a directory extension attribute in an OAuth/OIDC token:

```json
{
    "ClaimsMappingPolicy": {
        "Version": 1,
        "IncludeBasicClaimSet": "false",
        "ClaimsSchema": [{
                "Source": "User",
                "ExtensionID": "extension_xxxxxxx_test",
                "JWTClaimType": "http://schemas.contoso.com/identity/claims/exampleclaim"
            },
        ]
    }
}
```

Where `xxxxxxx` is the appID (or Client ID) of the application that the extension was registered with.

Warning

When you define a claims mapping policy for a directory extension attribute, use the `ExtensionID` property instead of the `ID` property within the body of the `ClaimsSchema` array, as shown in the previous example.

Tip

Case consistency is important when you set directory extension attributes on objects. Extension attribute names aren't case sensitive when being set up, but they are case sensitive when being read from the directory by the token service. If an extension attribute is set on a user object with the name "LegacyId" and on another user object with the name "legacyid", when the attribute is mapped to a claim using the name "LegacyId" the data is successfully retrieved and the claim included in the token for the first user but not the second.