---
layout: Conceptual
title: Troubleshoot B2B issues - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to troubleshoot common issues with Microsoft Entra B2B collaboration. Resolve guest sign-in errors, direct connect access problems, policy update failures, and encrypted email access issues.
ms.topic: troubleshooting
ms.date: 2025-02-19T00:00:00.0000000Z
tags: active-directory
ms.custom: it-pro, no-azure-ad-ps-ref
ms.collection: M365-identity-device-management
locale: en-us
document_id: 3f76cc85-8dc0-9be3-4071-217589ddef56
document_version_independent_id: e7bdba65-bacc-7fef-2c27-b3425f697b12
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 9dde6114-9f73-aa2b-8e4e-0dc5c1b2f76d
---

# Troubleshoot B2B issues - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Here are some remedies for common problems with Microsoft Entra B2B collaboration.

## Guest sign-in fails with error code AADSTS50020

When a guest user from an identity provider (IdP) can't sign in to a resource tenant in Microsoft Entra ID and receives an error code AADSTS50020, there are several possible causes. See the troubleshooting article for error [AADSTS50020](/en-us/troubleshoot/azure/active-directory/error-code-aadsts50020-user-account-identity-provider-does-not-exist).

## B2B direct connect user is unable to access a shared channel (error AADSTS90071)

When a B2B direct connect sees the following error message when trying to access another organization's Teams shared channel, multifactor authentication trust settings haven't been configured by the external organization:

> 
> The organization you're trying to reach needs to update their settings to let you sign in.
> 
> AADSTS90071: An admin from *&lt;organization&gt;* must update their access settings to accept inbound multifactor authentication.

The organization hosting the Teams shared channel must enable the trust setting for multifactor authentication to allow access to B2B direct connect users. Trust settings are configurable in an organization's [cross-tenant access settings](cross-tenant-access-settings-b2b-direct-connect).

## An error similar to "Failure to update policy due to object limit" appears while configuring cross-tenant access settings

As you configure [cross-tenant access settings](cross-tenant-access-settings-b2b-collaboration), if you receive an error that says “Failure to update policy due to object limit,” you've reached the policy object limit of 25 KB. We're working toward increasing this limit. If you need to be able to calculate how close the current policy is to this limit, do the following:

1. Open Microsoft Graph Explorer and run the following:

    `GET https://graph.microsoft.com/beta/policies/crosstenantaccesspolicy`
2. Copy the entire JSON response and save it as a txt file, for example `policyobject.txt`.
3. Open PowerShell and run the following script, substituting the file location in the first line with your text file:

```powershell
$policy = Get-Content “C:\policyobject.txt”
$maxSize = 1024*25 
$size = [System.Text.Encoding]::UTF8.GetByteCount($policy) 
write-host "Remaining Bytes available in policy object" 
$maxSize - $size 
write-host "Is current policy within limits?" 
if ($size -le $maxSize) { return “valid” }; else { return “invalid” } 
```

## Users can no longer read email encrypted with Microsoft Rights Management Service (OME))

As you configure [cross-tenant access settings](cross-tenant-access-settings-b2b-collaboration), if you block access to all apps by default, users will be unable to read emails encrypted with Microsoft Rights Management Service (also known as OME). To avoid this issue, we recommend configuring your outbound settings to allow your users to access this app ID: 00000012-0000-0000-c000-000000000000. If this is the only application you allow, access to all other apps will be blocked by default.

## I’ve added an external user but don't see them in my Global Address Book or in the people picker

In cases where external users aren't populated in the list, the object might take a few minutes to replicate.

## A B2B guest user isn't showing up in SharePoint Online/OneDrive people picker

The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.

You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level. You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory. Changes in the tenant scope don't affect already provisioned SPO sites.

## My guest invite settings and domain restrictions aren't being respected by SharePoint Online/OneDrive

By default, SharePoint Online and OneDrive have their own set of external user options and don't use the settings from Microsoft Entra ID. You need to enable [SharePoint and OneDrive integration with Microsoft Entra B2B](/en-us/sharepoint/sharepoint-azureb2b-integration) to ensure the options are consistent among those applications.

## Invitations have been disabled for directory

If you're notified that you don't have permissions to invite users, verify that your user account is authorized to invite external users under Microsoft Entra ID &gt; Users &gt; User settings &gt; External users &gt; Manage external collaboration settings:

![Screenshot showing the External User settings.](media/troubleshoot/external-user-settings.png)

If you've recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.

## The user that I invited is receiving an error during the redemption process

Common errors include:

### Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant

When inviting users whose organization is using Microsoft Entra ID, but where the specific user’s account doesn't exist (for example, the user doesn't exist in Microsoft Entra contoso.com). The administrator of contoso.com may have a policy in place preventing users from being created. The user must check with their admin to determine if external users are allowed. The external user’s admin may need to allow Email Verified users in their domain (see this [article](/en-us/powershell/module/microsoft.graph.identity.signins/update-mgpolicyauthorizationpolicy) on allowing Email Verified Users).

