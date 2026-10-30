---
layout: Conceptual
title: External Tenant Features - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-supported-features-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Compare features and capabilities of a workforce versus an external tenant configuration. Determine which tenant type applies to your external identities scenario.
ms.topic: concept-article
ms.date: 2026-03-30T00:00:00.0000000Z
ms.custom: it-pro, seo-july-2024, sfi-ropc-nochange
locale: en-us
document_id: 2bb93356-67a7-32cd-fd3b-cdce20871675
document_version_independent_id: a5c1d845-10eb-c72e-4560-ff2206c4ee7e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-supported-features-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-supported-features-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-supported-features-customers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/54918a83-0404-4863-9c91-715186c1f582
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/b26f5f7a-0913-4a95-8337-ed7543902f2d
platformId: 82b38328-5842-5455-5bd3-9a2828bdaf81
---

# External Tenant Features - Microsoft Entra External ID | Microsoft Learn

There are two ways to configure a Microsoft Entra tenant, depending on how an organization intends to use the tenant and the resources that you want to manage:

- A *workforce* tenant configuration is for your employees, internal business apps, and other organizational resources. A workforce tenant uses B2B collaboration in Microsoft Entra External ID for collaboration with external business partners and guests.
- An *external* tenant configuration is exclusively for External ID scenarios where you want to publish apps to consumers or business customers.

This article gives a detailed comparison of the features and capabilities in workforce and external tenants. For more information about these tenants, see [Workforce and external tenant configurations in Microsoft Entra External ID](../tenant-configurations).

Note

During the preview, features or capabilities that require a premium license are unavailable in external tenants.

## General feature comparison

The following table compares the general features and capabilities in workforce and external tenants.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| External identities scenario | Allow business partners and other external users to collaborate with your workforce. Guests can securely access your business applications through invitations or self-service sign-up. | Use External ID to help secure your applications. Consumers and business customers can access your consumer apps through self-service sign-up. Invitations are also supported. |
| Local accounts | Local accounts are supported for *internal* members of your organization only. | Local accounts are supported for:<br>- Consumers and business customers who use self-service sign-up.<br>- Admin-created internal accounts (with or without an admin role).<br><br> All users in an external tenant have [default permissions](reference-user-permissions) unless they're [assigned an admin role](how-to-manage-admin-accounts). |
| Groups | Use [groups](/en-us/entra/fundamentals/how-to-manage-groups) to manage administrative and user accounts. | Use groups to manage administrative accounts. Support for Microsoft Entra groups and [application roles](how-to-use-app-roles-customers) is being phased into customer tenants. For the latest updates, see [Groups and application roles support](reference-group-app-roles-support). |
| Roles and administrators | [Roles and administrators](../../fundamentals/how-subscriptions-associated-directory) are fully supported for administrative and user accounts. | Roles are supported for all users. All users in an external tenant have [default permissions](reference-user-permissions) unless they're assigned an [admin role](how-to-manage-admin-accounts). |
| Microsoft Entra ID Protection | This product provides ongoing risk detection for your Microsoft Entra tenant. It allows organizations to discover, investigate, and remediate identity-based risks. | Not available. |
| Microsoft Entra ID Governance | This product enables organizations to govern identity and access lifecycles, along with secure privileged access. [Learn more](../../id-governance/identity-governance-overview). | Not available. |
| Self-service password reset | Allow users to reset their password by using up to two authentication methods. | Allow users to reset their password by using email with a one-time passcode or SMS. [Learn more](how-to-enable-password-reset-customers). |
| Language customization | Customize the sign-in experience based on browser language when users authenticate into your corporate intranet or web-based applications. | Use languages to modify the strings displayed to your customers as part of the sign-in and sign-up process. [Learn more](concept-branding-customers). |
| Custom attributes | Use directory extension attributes to store more data in the Microsoft Entra directory for user objects, groups, tenant details, and service principals. | Use directory extension attributes to store more data in the customer directory for user objects. Create custom user attributes and add them to your sign-up user flow. [Learn more](how-to-define-custom-attributes). |
| Pricing | Get [monthly active users (MAU) pricing](../external-identities-pricing) for external guests through B2B collaboration (`UserType=Guest`). | Get [MAU pricing](../external-identities-pricing) for all users in the external tenant regardless of role or `UserType` value. |

