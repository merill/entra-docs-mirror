---
layout: Conceptual
title: Configure single-page app - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-spa-app-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a single-page application (app's code configuration)
manager: pmwongera
ms.custom: 
ms.date: 2025-05-12T00:00:00.0000000Z
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 5e6e5855-ef79-2759-6773-f3a44886cb14
document_version_independent_id: 73154754-ea03-f123-3506-9173f7472322
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-spa-app-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-spa-app-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-spa-app-configuration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/80beb97b-18aa-44f8-9420-8f2a4cd448eb
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/8c09e0ef-0fde-4b6d-bf1b-b517e4db7f80
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: dcb64b8f-0722-aa04-7f7f-3a53ba3eb11b
---

# Configure single-page app - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Learn how to configure the code for your single-page application (SPA).

## Prerequisites

- Register a new app in the [Microsoft Entra admin center](https://entra.microsoft.com), configured for *Accounts in this organizational directory only*. Refer to [Register an application](quickstart-register-app) for more details. Record the following values from the application **Overview**page for later use:
    - Application (client) ID
    - Directory (tenant) ID
- Add the following redirect URIs using the **Single-page application** platform configuration. Refer to [How to add a redirect URI in your application](how-to-add-redirect-uri)for more details.
    - **Redirect URI**: `http://localhost:3000/`.

## Microsoft libraries supporting single-page apps

The following Microsoft libraries support single-page apps:

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs |
| --- | --- | --- | --- | --- | --- |
| React | [MSAL React](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-react)^2^ | [msal-react](https://www.npmjs.com/package/@azure/msal-react) | [Quickstart](quickstart-register-app) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) |
| JavaScript | [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser)^2^ | [msal-browser](https://www.npmjs.com/package/@azure/msal-browser) | [Quickstart](quickstart-register-app) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) |
| Angular | [MSAL Angular](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-angular)^2^ | [msal-angular](https://www.npmjs.com/package/@azure/msal-angular) | [Quickstart](quickstart-register-app) | ![Library can request ID tokens for user sign-in.](media/common/yes.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) |

## Application code configuration

In an MSAL library, the application registration information is passed as configuration during the library initialization.

# [React](#tab/react)
```javascript
import { PublicClientApplication } from "@azure/msal-browser";
import { MsalProvider } from "@azure/msal-react";

// Configuration object constructed.
const config = {
    auth: {
        clientId: 'your_client_id'
    }
};

// create PublicClientApplication instance
const publicClientApplication = new PublicClientApplication(config);

// Wrap your app component tree in the MsalProvider component
ReactDOM.render(
    <React.StrictMode>
        <MsalProvider instance={publicClientApplication}>
            <App />
        </ MsalProvider>
    </React.StrictMode>,
    document.getElementById('root')
);
```

# [JavaScript](#tab/javascript2)
```javascript
import * as Msal from "@azure/msal-browser"; // if using CDN, 'Msal' will be available in global scope

// Configuration object constructed.
const config = {
    auth: {
        clientId: 'your_client_id'
    }
};

// create PublicClientApplication instance
const publicClientApplication = new Msal.PublicClientApplication(config);
```

# [Angular](#tab/angular2)
```javascript
// In app.module.ts
import { MsalModule } from '@azure/msal-angular';
import { PublicClientApplication } from '@azure/msal-browser';

@NgModule({
    imports: [
        MsalModule.forRoot( new PublicClientApplication({
            auth: {
                clientId: 'Enter_the_Application_Id_Here',
            }
        }), null, null)
    ]
})
export class AppModule { }
```

---

For more information on the configurable options, see [Initializing application with MSAL.js](msal-js-initializing-client-applications).