![Screenshot of the error stating the tenant doesn't allow email verified users.](media/troubleshoot/allow-email-verified-users.png)

### External user doesn't exist already in a federated domain

If you're using federation authentication and the user doesn't already exist in Microsoft Entra ID, the user can't be invited.

To resolve this issue, the external user’s admin must synchronize the user’s account to Microsoft Entra ID.

### External user has a proxyAddress that conflicts with a proxyAddress of an existing local user

When we check whether a user is able to be invited to your tenant, one of the things we check for is for a collision in the proxyAddress. This includes any proxyAddresses for the user in their home tenant and any proxyAddress for local users in your tenant. For external users, we'll add the email to the proxyAddress of the existing B2B user. For local users, you can ask them to sign in using the account they already have.

## I can't invite an email address because of a conflict in proxyAddresses

This happens when another object in the directory has the same invited email address as one of its proxyAddresses. The other conflicting object could be a User, Group, or Microsoft 365 Contact.

To fix this conflict, search for the email address in the Microsoft 365 admin center to find the conflicting object. You must remove the email address using the Microsoft Graph API.

To fix this conflict:

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com).
2. Browse to **Users** &gt; **All users** and search for the email address that you're trying to invite.
3. Remove the email from the [Microsoft Graph user](/en-us/graph/api/resources/user) object.
4. Browse to **Users** &gt; **Contacts** to see if there's a contact using that email address.
5. Remove the associated [Microsoft Graph contact](/en-us/graph/api/resources/contact) object.
6. Browse to **Teams & groups** &gt; **Active teams & groups** and search for the email address that you're trying to invite, and change the email address if found.

Once you've removed the conflicting email address, you can invite the user.

## On a guest user object, the proxyAddresses or email attribute isn't populated

When you add or invite a guest with an email that matches an existing [Contact object](/en-us/graph/api/resources/contact) in the directory, the proxyAddresses property on the guest user object isn't populated. Also, when synchronizing contact objects from on-premises AD, if a guest user has a matching proxyAddresses property, the conflicting proxyAddresses property is removed from the existing guest user.

