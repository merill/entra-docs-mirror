---
layout: Conceptual
title: 'Quickstart: Call Microsoft Graph from a Java daemon - Microsoft identity platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/daemon-quickstart-portal-java
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: In this quickstart, you learn how a Java app can get an access token and call an API protected by Microsoft identity platform endpoint, using the app's own identity
ROBOTS: NOINDEX
manager: pmwongera
ms.custom: 
ms.date: 2025-04-16T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: f1a859d7-745d-48bd-3a28-2fa9f6846ddc
document_version_independent_id: 1e97f276-bef8-8e52-cb28-fe4fe7d61aba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/daemon-quickstart-portal-java.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/daemon-quickstart-portal-java
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/daemon-quickstart-portal-java.md
platformId: 469608d4-8a6b-ba43-03bb-50ced46a9937
---

# Quickstart: Call Microsoft Graph from a Java daemon - Microsoft identity platform | Microsoft Learn

Welcome! This probably isn't the page you were expecting. While we work on a fix, this link should take you to the right article:

> 
> [Quickstart: Acquire a token and call Microsoft Graph from a Java daemon app](quickstart-daemon-app-java-acquire-token)

We apologize for the inconvenience and appreciate your patience while we work to get this resolved.

# Quickstart: Acquire a token and call Microsoft Graph API from a Java console app using app's identity

In this quickstart, you download and run a code sample that demonstrates how a Java application can get an access token using the app's identity to call the Microsoft Graph API and display a [list of users](/en-us/graph/api/user-list) in the directory. The code sample demonstrates how an unattended job or Windows service can run with an application identity, instead of a user's identity.

## Prerequisites

To run this sample, you need:

- [Java Development Kit (JDK)](https://openjdk.java.net/) 8 or greater
- [Maven](https://maven.apache.org/)

### Download and configure the quickstart app

#### Step 1: Configure the application in Azure portal

For the code sample for this quickstart to work, you need to create a client secret, and add Graph API's **User.Read.All** application permission.

![Already configured](media/quickstart-v2-netcore-daemon/green-check.png) Your application is configured with these attributes.

#### Step 2: Download the Java project

Note

`Enter_the_Supported_Account_Info_Here`

##### Standard user

If you're a standard user of your tenant, then you need to ask a Global Administrator to grant admin consent for your application. To do this, give the following URL to your administrator:

```url
https://login.microsoftonline.com/Enter_the_Tenant_Id_Here/adminconsent?client_id=Enter_the_Application_Id_Here
```

#### Step 4: Run the application

You can test the sample directly by running the main method of ClientCredentialGrant.java from your IDE.

From your shell or command line:

```
$ mvn clean compile assembly:single
```

This will generate a msal-client-credential-secret-1.0.0.jar file in your /targets directory. Run this using your Java executable like below:

```
$ java -jar msal-client-credential-secret-1.0.0.jar
```

After running, the application should display the list of users in the configured tenant.

Important

This quickstart application uses a client secret to identify itself as confidential client. Because the client secret is added as a plain-text to your project files, for security reasons, it is recommended that you use a certificate instead of a client secret before considering the application as production application. For more information on how to use a certificate, see [these instructions](https://github.com/Azure-Samples/ms-identity-java-daemon/tree/master/msal-client-credential-certificate) in the same GitHub repository for this sample, but in the second folder **msal-client-credential-certificate**.

## More information

### MSAL Java

[MSAL Java](https://github.com/AzureAD/microsoft-authentication-library-for-java) is the library used to sign in users and request tokens used to access an API protected by Microsoft identity platform. As described, this quickstart requests tokens by using the application own identity instead of delegated permissions. The authentication flow used in this case is known as *[client credentials oauth flow](v2-oauth2-client-creds-grant-flow)*. For more information on how to use MSAL Java with daemon apps, see [this article](scenario-daemon-app-configuration).

Add MSAL4J to your application by using Maven or Gradle to manage your dependencies by making the following changes to the application's pom.xml (Maven) or build.gradle (Gradle) file.

In pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>msal4j</artifactId>
    <version>1.0.0</version>
</dependency>
```

In build.gradle:

```
compile group: 'com.microsoft.azure', name: 'msal4j', version: '1.0.0'
```

### MSAL initialization

Add a reference to MSAL for Java by adding the following code to the top of the file where you will be using MSAL4J:

```Java
import com.microsoft.aad.msal4j.*;
```

Then, initialize MSAL using the following code:

```Java
IClientCredential credential = ClientCredentialFactory.createFromSecret(CLIENT_SECRET);

ConfidentialClientApplication cca =
        ConfidentialClientApplication
                .builder(CLIENT_ID, credential)
                .authority(AUTHORITY)
                .build();
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `CLIENT_SECRET` | Is the client secret created for the application in Azure portal. |
> | `CLIENT_ID` | Is the **Application (client) ID** for the application registered in the Azure portal. You can find this value in the app's **Overview** page in the Azure portal. |
> | `AUTHORITY` | The STS endpoint for user to authenticate. Usually `https://login.microsoftonline.com/{tenant}` for public cloud, where {tenant} is the name of your tenant or your tenant Id. |
> 

### Requesting tokens

To request a token using app's identity, use `acquireToken` method:

```Java
IAuthenticationResult result;
     try {
         SilentParameters silentParameters =
                 SilentParameters
                         .builder(SCOPE)
                         .build();

         // try to acquire token silently. This call will fail since the token cache does not
         // have a token for the application you are requesting an access token for
         result = cca.acquireTokenSilently(silentParameters).join();
     } catch (Exception ex) {
         if (ex.getCause() instanceof MsalException) {

             ClientCredentialParameters parameters =
                     ClientCredentialParameters
                             .builder(SCOPE)
                             .build();

             // Try to acquire a token. If successful, you should see
             // the token information printed out to console
             result = cca.acquireToken(parameters).join();
         } else {
             // Handle other exceptions accordingly
             throw ex;
         }
     }
     return result;
```

> 
> 
> | Where: | Description |
> | --- | --- |
> | `SCOPE` | Contains the scopes requested. For confidential clients, this should use the format similar to `{Application ID URI}/.default` to indicate that the scopes being requested are the ones statically defined in the app object set in the Azure portal (for Microsoft Graph, `{Application ID URI}` points to `https://graph.microsoft.com`). For custom web APIs, `{Application ID URI}` is defined under the **Expose an API** section in **App registrations** in the Azure portal. |
> 

## Help and support

If you need help, want to report an issue, or want to learn about your support options, see [Help and support for developers](developer-support-help-options).