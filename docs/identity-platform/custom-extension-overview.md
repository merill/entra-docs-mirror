---
layout: Conceptual
title: Custom authentication extensions overview - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/custom-extension-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Use Microsoft Entra custom authentication extensions to customize your user's sign-in experience by using REST APIs or outbound webhooks.
manager: pmwongera
ms.custom: 
ms.date: 2025-06-25T00:00:00.0000000Z
ms.reviewer: jasuri
ms.topic: concept-article
locale: en-us
document_id: ca040724-e255-7ede-4509-aceab9bf4258
document_version_independent_id: 5e1e1f68-478a-e60f-8e78-bbd4a9de014e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/custom-extension-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/custom-extension-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/custom-extension-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: fd47af07-aebc-37a4-1aa2-e86e78a8129d
---

# Custom authentication extensions overview - Microsoft identity platform | Microsoft Learn

The Microsoft Entra ID authentication pipeline consists of several built-in authentication events, like the validation of user credentials, Conditional Access policies, multifactor authentication, self-service password reset, and more.

Microsoft Entra custom authentication extensions allow you to extend authentication flows with your own business logic at specific points within the authentication flow. A custom authentication extension is essentially an event listener that, when activated, makes an HTTP call to a REST API endpoint where you define a workflow action.

For example, you could use a custom claims provider to add external user data to the security token before the token is issued. You could add an attribute collection workflow to validate the attributes a user enters during sign-up. This article provides a high-level, technical overview of Microsoft Entra ID custom authentication extensions.

