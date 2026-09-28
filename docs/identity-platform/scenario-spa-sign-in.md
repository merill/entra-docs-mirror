---
layout: Conceptual
title: Single-page app sign-in & sign-out code - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-spa-sign-in
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a single-page application (sign-in)
manager: pmwongera
ms.custom: 
ms.date: 2025-05-12T00:00:00.0000000Z
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 21db2aed-de6f-185b-bacf-ec00fbfba2bf
document_version_independent_id: 3f09d8fe-0b80-3055-3a6d-25c1de986eef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-spa-sign-in.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-spa-sign-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-spa-sign-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 79ee7b49-0123-ff57-89fc-87968fc6e5b2
---

# Single-page app sign-in & sign-out code - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Before you can get tokens to access APIs in your application, you need an authenticated user context. To authenticate a user, you can use a Pop-up window and/or a Redirect sign in method.

If your application has access to an authenticated user context or ID token, you can skip the sign in step, and directly acquire tokens. For details, see [Single sign-on (SSO) with user hint](msal-js-sso#with-user-hint).

## Choosing between a pop-up or redirect experience

The choice between a pop-up or redirect experience depends on your application flow.

- Use a pop-up window if you don't want users to move away from your main application page during authentication. Because the authentication redirect happens in a pop-up window, the state of the main application is preserved.
- Use a redirect if users have browser constraints or policies where pop-up windows are disabled. For example, there are [known issues with pop-up windows on Internet Explorer](msal-js-use-ie-browser).

## Sign in with a pop-up window

# [React](#tab/react)
To invoke a sign in experience when a user isn't already signed in, use the `MsalAuthenticationTemplate` function from `@azure/msal-react`. The MSAL React wrapper protects specific components by wrapping them in the `MsalAuthenticationTemplate` component.

```javascript
import { InteractionType } from "@azure/msal-browser";
import { MsalAuthenticationTemplate, useMsal } from "@azure/msal-react";

function WelcomeUser() {
  const { accounts } = useMsal();
  const username = accounts[0].username;

  return <p>Welcome, {username}</p>;
}

// Remember that MsalProvider must be rendered somewhere higher up in the component tree
function App() {
  return (
    <MsalAuthenticationTemplate interactionType={InteractionType.Popup}>
      <p>This will only render if a user is not signed-in.</p>
      <WelcomeUser />
    </MsalAuthenticationTemplate>
  );
}
```

To invoke a specific sign in experience based on user interaction (for example, button select), use the `AuthenticatedTemplate` and/or `UnauthenticatedTemplate` function from `@azure/msal-react`.

```javascript
import {
  useMsal,
  AuthenticatedTemplate,
  UnauthenticatedTemplate,
} from "@azure/msal-react";

function signInClickHandler(instance) {
  instance.loginPopup();
}

// SignInButton Component returns a button that invokes a popup sign in when clicked
function SignInButton() {
  // useMsal hook will return the PublicClientApplication instance you provided to MsalProvider
  const { instance } = useMsal();

  return <button onClick={() => signInClickHandler(instance)}>Sign In</button>;
}

function WelcomeUser() {
  const { accounts } = useMsal();
  const username = accounts[0].username;

  return <p>Welcome, {username}</p>;
}

// Remember that MsalProvider must be rendered somewhere higher up in the component tree
function App() {
  return (
    <>
      <AuthenticatedTemplate>
        <p>This will only render if a user is signed-in.</p>
        <WelcomeUser />
      </AuthenticatedTemplate>
      <UnauthenticatedTemplate>
        <p>This will only render if a user is not signed-in.</p>
        <SignInButton />
      </UnauthenticatedTemplate>
    </>
  );
}
```

# [JavaScript (MSAL.js)](#tab/javascript)
```javascript
const config = {
  auth: {
    clientId: "your_app_id",
    redirectUri: "your_app_redirect_uri", //defaults to application start page
    postLogoutRedirectUri: "your_app_logout_redirect_uri",
  },
};

const loginRequest = {
  scopes: ["User.ReadWrite"],
};

let accountId = "";

const myMsal = new PublicClientApplication(config);

myMsal
  .loginPopup(loginRequest)
  .then(function (loginResponse) {
    accountId = loginResponse.account.homeAccountId;
    // Display signed-in user content, call API, etc.
  })
  .catch(function (error) {
    //login failure
    console.log(error);
  });
```

# [Angular (MSAL.js)](#tab/angular)
To invoke a sign in experience for a specific route, import `@angular/router` and add `MsalGuard` to the route definition.

```javascript
// In app-routing.module.ts
import { NgModule } from "@angular/core";
import { Routes, RouterModule } from "@angular/router";
import { ProfileComponent } from "./profile/profile.component";
import { MsalGuard } from "@azure/msal-angular";
import { HomeComponent } from "./home/home.component";

const routes: Routes = [
  {
    path: "profile",
    component: ProfileComponent,
    canActivate: [MsalGuard],
  },
  {
    path: "",
    component: HomeComponent,
  },
];

@NgModule({
  imports: [RouterModule.forRoot(routes, { useHash: false })],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

To enable a pop-up window experience, set the `interactionType` configuration to `InteractionType.Popup` in the `MsalGuardConfiguration`. You can also pass the scopes that require consent.

```javascript
// In app.module.ts
import { PublicClientApplication, InteractionType } from "@azure/msal-browser";
import { MsalModule } from "@azure/msal-angular";

@NgModule({
  imports: [
    MsalModule.forRoot(
      new PublicClientApplication({
        auth: {
          clientId: "your_app_id",
        },
        cache: {
          cacheLocation: "localStorage",
          storeAuthStateInCookie: isIE,
        },
      }),
      {
        interactionType: InteractionType.Popup, // MsalGuard Configuration
        authRequest: {
          scopes: ["User.Read"],
        },
      },
      null
    ),
  ],
})
export class AppModule {}
```

---

## Sign in with a redirect

# [React](#tab/react)
To invoke a sign in experience when a user isn't signed in, use the `MsalAuthenticationTemplate` function from `@azure/msal-react`.

```javascript
import { InteractionType } from "@azure/msal-browser";
import { MsalAuthenticationTemplate, useMsal } from "@azure/msal-react";

function WelcomeUser() {
  const { accounts } = useMsal();
  const username = accounts[0].username;

  return <p>Welcome, {username}</p>;
}

// Remember that MsalProvider must be rendered somewhere higher up in the component tree
function App() {
  return (
    <MsalAuthenticationTemplate interactionType={InteractionType.Redirect}>
      <p>This will only render if a user is not signed-in.</p>
      <WelcomeUser />
    </MsalAuthenticationTemplate>
  );
}
```

To invoke a specific sign in experience based on user interaction (for example, button select), use the `AuthenticatedTemplate` and/or `UnauthenticatedTemplate` function from `@azure/msal-react`.

```javascript
import {
  useMsal,
  AuthenticatedTemplate,
  UnauthenticatedTemplate,
} from "@azure/msal-react";

function signInClickHandler(instance) {
  instance.loginRedirect();
}

// SignInButton Component returns a button that invokes a popup login when clicked
function SignInButton() {
  // useMsal hook will return the PublicClientApplication instance you provided to MsalProvider
  const { instance } = useMsal();

  return <button onClick={() => signInClickHandler(instance)}>Sign In</button>;
}

function WelcomeUser() {
  const { accounts } = useMsal();
  const username = accounts[0].username;

  return <p>Welcome, {username}</p>;
}

// Remember that MsalProvider must be rendered somewhere higher up in the component tree
function App() {
  return (
    <>
      <AuthenticatedTemplate>
        <p>This will only render if a user is signed-in.</p>
        <WelcomeUser />
      </AuthenticatedTemplate>
      <UnauthenticatedTemplate>
        <p>This will only render if a user is not signed-in.</p>
        <SignInButton />
      </UnauthenticatedTemplate>
    </>
  );
}
```

# [JavaScript (MSAL.js)](#tab/javascript)
```javascript
const config = {
  auth: {
    clientId: "your_app_id",
    redirectUri: "your_app_redirect_uri", //defaults to application start page
    postLogoutRedirectUri: "your_app_logout_redirect_uri",
  },
};

const loginRequest = {
  scopes: ["User.ReadWrite"],
};

let accountId = "";

const myMsal = new PublicClientApplication(config);

function handleResponse(response) {
  if (response !== null) {
    accountId = response.account.homeAccountId;
    // Display signed-in user content, call API, etc.
  } else {
    // In case multiple accounts exist, you can select
    const currentAccounts = myMsal.getAllAccounts();

    if (currentAccounts.length === 0) {
      // no accounts signed-in, attempt to sign a user in
      myMsal.loginRedirect(loginRequest);
    } else if (currentAccounts.length > 1) {
      // Add choose account code here
    } else if (currentAccounts.length === 1) {
      accountId = currentAccounts[0].homeAccountId;
    }
  }
}

myMsal.handleRedirectPromise().then(handleResponse);
```

# [Angular (MSAL.js)](#tab/angular)
To enable a redirect experience, set the `interactionType` configuration to `InteractionType.Redirect` in the `MsalGuardConfiguration`, and then bootstrap `MsalRedirectComponent` to handle redirects.

```javascript
// In app.module.ts
import { PublicClientApplication, InteractionType } from "@azure/msal-browser";
import { MsalModule, MsalRedirectComponent } from "@azure/msal-angular";

@NgModule({
  imports: [
    MsalModule.forRoot(
      new PublicClientApplication({
        auth: {
          clientId: "Enter_the_Application_Id_Here",
        },
        cache: {
          cacheLocation: "localStorage",
          storeAuthStateInCookie: isIE,
        },
      }),
      {
        interactionType: InteractionType.Redirect, // Msal Guard Configuration
        authRequest: {
          scopes: ["user.read"],
        },
      },
      null
    ),
  ],
  bootstrap: [AppComponent, MsalRedirectComponent],
})
export class AppModule {}
```

---

## Sign out behavior on browsers

To ensure secure sign out of one or more apps, the following methods are recommended:

- On shared devices, users should use a browser's private/incognito mode and close all browser windows before they step away from the device.
- On devices that aren't shared, users should use an operating system lock screen to lock or sign out of their entire operating system session on the device. Microsoft uses its sign out page to remind users of these privacy and security best practices.

For more information, see Microsoft's [internet privacy best practices](https://support.microsoft.com/en-us/windows/protect-your-privacy-on-the-internet-ffe36513-e208-7532-6f95-a3b1c8760dfa).

If a user chooses not to sign out using the recommendations, the following are other methods to enable sign out functionality:

- Microsoft's OpenID Connect's [Front Channel Logout](https://openid.net/specs/openid-connect-frontchannel-1_0.html) for federated sign out. You can use this option when an app shares a sign in state with a new app, but manages its own session tokens/cookies. There are some limitations to this implementation where content is blocked, for example when browsers block third-party cookies.
- Pop-up window and/or a Redirect for local app sign out. The pop-up and redirect methods end the user's session at the endpoint and for the local app. But, these methods might not immediately clear the session for other federated applications if front-channel communication is blocked.

## Sign out with a pop-up window

MSAL.js v2 and higher provides a `logoutPopup` method that clears the cache in browser storage and opens a pop-up window to the Microsoft Entra sign out page. After sign out, the redirect defaults to the sign in start page, and the pop-up is closed.

For the after sign out experience, you can set the `postLogoutRedirectUri` to redirect the user to a specific URI. This URI should be registered as a redirect URI in your application registration. You can also configure `logoutPopup` to redirect the main window to a different page, such as the home page or sign in page by passing `mainWindowRedirectUri` as part of the request.

# [React](#tab/react)
```javascript
import {
  useMsal,
  AuthenticatedTemplate,
  UnauthenticatedTemplate,
} from "@azure/msal-react";

function signOutClickHandler(instance) {
  const logoutRequest = {
    account: instance.getAccountByHomeId(homeAccountId),
    mainWindowRedirectUri: "your_app_main_window_redirect_uri",
    postLogoutRedirectUri: "your_app_logout_redirect_uri",
  };
  instance.logoutPopup(logoutRequest);
}

// SignOutButton component returns a button that invokes a pop-up sign out when clicked
function SignOutButton() {
  // useMsal hook will return the PublicClientApplication instance you provided to MsalProvider
  const { instance } = useMsal();

  return (
    <button onClick={() => signOutClickHandler(instance)}>Sign Out</button>
  );
}

// Remember that MsalProvider must be rendered somewhere higher up in the component tree
function App() {
  return (
    <>
      <AuthenticatedTemplate>
        <p>This will only render if a user is signed-in.</p>
        <SignOutButton />
      </AuthenticatedTemplate>
      <UnauthenticatedTemplate>
        <p>This will only render if a user is not signed-in.</p>
      </UnauthenticatedTemplate>
    </>
  );
}
```

# [JavaScript (MSAL.js)](#tab/javascript)
```javascript
const config = {
  auth: {
    clientId: "your_app_id",
    redirectUri: "your_app_redirect_uri", // defaults to application start page
    postLogoutRedirectUri: "your_app_logout_redirect_uri",
  },
};

const myMsal = new PublicClientApplication(config);

// you can select which account application should sign out
const logoutRequest = {
  account: myMsal.getAccountByHomeId(homeAccountId),
  mainWindowRedirectUri: "your_app_main_window_redirect_uri",
};

await myMsal.logoutPopup(logoutRequest);
```

# [Angular (MSAL.js)](#tab/angular)
```javascript
// In app.module.ts
@NgModule({
    imports: [
        MsalModule.forRoot( new PublicClientApplication({
            auth: {
                clientId: 'your_app_id',
                postLogoutRedirectUri: 'your_app_logout_redirect_uri'
            }
        }), null, null)
    ]
})

// In app.component.ts
logout() {
    this.authService.logoutPopup({
        mainWindowRedirectUri: "/"
    });
}
```

---

## Sign out with a redirect

MSAL.js provides a `logoutRedirect` method in v2 that clears the cache in browser storage and redirects to the Microsoft Entra sign out page. After sign out, the redirect defaults to the sign in start page. For the after sign out experience, you can set the `postLogoutRedirectUri` to redirect the user to a specific URI. This URI should be registered as a redirect URI in your application registration.

Because the Microsoft's reminder of [internet privacy best practices](https://support.microsoft.com/en-us/windows/protect-your-privacy-on-the-internet-ffe36513-e208-7532-6f95-a3b1c8760dfa) about using a private browser and lock screen isn't shown in this method, you might want to describe best practices and remind users to close all browser windows when they've signed out of their app.

# [React](#tab/react)
```javascript
import {
  useMsal,
  AuthenticatedTemplate,
  UnauthenticatedTemplate,
} from "@azure/msal-react";

function signOutClickHandler(instance) {
  const logoutRequest = {
    account: instance.getAccountByHomeId(homeAccountId),
    postLogoutRedirectUri: "your_app_logout_redirect_uri",
  };
  instance.logoutRedirect(logoutRequest);
}

// SignOutButton Component returns a button that invokes a redirect logout when clicked
function SignOutButton() {
  // useMsal hook will return the PublicClientApplication instance you provided to MsalProvider
  const { instance } = useMsal();

  return (
    <button onClick={() => signOutClickHandler(instance)}>Sign Out</button>
  );
}

// Remember that MsalProvider must be rendered somewhere higher up in the component tree
function App() {
  return (
    <>
      <AuthenticatedTemplate>
        <p>This will only render if a user is signed-in.</p>
        <SignOutButton />
      </AuthenticatedTemplate>
      <UnauthenticatedTemplate>
        <p>This will only render if a user is not signed-in.</p>
      </UnauthenticatedTemplate>
    </>
  );
}
```

# [JavaScript (MSAL.js)](#tab/javascript)
```javascript
const config = {
  auth: {
    clientId: "your_app_id",
    redirectUri: "your_app_redirect_uri", //defaults to application start page
    postLogoutRedirectUri: "your_app_logout_redirect_uri",
  },
};

const myMsal = new PublicClientApplication(config);

// you can select which account application should sign out
const logoutRequest = {
  account: myMsal.getAccountByHomeId(homeAccountId),
};

myMsal.logoutRedirect(logoutRequest);
```

# [Angular (MSAL.js)](#tab/angular)
```javascript
// In app.module.ts
@NgModule({
    imports: [
        MsalModule.forRoot( new PublicClientApplication({
            auth: {
                clientId: 'your_app_id',
                postLogoutRedirectUri: 'your_app_logout_redirect_uri'
            }
        }), null, null)
    ]
})

// In app.component.ts
logout() {
    this.authService.logoutRedirect();
}
```

---