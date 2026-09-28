---
layout: Conceptual
title: Use additional context in Authenticator notifications - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-mfa-additional-context
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to use additional context in multifactor authentication (MFA) notifications.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: mayurs
ms.custom: sfi-image-nochange
locale: en-us
document_id: fd355305-7e5d-014c-0aff-988233965650
document_version_independent_id: b46f45d0-0bfa-95d8-ca22-f7a348e526ee
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-mfa-additional-context.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: msgraph
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-mfa-additional-context
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-mfa-additional-context.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 4b84f8bd-4695-57c0-2851-96617699eda2
---

# Use additional context in Authenticator notifications - Microsoft Entra ID | Microsoft Learn

This article discusses how to improve the security of user sign-in by adding the application name and geographic location of the sign-in to Authenticator passwordless and push notifications.

## Prerequisites

- Your organization needs to enable Authenticator passwordless and push notifications for some users or groups by using the new Authentication methods policy. You can edit the Authentication methods policy by using the Microsoft Entra admin center or Microsoft Graph API.
- Additional context can be targeted to only a single group, which can be dynamic or nested. The group can be synchronized from on-premises or cloud-only.

## Passwordless phone sign-in and multifactor authentication

When a user receives a passwordless phone sign-in or multifactor authentication (MFA) push notification in Authenticator, they see the name of the application that requests the approval and the location based on the IP address from where the sign-in originated.

![Screenshot that shows additional context in the MFA push notification.](media/howto-authentication-passwordless-phone/location.png)

Admins can combine additional context with [number matching](how-to-mfa-number-match) to further improve sign-in security.

![Screenshot that shows additional context with number matching in the MFA push notification.](media/howto-authentication-passwordless-phone/location-with-number-match.png)

### Policy schema changes

You can enable and disable the application name and geographic location separately. Under `featureSettings`, you can use the following name mapping for each feature:

- **Application name**: `displayAppInformationRequiredState`
- **Geographic location**: `displayLocationInformationRequiredState`

Note

Make sure that you use the new policy schema for Microsoft Graph APIs. In Graph Explorer, you need to consent to the `Policy.Read.All` and `Policy.ReadWrite.AuthenticationMethod` permissions.

Identify your single target group for each of the features. Then use the following API endpoint to change `displayAppInformationRequiredState` or `displayLocationInformationRequiredState properties` under `featureSettings` to `enabled` and include or exclude the groups you want:

```msgraph
GET https://graph.microsoft.com/v1.0/authenticationMethodsPolicy/authenticationMethodConfigurations/MicrosoftAuthenticator
```

For more information, see [microsoftAuthenticatorAuthenticationMethodConfiguration resource type](/en-us/graph/api/resources/microsoftAuthenticatorAuthenticationMethodConfiguration).

#### Example of how to enable additional context for all users

In `featureSettings`, change `displayAppInformationRequiredState` and `displayLocationInformationRequiredState` from `default` to `enabled`.

The value of Authentication mode is either `any` or `push`, depending on whether or not you also want to enable passwordless phone sign-in. In these examples, we use `any`, but if you don't want to allow passwordless, use `push`.

You might need to `PATCH` the entire schema to prevent overwriting any previous configuration. In that case, do a `GET` first. Then update only the relevant fields and then `PATCH`. The following example shows how to update `displayAppInformationRequiredState` and `displayLocationInformationRequiredState` under `featureSettings`.

Only users who are enabled for Authenticator under `includeTargets` see the application name or geographic location. Users who aren't enabled for Authenticator don't see these features.

```json
//Retrieve your existing policy via a GET. 
//Leverage the Response body to create the Request body section. Then update the Request body similar to the Request body as shown below.
//Change the Query to PATCH and Run query
 
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodConfigurations/$entity",
    "@odata.type": "#microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration",
    "id": "MicrosoftAuthenticator",
    "state": "enabled",
    "featureSettings": {
        "displayAppInformationRequiredState": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "all_users"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        },
        "displayLocationInformationRequiredState": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "all_users"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        }
    },
    "includeTargets@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodsPolicy/authenticationMethodConfigurations('MicrosoftAuthenticator')/microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration/includeTargets",
    "includeTargets": [
        {
            "targetType": "group",
            "id": "all_users",
            "isRegistrationRequired": false,
            "authenticationMode": "any",
        }
    ]
} 
```

#### Example of how to enable application name and geographic location for separate groups

In `featureSettings`, change `displayAppInformationRequiredState` and `displayLocationInformationRequiredState` from `default` to `enabled`. Inside `includeTarget` for each `featureSetting`, change the ID from `all_users` to the object ID of the group from the Microsoft Entra admin center.

