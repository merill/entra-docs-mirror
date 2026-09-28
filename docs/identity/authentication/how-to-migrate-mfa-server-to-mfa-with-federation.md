---
layout: Conceptual
title: Migrate to Microsoft Entra multifactor authentication with federations - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-migrate-mfa-server-to-mfa-with-federation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Step-by-step guidance to move from MFA Server on-premises to Microsoft Entra multifactor authentication with federation
ms.custom: no-azure-ad-ps-ref
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: michmcla, gasinh
locale: en-us
document_id: 1aed49e2-8470-aaaf-5f92-c8453016582e
document_version_independent_id: 6b16acbf-7398-3547-b37e-fd688d547dfd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-migrate-mfa-server-to-mfa-with-federation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-migrate-mfa-server-to-mfa-with-federation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-migrate-mfa-server-to-mfa-with-federation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 57e628a2-0c2a-4ebb-7d72-53ed6cd0a799
---

# Migrate to Microsoft Entra multifactor authentication with federations - Microsoft Entra ID | Microsoft Learn

Moving your multifactor-authentication (MFA) solution to Microsoft Entra ID is a great first step in your journey to the cloud. Consider also moving to Microsoft Entra ID for user authentication in the future. For more information, see the process for migrating to Microsoft Entra multifactor authentication with cloud authentication.

To migrate to Microsoft Entra multifactor authentication with federation, the Microsoft Entra multifactor authentication authentication provider is installed on AD FS. The Microsoft Entra ID relying party trust and other relying party trusts are configured to use Microsoft Entra multifactor authentication for migrated users.

The following diagram shows the migration process.

![Flow chart of the migration process. Process areas and headings in this document are in the same order](media/how-to-migrate-mfa-server-to-mfa-with-federation/mfa-federation-flow.png)

## Create migration groups

To create new Conditional Access policies, you'll need to assign those policies to groups. You can use Microsoft Entra security groups or Microsoft 365 Groups for this purpose. You can also create or sync new ones.

You'll also need a Microsoft Entra security group for iteratively migrating users to Microsoft Entra multifactor authentication. These groups are used in your claims rules.

Don't reuse groups that are used for security. If you're using a security group to secure a group of high-value apps with a Conditional Access policy, only use the group for that purpose.

## Prepare AD FS

### Upgrade AD FS server farm to 2019, FBL 4

In AD FS 2019, you can specify additional authentication methods for a relying party, such as an application. You use group membership to determine authentication provider. By specifying an additional authentication method, you can transition to Microsoft Entra multifactor authentication while keeping other authentication intact during the transition. For more information, see [Upgrading to AD FS in Windows Server 2016 using a WID database](/en-us/windows-server/identity/ad-fs/deployment/upgrading-to-ad-fs-in-windows-server). The article covers both upgrading your farm to AD FS 2019 and upgrading your FBL to 4.

### Configure claims rules to invoke Microsoft Entra multifactor authentication

Now that Microsoft Entra multifactor authentication is an additional authentication method, you can assign groups of users to use it. You do so by configuring claims rules, also known as relying party trusts. By using groups, you can control which authentication provider is called globally or by application. For example, you can call Microsoft Entra multifactor authentication for users who have registered for combined security information, while calling MFA Server for those who haven't.

Note

Claims rules require on-premises security group. Before making changes to claims rules, back them up.

#### Back up rules

Before configuring new claims rules, back up your rules. You'll need to restore these rules as a part of your clean-up steps.

Depending on your configuration, you may also need to copy the rule and append the new rules being created for the migration.

To view global rules, run:

```powershell
Get-AdfsAdditionalAuthenticationRule
```

To view relying party trusts, run the following command and replace RPTrustName with the name of the relying party trust claims rule:

```powershell
(Get-AdfsRelyingPartyTrust -Name "RPTrustName").AdditionalAuthenticationRules 
```

#### Access control policies

Note

Access control policies can't be configured so that a specific authentication provider is invoked based on group membership.

To transition from access control policies to additional authentication rules, run the following command for each of your Relying Party Trusts using the MFA Server authentication provider:

```powershell
Set-AdfsRelyingPartyTrust -TargetName AppA -AccessControlPolicyName $Null
```

