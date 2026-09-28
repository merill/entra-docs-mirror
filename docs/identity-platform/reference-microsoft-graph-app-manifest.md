---
layout: Conceptual
title: Understand the app manifest (Microsoft Graph format) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/reference-microsoft-graph-app-manifest
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Describes the Microsoft Entra app manifest (Microsoft Graph format), which represents an application's identity configuration in a Microsoft Entra tenant.
manager: pmwongera
ms.topic: reference
ms.date: 2025-02-03T00:00:00.0000000Z
ms.custom: 
ms.reviewer: 
locale: en-us
document_id: bbfbca94-08cb-1afe-6d07-b882160bd19b
document_version_independent_id: bbfbca94-08cb-1afe-6d07-b882160bd19b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/reference-microsoft-graph-app-manifest.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/reference-microsoft-graph-app-manifest
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/reference-microsoft-graph-app-manifest.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9e2bf484-356a-c6c4-7efa-27302e818013
---

# Understand the app manifest (Microsoft Graph format) - Microsoft identity platform | Microsoft Learn

The application manifest contains all the attributes and their values of an app registration in the Microsoft identity platform.

A Microsoft Graph app manifest is a JSON object that represents an app registration. It's also called the [Microsoft Graph Application resource type](/en-us/graph/api/resources/application) or Microsoft Graph app object (application object). It contains all the attributes and their values of an app registration.

