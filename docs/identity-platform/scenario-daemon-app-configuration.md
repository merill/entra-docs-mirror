---
layout: Conceptual
title: How to configure daemon apps that call web APIs - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-daemon-app-configuration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to configure daemon apps that call web APIs using secrets, certificates, or client assertions.
ms.date: 2026-06-15T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.subservice: workforce
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 08bcd9e7-d45f-1867-185a-c74636a9f448
document_version_independent_id: 20e2b7a4-12b0-8cbf-d36f-63a9b527b7da
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-daemon-app-configuration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-daemon-app-configuration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-daemon-app-configuration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/7696cda6-0510-47f6-8302-71bb5d2e28cf
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/69c76c32-967e-4c65-b89a-74cc527db725
platformId: a4c80102-53e0-d35b-fd49-1056434d3883
---

# How to configure daemon apps that call web APIs - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Learn how to configure the code for your daemon application that calls web APIs.

## Microsoft libraries supporting daemon apps

The following Microsoft libraries support daemon apps:

| Language / framework | Project onGitHub | Package | Gettingstarted | Sign in users | Access web APIs | Generally available (GA)*or*Public preview^1^ |
| --- | --- | --- | --- | --- | --- | --- |
| .NET | [MSAL.NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) | [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client/) | [Quickstart](quickstart-daemon-dotnet-acquire-token) | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Java | [MSAL4J](https://github.com/AzureAD/microsoft-authentication-library-for-java) | [msal4j](https://javadoc.io/doc/com.microsoft.azure/msal4j/latest/index.html) | — | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Node | [MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-node) | [msal-node](https://www.npmjs.com/package/@azure/msal-node) | [Quickstart](quickstart-console-app-nodejs-acquire-token) | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |
| Python | [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) | [msal-python](https://github.com/AzureAD/microsoft-authentication-library-for-python) | [Quickstart](quickstart-daemon-app-python-acquire-token) | ![Library cannot request ID tokens for user sign-in.](media/common/no.png) | ![Library can request access tokens for protected web APIs.](media/common/yes.png) | GA |

^1^[Universal License Terms for Online Services](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all) apply to libraries in *Public preview*.

## Configure the authority

Daemon applications use application permissions rather than delegated permissions. So their supported account type can't be an account in any organizational directory or any personal Microsoft account (for example, Skype, Xbox, Outlook.com). There's no tenant admin to grant consent to a daemon application for a Microsoft personal account. You need to choose *accounts in my organization* or *accounts in any organization*.

The authority specified in the application configuration should include your tenant ID or a domain name associated with your organization.

Even if you want to provide a multitenant tool, you should use a tenant ID or domain name, and **not**`common` or `organizations` with this flow, because the service can't reliably infer which tenant should be used.

## Configure and instantiate the application

In Microsoft Authentication Libraries (MSAL), the client credentials (secret or certificate) are passed as a parameter of the confidential client application construction.

Important

Even if your application is a console application that runs as a service, if it's a daemon application, it needs to be a confidential client application.

### Configuration file

The configuration file defines:

- The cloud instance and tenant ID, which together make up the *authority*.
- The client ID that you got from the application registration.
- Either a client secret or a certificate.

# [.NET](#tab/idweb)
Here's an example of defining the configuration in an [*appsettings.json* sample configuration file](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/blob/master/1-Call-MSGraph/daemon-console/appsettings.json). This example is taken from the [.NET console daemon](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2) code sample on GitHub.

```json
{
    "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "TenantId": "[Enter here the tenantID or domain name for your Azure AD tenant]",
        "ClientId": "[Enter here the ClientId for your application]",
        "ClientCredentials": [
            {
                "SourceType": "ClientSecret",
                "ClientSecret": "[Enter here a client secret for your application]"
            }
        ]
    }
}

```

You provide a certificate instead of the client secret, or [workload identity federation](../workload-id/workload-identity-federation) credentials.

# [Java](#tab/java)
The following example shows the Java configuration constants for a daemon app:

```Java
 private final static String CLIENT_ID = "";
 private final static String AUTHORITY = "https://login.microsoftonline.com/<tenant>/";
 private final static String CLIENT_SECRET = "";
 private final static Set<String> SCOPE = Collections.singleton("https://graph.microsoft.com/.default");
```

# [Node.js](#tab/nodejs)
Configuration parameters for the [Node.js daemon sample](https://github.com/Azure-Samples/ms-identity-javascript-nodejs-console/) are located in an *.env* file:

```JavaScript
# Credentials
TENANT_ID=Enter_the_Tenant_Info_Here
CLIENT_ID=Enter_the_Application_Id_Here

// You provide either a ClientSecret or a CertificateConfiguration, or a ClientAssertion. These settings are exclusive
CLIENT_SECRET=Enter_the_Client_Secret_Here
CERTIFICATE_THUMBPRINT=Enter_the_certificate_thumbprint_Here
CERTIFICATE_PRIVATE_KEY=Enter_the_certificate_private_key_Here
CLIENT_ASSERTION=Enter_the_Assertion_String_Here

# Endpoints
// the Azure AD endpoint is the authority endpoint for token issuance
AAD_ENDPOINT=Enter_the_Cloud_Instance_Id_Here // https://login.microsoftonline.com/
// the graph endpoint is the application ID URI of Microsoft Graph
GRAPH_ENDPOINT=Enter_the_Graph_Endpoint_Here // https://graph.microsoft.com/
```

# [Python](#tab/python)
When you build a confidential client with client secrets, the [parameters.json sample for the client secret flow](https://github.com/Azure-Samples/ms-identity-python-daemon/blob/master/1-Call-MsGraph-WithSecret/parameters.json) config file in the [Python daemon](https://github.com/Azure-Samples/ms-identity-python-daemon) sample is as follows:

```Json
{
  "authority": "https://login.microsoftonline.com/<your_tenant_id>",
  "client_id": "your_client_id",
  "scope": [ "https://graph.microsoft.com/.default" ],
  "secret": "The secret generated by Azure AD during your confidential app registration",
  "endpoint": "https://graph.microsoft.com/v1.0/users"
}
```

When you build a confidential client with certificates, the [parameters.json sample for the certificate flow](https://github.com/Azure-Samples/ms-identity-python-daemon/blob/master/2-Call-MsGraph-WithCertificate/parameters.json) config file in the [Python daemon](https://github.com/Azure-Samples/ms-identity-python-daemon) sample is as follows:

```Json
{
  "authority": "https://login.microsoftonline.com/<your_tenant_id>",
  "client_id": "your_client_id",
  "scope": [ "https://graph.microsoft.com/.default" ],
  "thumbprint": "790E... The thumbprint generated by Azure AD when you upload your public cert",
  "private_key_file": "server.pem",
  "endpoint": "https://graph.microsoft.com/v1.0/users"
}
```

# [.NET (low level)](#tab/dotnet)
Here's an example of defining the configuration in an [*appsettings.json* daemon console configuration file](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/blob/master/1-Call-MSGraph/daemon-console/appsettings.json). This example is taken from the [.NET console daemon](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2) code sample on GitHub.

```json
{
  "Instance": "https://login.microsoftonline.com/{0}",
  "Tenant": "[Enter here the tenantID or domain name for your Azure AD tenant]",
  "ClientId": "[Enter here the ClientId for your application]",
  "ClientSecret": "[Enter here a client secret for your application]",
  "CertificateName": "[Or instead of client secret: Enter here the name of a certificate (from the user cert store) as registered with your application]"
}
```

You provide either a `ClientSecret` or a `CertificateName`. These settings are exclusive.

---

### Instantiate the MSAL application

To instantiate the MSAL application, add, reference, or import the MSAL package (depending on the language).

The construction is different, depending on whether you're using client secrets or certificates (or, as an advanced scenario, signed assertions).

#### Reference the package

Reference the MSAL package in your application code.

# [.NET](#tab/idweb)
Add the [Microsoft.Identity.Web.TokenAcquisition](https://www.nuget.org/packages/Microsoft.Identity.Web.TokenAcquisition) NuGet package to your application. Alternatively, if you want to call Microsoft Graph, add the [Microsoft.Identity.Web.GraphServiceClient](https://www.nuget.org/packages/Microsoft.Identity.Web.GraphServiceClient) package. Your project could be as follows. The *appsettings.json* file needs to be copied to the output directory.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
    <RootNamespace>daemon_console</RootNamespace>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.Identity.Web.GraphServiceClient" Version="2.12.2" />
  </ItemGroup>

  <ItemGroup>
    <None Update="appsettings.json">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
  </ItemGroup>
</Project>
```

In the Program.cs file, add a `using` directive in your code to reference Microsoft.Identity.Web.

```csharp
using Microsoft.Identity.Abstractions;
using Microsoft.Identity.Web;
```

# [Java](#tab/java)
```java
import com.microsoft.aad.msal4j.ClientCredentialFactory;
import com.microsoft.aad.msal4j.ClientCredentialParameters;
import com.microsoft.aad.msal4j.ConfidentialClientApplication;
import com.microsoft.aad.msal4j.IAuthenticationResult;
import com.microsoft.aad.msal4j.IClientCredential;
import com.microsoft.aad.msal4j.MsalException;
import com.microsoft.aad.msal4j.SilentParameters;
```

# [Node.js](#tab/nodejs)
Install the packages by running `npm install` in the folder where `package.json` file resides. Then, import the `msal-node` package:

```JavaScript
const msal = require('@azure/msal-node');
```

# [Python](#tab/python)
Import the required MSAL and helper modules in your Python application:

```python
import msal
import json
import sys
import logging
```

# [.NET (low level)](#tab/dotnet)
Add the [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client) NuGet package to your application, and then add a `using` directive in your code to reference it.

In MSAL.NET, the confidential client application is represented by the `IConfidentialClientApplication` interface.

```csharp
using Microsoft.Identity.Client;
IConfidentialClientApplication app;
```

---

#### Instantiate the confidential client application with a client secret

Here's the code to instantiate the confidential client application with a client secret:

# [.NET](#tab/idweb)
The following example creates the confidential client application by using a client secret with Microsoft.Identity.Web:

```csharp
   class Program
    {
        static async Task Main(string[] _)
        {
            // Get the Token acquirer factory instance. By default it reads an appsettings.json
            // file if it exists in the same folder as the app (make sure that the 
            // "Copy to Output Directory" property of the appsettings.json file is "Copy if newer").
            TokenAcquirerFactory tokenAcquirerFactory = TokenAcquirerFactory.GetDefaultInstance();

            // Configure the application options to be read from the configuration
            // and add the services you need (Graph, token cache)
            IServiceCollection services = tokenAcquirerFactory.Services;
            services.AddMicrosoftGraph();
            // By default, you get an in-memory token cache.
            // For more token cache serialization options, see https://aka.ms/msal-net-token-cache-serialization

            // Resolve the dependency injection.
            var serviceProvider = tokenAcquirerFactory.Build();

            // ...
        }
    }
```

The configuration is read from the *appsettings.json*:

# [Java](#tab/java)
Use the following Java code to create a confidential client application with a client secret:

```Java
IClientCredential credential = ClientCredentialFactory.createFromSecret(CLIENT_SECRET);

ConfidentialClientApplication cca =
        ConfidentialClientApplication
                .builder(CLIENT_ID, credential)
                .authority(AUTHORITY)
                .build();
```

# [Node.js](#tab/nodejs)
Use the following Node.js configuration to instantiate a confidential client application with a client secret:

```JavaScript

const msalConfig = {
  auth: {
    clientId: process.env.CLIENT_ID,
    authority: process.env.AAD_ENDPOINT + process.env.TENANT_ID,
    clientSecret: process.env.CLIENT_SECRET,
  }
};

const apiConfig = {
  uri: process.env.GRAPH_ENDPOINT + 'v1.0/users',
};

const tokenRequest = {
  scopes: [process.env.GRAPH_ENDPOINT + '.default'],
};

const cca = new msal.ConfidentialClientApplication(msalConfig);
```

# [Python](#tab/python)
```Python
# Pass the parameters.json file as an argument to this Python script. E.g.: python your_py_file.py parameters.json
config = json.load(open(sys.argv[1]))

# Create a preferably long-lived app instance that maintains a token cache.
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential=config["secret"],
    # token_cache=...  # Default cache is in memory only.
                       # You can learn how to use SerializableTokenCache from
                       # https://msal-python.rtfd.io/en/latest/#msal.SerializableTokenCache
    )
```

# [.NET (low level)](#tab/dotnet)
The following MSAL.NET example creates a confidential client application by using the configured client secret:

```csharp
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
           .WithClientSecret(config.ClientSecret)
           .WithAuthority(new Uri(config.Authority))
           .Build();
```

The `Authority` is a concatenation of the cloud instance and the tenant ID, for example `https://login.microsoftonline.com/contoso.onmicrosoft.com` or `https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee`. In the *appsettings.json* file shown in the Configuration file section, instance and tenant are represented by the `Instance` and `Tenant` values, respectively.

In the code sample the previous snippet was taken from, `Authority` is a property on the [AuthenticationConfig](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/blob/ffc4a9f5d9bdba5303e98a1af34232b434075ac7/1-Call-MSGraph/daemon-console/AuthenticationConfig.cs#L61-L70) class, and is defined as such:

```csharp
/// <summary>
/// URL of the authority
/// </summary>
public string Authority
{
    get
    {
        return String.Format(CultureInfo.InvariantCulture, Instance, Tenant);
    }
}
```

---

#### Instantiate the confidential client application with a client certificate

Here's the code to build an application with a certificate:

# [.NET](#tab/idweb)
The application-construction code is the same as the client-secret example. The only difference is that the certificate is described in the configuration instead of a secret. There are many ways to get the certificate. For details, see [Use certificates with Microsoft Identity Web](https://aka.ms/ms-id-web-certificates). The following configuration example shows how to retrieve your certificate from Azure Key Vault. Microsoft identity delegates to Azure Identity's DefaultAzureCredential, and used Managed identity when available to access the certificate from KeyVault. You can debug your application locally because DefaultAzureCredential then uses your developer credentials.

```json
  "ClientCredentials": [
      {
        "SourceType": "KeyVault",
        "KeyVaultUrl": "https://yourKeyVaultUrl.vault.azure.net",
        "KeyVaultCertificateName": "NameOfYourCertificate"
      }
```

# [Java](#tab/java)
In MSAL Java, there are two builders to instantiate the confidential client application with certificates:

```Java

InputStream pkcs12Certificate = ... ; /* Containing PCKS12-formatted certificate*/
string certificatePassword = ... ;    /* Contains the password to access the certificate */

IClientCredential credential = ClientCredentialFactory.createFromCertificate(pkcs12Certificate, certificatePassword);

ConfidentialClientApplication cca =
        ConfidentialClientApplication
                .builder(CLIENT_ID, credential)
                .authority(AUTHORITY)
                .build();
```

or

```Java
PrivateKey key = getPrivateKey(); /* RSA private key to sign the assertion */
X509Certificate publicCertificate = getPublicCertificate(); /* x509 public certificate used as a thumbprint */

IClientCredential credential = ClientCredentialFactory.createFromCertificate(key, publicCertificate);

ConfidentialClientApplication cca =
        ConfidentialClientApplication
                .builder(CLIENT_ID, credential)
                .authority(AUTHORITY)
                .build();
```

# [Node.js](#tab/nodejs)
The following Node.js example configures a confidential client application to use a certificate:

```JavaScript

const config = {
    auth: {
        clientId: process.env.CLIENT_ID,
        authority: process.env.AAD_ENDPOINT + process.env.TENANT_ID,
        clientCertificate: {
            thumbprint:  process.env.CERTIFICATE_THUMBPRINT, // a 40-digit hexadecimal string
            privateKey:  process.env.CERTIFICATE_PRIVATE_KEY,
        }
    }
};

// Create an MSAL application object
const cca = new msal.ConfidentialClientApplication(config);
```

For details, see [Use certificate credentials with MSAL Node](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/certificate-credentials.md).

# [Python](#tab/python)
```Python
# Pass the parameters.json file as an argument to this Python script. E.g.: python your_py_file.py parameters.json
config = json.load(open(sys.argv[1]))

# Create a preferably long-lived app instance that maintains a token cache.
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential={"thumbprint": config["thumbprint"], "private_key": open(config['private_key_file']).read()},
    # token_cache=...  # Default cache is in memory only.
                       # You can learn how to use SerializableTokenCache from
                       # https://msal-python.rtfd.io/en/latest/#msal.SerializableTokenCache
    )
```

# [.NET](#tab/dotnet)
Use the following MSAL.NET code to load a certificate and build the confidential client application:

```csharp
X509Certificate2 certificate = ReadCertificate(config.CertificateName);
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
    .WithCertificate(certificate)
    .WithAuthority(new Uri(config.Authority))
    .Build();
```

---

#### Advanced scenario: Instantiate the confidential client application with client assertions

# [.NET](#tab/idweb)
In addition to using a client secret or certificate, confidential client applications can also prove their identity by using client assertions. See [CredentialDescription](/en-us/dotnet/api/microsoft.identity.abstractions.credentialdescription?view=msal-model-dotnet-latest&amp;preserve-view=true) for details.

# [Java](#tab/java)
The following Java example creates a confidential client application by using a client assertion:

```Java
IClientCredential credential = ClientCredentialFactory.createFromClientAssertion(assertion);

ConfidentialClientApplication cca =
        ConfidentialClientApplication
                .builder(CLIENT_ID, credential)
                .authority(AUTHORITY)
                .build();
```

# [Node.js](#tab/nodejs)
Use the following Node.js configuration to initialize a confidential client application with a client assertion:

```JavaScript
const clientConfig = {
    auth: {
        clientId: process.env.CLIENT_ID,
        authority: process.env.AAD_ENDPOINT + process.env.TENANT_ID,
        clientAssertion:  process.env.CLIENT_ASSERTION
    }
};
const cca = new msal.ConfidentialClientApplication(clientConfig);
```

For details, see [Initialize the ConfidentialClientApplication object](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-node/docs/initialize-confidential-client-application.md).

# [Python](#tab/python)
In MSAL Python, you can provide client claims by using the claims that will be signed by this `ConfidentialClientApplication`'s private key.

```Python
# Pass the parameters.json file as an argument to this Python script. E.g.: python your_py_file.py parameters.json
config = json.load(open(sys.argv[1]))

# Create a preferably long-lived app instance that maintains a token cache.
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential={"thumbprint": config["thumbprint"], "private_key": open(config['private_key_file']).read()},
    client_claims = {"client_ip": "x.x.x.x"}
    # token_cache=...  # Default cache is in memory only.
                       # You can learn how to use SerializableTokenCache from
                       # https://msal-python.rtfd.io/en/latest/#msal.SerializableTokenCache
    )
```

For details, see the MSAL Python reference documentation for [ConfidentialClientApplication](https://msal-python.readthedocs.io/en/latest/#msal.ClientApplication.__init__).

# [.NET (low level)](#tab/dotnet)
Instead of a client secret or a certificate, the confidential client application can also prove its identity by using client assertions.

MSAL.NET has two methods to provide signed assertions to the confidential client app:

- `.WithClientAssertion()`
- `.WithClientClaims()`

When you use `WithClientAssertion`, provide a signed JWT. This advanced scenario is detailed in [Client assertions](/en-us/entra/msal/dotnet/acquiring-tokens/msal-net-client-assertions).

```csharp
string signedClientAssertion = ComputeAssertion();
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
                                          .WithClientAssertion(signedClientAssertion)
                                          .Build();
```

When you use `WithClientClaims`, MSAL.NET produces a signed assertion that contains the claims expected by Microsoft Entra ID, plus additional client claims that you want to send. This code shows how to do that:

```csharp
string ipAddress = "192.168.1.2";
var claims = new Dictionary<string, string> { { "client_ip", ipAddress } };
X509Certificate2 certificate = ReadCertificate(config.CertificateName);
app = ConfidentialClientApplicationBuilder.Create(config.ClientId)
                                          .WithAuthority(new Uri(config.Authority))
                                          .WithClientClaims(certificate, claims)
                                          .Build();
```

For details, see [Client assertions](/en-us/entra/msal/dotnet/acquiring-tokens/msal-net-client-assertions).

---