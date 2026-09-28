---
layout: Conceptual
title: Troubleshoot publisher verification - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/troubleshoot-publisher-verification
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Describes how to troubleshoot publisher verification for the Microsoft identity platform by calling Microsoft Graph APIs.
manager: dougeby
ms.date: 2024-07-19T00:00:00.0000000Z
ms.topic: troubleshooting
ms.custom: sfi-ga-nochange
locale: en-us
document_id: df11cb03-70da-7df3-4941-3c2f8ea022f8
document_version_independent_id: 96cd8eec-ed94-05bf-1288-86b6ef3db105
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/troubleshoot-publisher-verification.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/troubleshoot-publisher-verification
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/troubleshoot-publisher-verification.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 3824e199-feff-edd7-ae5f-418081ac07ea
---

# Troubleshoot publisher verification - Microsoft identity platform | Microsoft Learn

If you're unable to complete the process, see error messages, or experience unexpected behavior with [publisher verification](publisher-verification-overview), follow these steps to troubleshoot the issue:

1. Review the [requirements](publisher-verification-overview#requirements) and ensure they've all been met.
2. Review the instructions to [mark an app as publisher verified](mark-app-as-publisher-verified) and ensure all steps have been performed successfully.
3. Review the list of common issues.
4. Reproduce the request using Graph Explorer to gather more info and rule out any issues in the UI.

## Common issues

Here are some common issues that may occur during the process of publisher verification:

- **I don't know my Cloud Partner Program ID (Partner One ID) or I don't know who the primary contact for the account is.**

    1. Navigate to the [Cloud Partner Program enrollment page](https://partner.microsoft.com/dashboard/account/v3/enrollment/joinnow/basicpartnernetwork/new).
    2. Sign in with a user account in the org's primary Microsoft Entra tenant.
    3. If a Cloud Partner Program account already exists, this account is recognized and you are added to the account.
    4. Navigate to the [partner profile page](https://partner.microsoft.com/dashboard/account/v3/overview) where the Partner One ID and primary account contact are listed.
- **I don't know who my Microsoft Entra Global Administrator (also known as company admin or tenant admin) is, how do I find them? What about the Application Administrator or Cloud Application Administrator?**

    1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
    2. Browse to **Entra ID** &gt; **Roles & admins**.
    3. Select the desired admin role.
    4. The list of users assigned that role are displayed.
- **I don't know who the admin(s) for my CPP account are** Go to the [CPP User Management page](https://partner.microsoft.com/dashboard/account/v3/usermanagement) and filter the user list to see what users are in various admin roles.
- **I am getting an error saying that my Partner One ID is invalid or that I do not have access to it.** Follow the remediation guidance.
- **When I sign in to the Microsoft Entra admin center, I do not see any apps registered. Why?** Your app registrations may have been created using a different user account in this tenant, a personal/consumer account, or in a different tenant. Ensure you're signed in with the correct account in the tenant where your app registrations were created.
- **I'm getting an error related to multi-factor authentication. What should I do?** Ensure [multifactor authentication](../identity/authentication/concept-mfa-licensing) is enabled and **required** for the user you're signing in with and for this scenario. For example, MFA could be:

    - Always required for the user you're signing in with.
    - [Required for Azure management](../identity/conditional-access/policy-old-require-mfa-azure-mgmt).
    - [Required for the type of administrator](../identity/conditional-access/policy-old-require-mfa-admin) you're signing in with.

## Making Microsoft Graph API calls

If you're having an issue but unable to understand why based on what you are seeing in the UI, it may be helpful to perform further troubleshooting by using Microsoft Graph calls to perform the same operations you can perform in the App Registration portal.

The easiest way to make these requests is to use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer). You may also consider other options like PowerShell to [invoke a web request](/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest).

You can use Microsoft Graph to both set and unset your app’s verified publisher and check the result after performing one of these operations. The result can be seen on both the [application](/en-us/graph/api/resources/application) object corresponding to your app registration and any [service principals](/en-us/graph/api/resources/serviceprincipal) that have been instantiated from that app. For more information on the relationship between those objects, see: [Application and service principal objects in Microsoft Entra ID](app-objects-and-service-principals).

Here are examples of some useful requests:

### Set Verified Publisher

Request

```
POST /applications/00001111-aaaa-2222-bbbb-3333cccc4444/setVerifiedPublisher 

{ 

    "verifiedPublisherId": "12345678" 

} 
```

Response

```
204 No Content 
```

Note

*verifiedPublisherID* is your Partner One ID.

### Unset Verified Publisher

Request:

```
POST /applications/00001111-aaaa-2222-bbbb-3333cccc4444/unsetVerifiedPublisher 
```

Response

```
204 No Content 
```

### Get Verified Publisher info from Application

```
GET https://graph.microsoft.com/v1.0/applications/00001111-aaaa-2222-bbbb-3333cccc4444 

HTTP/1.1 200 OK 

{ 
    "id": "00001111-aaaa-2222-bbbb-3333cccc4444", 

    ... 

    "verifiedPublisher" : { 
        "displayName": "myexamplePublisher", 
        "verifiedPublisherId": "12345678", 
        "addedDateTime": "2019-12-10T00:00:00" 
    } 
} 
```

### Get Verified Publisher info from Service Principal

```
GET https://graph.microsoft.com/v1.0/servicePrincipals/11112222-bbbb-3333-cccc-4444dddd5555

HTTP/1.1 200 OK 

{ 
    "id": "11112222-bbbb-3333-cccc-4444dddd5555", 

    ... 

    "verifiedPublisher" : { 
        "displayName": "myexamplePublisher", 
        "verifiedPublisherId": "12345678", 
        "addedDateTime": "2019-12-10T00:00:00" 
    } 
} 
```

## Error Reference

The following list shows the potential error codes you may receive, either when troubleshooting with Microsoft Graph or going through the process in the app registration portal.

### MPNAccountNotFoundOrNoAccess

The Partner One ID you provided (`MPNID`) doesn't exist or you don't have access to it. Provide a valid Partner One ID and try again.

Most commonly caused by the signed-in user not being a member of the proper role for the CPP account in Partner Center. See [requirements](publisher-verification-overview#requirements) for a list of eligible roles and see common issues for more info. This error may also be due to the tenant (where the app is registered in) not being added to the CPP account, or an invalid Partner One ID.

**Remediation Steps**

1. Go to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile) and verify that:

    - The Partner One ID is correct.
    - There are no errors or "pending actions" shown, and the verification status under Legal business profile and Partner info both say "authorized" or "success".
2. Go to the [CPP tenant management page](https://partner.microsoft.com/dashboard/account/v3/tenantmanagement) and confirm that the tenant the app is registered in and that you're signing with a user account from is on the list of associated tenants. To add another tenant, follow the [multi-tenant-account instructions](/en-us/partner-center/multi-tenant-account). All Global Administrators of any tenant you add are granted Global Administrator privileges on your Partner Center account.
3. Go to the [CPP User Management page](https://partner.microsoft.com/pcv/users) and confirm the user you're signing in as is either a Global Administrator, MPN Admin, or Accounts Admin. To add a user to a role in Partner Center, follow the instructions for [creating user accounts and setting permissions](/en-us/partner-center/create-user-accounts-and-set-permissions).

### MPNGlobalAccountNotFound

The Partner One ID you provided (`MPNID`) isn't valid. Provide a valid Partner One ID and try again.

Most commonly caused when a Partner One ID is provided which corresponds to a Partner Location Account (PLA). Only Partner Global Accounts are supported. See [Partner Center account structure](/en-us/partner-center/account-structure) for more details.

**Remediation Steps**

1. Navigate to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile) &gt; **Identifiers blade** &gt; **Microsoft Cloud Partners Program Tab**.
2. Use the Partner ID with type PartnerGlobal.

### MPNAccountInvalid

The Partner One ID you provided (`MPNID`) isn't valid. Provide a valid Partner One ID and try again.

Most commonly caused by the wrong Partner One ID being provided.

**Remediation Steps**

1. Navigate to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile) &gt; **Identifiers blade** &gt; **Microsoft Cloud Partners Program Tab**.
2. Use the Partner ID with type PartnerGlobal.

### MPNAccountNotVetted

The Partner One ID (`MPNID`) you provided hasn't completed the vetting process. Complete this process in Partner Center and try again.

Most commonly caused by when the CPP account hasn't completed the [verification](/en-us/partner-center/verification-responses) process.

**Remediation Steps**

1. Navigate to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile) and verify that there are no errors or **pending actions** shown, and that the verification status under Legal business profile and Partner info both say **authorized** or **success**.
2. If not, view pending action items in Partner Center and troubleshoot with [here](/en-us/partner-center/verification-responses).

### NoPublisherIdOnAssociatedMPNAccount

The Partner One ID you provided (`MPNID`) isn't valid. Provide a valid Partner One ID and try again.

Most commonly caused by the wrong Partner One ID being provided.

**Remediation Steps**

1. Navigate to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile) &gt; **Identifiers blade** &gt; **Microsoft Cloud Partners Program Tab**.
2. Use the Partner ID with type PartnerGlobal.

