---
layout: Conceptual
title: Troubleshoot problems signing in to an application from My Apps portal - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/application-sign-in-other-problem-access-panel
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Troubleshoot problems signing in to an application from Microsoft Entra My Apps
ms.topic: troubleshooting
ms.date: 2023-09-05T00:00:00.0000000Z
ms.reviewer: lenalepa
ms.custom: enterprise-apps
locale: en-us
document_id: bda92353-1dd8-a0d4-1326-de8112b3f311
document_version_independent_id: a4df7077-40a2-6686-55c2-5b62e4669cfb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/application-sign-in-other-problem-access-panel.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/application-sign-in-other-problem-access-panel
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/application-sign-in-other-problem-access-panel.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 3dcfd551-aa46-f190-fd06-99fb574972f4
---

# Troubleshoot problems signing in to an application from My Apps portal - Microsoft Entra ID | Microsoft Learn

My Apps is a web-based portal that enables a user with a work or school account in Microsoft Entra ID to view and start cloud-based applications that the Microsoft Entra administrator has granted them access to. My Apps is accessed using a web browser at https://myapps.microsoft.com.

To learn more about using Microsoft Entra ID as an identity provider for an app, see the [What is Application Management in Microsoft Entra ID](what-is-application-management). To get up to speed quickly, check out the [Quickstart Series on Application Management](view-applications-portal).

These applications are configured on behalf of the user in the Microsoft Entra admin center. The application must be configured properly and assigned to the user or a group the user is a member of to see the application in My Apps.

The type of apps a user may be seeing fall in the following categories:

- Microsoft 365 Applications
- Microsoft and third-party applications configured with federation-based SSO
- Password-based SSO applications
- Applications with existing SSO solutions

Here are some things to check if an app is appearing or not appearing:

- Make sure the app is added to Microsoft Entra ID and make sure the user is assigned. To learn more, see the [Quickstart Series on Application Management](add-application-portal).
- If an app was recently added, have the user sign out and back in again.
- If the app requires a license, such as Office, then make sure the user is assigned the appropriate license.
- The time it takes for licensing changes can vary depending on the size and complexity of the group.

## General issues to check first

- Make sure the web browser meets the requirements, see [My Apps supported browsers](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).
- Make sure the user’s browser has added the URL of the application to its **trusted sites**.
- Make sure to check the application is **configured** correctly.
- Make sure the user’s account is **enabled** for sign-ins.
- Make sure the user’s account is **not locked out.**
- Make sure the user’s **password is not expired or forgotten.**
- Make sure **Multi-Factor Authentication** isn't blocking user access.
- Make sure a **Conditional Access policy** or **legacy Identity Protection** policy isn't blocking user access.
- Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.
- Make sure to also try clearing your browser’s cookies and trying to sign in again.

## Problems with the user’s account

Access to My Apps can be blocked due to a problem with the user’s account. Following are some ways you can troubleshoot and solve problems with users and their account settings:

- Check if a user account exists in Microsoft Entra ID
- Check a user’s account status
- Reset a user’s password
- Enable self-service password reset
- Check a user’s multi-factor authentication status
- Check a user’s authentication contact info
- Check a user’s group memberships
- Check if a user has more than 999 app role assignments
- Check a user’s assigned licenses
- Assign a user a license

### Check if a user account exists in Microsoft Entra ID

To check if a user’s account is present, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for the user you're interested in and select the row to view the details of the user.
4. Check the properties of the user object to be sure that they look as you expect and no data is missing.

### Check a user’s account status

To check a user’s account status, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for the user you're interested in and select the row with the user's details.
4. Select **Profile**.
5. Under **Settings** ensure that **Block sign in** is set to **No**.

### Reset a user’s password

To reset a user’s password, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for the user you're interested in and select the row with the user's details.
4. Select the **Reset password** button at the top of the user pane.
5. Select the **Reset password** button on the **Reset password** pane that appears.
6. Copy the **temporary password** or **enter a new password** for the user.
7. Communicate this new password to the user. They might be required to change this password during their next sign-in to Microsoft Entra ID.

### Enable self-service password reset

To enable self-service password reset, follow these deployment steps:

- [Enable users to reset their Microsoft Entra passwords](../authentication/tutorial-enable-sspr)
- [Enable users to reset or change their Active Directory on-premises passwords](../authentication/tutorial-enable-sspr)

### Check a user’s multi-factor authentication status

To check a user’s multi-factor authentication status, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select the **Per-user MFA** button at the top of the pane.
4. Once the **Multi-Factor Authentication** administration portal loads, ensure you are on the **Users** tab.
5. Find the user in the list of users by searching, filtering, or sorting.
6. Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired. 
    Note

    If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account. Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign-in. Alternatively, you can follow the steps in the Check a user’s authentication contact info to verify or set this data for them.

### Check a user’s authentication contact info

To check a user’s authentication contact info used for multifactor authentication, Conditional Access, and Password Reset, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for the user you're interested in and select the row with the user's details.
4. Select **Authentication method** under **Manage**.
5. **Review** the data registered for the user and update as needed.

### Check a user’s group memberships

To check a user’s group memberships, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for the user you're interested in and select the row with the user's details.
4. Select **Groups** to see which groups the user is a member of.

### Check if a user has more than 999 app role assignments

If a user has more than 999 app role assignments, then they may not see all of their apps on My Apps.

This is because My Apps currently reads up to 999 app role assignments to determine the apps to which users are assigned. If a user is assigned to more than 999 apps, it isn't possible to control which of those apps show in the My Apps portal.

To check if a user has more than 999 app role assignments, follow these steps:

1. Install the [**Microsoft.Graph**](https://github.com/microsoftgraph/msgraph-sdk-powershell) PowerShell module.
2. Run `Connect-MgGraph -Scopes "User.ReadBasic.All Application.Read.All"`and sign in as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator)..
3. Run `(Get-MgUserAppRoleAssignment -UserId "<user-id>" -PageSize 999).Count` to determine the number of app role assignments the user currently has granted.
4. If the result is 999, the user likely has more than 999 app roles assignments.

### Check a user’s assigned licenses

To check a user’s assigned licenses, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for the user you're interested in and select the row with the user's details.
4. Select **Licenses** to see which licenses the user currently has assigned.

### Assign a user a license

To assign a license to a user, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [user administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Search for the user you're interested in and select the row with the user's details.
4. Select **Licenses** to see which licenses the user currently has assigned.
5. Select the **Assignments** button.
6. Select one or more licenses from the list of available products.
7. Optional: Select **Review license options** to granularly assign products.
8. Select **Save**.

## Troubleshooting deep links

Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars. By navigating to this link, users are automatically signed into the application without having to go to My Apps first. The link is the same one that users use to access these applications from the Microsoft 365 application launcher.

### Checking the deep link

To check if you have the correct deep link, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**.
3. Enter the name of the existing application in the search box, and then select the application from the search results.
4. Find the label **User Access URL**. Your deep link should match this URL.

## Contact support

Open a support ticket with the following information if available:

- Correlation error ID
- UPN (user email address)
- TenantID
- Browser type
- Time zone and time/timeframe during error occurs
- Fiddler traces