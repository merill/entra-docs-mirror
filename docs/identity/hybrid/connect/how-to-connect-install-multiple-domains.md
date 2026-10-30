---
layout: Conceptual
title: Multiple Domain Support for Federating with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-install-multiple-domains
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document describes setting up and configuring multiple top level domains with Microsoft 365 and Microsoft Entra ID.
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.tgt_pltfrm: na
ms.custom: no-azure-ad-ps-ref, sfi-image-nochange
ms.topic: how-to
ms.date: 2025-09-18T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: bb804059-d0a7-e608-116a-2e0828814479
document_version_independent_id: e78f23cf-8d7c-e668-a9d6-f0803d4124f0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-install-multiple-domains.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-install-multiple-domains
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-install-multiple-domains.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5c4a180f-5866-a5fd-6493-d50579f2ad77
---

# Multiple Domain Support for Federating with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

This article provides guidance on using multiple top-level domains and subdomains when federating with Microsoft 365 or Microsoft Entra domains.

## Multiple top-level domain support

Federating multiple, top-level domains with Microsoft Entra ID requires some extra configuration that isn't required when federating with one top-level domain.

When a domain is federated with Microsoft Entra ID, several properties are set on the domain in Azure. One important property is IssuerUri. This property is a URI that is used by Microsoft Entra ID to identify the domain that the token is associated with. The URI doesn’t need to resolve to anything, but it must be a valid URI. By default, Microsoft Entra ID sets the URI to the value of the federation service identifier in your on-premises AD FS configuration.

Note

The federation service identifier is a URI that uniquely identifies a federation service. The federation service is an instance of AD FS that acts as the security token service.

You can view the IssuerUri by using the PowerShell command `Get-EntraDomainFederationSettings -DomainName <your domain>`.

A problem occurs when you add more than one top-level domain. For example, let's say you have set up federation between Microsoft Entra ID and your on-premises environment. For this document, the domain bmcontoso.com is used. Now a second, top-level domain, bmfabrikam.com has been added.

![Screenshot of multiple top-level domains.](media/how-to-connect-install-multiple-domains/domains.png)

When you attempt to federate the bmfabrikam.com domain, an error occurs. This occurs because Microsoft Entra ID doesn’t allow the IssuerUri property to have the same value for more than one domain.

### SupportMultipleDomain Parameter

Note

SupportMultipleDomain parameter is no longer available and does not work with the following modules:

- `Microsoft.Graph`
- `Microsoft.Entra`

Important

To federate multiple domains, you might need to make changes one by one because the -SupportMultipleDomain parameter is no longer available.

## How to update the trust between AD FS and Microsoft Entra ID

If you've added a new domain in the [Microsoft Entra admin center](https://entra.microsoft.com) and changed the token signing certificate, you're one step away from updating your federation information in Entra ID.

Follow these steps to update your federation information in Entra ID:

1. Open a new PowerShell session and run the below commands to install the Microsoft Entra PowerShell module:

    Note

    `-allowclobber` will override warning messages about installation conflicts and overwrite existing commands that have the same name as commands being installed by a module. Use this value if you already have installed Microsoft.Graph module:
2. - `Install-Module -Name Microsoft.Entra -allowClobber`
    - `Import-Module -Name Microsoft.Entra.DirectoryManagement`
    - `Connect-Entra -Scopes 'Domain.Read.All'`
    - `Get-EntraFederationProperty -domainname domain.com`

    ![Screenshot of output of the Get-EntraFederationProperty cmdlet.](media/how-to-connect-install-multiple-domains/entra-fed-property.png)

Once you have copied the ID displayed in the second column from the output, run:

- `Update-MgDomainFederationConfiguration -DomainID domain.com -InternalDomainFederationId 0f6ftrte-xxxx-xxxx-xxxx-19xxxxxxxx23'`

Follow these steps to add the new top-level domain using PowerShell:

1. On a machine that has [Azure AD PowerShell module](/en-us/previous-versions/azure/jj151815%28v=azure.100%29) installed on it run the following PowerShell: `$cred=Get-Credential`.
2. Enter the username and password of a hybrid identity administrator for the Microsoft Entra domain you're federating with.
3. In PowerShell, enter `Connect-Entra -Scopes 'Domain.ReadWrite.All'`
4. Enter all the values as the below example to add a new domain:

```powershell
  New-MgDomainFederationConfiguration -DomainId "contoso.com" -ActiveSigninUri " https://sts.contoso.com/adfs/services/trust/2005/usernamemixed" -DisplayName "Contoso" -IssuerUri " http://contoso.com/adfs/services/trust" -MetadataExchangeUri " https://sts.contoso.com/adfs/services/trust/mex" -PassiveSigninUri " https://sts.contoso.com/adfs/ls/" -SignOutUri " https://sts.contoso.com/adfs/ls/" -SigningCertificate <*Base64 Encoded Format cert*> -FederatedIdpMfaBehavior "acceptIfMfaDoneByFederatedIdp" -PreferredAuthenticationProtocol "wsFed"
```

Follow these steps to add the new top-level domain using Microsoft Entra Connect:

1. Launch Microsoft Entra Connect from the desktop or start menu
2. Choose **Add an additional Microsoft Entra Domain**

![Screenshot of the Additional tasks page with Add an additional Microsoft Entra domain selected.](media/how-to-connect-install-multiple-domains/add1.png)

1. Enter your Microsoft Entra ID and Active Directory credentials
2. Select the second domain you wish to configure for federation

![Screenshot of Add an additional Microsoft Entra domain.](media/how-to-connect-install-multiple-domains/add2.png)

1. Select **Install**.

### Verify the new top-level domain

Use the PowerShell command `Get-MgDomainFederationConfiguration -DomainName <your domain>` to view the updated IssuerUri. The screenshot below shows that the federation settings are updated on the original domain `http://bmcontoso.com/adfs/services/trust`.

And the IssuerUri on the new domain has been set to `https://bmcontoso.com/adfs/services/trust`

## Support for subdomains

When you add a subdomain, because of the way Microsoft Entra ID handles domains, it inherits the settings of the parent. So, the IssuerUri needs to match the parent domain.

For example, if you have bmcontoso.com and then add corp.bmcontoso.com, The IssuerUri for a user from corp.bmcontoso.com needs to be **`http://bmcontoso.com/adfs/services/trust`**. However the standard rule implemented above for Microsoft Entra ID, generates a token with an issuer as **`http://corp.bmcontoso.com/adfs/services/trust`**, which won't match the domain's required value and authentication fails.

### How to enable support for subdomains

To work around this behavior, update the AD FS relying party trust for Microsoft Online. To do this, you must configure a custom claim rule so that it strips off any subdomains from the user’s UPN suffix when constructing the custom Issuer value.

Use the following claim:

```
c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));
```

Note

The last number in the regular expression set is how many parent domains there are in your root domain. Here bmcontoso.com is used, so two parent domains are necessary. If three parent domains were to be kept (that is, corp.bmcontoso.com), then the number would have been three. Eventually a range can be indicated, the match is made to match the maximum of domains. "{2,3}" matches two to three domains (that is, bmfabrikam.com and corp.bmcontoso.com).

Use the following steps to add a custom claim to support subdomains.

1. Open AD FS Management
2. Right-click the Microsoft Online RP trust and select **Edit Claim Rules**.
3. Select the third claim rule, and replace

![Screenshot of the Edit claim dialog.](media/how-to-connect-install-multiple-domains/sub1.png)

1. Replace the current claim:

```
c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
```

with

```
c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));
```

![Screenshot of the Replace claim dialog.](media/how-to-connect-install-multiple-domains/sub2.png)

1. Select **OK**, then select **Apply**, and finally select **OK** again. Close AD FS Management.