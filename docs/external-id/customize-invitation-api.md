---
layout: Conceptual
title: B2B collaboration API and customization - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customize-invitation-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Microsoft Entra B2B collaboration supports your cross-company relationships by enabling business partners to selectively access your corporate applications.
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.topic: how-to
ms.date: 2024-12-10T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: 5cea15b5-0fca-d8ae-9423-4f4c91d7a9de
document_version_independent_id: 6f6159f1-8a56-7aa2-81ab-bf9e6c339a7d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customize-invitation-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customize-invitation-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customize-invitation-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 293d2658-a7c9-7c83-920d-daef1a10ca2c
---

# B2B collaboration API and customization - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

[With the Microsoft Graph REST API](/en-us/graph/api/resources/invitation), you can customize the invitation process in a way that works best for your organization.

## Capabilities of the invitation API

The API offers the following capabilities:

1. The following JSON representation shows how to invite an external user with *any* email address.

    ```
    "invitedUserDisplayName": "Taylor",
    "invitedUserEmailAddress": "taylor@fabrikam.com"
    ```
2. Customize where you want your users to land after they accept their invitation.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```
3. Choose to send the standard invitation mail through us.

    ```
    "sendInvitationMessage": true
    ```

    With a message to the recipient that you can customize.

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```
4. And choose to cc: people you want to keep in the loop about your inviting this collaborator.
5. Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Microsoft Entra ID.

    ```
    "sendInvitationMessage": false
    ```

    In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.
6. Finally, if you're an admin, you can choose to invite the user as member.

    ```
    "invitedUserType": "Member"
    ```

## Determine if a user was already invited to your directory

You can use the invitation API to determine if a user already exists in your resource tenant. This can be useful when you're developing an app that uses the invitation API to invite a user. If the user already exists in your resource directory, they won't receive an invitation, so you can run a query first to determine whether the email already exists as a UPN or other sign-in property.

1. Make sure the user's email domain isn't part of your resource tenant's verified domain.
2. In the resource tenant, use the following get user query where 0 is the email address you're inviting:

    ```
    “userPrincipalName eq '0' or mail eq '0' or proxyAddresses/any(x:x eq 'SMTP:0') or signInNames/any(x:x eq '0') or otherMails/any(x:x eq '0')" 
    ```

## Authorization model

The API can be run in the following authorization modes:

### App + User mode

In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.

### App only mode

In app only context, the app needs the User.Invite.All scope for the invitation to succeed.

For more information, see: https://developer.microsoft.com/graph/docs/authorization/permission_scopes

## PowerShell

You can use PowerShell to add and invite external users to an organization easily. Create an invitation using the cmdlet:

```powershell
New-MgInvitation
```

You can use the following options:

- -InvitedUserDisplayName
- -InvitedUserEmailAddress
- -SendInvitationMessage
- -InvitedUserMessageInfo

### Invitation status

After you send an external user an invitation, you can use the **Get-MgBetaUser** cmdlet to see if they've accepted it. The following properties of Get-MgBetaUser are populated when an external user is sent an invitation:

- **externalUserState** indicates whether the invitation is **PendingAcceptance** or **Accepted**.
- **externalUserStateChangeDateTime** shows the timestamp for the latest change to the **externalUserState** property.

You can use the **Filter** option to filter the results by **externalUserState**. The example below shows how to filter results to show only users who have a pending invitation. The example also shows the **Format-List** option, which lets you specify the properties to display.

```powershell
Get-MgBetaUser -Filter "externalUserState eq 'PendingAcceptance'" | Format-List -Property DisplayName,UserPrincipalName,externalUserState,externalUserStateChangeDateTime
```

Note

Make sure you have the latest version of the [Microsoft Graph PowerShell module](/en-us/powershell/microsoftgraph/overview)