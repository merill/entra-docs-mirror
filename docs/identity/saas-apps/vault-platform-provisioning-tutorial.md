---
layout: Conceptual
title: Configure Vault Platform for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/vault-platform-provisioning-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to automatically provision and de-provision user accounts from Microsoft Entra ID to Vault Platform.
ms.topic: how-to
ms.date: 2026-04-06T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f3ea4672-ec9b-4a03-df1e-c5f5075c3c18
document_version_independent_id: 4f9e2026-f9ab-8950-a3bc-8ef38b5c7bd1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/vault-platform-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/vault-platform-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/vault-platform-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 90547347-8c58-0bbe-b13a-d9da8f6ab6f6
---

# Configure Vault Platform for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Vault Platform and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and de-provisions users to [Vault Platform](https://vaultplatform.com) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Supported capabilities

- Create users in Vault Platform.
- Remove users in Vault Platform when they don't require access anymore.
- Keep user attributes synchronized between Microsoft Entra ID and Vault Platform.
- [Single sign-on](vault-platform-tutorial) to Vault Platform (recommended).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- [A Microsoft Entra tenant](../../identity-platform/quickstart-create-new-tenant)
- One of the following roles: [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- An administrator account with Vault Platform.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who's in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and Vault Platform](../app-provisioning/customize-application-attributes).

## Step 2: Configure Vault Platform to support provisioning with Microsoft Entra ID

Contact Vault Platform support to configure Vault Platform to support provisioning with Microsoft Entra ID.

### 1. Authentication

Go to the Vault Platform, login with your email and password (initial login method), then head to the **Administration &gt; Authentication page**.

There, first change the login method dropdown to **Identity Provider - Azure - SAML**

Using the details in the SAML setup instructions page, enter the information:

![Screenshot of VaultPlatform Authentication page.](media/vault-platform-provisioning-tutorial/authentication.png)

1. Issuer URI must be set to `vaultplatform`
2. SSO URL must be set to the value of Login URL ![Screenshot for identifying SSO URL.](media/vault-platform-provisioning-tutorial/sso-url-entry-point-uri.png)
3. Download the **Certificate (Base64)** file, open it in a text editor and copy its contents (including the `-----BEGIN/END CERTIFICATE-----` markers) into the **Certificate** text field ![Screenshot of Certificate.](media/vault-platform-provisioning-tutorial/certificate-base64.png)

### 2. Data Integration

Next go to **Administration &gt; Data Integration** inside Vault Platform

![Screenshot of Data Integration page.](media/vault-platform-provisioning-tutorial/data-integration.png)

1. For **Data Integration** select `Azure`.
2. For **Method of providing SCIM secret location** set `bearer`.
3. For **Secret** set a complex string, similar to a strong password. Keep this string secure as it's used later on at **Step 5**
4. Toggle **Set as active SCIM Provider** to be active.

## Step 3: Add Vault Platform from the Microsoft Entra application gallery

Add Vault Platform from the Microsoft Entra application gallery to start managing provisioning to Vault Platform. If you have previously setup Vault Platform for SSO you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to Vault Platform

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users in TestApp based on user and/or group assignments in Microsoft Entra ID.

### Configure automatic user provisioning for Vault Platform in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**

    ![Screenshot of Enterprise applications blade.](common/enterprise-applications.png)
3. In the applications list, select **Vault Platform**.

    ![Screenshot of the Vault Platform link in the Applications list.](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of Provisioning tab.](common/provisioning.png)
5. Select **+ New configuration**.

    ![Screenshot of new configuration.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, input your Vault Platform Tenant URL (URL with structure `https://app.vaultplatform.com/api/scim/${organization-slug}`) and Secret Token (from Step 2.2). Select **Test Connection** to ensure Microsoft Entra ID can connect to Vault Platform. If the connection fails, ensure your Vault Platform account has Admin permissions and try again.

    ![Screenshot of Token.](common/provisioning-testconnection-tenanturltoken.png)
7. Select **Create** to create your configuration.
8. Select **Properties** on the **Overview** page.
9. Select the **Edit** icon to edit the properties. Enable notification emails and provide an email to receive quarantine notifications. Enable **Accidental deletions prevention**. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
10. Select **Attribute Mapping** in the left panel and select **users**.
11. Review the user attributes that are synchronized from Microsoft Entra ID to Vault Platform in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Vault Platform for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes), you need to ensure that the Vault Platform API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

    | Attribute | Type | Supported for filtering | Required by Vault Platform |
    | --- | --- | --- | --- |
    | userName | String | ✓ | ✓ |
    | externalId | String | ✓ | ✓ |
    | active | Boolean |  | ✓ |
    | displayName | String |  |  |
    | title | String |  | ✓ |
    | emails[type eq "work"].value | String |  | ✓ |
    | name.givenName | String |  | ✓ |
    | name.familyName | String |  | ✓ |
    | addresses[type eq "work"].locality | String |  | ✓ |
    | addresses[type eq "work"].country | String |  | ✓ |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber | String |  | ✓ |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department | String |  | ✓ |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager | String |  |  |
    | userType | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:division | String |  |  |
    | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:organization | String |  |  |

    Note

    The attribute "externalID" is only sent to Vault on object creation and will not be updated if changed in Entra ID.
12. To configure scoping filters, refer to the instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
13. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
14. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.