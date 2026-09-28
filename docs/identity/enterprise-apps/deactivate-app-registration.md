---
layout: Conceptual
title: Deactivate an app registration - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/deactivate-app-registration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to deactivate an app registration in Microsoft Entra ID to prevent token issuance while preserving application configuration.
ms.topic: how-to
ms.date: 2026-03-16T00:00:00.0000000Z
ms.reviewer: ariels
ms.custom: enterprise-apps, no-azure-ad-ps-ref, sfi-image-nochange
locale: en-us
document_id: e14d3879-33ed-664d-49b5-5001563b4a22
document_version_independent_id: e14d3879-33ed-664d-49b5-5001563b4a22
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/deactivate-app-registration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/deactivate-app-registration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/deactivate-app-registration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: c15abd04-ccbe-cd38-260e-fae8b053dd3d
---

# Deactivate an app registration - Microsoft Entra ID | Microsoft Learn

Deactivating an app registration provides a reversible way to prevent the application from accessing protected resources without permanently removing it from your tenant. When you deactivate an application, it immediately stops receiving new access tokens, but existing tokens remain valid until they expire. This approach is useful for security investigations, temporary suspension of suspicious applications, or when you need to maintain application configuration data.

Unlike permanently deleting an application, deactivation preserves all application metadata, permissions, and configuration settings, making it easy to reactivate the application if needed. The application remains visible in your tenant's enterprise applications list, but users can't sign in and no new tokens are issued.

This article shows you how to deactivate an enterprise application, view deactivated applications, and reactivate them when necessary.

## Prerequisites

Before you can deactivate an application, ensure you meet the following requirements:

- One of the following Microsoft Entra roles:
    - [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Administrator](../role-based-access-control/permissions-reference#application-administrator)
- OR a custom role with the following action:
    - `microsoft.directory/applications/disablement/update`
- The following API permissions if using Microsoft Graph:
    - `Application.ReadWrite.All` (delegated or application)
    - `Application.ReadWrite.OwnedBy` (application, for owned apps only)

## Understand application deactivation

When an application is deactivated, the following behavior occurs:

- Immediate effects:

    - New access token requests are denied
    - Users can't sign in to the application
    - Application can't access protected resources with new tokens
- Preserved elements:

    - Existing access tokens remain valid until their configured lifetime expires
    - Application configuration, permissions, and metadata are preserved
    - Application remains visible in **Enterprise applications** list
    - Service principal object is maintained in the tenant

When users attempt to sign in to a deactivated application, they receive an error message indicating the application has been disabled by its owner. This is different from other error messages like invalid credentials or access denied.

### Comparison with other options

Microsoft Entra apps and service principals can be prevented from usage in four ways:

- **isDisabled** (deactivate) property is set on apps that have been disabled globally by the app owner or administrator.
- **disabledByMicrosoftStatus** (disabled by Microsoft) property is set on apps that have been disabled globally by Microsoft.
- **accountEnabled** (disable sign-in) property is set on service principals disabled in the tenant by the app owner or administrator.
- **DELETE** (delete) operation is completed as an operation on apps or service principals by the app owner or administrator.

The following table outlines the different approaches in more detail:

| Action | Token issuance | Configuration preserved | Reversible | Scope |
| --- | --- | --- | --- | --- |
| Deactivate | Blocked | Yes | Yes | Global (all tenants) |
| Disabled by Microsoft | Blocked | Yes | Yes | Global (all tenants) |
| Disable sign-in | Blocked in tenant | Yes | Yes | Single tenant only |
| Delete | Blocked | No (30-day recycle bin) | Yes (30 days) | Global |

## Deactivate an application

To deactivate an application using Microsoft Graph API or Microsoft Entra admin center, you need at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) role or a custom role with the `microsoft.directory/applications/disablement/update` action.

# [Microsoft Entra admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **App registrations**.
3. Locate the app that needs deactivating from your list of registered apps.
4. Once you have identified the app to deactivate, select the **Deactivate** button on its app registration page.
5. Review the information provided in the **Deactivate app registration** pane before selecting the second **Deactivate** button.

    - The app won't be able to access protected resources.
    - It won't be able to obtain new access tokens, but existing ones will still be valid.
    - It will still be visible in the **Enterprise applications** list for tenants that have an instance of it, but users won't be able to sign in.
    - Previously issued access tokens will invalidate based on their lifetime. Expiration or invalidation of an access token depends on various factors such as default expiration time and token lifetime policy.
6. Once you have confirmed you would like to deactivate the app, select the **Deactivate** button Deactivation takes place immediately and the `isDisabled` property for this application is set to `true`. You can ensure the app status reflects the change by verifying its deactivated **State** change on the **App Registration** page.

    ![Screenshot of Deactivate app registration pane in Microsoft Entra admin center.](media/deactivate-app-registration/deactivate-app-registration.png)

Important

If the app has assigned owners, this information appears in the **Deactivate app registration** pane. Before deactivating, review the list of owners and decide whether to remove any of them. To prevent others from reactivating the app, remove all other owners.