### MPNIdDoesNotMatchAssociatedMPNAccount

The Partner One ID you provided (`MPNID`) isn't valid. Provide a valid Partner One ID and try again.

Most commonly caused by the wrong Partner One ID being provided.

**Remediation Steps**

1. Navigate to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile) &gt; **Identifiers blade** &gt; **Microsoft Cloud Partners Program Tab**.
2. Use the Partner ID with type PartnerGlobal.

### ApplicationNotFound

The target application (`AppId`) can't be found. Provide a valid application ID and try again.

Most commonly caused when verification is being performed via Graph API, and the ID of the application provided is incorrect.

**Remediation Steps**

1. The Object ID of the application must be provided, not the AppId/ClientId. See **id** on the list of application properties [here](/en-us/graph/api/resources/application).
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
3. Browse to **Entra ID** &gt; **App registrations**.
4. Find your app's registration to view the Object ID.

### ApplicationObjectisInvalid

The target application's object ID is invalid. Provide a valid ID and try again.

Most commonly caused when the verification is being performed via Graph API, and the ID of the application provided does not exist.

**Remediation Steps**

1. The Object ID of the application must be provided, not the AppId/ClientId. See **id** on the list of application properties [here](/en-us/graph/api/resources/application).
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
3. Browse to **Entra ID** &gt; **App registrations**.
4. Find your app's registration to view the Object ID.

