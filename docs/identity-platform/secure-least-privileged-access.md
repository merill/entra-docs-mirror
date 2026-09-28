---
layout: Conceptual
title: Increase application security with the principle of least privilege - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/secure-least-privileged-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how the principle of least privilege can help increase the security of an application and its data.
manager: pmwongera
ms.custom: 
ms.date: 2023-01-06T00:00:00.0000000Z
ms.reviewer: 
ms.topic: concept-article
locale: en-us
document_id: 7cf9f309-75d1-c364-b400-1ab4135226c8
document_version_independent_id: 83e7ed48-d96b-f8c0-e771-a2567446c01a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/secure-least-privileged-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/secure-least-privileged-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/secure-least-privileged-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 34496205-e6ee-1cae-d82b-6ebdd0099117
---

# Increase application security with the principle of least privilege - Microsoft identity platform | Microsoft Learn

The information security principle of least privilege asserts that users and applications should be granted access only to the data and operations they require to perform their jobs. Follow the guidance here to help reduce the attack surface of an application and the impact of a security breach (the *blast radius*) should one occur in a Microsoft identity platform-integrated application.

## Recommendations at a glance

- Prevent **overprivileged** applications by revoking *unused* and *reducible* permissions.
- Use the identity platform's **consent** framework to require that a human consent to the request from the application to access protected data.
- **Build** applications with least privilege in mind during all stages of development.
- **Audit** the deployed applications periodically to identify the ones that are overprivileged.

## Overprivileged applications

Any application that's been granted an **unused** or **reducible** permission is considered overprivileged. Unused and reducible permissions have the potential to provide unauthorized or unintended access to data or operations not required by the application or its users to perform their jobs. Avoid security risks posed by unused and reducible permissions by granting only the appropriate permissions. The appropriate permissions are the ones with the least-permissive access required by an application or user to perform their required tasks.

### Unused permissions

An unused permission is a permission that's been granted to an application but whose API or operation exposed by that permission isn't called by the application when used as intended.

- **Example**: An application displays a list of files stored in the signed-in user's OneDrive by calling the Microsoft Graph API using the [Files.Read](/en-us/graph/permissions-reference) permission. However, the application has also been granted the [Calendars.Read](/en-us/graph/permissions-reference#calendars-permissions) permission, yet it provides no calendar features and doesn't call the Calendars API.
- **Security risk**: Unused permissions pose a *horizontal privilege escalation* security risk. An entity that exploits a security vulnerability in the application could use an unused permission to gain access to an API or operation not normally supported or allowed by the application when it's used as intended.
- **Mitigation**: Remove any permission that isn't used in API calls made by the application.

### Reducible permissions

A reducible permission is a permission that has a lower-privileged counterpart that would still provide the application and its users the access they need to perform their required tasks.

- **Example**: An application displays the signed-in user's profile information by calling the Microsoft Graph API, but doesn't support profile editing. However, the application has been granted the [User.ReadWrite.All](/en-us/graph/permissions-reference#user-permissions) permission. The *User.ReadWrite.All* permission is considered reducible here because the less permissive *User.Read.All* permission grants sufficient read-only access to user profile data.
- **Security risk**: Reducible permissions pose a *vertical privilege escalation* security risk. An entity that exploits a security vulnerability in the application could use the reducible permission for unauthorized access to data or to perform operations not normally allowed by that role of the entity.
- **Mitigation**: Replace each reducible permission in the application with its least-permissive counterpart still enabling the intended functionality of the application.

## Use consent to control access to data

Most applications require access to protected data, and the owner of that data needs to [consent](consent-types-developer) to that access. Consent can be granted in several ways, including by a tenant administrator who can consent for *all* users in a Microsoft Entra tenant, or by the application users themselves who can grant access.

Whenever an application that runs in a device requests access to protected data, the application should ask for the consent of the user before granting access to the protected data. The user is required to grant (or deny) consent for the requested permission before the application can progress.

## Least privilege during application development

The security of an application and the user data that it accesses is the responsibility of the developer.

Adhere to these guidelines during application development to help avoid making it overprivileged:

- Fully understand the permissions required for the API calls that the application needs to make.
- Understand the least privileged permission for each API call that the application needs to make using [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
- Find the corresponding [permissions](/en-us/graph/permissions-reference) from least to most privileged.
- Remove any duplicate sets of permissions in cases where the application makes API calls that have overlapping permissions.
- Apply only the least privileged set of permissions to the application by choosing the least privileged permission in the permission list.

## Least privilege for deployed applications

Organizations often hesitate to modify running applications to avoid impacting their normal business operations. However, an organization should consider mitigating the risk of a security incident made possible or more severe by using overprivileged permissions to be worthy of a scheduled application update.

Make these standard practices in an organization to help make sure that deployed applications aren't overprivileged and don't become overprivileged over time:

- Evaluate the API calls being made from the applications.
- Use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) and the [Microsoft Graph](/en-us/graph/overview) documentation for the required and least privileged permissions.
- Audit privileges that are granted to users or applications.
- Update the applications with the least privileged permission set.
- Review permissions regularly to make sure all authorized permissions are still relevant.