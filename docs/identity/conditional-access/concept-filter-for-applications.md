---
layout: Conceptual
title: Filter for applications in Conditional Access policy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-filter-for-applications
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Discover how to use Conditional Access filters for applications to streamline policy management and enhance security in Microsoft Entra ID.
ms.topic: how-to
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: calebb, oanae
ms.custom:
- subject-rbac-steps
- ai-gen-docs-bap
- ai-gen-description
- ai-seo-date:07/22/2025
locale: en-us
document_id: ea596b1a-7176-712b-453c-a5df7316db08
document_version_independent_id: cf645574-1664-5b67-c494-c4469e86413b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-filter-for-applications.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-filter-for-applications
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-filter-for-applications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: b15fc733-8c4d-595f-8dde-287272cf96dc
---

# Filter for applications in Conditional Access policy - Microsoft Entra ID | Microsoft Learn

## Overview

Currently Conditional Access policies can be applied to all apps or to individual apps. Organizations with a large number of apps might find this process difficult to manage across multiple Conditional Access policies.

Application filters for Conditional Access allow organizations to tag service principals with custom attributes. These custom attributes are then added to their Conditional Access policies. Filters for applications are evaluated at token issuance runtime, not configuration.

In this document, you create a custom attribute set, assign a custom security attribute to your application, and create a Conditional Access policy to secure the application.

## Assign roles

Custom security attributes are security sensitive and can only be managed by delegated users. One or more of the following roles should be assigned to the users who manage or report on these attributes.

| Role name | Description |
| --- | --- |
| [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator) | Assign custom security attribute keys and values to supported Microsoft Entra objects. |
| [Attribute Assignment Reader](../role-based-access-control/permissions-reference#attribute-assignment-reader) | Read custom security attribute keys and values for supported Microsoft Entra objects. |
| [Attribute Definition Administrator](../role-based-access-control/permissions-reference#attribute-definition-administrator) | Define and manage the definition of custom security attributes. |
| [Attribute Definition Reader](../role-based-access-control/permissions-reference#attribute-definition-reader) | Read the definition of custom security attributes. |

Assign the appropriate role to the users who manage or report on these attributes at the directory scope. For detailed steps, see [Assign Microsoft Entra roles](../role-based-access-control/manage-roles-portal#assign-roles-with-tenant-scope).

Important

By default, [Global Administrator](../role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

## Create custom security attributes

Follow the instructions in the article, [Add or deactivate custom security attributes in Microsoft Entra ID](../../fundamentals/custom-security-attributes-add) to add the following **Attribute set** and **New attributes**.

- Create an **Attribute set** named *ConditionalAccessTest*.
- Create **New attributes** named *policyRequirement* that **Allow multiple values to be assigned** and **Only allow predefined values to be assigned**. Add the following predefined values:
    - legacyAuthAllowed
    - blockGuestUsers
    - requireMFA
    - requireCompliantDevice
    - requireHybridJoinedDevice
    - requireCompliantApp

[![A screenshot showing custom security attribute and predefined values in Microsoft Entra ID.](media/concept-filter-for-applications/custom-attributes.png)](media/concept-filter-for-applications/custom-attributes.png#lightbox)

Note

Conditional Access filters for applications only work with custom security attributes of type `string`. Custom Security Attributes support creation of Boolean data type but Conditional Access Policy only supports `string`.

## Create a Conditional Access policy

[![A screenshot showing a Conditional Access policy with the edit filter window showing an attribute of require MFA.](media/concept-filter-for-applications/edit-filter-for-applications.png)](media/concept-filter-for-applications/edit-filter-for-applications.png#lightbox)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) and [Attribute Definition Reader](../role-based-access-control/permissions-reference#attribute-definition-reader).
2. Browse to **Entra ID** &gt; **Conditional Access**.
3. Select **New policy**.
4. Give your policy a name. Create a meaningful standard for the names of your policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**.
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
    3. Select **Done**.
6. Under **Target resources**, select the following options:
    1. Select what this policy applies to **Resources (formerly cloud apps)**.
    2. Include **Select resources**.
    3. Select **Edit filter**.
    4. Set **Configure** to **Yes**.
    5. Select the **Attribute** created earlier called *policyRequirement*.
    6. Set **Operator** to **Contains**.
    7. Set **Value** to **requireMFA**.
    8. Select **Done**.
7. Under **Access controls** &gt; **Grant**, select **Grant access**, **Require multifactor authentication**, and select **Select**.
8. Confirm your settings and set **Enable policy** to **Report-only**.
9. Select **Create** to enable your policy.

After confirming your settings using [policy impact or report-only mode](concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

## Configure custom attributes

### Step 1: Set up a sample application

If you already have a test application that makes use of a service principal, you can skip this step.

Set up a sample application that, demonstrates how a job or a Windows service can run with an application identity, instead of a user's identity. Follow the instructions in the article [Quickstart: Get a token and call the Microsoft Graph API by using a console app's identity](../../identity-platform/quickstart-daemon-app-call-api) to create this application.

### Step 2: Assign a custom security attribute to an application

When you don't have a service principal listed in your tenant, it can't be targeted. The Office 365 suite is an example of one such service principal.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../role-based-access-control/permissions-reference#conditional-access-administrator) and [Attribute Assignment Administrator](../role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select the service principal you want to apply a custom security attribute to.
4. Under **Manage** &gt; **Custom security attributes**, select **Add assignment**.
5. Under **Attribute set**, select **ConditionalAccessTest**.
6. Under **Attribute name**, select **policyRequirement**.
7. Under **Assigned values**, select **Add values**, select **requireMFA** from the list, then select **Done**.
8. Select **Save**.

### Step 3: Test the policy

Sign in as a user who the policy would apply to and test to see that MFA is required when accessing the application.

## Other scenarios

- Blocking legacy authentication
- Blocking external access to applications
- Requiring compliant device or Intune app protection policies
- Enforcing sign in frequency controls for specific applications
- Requiring a privileged access workstation for specific applications
- Require session controls for high risk users and specific applications