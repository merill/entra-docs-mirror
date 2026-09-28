---
layout: Conceptual
title: Call a protected web API in an Android app using the Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/tutorial-mobile-app-android-call-web-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: The tutorials provide a step-by-step guide on how to call a protected web API in Android app for authentication.
manager: pmwongera
ms.topic: tutorial
ms.date: 2025-01-27T00:00:00.0000000Z
ms.custom: 
locale: en-us
document_id: 721e1691-43aa-57dc-37f0-9e281836576f
document_version_independent_id: 721e1691-43aa-57dc-37f0-9e281836576f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/tutorial-mobile-app-android-call-web-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/tutorial-mobile-app-android-call-web-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/tutorial-mobile-app-android-call-web-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 32fae5e6-b240-ae2d-2c4a-c530b0d4a86d
---

# Call a protected web API in an Android app using the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../external-id/media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This is the third tutorial in the tutorial series that guides you on calling a protected web API using Microsoft Entra External ID.

In this tutorial, you:

- Call a protected web API

## Prerequisites

# [Workforce tenant configuration](#tab/android-workforce)
- [Tutorial: Add add sign-in to an Android app by using Microsoft identity platform](tutorial-mobile-app-android-sign-in-sign-out)

# [External tenant configuration](#tab/android-external)
- [Tutorial: Add add sign-in to an Android app by using Microsoft identity platform](tutorial-mobile-app-android-sign-in-sign-out)
- An API registration that exposes at least one scope (delegated permissions) and one app role (application permission) such as *ToDoList.Read*. If you haven't already, follow the instructions for [call an API in a sample Android mobile app](quickstart-native-authentication-android-call-api) to have a functional protected ASP.NET Core web API. Make sure you complete the following steps:

    - Register a web API application
    - Configure API scopes
    - Configure app roles
    - Configure optional claims
    - Clone or download sample web API
    - Configure and run sample web API

---

## Call a protected web API

# [Workforce tenant configuration](#tab/android-workforce)
1. In **app** &gt; **src** &gt; **main**&gt; **java** &gt; **com.example(your app name)**. Create the following Android fragments:

    - *MSGraphRequestWrapper*
2. Open *MSGraphRequestWrapper.java* and replace the code with following code snippet to call the Microsoft Graph API using the token provided by MSAL:

    ```java
     package com.azuresamples.msalandroidapp;
    
     import android.content.Context;
     import android.util.Log;
    
     import androidx.annotation.NonNull;
    
     import com.android.volley.DefaultRetryPolicy;
     import com.android.volley.Request;
     import com.android.volley.RequestQueue;
     import com.android.volley.Response;
     import com.android.volley.toolbox.JsonObjectRequest;
     import com.android.volley.toolbox.Volley;
    
     import org.json.JSONObject;
    
     import java.util.HashMap;
     import java.util.Map;
    
     public class MSGraphRequestWrapper {
         private static final String TAG = MSGraphRequestWrapper.class.getSimpleName();
    
         // See: https://docs.microsoft.com/en-us/graph/deployments#microsoft-graph-and-graph-explorer-service-root-endpoints
         public static final String MS_GRAPH_ROOT_ENDPOINT = "https://graph.microsoft.com/";
    
         /**
          * Use Volley to make an HTTP request with
          * 1) a given MSGraph resource URL
          * 2) an access token
          * to obtain MSGraph data.
          **/
         public static void callGraphAPIUsingVolley(@NonNull final Context context,
                                                    @NonNull final String graphResourceUrl,
                                                    @NonNull final String accessToken,
                                                    @NonNull final Response.Listener<JSONObject> responseListener,
                                                    @NonNull final Response.ErrorListener errorListener) {
             Log.d(TAG, "Starting volley request to graph");
    
             /* Make sure we have a token to send to graph */
             if (accessToken == null || accessToken.length() == 0) {
                 return;
             }
    
             RequestQueue queue = Volley.newRequestQueue(context);
             JSONObject parameters = new JSONObject();
    
             try {
                 parameters.put("key", "value");
             } catch (Exception e) {
                 Log.d(TAG, "Failed to put parameters: " + e.toString());
             }
    
             JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, graphResourceUrl,
                     parameters, responseListener, errorListener) {
                 @Override
                 public Map<String, String> getHeaders() {
                     Map<String, String> headers = new HashMap<>();
                     headers.put("Authorization", "Bearer " + accessToken);
                     return headers;
                 }
             };
    
             Log.d(TAG, "Adding HTTP GET to Queue, Request: " + request.toString());
    
             request.setRetryPolicy(new DefaultRetryPolicy(
                     3000,
                     DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
                     DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
             queue.add(request);
         }
     }
    ```