The application object you receive using [Microsoft Graph Get Application method](/en-us/graph/api/application-get) is the same JSON object you see in **App Registration manifest** page in the [Microsoft Entra admin center](https://entra.microsoft.com).

Note

For apps registered with your personal Microsoft account (MSA account), you will continue to see app manifests in Azure AD Graph format in the Microsoft Entra admin center until further notice. For more information, see [Microsoft Entra app manifest (Azure AD Graph format)](reference-app-manifest).

## Configure the Microsoft Graph app manifest

If you would like to configure Microsoft Graph App Manifest programmatically, you can either use [Microsoft Graph API](/en-us/graph/api/resources/application) or [Microsoft Graph PowerShell SDK](/en-us/powershell/module/microsoft.graph.applications/?view=graph-powershell-1.0&amp;preserve-view=true).

You can also configure the app manifest through the Microsoft Entra admin center. Most attributes can be configured using a UI element in **App registrations**. However, some attributes need to be configured by editing the app manifest directly in the **Manifest** page.

### Configure the app manifest in the Microsoft Entra admin center

To configure the Microsoft Graph app manifest:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as at least an [Application Developer](/en-us/entra/identity/role-based-access-control/permissions-reference#application-developer).
2. Browse to **Entra ID** &gt; **App registrations**.
3. Select the app you want to configure.
4. From the app's **Overview** page, select the **Manifest** section. A web-based manifest editor opens, allowing you to edit the manifest. Optionally, you can select **Download** to edit the manifest locally, and then use **Upload** to reapply it to your application.

## Manifest reference

This section describes the attributes found in the Microsoft Graph app manifest.

### id attribute

| Key | Value type |
| --- | --- |
| id | String |

This property is referred to as Object ID in the Microsoft Entra admin center. It's a unique identifier for the application object in the directory.

This ID isn't the identifier used to identify the app in any protocol transaction. It's used for the referencing the object in directory queries.

It's a not nullable and Read-only attribute.

Example:

```json
"id": "f7f9acfc-ae0c-4d6c-b489-0a81dc1652dd"
```

### appId attribute

| Key | Value type |
| --- | --- |
| appId | String |

This property is referred to as application (client) ID in the Microsoft Entra admin center. It's a unique identifier for the application object in the directory.

This ID is the identifier used to identify the app in any protocol transaction.

It's a not nullable and read-only attribute.

Example:

```json
"appId": "00001111-aaaa-2222-bbbb-3333cccc4444"
```

### addIns attribute

| Key | Value type |
| --- | --- |
| addIns | Collection |

Defines custom behavior that a consuming service can use to call an app in specific contexts. For example, applications that can render file streams may set the `addIns` property for its "FileHandler" functionality. This parameter lets services like Microsoft 365 call the application in the context of a document the user is working on.

Example:

```json
"addIns": [
    {
        "id": "968A844F-7A47-430C-9163-07AE7C31D407",
        "type": " FileHandler",
        "properties": [
            {
                "key": "version",
                "value": "2"
            }
        ]
    }
]
```

### appRoles

| Key | Value type |
| --- | --- |
| appRoles | Collection |

Specifies the collection of roles that an app may declare. These roles can be assigned to users, groups, or service principals. For more examples and info, see [Add app roles in your application and receive them in the token](howto-add-app-roles-in-apps).

App roles and exposed delegated permission scopes share a default limit of 700 permission definitions per application or service principal. Disabled definitions also count. See [App role limits](howto-add-app-roles-in-apps#app-role-limits) for counting rules and behavior for existing objects above the limit.

Example:

```json
"appRoles": [
    {
        "allowedMemberTypes": [
            "User"
        ],
        "description": "Read-only access to device information",
        "displayName": "Read Only",
        "id": "00001111-aaaa-2222-bbbb-3333cccc4444",
        "isEnabled": true,
        "value": "ReadOnly"
    }
]
```

### groupMembershipClaims

| Key | Value type |
| --- | --- |
| groupMembershipClaims | String |

Configures the `groups` claim issued in a user or OAuth 2.0 access token that the app expects. To set this attribute, use one of the following valid string values:

- `None`
- `SecurityGroup` (for security groups and Microsoft Entra roles)
- `ApplicationGroup` (this option includes only groups that are assigned to the application)
- `DirectoryRole` (gets the Microsoft Entra directory roles the user is a member of)
- `All` (this gets all of the security groups, distribution groups, and Microsoft Entra directory roles that the signed-in user is a member of).

Example:

```json
"groupMembershipClaims": "SecurityGroup"
```

### optionalClaims attribute

| Key | Value type |
| --- | --- |
| optionalClaims | String |

The optional claims returned in the token by the security token service for this specific app.

Apps that support both personal accounts and Microsoft Entra ID can't use optional claims. However, apps registered for just Microsoft Entra ID using the v2.0 endpoint can get the optional claims they requested in the manifest. For more info, see [Optional claims](optional-claims).

Example:

```json
"optionalClaims": {
    "idToken": [
        {
            "@odata.type": "microsoft.graph.optionalClaim"
        }
    ],
    "accessToken": [
        {
            "@odata.type": "microsoft.graph.optionalClaim"
        }
    ],
    "saml2Token": [
        {
            "@odata.type": "microsoft.graph.optionalClaim"
        }
    ]
}
```

### identifierUris attribute

| Key | Value type |
| --- | --- |
| identifierUris | String Array |

User-defined URIs that uniquely identify a web app within its Microsoft Entra tenant or verified customer owned domain. When an application is used as a resource app, the identifierUri value is used to uniquely identify and access the resource.

The following API and HTTP scheme-based application ID URI formats are supported. Replace the placeholder values as described in the list following the table.

| Supported application IDURI formats | Example app ID URIs |
| --- | --- |
| *api://&lt;appId&gt;* | *api://aaaabbbb-0000-cccc-1111-dddd2222eeee* |
| *api://&lt;tenantId&gt;/&lt;appId&gt;* | *api://aaaabbbb-0000-cccc-1111-dddd2222eeee/00001111-aaaa-2222-bbbb-3333cccc4444* |
| *api://&lt;tenantId&gt;/&lt;string&gt;* | *api://aaaabbbb-0000-cccc-1111-dddd2222eeee/api* |
| *api://&lt;string&gt;/&lt;appId&gt;* | *api://productapi/00001111-aaaa-2222-bbbb-3333cccc4444* |
| *https://&lt;tenantInitialDomain&gt;.onmicrosoft.com/&lt;string&gt;* | *`https://contoso.onmicrosoft.com/productsapi`* |
| *https://&lt;verifiedCustomDomain&gt;/&lt;string&gt;* | *`https://contoso.com/productsapi`* |
| *https://&lt;string&gt;.&lt;verifiedCustomDomain&gt;* | *`https://product.contoso.com`* |
| *https://&lt;string&gt;.&lt;verifiedCustomDomain&gt;/&lt;string&gt;* | *`https://product.contoso.com/productsapi`* |
| *api://&lt;string&gt;.&lt;verifiedCustomDomainOrInitialDomain&gt;/&lt;string&gt;* | *`api://contoso.com/productsapi`* |

- *&lt;appId&gt;* - The application identifier (appId) property of the application object.
- *&lt;string&gt;* - The string value for the host or the api path segment.
- *&lt;tenantId&gt;* - A GUID generated by Azure to represent the tenant within Azure.
- *&lt;tenantInitialDomain&gt;* - *&lt;tenantInitialDomain&gt;.onmicrosoft.com*, where *&lt;tenantInitialDomain&gt;* is the initial domain name the tenant creator specified at tenant creation.
- *&lt;verifiedCustomDomain&gt;* - A [verified custom domain](../fundamentals/add-custom-domain) configured for your Microsoft Entra tenant.

Note

If you use the *api://* scheme, you add a string value directly after the "api://". For example, *api://&lt;string&gt;*. That string value can be a GUID or an arbitrary string. If you add a GUID value, it must match either the app ID or the tenant ID. If you use a string value, it must use either a verified custom domain or initial domain of your tenant. The recommendation is to use *api://&lt;appId&gt;*.

Important

The application ID URI value must not end with a slash "/" character.

Important

The application ID URI value must be unique within your tenant.

Example:

```json
"identifierUris": "https://contoso.onmicrosoft.com/fc4d2d73-d05a-4a9b-85a8-4f2b3a5f38ed"
```

### keyCredentials attribute

| Key | Value type |
| --- | --- |
| keyCredentials | Collection |

Holds references to app-assigned credentials, string-based shared secrets and X.509 certificates. These credentials are used when requesting access tokens (when the app is acting as a client rather that as a resource).

Example:

```json
"keyCredentials": [
    {
        "customKeyIdentifier": null,
        "endDateTime": "2018-09-13T00:00:00Z",
        "keyId": "<guid>",
        "startDateTime": "2017-09-12T00:00:00Z",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value": null
    }
]
```

### displayName attribute

| Key | Value type |
| --- | --- |
| displayName | String |

The display name for the app.

Example:

```json
"displayName": "MyRegisteredApp"
```

### oauth2RequiredPostResponse attribute

| Key | Value type |
| --- | --- |
| oauth2RequiredPostResponse | Boolean |

Specifies whether, as part of OAuth 2.0 token requests, Microsoft Entra ID allows POST requests, as opposed to GET requests. The default is false, which specifies that only GET requests will be allowed.

Example:

```json
"oauth2RequirePostResponse": false
```

### parentalControlSettings attribute

| Key | Value type |
| --- | --- |
| parentalControlSettings | String |

- `countriesBlockedForMinors` specifies the countries/regions in which the app is blocked for minors.
- `legalAgeGroupRule` specifies the legal age group rule that applies to users of the app. Can be set to `Allow`, `RequireConsentForPrivacyServices`, `RequireConsentForMinors`, `RequireConsentForKids`, or `BlockMinors`.

Example:

```json
"parentalControlSettings": {
    "countriesBlockedForMinors": [],
    "legalAgeGroupRule": "Allow"
}
```

### passwordCredentials attribute

| Key | Value type |
| --- | --- |
| passwordCredentials | Collection |

See the description for the `keyCredentials` property.

Example:

```json
"passwordCredentials": [
    {
        "customKeyIdentifier": null,
        "displayName": "Generated by App Service",
        "endDateTime": "2022-10-19T17:59:59.6521653Z",
        "hint": "Nsn",
        "keyId": "<guid>",
        "secretText": null,
        "startDateTime": "2022-10-19T17:59:59.6521653Z"
    }
]
```

### publisherDomain attribute

| Key | Value type |
| --- | --- |
| publisherDomain | String |

The verified publisher domain for the application. Read-only. To edit the publisher domain of your app registration, please follow the steps listed in [Configure an app's publisher domain](/en-us/entra/identity-platform/howto-configure-publisher-domain).

Example:

```json
"publisherDomain": "{tenant}.onmicrosoft.com"
```

### requiredResourceAccess attribute

| Key | Value type |
| --- | --- |
| requiredResourceAccess | Collection |

With dynamic consent, `requiredResourceAccess` drives the admin consent experience and the user consent experience for users who are using static consent. However, this parameter doesn't drive the user consent experience for the general case.

- `resourceAppId` is the unique identifier for the resource that the app requires access to. This value should be equal to the appId declared on the target resource app.
- `resourceAccess` is an array that lists the OAuth2.0 permission scopes and app roles that the app requires from the specified resource. Contains the `id` and `type` values of the specified resources.

Example:

```json
"requiredResourceAccess": [
    {
        "resourceAppId": "00000002-0000-0000-c000-000000000000",
        "resourceAccess": [
            {
                "id": "311a71cc-e848-46a1-bdf8-97ff7156d8e6",
                "type": "Scope"
            }
        ]
    }
]
```

### samlMetadataUrl attribute

| Key | Value type |
| --- | --- |
| samlMetadataUrl | String |

The URL to the SAML metadata for the app.

Example:

```json
"samlMetadataUrl": "https://MyRegisteredAppSAMLMetadata"
```

### signInAudience attribute

| Key | Value type |
| --- | --- |
| signInAudience | String |

Specifies what Microsoft accounts are supported for the current application. Supported values are:

- `AzureADMyOrg` - Users with a Microsoft work or school account in my organization's Microsoft Entra tenant (for example, single tenant)
- `AzureADMultipleOrgs` - Users with a Microsoft work or school account in any organization's Microsoft Entra tenant (for example, multitenant)
- `AzureADandPersonalMicrosoftAccount` - Users with a personal Microsoft account, or a work or school account in any organization's Microsoft Entra tenant
- `PersonalMicrosoftAccount` - Personal accounts that are used to sign in to services like Xbox and Skype.

Example:

```json
"signInAudience": "AzureADandPersonalMicrosoftAccount"
```

### tags attribute

| Key | Value type |
| --- | --- |
| tags | String Array |

Custom strings that can be used to categorize and identify the application.

Individual tags must be between 1 and 256 characters (inclusive). No whitespaces or duplicate tags are allowed. There is no specific limit on the number of tags that can be added, subject to general manifest size limits.

Example:

```json
"tags": [
    "ProductionApp"
]
```

### isFallbackPublicClient attribute

| Key | Value type |
| --- | --- |
| isFallbackPublicClient | Boolean |

Specifies the fallback application type as public client, such as an installed application running on a mobile device. The default value of this attribute is false, which means the fallback application type is confidential client such as a web app. There are certain scenarios where Microsoft Entra ID can't determine the client application type. For example, the ROPC flow where it's configured without specifying a redirect URI. In those cases Microsoft Entra ID interprets the application type based on the value of this property.

Example:

```json
"isFallbackPublicClient": "false"
```

### info attribute

| Key | Value type |
| --- | --- |
| info | [informationalUrl](/en-us/graph/api/resources/informationalurl) |

Specifies basic profile information of the application including the app's marketing, support, terms of service, privacy statement and logo URLs.

Note that:

- "logoUrl" is a read-only property. You can't edit it in app manifest. Navigate to "branding and property" page in your desired app registration and use "Upload new logo" to upload a new logo.
- The terms of service and privacy statement are surfaced to users through the user consent experience. For more info, see How to: [Add Terms of service and privacy statement for registered Microsoft Entra apps](/en-us/azure/active-directory/develop/howto-add-terms-of-service-privacy-statement).

Example:

```json
"info": {
    "termsOfService": "https://MyRegisteredApp/termsofservice",
    "support": "https://MyRegisteredApp/support",
    "privacy": "https://MyRegisteredApp/privacystatement",
    "marketing": "https://MyRegisteredApp/marketing",
    "logoUrl": "https://MyRegisteredApp/logoUrl",
}
```

### api attribute

| Key | Value type |
| --- | --- |
| api | [apiApplication resource type](/en-us/graph/api/resources/apiapplication) |

Specifies settings for an application that implements a web API. It includes five properties:

| Property | Type | Description |
| --- | --- | --- |
| acceptMappedClaims | Boolean | When set to true, it allows an application to use claims mapping without specifying a custom signing key. Applications that receive tokens rely on the fact that the claim values are authoritatively issued by Microsoft Entra ID and can't be tampered with. However, when you modify the token contents through claims-mapping policies, these assumptions may no longer be correct. Applications must explicitly acknowledge that tokens have been modified by the creator of the claims-mapping policy to protect themselves from claims-mapping policies created by malicious actors. Warning: Don't set acceptMappedClaims property to true for multitenant apps, which can allow malicious actors to create claims-mapping policies for your app. |
| knownClientApplications | collection | Used for bundling consent if you have a solution that contains two parts: a client app and a custom web API app. If you set the appID of the client app to this value, the user only consents once to the client app. Microsoft Entra ID knows that consenting to the client means implicitly consenting to the web API and automatically provisions service principals for both APIs at the same time. Both the client and the web API app must be registered in the same tenant. |
| oauth2PermissionScopes | permissionScope collection | The definition of the delegated permissions exposed by the web API represented by this application registration. These delegated permissions may be requested by a client application, and may be granted by users or administrators during consent. Delegated permissions are sometimes referred to as OAuth 2.0 scopes. |
| preAuthorizedApplications | preAuthorizedApplication collection | Lists the client applications that are preauthorized with the specified delegated permissions to access this application's APIs. Users aren't required to consent to any preauthorized application (for the permissions specified). However, any other permissions not listed in preAuthorizedApplications (requested through incremental consent for example) will require user consent. |
| requestedAccessTokenVersion | Int32 | Specifies the access token version expected by this resource. This changes the version and format of the JWT produced independent of the endpoint or client used to request the access token. The endpoint used, v1.0 or v2.0, is chosen by the client and only impacts the version of id\_tokens. Resources need to explicitly configure *requestedAccessTokenVersion* to indicate the supported access token format. Possible values for *requestedAccessTokenVersion* are 1, 2, or null. If the value is null, this defaults to 1, which corresponds to the v1.0 endpoint. If **signInAudience** on the application is configured as AzureADandPersonalMicrosoftAccount or PersonalMicrosoftAccount, the value for this property must be 2. |

Example:

```json
"api": {
    "acceptMappedClaims": true,
    "knownClientApplications": [
        "f7f9acfc-ae0c-4d6c-b489-0a81dc1652dd"
    ],
    "oauth2PermissionScopes": [
        {
            "adminConsentDescription": "Allow the app to access resources on behalf of the signed-in user.",
            "adminConsentDisplayName": "Access resource1",
            "id": "<guid>",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow the app to access resource1 on your behalf.",
            "userConsentDisplayName": "Access resources",
            "value": "user_impersonation"
        }
    ],
    "preAuthorizedApplications": [
        {
            "appId": "00001111-aaaa-2222-bbbb-3333cccc4444",
            "permissionIds": [
                "8748f7db-21fe-4c83-8ab5-53033933c8f1"
            ]
        }
    ],

    "requestedAccessTokenVersion": 2
}
```

### web attribute

| Key | Value type |
| --- | --- |
| web | [webApplication resource type](/en-us/graph/api/resources/webapplication) |

Specifies settings for a web application. It includes four properties.

| Property | Type | Description |
| --- | --- | --- |
| homePageUrl | String | Home page or landing page of the application. |
| implicitGrantSettings | [implicitGrantSettings](/en-us/graph/api/resources/implicitgrantsettings) | Specifies whether this web application can request tokens using the OAuth 2.0 implicit flow. |
| logoutUrl | String | Specifies the URL that is used by Microsoft's authorization service to sign out a user using [front-channel](https://openid.net/specs/openid-connect-frontchannel-1_0.html), [back-channel](https://openid.net/specs/openid-connect-backchannel-1_0.html) or SAML sign out protocols. |
| redirectUris | String collection | Specifies the URLs where user tokens are sent for sign-in, or the redirect URIs where OAuth 2.0 authorization codes and access tokens are sent in the web platform. |

Example:

```json
"web": {
    "homePageUrl": "String",
    "implicitGrantSettings": {
        "enableIdTokenIssuance": "Boolean",
        "enableAccessTokenIssuance": "Boolean"
    },
    "logoutUrl": "String",
    "redirectUris": [
        "String"
    ]
}
```

### spa attribute

| Key | Value type |
| --- | --- |
| spa | [spaApplication resource type](/en-us/graph/api/resources/spaapplication) |

Specifies settings for a single-page application, including sign out URLs and redirect URIs for authorization codes and access tokens.

| Property | Type | Description |
| --- | --- | --- |
| redirectUris | String collection | Specifies the URLs where user tokens are sent for sign-in, or the redirect URIs where OAuth 2.0 authorization codes and access tokens are sent. |

Example:

```json
"spa": {
    "redirectUris": [
        "String"
    ]
}
```

### publicClient attribute

| Key | Value type |
| --- | --- |
| publicClient | [publicClientApplication resource type](/en-us/graph/api/resources/publicclientapplication) |

Specifies settings for nonweb app or nonweb API (for example, iOS, Android, mobile or other public clients such as an installed application running on a desktop device).

| Property | Type | Description |
| --- | --- | --- |
| redirectUris | String collection | Specifies the URLs where user tokens are sent for sign-in, or the redirect URIs where OAuth 2.0 authorization codes and access tokens are sent. |

Example:

```json
"publicClient": {
    "redirectUris": [
        "String"
    ]
}
```

## Common issues

### Manifest limits

Individual collections also have limits. App roles and exposed delegated permission scopes share a default limit of 700 permission definitions, separate from the aggregate manifest limit. See [App role limits](howto-add-app-roles-in-apps#app-role-limits).

An application manifest has multiple attributes that are referred to as collections; for example, appRoles, keyCredentials, knownClientApplications, identifierUris, redirectUris, requiredResourceAccess, and oauth2PermissionScopes. Within the complete application manifest for any application, the total number of entries in all the collections combined has been capped at 1200. If you previously specify 100 appRoles in the application manifest, then you're only left with 1,100 remaining entries to use across all other collections combined that make up the manifest.

Note

In case you try to add more than 1200 entries in the application manifest, you may see an error **"Failed to update application xxxxxx. Error details: The size of the manifest has exceeded its limit. Please reduce the number of values and retry your request."**

### Troubleshoot manifest migration from Azure AD Graph format to Microsoft Graph format

When you upload a previously downloaded app manifest in Azure AD Graph format, you may get the following error:

#### Failed to update {app name} application. Error detail: invalid property '{property name}'.\*\*

This might be due to the migration from Azure AD Graph to Microsoft Graph app manifest. Firstly, you should check if the app manifest is in [Azure AD Graph format](azure-active-directory-graph-app-manifest-deprecation#how-do-i-tell-the-format-of-my-app-manifest). If it is, you should [convert the app manifest to Microsoft Graph format](azure-active-directory-graph-app-manifest-deprecation#convert-an-app-manifest-in-azure-ad-graph-format-to-microsoft-graph-format).

**I can't find trustedCertificateSubjects attribute**

This is a Microsoft internal property. The portal shows v1.0 version of MS Graph app manifest while this property is only present in beta version of MS Graph app manifest. Please continue to edit this property using Azure AD Graph app manifest in Entra portal. We will expose MS Graph app manifest beta version in Entra portal before deprecating Azure AD Graph app manifest.