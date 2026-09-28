---
layout: Conceptual
title: How to integrate with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/how-to-integrate
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn the benefits of integrating your application with the Microsoft identity platform, and get resources for features like simplified sign-in, identity management, multifactor authentication, and access control.
ROBOTS: NOINDEX
manager: pmwongera
ms.date: 2024-11-06T00:00:00.0000000Z
ms.reviewer: jmprieur
ms.topic: concept-article
locale: en-us
document_id: d88d9a08-48b2-6cd6-51ec-46190ab2b6dd
document_version_independent_id: 461f8df8-e23a-11bf-84c7-5dfb3adada9c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/how-to-integrate.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/how-to-integrate
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/how-to-integrate.md
platformId: 411ca1ec-3c1c-4f7a-d6f3-29eebaa7f769
---

# How to integrate with the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

Note

This article is part of the [Microsoft identity platform (Azure Active Directory for developers) documentation](./).

In this article, you learn about the benefits of integrating your application with the Microsoft identity platform and get resources for integration. Microsoft identity platform and Microsoft Entra ID provide organizations with enterprise-grade identity management for cloud applications. The Microsoft identity platform integration gives your users a streamlined sign-in experience, and helps your application conform to IT policy.

## How to integrate

There are several ways for your application to integrate with the Microsoft identity platform. Take advantage of as many or as few of these scenarios as is appropriate for your application.

### Support the Microsoft identity platform as a way to sign in to your application

**Reduce sign in friction and reduce support costs.** By using the Microsoft identity platform to sign in to your application, your users won't have one more name and password to remember. As a developer, you'll have one less password to store and protect. Not having to handle forgotten password resets may be a significant savings alone. The Microsoft identity platform powers sign in for some of the world's most popular cloud applications, including Microsoft 365 and Microsoft Azure. With hundreds of millions users from millions of organizations, chances are your user is already signed in to the Microsoft identity platform. Learn more about [adding support for the Microsoft identity platform sign in](authentication-vs-authorization).

**Simplify sign up for your application.** During sign-up for your application, the Microsoft identity platform can send essential information about a user so that you can prefill your sign-up form or eliminate it completely. Users can sign up for your application using their Microsoft Entra account via a familiar consent experience similar to those found in social media and mobile applications. Any user can sign up and sign in to an application that is integrated with the Microsoft identity platform without requiring IT involvement. Learn more about [signing-up your application for Microsoft Entra account login](/en-us/azure/app-service/configure-authentication-provider-aad).

### Browse for users, manage user provisioning, and control access to your application

**Browse for users in the directory.** Use the Microsoft Graph API to help users search and browse for other people in their organization when inviting others or granting access, instead of requiring them to type email addresses. Users can browse using a familiar address book style interface, including viewing the details of the organizational hierarchy. Learn more about the [Microsoft Graph API](/en-us/graph/overview).

**Re-use Active Directory groups and distribution lists your customer is already managing.** Microsoft Entra ID contains the groups that your customer is already using for email distribution and managing access. Using the Microsoft Graph API, reuse these groups instead of requiring your customer to create and manage a separate set of groups in your application. Group information can also be sent to your application in sign in tokens. Learn more about the [Microsoft Graph API](/en-us/graph/overview).

**Use the Microsoft identity platform to control who has access to your application.** Administrators and application owners in Microsoft Entra ID can assign access to applications to specific users and groups. Using the Microsoft Graph API, you can read this list and use it to control provisioning and deprovisioning of resources and access within your application.

**Use the Microsoft identity platform for Roles Based Access Control.** Administrators and application owners can assign users and groups to roles that you define when you register your application in Microsoft identity platform. Role information is sent to your application in sign in tokens and can also be read using the Microsoft Graph API. Learn more about how to [implement role-based access control in your application](howto-implement-rbac-for-apps).

### Get access to users' profile, calendar, email, contacts, files, and more

