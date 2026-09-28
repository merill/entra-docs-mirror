---
layout: Conceptual
title: Microsoft identity platform admin consent protocols - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/v2-admin-consent
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: A description of authorization in the Microsoft identity platform, including scopes, permissions, and consent.
manager: pmwongera
ms.custom: 
ms.date: 2023-11-08T00:00:00.0000000Z
ms.reviewer: ludwignick
ms.topic: reference
locale: en-us
document_id: a5837e27-7af3-12ad-3fd7-10995017581e
document_version_independent_id: 6ccb62ba-b31c-0cd5-c169-06c3ca899a4b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/v2-admin-consent.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/v2-admin-consent
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/v2-admin-consent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 0b59baa7-2026-ff1d-9cd7-b74fb39e45d0
---

# Microsoft identity platform admin consent protocols - Microsoft identity platform | Microsoft Learn

Some permissions require consent from an administrator before they can be granted within a tenant. You can also use the admin consent endpoint to grant permissions to an entire tenant.

## Recommended: Sign the user into your app

Typically, when you build an application that uses the admin consent endpoint, the app needs a page or view in which the admin can approve the app's permissions. This page can be part of the app's sign-up flow, part of the app's settings, or it can be a dedicated "connect" flow. In many cases, it makes sense for the app to show this "connect" view only after a user has signed in with a work or school Microsoft account.

When you sign the user into your app, you can identify the organization to which the admin belongs before asking them to approve the necessary permissions. Although not strictly necessary, it can help you create a more intuitive experience for your organizational users.

## Request the permissions from a directory admin

When you're ready to request permissions from your organization's admin, you can redirect the user to the Microsoft identity platform *admin consent endpoint*.

```none
https://login.microsoftonline.com/{tenant}/v2.0/adminconsent
        ?client_id=00001111-aaaa-2222-bbbb-3333cccc4444
        &scope=https://graph.microsoft.com/Calendars.Read https://graph.microsoft.com/Mail.Send
        &redirect_uri=http://localhost/myapp/permissions
        &state=12345
```

| Parameter | Condition | Description |
| --- | --- | --- |
| `tenant` | Required | The directory tenant that you want to request permission from. Can be provided in GUID or friendly name format OR generically referenced with `organizations` as seen in the example. Do not use 'common', as personal accounts cannot provide admin consent except in the context of a tenant. To ensure best compatibility with personal accounts that manage tenants, use the tenant ID when possible. |
| `client_id` | Required | The **Application (client) ID** that the [Microsoft Entra admin center – App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) experience assigned to your app. |
| `redirect_uri` | Required | The redirect URI where you want the response to be sent for your app to handle. It must exactly match one of the redirect URIs that you registered in the app registration portal. |
| `state` | Recommended | A value included in the request that will also be returned in the token response. It can be a string of any content you want. Use the state to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on. |
| `scope` | Required | Defines the set of permissions being requested by the application. This can be either static (using `/.default`) or dynamic scopes. This can include the OIDC scopes (`openid`, `profile`, `email`). |

At this point, Microsoft Entra ID requires a tenant administrator to sign in to complete the request. The administrator is asked to approve all the permissions that you have requested in the `scope` parameter. If you've used a static (`/.default`) value, it will function like the v1.0 admin consent endpoint and request consent for all scopes found in the required permissions (both user and app). In order to request app permissions, you must use the `/.default` value. If you don't want admins to see a given permission in the admin consent screen all the time when you use `/.default`, the best practice is to not put the permission in the required permissions section. Instead you can use dynamic consent to add the permissions you want to be in the consent screen at run time, rather than using `/.default`.

### Successful response

If the admin approves the permissions for your app, the successful response looks like this:

```none
http://localhost/myapp/permissions
    ?admin_consent=True
    &tenant=aaaabbbb-0000-cccc-1111-dddd2222eeee
    &scope=https://graph.microsoft.com/Calendars.Read https://graph.microsoft.com/Mail.Send
    &state=12345
```

| Parameter | Description |
| --- | --- |
| `tenant` | The directory tenant that granted your application the permissions it requested, in GUID format. |
| `state` | A value included in the request that also will be returned in the token response. It can be a string of any content you want. The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on. |
| `scope` | The set of permissions that were granted access to, for the application. |
| `admin_consent` | Will be set to `True`. |

Warning

Never use the **tenant ID** value of the `tenant` parameter to authenticate or authorize users. The tenant ID value can be updated and sent by bad actors to impersonate a response to your app. This can cause your application to be exposed to security incidents.

### Error response

```none
http://localhost/myapp/permissions
        ?admin_consent=True
        &error=consent_required
        &error_description=AADSTS65004%3a+The+resource+owner+or+authorization+server+denied+the+request.%0d%0aTrace+ID%3a+0000aaaa-11bb-cccc-dd22-eeeeee333333%0d%0aCorrelation+ID%3a+8478d534-5b2c-4325-8c2c-51395c342c89%0d%0aTimestamp%3a+2019-09-24+18%3a34%3a26Z
        &state=12345
```

Adding to the parameters seen in a successful response, error parameters are seen as below.

| Parameter | Description |
| --- | --- |
| `error` | An error code string that can be used to classify types of errors that occur, and can be used to react to errors. |
| `error_description` | A specific error message that can help a developer identify the root cause of an error. |
| `state` | A value included in the request that also will be returned in the token response. It can be a string of any content you want. The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on. |
| `admin_consent` | Will be set to `True` to indicate that this response occurred on an admin consent flow. |