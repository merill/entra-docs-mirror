---
layout: Conceptual
title: Web API that calls web APIs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-web-api-call-api-call-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: 'Build a web API that calls other APIs using the Microsoft identity platform. Learn how to acquire tokens and make secure API calls.  '
manager: pmwongera
ms.custom: 
ms.date: 2025-03-21T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: b124de3b-0981-7064-5ff6-43fd67eeb36d
document_version_independent_id: 0c36165d-80b7-56ba-8208-3e13b9f754e6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-web-api-call-api-call-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-web-api-call-api-call-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-web-api-call-api-call-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: d92ddbc8-cba2-3e07-da21-e17d7b5132b1
---

# Web API that calls web APIs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

After you have a token, you can call a protected web API. You usually call the downstream APIs from the controller or pages of your web API.

## Controller code

# [ASP.NET Core](#tab/aspnetcore)
When you use *Microsoft.Identity.Web*, you have three usage scenarios:

- Option 1: Call Microsoft Graph with the SDK
- Option 2: Call a downstream web API with the helper class
- Option 3: Call a downstream web API without the helper class

#### Option 1: Call Microsoft Graph with the SDK

In this scenario, you've added the **Microsoft.Identity.Web.GraphServiceClient** NuGet package and added `.AddMicrosoftGraph()` in *Startup.cs* as specified in [Code configuration](scenario-web-api-call-api-app-configuration#option-1-call-microsoft-graph), and you can directly inject the `GraphServiceClient` in your controller or page constructor for use in the actions. The following example Razor page displays the photo of the signed-in user.

```csharp
 [Authorize]
 [AuthorizeForScopes(Scopes = new[] { "user.read" })]
 public class IndexModel : PageModel
 {
     private readonly GraphServiceClient _graphServiceClient;

     public IndexModel(GraphServiceClient graphServiceClient)
     {
         _graphServiceClient = graphServiceClient;
     }

     public async Task OnGet()
     {
         var user = await _graphServiceClient.Me.GetAsync();
         try
         {
             using (var photoStream = await _graphServiceClient.Me.Photo.Content.GetAsync())
             {
                 byte[] photoByte = ((MemoryStream)photoStream).ToArray();
                 ViewData["photo"] = Convert.ToBase64String(photoByte);
             }
             ViewData["name"] = user.DisplayName;
         }
         catch (Exception)
         {
             ViewData["photo"] = null;
         }
     }
 }
```

#### Option 2: Call a downstream web API with the helper class

In this scenario, you've added `.AddDownstreamApi()` in *Startup.cs* as specified in [Code configuration](scenario-web-api-call-api-app-configuration#option-2-call-a-downstream-web-api-other-than-microsoft-graph), and you can directly inject an `IDownstreamWebApi` service in your controller or page constructor and use it in the actions:

```csharp
 [Authorize]
 [AuthorizeForScopes(ScopeKeySection = "TodoList:Scopes")]
 public class TodoListController : Controller
 {
     private IDownstreamWebApi _downstreamWebApi;
     private const string ServiceName = "TodoList";

     public TodoListController(IDownstreamWebApi downstreamWebApi)
     {
         _downstreamWebApi = downstreamWebApi;
     }

     public async Task<ActionResult> Details(int id)
     {
         var value = await _downstreamWebApi.CallApiForUserAsync(
             ServiceName,
             options =>
             {
                 options.RelativePath = $"me";
             });
         return View(value);
     }
```

The `CallApiForUserAsync` method also has strongly typed generic overrides that enable you to directly receive an object. For example, the following method received a `Todo` instance, which is a strongly typed representation of the JSON returned by the web API.

```csharp
 // GET: TodoList/Details/5
 public async Task<ActionResult> Details(int id)
 {
     var value = await _downstreamWebApi.CallApiForUserAsync<object, Todo>(
         ServiceName,
         null,
         options =>
         {
             options.HttpMethod = HttpMethod.Get;
             options.RelativePath = $"api/todolist/{id}";
         });
     return View(value);
 }
```

#### Option 3: Call a downstream web API without the helper class

If you've decided to get an authorization header using the `IAuthorizationHeaderProvider` interface, the following code continues the example code shown in [A web API that calls web APIs: Acquire a token for the app](scenario-web-api-call-api-acquire-token). The code is called in the actions of the API controllers. It calls a downstream API named *todolist*.

After acquiring the token, use it as a bearer token to call the downstream API.

```csharp
private async Task CallTodoListService(string accessToken)
{
  // After the token has been returned by Microsoft.Identity.Web, add it to the HTTP authorization header before making the call to access the todolist service.
  authorizationHeader = await authorizationHeaderProvider.GetAuthorizationHeaderForUserAsync(scopes);
  _httpClient.DefaultRequestHeaders["Authorization"] = authorizationHeader;

  // Call the todolist service.
  HttpResponseMessage response = await _httpClient.GetAsync(TodoListBaseAddress + "/api/todolist");
  // ...
}
```

