---
layout: Conceptual
title: Signing Key Rollover in Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/signing-key-rollover
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: This article discusses the best practices for signing key rollover in Microsoft Entra ID.
manager: pmwongera
ms.custom: 
ms.date: 2024-10-28T00:00:00.0000000Z
ms.reviewer: paulgarn, ludwignick
ms.topic: concept-article
locale: en-us
document_id: 609a07b8-4c70-edb5-d384-dbdaaef25f25
document_version_independent_id: a50751eb-5103-8f79-2d1b-f2a3783c20c4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/signing-key-rollover.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/signing-key-rollover
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/signing-key-rollover.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/4628cbd9-6f47-4ae1-b371-d34636609eaf
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/43ab1a66-ffe1-45dd-a4cb-6580218ef802
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/be21deb8-8c64-44b0-b71f-2dc56ca7364f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/bbc4fbf6-70c4-4d12-b47f-9360080c4977
platformId: b27dc088-4168-c3ef-c9a9-0e42855bbe4b
---

# Signing Key Rollover in Microsoft identity platform - Microsoft identity platform | Microsoft Learn

This article discusses what you need to know about the public keys that are used by the Microsoft identity platform to sign security tokens. It's important to note that these keys roll over on a periodic basis and, in an emergency, could be rolled over immediately. All applications that use the Microsoft identity platform should be able to programmatically handle the key rollover process. You'll understand how the keys work, how to assess the impact of the rollover to your application. You'll also learn how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.

## Overview of signing keys in the Microsoft identity platform

