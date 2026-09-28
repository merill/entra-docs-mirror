---
layout: Conceptual
title: Add OIDC for customer sign-in - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-custom-oidc-federation-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to set up OpenID Connect as an external identity provider in Microsoft Entra External ID, enabling users to sign in using their existing accounts.
ms.topic: how-to
ms.date: 2026-07-29T00:00:00.0000000Z
ms.reviewer: brozbab
ms.custom: it-pro, msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: e3106d07-fe50-3fd6-fe45-4f0d84a7362a
document_version_independent_id: e3106d07-fe50-3fd6-fe45-4f0d84a7362a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-custom-oidc-federation-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-custom-oidc-federation-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-custom-oidc-federation-customers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: bf942373-7346-26a6-944b-c737caeaa5ec
---

# Add OIDC for customer sign-in - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

By setting up federation with a custom-configured OpenID Connect (OIDC) identity provider, you enable users to sign in to your applications using their existing accounts from the federated external provider. This OIDC federation allows authentication with various providers that adhere to the OpenID Connect protocol. (Learn more about [authentication methods and identity providers for customers](concept-authentication-methods-customers).)

## Prerequisites

- An [external tenant](how-to-create-external-tenant-portal).
- A [registered application](/en-us/entra/identity-platform/quickstart-register-app) in the external tenant.
- A [sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers).

## Set up your OpenID Connect identity provider

To federate users to your identity provider, first prepare your identity provider to accept federation requests from your external tenant. To do this preparation, add your redirect URIs and register your identity provider to be recognized.

Before moving to the next step, add your redirect URIs as follows:

`https://<tenant-subdomain>.ciamlogin.com/<tenant-ID>/federation/oauth2`

`https://<tenant-subdomain>.ciamlogin.com/<tenant-subdomain>.onmicrosoft.com/federation/oauth2`

## Enable sign-in and sign-up with your identity provider

To enable sign-in and sign-up for users with an account in your identity provider, you need to register Microsoft Entra ID as an application in your identity provider. This step allows your identity provider to recognize and issue tokens to your Microsoft Entra ID for federation. Register the application using your populated redirect URIs. Save the details of your identity provider configuration to set up federation in your external tenant.

### Federation settings

To configure OpenID Connect federation with your identity provider in Microsoft Entra External ID, you need the following settings:

- **Well-known endpoint**
- **Issuer URI**
- **Client ID**
- **Client Authentication Method**
- **Client Secret**
- **Scope**
- **Response Type**
- **Claims mapping**
    - Sub
    - Name
    - Given name
    - Family name
    - Email (required by default; can be made optional)
    - Email\_verified
    - Phone number
    - Phone\_number\_verified
    - Street address
    - Locality
    - Region
    - Postal code
    - Country

## Configure a new OpenID Connect identity provider in the admin center

