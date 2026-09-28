---
layout: FAQ
title: Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sso-faq
summary: >
  <p>In this article, we address frequently asked questions about Microsoft Entra seamless single sign-on (Seamless SSO). Keep checking back for new content.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: mwongerapk
description: Answers to frequently asked questions about Microsoft Entra seamless single sign-on.
keywords: what is Azure AD Connect, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.tgt_pltfrm: na
ms.custom: no-azure-ad-ps-ref
ms.topic: faq
ms.date: 2026-09-15T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 20f01328-ebfa-31af-4e67-6de92c8f924e
document_version_independent_id: a990551f-e6c9-dede-308a-b5578fb7ee1e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sso-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sso-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sso-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 595ee271-90e5-e445-a3d2-b5791a7a6a69
---

# Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

In this article, we address frequently asked questions about Microsoft Entra seamless single sign-on (Seamless SSO). Keep checking back for new content.

## What sign-in methods do Seamless SSO work with

Seamless SSO can be combined with either the [Password Hash Synchronization](how-to-connect-password-hash-synchronization) or [Pass-through Authentication](how-to-connect-pta) sign-in methods. However this feature can't be used with Active Directory Federation Services (ADFS).

## Is Seamless SSO a free feature?

Seamless SSO is a free feature and you don't need any paid editions of Microsoft Entra ID to use it.

## Is Seamless SSO available in the Microsoft Azure Germany cloud and the Microsoft Azure Government cloud?

