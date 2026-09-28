---
layout: Conceptual
title: Get a token in a web app that calls web APIs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-web-app-call-api-acquire-token
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to acquire a token for a web app that calls web APIs
manager: pmwongera
ms.date: 2025-01-30T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 19609d01-2128-d7ec-6ee1-7c9b3e86cb35
document_version_independent_id: 0a5ce83e-b17f-9d1c-786e-50ef3958c203
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-web-app-call-api-acquire-token.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-web-app-call-api-acquire-token
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-web-app-call-api-acquire-token.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://authoring-docs-microsoft.poolparty.biz/devrel/d452572f-6212-498f-9050-ca4a9e50a425
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/a12e40b7-59a2-4437-96e2-166ce622b864
platformId: 1eddbf42-21ad-38e4-6d68-c4f2b1b16ab4
---

# Get a token in a web app that calls web APIs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

You've built your client application object. Now, you use it to acquire a token to call a web API. In ASP.NET or ASP.NET Core, calling a web API is done in the controller:

- Get a token for the web API by using the token cache. To get this token, you call the Microsoft Authentication Library (MSAL) `AcquireTokenSilent` method (or the equivalent in Microsoft.Identity.Web).
- Call the protected API, passing the access token to it as a parameter.

# [ASP.NET Core](#tab/aspnetcore)
*Microsoft.Identity.Web* adds extension methods that provide convenience services for calling Microsoft Graph or a downstream web API. These methods are explained in detail in [A web app that calls web APIs: Call an API](scenario-web-app-call-api-call-api). With these helper methods, you don't need to manually acquire a token.

If, however, you do want to manually acquire a token, the following code shows an example of using *Microsoft.Identity.Web* to do so in a home controller. It calls Microsoft Graph using the REST API (instead of the Microsoft Graph SDK). Usually, you don't need to get a token, you need to build an Authorization header that you add to your request. To get an authorization header, you inject the `IAuthorizationHeaderProvider` service by dependency injection in your controller's constructor (or your page constructor if you use Blazor), and you use it in your controller actions. This interface has methods that produce a string containing the protocol (Bearer, Pop, ...) and a token. To get an authorization header to call an API on behalf of the user, use (`CreateAuthorizationHeaderForUserAsync`). To get an authorization header to call a downstream API on behalf of the application itself, in a daemon scenario, use (`CreateAuthorizationHeaderForAppAsync`).

The controller methods are protected by an `[Authorize]` attribute that ensures only authenticated users can use the web app.

```csharp
[Authorize]
public class HomeController : Controller
{
 readonly IAuthorizationHeaderProvider authorizationHeaderProvider;

 public HomeController(IAuthorizationHeaderProvider authorizationHeaderProvider)
 {
  this.authorizationHeaderProvider = authorizationHeaderProvider;
 }

 // Code for the controller actions (see code below)

}
```

ASP.NET Core makes `IAuthorizationHeaderProvider` available by dependency injection.

Here's simplified code for the action of the `HomeController`, which gets a token to call Microsoft Graph:

```csharp
[AuthorizeForScopes(Scopes = new[] { "user.read" })]
public async Task<IActionResult> Profile()
{
 // Acquire the access token.
 string[] scopes = new string[]{"user.read"};
 string accessToken = await authorizationHeaderProvider.CreateAuthorizationHeaderForUserAsync(scopes);

 // Use the access token to call a protected web API.
 HttpClient client = new HttpClient();
 client.DefaultRequestHeaders.Add("Authorization", accessToken);
 string json = await client.GetStringAsync(url);
}
```