This command will move the logic from your current Access Control Policy into Additional Authentication Rules.

#### Set up the group, and find the SID

You'll need to have a specific group in which you place users for whom you want to invoke Microsoft Entra multifactor authentication. You'll need the security identifier (SID) for that group.

To find the group SID, use the following command, with your group name

`Get-ADGroup "GroupName"`

#### Setting the claims rules to call Microsoft Entra multifactor authentication

The following PowerShell cmdlets invoke Microsoft Entra multifactor authentication for users in the group when not on the corporate network. Replace "YourGroupSid" with the SID found by running the above cmdlet.

Make sure you review the [How to Choose Additional Auth Providers in 2019](/en-us/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server).

Important

Back up your claims rules

#### Set global claims rule

Run the following PowerShell cmdlet:

```powershell
(Get-AdfsRelyingPartyTrust -Name "RPTrustName").AdditionalAuthenticationRules
```

The command returns your current additional authentication rules for your relying party trust. Append the following rules to your current claim rules:

```console
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == 
"YourGroupSID"] => issue(Type = "http://schemas.microsoft.com/claims/authnmethodsproviders", 
Value = "AzureMfaAuthentication");
not exists([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
Value=="YourGroupSid"]) => issue(Type = 
"http://schemas.microsoft.com/claims/authnmethodsproviders", Value = 
"AzureMfaServerAuthentication");'
```

The following example assumes your current claim rules are configured to prompt for MFA when users connect from outside your network. This example includes the additional rules that you need to append.

```PowerShell
Set-AdfsAdditionalAuthenticationRule -AdditionalAuthenticationRules 'c:[type == 
"http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = 
"http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = 
"http://schemas.microsoft.com/claims/multipleauthn" );
 c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == 
"YourGroupSID"] => issue(Type = "http://schemas.microsoft.com/claims/authnmethodsproviders", 
Value = "AzureMfaAuthentication");
not exists([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
Value=="YourGroupSid"]) => issue(Type = 
"http://schemas.microsoft.com/claims/authnmethodsproviders", Value = 
"AzureMfaServerAuthentication");'
```

#### Set per-application claims rule

This example modifies claim rules on a specific relying party trust (application), and includes the information you must append.

```PowerShell
Set-AdfsRelyingPartyTrust -TargetName AppA -AdditionalAuthenticationRules 'c:[type == 
"http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = 
"http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = 
"http://schemas.microsoft.com/claims/multipleauthn" );
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == 
"YourGroupSID"] => issue(Type = "http://schemas.microsoft.com/claims/authnmethodsproviders", 
Value = "AzureMfaAuthentication");
not exists([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
Value=="YourGroupSid"]) => issue(Type = 
"http://schemas.microsoft.com/claims/authnmethodsproviders", Value = 
"AzureMfaServerAuthentication");'
```

### Configure Microsoft Entra multifactor authentication as an authentication provider in AD FS

To configure Microsoft Entra multifactor authentication for AD FS, you must configure each AD FS server. If you have multiple AD FS servers in your farm, you can configure them remotely using Microsoft Entra PowerShell.

For step-by-step directions on this process, see [Configure the AD FS servers](/en-us/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa) in the article [Configure Microsoft Entra multifactor authentication as authentication provider with AD FS](/en-us/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa).

Once you've configured the servers, you can add Microsoft Entra multifactor authentication as an additional authentication method.

![Screen shot showing the Edit authentication methods screen with Microsoft Entra multifactor authentication and Azure Multi-Factor Authentication Server selected](media/how-to-migrate-mfa-server-to-mfa-user-authentication/edit-authentication-methods.png)

## Prepare Microsoft Entra ID and implement migration

This section covers final steps before migrating user MFA settings.

### Set federatedIdpMfaBehavior to enforceMfaByFederatedIdp