After you configure your identity provider, complete this step to configure a new OpenID Connect federation in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External Identity Provider Administrator](../../identity/role-based-access-control/permissions-reference#external-identity-provider-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **All identity providers**.
3. Select the **Custom** tab, and then select **Add new** &gt; **Open ID Connect**.

    ![Screenshot of adding a new custom identity provider.](media/how-to-custom-oidc-federation-customers/add-new.jpg)
4. Enter the following details for your identity provider:

    - **Display name**: The name of your identity provider that you display to your users during the sign-in and sign-up flows. For example, *Sign in with IdP name* or *Sign up with IdP name*.
    - **Well-known endpoint** (also known as metadata URI) is the OIDC discovery URI to [obtain the configuration information](https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderConfig) for your identity provider. The response is a JSON document that includes OAuth 2.0 endpoint locations. At a minimum, the metadata document must contain the following properties: `issuer`, `authorization_endpoint`, `token_endpoint`, `token_endpoint_auth_methods_supported`, `response_types_supported`, `subject_types_supported`, and `jwks_uri`. For more details, see [OpenID Connect Discovery](https://openid.net/specs/openid-connect-discovery-1_0.html) specifications.
    - **OpenID Issuer URI**: The entity of your identity provider that issues access tokens for your application. For example, if you use OpenID Connect to [federate with your Azure AD B2C](how-to-b2c-federation-customers), your issuer URI looks like: `https://login.b2clogin.com/{tenant}/v2.0/`. The issuer URI is a case-sensitive URL that uses the https scheme. It contains scheme, host, and optionally port number and path components, but no query or fragment components.

    Note

    To federate with a Microsoft Entra ID tenant, see [Add a Microsoft Entra ID tenant as an OpenID Connect identity provider](how-to-entra-id-federation-customers). OIDC federation also isn't compatible with the [Invite external user (preview)](/en-us/entra/external-id/customers/concept-supported-features-customers#identity-providers-and-authentication-methods) feature.

    - **Client ID** and **Client Secret** are the identifiers your identity provider uses to identify the registered application service. Provide a client secret when you select a `client_secret`-based authentication method.
    - **Client Authentication** is the type of client authentication method to be used to authenticate with your identity provider using the token endpoint. `client_secret_post` and `client_secret_jwt` authentication methods are supported. Although the admin center UI might display `private_key_jwt` as an option, this method isn't currently supported and shouldn't be selected.

    Note

    Due to possible security problems, the `client_secret_basic` client authentication method isn't supported.

    - **Scope** defines the information and permissions you're looking to gather from your identity provider, for example `openid profile`. OpenID Connect requests must contain the `openid` scope value to receive the ID token from your identity provider. Other scopes can be appended separated by spaces. See the [OpenID Connect documentation](https://openid.net/specs/openid-connect-core-1_0.html) for other available scopes such as `profile`, `email`, and more.
    - **Response type** describes what kind of information is sent back in the initial call to the `authorization_endpoint` of your identity provider. Currently, only the `code` response type is supported. `id_token` and `token` aren't supported.
5. Select **Next: Claims mapping** to configure [claims mapping](reference-oidc-claims-mapping-customers) or **Review + create** to add your identity provider.

Note

Microsoft recommends you do *not* use the [implicit grant flow](/en-us/entra/identity-platform/v2-oauth2-implicit-grant-flow#security-concerns-with-implicit-grant-flow) or the [ROPC flow](/en-us/entra/identity-platform/v2-oauth-ropc). Therefore, OpenID Connect external identity provider configuration doesn't support these flows. The recommended way of supporting SPAs is [OAuth 2.0 Authorization code flow (with PKCE)](/en-us/entra/identity-platform/v2-oauth2-auth-code-flow#applications-that-support-the-auth-code-flow) which is supported by OIDC federation configuration.

## Enable users to sign in and sign up with the identity provider

After you configure the OIDC identity provider, add it to a user flow to allow sign-in and sign-up with the identity provider. See [Add an identity provider to a user flow](how-to-add-identity-provider-to-user-flow-customers).

## Make email optional for external identity provider sign-up

By default, an email address is required when users sign up with an external identity provider (IdP). If your external IdP doesn't send an email claim, users encounter the error `AADSTS901011: No email address was obtained from the external oidc identity provider` during sign-up. To avoid this error, configure your user flow to make the email attribute optional. Users can then complete sign-up with only their external IdP identity, without providing an email address.

Important

Making email optional is a user flow–level setting. This change applies to sign-ups for **all applications** associated with the user flow.

Tip

The account picker typically displays the user's email address. When no email address is collected, the display name is shown instead. To help users easily identify their account, map the `name` claim in [Claims mapping](reference-oidc-claims-mapping-customers) or collect display name during sign-up.

### Update the user flow to make email optional

To make the email attribute optional in your user flow, use the Microsoft Graph API to update the `onAttributeCollection` property of the user flow.

1. Find the ID of the user flow you want to update. One way to do this is to use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to list all your user flows:

    ```http
    GET https://graph.microsoft.com/v1.0/identity/authenticationEventsFlows
    ```

    Locate the `id` of the user flow and the `onAttributeCollection` property in the response.
2. Copy the `onAttributeCollection` property from the response, and use it to update the user flow with a `PATCH` request. The only change you need to make is to set the `required` property on the email attribute to `false`:

    ```http
    PATCH https://graph.microsoft.com/v1.0/identity/authenticationEventsFlows/{user-flow-id}
    Content-Type: application/json
    
    {
        "@odata.type": "#microsoft.graph.externalUsersSelfServiceSignUpEventsFlow",
        "onAttributeCollection": {
            "@odata.type": "#microsoft.graph.onAttributeCollectionExternalUsersSelfServiceSignUp",
            "attributeCollectionPage": {
                "views": [
                    {
                        "title": null,
                        "description": null,
                        "inputs": [
                            {
                                "attribute": "email",
                                "label": "Email Address",
                                "inputType": "text",
                                "defaultValue": null,
                                "hidden": false,
                                "editable": true,
                                "writeToDirectory": true,
                                "required": false,
                                "validationRegEx": "^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\\.[a-zA-Z0-9-]+)*$",
                                "options": []
                            }
                        ]
                    }
                ]
            }
        }
    }
    ```

    Note

    Include all the attribute inputs from your existing user flow in the `PATCH` request, not just the email attribute. The preceding example shows only the email input, but your user flow might include additional attributes. For the full schema, see [authenticationAttributeCollectionPage resource type](/en-us/graph/api/resources/authenticationattributecollectionpage).

## Known limitations

### Issuer URI updates

When you update the Issuer URI for an existing OIDC identity provider (IdP), the updated configuration might not automatically take effect in user flows. As a result, the IdP sign-in option might not appear on the sign-in page.

To apply the change:

1. Disable the IdP in the user flow.
2. Save the user flow.
3. Re-enable the IdP.
4. Save the user flow again.