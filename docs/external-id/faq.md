---
layout: FAQ
title: B2B collaboration FAQs - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/faq
summary: >
  <p><strong>Applies to</strong>: <img src="media/common/applies-to-yes.png" alt="Green circle with a white check mark symbol that indicates the following content applies to workforce tenants." /> Workforce tenants (<a href="/entra/external-id/tenant-configurations">learn more</a>)</p>

  <p>These frequently asked questions (FAQs) about Microsoft Entra business-to-business (B2B) collaboration are periodically updated to include new topics.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Get answers to frequently asked questions about Microsoft Entra B2B collaboration.
ms.topic: faq
ms.date: 2026-04-17T00:00:00.0000000Z
ms.custom: it-pro, has-azure-ad-ps-ref, azure-ad-ref-level-one-done
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 234804b8-f87e-6e42-3589-336b308c564f
document_version_independent_id: d6eca215-d352-50b0-994e-0077a5e54fe6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: b1bf21da-ac7c-2ddf-7532-c7257d376e23
---

# B2B collaboration FAQs - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

These frequently asked questions (FAQs) about Microsoft Entra business-to-business (B2B) collaboration are periodically updated to include new topics.

## What's changing in the guest user sign-in experience in B2B collaboration?

In July 2025, Microsoft began rolling out an update to the guest user sign-in experience for B2B collaboration. The rollout continued through the end of 2025. With this update, guest users are redirected to their own organization's sign-in page to provide credentials. Guest users see the branding and URL endpoint of their home tenant. This step gives clearer guidance about which sign-in information to use. After successful authentication in their own organization, guest users are returned to your organization to complete sign-in.

## Can B2B collaboration users access SharePoint Online and OneDrive?

Yes. However, the ability to search for existing guest users in SharePoint Online by using the people picker is **Off** by default. To turn on the option to search for existing guest users, set **ShowPeoplePickerSuggestionsForGuestUsers** to **On**. You can turn this setting on either at the tenant level or at the site collection level. You can change this setting by using the Set-SPOTenant and Set-SPOSite cmdlets. With these cmdlets, members can search all existing guest users in the directory. Changes in the tenant scope don't affect SharePoint Online sites that have already been provisioned.

## Can B2B collaboration users access Power BI content?

