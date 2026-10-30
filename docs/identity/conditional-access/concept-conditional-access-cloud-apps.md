---
layout: Conceptual
title: Targeting Resources in Conditional Access Policies - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-cloud-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: conditional-access
manager: dougeby
description: Learn how to configure Conditional Access policies to target specific resources, actions, and authentication contexts in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2026-03-24T00:00:00.0000000Z
ms.reviewer: kvenkit
ms.custom:
- has-azure-ad-ps-ref
- ai-gen-docs-bap
- ai-gen-title
- ai-seo-date:07/25/2025
- ai-gen-description
locale: en-us
document_id: 1c6d2ea9-04c9-d4e5-36b5-2ce7e17192e1
document_version_independent_id: eff8d31c-d3ce-f72c-22ab-53b415b221b0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/conditional-access/concept-conditional-access-cloud-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/conditional-access/concept-conditional-access-cloud-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/conditional-access/concept-conditional-access-cloud-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 32b21286-91f9-c4c6-d49a-5d98dfd4bbcf
---

# Targeting Resources in Conditional Access Policies - Microsoft Entra ID | Microsoft Learn

## Overview

Target resources (formerly cloud apps, actions, and authentication context) are key signals in a Conditional Access policy. Conditional Access policies let admins assign controls to specific applications, services, actions, or authentication context.

- Admins can choose from the list of applications or services that include built-in Microsoft applications and any [Microsoft Entra integrated applications](../enterprise-apps/what-is-application-management), including gallery, non-gallery, and applications published through [Application Proxy](../app-proxy/overview-what-is-app-proxy).
- Admins might define a policy based on a user action like **Register security information** or **Register or join devices**, letting Conditional Access enforce controls around those actions.
- Admins can target traffic forwarding profiles from Global Secure Access for enhanced functionality.
- Admins can use authentication context to provide an extra layer of security in applications.

