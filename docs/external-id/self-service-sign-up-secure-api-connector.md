---
layout: Conceptual
title: Secure APIs used as API connectors in Microsoft Entra External ID self-service sign-up user flows - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/self-service-sign-up-secure-api-connector
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Secure your custom RESTful APIs used as API connectors in self-service sign-up user flows.
ms.topic: how-to
ms.date: 2025-04-15T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 096ff804-707b-962a-93e6-b0671a150ad3
document_version_independent_id: f4dd45b9-e704-97d1-d3e1-ac3e52c987e1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/self-service-sign-up-secure-api-connector.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/self-service-sign-up-secure-api-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/self-service-sign-up-secure-api-connector.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: 9341e288-7d14-5e18-b4f0-47a5eb76afd4
---

# Secure APIs used as API connectors in Microsoft Entra External ID self-service sign-up user flows - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

When integrating a REST API within a Microsoft Entra External ID self-service sign-up user flow, you must protect your REST API endpoint with authentication. The REST API authentication ensures that only services that have proper credentials, such as Microsoft Entra ID, can make calls to your endpoint. This article explores how to secure REST API.

## Prerequisites

Complete the steps in the [Walkthrough: Add an API connector to a sign-up user flow](self-service-sign-up-add-api-connector) guide.

You can protect your API endpoint by using either HTTP basic authentication or HTTPS client certificate authentication. In either case, you provide the credentials that Microsoft Entra ID uses when calling your API endpoint. Your API endpoint then checks the credentials and performs authorization decisions.

## HTTP basic authentication