The Microsoft identity platform uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it. In practical terms, this works in the following way: The Microsoft identity platform uses a signing key that consists of a public and private key pair. When a user signs in to an application that uses the Microsoft identity platform for authentication, the Microsoft identity platform creates a security token that contains information about the user. This token is signed by the Microsoft identity platform using its private key before being sent back to the application. To verify that the token is valid and originated from Microsoft identity platform, the application must validate the token’s signature using the public keys exposed by the Microsoft identity platform that is contained in the tenant’s [OpenID Connect discovery document](https://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](federation-metadata).

For security purposes, the Microsoft identity platform’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately. There's no set or guaranteed time between these key rolls. Any application that integrates with the Microsoft identity platform should be prepared to handle a key rollover event no matter how frequently it may occur. If your application doesn't handle sudden refreshes, and attempts to use an expired key to verify the signature on a token, your application incorrectly rejects the token. It's recommended to use [standard libraries](reference-v2-libraries) to ensure key metadata is correctly refreshed, and kept up to date. In cases where standard libraries aren't used, make sure the implementation follows the best practices section.

There's always more than one valid key available in the OpenID Connect discovery document and the federation metadata document. Your application should be prepared to use any and all of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth. The number of keys present can change over time based on the internal architecture of the Microsoft identity platform as we support new platforms, new clouds, or new authentication protocols. Neither the order of the keys in the JSON response nor the order in which they were exposed should be considered meaningful to your application. To learn more about JSON Web Key data structure, you may reference [RFC7517](https://www.rfc-editor.org/rfc/rfc7517).

Applications that support only a single signing key, or applications that require manual updates to the signing keys, are inherently less secure and less reliable. They should be updated to use [standard libraries](reference-v2-libraries) to ensure that they're always using up-to-date signing keys, among other best practices.

## Best practices for keys metadata caching and validation

- Discover keys using the tenant-specific endpoint as described in [OpenID Connect (OIDC)](v2-protocols-oidc) and [Federation metadata](federation-metadata)
- Even if your application is deployed across multiple tenants, it’s recommended to always discover and cache keys independently for each tenant the application serves (using the tenant-specific endpoint). A key that is common across tenants today can become distinct across tenants in the future.
- Use the caching algorithm below to ensure the caching is resilient and secure

### Keys metadata caching algorithm:

Our [standard libraries](reference-v2-libraries) implement resilient and secure caching of keys. It’s recommended to use them to avoid subtle defects in the implementation. For custom implementations, here's the rough algorithm:

#### General considerations:

- The service validating tokens should have a cache capable of storing many distinct keys (10-1000).
- The keys should be cached individually, using the key ID (“kid” in the OIDC keys metadata specification) as a cache key.
- The time-to-live of keys in the cache should be configured to 24 hours, with refreshes happening every hour. This makes sure the system can respond quickly to keys being removed, but has enough cache duration to not be affected by problems in fetching keys.
- The keys should be refreshed:
    - Once on process startup or when cache is empty
    - Periodically (recommended every 1 hour) as a background job
    - Dynamically if a received token was signed with an unknown key (unknown **kid** or **tid** in the header)

#### KeyRefresh procedure (Conceptual algorithm from IdentityModel)

1. **Initialization**

    The configuration manager is set up with a specific address to fetch configuration data and necessary interfaces to retrieve and validate this data.
2. **Configuration Check**

    Before fetching new data, the system first checks if the existing data is still valid based on a predefined refresh interval.
3. **Data Retrieval** If the data is outdated or missing, the system locks down to ensure only one thread fetches the new data to avoid duplication (and thread exhaustion). The system then attempts to retrieve the latest configuration data from a specified endpoint.
4. **Validation**

    Once the new data is retrieved, it's validated to ensure it meets the required standards and isn't corrupted. The metadata is only accepted when an incoming request was successfully validated with the new keys.
5. **Error Handling**

    If any errors occur during data retrieval, they're logged. The system continues to operate with the last known good configuration if new data can't be fetched
6. **Automatic Updates** The system periodically checks and updates the configuration data automatically based on the refresh interval (recommend 12 h with a jitter of plus or minus 1 h). It can also manually request an update if needed, ensuring that the data is always current.
7. **Validation of a token with a new key** If a token arrives with a signing key that isn't known yet from the configuration, the system attempts to fetch the configuration with a sync call on the hot path to handle new keys in metadata outside of the regular expected updates(but no more frequently than 5 mins)

This approach ensures that the system always uses the most up-to-date and valid configuration data, while gracefully handling errors and avoiding redundant operations.

The .NET implementation of this algorithm is available from [BaseConfigurationManager](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet/blob/dev/src/Microsoft.IdentityModel.Tokens/BaseConfigurationManager.cs). It's subject to change based on resilience and security evaluations. See also an explanation [here](https://github.com/AzureAD/azure-activedirectory-identitymodel-extensions-for-dotnet/wiki/signing-key-rollover)

#### KeyRefresh procedure (pseudo code):

This procedure uses a global (lastSuccessfulRefreshTime timestamp) to prevent conditions that refresh keys too often.

- [OpenID Connect (OIDC)](v2-protocols-oidc)

```csharp
KeyRefresh(issuer)
{
  // Store cache entries and last successful refresh timestamp per distinct 'issuer'
 
  if (LastSuccessfulRefreshTime is set and more recent than 5 minutes ago) 
    return // without refreshing
 
  // Load keys URI using the tenant-specific OIDC configuration endpoint ('issuer' is the input parameter)
  oidcConfiguration = download JSON from "{issuer}/.well-known/openid-configuration"
 
  // Load list of keys from keys URI
  keyList = download JSON from jwks_uri property of oidcConfiguration
 
  foreach (key in keyList) 
  {
    cache entry = lookup in cache by kid property of key
    if (cache entry found) 
      set expiration of cache entry to now + 24h 
    else 
      add key to cache with expiration set to now + 24h
  }
 
  set LastSuccessfulRefreshTime to now // current timestamp
}

```

#### Service Startup procedure:

- KeyRefresh to update the keys
- Launch a background job which calls KeyRefresh every hour

### TokenValidation procedure for validating the key (pseudo code):

```csharp
ValidateToken(token)
{
  kid = token.header.kid // get key id from token header
  issuer = token.body.iss // get issuer from 'iss' claim in token body
 
  key = lookup in cache by issuer and kid
  if (key found)
  {
     validate token with key and return
  }
  else // key is not found in the cache
  {
    call KeyRefresh(issuer) // to opportunistically refresh the keys for the issuer
    key = lookup in cache by issuer and kid
    if (key found)
    {
      validate token with key and return
    }
    else // key is not found in the cache even after refresh
    {
      return token validation error
    }
  }
}
```

## How to assess if your application will be affected and what to do about it

How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used. The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.

- Native client applications accessing resources
- Web applications / APIs accessing resources
- Web applications / APIs protecting resources and built using Azure App Services
- Web applications / APIs protecting resources using ASP.NET OWIN OpenID Connect, WS-Fed, or WindowsAzureActiveDirectoryBearerAuthentication middleware
- Web applications / APIs protecting resources using ASP.NET Core OpenID Connect or JwtBearerAuthentication middleware
- Web applications / APIs protecting resources using Node.js `passport-azure-ad` module
- Web applications / APIs protecting resources and created with Visual Studio 2015 or later
- Web applications protecting resources and created with Visual Studio 2013
- Web APIs protecting resources and created with Visual Studio 2013
- Web applications protecting resources and created with Visual Studio 2012
- Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols

This guidance is **not** applicable for:

- Applications added from Microsoft Entra Application Gallery (including Custom) have separate guidance regarding signing keys. [More information.](../identity/enterprise-apps/tutorial-manage-certificates-for-federated-single-sign-on)
- On-premises applications published via application proxy don't have to worry about signing keys.

### Native client applications accessing resources

Applications that are only accessing resources (for example, Microsoft Graph, KeyVault, Outlook API, and other Microsoft APIs) only obtain a token and pass it along to the resource owner. Given that they aren't protecting any resources, they don't inspect the token and therefore don't need to ensure it's properly signed.

Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.

### Web applications / APIs accessing resources

Applications that are only accessing resources (such as Microsoft Graph, KeyVault, Outlook API, and other Microsoft APIs) only obtain a token and pass it along to the resource owner. Given that they aren't protecting any resources, they don't inspect the token and therefore don't need to ensure it's properly signed.

Web applications and web APIs that are using the app-only flow (client credentials / client certificate) to request tokens fall into this category and are thus not impacted by the rollover.

### Web applications / APIs protecting resources and built using Azure App Services

Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.

### Web applications / APIs protecting resources using ASP.NET OWIN OpenID Connect, WS-Fed, or WindowsAzureActiveDirectoryBearerAuthentication middleware

If your application is using the ASP.NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.

You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs files.

```csharp
app.UseOpenIdConnectAuthentication(
    new OpenIdConnectAuthenticationOptions
    {
        // ...
    });
```

```csharp
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
        // ...
    });
```

```csharp
app.UseWindowsAzureActiveDirectoryBearerAuthentication(
    new WindowsAzureActiveDirectoryBearerAuthenticationOptions
    {
        // ...
    });
```

### Web applications / APIs protecting resources using .NET Core OpenID Connect or JwtBearerAuthentication middleware

If your application is using the ASP.NET OWIN OpenID Connect or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.

You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```

```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### Web applications / APIs protecting resources using Node.js `passport-azure-ad` module

If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.

You can confirm that your application passport-ad by searching for the following snippet in your application's app.js

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### Web applications / APIs protecting resources and created with Visual Studio 2015 or later

If your application was built using a web application template in Visual Studio 2015 or later and you selected **Work Or School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically. This logic, embedded in the OWIN OpenID Connect middleware, retrieves, and caches the keys from the OpenID Connect discovery document and periodically refreshes them.

If you added authentication to your solution manually, your application might not have the necessary key rollover logic. You can write it yourself, or follow the steps in Web applications / APIs using any other libraries or manually implementing any of the supported protocols.

### Web applications protecting resources and created with Visual Studio 2013

If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically. This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project. You can find the connection string for the database in the project’s Web.config file.

If you added authentication to your solution manually, your application might not have the necessary key rollover logic. You need to write it yourself, or follow the steps in Web applications / APIs using any other libraries or manually implementing any of the supported protocols..

The following steps help you verify that the logic is working properly in your application.

1. In Visual Studio 2013, open the solution, and then select on the **Server Explorer** tab on the right window.
2. Expand **Data Connections**, **DefaultConnection**, and then **Tables**. Locate the **IssuingAuthorityKeys** table, right-click it, and then select **Show Table Data**.
3. In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key. Delete any rows in the table.
4. Right-click the **Tenants** table, and then select **Show Table Data**.
5. In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier. Delete any rows in the table. If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you get an error at runtime.
6. Build and run the application. After you have logged in to your account, you can stop the application.
7. Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table. You'll notice that they were automatically repopulated with the appropriate information from the federation metadata document.

### Web APIs protecting resources and created with Visual Studio 2013

If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.

If you manually configured authentication, follow the instructions below to learn how to configure your web API to automatically update its key information.

The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then uses the [JWT Token Handler](/en-us/previous-versions/dotnet/framework/windows-identity-foundation/json-web-token-handler) to validate the token. The code snippet assumes that you'll use your own caching mechanism for persisting the key to validate future tokens from Microsoft identity platform, whether it be in a database, configuration file, or elsewhere.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/aaaabbbb-0000-cccc-1111-dddd2222eeee/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### Web applications protecting resources and created with Visual Studio 2012

If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application. It’s also likely that you're using the [Validating Issuer Name Registry (VINR)](/en-us/previous-versions/dotnet/framework/windows-identity-foundation/validating-issuer-name-registry). The VINR is responsible for maintaining information about trusted identity providers (Microsoft identity platform) and the keys used to validate tokens issued by them. The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.

If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project. You'll notice that the code below already exists in your project. If your application doesn't already have this logic, follow the steps below to add it and to verify that it’s working correctly.

1. In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.
2. Open the **Global.asax.cs** file and add the following using directives: 

    ```
    using System.Configuration;
    using System.IdentityModel.Tokens;
    ```
3. Add the following method to the **Global.asax.cs** file: 

    ```
    protected void RefreshValidationSettings()
    {
     string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
     string metadataAddress =
                   ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
     ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
    }
    ```
4. Invoke the **RefreshValidationSettings()** method in the **Application\_Start()** method in **Global.asax.cs** as shown: 

    ```
    protected void Application_Start()
    {
     AreaRegistration.RegisterAllAreas();
     ...
     RefreshValidationSettings();
    }
    ```

Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys. This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.

Follow the steps below to verify that the key rollover logic is working.

1. After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **&lt;issuerNameRegistry&gt;** block, specifically looking for the following few lines: 

    ```
    <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
         <authority name="https://sts.windows.net/aaaabbbb-0000-cccc-1111-dddd2222eeee/">
           <keys>
             <add thumbprint="AA11BB22CC33DD44EE55FF66AA77BB88CC99DD00" />
           </keys>
    ```
2. In the **&lt;add thumbprint=""&gt;** setting, change the thumbprint value by replacing any character with a different one. Save the **Web.config** file.
3. Build the application, and then run it. If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document. If you're having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Microsoft identity platform](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) article, or downloading and inspecting the following code sample: [Multitenant Cloud Application for Microsoft Entra ID](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols

If you're using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document. One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.

If the key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by performing a manual rollover as per the instructions at the end of this guidance document. **It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if the Microsoft identity platform increases its rollover cadence or has an emergency out-of-band rollover.

## How to test your application to determine if it will be affected

You can validate whether your application supports automatic key rollover by using the following PowerShell scripts.

To check and update signing keys with PowerShell, you'll need the [MSIdentityTools](https://www.powershellgallery.com/packages/MSIdentityTools) PowerShell module.

1. Install the [MSIdentityTools](https://www.powershellgallery.com/packages/MSIdentityTools) PowerShell module:

    ```powershell
    Install-Module -Name MSIdentityTools
    ```
2. Sign in by using the Connect-MgGraph command with an admin account to consent to the required scopes:

    ```powershell
     Connect-MgGraph -Scope "Application.ReadWrite.All"
    ```
3. Get the list of available signing key thumbprints:

    ```powershell
    Get-MsIdSigningKeyThumbprint
    ```
4. Pick any of the key thumbprints and configure Microsoft Entra ID to use that key with your application (get the app ID from the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)):

    ```powershell
    Update-MsIdApplicationSigningKeyThumbprint -ApplicationId <ApplicationId> -KeyThumbprint <Thumbprint>
    ```
5. Test the web application by signing in to get a new token. The key update change is instantaneous, but make sure you use a new browser session (using, for example, Internet Explorer's "InPrivate," Chrome's "Incognito," or Firefox's "Private" mode) to ensure you're issued a new token.
6. For each of the returned signing key thumbprints, run the `Update-MsIdApplicationSigningKeyThumbprint` cmdlet and test your web application sign-in process.
7. If the web application signs you in properly, it supports automatic rollover. If it doesn't, modify your application to support manual rollover. Check out Establishing a manual rollover process for more information.
8. Run the following script to revert to normal behavior:

    ```powershell
    Update-MsIdApplicationSigningKeyThumbprint -ApplicationId <ApplicationId> -Default
    ```

## How to perform a manual rollover if your application doesn't support automatic rollover

If your application doesn't support automatic rollover, you need to establish a process that periodically monitors Microsoft identity platform's signing keys and performs a manual rollover accordingly.

To check and update signing keys with PowerShell, you need the [`MSIdentityTools`](https://www.powershellgallery.com/packages/MSIdentityTools) PowerShell module.

1. Install the [`MSIdentityTools`](https://www.powershellgallery.com/packages/MSIdentityTools) PowerShell module:

    ```powershell
    Install-Module -Name MSIdentityTools
    ```
2. Get the latest signing key (get the tenant ID from the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)):

    ```powershell
    Get-MsIdSigningKeyThumbprint -Tenant <tenantId> -Latest
    ```
3. Compare this key against the key your application is currently hardcoded or configured to use.
4. If the latest key is different from the key your application is using, download the latest signing key:

    ```powershell
    Get-MsIdSigningKeyThumbprint -Latest -DownloadPath <DownloadFolderPath>
    ```
5. Update your application's code or configuration to use the new key.
6. Configure Microsoft Entra ID to use that latest key with your application (get the app ID from the [Microsoft Entra admin center](https://entra.microsoft.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)):

    ```powershell
    Get-MsIdSigningKeyThumbprint -Latest | Update-MsIdApplicationSigningKeyThumbprint -ApplicationId <ApplicationId>
    ```
7. Test the web application by signing in to get a new token. The key update change is instantaneous, but make sure you use a new browser session to ensure you're issued a new token. For example, use Microsoft Edge's "InPrivate," Chrome's "Incognito," or Firefox's "Private" mode.
8. If you experience any issues, revert to the previous key you were using and contact Azure support:

    ```powershell
    Update-MsIdApplicationSigningKeyThumbprint -ApplicationId <ApplicationId> -KeyThumbprint <PreviousKeyThumbprint>
    ```
9. After you update your application to support manual rollover, revert to normal behavior:

    ```powershell
    Update-MsIdApplicationSigningKeyThumbprint -ApplicationId <ApplicationId> -Default
    ```