---
layout: Conceptual
title: Configure restrictions on how applications can be configured - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-app-management-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: CelesteDG
description: Configure app management policies in Microsoft Entra ID to set restrictions on how apps and service principals in your tenant can be configured. Secure your environment with step‑by‑step guidance.
ms.topic: how-to
ms.date: 2025-07-23T00:00:00.0000000Z
ms.reviewer: arcrowe
ms.custom: enterprise-apps
locale: en-us
document_id: cfc964be-ee72-1886-6f2d-a8d7a38c88c3
document_version_independent_id: cfc964be-ee72-1886-6f2d-a8d7a38c88c3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/configure-app-management-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/configure-app-management-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/configure-app-management-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: ef7ce99f-5f6d-9a1c-7f7f-eef77f3f046d
---

# Configure restrictions on how applications can be configured - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to configure app management policies in Microsoft Entra ID to control how app owners and administrators can configure applications and service principals in your organization. This guidance helps administrators reduce security risks caused by insecure configurations.

The set of restrictions available to configure includes:

| Restriction name | Description | Security value | Availability |
| --- | --- | --- | --- |
| asymmetricKeyLifetime | Enforce a max lifetime range for an asymmetric key (certificate). | Reduces security risk from long-lived credentials | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). Referred to as `Restrict max certificate lifetime` in the Microsoft Entra admin center. |
| audiences | Restricts creation or promotion of apps based on signInAudience values. | Prevents unsanctioned multitenant or consumer-facing applications | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). Referred to as `Block multitenant applications` and `Block consumer account applications` in the Microsoft Entra admin center. |
| customPasswordAddition | Restrict a custom password secret on application or service principal. | Prevents new user-provided app passwords, which are more easily compromised than system-generated ones | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). Referred to as `Block custom passwords` in the Microsoft Entra admin center. |
| nonDefaultUriAddition | Block new identifier URIs for apps unless they're one of the default formats `api://{appId}` or `api://{tenantId}/{appId}`. | Reduces security risk from improper audience validation | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). Referred to as `Block custom identifier URIs` in the Microsoft Entra admin center. |
| uriAdditionWithoutUniqueTenantIdentifier | Block new identifier URIs for apps unless they're one of the [secure formats](https://aka.ms/identifier-uri-policy). | Reduces security risk from audience overlap | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). Referred to as `Block identifier URIs without unique tenant identifier` in the Microsoft Entra admin center. |
| passwordAddition | Block the addition of new passwords (also referred to as secrets) on applications altogether. | Prevents new passwords, which are the most easily compromised form of credential | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). In the Microsoft Entra admin center, combined with the `symmetricKeyAddition` restriction under the `Block password addition` setting. |
| passwordLifetime | Enforce a max lifetime range for a password secret. | Reduces security risk from long-lived credentials | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). In the Microsoft Entra admin center, combined with the `symmetricKeyLifetime` restriction under the `Restrict max password lifetime` setting. |
| symmetricKeyAddition | Restrict symmetric keys on applications. | Prevents new symmetric keys, which are effectively passwords - the most easily compromised form of credential | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). In the Microsoft Entra admin center, combined with the `passwordAddition` restriction under the `Block password addition` setting. |
| symmetricKeyLifetime | Enforce a max lifetime range for a symmetric key. | Reduces security risk from long-lived credentials | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true) and the [Microsoft Entra admin center](https://aka.ms/app-mgmt-policy-ux). In the Microsoft Entra admin center, combined with the `passwordLifetime` restriction under the `Restrict max password lifetime` setting. |
| trustedCertificateAuthority | Block new certificate credentials if the issuer isn't listed in the trusted certificate authority list. | Ensures only trusted CAs are used by apps in your tenant | Can be configured through [app management policy APIs](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true). |

To learn more about how the app management policy API works, visit the [API documentation](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true).

## Prerequisites

To configure app management policies, you need:

- A user account. If you don't already have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- The [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) role, AND the [Cloud App Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) or [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) role. OR, just the [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) role.

## Configure a restriction

You can configure app management policies in Microsoft Entra ID using either the Microsoft Entra admin center or Microsoft Graph API.

### Enable a restriction for all applications

This example blocks the addition of new passwords on all applications and service principals in your organization. A similar process can be used to enable other restrictions.

# [Microsoft Entra admin center](#tab/portal)
To block new passwords using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application policies**.
3. Select **Block password addition**.
4. Set the status to **On**. Ensure the 'Applies to' field is set to **All applications**.
5. Select **Save** to save your settings.

![Screenshot of the 'password addition' restriction.](media/configure-app-management-policies/enable-password-addition-restriction.png)

# [Microsoft Graph](#tab/graph)
To block new password additions on applications and service principals using Microsoft Graph:

1. Retrieve your existing tenant wide app management policy.

    ```http
    GET https://graph.microsoft.com/beta/policies/defaultAppManagementPolicy
    ```
2. Find the `passwordCredentials` collection under the `applicationRestrictions` and `servicePrincipalsRestrictions` property. In both collections, set the state of the `passwordAddition` restriction and the `symmetricKeyAddition` restriction to `enabled`. If other restrictions are already present in the collection, include them in the request to avoid accidentally disabling them.

    ```http
    PATCH https://graph.microsoft.com/beta/policies/defaultAppManagementPolicy
    
    {
        "applicationRestrictions": {
            "passwordCredentials": [
                {
                    "restrictionType": "passwordAddition",
                    "state": "enabled"
                },
                {
                    "restrictionType": "symmetricKeyAddition",
                    "state": "enabled"
                }
            ]
        },
          "servicePrincipalRestrictions": {
            "passwordCredentials": [
                {
                    "restrictionType": "passwordAddition",
                    "state": "enabled"
                },
                {
                    "restrictionType": "symmetricKeyAddition",
                    "state": "enabled"
                }
            ]
        }      
    }
    ```

---

### Grant an exception to an application

Sometimes, exceptions are needed to your tenant-wide rules. This example grants an app an exception to the restriction blocking custom identifier URIs, so it can still have custom URIs added to it. A similar process can be followed for other restrictions.

# [Microsoft Entra admin center](#tab/portal)
To grant an app an exception to the restriction blocking custom identifier URIs using the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application policies**.
3. Select **Block custom identifier URIs**.
4. Ensure the status is **On**. Set the 'Applies to' field to **All applications with exclusions**.
5. Under **Excluded apps**, select **Add applications**.
6. Choose the application you'd like to exclude from the restriction.
7. Select **Save** to save your settings.

![Screenshot of the 'custom identifier URI' restriction.](media/configure-app-management-policies/identifier-uri-restriction-with-exemption.png)

# [Microsoft Graph](#tab/graph)
To grant an app an exception to the restriction blocking custom identifier URIs using the Microsoft Graph:

1. Create a new custom app management policy. When creating it, set the `nonDefaultUriAddition` restriction under `restrictions.applicationRestrictions` to `disabled`.

    ```http
    POST https://graph.microsoft.com/beta/policies/appManagementPolicies
    
    {
        "displayName": "Identifier URI exemption policy",
        "description": "Policy granting an exemption to the nonDefaultUriAddition restriction",
        "isEnabled": true,
        "restrictions": {
            "applicationRestrictions": {
                "identifierUris": {
                    "nonDefaultUriAddition": {
                        "state": "disabled"
                    }
                }
            }
        }
    }
    ```
2. Record the ID of the new policy from the response.
3. Assign the new custom policy to the application you'd like to exempt.

    ```http
    POST https://graph.microsoft.com/beta/applications/{objectIdOfTheApplication}/appManagementPolicies/$ref
    
    {
        "@odata.id":"https://graph.microsoft.com/v1.0/policies/appManagementPolicies/{idOfTheCustomPolicy}"
    }
    ```
4. If you get an error indicating that this application already has a custom policy assigned, then instead modify that policy to include this new exclusion. Make sure the existing policy isn't assigned to any other applications, or they'll also receive the exclusion.

---

### Grant an exception to a user or service

Sometimes, exceptions need to be granted to the user or service creating or modifying the application. For example, imagine an automated process in your organization periodically creates applications and sets passwords on them. You want to block the new passwords in your organization, but you don't want to break this automated process while you're working on updating it. Application exceptions wouldn't work in this case, because the apps being created/updated don't exist yet! Instead, you can apply an exception to the process itself.

This type of exception - sometimes labeled an 'actor' or 'caller' exception - is configured using [custom security attributes](/en-us/entra/fundamentals/custom-security-attributes-overview). Because of this, you need two additional roles for this scenario, in addition to the roles from prerequisites.

- [Attribute Definition Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#attribute-definition-administrator)
- [Attribute Assignment Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#attribute-assignment-administrator)

Note

If you assign a caller-based exemption to a user, that user still may not be able to use the Entra admin center or Azure portal to modify applications in a way that violates the policy unless they have the [attribute assignment reader role](/en-us/entra/identity/role-based-access-control/permissions-reference#attribute-assignment-reader). This isn't required for other app management interfaces, like Microsoft Graph or Powershell.

This example grants a service an exception to the restriction enforcing a max lifetime on new certificates it adds to other applications and service principals. The service will be represented by its service principal. Find the service principal for a service by searching for it in [Enterprise applications](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/%7E/AppAppsPreview).

# [Microsoft Entra admin center](#tab/portal)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application policies**.
3. Select **Restrict max certificate lifetime**.
4. Ensure the status is **On**. Set the 'Applies to' field to **All applications with exclusions**.
5. Under **Excluded callers**, select **Add excluded callers**.
6. Choose the user or service principal whose calls to create/update apps you'd like to exclude from the restriction.
7. Select **Save** to save your settings.

![Screenshot of the 'restrict max certificate lifetime' restriction.](media/configure-app-management-policies/restrict-certificate-lifetime.png)

# [Microsoft Graph](#tab/graph)
##### Create a custom security attribute definition

This caller-based exemption is done through [custom security attributes](/en-us/entra/fundamentals/custom-security-attributes-overview). Custom security attributes are key-value pairs; they require a definition for the key-value pair to be created in the tenant, and then instances of the key-value pair can be added to specific users or service principals.

Custom security attribute definitions can be [created through the Microsoft Entra admin center](/en-us/entra/fundamentals/custom-security-attributes-add), but you can also do so using Microsoft Graph. First, [create an attribute set](/en-us/graph/api/directory-post-attributesets) (if you don't have one already). Attribute sets are containers for custom security attribute definitions.

```http
POST https://graph.microsoft.com/v1.0/directory/attributeSets 
{
    "id":"PolicyExemptions",
    "description":"Attributes for granting exemptions to policy",
    "maxAttributesPerSet":25
}
```

Then, [create the definition](/en-us/graph/api/directory-post-customsecurityattributedefinitions).

```http
POST https://graph.microsoft.com/v1.0/directory/customSecurityAttributeDefinitions
{
    "attributeSet": "PolicyExemptions",
    "description": "App mgmt policy exemption attributes",
    "isCollection": false,
    "isSearchable": true,
    "name": "AppManagementExemption",
    "status": "Available",
    "type": "String",
    "usePreDefinedValuesOnly": true,
    "allowedValues": [
        {
            "id": "ExemptFromCertificateLifetimeRestriction",
            "isActive": true
        }
    ]
}
```

These are just example values; you can name your custom security attribute anything you like. However, make sure that the custom security attribute definition you create is of `String` type, and `isCollection` is set to `false`. Currently, single-value string types are the only custom security attributes supported as exemption indicators in app management policies.

##### Add the custom security attribute as an exemption indicator

Update the `excludeActors` property under the `asymmetricKeyLifetime` restriction in `applicationRestrictions` and `servicePrincipalRestrictions`.

```http
PATCH https://graph.microsoft.com/beta/policies/defaultAppManagementPolicy

 {  
    "applicationRestrictions": {
        "keyCredentials": [
            {
                "restrictionType": "asymmetricKeyLifetime",
                "state": "enabled",
                "maxLifetime": "P180D",
                "excludeActors": {
                    "customSecurityAttributes": [
                        {
                            "@odata.type": "#microsoft.graph.customSecurityAttributeStringValueExemption",
                            "id": "PolicyExemptions_AppManagementExemption",  //This `id` value is the concatenation of "AttributeSet_AttributeName"
                            "operator": "equals",
                            "value": "ExemptFromCertificateLifetimeRestriction"
                        }
                    ]
                }
            }
        ]
    },
    "servicePrincipalRestrictions": {
        "keyCredentials": [
            {
                "restrictionType": "asymmetricKeyLifetime",
                "state": "enabled",
                "maxLifetime": "P180D",
                "excludeActors": {
                    "customSecurityAttributes": [
                        {
                            "@odata.type": "#microsoft.graph.customSecurityAttributeStringValueExemption",
                            "id": "PolicyExemptions_AppManagementExemption",  //This `id` value is the concatenation of "AttributeSet_AttributeName"
                            "operator": "equals",
                            "value": "ExemptFromCertificateLifetimeRestriction"
                        }
                    ]
                }
            }
        ]
    }
 }
```

This indicates to Microsoft Entra that you want users or service principals with that specific custom security attribute value assigned to them to be exempt from the policy.

##### Assign the custom security attribute to the service principal

Custom security attributes can be assigned to both [users](/en-us/entra/identity/users/users-custom-security-attributes) and [service principals](/en-us/entra/identity/enterprise-apps/custom-security-attributes-apps) through the Microsoft Entra admin center, but you can also do so using Microsoft Graph.

To assign to a service principal:

```http
PATCH https://graph.microsoft.com/v1.0/servicePrincipals/{id}
{
    "customSecurityAttributes":
    {
        "Engineering":
        {
            "@odata.type":"#Microsoft.DirectoryServices.CustomSecurityAttributeValue",
            "AppManagementExemption":"ExemptFromCertificateLifetimeRestriction"
        }
    }
}
```

Replace {id} with the object ID of the service principal.

Once this completes, the service principal with the custom security attribute assigned will be able to add a long-lived certificate to any app it can modify.

---

### Apply a restriction to a specific application

Sometimes, you aren't ready to apply a restriction to your entire tenant, but still want to apply the rule to a select set of security-sensitive applications. This example applies the restriction blocking custom passwords to a single application. A similar process can be followed for other restrictions.

# [Microsoft Entra admin center](#tab/portal)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Application policies**.
3. Select **Block custom passwords**.
4. Ensure the status is **On**. Set the 'Applies to' field to **Select applications**.
5. Select **Add applications**.
6. Choose the application you'd like to apply the restriction to.
7. Select **Save** to save your settings.

![Screenshot of the 'block custom passwords' restriction.](media/configure-app-management-policies/block-custom-passwords.png)

# [Microsoft Graph](#tab/graph)
1. Create a new custom app management policy. When creating it, set the `customPasswordAddition` restriction under `restrictions.passwordCredentials` to `enabled`.

    ```http
    POST https://graph.microsoft.com/beta/policies/appManagementPolicies
    
    {
        "displayName": "Custom password policy",
        "description": "Policy that enforces the custom password restriction",
        "isEnabled": true,
        "restrictions": {
            "passwordCredentials": [
                {
                    "restrictionType": "customPasswordAddition",
                    "state": "enabled"
                }
            ]
        }
    }
    ```
2. Record the ID of the new policy from the response.
3. Assign the new custom policy to the application you'd like to apply the restriction to.

    ```http
    POST https://graph.microsoft.com/beta/applications/{objectIdOfTheApplication}/appManagementPolicies/$ref
    
    {
        "@odata.id":"https://graph.microsoft.com/v1.0/policies/appManagementPolicies/{idOfTheCustomPolicy}"
    }
    ```
4. If you get an error indicating that this application already has a custom policy assigned, then instead modify that policy to include this new restriction. Make sure the existing policy isn't assigned to any other applications, or they'll also receive the enforcement.

---

### View your custom policies

[Custom policies](/en-us/graph/api/resources/appmanagementpolicy?view=graph-rest-beta&amp;preserve-view=true) are applied to specific applications and service principals. They're used to override the tenant-wide configuration for a specific app. You can learn more about that [here](/en-us/graph/api/resources/applicationauthenticationmethodpolicy?view=graph-rest-beta&amp;preserve-view=true).

The Microsoft Entra admin center automatically configures custom policies for you based on your intent. For example, if you want to grant an exemption to a restriction for a specific app, the Microsoft Entra admin center crafts the custom policy with that behavior behind the scenes, and assigns it to the application.

Because of this, the list of custom policies can't be viewed directly in the Microsoft Entra admin center. But they can be viewed through Microsoft Graph.

# [Microsoft Entra admin center](#tab/portal)
The list of custom policies can't be viewed directly in the Microsoft Entra admin center. Switch to the Microsoft Graph tab.

# [Microsoft Graph](#tab/graph)
```http
GET https://graph.microsoft.com/beta/policies/appManagementPolicies
```

---

### Fix your policy state for use in the Microsoft Entra admin center

If you have ever configured your app management policies outside of the Microsoft Entra admin center, you might have configured them in a way the portal doesn't expect. If so, when loading a restriction, you'll see an error message like:

`The restriction have been modified outside of this interface. To prevent data loss, editing is disabled until restrictions are synchronized.`

In order to get your restrictions back into a state that the Microsoft Entra admin center expects, you'll need to update them using Microsoft Graph.

# [Microsoft Entra admin center](#tab/portal)
This can't be done using the Microsoft Entra admin center. Switch to the Microsoft Graph tab.

# [Microsoft Graph](#tab/graph)
First, retrieve your tenant-wide app management policy.

```http
GET https://graph.microsoft.com/beta/policies/defaultAppManagementPolicy
```

Jump to the whichever restriction is blocked for you in the Microsoft Entra admin center.

##### Password addition

The **Block password addition** restriction expects all four of the following restrictions to be in the same state:

- The `passwordAddition` restriction in the `applicationRestrictions.passwordCredentials` collection
- The `passwordAddition` restriction in the `servicePrincipalRestrictions.passwordCredentials` collection
- The `symmetricKeyAddition` restriction in the `applicationRestrictions.passwordCredentials` collection
- The `symmetricKeyAddition` restriction in the `servicePrincipalRestrictions.passwordCredentials` collection

This means the properties of all four restrictions should match. Or, all four restrictions shouldn't be present in the policy.

##### Password lifetime

The **Restrict max password lifetime** restriction expects all four of the following restrictions to be in the same state:

- The `passwordLifetime` restriction in the `applicationRestrictions.passwordCredentials` collection
- The `passwordLifetime` restriction in the `servicePrincipalRestrictions.passwordCredentials` collection
- The `symmetricKeyLifetime` restriction in the `applicationRestrictions.passwordCredentials` collection
- The `symmetricKeyLifetime` restriction in the `servicePrincipalRestrictions.passwordCredentials` collection

This means the properties of all four restrictions should match. Or, all four restrictions shouldn't be present in the policy.

##### Certificate lifetime

The **Restrict max certificate lifetime** restriction expects all both of the following restrictions to be in the same state:

- The `asymmetricKeyLifetime` restriction in the `applicationRestrictions.keyCredentials` collection
- The `asymmetricKeyLifetime` restriction in the `servicePrincipalRestrictions.keyCredentials` collection

This means the properties of both restrictions should match. Or, both restrictions shouldn't be present in the policy.

---