The [Microsoft Entra Custom Authentication Extension Overview](https://youtu.be/ZU90avf0Qyc?si=Gf77u4HS_5uw6Qjp) video provides a comprehensive outline of the key features and capabilities of the custom authentication extensions.

## Components overview

There are two components you need to configure: a custom authentication extension in Microsoft Entra and a REST API. The custom authentication extension specifies your REST API endpoint, when the REST API should be called, and the credentials to call the REST API.

This video provides detailed instructions on configuring Microsoft Entra custom authentication extensions and offers best practices and valuable tips for optimal implementation.

## Sign-in flow

The following diagram depicts the sign-in flow integrated with a custom authentication extension.

[![Diagram that shows a token being augmented with claims from an external source.](media/custom-extension-overview/workflow.png)](media/custom-extension-overview/workflow.png#lightbox)

1. A user attempts to sign into an app and is redirected to the Microsoft Entra sign-in page.
2. Once a user completes a certain step in the authentication, an **event listener** is triggered.
3. Your **custom authentication extension** sends an HTTP request to your **REST API endpoint**. The request contains information about the event, the user profile, session data, and other context information.
4. The **REST API** performs a custom workflow.
5. The **REST API** returns an HTTP response to Microsoft Entra ID.
6. The Microsoft Entra **custom authentication extension** processes the response and customizes the authentication based on the event type and the HTTP response payload.
7. A **token** is returned to the **app**.

## REST API endpoints

When an event is triggered, Microsoft Entra ID invokes a REST API endpoint that you own. The REST API must be publicly accessible. It can be hosted using Azure Functions, Azure App Service, Azure Logic Apps, or another publicly available API endpoint.

You have the flexibility to use any programming language, framework, or low-code-no-code solution, such as Azure Logic Apps to develop and deploy your REST API. For a quick way to get started, consider employing Azure Function. It lets you run your code in a serverless environment without having to first create a virtual machine (VM) or publish a web application.

Your REST API must handle:

- Token validation for securing the REST API calls.
- Business logic
- Return data and action type
- Incoming and outgoing validation of HTTP request and response schemas.
- Auditing and logging.
- Availability, performance, and security controls.

Watch this video to learn how to create an authentication extensions REST API endpoint with Azure Logic Apps, without writing code. Azure Logic App empowers users to build workflows using a visual designer. The video covers customizing verification emails, and it applies to all types of custom authentication extensions, including custom claims providers.

### Request payload

The request to the REST API includes a JSON payload containing details about the event, user profile, authentication request data, and other context information. The attributes within the JSON payload can be used to perform logic by your API.

For example, in the Token issuance start event, the request payload may include the user's unique identifier, allowing you to retrieve the user profile from your own database. The request payload data must follow the schema as specified in the event document.

### Return data and action type

After your web API performs the workflow with your business logic, it must return an **action type** that directs Microsoft Entra on how to proceed with the authentication process.

For example, in the case of the attribute collection start and attribute collection submit events, the **action type** returned by your web API indicates whether the account can be created in the directory, show a validation error, or completely block the sign-up flow.

The REST API response may include data. For example, the on token issuance start event may provide a set of attributes that can be mapped to the security token.

### Protect your REST API

To ensure the communications between the custom authentication extension and your REST API are secured appropriately, multiple security controls must be applied.

1. When the custom authentication extension calls your REST API, it sends an HTTP `Authorization` header with a bearer token issued by Microsoft Entra ID.
2. The bearer token contains an `appid` or `azp` claim. Validate that the respective claim contains the `99045fe1-7639-4a75-9d4a-577b6ca3810f`value. This value ensures that the Microsoft Entra ID is the one who calls the REST API.
    1. For **V1** Applications, validate the `appid` claim.
    2. For **V2** Applications, validate the `azp` claim.
3. The bearer token `aud` audience claim contains the ID of the associated application registration. Your REST API endpoint needs to validate that the bearer token is issued for that specific audience.
4. The bearer token `iss`issuer claim contains the Microsoft Entra issuer URL. Depending on your tenant configuration, the issuer URL is one of the following;
    - Workforce: `https://login.microsoftonline.com/{tenantId}/v2.0`.
    - Customer: `https://{domainName}.ciamlogin.com/{tenantId}/v2.0`.

## Custom authentication event types

This section lists the custom authentication extensions events available in Microsoft Entra ID workforce and external tenants. For detailed information about the events, refer to the respective documentation.

| Event | Workforce tenant | External tenant |
| --- | --- | --- |
| Token issuance start | ![](media/common/yes.png) | ![](media/common/yes.png) |
| Attribute collection start |  | ![](media/common/yes.png) |
| Attribute collection submit |  | ![](media/common/yes.png) |
| One time passcode send |  | ![](media/common/yes.png) |
| Account Recovery (additional claim validation) | ![](media/common/yes.png) |  |

### Token issuance start

The token issuance start event, **OnTokenIssuanceStart** is triggered when a token is about to be issued to an application. It is an event type set up within a [custom claims provider](custom-claims-provider-overview). The custom claims provider is a custom authentication extension that calls a REST API to fetch claims from external systems. A custom claims provider maps claims from external systems into tokens and can be assigned to one or many applications in your directory.

### Attribute collection start

[Attribute collection start](custom-extension-attribute-collection) events can be used with custom authentication extensions to add logic before attributes are collected from a user. The **OnAttributeCollectionStart** event occurs at the beginning of the attribute collection step, before the attribute collection page renders. It lets you add actions such as prefilling values and displaying a blocking error.

### Attribute collection submit

[Attribute collection submit](custom-extension-attribute-collection) events can be used with custom authentication extensions to add logic after attributes are collected from a user. The **OnAttributeCollectionSubmit** event triggers after the user enters and submits attributes, allowing you to add actions like validating entries or modifying attributes.

### One time passcode send

The **OnOtpSend** event is triggered when a one time passcode email is activated. It allows you to [call a REST API to use your own email provider](custom-extension-email-otp-get-started). This event can be used to send customized emails to users who sign up with email address, sign in with email one-time passcode (Email OTP), reset their password using Email OTP, or use Email OTP for multifactor authentication (MFA).

When the **OnOtpSend** event is activated, Microsoft Entra sends a one-time passcode to the specified REST API you own. The REST API then uses your chosen email provider, such as Azure Communication Service or SendGrid, to send the one-time passcode with your custom email template, from address, and email subject, while also supporting localization.

### Account Recovery (additional claim validation)

The **OnVerifiedIdClaimValidation** event is triggered during [account recovery](../identity/authentication/concept-account-recovery-overview) when a user presents Verified ID claims to re-establish their identity. The primary reason to use a custom authentication extension for account recovery is to confirm that the person requesting recovery is an actual employee, not just a valid human. When a user presents their Verified ID, Microsoft Entra passes the claims from the credential to your custom authentication extension. Your REST API can then compare those claims against an authoritative data source, such as an HR system or employee records database, and return a pass or fail decision.

When you move an account recovery profile from Eval mode to Production mode, we highly recommend using a custom authentication extension. The built-in first name and last name matching isn't reliable enough for larger user groups and should only be used for a very small set of users.

For more information, see [Create a custom authentication extension for account recovery claim validation](tutorial-custom-authentication-extension-account-recovery). Only one custom authentication extension per tenant is allowed for this event type.