# [ASP.NET](#tab/aspnet)
When you use *Microsoft.Identity.Web*, you have three usage options for calling an API:

- Option 1: Call Microsoft Graph with the Microsoft Graph SDK
- Option 2: Call a downstream web API with the helper class
- Option 3: Call a downstream web API without the helper class

#### Option 1: Call Microsoft Graph with the SDK from OWIN app

You call Microsoft Graph by adding `AddMicrosoftGraph` in *Startup.cs* as specified in [Code configuration](scenario-web-app-call-api-app-configuration#option-1-call-microsoft-graph). Use the `GetGraphServiceClient()` extension method on the controller to get the `GraphServiceClient` in your controller or page constructor for use in the actions. The following example displays the photo of the signed-in user.

```csharp
[Authorize]
public class HomeController : Controller
{

 public async Task GetIndex()
 {
  var graphServiceClient = this.GetGraphServiceClient();
  var user = await graphServiceClient.Me.GetAsync();
  try
  {
   using (var photoStream = await graphServiceClient.Me.Photo.Content.GetAsync())
   {
    byte[] photoByte = ((MemoryStream)photoStream).ToArray();
    ViewData["photo"] = Convert.ToBase64String(photoByte);
   }
   ViewData["name"] = user.DisplayName;
  }
  catch (Exception)
  {
   ViewData["photo"] = null;
  }
 }
}
```

#### Option 2: Call a downstream web API with the helper class from OWIN app

You want to call a web API other than Microsoft Graph. In that case, add `AddDownstreamApi` in *Startup.cs* as specified in [Code configuration](scenario-web-app-call-api-app-configuration#option-2-call-a-downstream-web-api-other-than-microsoft-graph). Use the `GetDownstreamApi` extension method on the controller to get the `IDownstreamApi` service:

```csharp
[Authorize]
public class TodoListController : Controller
{ 
  public async Task<ActionResult> Details(int id)
  {
    var downstreamApi = this.GetDownstreamApi();
    var value = await downstreamApi.CallApiForUserAsync(
      ServiceName,
      options =>
      {
        options.RelativePath = $"me";
      });
      return View(value);
  }
}
```

The `CallApiForUserAsync` also has strongly typed generic overrides that enable you to directly receive an object. For example, the following method receives a `Todo` instance, which is a strongly typed representation of the JSON returned by the web API.

```csharp
    // GET: TodoList/Details/5
    public async Task<ActionResult> Details(int id)
    {
        var downstreamApi = this.GetDownstreamApi();
        var value = await downstreamApi.GetForUserAsync<object, Todo>(
            ServiceName,
            null,
            options =>
            {
                options.RelativePath = $"api/todolist/{id}";
            });
        return View(value);
    }
```

#### Option 3: Call a downstream web API without the helper class from OWIN app

You've decided to acquire an authorization header using the `IAuthorizationHeaderProvider` service, and you now need to use it in your `HttpClient` or `HttpRequest`. In that case, the following code continues the example code shown in [A web API that calls web APIs: Acquire a token for the app](scenario-web-api-call-api-acquire-token). The code is called in the actions of the web API controllers.

```csharp
public async Task<IActionResult> Profile()
{
  // Acquire the access token.
  string[] scopes = new string[]{"user.read"};
  var IAuthorizationHeaderProvider = this.GetAuthorizationHeaderProvider();
  string authorizationHeader = await IAuthorizationHeaderProvider.GetAuthorizationHeaderForUserAsync(scopes);

  // Use the access token to call a protected web API.
  HttpClient httpClient = new HttpClient();
  client.DefaultRequestHeaders.Add("Authorization", authorizationHeader);

  var response = await httpClient.GetAsync($"{webOptions.GraphApiUrl}/beta/me");

  if (response.StatusCode == HttpStatusCode.OK)
  {
    var content = await response.Content.ReadAsStringAsync();

    dynamic me = JsonConvert.DeserializeObject(content);
    ViewData["Me"] = me;
  }

  return View();
}
```

# [Java](#tab/java)
The following code continues the example code that's shown in [A web API that calls web APIs: Acquire a token for the app](scenario-web-api-call-api-acquire-token). The code is called in the actions of the API controllers. It calls the downstream API MS Graph.

After you've acquired the token, use it as a bearer token to call the downstream API.

```java
private String callMicrosoftGraphMeEndpoint(String accessToken){
    RestTemplate restTemplate = new RestTemplate();

    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_JSON);

    headers.set("Authorization", "Bearer " + accessToken);

    HttpEntity<String> entity = new HttpEntity<>(null, headers);

    String result = restTemplate.exchange("https://graph.microsoft.com/v1.0/me", HttpMethod.GET,
            entity, String.class).getBody();

    return result;
}
```

# [Python](#tab/python)
A sample demonstrating this flow with MSAL Python is available at [ms-identity-python-on-behalf-of](https://github.com/Azure-Samples/ms-identity-python-on-behalf-of).

---