![Screenshot showing the option to remove app owners before deactivating an app registration to prevent unauthorized reactivation.](media/deactivate-app-registration/remove-owners.png)

# [Microsoft Graph API](#tab/graph-api)
1. Deactivate the application

    ```http
    PATCH https://graph.microsoft.com/beta/applications/{applicationObjectId}
    Content-Type: application/json
    
    {
        "isDisabled": true
    }
    ```

    ```http
    PATCH https://graph.microsoft.com/beta/applications(appId='{appId}')
    Content-Type: application/json
    
    {
        "isDisabled": true
    }
    ```
2. Verify deactivation

    ```http
    GET https://graph.microsoft.com/beta/applications/{applicationObjectId}
    ```

    The response includes `"isDisabled": true`.

    ```http
     GET https://graph.microsoft.com/beta/applications(appId='{appId}')
    ```

    The response includes `"isDisabled": true`.

---

## View deactivated applications

You can view deactivated applications to monitor their status and track which applications have been temporarily disabled in your tenant.

# [Microsoft Entra admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **App registrations**.
3. Select the **Deactivated applications** tab.
4. Alternatively, navigate to the **Enterprise apps** pane and check on a given enterprise app under **Manage** -&gt; **Properties** -&gt; **Activation status**.

    ![Screenshot showing the Activation status field in the Enterprise app Properties page displaying whether an application is active or deactivated.](media/deactivate-app-registration/view-activation-status.png)

# [Microsoft Graph API](#tab/graph-api)
1. List all deactivated applications

    ```http
    GET https://graph.microsoft.com/beta/applications?$filter=isDisabled eq true
    ```
2. Get specific application status

    ```http
    GET https://graph.microsoft.com/beta/applications/{applicationObjectId}?$select=displayName,isDisabled,appId
    ```

---

Important

Deactivation must be performed on the app registration (application object). The deactivated state is then reflected on the enterprise app (service principal object). You can't deactivate the service principal directly. You can only disable sign-in on the service principal, by using set `accountEnabled = false`.

## Investigate deactivated applications

When handling deactivated applications, conduct a thorough investigation by examining the application's configuration, including API permissions, authentication settings, certificates, and sign-in logs. Document your findings carefully, noting the reason for deactivation, any suspicious activity or security concerns, affected users, and dependencies that might impact your organization.

Based on your investigation, take appropriate action such as escalating to security teams if compromise is suspected, removing unnecessary permissions before reactivation, or updating the application configuration to address identified security issues. If the application is no longer needed or poses ongoing security risks, consider permanent deletion instead of reactivation.

## Reactivate an application

To reactivate an application using Microsoft Graph API or Microsoft Entra admin center, you need at least the [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) role or a custom role with the `microsoft.directory/applications/disablement/update` action.

# [Microsoft Entra admin center](#tab/admin-center)
1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **App registrations**.
3. Select the **Deactivated applications** tab to locate the deactivated app you want to reactivate.
4. Select the deactivated application from the list.
5. On the app registration page, select the **Reactivate** button.
6. Review the information provided in the **Reactivate app registration** pane before selecting the second **Reactivate** button.

    - The app will be able to access protected resources again.
    - It will be able to obtain new access tokens.
    - Users will be able to sign in to the application.
7. Once you have confirmed you would like to reactivate the app, select the **Reactivate** button. Reactivation takes place immediately and the `isDisabled` property for this application is set to `false`. You can ensure the app status reflects the change by verifying its **State** change on the **App Registration** page.

    ![Screenshot showing the option to reactivate an application.](media/deactivate-app-registration/reactivate-app.png)

# [Microsoft Graph API](#tab/graph-api)
1. Reactivate the application

    ```http
    PATCH https://graph.microsoft.com/v1.0/applications(appId='{appId}')
    Content-Type: application/json
    
    {
        "isDisabled": false
    }
    ```
2. Verify reactivation

    ```http
    GET https://graph.microsoft.com/v1.0/applications(appId='{appId}')?$select=displayName,isDisabled
    ```

    The response shows `"isDisabled": false`.

---

## Prevent reactivation by nonadministrators

Before deactivating the application, remove all owners from the application. This ensures only users with at least the [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator) role or a custom role with the `microsoft.directory/applications/disablement/update` action can reactivate the application.

## Audit deactivation and reactivation

Whenever an application is deactivated or reactivated, there will be a Microsoft Entra audit log event with:

- **Service**: Core Directory
- **Category**: ApplicationManagement
- **Activity** (activityDisplayName): "Update application"

In the Microsoft Entra admin center, you can find these events under **Monitoring & health &gt; Audit logs**. When you select an **Update application** event, navigate to the **Modified Properties** tab in the **Audit Log Details** pane.

![Screenshot showing audit log details for application deactivation with `isDisabled` property changes.](media/deactivate-app-registration/audit-log-details.png)

You will see the Property Name `isDisabled` with Old Value and New Value, where "true" is deactivated and "false" or null is activated or reactivated.