To better understand the code required for this scenario, see the phase 2 ([2-1-Web app Calls Microsoft Graph](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/2-WebApp-graph-user/2-1-Call-MSGraph)) step of the [ms-identity-aspnetcore-webapp-tutorial](https://github.com/Azure-Samples/ms-identity-aspnetcore-webapp-tutorial) tutorial.

The `AuthorizeForScopes` attribute on top of the controller action (or of the Razor page if you use a Razor template) is provided by Microsoft.Identity.Web. It ensures that the user is asked for consent if needed, and incrementally.

There are other complex variations, such as:

- Calling several APIs.
- Processing incremental consent and Conditional Access.

These advanced steps are covered in chapter 3 of the [3-WebApp-multi-APIs](https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/3-WebApp-multi-APIs) tutorial.

# [ASP.NET](#tab/aspnet)
The code for ASP.NET is similar to the code shown for ASP.NET Core:

- A controller action, protected by an `[Authorize]` attribute, extracts the tenant ID and user ID of the `ClaimsPrincipal` member of the controller (ASP.NET uses `HttpContext.User`). This ensures that only authenticated users can use the app. **Microsoft.Identity.Web** adds extension methods to the Controller that provide convenience services to call Microsoft Graph or a downstream web API, or to get an authorization header, or even a token. The methods used to call an API directly are explained in detail in [A web app that calls web APIs: Call an API](scenario-web-app-call-api-call-api). With these helper methods, you don't need to manually acquire a token.

If, however, you do want to manually acquire a token or build an authorization header, the following code shows how to use Microsoft.Identity.Web to do so in a controller. It calls an API (Microsoft Graph) using the REST API instead of the Microsoft Graph SDK.

To get an authorization header, you get an `IAuthorizationHeaderProvider` service from the controller using an extension method `GetAuthorizationHeaderProvider`. To get an authorization header to call an API on behalf of the user, use `CreateAuthorizationHeaderForUserAsync`. To get an authorization header to call a downstream API on behalf of the application itself, in a daemon scenario, use `CreateAuthorizationHeaderForAppAsync`.

The following snippet shows the action of the `HomeController`, which gets an authorization header to call Microsoft Graph as a REST API:

```csharp
[Authorize]
public class HomeController : Controller
{
 [AuthorizeForScopes(Scopes = new[] { "user.read" })]
 public async Task<IActionResult> Profile()
 {
  // Get an authorization header.
  IAuthorizationHeaderProvider authorizationHeaderProvider = this.GetAuthorizationHeaderProvider();
  string[] scopes = new string[]{"user.read"};
  string authorizationHeader = await authorizationHeaderProvider.CreateAuthorizationHeaderForUserAsync(scopes);

  // Use the access token to call a protected web API.
  HttpClient client = new HttpClient();
  client.DefaultRequestHeaders.Add("Authorization", authorizationHeader);
  string json = await client.GetStringAsync(url);
 }
}
```

The following snippet shows the action of the `HomeController`, which gets an access token to call Microsoft Graph as a REST API:

```csharp
[Authorize]
public class HomeController : Controller
{
 [AuthorizeForScopes(Scopes = new[] { "user.read" })]
 public async Task<IActionResult> Profile()
 {
  // Get an authorization header.
  ITokenAcquirer tokenAcquirer = TokenAcquirerFactory.GetDefaultInstance().GetTokenAcquirer();
  string[] scopes = new string[]{"user.read"};
  string token = await tokenAcquirer.GetTokenForUserAsync(scopes);

  // Use the access token to call a protected web API.
  HttpClient client = new HttpClient();
  client.DefaultRequestHeaders.Add("Authorization", $"Bearer {token}");
  string json = await client.GetStringAsync(url);
 }
}
```

# [Java](#tab/java)
In the Java sample, the code that calls an API is in the `getUsersFromGraph` method in [AuthPageController.java#L62](https://github.com/Azure-Samples/ms-identity-java-webapp/blob/d55ee4ac0ce2c43378f2c99fd6e6856d41bdf144/src/main/java/com/microsoft/azure/msalwebsample/AuthPageController.java#L62).

The method attempts to call `getAuthResultBySilentFlow`. If the user needs to consent to more scopes, the code processes the `MsalInteractionRequiredException` object to challenge the user.

```java
@RequestMapping("/msal4jsample/graph/me")
public ModelAndView getUserFromGraph(HttpServletRequest httpRequest, HttpServletResponse response)
        throws Throwable {

    IAuthenticationResult result;
    ModelAndView mav;
    try {
        result = authHelper.getAuthResultBySilentFlow(httpRequest, response);
    } catch (ExecutionException e) {
        if (e.getCause() instanceof MsalInteractionRequiredException) {

            // If the silent call returns MsalInteractionRequired, redirect to authorization endpoint
            // so user can consent to new scopes.
            String state = UUID.randomUUID().toString();
            String nonce = UUID.randomUUID().toString();

            SessionManagementHelper.storeStateAndNonceInSession(httpRequest.getSession(), state, nonce);

            String authorizationCodeUrl = authHelper.getAuthorizationCodeUrl(
                    httpRequest.getParameter("claims"),
                    "User.Read",
                    authHelper.getRedirectUriGraph(),
                    state,
                    nonce);

            return new ModelAndView("redirect:" + authorizationCodeUrl);
        } else {

            mav = new ModelAndView("error");
            mav.addObject("error", e);
            return mav;
        }
    }

    if (result == null) {
        mav = new ModelAndView("error");
        mav.addObject("error", new Exception("AuthenticationResult not found in session."));
    } else {
        mav = new ModelAndView("auth_page");
        setAccountInfo(mav, httpRequest);

        try {
            mav.addObject("userInfo", getUserInfoFromGraph(result.accessToken()));

            return mav;
        } catch (Exception e) {
            mav = new ModelAndView("error");
            mav.addObject("error", e);
        }
    }
    return mav;
}
// Code omitted here
```

# [Node.js](#tab/nodejs)
In the Node.js sample, the code that acquires a token is in the `acquireToken` method of the `AuthProvider` class.

```js
acquireToken(options = {}) {
    return async (req, res, next) => {
        try {
            const msalInstance = this.getMsalInstance(this.msalConfig);

            /**
             * If a token cache exists in the session, deserialize it and set it as the 
             * cache for the new MSAL CCA instance. For more, see: 
             * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/caching.md
             */
            if (req.session.tokenCache) {
                msalInstance.getTokenCache().deserialize(req.session.tokenCache);
            }

            const tokenResponse = await msalInstance.acquireTokenSilent({
                account: req.session.account,
                scopes: options.scopes || [],
            });

            /**
             * On successful token acquisition, write the updated token 
             * cache back to the session. For more, see: 
             * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/caching.md
             */
            req.session.tokenCache = msalInstance.getTokenCache().serialize();
            req.session.accessToken = tokenResponse.accessToken;
            req.session.idToken = tokenResponse.idToken;
            req.session.account = tokenResponse.account;

            res.redirect(options.successRedirect);
        } catch (error) {
            if (error instanceof msal.InteractionRequiredAuthError) {
                return this.login({
                    scopes: options.scopes || [],
                    redirectUri: options.redirectUri,
                    successRedirect: options.successRedirect || '/',
                })(req, res, next);
            }

            next(error);
        }
    };
}
```

This access token is then used to handle requests to the `/profile` endpoint:

```js
router.get('/profile',
    isAuthenticated, // check if user is authenticated
    async function (req, res, next) {
        try {
            const graphResponse = await fetch(GRAPH_ME_ENDPOINT, req.session.accessToken);
            res.render('profile', { profile: graphResponse });
        } catch (error) {
            next(error);
        }
    }
);
```

# [Python](#tab/python)
In the Python sample, the code that calls the API is in *app.py*.

The code attempts to get a token from the token cache. If it can't get a token, it redirects the user to the sign-in route. Otherwise, it can proceed to call the API.

```python
@app.route("/call_downstream_api")
def call_downstream_api():
    token = auth.get_token_for_user(app_config.SCOPE)
    if "error" in token:
        return redirect(url_for("login"))
    # Use access token to call downstream api
    api_result = requests.get(
        app_config.ENDPOINT,
        headers={'Authorization': 'Bearer ' + token['access_token']},
        timeout=30,
    ).json()
    return render_template('display.html', result=api_result)
```

---