HTTP basic authentication is defined in [RFC 2617](https://tools.ietf.org/html/rfc2617). Basic authentication works as follows: Microsoft Entra ID sends an HTTP request with the client credentials (`username` and `password`) in the `Authorization` header. The credentials are formatted as the base64-encoded string `username:password`. Your API then is responsible for checking these values to perform other authorization decisions.

To configure an API Connector with HTTP basic authentication, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Overview**.
3. Select **All API connectors**, and then select the **API Connector** you want to configure.
4. For the **Authentication type**, select **Basic**.
5. Provide the **Username**, and **Password** of your REST API endpoint. ![Screenshot of basic authentication configuration for an API connector.](media/secure-api-connector/api-connector-config.png)
6. Select **Save**.

## HTTPS client certificate authentication

Client certificate authentication is a mutual certificate-based authentication. The client, Microsoft Entra ID, provides its client certificate to the server to prove its identity as part of the SSL handshake. Your API is responsible for validating the certificates belong to a valid client, such as Microsoft Entra ID, and performing authorization decisions. The client certificate is an X.509 digital certificate.

Important

In production environments, the certificate must be signed by a certificate authority.

### Create a certificate

#### Option 1: Use Azure Key Vault (recommended)

To create a certificate, you can use [Azure Key Vault](/en-us/azure/key-vault/certificates/create-certificate), which has options for self-signed certificates and integrations with certificate issuer providers for signed certificates. Recommended settings include:

- **Subject**: `CN=<yourapiname>.<tenantname>.onmicrosoft.com`
- **Content Type**: `PKCS #12`
- **Lifetime Acton Type**: `Email all contacts at a given percentage lifetime` or `Email all contacts a given number of days before expiry`
- **Key Type**: `RSA`
- **Key Size**: `2048`
- **Exportable Private Key**: `Yes` (in order to be able to export `.pfx` file)

You can then [export the certificate](/en-us/azure/key-vault/certificates/how-to-export-certificate).

#### Option 2: prepare a self-signed certificate using PowerShell

If you don't already have a certificate, you can use a self-signed certificate. A self-signed certificate is a security certificate that is not signed by a certificate authority (CA) and doesn't provide the security guarantees of a certificate signed by a CA.

# [Windows](#tab/windows)
On Windows, use the [New-SelfSignedCertificate](/en-us/powershell/module/pki/new-selfsignedcertificate) cmdlet in PowerShell to generate a certificate.

1. Run the following PowerShell command to generate a self-signed certificate. Modify the `-Subject` argument as appropriate for your application and Azure AD B2C tenant name such as `contosowebapp.contoso.onmicrosoft.com`. You can also adjust the `-NotAfter` date to specify a different expiration for the certificate.

    ```PowerShell
    New-SelfSignedCertificate `
        -KeyExportPolicy Exportable `
        -Subject "CN=yourappname.yourtenant.onmicrosoft.com" `
        -KeyAlgorithm RSA `
        -KeyLength 2048 `
        -KeyUsage DigitalSignature `
        -NotAfter (Get-Date).AddMonths(12) `
        -CertStoreLocation "Cert:\CurrentUser\My"
    ```
2. On Windows computer, search for and select **Manage user certificates**
3. Under **Certificates - Current User**, select **Personal** &gt; **Certificates**&gt;*yourappname.yourtenant.onmicrosoft.com*.
4. Select the certificate, and then select **Action** &gt; **All Tasks** &gt; **Export**.
5. Select **Next** &gt; **Yes, export the private key** &gt; **Next**.
6. Accept the defaults for **Export File Format**, and then select **Next**.
7. Enable **Password** option, enter a password for the certificate, and then select **Next**.
8. To specify a location to save your certificate, select **Browse** and navigate to a directory of your choice.
9. On the **Save As** window, enter a **File name**, and then select **Save**.
10. Select **Next**&gt;**Finish**.

For Azure AD B2C to accept the .pfx file password, the password must be encrypted with the TripleDES-SHA1 option in the Windows Certificate Store Export utility, as opposed to AES256-SHA256.

# [macOS](#tab/macos)
On macOS, use [Certificate Assistant](https://support.apple.com/guide/keychain-access/aside/glosa3ed0609/11.0/mac/11.0) in Keychain Access to generate a certificate.

1. Follow the instructions for how to [create self-signed certificates in Keychain Access on a Mac](https://support.apple.com/guide/keychain-access/kyca8916/mac).
2. In the Keychain Access app on your Mac, select the certificate that you created.
3. Select **File** &gt; **Export Items**.
4. Select a file name to save your certificate. For example: **self-signed-certificate.p12**.
5. For **File Format**, select **Personal Information Exchange (.p12)**.
6. Select **Save**.
7. Enter a password in the **Password** and **Verify** boxes.
8. Replace the file extension to .pfx. For example: **self-signed-certificate.pfx**.

---

### Configure your API Connector

To configure an API Connector with client certificate authentication, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Overview**.
3. Select **All API connectors**, and then select the **API Connector** you want to configure.
4. For the **Authentication type**, select **Certificate**.
5. In the **Upload certificate** box, select your certificate's .pfx file with a private key.
6. In the **Enter Password** box, type the certificate's password. ![Screenshot of certificate authentication configuration for an API connector.](media/secure-api-connector/api-connector-upload-cert.png)
7. Select **Save**.

### Perform authorization decisions

Your API must implement the authorization based on sent client certificates in order to protect the API endpoints. For Azure App Service and Azure Functions, see [configure TLS mutual authentication](/en-us/azure/app-service/app-service-web-configure-tls-mutual-auth) to learn how to enable and *validate the certificate from your API code*. You can alternatively use Azure API Management as a layer in front of any API service to [check client certificate properties](/en-us/azure/api-management/api-management-howto-mutual-certificates-for-clients) against desired values.

### Renewing certificates

We recommend setting reminder alerts for when your certificate expires. You need to generate a new certificate and repeat the steps in this article when used certificates are about to expire. To "roll" the use of a new certificate, your API service can continue to accept old and new certificates for a temporary amount of time while the new certificate is deployed.

To upload a new certificate to an existing API connector, select the API connector under **API connectors** and select on **Upload new certificate**. Microsoft Entra ID automatically uses the most recently uploaded certificate that isn't expired and whose start date has passed.

![Screenshot of a new certificate, when one already exists.](media/secure-api-connector/api-connector-renew-cert.png)

## API key authentication

Some services use an "API key" mechanism to obfuscate access to your HTTP endpoints during development by requiring the caller to include a unique key as an HTTP header or HTTP query parameter. For [Azure Functions](/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger#authorization-keys), include the `code` as a query parameter in the **Endpoint URL** of your API connector. For example, `https://contoso.azurewebsites.net/api/endpoint`**`?code=0123456789`**).

You shouldn't use this mechanism alone in production. Therefore, configuration for basic or certificate authentication is always required. If you don't wish to implement any authentication method (not recommended) for development purposes, you can select 'basic' authentication in the API connector configuration and use temporary values for `username` and `password` that your API can disregard while you implement proper authorization.