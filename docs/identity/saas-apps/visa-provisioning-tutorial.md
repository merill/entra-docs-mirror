---
layout: Conceptual
title: Configure Visa Spend Clarity for Enterprise for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/visa-provisioning-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: jeedes
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Visa Spend Clarity for Enterprise.
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 38546c17-d561-e526-249d-bb6e149b592d
document_version_independent_id: 38546c17-d561-e526-249d-bb6e149b592d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/visa-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/visa-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/visa-provisioning-tutorial.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/029d2366-5c16-4816-8cb8-dadeaf730762
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/082dcafd-01b6-47e9-8abe-5795dbab1ea9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e6478e91-5b3f-1a25-8243-00b9b306bf3e
---

# Configure Visa Spend Clarity for Enterprise for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Visa Spend Clarity for Enterprise and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users to [Visa Spend Clarity for Enterprise](https://enterprise.spendclarity.visa.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in Visa Spend Clarity for Enterprise.
- Remove users in Visa Spend Clarity for Enterprise when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Visa Spend Clarity for Enterprise.
- Provision groups and group memberships in Visa Spend Clarity for Enterprise.
- Enable [single sign-on](../enterprise-apps/add-application-portal-setup-oidc-sso) to Visa Spend Clarity for Enterprise (recommended).
- Client Credentials Authentication supported.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A user account in Visa Spend Clarity for Enterprise with Admin permissions.

## Step 1: Plan your provisioning deployment

- Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
- Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- Determine what data to [map between Microsoft Entra ID and Visa Spend Clarity for Enterprise](../app-provisioning/customize-application-attributes).

## Step 2: Configure Visa Spend Clarity for Enterprise to support provisioning with Microsoft Entra ID

Before configuring provisioning in Microsoft Entra ID, you need to register an OAuth client in Visa Spend Clarity for Enterprise. Visa Spend Clarity for Enterprise supports Dynamic Client Registration, which automatically creates the OAuth 2.0 / OpenID Connect (OIDC) client when you map your Microsoft Entra tenant to your corporation or company.

To register an OAuth client and obtain the credentials Microsoft Entra ID uses to call the Visa Spend Clarity for Enterprise provisioning API, follow these steps:

1. Sign in to [Visa Spend Clarity for Enterprise](https://enterprise.spendclarity.visa.com/) with an Admin account.
2. Depending on your access level, navigate to one of the following:

    - **Administration** &gt; **Company Management** &gt; **Advanced Configuration** &gt; **External SSO Configuration** (for company-level mapping in a company context), or
    - **Administration** &gt; **Corporate Administration** &gt; **Manage Corporate SSO** (for corporation-level mapping).

    [![Screenshot of the External SSO Configuration option in the Visa Spend Clarity for Enterprise administration menu.](media/visa-provisioning-tutorial/visa-admin-client-registration.png)](media/visa-provisioning-tutorial/visa-admin-client-registration.png#lightbox)
3. In the **External SSO Configuration** dialog, complete the following fields:

    | Field | Value |
    | --- | --- |
    | **Identity Provider** | Select **Microsoft Entra ID** from the drop-down list. |
    | **Tenant ID** | Enter your Microsoft Entra tenant ID (for example, `12345678-1234-1234-1234-123456789abc`). |
    | **Create OAuth Client for User Provisioning** | Select this checkbox to automatically create an OAuth/OIDC client via Dynamic Client Registration. |

    Important

    The **Create OAuth Client** checkbox is hidden when editing an existing tenant mapping to prevent duplicate client creation. If you need to recreate credentials for an existing mapping, contact Visa Spend Clarity for Enterprise support.
4. Select **Save**. Visa Spend Clarity for Enterprise saves the tenant mapping and initiates Dynamic Client Registration in the background.

    [![Screenshot of the External SSO Configuration dialog in Visa Spend Clarity for Enterprise after the tenant mapping is saved.](media/visa-provisioning-tutorial/visa-client-registration.png)](media/visa-provisioning-tutorial/visa-client-registration.png#lightbox)
5. After successful registration, Visa Spend Clarity for Enterprise displays the OAuth client credentials:

    | Credential | Description |
    | --- | --- |
    | **Client ID** | The unique identifier of the OAuth client. |
    | **Client Secret** | The secret used to authenticate as the OAuth client. |

    Use the **Copy** buttons next to each value to copy them to your clipboard.

    [![Screenshot of the OAuth client credentials panel in Visa Spend Clarity for Enterprise, showing the Client ID and Client Secret with Copy buttons.](media/visa-provisioning-tutorial/visa-client-id-and-secret.png)](media/visa-provisioning-tutorial/visa-client-id-and-secret.png#lightbox)

    Warning

    **Save these credentials immediately.** The client secret is displayed only once and cannot be retrieved later. Store the values in a secure password manager or secrets vault. If the credentials are lost, you must delete the OAuth client and create a new tenant mapping.
6. If client registration fails, the tenant mapping is still saved, but you see an error message indicating that OAuth client creation failed. In this case, contact Visa Spend Clarity for Enterprise support to register the OAuth client manually.
7. Retain the **Client ID** and **Client Secret** values. You use them in Step 5 when configuring the **Tenant URL** and **Secret Token** in Microsoft Entra ID.

## Step 3: Add Visa Spend Clarity for Enterprise from the Microsoft Entra application gallery

Add Visa Spend Clarity for Enterprise from the Microsoft Entra application gallery to start managing provisioning to Visa Spend Clarity for Enterprise. If you've previously set up Visa Spend Clarity for Enterprise for SSO, you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. For more information, see [Add an application to your Microsoft Entra tenant](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Visa Spend Clarity for Enterprise

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in Visa Spend Clarity for Enterprise based on user assignments in Microsoft Entra ID.

To configure automatic user provisioning in Microsoft Entra ID, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an app owner or a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot shows the enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Visa Spend Clarity for Enterprise**.

    ![Screenshot shows the Visa Spend Clarity for Enterprise link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot shows the provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of the Provisioning tab in the Microsoft Entra admin center with the New configuration button highlighted.](common/application-provisioning.png)
6. In the **Tenant URL** field, input your Visa Spend Clarity for Enterprise **Tenant URL, Client identifier, Client secret** and **OAuth token endpoint**. Select **Test connection** to ensure Microsoft Entra ID can connect to Visa Spend Clarity for Enterprise. If the connection fails, ensure your Visa Spend Clarity for Enterprise account has Admin permissions and try again.

    ![Screenshot of Provisioning test connection.](common/provisioning-test-button.png)
7. Select **Create** to create your configuration.
8. Select **Properties** in the **Overview** page.
9. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of the Provisioning Properties page in the Microsoft Entra admin center.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select users.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Visa Spend Clarity for Enterprise in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Visa Spend Clarity for Enterprise for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Visa Spend Clarity for Enterprise API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Visa Spend Clarity for Enterprise |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | active | Boolean |  |  |
    | externalId | String |  |  |
    | givenName | String |  |  |
    | surname | String |  |  |
    | emails | String |  |  |
    | employeeNumber | Number |  |  |
    | urn:ietf:params:scim:schemas:extension:visa:2.0:User:subCompanyId | String |  |  |

    Note

    The **SubCompanyId** is required only when provisioning is set for a corporation.
12. Select **groups**.
13. Review the group attributes that are synchronized from Microsoft Entra ID to Visa Spend Clarity for Enterprise in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in Visa Spend Clarity for Enterprise for update operations. Select the **Save** button to commit any changes.
14. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) article.
15. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.