## Interface customization

The following table compares the features for interface customization in workforce and external tenants.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Company branding | You can add [company branding](../../fundamentals/how-to-customize-branding) that applies to all these experiences to create a consistent sign-in experience for your users. | Same as workforce. [Learn more](how-to-customize-branding-customers). |
| Language customization | [Customize the sign-in experience by browser language](../../fundamentals/how-to-customize-branding). | Same as workforce. [Learn more](how-to-customize-languages-customers). |
| Custom domain names | You can use [custom domains](../../fundamentals/add-custom-domain) for administrative accounts only. | You can use the [custom URL domain](concept-custom-url-domain) feature for external tenants to brand app sign-in endpoints with your own domain name. |
| Native authentication for mobile apps | Not available. | Microsoft Entra [native authentication](concept-native-authentication) gives you full control over the design of your mobile application's sign-in experiences. |

## Adding your own business logic

You can use [custom authentication extensions](concept-custom-extensions) to customize the Microsoft Entra authentication experience by integrating with external systems. A custom authentication extension is essentially an event listener. When you activate it, it makes an HTTP call to a REST API endpoint where you define your own business logic.

The following table compares the events for custom authentication extensions in workforce and external tenants.

| Event | Workforce tenant | External tenant |
| --- | --- | --- |
| `TokenIssuanceStart` | [Add claims from external systems](../../identity-platform/custom-extension-overview). | [Add claims from external systems](concept-custom-extensions). |
| `OnAttributeCollectionStart` | Not available. | This event occurs at the beginning of the sign-up's attribute collection step, before the attribute collection page renders. You can add actions such as prefilling values and displaying a blocking error. [Learn more](../../identity-platform/custom-extension-attribute-collection?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=start-continue,submit-continue). |
| `OnAttributeCollectionSubmit` | Not available. | This event occurs during the sign-up flow, after the user enters and submits attributes. You can add actions such as validating or modifying the user's entries. [Learn more](../../identity-platform/custom-extension-attribute-collection?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=start-continue,submit-continue). |
| `OnOtpSend` | Not available. | Configure a custom email provider for one-time passcode send events. [Learn more](../../identity-platform/custom-extension-email-otp-get-started?toc=/entra/external-id/toc.json&amp;bc=/entra/external-id/breadcrumb/toc.json&amp;tabs=azure-communication-services,azure-portal). |

## Identity providers and authentication methods