You need to `PATCH` the entire schema to prevent overwriting any previous configuration. We recommend that you do a `GET` first. Then update only the relevant fields and then `PATCH`. The following example shows an update to `displayAppInformationRequiredState` and `displayLocationInformationRequiredState` under `featureSettings`.

Only users who are enabled for Authenticator under `includeTargets` see the application name or geographic location. Users who aren't enabled for Authenticator don't see these features.

```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodConfigurations/$entity",
    "@odata.type": "#microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration",
    "id": "MicrosoftAuthenticator",
    "state": "enabled",
    "featureSettings": {
        "displayAppInformationRequiredState": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "44561710-f0cb-4ac9-ab9c-e6c394370823"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        },
        "displayLocationInformationRequiredState": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "a229e768-961a-4401-aadb-11d836885c11"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        }
    },
    "includeTargets@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodsPolicy/authenticationMethodConfigurations('MicrosoftAuthenticator')/microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration/includeTargets",
    "includeTargets": [
        {
            "targetType": "group",
            "id": "all_users",
            "isRegistrationRequired": false,
            "authenticationMode": "any",
        }
    ]
}
```

To verify, run `GET` again and verify the object ID:

```msgraph
GET https://graph.microsoft.com/v1.0/authenticationMethodsPolicy/authenticationMethodConfigurations/MicrosoftAuthenticator
```

#### Example of how to disable the application name and only enable the geographic location

In `featureSettings`, change the state of `displayAppInformationRequiredState` to `default` or `disabled` and `displayLocationInformationRequiredState` to `enabled`. Inside `includeTarget` for each `featureSetting` value, change the ID from `all_users` to the object ID of the group from the Microsoft Entra admin center.

You need to `PATCH` the entire schema to prevent overwriting any previous configuration. We recommend that you do a `GET` first. Then update only the relevant fields and then `PATCH`. The following example shows an update to `displayAppInformationRequiredState` and `displayLocationInformationRequiredState` under `featureSettings`.

Only users who are enabled for Authenticator under `includeTargets` see the application name or geographic location. Users who aren't enabled for Authenticator don't see these features.

```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodConfigurations/$entity",
    "@odata.type": "#microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration",
    "id": "MicrosoftAuthenticator",
    "state": "enabled",
    "featureSettings": {
        "displayAppInformationRequiredState": {
            "state": "disabled",
            "includeTarget": {
                "targetType": "group",
                "id": "44561710-f0cb-4ac9-ab9c-e6c394370823"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        },
        "displayLocationInformationRequiredState": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "a229e768-961a-4401-aadb-11d836885c11"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        }
    },
    "includeTargets@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodsPolicy/authenticationMethodConfigurations('MicrosoftAuthenticator')/microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration/includeTargets",
    "includeTargets": [
        {
            "targetType": "group",
            "id": "all_users",
            "isRegistrationRequired": false,
            "authenticationMode": "any",
        }
    ]
}
```

#### Example of how to exclude a group from the application name and geographic location

In addition, for each of the features, you change the ID of `excludeTarget` to the object ID of the group from the Microsoft Entra admin center. This change excludes that group from seeing the application name or geographic location.

You need to `PATCH` the entire schema to prevent overwriting any previous configuration. We recommend that you do a `GET` first. Then update only the relevant fields and then `PATCH`. The following example shows an update to `displayAppInformationRequiredState` and `displayLocationInformationRequiredState` under `featureSettings`.

Only users who are enabled for Authenticator under `includeTargets` see the application name or geographic location. Users who aren't enabled for Authenticator don't see these features.

```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodConfigurations/$entity",
    "@odata.type": "#microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration",
    "id": "MicrosoftAuthenticator",
    "state": "enabled",
    "featureSettings": {
        "displayAppInformationRequiredState": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "44561710-f0cb-4ac9-ab9c-e6c394370823"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "5af8a0da-5420-4d69-bf3c-8b129f3449ce"
            }
        },
        "displayLocationInformationRequiredState": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "a229e768-961a-4401-aadb-11d836885c11"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "b6bab067-5f28-4dac-ab30-7169311d69e8"
            }
        }
    },
    "includeTargets@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodsPolicy/authenticationMethodConfigurations('MicrosoftAuthenticator')/microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration/includeTargets",
    "includeTargets": [
        {
            "targetType": "group",
            "id": "all_users",
            "isRegistrationRequired": false,
            "authenticationMode": "any",
        }
    ]
}
```

#### Example of removing the excluded group

In `featureSettings`, change the states of `displayAppInformationRequiredState` from `default` to `enabled`. Change the ID of `excludeTarget` to `00000000-0000-0000-0000-000000000000`.