### B2CTenantNotAllowed

This capability isn't supported in an Azure AD B2C tenant.

### EmailVerifiedTenantNotAllowed

This capability isn't supported in an email verified tenant.

### NoPublisherDomainOnApplication

The target application (`AppId`) must have a Publisher Domain set. Set a Publisher Domain and try again.

Occurs when a [Publisher Domain](howto-configure-publisher-domain) isn't configured on the app.

**Remediation Steps** Follow the directions [here](howto-configure-publisher-domain) to set a Publisher Domain.

### PublisherDomainMismatch

The target application's Publisher Domain (`publisherDomain`) either doesn't match the domain used to perform email verification in Partner Center (`pcDomain`) or has not been verified. Ensure these domains match and have been verified then try again.

Occurs when neither the app's [Publisher Domain](howto-configure-publisher-domain) nor one of the [custom domains](../fundamentals/add-custom-domain) added to the Microsoft Entra tenant match the domain used to perform email verification in Partner Center or has not been verified.

See [requirements](publisher-verification-overview) for a list of allowed domain or sub-domain matches.

**Remediation Steps**

1. Navigate to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile), and view the email listed as Primary Contact
2. The domain used to perform email verification in Partner Center is the portion after the "@" in the Primary Contact's email
3. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
4. Browse to **Entra ID** &gt; **App registrations** &gt; **Branding and Properties**.
5. Select **Update Publisher Domain** and follow the instructions to **Verify a New Domain**.
6. Add the domain used to perform email verification in Partner Center as a New Domain.

