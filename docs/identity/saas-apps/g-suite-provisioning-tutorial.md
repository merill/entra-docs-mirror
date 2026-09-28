---
layout: Conceptual
title: Configure Google Cloud / Google Workspace for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/g-suite-provisioning-tutorial
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
description: Learn how to automatically provision and deprovision user accounts from Microsoft Entra ID to Google Cloud or Google Workspace.
ms.topic: how-to
ms.date: 2025-03-09T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6eba9a3b-88e4-8156-a31e-58a74c604f28
document_version_independent_id: 2e0e6273-3e21-1ea2-43f8-48e5effc9a83
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/g-suite-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/g-suite-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/g-suite-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ad2797ea-494e-57b3-6af7-9e3f94e44397
---

# Configure Google Cloud / Google Workspace for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article describes the steps you need to perform in both Google (Google Cloud or Google Workspace) and Microsoft Entra ID to configure automatic user provisioning. When configured, Microsoft Entra ID automatically provisions and deprovisions users and groups to [Google Workspace](https://workspace.google.com/) using the Microsoft Entra provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

Note

This article describes a connector built on top of the Microsoft Entra user provisioning service for Google G Suite, the former name of Google Workspace. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Capabilities supported

- Create users in G Suite
- Remove users in G Suite when they don't require access anymore (note: removing a user from the sync scope doesn't result in deletion of the object in G Suite)
- Keep user attributes synchronized between Microsoft Entra ID and G Suite
- Provision groups and group memberships in G Suite
- [Single sign-on](google-apps-tutorial) to G Suite (recommended)

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- [A G Suite tenant](https://gsuite.google.com/pricing.html)
- A user account on a G Suite with Admin permissions.

## Step 1: Plan your provisioning deployment

1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning).
2. Determine who is in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
3. Determine what data to [map between Microsoft Entra ID and G Suite](../app-provisioning/customize-application-attributes).

## Step 2: Configure G Suite to support provisioning with Microsoft Entra ID

Before configuring G Suite for automatic user provisioning with Microsoft Entra ID, you need to enable SCIM provisioning on G Suite.

