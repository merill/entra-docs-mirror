---
layout: Conceptual
title: Logging errors and exceptions in MSAL.js - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-logging-js
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to log errors and exceptions in MSAL.js
manager: dougeby
ms.custom: 
ms.date: 2023-12-19T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: concept-article
locale: en-us
document_id: 458301cb-79ae-0f32-8df3-c39ca6eabe2b
document_version_independent_id: 8ee3b8ee-2830-d72e-d743-07586def95cc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-logging-js.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-logging-js
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-logging-js.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: 48b60353-2574-e986-48fe-f5c5ea9d5ed3
---

# Logging errors and exceptions in MSAL.js - Microsoft identity platform | Microsoft Learn

The Microsoft Authentication Library (MSAL) apps generate log messages that can help diagnose issues. An app can configure logging with a few lines of code, and have custom control over the level of detail and whether or not personal and organizational data is logged. We recommend you create an MSAL logging implementation and provide a way for users to submit logs when they have authentication issues.

## Logging levels

MSAL provides several levels of logging detail:

- LogAlways: No level filtering is done on this log level. Log messages of all levels will be logged.
- Critical: Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention.
- Error: Indicates something has gone wrong and an error was generated. Used for debugging and identifying problems.
- Warning: There hasn't necessarily been an error or failure, but are intended for diagnostics and pinpointing problems.
- Informational: MSAL will log events intended for informational purposes not necessarily intended for debugging.
- Verbose (Default): MSAL logs the full details of library behavior.

Note

Not all log levels are available for all MSAL SDK's

## Personal and organizational data

By default, the MSAL logger doesn't capture any highly sensitive personal or organizational data. The library provides the option to enable logging personal and organizational data if you decide to do so.

The following sections provide more details about MSAL error logging for your application.

## Configure logging in MSAL.js

Enable logging in MSAL.js (JavaScript) by passing a loggerOptions object during the configuration for creating a `PublicClientApplication` instance. The only required config parameter is the client ID of the application. Everything else is optional, but may be required depending on your tenant and application model.

The loggerOptions object has the following properties:

- `loggerCallback`: a Callback function that can be provided by the developer to handle the logging of MSAL statements in a custom manner. Implement the `loggerCallback` function depending on how you want to redirect logs. The loggerCallback function has the following format `(level: LogLevel, message: string, containsPii: boolean): void`
    - The supported log levels are: `Error`, `Warning`, `Info`, and `Verbose`. The default is `Info`.
- `piiLoggingEnabled` (optional): if set to true, logs personal and organizational data. By default this is false so that your application doesn't log personal data. Personal data logs are never written to default outputs like Console, Logcat, or NSLog.

```javascript
import msal from "@azure/msal-browser"

const msalConfig = {
    auth: {
        clientId: "enter_client_id_here",
        authority: "https://login.microsoftonline.com/common",
        knownAuthorities: [],
        cloudDiscoveryMetadata: "",
        redirectUri: "enter_redirect_uri_here",
        postLogoutRedirectUri: "enter_postlogout_uri_here",
        navigateToLoginRequestUrl: true,
        clientCapabilities: ["CP1"]
    },
    cache: {
        cacheLocation: "sessionStorage",
        storeAuthStateInCookie: false,
        secureCookies: false
    },
    system: {
        loggerOptions: {
            logLevel: msal.LogLevel.Verbose,
            loggerCallback: (level, message, containsPii) => {
                if (containsPii) {
                    return;
                }
                switch (level) {
                    case msal.LogLevel.Error:
                        console.error(message);
                        return;
                    case msal.LogLevel.Info:
                        console.info(message);
                        return;
                    case msal.LogLevel.Verbose:
                        console.debug(message);
                        return;
                    case msal.LogLevel.Warning:
                        console.warn(message);
                        return;
                }
            },
            piiLoggingEnabled: false
        },
    },
};
```