### NotAuthorizedToVerifyPublisher

You aren't authorized to set the verified publisher property on application (&lt;`AppId`).

Most commonly caused by the signed-in user not being a member of the proper role for the CPP account in Microsoft Entra ID - see [requirements](publisher-verification-overview#requirements) for a list of eligible roles and see common issues for more information.

**Remediation Steps**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Roles & admins**.
3. Select the desired admin role and select **Add Assignment** if you have sufficient permissions.
4. If you do not have sufficient permissions, contact an admin role for assistance.

### MPNIdWasNotProvided

The Partner One ID wasn't provided in the request body or the request content type wasn't "application/json".

Most commonly caused when the verification is being performed via Graph API, and the Partner One ID wasn’t provided in the request.

**Remediation Steps**

1. Navigate to your [partner profile](https://partner.microsoft.com/pcv/accountsettings/connectedpartnerprofile) &gt; **Identifiers blade** &gt; **Microsoft Cloud Partners Program Tab**.
2. Use the Partner ID with type PartnerGlobal in the request.

### MSANotSupported

This feature isn't supported for Microsoft consumer accounts. Only applications registered in Microsoft Entra ID by a Microsoft Entra user are supported.

Occurs when a consumer account is used for app registration (Hotmail, Messenger, OneDrive, MSN, Xbox Live, or Microsoft 365).

### InteractionRequired

Occurs when multifactor authentication (MFA) hasn't been enabled and performed before attempting to add a verified publisher to the app. See common issues for more information. Note: MFA must be performed in the same session when attempting to add a verified publisher. If MFA is enabled but not required to be performed in the session, the request fails.

The error message displayed is: "Due to a configuration change made by your administrator, or because you moved to a new location, you must use multifactor authentication to proceed."

**Remediation Steps**

1. Ensure [multifactor authentication](../identity/authentication/concept-mfa-licensing) is enabled and **required** for the user you're signing in with and for this scenario
2. Retry Publisher Verification

### UserUnableToAddPublisher

Error: "You're unable to add a verified publisher to this application. Contact your administrator for assistance."

When a request to add a verified publisher is made, many signals are used to make a security risk assessment. If the user risk state is determined to be ‘AtRisk’, the above error is returned. Investigate the user risk and take the appropriate steps to remediate the risk (guidance below):

**Remediation Steps**

> 
> [Investigate risk](../id-protection/howto-identity-protection-investigate-risk)
> 
> [Remediate risk/unblock users](../id-protection/howto-identity-protection-remediate-unblock)
> 
> [Self-remediation guidance](../id-protection/howto-identity-protection-remediate-unblock)
> 
> Self-serve password reset (SSPR): If the organization allows SSPR, use aka.ms/sspr to reset the password for remediation. Please choose a strong password; Choosing a weak password may not reset the risk state.

Note

Please give some time after remediation for the risk state to update, and then try again.

### UnableToAddPublisher

Error: "A verified publisher cannot be added to this application. Please contact your administrator for assistance."

When a request to add a verified publisher is made, many signals are used to make a security risk assessment. If a request is determined to be risky, the above error is returned. For security reasons, Microsoft doesn't disclose the specific criteria used to determine whether a request is risky or not.

**Remediation Steps**

> 
> If you believe the "risky" assessment is incorrect, try resubmitting the verification request the next day. It may take some time for the risk state to update.