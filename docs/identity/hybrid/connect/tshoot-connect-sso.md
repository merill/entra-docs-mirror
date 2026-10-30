---
layout: Conceptual
title: 'Microsoft Entra Connect: Troubleshoot Seamless Single Sign-On - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tshoot-connect-sso
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic describes how to troubleshoot Microsoft Entra seamless single sign-on
ms.reviewer: swkrish
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.topic: troubleshooting
ms.date: 2026-09-15T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 69561745-8451-6cf6-ddac-dc7ef96638c5
document_version_independent_id: 3a3bb4f0-87b4-8daf-050d-76416ef490e7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tshoot-connect-sso.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tshoot-connect-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tshoot-connect-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 822667b8-d57a-64fb-83ab-6501c888866e
---

# Microsoft Entra Connect: Troubleshoot Seamless Single Sign-On - Microsoft Entra ID | Microsoft Learn

This article helps you find troubleshooting information about common problems regarding Microsoft Entra seamless single sign-on (Seamless SSO).

## Known issues

- In a few cases, enabling Seamless SSO can take up to 30 minutes.
- If you disable and re-enable Seamless SSO on your tenant, users won't get the single sign-on experience till their cached Kerberos tickets, typically valid for 10 hours, have expired.
- If Seamless SSO succeeds, the user doesn't have the opportunity to select **Keep me signed in**.
- Microsoft 365 Win32 clients (Outlook, Word, Excel, and others) with versions 16.0.8730.xxxx and above are supported using a non-interactive flow. Other versions aren't supported; on those versions, users will enter their usernames, but not passwords, to sign-in. For OneDrive, you have to activate the [OneDrive silent config feature](https://techcommunity.microsoft.com/t5/Microsoft-OneDrive-Blog/Previews-for-Silent-Sync-Account-Configuration-and-Bandwidth/ba-p/120894) for a silent sign-on experience.
- Seamless SSO doesn't work in private browsing mode on Firefox.
- Seamless SSO doesn't work in Internet Explorer when Enhanced Protected mode is turned on.
- Microsoft Edge (legacy) is no longer supported
- Seamless SSO doesn't work on mobile browsers on iOS and Android.
- If a user is part of too many groups in Active Directory, the user's Kerberos ticket will likely be too large to process, and this will cause Seamless SSO to fail. Microsoft Entra HTTPS requests can have headers with a maximum size of 50 KB; Kerberos tickets need to be smaller than that limit to accommodate other Microsoft Entra artifacts (typically, 2 - 5 KB) such as cookies. Our recommendation is to reduce user's group memberships and try again.
- If you're synchronizing 30 or more Active Directory forests, you can't enable Seamless SSO through Microsoft Entra Connect. As a workaround, you can manually enable the feature on your tenant.
- Adding the Microsoft Entra service URL (`https://autologon.microsoftazuread-sso.com`) to the Trusted sites zone instead of the Local intranet zone *blocks users from signing in*.
- Seamless SSO supports the AES256\_HMAC\_SHA1, AES128\_HMAC\_SHA1 and RC4\_HMAC\_MD5 encryption types for Kerberos. It's recommended that the encryption type for the AzureADSSOAcc$ account is set to AES256\_HMAC\_SHA1, or one of the AES types vs. RC4 for added security. The encryption type is stored on the msDS-SupportedEncryptionTypes attribute of the account in your Active Directory. If the AzureADSSOAcc$ account encryption type is set to RC4\_HMAC\_MD5, and you want to change it to one of the AES encryption types, please make sure that you first roll over the Kerberos decryption key of the AzureADSSOAcc$ account as explained in the [FAQ document](how-to-connect-sso-faq) under the relevant question, otherwise Seamless SSO won't happen.
- If you have more than one forest with forest trust, enabling SSO in one of the forests, will enable SSO in all trusted forests. If you enable SSO in a forest where SSO is already enabled, you'll get an error saying that SSO is already enabled in the forest.
- The policy that enables Seamless SSO has a 25600 char limit. This limit's for everything included in the policy, including the forest names you want Seamless SSO to be enabled on. You may hit the char limit if you have a high number of forests in your environment. If your forests have trust between them, it’s enough to enable Seamless SSO only on one forests. For example, if you have contoso.com and fabrikam.com and there’s trust between the two, you can enable Seamless SSO only on contoso.com and that will apply on fabrikam.com as well. This way, you can reduce the number of forests enabled in the policy and avoid hitting the policy char limit.