The invitation redemption process has been updated so that this scenario no longer causes issues with [just-in-time redemption](redemption-experience#redemption-process-through-a-direct-link) or [email one-time passcode authentication](one-time-passcode#user-experience-for-one-time-passcode-guest-users). Previously, External ID searched only the proxyAddresses property, so redemption with a direct link or one-time passcode failed when it couldn’t find a match. Now, External ID searches the proxyAddresses and invited email properties.

If you want to identify conflicting user objects in your directory, use these PowerShell steps:

1. Open the Microsoft Graph PowerShell module and run `Connect-MgGraph`.
2. Sign in as at least a [Directory Reader](/en-us/entra/identity/role-based-access-control/permissions-reference?branch=main#directory-readers) to the Microsoft Entra tenant for which you want to check for duplicate contact objects.
3. Run the PowerShell command `Get-MgContact -All | ? {$_.Mail -match 'user@domain.com'}`.

## How does ‘#’, which isn't normally a valid character, sync with Microsoft Entra ID?

“#” is a reserved character in UPNs for Microsoft Entra B2B collaboration or external users, because the invited account user@contoso.com becomes user\_contoso.com#EXT#@fabrikam.onmicrosoft.com. Therefore, # in UPNs coming from on-premises aren't allowed to sign in to the Microsoft Entra admin center.

## I receive an error when adding external users to a synchronized group

External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.

## My external user didn't receive an email to redeem

The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com.

Note

- For the Azure service operated by 21Vianet in China, the sender address is Invites@oe.21vianet.com.
- For the Microsoft Entra Government cloud, the sender address is invites@azuread.us.

## I notice that the custom message doesn't get included with invitation messages at times

To comply with privacy laws, our APIs don't include custom messages in the email invitation when:

- The inviter doesn’t have an email address in the inviting tenant
- When an appservice principal sends the invitation

If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice. Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.

## You receive an “AADSTS65005” error when you try to sign in to an Azure resource

A user who has a guest account can't sign in, and is receiving the following error message:

```plaintext
    AADSTS65005: Using application 'AppName' is currently not supported for your organization contoso.com because it is in an unmanaged state. An administrator needs to claim ownership of the company by DNS validation of contoso.com before the application AppName can be provisioned.
```

The user has an Azure user account and is a viral tenant who has been abandoned or unmanaged. Additionally, there are no administrators in the tenant.

To resolve this problem, you must take over the abandoned tenant. Refer to [Take over an unmanaged directory as administrator in Microsoft Entra ID](../identity/users/domains-admin-takeover). You must also access the internet-facing DNS for the domain suffix in question in order to provide direct evidence that you are in control of the namespace. After the tenant is returned to a managed state, discuss with the customer whether leaving the users and verified domain name is the best option for their organization.

## A guest user with a just-in-time or "viral" tenant is unable to reset their password

If the identity tenant is a just-in-time (JIT) or viral tenant (meaning it's a separate, unmanaged Azure tenant), only the guest user can reset their password. Sometimes an organization will [take over management of viral tenants](../identity/users/domains-admin-takeover) that are created when employees use their work email addresses to sign up for services. After the organization takes over a viral tenant, only an administrator in that organization can reset the user's password or enable SSPR. If necessary, as the inviting organization, you can remove the guest user account from your directory and resend an invitation.

## In an Azure US Government tenant, I can't invite a B2B collaboration guest user

Within the Azure US Government cloud, B2B collaboration is enabled between tenants that are both within Azure US Government cloud and that both support B2B collaboration. If you invite a user in a tenant that doesn't yet support B2B collaboration, you'll get an error. For details and limitations, see [Microsoft Entra ID P1 and P2 Variations](/en-us/azure/azure-government/compare-azure-government-global-azure#azure-active-directory-premium-p1-and-p2).

If you need to collaborate with a Microsoft Entra organization that's outside of the Azure US Government cloud, you can use [Microsoft cloud settings](cross-cloud-settings) to enable B2B collaboration.

## Invitation is blocked due to cross-tenant access policies

When you try to invite a B2B collaboration user, you might see this error message: "This invitation is blocked by cross-tenant access settings. Admins in both your organization and the invited user's organization must configure cross-tenant access settings to allow the invitation." This error message will appear, if B2B collaboration is supported, but is blocked by cross-tenant access settings. Check your cross-tenant access settings, and make sure that your settings allow B2B collaboration with the user. When you try to collaborate with another Microsoft Entra organization in a separate Microsoft Azure cloud, you can use [Microsoft cloud settings](cross-cloud-settings) to enable Microsoft Entra B2B collaboration.

## Invitation is blocked due to disabled Microsoft B2B Cross Cloud Worker application

Rarely, you might see this message: “This action can't be completed because the Microsoft B2B Cross Cloud Worker application has been disabled in the invited user’s tenant. Ask the invited user’s admin to re-enable it, then try again.” This error means that the Microsoft B2B Cross Cloud Worker application has been disabled in the B2B collaboration user’s home tenant. This app is typically enabled, but it might have been disabled by an admin in the user’s home tenant, either through PowerShell or the Microsoft Entra admin center (see [Disable how a user signs in](../identity/enterprise-apps/disable-user-sign-in-portal)). An admin in the user’s home tenant can re-enable the app through PowerShell or the Microsoft Entra admin center. In the admin center, search for “Microsoft B2B Cross Cloud Worker” to find the app, select it, and then choose to re-enable it.

## I receive the error that Microsoft Entra ID can't find the `aad-extensions-app` in my tenant

When you're using self-service sign-up features, like custom user attributes or user flows, an app called `aad-extensions-app. Do not modify. Used by AAD for storing user data.` is automatically created. It's used by Microsoft Entra External ID to store information about users who sign up and custom attributes collected.

If you accidentally deleted the `aad-extensions-app`, you have 30 days to recover it. You can restore the app using the Microsoft Graph PowerShell module.

1. Launch the Microsoft Graph PowerShell module and run `Connect-MgGraph`.
2. Sign in as at least an [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) to the Microsoft Entra tenant for which you want to recover the deleted app.
3. Run the PowerShell command `Get-MgDirectoryDeletedItem -DirectoryObjectId {id}`. As an example:

```powershell
Get-MgDirectoryDeletedItem -DirectoryObjectId '00aa00aa-bb11-cc22-dd33-44ee44ee44ee'
Id                                   DeletedDateTime
--                                   ---------------
00aa00aa-bb11-cc22-dd33-44ee44ee44ee 8/30/2021 7:37:37 AM
```

1. Run the PowerShell command `Restore-MgDirectoryDeletedItem -DirectoryObjectId {id}`. Replace the `{id}` portion of the command with the `DirectoryObjectId` from the previous step.

You should now see the restored app in the Microsoft Entra admin center.

## External access blocked by policy error on the login screen

When you try to log in to your tenant, you might see this error message: "Your network administrator has restricted what organizations can be accessed. Contact your IT department to unblock access." This error is related to tenant restriction settings. To resolve this issue, ask your IT team to follow the instructions in [this article](../identity/enterprise-apps/tenant-restrictions).

## Users get in a loop when they try to add passkey in Authenticator

Organizations that are deploying passkeys and have Conditional Access policies that require phishing-resistant authentication when accessing **All resources (formerly 'All cloud apps')** can run into a looping issue when users attempt to add a passkey to Microsoft Authenticator. For more information and possible workarounds, see [Workarounds for an authentication strength Conditional Access policy loop](../identity/authentication/how-to-enable-authenticator-passkey#workarounds-for-an-authentication-strength-conditional-access-policy-loop).

## Invitation is blocked due missing cross-tenant access settings

You might see this message: "This invitation is blocked by cross-tenant access settings in your organization. Your administrator must configure cross-tenant access settings to allow this invitation." In this case, ask your administrator to check the cross-tenant access settings.