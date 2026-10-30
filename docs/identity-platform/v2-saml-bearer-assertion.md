---
layout: Conceptual
title: Exchange a SAML token issued by Active Directory Federation Services (AD FS) for a Microsoft Graph access token - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/v2-saml-bearer-assertion
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to fetch data from Microsoft Graph without prompting an AD FS-federated user for credentials by using the SAML bearer assertion flow.
manager: pmwongera
ms.date: 2024-09-24T00:00:00.0000000Z
ms.reviewer: nickludwig, paulgarn
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 9f168986-8f8f-4e97-cba8-547564c97eb5
document_version_independent_id: 12ac4571-4f35-300e-9119-8d13673f3722
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/v2-saml-bearer-assertion.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/v2-saml-bearer-assertion
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/v2-saml-bearer-assertion.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: adb23037-62fd-651e-9504-8af844a388a5
---

# Exchange a SAML token issued by Active Directory Federation Services (AD FS) for a Microsoft Graph access token - Microsoft identity platform | Microsoft Learn

To enable single sign-on (SSO) in applications that use SAML tokens issued by Active Directory Federation Services (AD FS) and also require access to Microsoft Graph, follow the steps in this article.

You'll enable the SAML bearer assertion flow to exchange a SAMLv1 token issued by the federated AD FS instance for an OAuth 2.0 access token for Microsoft Graph. When the user's browser is redirected to Microsoft Entra ID to authenticate them, the browser picks up the session from the SAML sign-in instead of asking the user to enter their credentials.

Important

This scenario works **only** when AD FS is the federated identity provider that issued the original SAMLv1 token. You **cannot** exchange a SAMLv2 token issued by Microsoft Entra ID for a Microsoft Graph access token.

## Prerequisites

- AD FS federated as an identity provider for single sign-on; see [Setting up AD FS and Enabling Single Sign-On to Office 365](/en-us/archive/blogs/canitpro/step-by-step-setting-up-ad-fs-and-enabling-single-sign-on-to-office-365) for an example.
- A rest client to make HTTP requests.

## Scenario overview

The OAuth 2.0 SAML bearer assertion flow allows you to request an OAuth access token using a SAML assertion when a client needs to use an existing trust relationship. The signature applied to the SAML assertion provides authentication of the authorized app. A SAML assertion is an XML security token issued by an identity provider and consumed by a service provider. The service provider relies on its content to identify the assertion's subject for security-related purposes.

The SAML assertion is posted to the OAuth token endpoint. The endpoint processes the assertion and issues an access token based on prior approval of the app. The client isn't required to have or store a refresh token, nor is the client secret required to be passed to the token endpoint.

### Register the application with Microsoft Entra ID

To register the application with Microsoft Entra ID, complete the steps in the [Register an application with the Microsoft identity platform](quickstart-register-app) article.

### Get the SAML assertion from AD FS

Create a POST request to the AD FS endpoint using SOAP envelope to fetch the SAML assertion:

`POST https://ADFSFQDN/adfs/services/trust/2005/usernamemixed`

**Parameter values:**

| Key | Value |
| --- | --- |
| client-request-id | CLIENT\_ID |

**Header values:**

| Key | Value |
| --- | --- |
| SOAPAction | `http://schema.xlmsoap.org/ws/2005/02/trust/RST/Issue` |
| Content-Type | application/soap+xml |
| client-request-id | CLIENT\_ID |
| return-client-request-id | true |
| Accept | application/json |

**AD FS request body:**

```xml
<s:Envelope xmlns:s="http://www.w3.org/2003/05/soap-envelope">
  <s:Header>
    <a:Action s:mustUnderstand="1" xmlns:a="http://schemas.xmlsoap.org/ws/2004/08/addressing">http://schemas.xmlsoap.org/ws/2005/02/trust/RST/Issue</a:Action>
    <a:MessageID>urn:uuid:9af3303f-1f9e-466c-9938-c9a982822557</a:MessageID>
    <a:ReplyTo>
      <a:Address>http://www.w3.org/2005/08/addressing/anonymous</a:Address>
    </a:ReplyTo>
    <o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
      <o:UsernameToken u:Id="uuid-2525825F-6A4A-44D8-83BA-68E26F4DD99">
        <o:Username>USERNAME</o:Username>
        <o:Password>PASSWORD</o:Password>
      </o:UsernameToken>
    </o:Security>
  </s:Header>
  <s:Body>
    <trust:RequestSecurityToken xmlns:trust="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <a:EndpointReference>
          <a:Address>urn:federation:MicrosoftOnline</a:Address>
        </a:EndpointReference>
      </wsp:AppliesTo>
      <trust:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</trust:KeyType>
      <trust:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</trust:RequestType>
      <trust:TokenType>http://schemas.xmlsoap.org/ws/2005/02/sc/sct</trust:TokenType>
    </trust:RequestSecurityToken>
  </s:Body>
</s:Envelope>
```

Once the request is posted successfully, you should receive a SAML assertion from AD FS. Only the **SAML:Assertion** tag data is required, convert it to base64 encoding to use in further requests.

### Get the OAuth 2.0 token using the SAML assertion

Fetch an OAuth 2.0 token using the AD FS assertion response.

Create a POST request with the header values:

| Key | Value | Description |
| --- | --- | --- |
| Host | login.microsoftonline.com |  |
| Content-Type | application/x-www-form-urlencoded |  |

In the body of the request, replace client\_id, client\_secret, and assertion (the base64 encoded SAML assertion obtained the previous step):

| Key | Value | Description |
| --- | --- | --- |
| grant\_type | urn:ietf:params:oauth:grant-type:saml2-bearer | Specifies the type of grant |
| client\_id | CLIENTID | Your application's client ID |
| client\_secret | CLIENTSECRET | Your application's client secret |
| assertion | ASSERTION | The base64 encoded SAML assertion |
| scope | openid `https://graph.microsoft.com/.default` | The scopes for which the token is valid |

Upon successful request, you'll receive an access token from Microsoft Entra ID.

### Get the data with the OAuth 2.0 token

After receiving the access token, call the Graph APIs (Outlook tasks in this example).

Create a GET request with the access token fetched in the previous step:

| Key | Value | Description |
| --- | --- | --- |
| Content-Type | application/x-www-form-urlencoded |  |
| Authorization | Bearer ACCESS\_TOKEN | Access token obtained from the OAuth 2.0 token request |

Upon successful request, you'll receive a JSON response.