# [External tenant configuration](#tab/android-external)
1. To call a web API from an Android application to access external data or services, begin by creating a companion object in your `MainActivity` class. The companion object should include the following code:

    ```kotlin
    companion object {
        private const val WEB_API_BASE_URL = "" // Developers should set the respective URL of their web API here
        private const val scopes = "" // Developers should append the respective scopes of their web API.
    }
    ```

    The companion object defines two private constants: `WEB_API_BASE_URL`, where developers set their web API's URL, and `scopes`, where developers append the respective `scopes` of their web API.
2. To handle the process of accessing a web API, use the following code:

    ```kotlin
    private fun accessWebApi() {
        CoroutineScope(Dispatchers.Main).launch {
            binding.txtLog.text = ""
            try {
                if (WEB_API_BASE_URL.isBlank()) {
                    Toast.makeText(this@MainActivity, getString(R.string.message_web_base_url), Toast.LENGTH_LONG).show()
                    return@launch
                }
                val apiResponse = withContext(Dispatchers.IO) {
                    ApiClient.performGetApiRequest(WEB_API_BASE_URL, accessToken)
                }
                binding.txtLog.text = getString(R.string.log_web_api_response)  + apiResponse.toString()
            } catch (exception: Exception) {
                Log.d(TAG, "Exception while accessing web API: $exception")
    
                binding.txtLog.text = getString(R.string.exception_web_api) + exception
            }
        }
    }
    ```

    The code launches a coroutine in the main dispatcher. It begins by clearing the text log. Then, it checks if the web API base URL is blank; if so, it displays a toast message and returns. Next, it performs a GET request to the web API using the provided access token in a background thread.

    After receiving the API response, it updates the text log with the response content. If any exception occurs during this process, it logs the exception and updates the text log with the corresponding error message.

    In the code, where we specify our callback, we use a function called `performGetApiRequest()`. The function should have the following code:

    ```kotlin
    object ApiClient {
        private val client = OkHttpClient()
    
        fun performGetApiRequest(WEB_API_BASE_URL: String, accessToken: String?): Response {
            val fullUrl = "$WEB_API_BASE_URL/api/todolist"
    
            val requestBuilder = Request.Builder()
                    .url(fullUrl)
                    .addHeader("Authorization", "Bearer $accessToken")
                    .get()
    
            val request = requestBuilder.build()
    
            client.newCall(request).execute().use { response -> return response }
        }
    }
    ```

    The code facilitates making `GET` requests to a web API. The main method is `performGetApiRequest()`, which takes the web API base URL and an access token as parameters. Inside this method, it constructs a full URL by appending `/api/todolist` to the base URL. Then, it builds an HTTP request with the appropriate headers, including the authorization header with the access token.

    Finally, it executes the request synchronously using OkHttp's `newCall()` method and returns the response. The `ApiClient` object maintains an instance of `OkHttpClient` to handle HTTP requests. To use `OkHttpClient`, you need to add the dependency `implementation 'com.squareup.okhttp3:okhttp:4.9.0'` to your Android Gradle file.

    Make sure you include the import statements. Android Studio should include the import statements for you automatically.

---

## Test your app

Build and deploy the app to a test device or emulator. You should be able to sign in and get tokens for Microsoft Entra ID.