1. Sign in to the [G Suite Admin console](https://admin.google.com/) with your administrator account, then select **Main menu** and then select **Security**. If you don't see it, it might be hidden under the **Show More** menu.

    ![G Suite Security](media/g-suite-provisioning-tutorial/security.png)

    ![G Suite Show More](media/g-suite-provisioning-tutorial/show-more.png)
2. Navigate to **Security -&gt; Access and data control -&gt; API Controls** .Select the check box **Trust internal,domain-owned apps** and then select **SAVE**

    ![G Suite API](media/g-suite-provisioning-tutorial/api-control.png)

    Important

    For every user that you intend to provision to G Suite, their user name in Microsoft Entra ID **must** be tied to a custom domain. For example, user names that look like bob@contoso.onmicrosoft.com aren't accepted by G Suite. On the other hand, bob@contoso.com is accepted. You can change an existing user's domain by following the instructions [here](../../fundamentals/add-custom-domain).
3. Once you add and verify your desired custom domains with Microsoft Entra ID, you must verify them again with G Suite. To verify domains in G Suite, refer to the following steps:

    1. In the [G Suite Admin Console](https://admin.google.com/), navigate to **Account -&gt; Domains -&gt; Manage Domains**.

        ![G Suite Domains](media/g-suite-provisioning-tutorial/domains.png)
    2. In the Manage Domain page, select **Add a domain**.

        ![G Suite Add Domain](media/g-suite-provisioning-tutorial/add-domains.png)
    3. In the Add Domain page, type in the name of the domain that you want to add.

        ![G Suite Verify Domain](media/g-suite-provisioning-tutorial/verify-domains.png)
    4. Select **ADD DOMAIN & START VERIFICATION**. Then follow the steps to verify that you own the domain name. For comprehensive instructions on how to verify your domain with Google, see [Verify your site ownership](https://support.google.com/webmasters/answer/35179).
    5. Repeat the preceding steps for any more domains that you intend to add to G Suite.
4. Next, determine which admin account you want to use to manage user provisioning in G Suite. Navigate to **Account-&gt;Admin roles**.

    ![G Suite Admin](media/g-suite-provisioning-tutorial/admin-roles.png)
5. For the **Admin role** of that account, edit the **Privileges** for that role. Make sure to enable all **Admin API Privileges** so that this account can be used for provisioning.

    ![G Suite Admin Privileges](media/g-suite-provisioning-tutorial/admin-privilege.png)

## Step 3: Add G Suite from the Microsoft Entra application gallery

Add G Suite from the Microsoft Entra application gallery to start managing provisioning to G Suite. If you have previously setup G Suite for SSO, you can use the same application. However, we recommend that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../enterprise-apps/add-application-portal).

## Step 4: Define who is in scope for provisioning

The Microsoft Entra provisioning service allows you to scope who is provisioned based on assignment to the application, or based on attributes of the user or group. If you choose to scope who is provisioned to your app based on assignment, you can use the [steps to assign users and groups to the application](../enterprise-apps/assign-user-or-group-access-portal). If you choose to scope who is provisioned based solely on attributes of the user or group, you can [use a scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).

- Start small. Test with a small set of users and groups before rolling out to everyone. When scope for provisioning is set to assigned users and groups, you can control this by assigning one or two users or groups to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
- If you need extra roles, you can [update the application manifest](../../identity-platform/howto-add-app-roles-in-apps) to add new roles.

## Step 5: Configure automatic user provisioning to G Suite

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in TestApp based on user and/or group assignments in Microsoft Entra ID.

Note

To learn more about the G Suite Directory API endpoint, refer to the [Directory API reference documentation](https://developers.google.com/admin-sdk/directory).

### To configure automatic user provisioning for G Suite in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.

    ![Enterprise applications blade](media/g-suite-provisioning-tutorial/enterprise-applications.png)

    ![All applications blade](media/g-suite-provisioning-tutorial/all-applications.png)
3. In the applications list, select **G Suite**.

    ![The G Suite link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab. Select **Get started**.

    ![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, select **Authorize**. You're redirected to a Google authorization dialog box in a new browser window.

    ![G Suite authorize](media/g-suite-provisioning-tutorial/authorize-1.png)
7. Confirm that you want to give Microsoft Entra permissions to make changes to your G Suite tenant. Select **Accept**.

    ![G Suite Tenant Auth](media/g-suite-provisioning-tutorial/gapps-auth.png)
8. Select **Test Connection** to ensure Microsoft Entra ID can connect to G Suite. If the connection fails, ensure your G Suite account has Admin permissions and try again. Then try the **Authorize** step again.
9. Select **Create** to create your configuration.
10. Select **Properties** in the **Overview** page.
11. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
12. Select **Attribute Mapping** in the left panel and select **users**.
13. Review the user attributes that are synchronized from Microsoft Entra ID to G Suite in the **Attribute-Mapping** section. Select the **Save** button to commit any changes.

Note

G Suite Provisioning currently only supports the use of primaryEmail as the matching attribute.

| Attribute | Type |
| --- | --- |
| primaryEmail | String |
| relations.[type eq "manager"].value | String |
| name.familyName | String |
| name.givenName | String |
| suspended | String |
| externalIds.[type eq "custom"].value | String |
| externalIds.[type eq "organization"].value | String |
| addresses.[type eq "work"].country | String |
| addresses.[type eq "work"].streetAddress | String |
| addresses.[type eq "work"].region | String |
| addresses.[type eq "work"].locality | String |
| addresses.[type eq "work"].postalCode | String |
| emails.[type eq "work"].address | String |
| organizations.[type eq "work"].department | String |
| organizations.[type eq "work"].title | String |
| phoneNumbers.[type eq "work"].value | String |
| phoneNumbers.[type eq "mobile"].value | String |
| phoneNumbers.[type eq "work\_fax"].value | String |
| emails.[type eq "work"].address | String |
| organizations.[type eq "work"].department | String |
| organizations.[type eq "work"].title | String |
| addresses.[type eq "home"].country | String |
| addresses.[type eq "home"].formatted | String |
| addresses.[type eq "home"].locality | String |
| addresses.[type eq "home"].postalCode | String |
| addresses.[type eq "home"].region | String |
| addresses.[type eq "home"].streetAddress | String |
| addresses.[type eq "other"].country | String |
| addresses.[type eq "other"].formatted | String |
| addresses.[type eq "other"].locality | String |
| addresses.[type eq "other"].postalCode | String |
| addresses.[type eq "other"].region | String |
| addresses.[type eq "other"].streetAddress | String |
| addresses.[type eq "work"].formatted | String |
| changePasswordAtNextLogin | String |
| emails.[type eq "home"].address | String |
| emails.[type eq "other"].address | String |
| externalIds.[type eq "account"].value | String |
| externalIds.[type eq "custom"].customType | String |
| externalIds.[type eq "customer"].value | String |
| externalIds.[type eq "login\_id"].value | String |
| externalIds.[type eq "network"].value | String |
| gender.type | String |
| GeneratedImmutableId | String |
| Identifier | String |
| ims.[type eq "home"].protocol | String |
| ims.[type eq "other"].protocol | String |
| ims.[type eq "work"].protocol | String |
| includeInGlobalAddressList | String |
| ipWhitelisted | String |
| organizations.[type eq "school"].costCenter | String |
| organizations.[type eq "school"].department | String |
| organizations.[type eq "school"].domain | String |
| organizations.[type eq "school"].fullTimeEquivalent | String |
| organizations.[type eq "school"].location | String |
| organizations.[type eq "school"].name | String |
| organizations.[type eq "school"].symbol | String |
| organizations.[type eq "school"].title | String |
| organizations.[type eq "work"].costCenter | String |
| organizations.[type eq "work"].domain | String |
| organizations.[type eq "work"].fullTimeEquivalent | String |
| organizations.[type eq "work"].location | String |
| organizations.[type eq "work"].name | String |
| organizations.[type eq "work"].symbol | String |
| OrgUnitPath | String |
| phoneNumbers.[type eq "home"].value | String |
| phoneNumbers.[type eq "other"].value | String |
| websites.[type eq "home"].value | String |
| websites.[type eq "other"].value | String |
| websites.[type eq "work"].value | String |

1. Select **Groups**.
2. Review the group attributes that are synchronized from Microsoft Entra ID to G Suite in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the groups in G Suite for update operations. Select the **Save** button to commit any changes.

    | Attribute | Type |
    | --- | --- |
    | email | String |
    | Members | String |
    | name | String |
    | description | String |
3. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
4. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a few users before deploying more broadly in your organization.
5. When you're ready to provision, select **Start Provisioning** from the **Overview** page.

Note

If the users already have an existing personal/consumer account using the email address of the Microsoft Entra user, then it might cause some issue, which could be resolved by using the Google Transfer Tool prior to performing the directory sync.

## Step 6: Monitor your deployment

Once you configure provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../monitoring-health/concept-provisioning-logs) to determine which users are provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) to see the status of the provisioning cycle and how close it's to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application goes into quarantine. Learn more about quarantine states the [application provisioning quarantine status](../app-provisioning/application-provisioning-quarantine-status) article.

## Troubleshooting Tips

- Removing a user from the sync scope disables them in GSuite but won't result in deletion of the user in G Suite

## Just-in-time (JIT) application access with PIM for groups

With PIM for Groups, you can provide just-in-time access to groups in Google Cloud / Google Workspace and reduce the number of users that have permanent access to privileged groups in Google Cloud / Google Workspace.

**Configure your enterprise application for SSO and provisioning**

1. Add Google Cloud / Google Workspace to your tenant, configure it for provisioning as described in this article, and start provisioning.
2. Configure [single sign-on](google-apps-tutorial) for Google Cloud / Google Workspace.
3. Create a [group](/en-us/azure/active-directory/fundamentals/how-to-manage-groups) that provides all users access to the application.
4. Assign the group to the Google Cloud / Google Workspace application.
5. Assign your test user as a direct member of the group created in the previous step, or provide them with access to the group through an access package. This group can be used for persistent, nonadmin access in Google Cloud / Google Workspace.

**Enable PIM for groups**

1. Create a second group in Microsoft Entra ID. This group provides access to admin permissions in Google Cloud / Google Workspace.
2. Bring the group under [management in Microsoft Entra PIM](/en-us/azure/active-directory/privileged-identity-management/groups-discover-groups).
3. Assign your test user as [eligible for the group in PIM](/en-us/azure/active-directory/privileged-identity-management/groups-assign-member-owner) with the role set to member.
4. Assign the second group to the Google Cloud / Google Workspace application.
5. Use on-demand provisioning to create the group in Google Cloud / Google Workspace.
6. Sign-in to Google Cloud / Google Workspace and assign the second group the necessary permissions to perform admin tasks.

Now any end user that was made eligible for the group in PIM can get JIT access to the group in Google Cloud / Google Workspace by [activating their group membership](/en-us/azure/active-directory/privileged-identity-management/groups-activate-roles#activate-a-role). When their assignment expires, the user is removed from the group in Google Cloud / Google Workspace. During the next incremental cycle, the provisioning service attempts to remove the user from the group again. This might result in an error in the provisioning logs. This error is expected because the group membership was already removed. The error message can be ignored.

- How long does it take to have a user provisioned to the application?
    - When a user is added to a group in Microsoft Entra ID outside of activating their group membership using Microsoft Entra ID Privileged Identity Management (PIM):
        - The group membership is provisioned in the application during the next synchronization cycle. The synchronization cycle runs every 40 minutes.
    - When a user activates their group membership in Microsoft Entra ID PIM:
        - The group membership is provisioned in 2 – 10 minutes. When there's a high rate of requests at one time, requests are throttled at a rate of five requests per 10 seconds.
        - For the first five users within a 10-second period activating their group membership for a specific application, group membership is provisioned in the application within 2-10 minutes.
        - For the sixth user and beyond within a 10-second period activating their group membership for a specific application, group membership is provisioned to the application in the next synchronization cycle. The synchronization cycle runs every 40 minutes. The throttling limits are per enterprise application.
- If the user is unable to access the necessary group in Google Cloud / Google Workspace, review the PIM logs, and provisioning logs to ensure that the group membership was updated successfully. Depending on how the target application is architected, it might take more time for the group membership to take effect in the application.
- You can create alerts for failures using [Azure Monitor](/en-us/entra/identity/app-provisioning/application-provisioning-log-analytics).

## Change log

- 10/17/2020 - Added support for more G Suite user and group attributes.
- 10/17/2020 - Updated G Suite target attribute names to match what is defined [here](https://developers.google.com/admin-sdk/directory).
- 10/17/2020 - Updated default attribute mappings.