[![Screenshot of a Conditional Access policy and the target resources panel.](media/concept-conditional-access-cloud-apps/conditional-access-cloud-apps-or-actions.png)](media/concept-conditional-access-cloud-apps/conditional-access-cloud-apps-or-actions.png#lightbox)

## Microsoft cloud applications

Admins can assign a Conditional Access policy to Microsoft cloud apps if the service principal appears in their tenant, except for Microsoft Graph. Microsoft Graph functions as an umbrella resource. Use [Audience Reporting](troubleshoot-conditional-access#audience-reporting) to see the underlying services and target those services in your policies. Some apps like Microsoft 365/Office 365 and Windows Azure Service Management API include multiple related child apps or services. When new Microsoft cloud applications are created, they appear in the app picker list as soon as the service principal is created in the tenant.

## Office 365

Microsoft 365 offers cloud-based productivity and collaboration services like Exchange, SharePoint, and Microsoft Teams. In Conditional Access, the Microsoft 365 suite of applications appears under 'Office 365'. Microsoft 365 cloud services are deeply integrated to ensure smooth and collaborative experiences. This integration might cause confusion when creating policies because some apps, like Microsoft Teams, depend on others, like SharePoint or Exchange.

The Office 365 app grouping in Conditional Access makes it possible to target these services all at once. Use the Microsoft 365 grouping, instead of targeting individual cloud apps, to avoid issues with [service dependencies](service-dependencies).

Targeting this group of applications helps to avoid issues that might arise because of inconsistent policies and dependencies. For example: The Exchange Online app is tied to traditional Exchange Online data like mail, calendar, and contact information. Related metadata might be exposed through different resources like search. To ensure that all metadata is protected as intended, admins should assign policies to the Microsoft 365 app.

Admins can exclude the entire Microsoft 365 suite or specific Microsoft 365 cloud apps from Conditional Access policies.

For a complete list of all included services, see [Apps included in Conditional Access Microsoft 365 app suite](reference-office-365-application-contents).

## Windows Azure Service Management API

When you target the Windows Azure Service Management API application, policy is enforced for tokens issued to a set of services closely bound to the portal. This grouping includes the application IDs of:

- Azure Resource Manager
- Azure portal, which also covers the Microsoft Entra admin center and the Microsoft Engage Center
- Azure Data Lake
- Application Insights API
- Log Analytics API

Because the policy is applied to the Azure management portal and API, any services or clients that depend on the Azure API can be indirectly affected. For example:

- Azure CLI
- Azure Data Factory portal
- Azure Event Hubs
- Azure PowerShell
- Azure Service Bus
- Azure SQL Database
- Azure Synapse
- Classic deployment model APIs
- Microsoft 365 admin center
- Microsoft IoT Central
- Microsoft Defender Multitenant management
- SQL Managed Instance
- Visual Studio subscriptions administrator portal

Caution

Conditional Access policies associated with the Windows Azure Service Management API [no longer cover Azure DevOps](/en-us/azure/devops/organizations/accounts/conditional-access-policies#azure-resource-manager-audience).

Note

The Windows Azure Service Management API application applies to [Azure PowerShell](/en-us/powershell/azure/what-is-azure-powershell), which calls the [Azure Resource Manager API](/en-us/azure/azure-resource-manager/management/overview). It doesn't apply to [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/overview), which calls the [Microsoft Graph API](/en-us/graph/overview).

For Azure Government, you should target the Azure Government Cloud Management API application.

## Microsoft Admin Portals

When a Conditional Access policy targets the Microsoft Admin Portals cloud app, the policy is enforced for tokens issued to specific underlying resource application IDs associated with Microsoft admin portals. The app grouping doesn't include the backend services that those portals might call or depend on. To identify service dependencies of the admin portals, use the [Conditional Access audience reporting in sign-in logs](troubleshoot-conditional-access#audience-reporting).

The following applications comprise the Microsoft Admin Portals:

- Exchange Admin Center app ID: 497effe9-df71-4043-a8bb-14cf78c4b63b
- Azure portal app ID: c44b4083-3bb0-49c1-b47d-974e53cbdf3c
- Microsoft Office 365 Portal app ID: 00000006-0000-0ff1-ce00-000000000000
- Microsoft 365 Security And Compliance Center (Protection Center) app ID: 80ccca67-54bd-44ab-8625-4b79c4dc7775

The Admin Portal grouping is primarily intended for include scenarios, for a simplified way to target one or more admin portals with Conditional Access policies (for example, enforcing MFA). This grouping is used in the [MFA for admins Microsoft-managed policy](managed-policies#multifactor-authentication-for-admins-accessing-microsoft-admin-portals) to streamline policy creation.

This option isn't intended to function as a bulk exclusion mechanism for all backend services associated with the underlying application IDs.

Note

Block policies that target the Microsoft Admin Portals will block end users from accessing the Microsoft 365 self-install page, as this page is currently located in the Microsoft 365 admin center. For information on alternative deployment options, see [Plan your enterprise deployment of Microsoft 365 Apps](/en-us/microsoft-365-apps/deploy/plan-microsoft-365-apps).

### Other applications

Admins can add any Microsoft Entra registered application to Conditional Access policies. These applications might include:

- Applications published through [Microsoft Entra application proxy](../app-proxy/overview-what-is-app-proxy)
- [Applications added from the gallery](../enterprise-apps/add-application-portal)
- [Custom applications not in the gallery](../enterprise-apps/view-applications-portal)
- [Legacy applications published through app delivery controllers and networks](../enterprise-apps/secure-hybrid-access)
- Applications that use [password based single sign-on](../enterprise-apps/configure-password-single-sign-on-non-gallery-applications)

Note

Because Conditional Access policy sets the requirements for accessing a service, you aren't able to apply it to a client (public/native) application. In other words, the policy isn't set directly on a client (public/native) application, but is applied when a client calls a service. For example, a policy set on SharePoint service applies to all clients calling SharePoint. A policy set on Exchange applies to the attempt to access the email using Outlook client. That is why client (public/native) applications aren't available for selection in the app picker and Conditional Access option isn't available in the application settings for the client (public/native) application registered in your tenant.

Some applications don't appear in the picker at all. The only way to include these applications in a Conditional Access policy is to include **All resources (formerly 'All cloud apps')** or add the missing service principal using the [New-MgServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/new-mgserviceprincipal) PowerShell cmdlet or by using the [Microsoft Graph API](/en-us/graph/api/serviceprincipal-post-serviceprincipals).

### Conditional Access for different client types

Conditional Access applies to resources not clients, except when the client is a confidential client requesting an ID token.

- Public client
    - Public clients are those that run locally on devices like Microsoft Outlook on the desktop or mobile apps like Microsoft Teams.
    - Conditional Access policies don't apply to public clients themselves but are based on the resources they request.
- Confidential client
    - Conditional Access applies to the resources requested by the client and the confidential client itself if it requests an ID token.
    - For example: If Outlook Web requests a token for scopes `Mail.Read` and `Files.Read`, Conditional Access applies policies for Exchange and SharePoint. Additionally, if Outlook Web requests an ID token, Conditional Access also applies the policies for Outlook Web.

To view [sign-in logs](/en-us/entra/identity/monitoring-health/concept-sign-ins) for these client types from the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-in logs**.
3. Add a filter for **Client credential type**.
4. Adjust the filter to view a specific set of logs based on the client credential used in the sign-in.

For more information, see the article [Public client and confidential client applications](/en-us/entra/identity-platform/msal-client-applications).

## Conditional Access for ALL resources

Applying a Conditional Access policy to **All resources (formerly 'All cloud apps')** without any resource exclusions enforces the policy for all token requests from websites and services, including [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding). This option includes applications that aren't individually targetable in Conditional Access policy, such as `Windows Azure Active Directory` (00000002-0000-0000-c000-000000000000).

Important

Microsoft recommends creating a baseline multifactor authentication policy targeting all users and all resources (without any resource exclusions), like the one explained in [Require multifactor authentication for all users](policy-all-users-mfa-strength).

### Legacy Conditional Access behavior when an ALL resources policy has a resource exclusion

Warning

[The following Conditional Access behavior is changing](https://aka.ms/CAAllResourcesWithExclusionsChange). Those low privileged scopes that were previously excluded from policy enforcement will **no longer be excluded**. This change means that users who were previously able to access the application without any Conditional Access enforcement might now receive Conditional Access challenges. The change is rolling out in phases starting in March, 2026. For more information see [Enforcement for baseline scopes](concept-enforcement-resource-exclusions).

If any app is excluded from the policy, to avoid inadvertently blocking user access, certain low privilege scopes were *previously* excluded from policy enforcement. These scopes allowed calls to the underlying Graph APIs, like `Windows Azure Active Directory` (00000002-0000-0000-c000-000000000000) and `Microsoft Graph` (00000003-0000-0000-c000-000000000000), to access user profile and group membership information commonly used by applications as part of authentication. For example: when Outlook requests a token for Exchange, it also asks for the `User.Read` scope to be able to display the basic account information of the current user.

Most apps have a similar dependency, which is why these low privilege scopes were automatically excluded in **All resources** policies. The *previously* excluded scopes are listed as follows, consent is still required for apps to use these permissions.

- Native clients and Single page applications (SPAs) have access to the following low privilege scopes:
    - Azure AD Graph: `email`, `offline_access`, `openid`, `profile`, `User.Read`
    - Microsoft Graph: `email`, `offline_access`, `openid`, `profile`, `User.Read`, `People.Read`
- Confidential clients have access to the following low privilege scopes, if they're excluded from an **All resources**policy:
    - Azure AD Graph: `email`, `offline_access`, `openid`, `profile`, `User.Read`, `User.Read.All`,`User.ReadBasic.All`
    - Microsoft Graph: `email`, `offline_access`, `openid`, `profile`, `User.Read`, `User.Read.All`, `User.ReadBasic.All`, `People.Read`, `People.Read.All`, `GroupMember.Read.All`, `Member.Read.Hidden`

### New Conditional Access behavior when an ALL resources policy has a resource exclusion

The scopes listed in the previous section are now evaluated as directory access and mapped to Azure AD Graph (resource: Windows Azure Active Directory, ID: 00000002-0000-0000-c000-000000000000) for Conditional Access evaluation purposes.

Conditional Access policies that target All resources with one or more resource exclusions, or policies that explicitly target Azure AD Graph, are enforced in user sign-in flows where the client application requests only these scopes. There is no change in behavior when an application requests any additional scope beyond those listed above.

For guidance on assessing impact, identifying affected applications, and retaining legacy behavior, see [Improved enforcement for policies with resource exclusions](concept-enforcement-resource-exclusions).

Note

The [Azure AD Graph retirement](https://techcommunity.microsoft.com/blog/microsoft-entra-blog/important-update-azure-ad-graph-retirement/4364990) does not affect the Azure AD Graph (Windows Azure Active Directory) resource registered in your tenant.

### Protect directory information

Note

The following section applies until the rollout of the low-privilege scope enforcement change is complete.

If the [recommended baseline MFA policy without resource exclusions](policy-all-users-mfa-strength) can't be configured because of business reasons, and your organization's security policy must include directory-related low privilege scopes (`User.Read`, `User.Read.All`, `User.ReadBasic.All`, `People.Read`, `People.Read.All`, `GroupMember.Read.All`, `Member.Read.Hidden`), create a separate Conditional Access policy targeting `Windows Azure Active Directory` (00000002-0000-0000-c000-000000000000). Windows Azure Active Directory (also called Azure AD Graph) is a resource representing data stored in the directory such as users, groups, and applications. The Windows Azure Active Directory resource is included in **All resources** but can be individually targeted in Conditional Access policies by using the following steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Attribute Definition Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#attribute-definition-administrator) and [Attribute Assignment Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#attribute-assignment-administrator).
2. Browse to **Entra ID** &gt; **Custom security attributes**.
3. Create a new attribute set and attribute definition. For more information, see [Add or deactivate custom security attribute definitions in Microsoft Entra ID](../../fundamentals/custom-security-attributes-add).
4. Browse to **Entra ID** &gt; **Enterprise apps**.
5. Remove the **Application type** filter and search for **Application ID** that starts with 00000002-0000-0000-c000-000000000000.
6. Select **Windows Azure Active Directory** &gt; **Custom security attributes** &gt; **Add assignment**.
7. Select the attribute set and attribute value that you plan to use in the policy.
8. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
9. Create or modify an existing policy.
10. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include**, select &gt; **Select resources** &gt; **Edit filter**.
11. Adjust the filter to include your attribute set and definition from earlier.
12. Under **Access controls** &gt; **Grant**, select **Grant access**, **Require authentication strength**, select **Multifactor authentication**, then select **Select**.
13. Confirm your settings and set **Enable policy** to **Report-only**.
14. Select **Create** to enable your policy.

Note

Configure this policy as described in the guidance above. Any deviations in creating the policy as described (such as defining resource exclusions) may result in low privilege scopes being excluded and the policy not applying as intended.

#### All internet resources with Global Secure Access

The **All internet resources with Global Secure Access** option allows admins to target the [internet access traffic forwarding profile](/en-us/entra/global-secure-access/concept-traffic-forwarding) from [Microsoft Entra Internet Access](/en-us/entra/global-secure-access/overview-what-is-global-secure-access#microsoft-entra-internet-access).

These profiles in Global Secure Access enable admins to define and control how traffic is routed through Microsoft Entra Internet Access and Microsoft Entra Private Access. Traffic forwarding profiles can be assigned to devices and remote networks. For an example of how to apply a Conditional Access policy to these traffic profiles, see the article [How to apply Conditional Access policies to the Microsoft 365 traffic profile](/en-us/entra/global-secure-access/how-to-target-resource-microsoft-365-profile).

For more information about these profiles, see the article [Global Secure Access traffic forwarding profiles](/en-us/entra/global-secure-access/concept-traffic-forwarding).

#### All agent resources (Preview)

Applying a Conditional Access policy to All agent resources enforces the policy for all token requests to agent identity blueprint principals and agent identities.

## User actions

User actions are tasks that a user performs. Conditional Access supports two user actions:

- **Register security information**: This user action lets Conditional Access policies enforce rules when users try to register their security information. For more information, see [Combined security information registration](../authentication/concept-registration-mfa-sspr-combined).

Note

If admins apply a policy targeting user actions for registering security information and the user account is a guest from a [Microsoft personal account (MSA)](../../external-id/microsoft-account), the 'Require multifactor authentication' control requires the MSA user to register security information with the organization. If the guest user is from another provider such as [Google](../../external-id/google-federation), access is blocked.

- **Register or join devices**: This user action enables admins to enforce Conditional Access policy when users [register](../devices/concept-device-registration) or [join](../devices/concept-directory-join)devices to Microsoft Entra ID. It lets admins configure multifactor authentication for registering or joining devices with more granularity than a tenant-wide policy. There are three key considerations with this user action:
    - `Require multifactor authentication` and `Require auth strength`are the only access controls available with this user action and all others are disabled. This restriction prevents conflicts with access controls that are either dependent on Microsoft Entra device registration or not applicable to Microsoft Entra device registration.
        - Windows Hello for Business and device-bound passkeys aren't supported because those scenarios require the device to be already registered.
    - `Client apps`, `Filters for devices`, and `Device state` conditions aren't available with this user action because they're dependent on Microsoft Entra device registration to enforce Conditional Access policies.

Warning

If a Conditional Access policy is configured with the **Register or join devices** user action, set **Entra ID** &gt; **Devices** &gt; **Overview** &gt; **Device Settings** - `Require Multifactor Authentication to register or join devices with Microsoft Entra` to **No**. Otherwise, Conditional Access policies with this user action aren't properly enforced. Learn more about this device setting in [Configure device settings](../devices/manage-device-identities#configure-device-settings).

## Authentication context

Authentication context secures data and actions in applications. These applications include custom applications, line-of-business (LOB) applications, SharePoint, or applications protected by Microsoft Defender for Cloud Apps. It can also be used with Microsoft Entra Privileged Identity Management (PIM) to enforce Conditional Access policies during role activation.

For example, an organization might store files in SharePoint sites like a lunch menu or a secret BBQ sauce recipe. Everyone might access the lunch menu site, but users accessing the secret BBQ sauce recipe site might need to use a managed device and agree to specific terms of use. Similarly, an administrator activating a privileged role through PIM might be required to perform multifactor authentication or use a compliant device.

Authentication context works with users or [workload identities](workload-identity), but not in the same Conditional Access policy.

### Configure authentication contexts

Manage authentication contexts by going to **Entra ID** &gt; **Conditional Access** &gt; **Authentication context**.

[![Screenshot showing the management of authentication contexts.](media/concept-conditional-access-cloud-apps/conditional-access-authentication-context-get-started.png)](media/concept-conditional-access-cloud-apps/conditional-access-authentication-context-get-started.png#lightbox)

Select **New authentication context** to create an authentication context definition. Organizations can create up to 99 authentication context definitions (**c1-c99**). Configure these attributes:

- **Display name** is the name that is used to identify the authentication context in Microsoft Entra ID and across applications that consume authentication contexts. Use names that can be used across resources, like *trusted devices*, to reduce the number of authentication contexts needed. Having a reduced set limits the number of redirects and provides a better end to end-user experience.
- **Description** provides more information about the policies. This information is used by admins and those applying authentication contexts to resources.
- **Publish to apps** checkbox, when selected, advertises the authentication context to apps and makes it available to be assigned. If not selected, the authentication context is unavailable to downstream resources.
- **ID** is read-only and used in tokens and apps for request-specific authentication context definitions. Listed here for troubleshooting and development use cases.

#### Add to Conditional Access policy

Admins can select published authentication contexts in Conditional Access policies by going to **Assignments** &gt; **Target resources** and selecting **Authentication context** from the **Select what this policy applies to** menu.

![Screenshot showing how to add a Conditional Access authentication context to a policy](media/concept-conditional-access-cloud-apps/conditional-access-authentication-context-in-policy.png)

#### Delete an authentication context

Before deleting an authentication context, ensure no applications use it. Otherwise, access to app data isn't protected. Confirm this by checking sign-in logs for cases where authentication context Conditional Access policies are applied.

To delete an authentication context, ensure it has no assigned Conditional Access policies and isn't published to apps. This prevents accidental deletion of an authentication context still in use.

### Tag resources with authentication contexts

To learn more about using authentication contexts, see the following articles.

- [Use sensitivity labels to protect content in Microsoft Teams, Microsoft 365 groups, and SharePoint sites](/en-us/purview/sensitivity-labels-teams-groups-sites)
- [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/session-policy-aad?branch=pr-en-us-2082#require-step-up-authentication-authentication-context)
- [Custom applications](../../identity-platform/developer-guide-conditional-access-authentication-context)
- [Privileged Identity Management - On activation, require Microsoft Entra Conditional Access authentication context](/en-us/entra/id-governance/privileged-identity-management/pim-resource-roles-configure-role-settings#on-activation-require-microsoft-entra-conditional-access-authentication-context)