You need to `PATCH` the entire schema to prevent overwriting any previous configuration. We recommend that you do a `GET` first. Then update only the relevant fields and then `PATCH`. The following example shows an update to `displayAppInformationRequiredState` and `displayLocationInformationRequiredState` under `featureSettings`.

Only users who are enabled for Authenticator under `includeTargets` see the application name or geographic location. Users who aren't enabled for Authenticator don't see these features.

```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodConfigurations/$entity",
    "@odata.type": "#microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration",
    "id": "MicrosoftAuthenticator",
    "state": "enabled",
    "featureSettings": {
        " displayAppInformationRequiredState ": {
            "state": "enabled",
            "includeTarget": {
                "targetType": "group",
                "id": "1ca44590-e896-4dbe-98ed-b140b1e7a53a"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": " 00000000-0000-0000-0000-000000000000"
            }
        }
    },
    "includeTargets@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodsPolicy/authenticationMethodConfigurations('MicrosoftAuthenticator')/microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration/includeTargets",
    "includeTargets": [
        {
            "targetType": "group",
            "id": "all_users",
            "isRegistrationRequired": false,
            "authenticationMode": "any"
        }
    ]
}
```

### Turn off additional context

To turn off additional context, you need to `PATCH``displayAppInformationRequiredState` and `displayLocationInformationRequiredState` from `enabled` to `disabled`/`default`. You can also turn off only one of the features.

```json
{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodConfigurations/$entity",
    "@odata.type": "#microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration",
    "id": "MicrosoftAuthenticator",
    "state": "enabled",
    "featureSettings": {
        "displayAppInformationRequiredState": {
            "state": "disabled",
            "includeTarget": {
                "targetType": "group",
                "id": "44561710-f0cb-4ac9-ab9c-e6c394370823"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        },
        "displayLocationInformationRequiredState": {
            "state": "disabled",
            "includeTarget": {
                "targetType": "group",
                "id": "a229e768-961a-4401-aadb-11d836885c11"
            },
            "excludeTarget": {
                "targetType": "group",
                "id": "00000000-0000-0000-0000-000000000000"
            }
        }
    },
    "includeTargets@odata.context": "https://graph.microsoft.com/v1.0/$metadata#authenticationMethodsPolicy/authenticationMethodConfigurations('MicrosoftAuthenticator')/microsoft.graph.microsoftAuthenticatorAuthenticationMethodConfiguration/includeTargets",
    "includeTargets": [
        {
            "targetType": "group",
            "id": "all_users",
            "isRegistrationRequired": false,
            "authenticationMode": "any",
        }
    ]
}
```

## Enable additional context in the Microsoft Entra admin center

To enable the application name or geographic location in the Microsoft Entra admin center, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Microsoft Authenticator**.
3. On the **Basics** tab, select **Yes** and **All users** to enable the policy for everyone. Change **Authentication mode** to **Any**.

    Only users who are enabled for Authenticator here are included in the policy to show the application name or geographic location of the sign-in, or excluded from it. Users who aren't enabled for Authenticator can't see the application name or geographic location.

    ![Screenshot that shows how to enable Authenticator settings for Any authentication mode.](media/how-to-mfa-additional-context/enable-settings-additional-context.png)
4. On the **Configure** tab, for **Show application name in push and passwordless notifications**, change **Status** to **Enabled**. Choose who to include or exclude from the policy, and then select **Save**.

    ![Screenshot that shows how to enable the application name.](media/how-to-mfa-additional-context/enable-app-name.png)

    Then do the same for **Show geographic location in push and passwordless notifications**.

    ![Screenshot that shows how to enable the geographic location.](media/how-to-mfa-additional-context/enable-geolocation.png)

    You can configure the application name and geographic location separately. For example, the following policy enables the application name and geographic location for all users but excludes the Operations group from seeing the geographic location.

    ![Screenshot that shows how to enable the application name and geographic location separately.](media/how-to-mfa-additional-context/exclude.png)

## Known issues

- Additional context isn't supported for Network Policy Server (NPS) or Active Directory Federation Services.
- Users can modify the location reported by iOS and Android devices. As a result, Authenticator is updating its security baseline for Location-Based Access Control (LBAC) Conditional Access policies. Authenticator denies authentications where the user might be using a different location than the actual GPS location of the mobile device where Authenticator is installed.

    In the November 2023 release of Authenticator, users who modify the location of their device see a denial message in Authenticator when they do an LBAC authentication. Beginning in January 2024, any users who run older Authenticator versions are blocked from LBAC authentication with a modified location:

    - Authenticator version 6.2309.6329 or earlier on Android
    - Authenticator version 6.7.16 or earlier on iOS

    To find which users run older versions of Authenticator, use [Microsoft Graph APIs](/en-us/graph/api/resources/microsoftauthenticatorauthenticationmethod#properties).