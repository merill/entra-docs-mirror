---
layout: Conceptual
title: Avoid page reloads (MSAL.js) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-js-avoid-page-reloads
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to avoid page reloads when acquiring and renewing tokens silently using the Microsoft Authentication Library for JavaScript (MSAL.js).
manager: pmwongera
ms.custom: 
ms.date: 2019-05-29T00:00:00.0000000Z
ms.reviewer: 
ms.topic: how-to
locale: en-us
document_id: a8559ad3-5bb7-dc0a-8148-8b0c669bae1b
document_version_independent_id: a9d9d349-ba37-263c-5584-a779b34e3c6c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-js-avoid-page-reloads.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-js-avoid-page-reloads
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-js-avoid-page-reloads.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fe39cd45-39de-4047-953d-db268d7c71d9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ca56ff04-5597-4109-9f5d-17812bae2fac
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 6b40a756-74c7-dd22-27d7-118c470ee643
---

# Avoid page reloads (MSAL.js) - Microsoft identity platform | Microsoft Learn

The Microsoft Authentication Library for JavaScript (MSAL.js) uses hidden `iframe` elements to acquire and renew tokens silently in the background. Microsoft Entra ID returns the token back to the registered `redirect_uri` specified in the token request(by default this is the app's root page). Since the response is a 302, it results in the HTML corresponding to the `redirect_uri` getting loaded in the `iframe`. Usually the app's `redirect_uri` is the root page and this causes it to reload.

In other cases, if navigating to the app's root page requires authentication, it might lead to nested `iframe` elements or `X-Frame-Options: deny` error.

Since MSAL.js can't dismiss the 302 issued by Microsoft Entra ID and is required to process the returned token, it can't prevent the `redirect_uri` from getting loaded in the `iframe`.

To avoid the entire app reloading again or other errors caused due to this, please follow these workarounds.

## Specify different HTML for the iframe

Set the `redirect_uri` property on config to a simple page, that doesn't require authentication. You have to make sure that it matches with the `redirect_uri` registered in Microsoft Entra admin center. This won't affect user's login experience as MSAL saves the start page when user begins the login process and redirects back to the exact location after login is completed.

## Initialization in your main app file

If your app is structured such that there is one central JavaScript file that defines the app's initialization, routing, and other stuff, you can conditionally load your app modules based on whether the app is loading in an `iframe` or not. For example:

In AngularJS: app.js

```javascript
// Check that the window is an iframe and not popup
if (window !== window.parent && !window.opener) {
angular.module('todoApp', ['ui.router', 'MsalAngular'])
    .config(['$httpProvider', 'msalAuthenticationServiceProvider','$locationProvider', function ($httpProvider, msalProvider,$locationProvider) {
        msalProvider.init(
            // msal configuration
        );

        $locationProvider.html5Mode(false).hashPrefix('');
    }]);
}
else {
    angular.module('todoApp', ['ui.router', 'MsalAngular'])
        .config(['$stateProvider', '$httpProvider', 'msalAuthenticationServiceProvider', '$locationProvider', function ($stateProvider, $httpProvider, msalProvider, $locationProvider) {
            $stateProvider.state("Home", {
                url: '/Home',
                controller: "homeCtrl",
                templateUrl: "/App/Views/Home.html",
            }).state("TodoList", {
                url: '/TodoList',
                controller: "todoListCtrl",
                templateUrl: "/App/Views/TodoList.html",
                requireLogin: true
            })

            $locationProvider.html5Mode(false).hashPrefix('');

            msalProvider.init(
                // msal configuration
            );
        }]);
}
```

In Angular: app.module.ts

```javascript
// Imports...
@NgModule({
  declarations: [
    AppComponent,
    MsalComponent,
    MainMenuComponent,
    AccountMenuComponent,
    OsNavComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule,
    ServiceWorkerModule.register('ngsw-worker.js', { enabled: environment.production }),
    MsalModule.forRoot(environment.MsalConfig),
    SuiModule,
    PagesModule
  ],
  providers: [
    HttpServiceHelper,
    {provide: HTTP_INTERCEPTORS, useClass: MsalInterceptor, multi: true},
    AuthService
  ],
  entryComponents: [
    AppComponent,
    MsalComponent
  ]
})
export class AppModule {
  constructor() {
    console.log('APP Module Constructor!');
  }

  ngDoBootstrap(ref: ApplicationRef) {
    if (window !== window.parent && !window.opener)
    {
      console.log("Bootstrap: MSAL");
      ref.bootstrap(MsalComponent);
    }
    else
    {
    //this.router.resetConfig(RouterModule);
      console.log("Bootstrap: App");
      ref.bootstrap(AppComponent);
    }
  }
}
```

MsalComponent:

```javascript
import { Component} from '@angular/core';
import { MsalService } from '@azure/msal-angular';

// This component is used only to avoid Angular reload
// when doing acquireTokenSilent()

@Component({
  selector: 'app-root',
  template: '',
})
export class MsalComponent {
  constructor(private Msal: MsalService) {
  }
}
```