Seamless SSO is available for the [Azure Government cloud](https://www.microsoft.com/de-de/microsoft-cloud). For details, view [Hybrid Identity Considerations for Azure Government](reference-connect-government-cloud).

## What applications take advantage of `domain_hint` or `login_hint` parameter capability of Seamless SSO?

The table has a list of applications that can send these parameters to Microsoft Entra ID. This action provides users a silent sign-on experience using Seamless SSO.:

| Application name | Application URL |
| --- | --- |
| Access panel | https://myapps.microsoft.com/contoso.com |
| Outlook on Web | https://outlook.office365.com/contoso.com |
| Office 365 portals | https://portal.office.com?domain\_hint=contoso.com, https://www.office.com?domain\_hint=contoso.com |

In addition, users get a silent sign-on experience if an application sends sign-in requests to Microsoft Entra endpoints set up as tenants - that is, https://login.microsoftonline.com/contoso.com/&lt;..&gt; or https://login.microsoftonline.com/&lt;tenant\_ID&gt;/&lt;..&gt; - instead of the Microsoft Entra common endpoint - that is, https://login.microsoftonline.com/common/&lt;...&gt;. The table has a list of applications that make these types of sign-in requests.

| Application name | Application URL |
| --- | --- |
| SharePoint Online | https://contoso.sharepoint.com |
| [Microsoft Entra admin center](https://entra.microsoft.com) | https://portal.azure.com/contoso.com |

In the above tables, replace "contoso.com" with your domain name to get to the right application URLs for your tenant.

If you want other applications using our silent sign-on experience, let us know in the feedback section.

## Does Seamless SSO support `Alternate ID` as the username, instead of `userPrincipalName`?

Yes. Seamless SSO supports `Alternate ID` as the username when configured in Microsoft Entra Connect as shown [here](how-to-connect-install-custom). Not all Microsoft 365 applications support `Alternate ID`. Refer to the specific application's documentation for the support statement.

## What is the difference between the single sign-on experience provided by Microsoft Entra join and Seamless SSO?

[Microsoft Entra join](../../devices/overview) provides SSO to users if their devices are registered with Microsoft Entra ID. These devices don't necessarily have to be domain-joined. SSO is provided using *primary refresh tokens* or *PRTs*, and not Kerberos. The user experience is most optimal on Windows 10 devices. SSO happens automatically on the Microsoft Edge browser. It also works on Chrome with the use of a browser extension.

You can use Microsoft Entra join and Seamless SSO on your tenant. These two features are complementary. If both features are turned on, then SSO from Microsoft Entra join takes precedence over Seamless SSO.

## I want to register non-Windows 10 devices with Microsoft Entra ID, without using AD FS. Can I use Seamless SSO instead?

Yes, this scenario needs version 2.1 or later of the [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).

## How can I roll over the Kerberos decryption key of the `AZUREADSSO` computer account?

It's important to frequently roll over the Kerberos decryption key of the `AZUREADSSO` computer account (which represents Microsoft Entra ID) created in your on-premises AD forest.

Important

We highly recommend that you roll over the Kerberos decryption key at least every **30 days** using the `Update-AzureADSSOForest` cmdlet. When using the `Update-AzureADSSOForest` cmdlet, ensure that you *don't* run the `Update-AzureADSSOForest` command more than once per forest. Otherwise, the feature stops working until the time your users' Kerberos tickets expire and are reissued by your on-premises Active Directory.

Follow these steps on the on-premises server where you're running Microsoft Entra Connect:

Note

You need domain administrator and Hybrid Identity Administrator credentials for the steps. If you're not a domain admin and you were assigned permissions by the domain admin, you should call `Update-AzureADSSOForest -OnPremCredentials $creds -PreserveCustomPermissionsOnDesktopSsoAccount`

**Step 1. Get list of AD forests where Seamless SSO is enabled**

1. Navigate to the `%ProgramFiles%\Microsoft Azure Active Directory Connect` folder.
2. Import the ADSync PowerShell module using this command: `Import-Module "$env:ProgramFiles\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1"`.
3. Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.
4. Run PowerShell as an Administrator. In PowerShell, call `New-AzureADSSOAuthenticationContext`. This command should give you a popup to enter your tenant's Hybrid Identity Administrator credentials.
5. Call `Get-AzureADSSOStatus | ConvertFrom-Json`. This command provides a list of AD forests (look at the "Domains" list) on which this feature has been enabled.

**Step 2. Update the Kerberos decryption key on each AD forest that it was set up on**

1. Call `$creds = Get-Credential`. When prompted, enter the Domain Administrator credentials for the intended AD forest.

Note

The domain administrator credentials username must be entered in the SAM account name format (contoso\johndoe or contoso.com\johndoe). We use the domain portion of the username to locate the Domain Controller of the Domain Administrator using DNS.

Note

The domain administrator account used must not be a member of the Protected Users group. If so, the operation fails.

1. Call `Update-AzureADSSOForest -OnPremCredentials $creds`. This command updates the Kerberos decryption key for the `AZUREADSSO` computer account in this specific AD forest and updates it in Microsoft Entra ID.
2. Repeat the preceding steps for each AD forest that you’ve set up the feature on.

Note

If you're updating a forest, other than the Microsoft Entra Connect one, make sure connectivity to the global catalog server (TCP 3268 and TCP 3269) is available.

Important

This doesn't need to be done on servers running Microsoft Entra Connect in staging mode.

## How can I disable Seamless SSO?

**Step 1. Disable the feature on your tenant**

**Option A: Disable using Microsoft Entra Connect**

1. Run Microsoft Entra Connect, choose **Change user sign-in page** and click **Next**.
2. Uncheck the **Enable single sign-on** option. Continue through the wizard.

After completing the wizard, Seamless SSO is disabled on your tenant. However, you'll see a message on screen that reads as follows:

"Single sign-on is now disabled, but there are other manual steps to perform in order to complete clean-up. [Learn more](tshoot-connect-sso#step-3-disable-seamless-sso-for-each-active-directory-forest-where-youve-set-up-the-feature)"

To complete the clean-up process, follow steps 2 and 3 on the on-premises server where you're running Microsoft Entra Connect.

**Option B: Disable using PowerShell**

Run the following steps on the on-premises server where you're running Microsoft Entra Connect:

1. Navigate to the `%ProgramFiles%\Microsoft Azure Active Directory Connect` folder.
2. Import the ADSync PowerShell module using this command: `Import-Module "$env:ProgramFiles\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1"`.
3. Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.
4. Run PowerShell as an Administrator. In PowerShell, call `New-AzureADSSOAuthenticationContext`. This command should give you a popup to enter your tenant's Hybrid Identity Administrator credentials.
5. Call `Enable-AzureADSSO -Enable $false`.

At this point Seamless SSO is disabled but the domains remain configured in case you would like to enable Seamless SSO back. If you would like to remove the domains from Seamless SSO configuration completely, call the following cmdlet after you completed step 5 above: `Disable-AzureADSSOForest -DomainFqdn <fqdn>`.

Important

Disabling Seamless SSO using PowerShell won't change the state in Microsoft Entra Connect. Seamless SSO shows as enabled in the **Change user sign-in** page.

Note

If you don’t have a Microsoft Entra Connect Sync server, you can download one and run the initial installation. This will not set up the server but it will unpack the necessary files required to disable SSO. Once the MSI installation completes, close the Microsoft Entra Connect wizard and run the steps to disable Seamless SSO using PowerShell.

**Step 2. Get list of AD forests where Seamless SSO has been enabled**

Follow tasks 1 through 4 if you have disabled Seamless SSO using Microsoft Entra Connect. If you have disabled Seamless SSO using PowerShell instead, jump ahead to task 5.

1. Navigate to the `%ProgramFiles%\Microsoft Azure Active Directory Connect` folder.
2. Import the ADSync PowerShell module using this command: `Import-Module "$env:ProgramFiles\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1"`.
3. Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.
4. Run PowerShell as an Administrator. In PowerShell, call `New-AzureADSSOAuthenticationContext`. This command should give you a popup to enter your tenant's Hybrid Identity Administrator credentials.
5. Call `Get-AzureADSSOStatus | ConvertFrom-Json`. This command provides you with the list of AD forests (look at the "Domains" list) on which this feature has been enabled.

**Step 3. Manually delete the `AZUREADSSO` computer account from each AD forest that you see listed.**