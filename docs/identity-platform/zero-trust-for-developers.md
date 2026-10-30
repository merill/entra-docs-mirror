---
layout: Conceptual
title: Increase application security using Zero Trust principles - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/zero-trust-for-developers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how using Zero Trust principles can help increase the security of your application and its data.
manager: pmwongera
ms.custom: 
ms.date: 2023-01-06T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: 8d25049c-846c-81eb-eac8-16ce816e288d
document_version_independent_id: f64eb6e5-c0db-c955-03b5-aa3a92c75871
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/zero-trust-for-developers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/zero-trust-for-developers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/zero-trust-for-developers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: bdee2894-f424-4c73-434f-aaa1926a9bd8
---

# Increase application security using Zero Trust principles - Microsoft identity platform | Microsoft Learn

A secure network perimeter around the applications that are developed can't be assumed. Nearly every developed application, by design, will be accessed from outside the network perimeter. Applications can't be guaranteed to be secure when they're developed or will remain so after they're deployed. It's the responsibility of the application developer to not only maximize the security of the application, but also minimize the damage the application can cause if it's compromised.

Additionally, the responsibility includes supporting the evolving needs of the customers and users, who expect that the application meets Zero Trust security requirements. Learn the principles of the [Zero Trust model](https://www.microsoft.com/security/business/zero-trust?rtc=1) and adopt the practices. By learning and adopting the principles, applications can be developed that are more secure and that minimize the damage they could cause if there's a break in security.

The Zero Trust model prescribes a culture of explicit verification rather than implicit trust. The model is anchored on three key [guiding principles](/en-us/security/zero-trust/#guiding-principles-of-zero-trust):

- Verify explicitly
- Use least privileged access
- Assume breach

## Zero Trust best practices

Follow these best practices to build Zero Trust-ready applications with the [Microsoft identity platform](v2-overview) and its tools.

### Verify explicitly

The Microsoft identity platform offers authentication mechanisms for verifying the identity of the person or service accessing a resource. Apply the best practices described below to *verify explicitly* any entities that need to access data or resources.

| Best practice | Benefits to application security |
| --- | --- |
| Use the [Microsoft Authentication Libraries (MSAL)](reference-v2-libraries). | MSAL is a set of Microsoft Authentication Libraries for developers. With MSAL, users and applications can be authenticated, and tokens can be acquired to access corporate resources using just a few lines of code. MSAL uses modern protocols ([OpenID Connect and OAuth 2.0](v2-protocols)) that remove the need for applications to ever handle a user's credentials directly. This handling of credentials vastly improves the security for both users and applications as the identity provider becomes the security perimeter. Also, these protocols continuously evolve to address new paradigms, opportunities, and challenges in identity security. |
| Adopt enhanced security extensions like [Continuous Access Evaluation (CAE)](../identity/conditional-access/concept-continuous-access-evaluation) and Conditional Access authentication context when appropriate. | In Microsoft Entra ID, some of the most used extensions include [Conditional Access](../identity/conditional-access/overview), [Conditional Access authentication context](developer-guide-conditional-access-authentication-context) and CAE. Applications that use enhanced security features like CAE and Conditional Access authentication context must be coded to handle claims challenges. Open protocols enable the [claims challenges and claims requests](claims-challenge) to be used to invoke extra client capabilities. The capabilities might be to continue interaction with Microsoft Entra ID, such as when there was an anomaly or if the user authentication conditions change. These extensions can be coded into an application without disturbing the primary code flows for authentication. |
| Use the correct **authentication flow** by [application type](v2-app-types). For web applications, always try to use [confidential client flows](authentication-flows-app-scenarios#single-page-public-client-and-confidential-client-applications). For mobile applications, try to use [brokers](msal-android-single-sign-on#sso-through-brokered-authentication) or the [system browser](msal-android-single-sign-on#sso-through-system-browser) for authentication. | The flows for web applications that can hold a secret (confidential clients) are considered more secure than public clients (for example: Desktop and Console applications). When the system web browser is used to authenticate a mobile application, a secure [single sign-on (SSO)](../identity/enterprise-apps/what-is-single-sign-on) experience enables the use of application protection policies. |

### Use least privileged access

A developer uses the Microsoft identity platform to grant permissions (scopes) and verify that a caller has been granted proper permission before allowing access. Enforce least privileged access in applications by enabling fine-grained permissions that allow the smallest amount of access necessary to be granted. Consider the following practices to make sure of adherence to the [principle of least privilege](secure-least-privileged-access):

- Evaluate the permissions that are requested to make sure that the absolute least privileged is set to get the job done. Don't create "catch-all" permissions with access to the entire API surface.
- When designing APIs, provide granular permissions to allow least-privileged access. Start with dividing the functionality and data access into sections that can be controlled by using [scopes](scopes-oidc) and [App roles](howto-add-app-roles-in-apps). Don't add APIs to existing permissions in a way that changes the semantics of the permission.
- Offer **read-only** permissions. `Write` access, includes privileges for create, update, and delete operations. A client should never require write access to only read data.
- Offer both [delegated and application](/en-us/graph/auth/auth-concepts#delegated-and-application-permissions) permissions. Skipping application permissions can create hard requirement for clients to achieve common scenarios like automation, microservices and more.
- Consider "standard" and "full" access permissions if working with sensitive data. Restrict the sensitive properties so that they can't be accessed using a "standard" access permission, for example `Resource.Read`. And then implement a "full" access permission, for example `Resource.ReadFull` that returns all available properties including sensitive information.

### Assume breach

The Microsoft identity platform application registration portal is the primary entry point for applications intending to use the platform for their authentication and associated needs. When registering and configuring applications, follow the practices described below to minimize the damage they could cause if there's a security breach. For more information, see [Microsoft Entra application registration security best practices](security-best-practices-for-app-registration).

Consider the following actions prevent breaches in security:

- Properly define the redirect URIs for the application. Don't use the same application registration for multiple applications.
- Verify redirect URIs used in the application registration for ownership and to avoid domain takeovers. Don't create the application as a multitenant unless it's intended to be.
- Make sure application and service principal owners are always defined and maintained for the applications registered in the tenant.