**The Microsoft identity platform is the authorization server for Microsoft 365 and other Microsoft business services.** If you support the Microsoft identity platform for sign in to your application or support linking your current user accounts to Microsoft Entra user accounts using OAuth 2.0, you can request read and write access to a user's profile, calendar, email, contacts, files, and other information. You can seamlessly write events to user's calendar, and read or write files to their OneDrive. Learn more about [the Microsoft 365 APIs](/en-us/graph/overview).

### Promote your application in the Azure and Microsoft 365 Marketplaces

**Promote your application to the millions of organizations who are already using Microsoft Entra ID.** Users who search and browse these marketplaces are already using one or more cloud services, making them qualified cloud service customers. Learn more about promoting your application in [the Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).

**When users sign up for your application, it will appear in their Microsoft Entra ID access panel and Microsoft 365 app launcher.** Users are able to quickly and easily return to your application later, improving user engagement. Learn more about the [Microsoft Entra ID access panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

### Secure device-to-service and service-to-service communication

**Using the Microsoft identity platform for identity management of services and devices reduces the code you need to write and enables IT to manage access.** Services and devices can get tokens from the Microsoft identity platform using OAuth and use those tokens to access web APIs. Using the Microsoft identity platform you can avoid writing complex authentication code. Since the identities of the services and devices are stored in Microsoft Entra ID, IT can manage keys and revocation in one place instead of having to do this separately in your application.

## Benefits of integration

Integration with the Microsoft identity platform comes with benefits that don#t require you to write extra code.

### Integration with enterprise identity management

**Help your application comply with IT policies.** Organizations integrate their enterprise identity management systems with Microsoft identity platform, so when a person leaves an organization, they'll automatically lose access to your application without IT needing to take extra steps. IT can manage who can access your application and determine what access policies are required - for example multifactor authentication - reducing your need to write code to comply with complex corporate policies. Microsoft Entra ID provides administrators with a detailed audit log of who signed in to your application so IT can track usage.

**Microsoft Entra ID extends Active Directory to the cloud so that your application can integrate with AD.** Many organizations around the world use Active Directory as their principal sign-in and identity management system, and require their applications to work with AD. Integrating with Microsoft Entra ID integrates your app with Active Directory.

### Advanced security features

**Multi-factor authentication.** The Microsoft identity platform provides native multifactor authentication. IT administrators can require multifactor authentication to access your application, so that you don't have to code this support yourself. Learn more about [Multifactor Authentication](../identity/authentication/).

**Anomalous sign in detection.** The Microsoft identity platform processes more than a billion sign-ins a day, while using machine learning algorithms to detect suspicious activity and notify IT administrators of possible problems. By supporting the Microsoft identity platform sign-in, your application gets the benefit of this protection. Learn more about [viewing Microsoft Entra reports](../identity/monitoring-health/overview-monitoring-health).

**Conditional Access.** In addition to multifactor authentication, administrators can require specific conditions be met before users can sign-in to your application. Conditions that can be set include the IP address range of client devices, membership in specified groups, and the state of the device being used for access. Learn more about [Microsoft Entra Conditional Access](../identity/conditional-access/overview).

### Easy development

**Industry standard protocols.** Microsoft is committed to supporting industry standards. The Microsoft identity platform supports the industry-standard OAuth 2.0 and OpenID Connect 1.0 protocols. Learn more about the [Microsoft identity platform authentication protocols](v2-protocols).

**Open source libraries.** Microsoft provides fully supported open source libraries for popular languages and platforms to speed development. The source code is licensed under Apache 2.0, and you're free to fork and contribute back to the projects. Learn more about the [Microsoft Authentication Library (MSAL)](reference-v2-libraries).

### Worldwide presence and high availability

**Microsoft Entra ID is deployed in datacenters around the world and is managed and monitored around the clock.** Microsoft Entra ID is the identity management system for Microsoft Azure and Microsoft 365 and is deployed in 28 datacenters around the world. Directory data is guaranteed to be replicated to at least three datacenters. Global load balancers ensure users access the closest copy of Microsoft Entra ID containing their data, and automatically re-route requests to other datacenters if a problem is detected.