Yes, you can [distribute Power BI content to external guest users using B2B collaboration](/en-us/fabric/enterprise/powerbi/service-admin-entra-b2b). To share Power BI content across Microsoft clouds, you can [use Microsoft cloud settings](cross-tenant-access-overview#microsoft-cloud-settings) to establish mutual B2B collaboration between your cloud and an external cloud.

## Is the CSV upload feature still supported?

Yes. For more information about using the .csv file upload feature, see [this PowerShell sample](code-samples).

## How can I customize my invitation emails?

You can customize almost everything about the inviter process by using the [B2B invitation APIs](customize-invitation-api).

## Can guest users reset their multifactor authentication method?

Yes. Guest users can reset their multifactor authentication method the same way that regular users do.

## Which organization is responsible for multifactor authentication licenses?

The inviting organization performs multifactor authentication. The inviting organization must make sure that the organization has enough licenses for their B2B users who are using multifactor authentication.

## What if a partner organization already has multifactor authentication set up? Can we trust their multifactor authentication?

[Cross-tenant access settings](cross-tenant-access-overview) let you trust multifactor authentication and device claims ([compliant claims and Microsoft Entra hybrid joined claims](../identity/conditional-access/policy-alt-all-users-compliant-hybrid-or-mfa)) from other Microsoft Entra organizations.

## How many organizations can I add in cross-tenant access settings?

Cross-tenant access settings are a policy in the directory that stores your settings for how you collaborate with other organizations. There are no limits to the number of organizations you can add in cross-tenant access settings.

## How can I use delayed invitations?

An organization might want to add B2B collaboration users, provision them to applications as needed, and then send invitations. You can use the B2B collaboration invitation API to customize the onboarding workflow.

## Can I make guest users visible in the Exchange Global Address List?

Yes. By default, guest objects aren't visible in your organization's global address list, but you can make them visible. For details, see [Add guests to the global address list](/en-us/microsoft-365/solutions/per-group-guest-access#add-guests-to-the-global-address-list) in the Microsoft 365 per-group guest access article.

## Can I make a guest user a limited administrator?

Absolutely. For more information, see [Adding guest users to a role](add-users-administrator).

## Does Microsoft Entra B2B collaboration allow B2B users to access the Microsoft Entra admin center?

Unless a user is assigned the role of limited administrator, B2B collaboration users won't require access to the Microsoft Entra admin center. However, B2B collaboration users who are assigned the role of limited administrator can access the portal. Also, if a guest user who isn't assigned one of these admin roles accesses the portal, the user might be able to access certain parts of the experience. The guest user role has some permissions in the directory.

## Can I block access to the Microsoft Entra admin center for guest users?

Yes, you can create a Conditional Access policy that blocks guest user access to the admin center or portal. When configuring the Conditional Access policy, you have granular control over the types of external users you want to apply the policy to. When you configure this policy, be careful to avoid accidentally blocking access to members and admins. Learn more about [Conditional Access for external users](authentication-conditional-access#conditional-access-for-external-users).

## Does Microsoft Entra B2B collaboration support multifactor authentication and consumer email accounts?

Yes. Multifactor authentication and consumer email accounts are both supported for Microsoft Entra B2B collaboration.

## Do you support password reset for Microsoft Entra B2B collaboration users?

If your Microsoft Entra tenant is the home directory for a user, you can [reset the user's password](../fundamentals/users-reset-password-azure-portal) from the Microsoft Entra admin center. But you can't directly reset a password for a guest user who signs in with an account that's managed by another Microsoft Entra directory or external identity provider. Only the guest user or an administrator in the user’s home directory can reset the password. Here are some examples of how password reset works for guest users:

- Guest users in a Microsoft Entra tenant that are marked "Guest" (UserType==Guest) can't register for SSPR through https://aka.ms/ssprsetup. These type of guest user can only perform SSPR through https://aka.ms/sspr.
- Guest users who sign in with a Microsoft account (for example guestuser@live.com) can reset their own passwords using Microsoft account self-service password reset (SSPR). See [How to reset your Microsoft account password](https://support.microsoft.com/help/4026971/microsoft-account-how-to-reset-your-password).
- Guest users who sign in with a Google account or another external identity provider can reset their own passwords using their identity provider's SSPR method. For example, a guest user with the Google account guestuser@gmail.com can reset their password by following the instructions in [Change or reset your password](https://support.google.com/accounts/answer/41078).
- If the identity tenant is a just-in-time (JIT) or "viral" tenant (meaning it's a separate, unmanaged Azure tenant), only the guest user can reset their password. Sometimes an organization will [take over management of viral tenants](../identity/users/domains-admin-takeover) that are created when employees use their work email addresses to sign up for services. After the organization takes over a viral tenant, only an administrator in that organization can reset the user's password or enable SSPR. If necessary, as the inviting organization, you can remove the guest user account from your directory and resend an invitation.
- If the guest user's home directory is your Microsoft Entra tenant, you can reset the user's password. For example, you might have created a user or synced a user from your on-premises Active Directory and set their UserType to Guest. Because this user is homed in your directory, you can reset their password from the Microsoft Entra admin center.

## Does Microsoft Dynamics 365 provide online support for Microsoft Entra B2B collaboration?

Yes, Dynamics 365 (online) supports Microsoft Entra B2B collaboration. For more information, see the Dynamics 365 article [Invite users with Microsoft Entra B2B collaboration](/en-us/power-platform/admin/invite-users-azure-active-directory-b2b-collaboration).

## What is the lifetime of an initial password for a newly created B2B collaboration user?

Microsoft Entra ID has a fixed set of character, password strength, and account lockout requirements that apply equally to all Microsoft Entra cloud user accounts. Cloud user accounts are accounts that aren't federated with another identity provider, such as

- Microsoft account
- Facebook
- Active Directory Federation Services
- Another cloud tenant (for B2B collaboration)

For federated accounts, password policy depends on the policy that is applied in the on-premises tenancy and the user's Microsoft account settings.

## An organization might want to have different experiences in their applications for tenant users and guest users. Is there standard guidance for this? Is the presence of the identity provider claim the correct model to use?

A guest user can use any identity provider to authenticate. For more information, see [Properties of a B2B collaboration user](user-properties). Use the **UserType** property to determine user experience. The **UserType** claim isn't currently included in the token. Applications should use the Microsoft Graph API to query the directory for the user, and to get the UserType.

## Where can I find a B2B collaboration community to share solutions and to submit ideas?

We're constantly listening to your feedback, to improve B2B collaboration. Please share your user scenarios, best practices, and what you like about Microsoft Entra B2B collaboration. Join the discussion in the [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).

We also invite you to submit your ideas and vote for future features at [B2B Collaboration Ideas](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

## Can we send an invitation that is automatically redeemed, so that the user is just “ready to go”? Or does the user always have to click through to the redemption URL?

You can invite other users in the partner organization by using the UI, PowerShell scripts, or APIs. You can then send the guest user a direct link to a shared app. In most cases, there's no longer a need to open the email invitation and click a redemption URL. See [Microsoft Entra B2B collaboration invitation redemption](redemption-experience).

## How does B2B collaboration work when the invited partner is using federation to add their own on-premises authentication?

If the partner has a Microsoft Entra tenant that is federated to the on-premises authentication infrastructure, on-premises single sign-on (SSO) is automatically achieved. If the partner doesn't have a Microsoft Entra tenant, a Microsoft Entra account is created for new users.

## Can an Azure AD B2C local account be invited to a Microsoft Entra tenant for B2B collaboration?

No. An Azure AD B2C local account can only be used to sign in to the Azure AD B2C tenant. The account can't be used to sign into a Microsoft Entra tenant. Inviting an Azure AD B2C local account to a Microsoft Entra tenant for B2B collaboration isn't supported.

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

## What applications and services support Azure B2B guest users?

All Microsoft Entra integrated applications can support Azure B2B guest users, but they must use an endpoint set up as a tenant to authenticate guest users. You might also need to [customize the claims](claims-mapping) in the SAML token that is issued when a guest user authenticates to the app.

## Can we force multifactor authentication for B2B guest users if our partners don't have multifactor authentication?

Yes. For more information, see [Conditional Access for B2B collaboration users](authentication-conditional-access).

## In SharePoint, you can define an "allow" or "deny" list for external users. Can we do this in Azure?

Yes. Microsoft Entra B2B collaboration supports allowlists and blocklists.

## What licenses do we need to use Microsoft Entra B2B?

For information about what licenses your organization needs to use Microsoft Entra B2B, see [External ID pricing](external-identities-pricing).

## What happens if I invite a user whose email and UPN don’t match?

It depends. By default, Microsoft Entra ID allows only UPN as the login ID. When UPN and email are the same, Microsoft Entra B2B invitations and subsequent sign-ins work as expected. However, issues can arise when a user's email and UPN don't match, and the email is used instead of the UPN to sign in. When a user is invited with a non-UPN email, they will be able to redeem the invitation if they redeem using the [email invitation link](redemption-experience#redemption-process-through-the-invitation-email), but redemptions via a [direct link](redemption-experience#redemption-process-through-a-direct-link) will fail. However, even if the user successfully redeems the invitation, subsequent sign-in attempts using the non-UPN email will fail unless the identity provider (either Microsoft Entra ID or a federated identity provider) is configured to allow email as an alternative login ID. This issue can be mitigated by:

1. [Enabling email as an alternate login ID](../identity/authentication/howto-authentication-use-email-signin) in the invited/home Microsoft Entra tenant
2. Enabling the federated identity provider to support email as login ID (if Microsoft Entra ID is federated to another identity provider) or
3. Instructing the user to redeem/sign-in using their UPN.

To avoid this issue entirely, administrators should ensure users’ UPN and email are the same value.

![Flow diagram showing invitation redemption behavior when a guest user's email and UPN don't match.](media/user-invitation-different-email-upn/guest-redemption.png)

![Flow diagram showing subsequent sign-in behavior when a guest user's email and UPN don't match.](media/user-invitation-different-email-upn/subsequent-sign-in.png)

Note

Invitations and redemptions being sent across Microsoft clouds must use UPN. Email is not supported at this time. For example, if a user from a US Government tenant is invited to a Commercial tenant, the user must be invited using their UPN.

## Instant-on: What can cause replication latency?

In the B2B collaboration flows, we add users to the directory and dynamically update them during the invitation redemption process, app assignment, and so on. The updates and writes ordinarily happen in one directory instance and must be replicated across all instances. Replication is completed once all instances are updated. Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur. If that happens, refresh or retry to help. If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.

## Is your app ready for Google's WebView deprecation and Microsoft’s OTP defaults?

Starting January 4, 2021, Google [deprecated WebView sign-in support](https://developers.googleblog.com/2020/08/guidance-for-our-effort-to-block-less-secure-browser-and-apps.html). If you're using Google federation or self-service sign-up with Gmail, you should [test your line-of-business native applications for compatibility](google-federation#deprecation-of-web-view-sign-in-support). The [email one-time passcode](one-time-passcode) feature is now turned on by default for all new tenants and for any existing tenants where you haven't explicitly turned it off. When this feature is turned off, the fallback authentication method is to prompt invitees to create a Microsoft account.