## Check status of feature

Ensure that the Seamless SSO feature is still **Enabled** on your tenant. You can check the status by going to the **Entra ID** &gt; **Entra Connect** &gt; **Connect Sync** pane in the [[Microsoft Entra admin center](https://entra.microsoft.com)](https://portal.azure.com/).

![Screenshot of the Microsoft Entra admin center: Microsoft Entra Connect pane.](media/tshoot-connect-sso/sso10.png)

Click through to see all the AD forests that have been enabled for Seamless SSO.

![Screenshot of the Microsoft Entra admin center: Seamless SSO pane.](media/tshoot-connect-sso/sso13.png)

## Sign-in failure reasons in the [Microsoft Entra admin center](https://entra.microsoft.com) (needs a Premium license)

If your tenant has a Microsoft Entra ID P1 or P2 license associated with it, you can also look at the [sign-in activity report](../../monitoring-health/concept-sign-ins) inside of Microsoft Entra ID in the [Microsoft Entra admin center](https://entra.microsoft.com).

![Screenshot of the Microsoft Entra admin center: Sign-ins report.](media/tshoot-connect-sso/sso9.png)

Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Sign-ins** in the [[Microsoft Entra admin center](https://entra.microsoft.com)](https://portal.azure.com/), and then select a specific user's sign-in activity. Look for the **SIGN-IN ERROR CODE** field. Map the value of that field to a failure reason and resolution by using the following table:

| Sign-in error code | Sign-in failure reason | Resolution |
| --- | --- | --- |
| 81001 | User's Kerberos ticket is too large. | Reduce the user's group memberships and try again. |
| 81002 | Unable to validate the user's Kerberos ticket. | See the troubleshooting checklist. |
| 81003 | Unable to validate the user's Kerberos ticket. | See the troubleshooting checklist. |
| 81004 | Kerberos authentication attempt failed. | See the troubleshooting checklist. |
| 81008 | Unable to validate the user's Kerberos ticket. | See the troubleshooting checklist. |
| 81009 | Unable to validate the user's Kerberos ticket. | See the troubleshooting checklist. |
| 81010 | Seamless SSO failed because the user's Kerberos ticket has expired or is invalid. | The user needs to sign in from a domain-joined device inside your corporate network. |
| 81011 | Unable to find the user object based on the information in the user's Kerberos ticket. | Use Microsoft Entra Connect to synchronize the user's information into Microsoft Entra ID. |
| 81012 | The user trying to sign in to Microsoft Entra ID is different from the user that is signed in to the device. | The user needs to sign in from a different device. |
| 81013 | Unable to find the user object based on the information in the user's Kerberos ticket. | Use Microsoft Entra Connect to synchronize the user's information into Microsoft Entra ID. |

## Troubleshooting checklist

Use the following checklist to troubleshoot Seamless SSO problems:

- Ensure that the Seamless SSO feature is enabled in Microsoft Entra Connect. If you can't enable the feature (for example, due to a blocked port), ensure that you have all the [prerequisites](how-to-connect-sso-quick-start#step-1-check-the-prerequisites) in place.
- If you have enabled both [Microsoft Entra join](../../devices/overview) and Seamless SSO on your tenant, ensure that the issue is not with Microsoft Entra join. SSO from Microsoft Entra join takes precedence over Seamless SSO if the device is both registered with Microsoft Entra ID and domain-joined. With SSO from Microsoft Entra join the user sees a sign-in tile that says "Connected to Windows".
- Ensure that the Microsoft Entra URL (`https://autologon.microsoftazuread-sso.com`) is part of the user's Intranet zone settings.
- Ensure that the corporate device is joined to the Active Directory domain. The device *doesn't* need to be [Microsoft Entra joined](../../devices/overview) for Seamless SSO to work.
- Ensure that the user is logged on to the device through an Active Directory domain account.
- Ensure that the user's account is from an Active Directory forest where Seamless SSO has been set up.
- Ensure that the device is connected to the corporate network.
- Ensure that the device's time is synchronized with the time in both Active Directory and the domain controllers, and that they are within five minutes of each other.
- Ensure that the `AZUREADSSOACC` computer account is present and enabled in each AD forest that you want Seamless SSO enabled. If the computer account has been deleted or is missing, you can use PowerShell cmdlets to re-create them.
- List the existing Kerberos tickets on the device by using the `klist` command from a command prompt. Ensure that the tickets issued for the `AZUREADSSOACC` computer account are present. Users' Kerberos tickets are typically valid for 10 hours. You might have different settings in Active Directory.
- If you disabled and re-enabled Seamless SSO on your tenant, users won't get the single sign-on experience until their cached Kerberos tickets have expired.
- Purge existing Kerberos tickets from the device by using the `klist purge` command, and try again.
- To determine if there are JavaScript-related problems, review the console logs of the browser (under **Developer Tools**).
- Review the domain controller logs.

### Domain controller logs

If you enable success auditing on your domain controller, then every time a user signs in through Seamless SSO, a security entry is recorded in the event log. You can find these security events by using the following query. (Look for event **4769** associated with the computer account **AzureADSSOAcc$**.)

```
  <QueryList>
    <Query Id="0" Path="Security">
      <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
    </Query>
  </QueryList>
```

## Manual reset of the feature

If troubleshooting didn't help, you can manually reset the feature on your tenant. Follow these steps on the on-premises server where you're running Microsoft Entra Connect.

### Step 1: Import the ADSync and Seamless SSO PowerShell modules

1. Ensure Microsoft Entra Connect is installed. Download it from the [Microsoft Entra Admin Center](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted).
2. Import the ADSync PowerShell module:

    ```powershell
    Import-Module "$env:ProgramFiles\Microsoft Azure AD Sync\Bin\ADSync\ADSync.psd1"
    ```
3. Browse to the `%ProgramFiles%\Microsoft Azure Active Directory Connect` folder.
4. Import the Seamless SSO PowerShell module:

    ```powershell
    Import-Module .\AzureADSSO.psd1
    ```

### Step 2: Get the list of Active Directory forests on which Seamless SSO has been enabled

1. Run PowerShell as an administrator. In PowerShell, call `New-AzureADSSOAuthenticationContext`. When prompted, enter your tenant's Hybrid Identity Administrator credentials.
2. Call `Get-AzureADSSOStatus`. This command provides you with the list of Active Directory forests (look at the "Domains" list) on which this feature has been enabled.

### Step 3: Disable Seamless SSO for each Active Directory forest where you've set up the feature

1. Call `$creds = Get-Credential`. When prompted, enter the domain administrator credentials for the intended Active Directory forest.

    Note

    The domain administrator credentials username must be entered in the SAM account name format (contoso\johndoe or contoso.com\johndoe). We use the domain portion of the username to locate the Domain Controller of the Domain Administrator using DNS.

    Note

    The domain administrator account used must not be a member of the Protected Users group. If so, the operation will fail.
2. Call `Disable-AzureADSSOForest -OnPremCredentials $creds`. This command removes the `AZUREADSSOACC` computer account from the on-premises domain controller for this specific Active Directory forest.

    Note

    If for any reason you can't access your AD on-premises, you can skip **steps 3.1** and **3.2** and instead call `Disable-AzureADSSOForest -DomainFqdn <Domain name from the output list in step 2>`.
3. Repeat the preceding steps for each Active Directory forest where you’ve set up the feature.

### Step 4: Enable Seamless SSO for each Active Directory forest

1. Call `Enable-AzureADSSOForest`. When prompted, enter the domain administrator credentials for the intended Active Directory forest.

    Note

    The domain administrator credentials username must be entered in the SAM account name format (contoso\johndoe or contoso.com\johndoe). We use the domain portion of the username to locate the Domain Controller of the Domain Administrator using DNS.

    Note

    The domain administrator account used must not be a member of the Protected Users group. If so, the operation will fail.
2. Repeat the preceding step for each Active Directory forest where you want to set up the feature.

### Step 5: Enable the feature on your tenant

To turn on the feature on your tenant, call `Enable-AzureADSSO -Enable $true`.