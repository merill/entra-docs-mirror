---
layout: Conceptual
title: Application consent management and evaluation of consent requests - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/manage-consent-requests
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Understand consent request evaluation and tenant-wide admin consent in Microsoft Entra ID. Essential guidance for administrators managing application permissions and security.
ms.topic: concept-article
ms.date: 2025-07-20T00:00:00.0000000Z
ms.reviewer: phsignor
ms.custom: enterprise-apps
locale: en-us
document_id: 17a52e9f-e485-bf0f-36d9-4e9061ad5a5a
document_version_independent_id: 377c1a82-64af-4055-fd25-9f1c01ba6e06
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/manage-consent-requests.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/manage-consent-requests
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/manage-consent-requests.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c9b37b6d-0da8-a1cc-0150-123a46a202a0
---

# Application consent management and evaluation of consent requests - Microsoft Entra ID | Microsoft Learn

Microsoft recommends that you [restrict user consent](configure-user-consent) to allow users to consent only for apps from verified publishers, and only for permissions that you select. For apps that don't meet these criteria, the decision-making process is centralized with your organization's security and identity administrator team.

After disabling or restricting user consent, you have several important steps to take to help keep your organization secure as you continue to allow business-critical applications to be used. These steps are crucial to minimize impact on your organization's support team and IT administrators, and to help prevent the use of unmanaged accounts in non-Microsoft applications.

This article explains the main concepts on managing consent to applications and evaluating consent requests in Microsoft's recommendations, including restricting user consent to verified publishers and selected permissions. It covers concepts such as process changes, education for administrators, auditing and monitoring, and managing tenant-wide admin consent.

## Process changes and education

- Consider enabling the [admin consent workflow](configure-admin-consent-workflow) to allow users to request administrator approval directly from the consent screen.
- Ensure that all administrators understand the:

    - [Permissions and consent framework](../../identity-platform/permissions-consent-overview)
    - How the [consent experience and prompts](../../identity-platform/application-consent-experience) work.
    - How to evaluate a request for tenant-wide admin consent.
- Review your organization's existing processes for users to request administrator approval for an application, and update them if necessary. If processes are changed:

    - Update the relevant documentation, monitoring, automation, and so on.
    - Communicate process changes to all affected users, developers, support teams, and IT administrators.

## Auditing and monitoring

- [Audit apps and granted permissions](/en-us/azure/security/fundamentals/steps-secure-identity#audit-apps-and-consented-permissions) in your organization to ensure that no unwarranted or suspicious applications are already granted access to data.
- Review the [Detect and Remediate Illicit Consent Grants in Office 365](/en-us/microsoft-365/security/office-365-security/detect-and-remediate-illicit-consent-grants) article for more best practices and safeguards against suspicious applications that request OAuth consent.
- If your organization has the appropriate license:

    - Use other [OAuth application auditing features in Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/investigate-risky-oauth).
    - Use [Azure Monitor Workbooks](../monitoring-health/howto-use-workbooks) to monitor permissions and consent-related activity. The *Consent Insights* workbook provides a view of apps by number of failed consent requests. This information can help you prioritize applications for administrators to review and decide whether to grant them admin consent.

### Other considerations for reducing friction

To minimize impact on trusted, business-critical applications that are already in use, consider proactively granting administrator consent to applications that have a high number of user consent grants:

- Take an inventory of the apps already added to your organization with high usage, based on sign-in logs or consent grant activity. You can use a [PowerShell script](https://gist.github.com/psignoret/41793f8c6211d2df5051d77ca3728c09) to quickly and easily discover applications with a large number of user consent grants.
- Evaluate the top applications to grant admin consent.

    Important

    Carefully evaluate an application before granting tenant-wide admin consent, even if many users in the organization already consented for themselves.
- For each approved application, grant tenant-wide admin consent and consider restricting user access by [requiring user assignment](assign-user-or-group-access-portal).

## Evaluate a request for tenant-wide admin consent

Granting tenant-wide admin consent is a sensitive operation. Permissions are granted on behalf of the entire organization, and they can include permissions to attempt highly privileged operations. Examples of such operations are role management, full access to all mailboxes or all sites, and full user impersonation.

Before you grant tenant-wide admin consent, it's important to ensure that you trust the application, and the application publisher for the level of access you're granting. If you aren't confident that you understand who controls the application and why the application is requesting the permissions, don't grant consent.

When you're evaluating a request to grant admin consent, here are some recommendations to consider:

- Understand the [permissions and consent framework](../../identity-platform/permissions-consent-overview) in the Microsoft identity platform.
- Understand the difference between [delegated permissions and application permissions](../../identity-platform/permissions-consent-overview#types-of-permissions).

    Application permissions allow the application to access the data for the entire organization, without any user interaction. Delegated permissions allow the application to act on behalf of a user who was signed into the application at some point.
- Understand the permissions that are being requested.

    The permissions requested by the application are listed in the [consent prompt](../../identity-platform/application-consent-experience). Expanding the permission title displays the permission’s description. The description for application permissions generally ends in "without a signed-in user." The description for delegated permissions generally end with "on behalf of the signed-in user." Permissions for the Microsoft Graph API are described in [Microsoft Graph Permissions Reference](/en-us/graph/permissions-reference). Refer to the documentation for other APIs to understand the permissions they expose.

    If you don't understand a permission that's being requested, don't grant consent.
- Understand which application is requesting permissions and who published the application.

    Be wary of malicious applications that try to look like other applications.

    If you doubt the legitimacy of an application or its publisher, don't grant consent. Instead, seek confirmation (for example, directly from the application publisher).
- Ensure that the requested permissions are aligned with the features you expect from the application.

    For example, an application that offers SharePoint site management might require delegated access to read all site collections, but it wouldn't necessarily need full access to all mailboxes, or full impersonation privileges in the directory.

    If you suspect that the application is requesting more permissions than it needs, don't grant consent. Contact the application publisher to obtain more details.

## Grant tenant-wide admin consent

For step-by-step instructions for granting tenant-wide admin consent from the Microsoft Entra admin center, see [Grant tenant-wide admin consent to an application](grant-admin-consent).

## Revoke tenant wide admin consent

To revoke tenant-wide admin consent, you can review and revoke the permissions previously granted to the application. For more information, see [review permissions granted to applications](manage-application-permissions). You can also remove user’s access to the application by [disabling user sign-in to application](disable-user-sign-in-portal) or by [hiding the application](hide-application-from-user-portal) so that it doesn’t appear in the My apps portal.

### Grant consent on behalf of a specific user

Instead of granting consent for the entire organization, an administrator can also use the [Microsoft Graph API](/en-us/graph/use-the-api) to grant consent to delegated permissions on behalf of a single user. For a detailed example that uses Microsoft Graph PowerShell, see [Grant consent on behalf of a single user by using PowerShell](grant-consent-single-user).

## Limit user access to applications

User access to applications can still be limited even when tenant-wide admin consent is granted. To limit user access, require user assignment to an application. For more information, see [Methods for assigning users and groups](assign-user-or-group-access-portal). Administrators can also limit user access to applications by disabling all future user consent operations to any application.

For a broader overview, including how to handle more complex scenarios, see [Use Microsoft Entra ID for application access management](what-is-access-management).