The following table compares the [identity providers](../identity-providers) and methods for primary authentication and multifactor authentication (MFA) in workforce and external tenants.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Identity providers for external users (primary authentication) | For self-service sign-up guests:<br>- Microsoft Entra accounts<br>- Microsoft accounts<br>- Emailed one-time passcode<br>- Google federation<br>- Facebook federation<br><br>For invited guests:<br>- Microsoft Entra accounts<br>- Microsoft accounts<br>- Emailed one-time passcode<br>- Google federation<br>- SAML/WS-Fed federation | For self-service sign-up users (consumers, business customers):<br>- Authentication methods available in External ID<br><br>For invited guests (preview) via a directory role (for example, admins):<br>- Microsoft Entra accounts<br>- Microsoft accounts<br>- [Emailed one-time passcode](concept-authentication-methods-customers#email-with-one-time-passcode-sign-in)<br>- [SAML/WS-Fed federation](../direct-federation)<br><br> You can invite external users for administrative purposes only. You can't use this feature to invite customers to sign in to your apps. This feature isn't compatible with customer identity and access management (CIAM) user flows. |
| Authentication methods for MFA | For internal users (employees and admins):<br>- [Authentication and verification methods](../../identity/authentication/overview-authentication)<br><br>For guests (invited or self-service sign-up):<br>- [Authentication methods for guest MFA](../authentication-conditional-access#table-1-authentication-strength-mfa-methods-for-external-users) | For self-service sign-up users (consumers, business customers):<br>- [Emailed one-time passcode](concept-multifactor-authentication-customers#email-one-time-passcode)<br>- [SMS-based authentication](concept-multifactor-authentication-customers#sms-based-authentication)<br>- [Passkey (FIDO2)](how-to-sign-in-with-passkey)<br><br>For invited users (preview):<br>- [Emailed one-time passcode](concept-multifactor-authentication-customers#email-one-time-passcode)<br>- [SMS-based authentication](concept-multifactor-authentication-customers#sms-based-authentication) |

### Authentication methods available in External ID

You can use some authentication methods as the primary factor when users sign in to an application, such username and password. Other authentication methods are available only as a secondary factor. The following table outlines when you can use an authentication method during sign-in, self-service sign-up, self-service password reset, and MFA in External ID.

| Method | Sign-in | Sign-up | Password reset | MFA |
| --- | --- | --- | --- | --- |
| [Email with password](concept-authentication-methods-customers#email-and-password-sign-in) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |
| [Email one-time passcode](concept-authentication-methods-customers#email-with-one-time-passcode-sign-in) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |
| [SMS-based authentication](concept-multifactor-authentication-customers#sms-based-authentication) |  |  |  | ![](../media/common/applies-to-yes.png) |
| [Passkey (FIDO2)](how-to-sign-in-with-passkey) | ![](../media/common/applies-to-yes.png) |  |  | ![](../media/common/applies-to-yes.png) |
| [Apple federation](how-to-apple-federation-customers) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |
| [Facebook federation](how-to-facebook-federation-customers) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |
| [Google federation](how-to-google-federation-customers) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |
| Microsoft personal account ([OpenID Connect](how-to-custom-oidc-federation-customers)) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |
| [Microsoft Entra ID federation](how-to-entra-id-federation-customers) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |
| [OpenID Connect federation](how-to-custom-oidc-federation-customers) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |
| [SAML/WS-Fed federation](../direct-federation) | ![](../media/common/applies-to-yes.png) | ![](../media/common/applies-to-yes.png) |  |  |

## Application registration

The following table compares the features for [application registration](../../identity-platform/quickstart-register-app) in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Protocol | Protocols include SAML relying parties, OpenID Connect, and OAuth2. | Protocols include [SAML relying parties](how-to-register-saml-app), [OpenID Connect](how-to-register-ciam-app), and OAuth2. |
| Supported account types | The following [account types](../../identity-platform/quickstart-register-app#register-an-application) are available: <br>- Accounts in this organizational directory only (single tenant)<br>- Accounts in any organizational directory (any Microsoft Entra tenant in a multitenant configuration)<br>- Accounts in any organizational directory (any Microsoft Entra tenant in a multitenant configuration) and personal Microsoft accounts (such as Skype and Xbox)<br>- Personal Microsoft accounts only | Always use accounts in this organizational directory only (single tenant). |
| Platform | The following [platforms](../../identity-platform/how-to-add-redirect-uri) are available: <br>- Public client/native (mobile and desktop)<br>- Web<br>- Single-page application (SPA) | The following [platforms](../../identity-platform/how-to-add-redirect-uri) are available: <br>- Public client (mobile and desktop)<br>- Web<br>- SPA<br>- Native authentication for [mobile](concept-native-authentication) and [single-page](how-to-native-authentication-cors-solution-production-environment) applications |
| Redirect URIs for authentication | Microsoft Entra ID accepts these URIs as destinations when it returns authentication responses (tokens) after successfully authenticating or signing out users. | Same as workforce. |
| Front-channel logout URL for authentication | This URL is where Microsoft Entra ID sends a request to have the application clear the user's session data. The front-channel logout URL is required for single sign-out to work correctly. | Same as workforce. |
| Implicit grant and hybrid flows for authentication | Request a token directly from the authorization endpoint. | Same as workforce. |
| Certificates and secrets | Multiple credentials are available: <br>- [Certificates](../../identity-platform/how-to-add-credentials?tabs=certificate)<br>- [Client secrets](../../identity-platform/how-to-add-credentials?tabs=client-secret)<br>- [Federated credentials](../../identity-platform/how-to-add-credentials?tabs=federated-credential) | Same as workforce. |
| Rotation for certificates and secrets | Update client credentials to help ensure that they remain valid and secure, while users can continue to sign-in. You can rotate [certificates](../../identity-platform/how-to-add-credentials?tabs=certificate), [secrets](../../identity-platform/how-to-add-credentials?tabs=client-secret), and [federated credentials](../../identity-platform/how-to-add-credentials?tabs=federated-credential) by adding a new one and then removing the old one. | Same as workforce. |
| Policy for certificates and secrets | Configure the [application management policies](../../identity/enterprise-apps/tutorial-enforce-secret-standards) to enforce secret and certificate restrictions. | Not available. |
| API permissions | Add, remove, and replace permissions to an application. After permissions are added to your application, users or admins need to grant consent to the new permissions. [Learn more about updating an app's requested permissions in Microsoft Entra ID](../../identity-platform/howto-update-permissions). | The following permissions are allowed: Microsoft Graph `offline_access`, `openid`, and `User.Read`, along with your **My APIs** delegated permissions. Only an admin can consent on behalf of the organization. |
| Expose an API | [Define custom scopes](../../identity-platform/quickstart-configure-app-expose-web-apis) to restrict access to data and functionality that the API helps protect. An application that requires access to parts of this API can request user or admin consent to one or more of these scopes. | Same as workforce. |
| Owners | Application owners can view and edit the application registration. Additionally, any user (who might not be listed) with administrative privileges to manage any application (for example, [Cloud Application Administrator](../../identity/role-based-access-control/permissions-reference#cloud-application-administrator)) can view and edit the application registration. | Same as workforce. |
| Roles and administrators | [Administrative roles](../../identity/role-based-access-control/permissions-reference) are used for granting access for privileged actions in Microsoft Entra ID. | Only the [Cloud Application Administrator](../../identity/role-based-access-control/permissions-reference#cloud-application-administrator) role can be used for apps in external tenants. This role grants the ability to create and manage all aspects of application registrations and enterprise applications. |

### Access control for applications

The following table compares the features for application authorization in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Role-based access control (RBAC) | You can define [application roles](../../identity-platform/custom-rbac-for-developers#app-roles) for your application and assign those roles to users and groups. Microsoft Entra ID includes the user roles in the security token. Your application can then make authorization decisions based on the values in the security token. | Same as workforce. [Learn more about using role-based access control for applications in an external tenant](how-to-use-app-roles-customers). For available features, see [Groups and application roles support](reference-group-app-roles-support). |
| Security groups | You can use [security groups](../../identity-platform/custom-rbac-for-developers#groups) to implement RBAC in your applications, where the memberships of users in specific groups are interpreted as their role memberships. Microsoft Entra ID includes user group membership in the security token. Your application can then make authorization decisions based on the values in the security token. | Same as workforce. The [group optional claims](../../identity-platform/optional-claims#configure-groups-optional-claims) are limited to the group object ID. |
| Attribute-based access control (ABAC) | You can configure the app to include user attributes in the access token. Your application can then make authorization decisions based on the values in the security token. For more information, see Token customization. | Same as workforce. |
| Require user assignment | When user assignment is required, only the users you assign to the application (either through direct user assignment or based on group membership) can sign in. For more information, see [Manage user and group assignments to an application](../../identity-platform/howto-restrict-your-app-to-a-set-of-users). | Same as workforce. For details, see [Groups and application roles support](reference-group-app-roles-support). |

## Enterprise applications

The following table compares the unique features for [enterprise application](/en-us/entra/identity/enterprise-apps/) registration in workforce and external tenants.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Application gallery | The [application gallery](/en-us/entra/identity/enterprise-apps/overview-application-gallery) contains thousands of applications that are integrated into Microsoft Entra ID. | Choose from a range of integrated apps. To find a partner app, use the search bar. The application gallery catalog isn't available. |
| Register a custom enterprise application | [Add an enterprise application.](/en-us/entra/identity/enterprise-apps/add-application-portal) | [Register a SAML app in your external tenant.](/en-us/entra/external-id/customers/how-to-register-saml-app) |
| Self-service application assignment | Let users [self-discover apps](/en-us/entra/identity/enterprise-apps/manage-self-service-access). | Self-service application assignment in the [My Apps portal](/en-us/entra/identity/enterprise-apps/myapps-overview) isn't available. |
| Application proxy | [Microsoft Entra application proxy](/en-us/entra/identity/app-proxy/overview-what-is-app-proxy) provides secure remote access to on-premises web applications. | Not available. |
| Deactivate app registration | [Deactivate an app registration](/en-us/entra/identity/enterprise-apps/deactivate-app-registration) to prevent token issuance while preserving configuration. | Same as workforce. |

### Consent and permission features for enterprise applications

The following table shows which consent and permission features are available for enterprise applications in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Admin consent for enterprise applications | You can [grant tenant-wide admin permissions](/en-us/entra/identity/enterprise-apps/grant-admin-consent). You can also [review and revoke](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=portal) them. | Same as workforce. |
| User consent for enterprise applications | You can configure how [users consent to applications](/en-us/entra/identity/enterprise-apps/configure-user-consent), and you can [update these permissions](/en-us/entra/identity-platform/howto-update-permissions). | Limited to permissions that don't require [admin consent](/en-us/entra/identity/enterprise-apps/grant-admin-consent). |
| Review or revoke admin consent | [Review and revoke](/en-us/entra/identity/enterprise-apps/manage-application-permissions) permissions. | [Use the Microsoft Entra admin center](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=portal) to revoke admin consent. |
| Review or revoke user consent | [Review and revoke](/en-us/entra/identity/enterprise-apps/manage-application-permissions) permissions. | Use [Microsoft Graph API](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=ms-graph) or [PowerShell](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=entra-powershell) to revoke user consent. |
| Assign users or groups to apps | You can [manage access to apps](/en-us/entra/identity/enterprise-apps/what-is-access-management) in an individual or group-based assignment. [Nested group](/en-us/entra/fundamentals/how-to-manage-groups) memberships aren't supported. | Same as workforce. |
| RBAC for app roles | You can define and assign roles for fine-grained [access control](/en-us/entra/external-id/customers/how-to-use-app-roles-customers). | Same as workforce. |

## OpenID Connect and OAuth2 flows

The following table compares the features for OAuth 2.0 and OpenID Connect authorization flows in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| [OpenID Connect](../../identity-platform/v2-protocols-oidc) | Yes | Yes |
| [Authorization code](../../identity-platform/v2-oauth2-auth-code-flow) | Yes | Yes |
| [Authorization code with Proof Key for Code Exchange (PKCE)](../../identity-platform/v2-oauth2-auth-code-flow) | Yes | Yes |
| [Client credentials](../../identity-platform/v2-oauth2-client-creds-grant-flow) | Yes | [v2.0 applications](../../identity-platform/reference-app-manifest) |
| [Device authorization](../../identity-platform/v2-oauth2-device-code) | Yes | Yes |
| [On-behalf-of flow](../../identity-platform/v2-oauth2-on-behalf-of-flow) | Yes | Yes |
| [Implicit grant](../../identity-platform/v2-oauth2-implicit-grant-flow) | Yes | Yes |
| [Resource owner password credentials](../../identity-platform/v2-oauth-ropc) | Yes | No; for mobile applications, use [native authentication](concept-native-authentication) |

### Authority URL in OpenID Connect and OAuth2 flows

The authority URL indicates a directory that the Microsoft Authentication Library (MSAL) can request tokens from. For apps in external tenants, always use the following format: `<tenant-name>.ciamlogin.com`.

The following JSON shows an example of a .NET application `appsettings.json` file with an authority URL:

```json
{
    "AzureAd": {
        "Authority": "https://<Enter_the_Tenant_Subdomain_Here>.ciamlogin.com/",
        "ClientId": "<Enter_the_Application_Id_Here>"
    }
}
```

## Conditional Access

The following table compares the features for Microsoft Entra Conditional Access in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Assignments | [Users, groups](../../identity/conditional-access/concept-conditional-access-users-groups), and [workload identities](../../identity/conditional-access/concept-conditional-access-users-groups#workload-identities). | Include all users, and exclude users and groups. For more information, see [Add multifactor authentication (MFA) to an app](how-to-multifactor-authentication-customers). |
| Target resources | - [Cloud apps](../../identity/conditional-access/concept-conditional-access-cloud-apps)<br>- [User actions](../../identity/conditional-access/concept-conditional-access-cloud-apps#user-actions)<br>- [Global Secure Access](../../identity/conditional-access/concept-conditional-access-cloud-apps#traffic-forwarding-profiles)<br>- [Authentication context](../../identity/conditional-access/concept-conditional-access-cloud-apps#authentication-context) | - [All resources, selected apps](how-to-multifactor-authentication-customers), or [filter applications](../../identity/conditional-access/concept-filter-for-applications)<br>- [Authentication context](../../identity/conditional-access/concept-conditional-access-cloud-apps#authentication-context) |
| Conditions | - [Sign-in risk](../../identity/conditional-access/concept-conditional-access-conditions#sign-in-risk)<br>- [User risk](../../identity/conditional-access/concept-conditional-access-conditions#user-risk)<br>- [Device platforms](../../identity/conditional-access/concept-conditional-access-conditions#device-platforms)<br>- [Locations](../../identity/conditional-access/concept-conditional-access-conditions#locations)<br>- [Client apps](../../identity/conditional-access/concept-conditional-access-conditions#client-apps)<br>- [Filter for devices](../../identity/conditional-access/concept-conditional-access-conditions#filter-for-devices) | - [Device platforms](../../identity/conditional-access/concept-conditional-access-conditions#device-platforms)<br>- [Locations](../../identity/conditional-access/concept-conditional-access-conditions#locations) |
| Grant | [Grant or block access to resources](../../identity/conditional-access/concept-conditional-access-grant) | - [Block access](../../identity/conditional-access/concept-conditional-access-grant#block-access)<br>- [Require multifactor authentication](how-to-multifactor-authentication-customers)<br>- [Require password reset](how-to-enable-password-reset-customers) |
| Session | [Session controls](../../identity/conditional-access/concept-conditional-access-session) | The following session controls are available: <br>- Sign-in frequency<br>- Persistent browser session |

## Terms-of-use policies

The following table compares the features for terms-of-use policies in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Conditional Access policies | See the [Microsoft Entra terms of use](../../identity/conditional-access/terms-of-use). | Not available. |
| Self-service sign-up | Not available. | Add a [required attribute](how-to-define-custom-attributes#configure-a-single-select-checkbox-checkboxsingleselect) linked to your terms-of-use policies on the sign-up page. You can customize the hyperlink to support various languages. |
| Sign-in page | You can add links to the lower-right corner for privacy information by using [company branding](../../fundamentals/how-to-customize-branding). | [Same as workforce](how-to-customize-branding-customers#to-customize-the-logo-privacy-link-and-terms-of-use). |

## Account management

The following table compares the features for user management in each type of tenant. As noted in the table, certain account types are created through invitation or self-service sign-up. A user admin in the tenant can also create accounts via the admin center.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Types of accounts | - Internal members, such as employees and admins.<br>- External users who are [invited](../what-is-b2b) or use self-service sign-up. | - External users created through self-service sign-up or [by an admin](how-to-manage-customer-accounts).<br>- Internal users, with or without an admin role.<br>- Invited users (preview), with or without an admin role.<br><br> All users in an external tenant have [default permissions](reference-user-permissions) unless they're assigned an [admin role](how-to-manage-admin-accounts). |
| Manage user profile info | - Manage users programmatically and by [using the admin center](../../fundamentals/how-to-manage-user-profile-info).<br>- Manage guest users across tenants with [cross-tenant synchronization](/en-us/entra/identity/multi-tenant-organizations/cross-tenant-synchronization-overview). | Same as workforce, except cross-tenant synchronization isn't available. |
| Reset a user's password | Administrators can [reset a user's password](../../fundamentals/users-reset-password-azure-portal) if the user forgets the password, is locked out of a device, or never received a password. | Same as workforce. |
| Restore or remove a recently deleted user | After you delete a user, the account remains in a suspended state for 30 days. During that 30-day window, the user account can be restored, along with all its properties. | Same as workforce. |
| Disable accounts | Prevent the new user from signing in. | Same as workforce. |

## Password protection

The following table compares the features for password protection in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Smart lockout | [Smart lockout](../../identity/authentication/howto-password-smart-lockout) helps lock out bad actors who try to guess your users' passwords or use brute-force methods to get in. | Same as workforce. |
| Global banned passwords | The [global banned passwords list](../../identity/authentication/concept-password-ban-bad#global-banned-password-list) automatically blocks commonly used weak or compromised passwords based on analysis of Microsoft Entra security data. | Same as workforce. |
| Custom banned passwords | Use the [custom banned passwords list](../../identity/authentication/tutorial-configure-custom-password-protection) to add specific strings to evaluate and block during password creation and reset. | Same as workforce. |

## Token customization

The following table compares the features for token customization in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Claims mapping | [Customize claims](../../identity-platform/jwt-claims-customization) issued in the JSON web token (JWT) for enterprise applications. | Same as workforce. Optional claims must be configured through [Attributes & Claims](how-to-add-attributes-to-token). |
| Claims transformation | [Apply a transformation to a user attribute](../../identity-platform/jwt-claims-customization) issued in the JWT for enterprise applications. | Same as workforce. |
| Custom claims provider | Use a [custom authentication extension](../../identity-platform/custom-extension-overview) that calls an external REST API to fetch claims from external systems. | Same as workforce. [Learn more](../../identity-platform/custom-claims-provider-overview). |
| Security groups | [Configure group optional claims](../../identity-platform/optional-claims#configure-groups-optional-claims). | [Configure group optional claims](../../identity-platform/optional-claims#configure-groups-optional-claims), limited to the group object ID. |
| Token lifetimes | [Specify the lifetime](../../identity-platform/configurable-token-lifetimes) of security tokens issued by Microsoft Entra ID. | Same as workforce. |
| Session and token revocation | An administrator can [invalidate all the refresh tokens and session](/en-us/graph/api/user-revokesigninsessions) for a user. | Same as workforce. |

## Single sign-on

[Single sign-on (SSO)](../../identity-platform/msal-js-sso) provides a more seamless experience by reducing the number of times a user is asked for credentials. Users enter their credentials once. Other applications can reuse the established session on the same device and web browser without further prompting.

The following table compares the features for SSO in each type of tenant.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Types of application registration | - OpenID Connect<br>- OAuth 2.0<br>- SAML (enterprise application)<br><br>Enterprise applications offer [more options](../../identity/enterprise-apps/plan-sso-deployment), like password-based, linked, and header-based registration. | - OpenID Connect<br>- OAuth 2.0<br>- SAML (enterprise application) |
| Domain name | When a user is authenticated, a session cookie is set on the Microsoft Entra domain `login.microsoftonline.com` in the web browser. | When a user is authenticated, a session cookie is set on the Microsoft Entra External ID domain `<tenant-name>.ciamlogin.com` or a [custom URL domain](concept-custom-url-domain) in the web browser. To ensure that SSO functions correctly, use a single URL domain. |
| Stay signed in | You can turn on or turn off the option to [stay signed in](../../fundamentals/how-to-manage-stay-signed-in-prompt). | The **Stay signed in?** prompt appears by default. To change or suppress it, use the **Persistent browser session** session control in a Conditional Access policy. [Learn more](how-to-user-flow-sign-up-sign-in-customers#control-the-stay-signed-in-prompt). |
| User provisioning | Use [automatic user provisioning](/en-us/entra/architecture/sync-scim) with System for Cross-domain Identity Management (SCIM) to sync user accounts between External ID and supported apps. This approach keeps user data up to date automatically. User provisioning supports differential queries. These queries sync only the changes since the last update. This behavior improves performance and reduces system load. | Same as workforce. |
| Session invalidation | Scenarios where SSO might be invalidated, which requires reauthentication: <br>- Session expiry<br>- Browser issues, such as clearing browser cookies or cache<br>- Conditional Access policy, such as a multifactor authentication requirement<br>- [Session revocation](/en-us/graph/api/user-revokesigninsessions)<br>- Security issues, such as suspicious activity<br><br>The application specifies in the authorization request to prompt the user for credentials by using the `login=prompt` query string parameter in OpenID Connect and the `ForceAuthn` attribute in the SAML request. | Same as workforce. |
| Conditional Access | Check the Conditional Access section. | Check the Conditional Access section. |
| Microsoft Entra native authentication | Not available. | [Native authentication](concept-native-authentication) supports SSO for embedded web views. Cross-app SSO through system browsers isn't available with native authentication. |
| Sign-out | When a [SAML](../../identity-platform/single-sign-out-saml-protocol) or [OpenID Connect](../../identity-platform/v2-protocols-oidc#send-a-sign-out-request) application directs the user to the logout endpoint, Microsoft Entra ID removes and invalidates the user's session from the browser. | Same as workforce. |
| Single sign-out | Upon successful sign-out, Microsoft Entra ID sends a sign-out notification to all other [SAML](../../identity-platform/single-sign-out-saml-protocol) and [OpenID Connect](../../identity-platform/v2-protocols-oidc#single-sign-out) applications that the user is signed in to. | Same as workforce. |

## Integrated security solutions

Microsoft Entra External ID supports integrated security features and partner solutions to help protect identities across the lifecycle. These capabilities include protection against distributed denial-of-service (DDoS) attacks, prevention of sign-up fraud, and unified monitoring.

You can enable these solutions directly in External ID and access partner integrations through the [Microsoft Security Store](https://securitystore.microsoft.com/). This approach allows organizations to deploy trusted security tools quickly without complex setup.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| Sign-up fraud protection | The Security Store wizard experience isn't available. | Use [Arkose Labs](/en-us/entra/external-id/customers/how-to-integrate-fraud-protection?pivots=arkose) and [HUMAN Security](/en-us/entra/external-id/customers/how-to-integrate-fraud-protection?pivots=human) to help protect against sign-up fraud and block automated bot attacks. |
| DDoS and web application firewall (WAF) protection | The Security Store wizard experience isn't available. | Use [Cloudflare](/en-us/entra/external-id/customers/how-to-configure-waf-integration) and [Akamai](/en-us/entra/external-id/customers/how-to-configure-akamai-integration) to help protect against DDoS attacks and secure apps with a WAF. |
| Security analytics | The Security Store wizard experience isn't available. | Use [Azure Monitor and Microsoft Sentinel](/en-us/entra/external-id/customers/how-to-azure-monitor) to enable one-click monitoring, Log Analytics, and advanced threat detection. |

### Akamai and Cloudflare

[Akamai](/en-us/entra/external-id/customers/how-to-configure-akamai-integration) and [Cloudflare](/en-us/entra/external-id/customers/how-to-configure-waf-integration) provide DDoS protection, bot mitigation, and WAF capabilities. These capabilities help defend applications against malicious traffic, abusive automation, and common web vulnerabilities such as SQL injection, cross‑site scripting, and API‑based attacks.

When you integrate either service with External ID, you can apply these security controls in front of your customer-facing identity flows. This action improves resilience and reduces exposure to credential stuffing and other identity‑targeted threats.

## Activity logs and reports

The following table compares the features for activity logs and reports across various types of tenants.

| Feature | Workforce tenant | External tenant |
| --- | --- | --- |
| [Audit logs](../../identity/monitoring-health/concept-audit-logs) | These logs provide a detailed report of all events logged in Microsoft Entra ID, including modifications to applications, groups, and users. | Same as workforce. |
| [Sign-in logs](../../identity/monitoring-health/concept-sign-ins) | The sign-in logs track all sign-in activities within a Microsoft Entra tenant, including access to your applications and resources. | Same as workforce. |
| [Sign-up logs](../../identity/monitoring-health/concept-sign-ups) (preview) | Not available. | Microsoft Entra External ID logs all self-service sign-up events, including both successful sign-ups and failed attempts. |
| [Provisioning logs](../../identity/monitoring-health/concept-provisioning-logs) | The provisioning logs provide detailed records of provisioning events within a tenant, such as user account creations, updates, and deletions. | Not available. |
| [Activity logs for retention policies](../../identity/monitoring-health/concept-provisioning-logs) | Microsoft Entra data retention policies determine how long various types of logs (like audit, sign-in, and provisioning logs) are stored. | Seven days. |
| [Export activity logs](../../identity/monitoring-health/howto-configure-diagnostic-settings) | By using diagnostic settings in Microsoft Entra ID, you can integrate logs with Azure Monitor, stream logs to an event hub, or integrate with security information and event management (SIEM) tools. | [Azure Monitor for external tenants (preview)](how-to-azure-monitor). |
| [Reports for application user activity](how-to-user-insights) (retiring August 31, 2026; see [migration guidance](how-to-user-insights#migrate-from-user-insights)) | Not available. | Application user activity provides analytics on how users interact with registered applications in your tenant. It tracks metrics like active users, new users, sign-ins, and MFA success rates. |

## Microsoft Graph APIs

All features that are supported in external tenants are also supported for automation through Microsoft Graph APIs. Some features that are in preview in external tenants might be generally available through Microsoft Graph. For more information, see [Manage Microsoft Entra identity and network access by using Microsoft Graph](/en-us/graph/api/resources/identity-network-access-overview).