For federated domains, MFA may be enforced by Microsoft Entra Conditional Access or by the on-premises federation provider. Each federated domain has a Microsoft Graph PowerShell security setting named **federatedIdpMfaBehavior**. You can set **federatedIdpMfaBehavior** to `enforceMfaByFederatedIdp` so Microsoft Entra ID accepts MFA that's performed by the federated identity provider. If the federated identity provider didn't perform MFA, Microsoft Entra ID redirects the request to the federated identity provider to perform MFA. For more information, see [federatedIdpMfaBehavior](/en-us/graph/api/resources/internaldomainfederation?view=graph-rest-beta&amp;preserve-view=true#federatedidpmfabehavior-values).

Note

The **federatedIdpMfaBehavior** setting is a new version of the **SupportsMfa** property of the [New-MgDomainFederationConfiguration](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/new-mgdomainfederationconfiguration) cmdlet.

For domains that set the **SupportsMfa** property, these rules determine how **federatedIdpMfaBehavior** and **SupportsMfa** work together:

- Switching between **federatedIdpMfaBehavior** and **SupportsMfa** isn't supported.
- Once **federatedIdpMfaBehavior** property is set, Microsoft Entra ID ignores the **SupportsMfa** setting.
- If the **federatedIdpMfaBehavior** property is never set, Microsoft Entra ID will continue to honor the **SupportsMfa** setting.
- If **federatedIdpMfaBehavior** or **SupportsMfa** isn't set, Microsoft Entra ID will default to `acceptIfMfaDoneByFederatedIdp` behavior.

You can check the status of **federatedIdpMfaBehavior** by using [Get-MgDomainFederationConfiguration](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdomainfederationconfiguration?view=graph-powershell-1.0&amp;preserve-view=true&amp;viewFallbackFrom=graph-powershell-beta).

```powershell
Get-MgDomainFederationConfiguration –DomainID contoso.com
```

You can also check the status of your **SupportsMfa** flag with [Get-MgDomainFederationConfiguration](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdomainfederationconfiguration):

```powershell
Get-MgDomainFederationConfiguration –DomainName contoso.com
```

The following example shows how to set **federatedIdpMfaBehavior** to `enforceMfaByFederatedIdp` by using Graph PowerShell.

#### Request

```http
PATCH https://graph.microsoft.com/beta/domains/contoso.com/federationConfiguration/6601d14b-d113-8f64-fda2-9b5ddda18ecc
Content-Type: application/json
{
  "federatedIdpMfaBehavior": "enforceMfaByFederatedIdp"
}
```

#### Response

> 
> **Note:** The response object shown here might be shortened for readability.

```http
HTTP/1.1 200 OK
Content-Type: application/json
{
  "@odata.type": "#microsoft.graph.internalDomainFederation",
  "id": "6601d14b-d113-8f64-fda2-9b5ddda18ecc",
   "issuerUri": "http://contoso.com/adfs/services/trust",
   "metadataExchangeUri": "https://sts.contoso.com/adfs/services/trust/mex",
   "signingCertificate": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0u",
   "passiveSignInUri": "https://sts.contoso.com/adfs/ls",
   "preferredAuthenticationProtocol": "wsFed",
   "activeSignInUri": "https://sts.contoso.com/adfs/services/trust/2005/usernamemixed",
   "signOutUri": "https://sts.contoso.com/adfs/ls",
   "promptLoginBehavior": "nativeSupport",
   "isSignedAuthenticationRequestRequired": true,
   "nextSigningCertificate": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0u",
   "signingCertificateUpdateStatus": {
        "certificateUpdateResult": "Success",
        "lastRunDateTime": "2021-08-25T07:44:46.2616778Z"
    },
   "federatedIdpMfaBehavior": "enforceMfaByFederatedIdp"
}
```

### Configure Conditional Access policies if needed

If you use Conditional Access to determine when users are prompted for MFA, you shouldn't need to change your policies.

If your federated domain(s) have SupportsMfa set to false, analyze your claims rules on the Microsoft Entra ID relying party trust and create Conditional Access policies that support the same security goals.

After creating Conditional Access policies to enforce the same controls as AD FS, you can back up and remove your claim rules customizations on the Microsoft Entra ID Relying Party.

For more information, see the following resources:

- [Plan a Conditional Access deployment](../conditional-access/plan-conditional-access)
- [Common Conditional Access policies](../conditional-access/concept-conditional-access-policy-common)

## Register users for Microsoft Entra multifactor authentication

This section covers how users can register for combined security (MFA and self-service-password reset) and how to migrate their MFA settings. Microsoft Authenticator can be used as in passwordless mode. It can also be used as a second factor for MFA with either registration method.

### Register for combined security registration (recommended)

We recommend having your users register for combined security information, which is a single place to register their authentication methods and devices for both MFA and SSPR.

Microsoft provides communication templates that you can provide to your users to guide them through the combined registration process. These include templates for email, posters, table tents, and various other assets. Users register their information at `https://aka.ms/mysecurityinfo`, which takes them to the combined security registration screen.

We recommend that you [secure the security registration process with Conditional Access](../conditional-access/policy-all-users-security-info-registration) that requires the registration to occur from a trusted device or location. For information on tracking registration statuses, see [Authentication method activity for Microsoft Entra ID](howto-authentication-methods-activity).

Note

Users who must register their combined security information from a non-trusted location or device can be issued a Temporary Access Pass or alternatively, temporarily excluded from the policy.

### Migrate MFA settings from MFA Server

You can use the [MFA Server Migration utility](how-to-mfa-server-migration-utility) to synchronize registered MFA settings for users from MFA Server to Microsoft Entra ID. You can synchronize phone numbers, hardware tokens, and device registrations such as Microsoft Authenticator settings.

### Add users to the appropriate groups

- If you created new Conditional Access policies, add the appropriate users to those groups.
- If you created on-premises security groups for claims rules, add the appropriate users to those groups.

We don't recommend that you reuse groups that are used for security. If you're using a security group to secure a group of high-value apps with a Conditional Access policy, only use the group for that purpose.

## Monitoring

Microsoft Entra multifactor authentication registration can be monitored using the [Authentication methods usage & insights report](https://portal.azure.com/). This report can be found in Microsoft Entra ID. Select **Monitoring**, then select **Usage & insights**.

In Usage & insights, select **Authentication methods**.

Detailed Microsoft Entra multifactor authentication registration information can be found on the Registration tab. You can drill down to view a list of registered users by selecting the **Users capable of Azure multifactor authentication** hyperlink.

![Image of Authentication methods activity screen showing user registrations to MFA](media/how-to-migrate-mfa-server-to-mfa-with-federation/authentication-methods.png)

## Cleanup steps

Once you have completed migration to Microsoft Entra multifactor authentication and are ready to decommission the MFA Server, do the following three things:

1. Revert your claim rules on AD FS to their pre-migration configuration and remove the MFA Server authentication provider.
2. Remove MFA server as an authentication provider in AD FS. This will ensure all users use Microsoft Entra multifactor authentication as it will be the only additional authentication method enabled.
3. Decommission the MFA Server.

### Revert claims rules on AD FS and remove MFA Server authentication provider

Follow the steps under Configure claims rules to invoke Microsoft Entra multifactor authentication to revert back to the backed up claims rules and remove any AzureMFAServerAuthentication claims rules.

For example, remove the following from the rule(s):

```console
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value ==
"**YourGroupSID**"] => issue(Type = "http://schemas.microsoft.com/claims/authnmethodsproviders",
Value = "AzureMfaAuthentication");
not exists([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid",
Value=="YourGroupSid"]) => issue(Type =
"http://schemas.microsoft.com/claims/authnmethodsproviders", Value =
"AzureMfaServerAuthentication");'
```

### Disable MFA Server as an authentication provider in AD FS

This change ensures only Microsoft Entra multifactor authentication is used as an authentication provider.

1. Open the **AD FS management console**.
2. Under **Services**, right-click on **Authentication Methods**, and select **Edit multifactor authentication Methods**.
3. Uncheck the box next to **Azure Multi-Factor Authentication Server**.

### Decommission the MFA Server

Follow your enterprise server decommissioning process to remove the MFA Servers in your environment.

Possible considerations when decommissions the MFA Servers include:

- Review MFA Servers' logs to ensure no users or applications are using it before you remove the server.
- Uninstall Multi-Factor Authentication Server from the Control Panel on the server
- Optionally clean up logs and data directories that are left behind after backing them up first.
- Uninstall the multifactor authentication Web Server SDK if applicable, including any files left over inetpub\wwwroot\MultiFactorAuthWebServiceSdk and or MultiFactorAuth directories
- For MFA Server versions prior to 8.0, it may also be necessary to remove the multifactor authentication Phone App Web Service