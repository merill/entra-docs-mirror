---
layout: Conceptual
title: Known issues and troubleshooting for hybrid FIDO2 security keys - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-authentication-passwordless-troubleshoot
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about some known issues and ways to troubleshoot passwordless hybrid FIDO2 security key sign-in using Microsoft Entra ID
ms.topic: troubleshooting
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: aakapo
ms.custom: sfi-ga-nochange
locale: en-us
document_id: b090d15a-67ab-b973-bbde-8c5959ef2a2a
document_version_independent_id: d2cc01df-6127-8927-480e-26c7516af930
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-authentication-passwordless-troubleshoot.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-authentication-passwordless-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-authentication-passwordless-troubleshoot.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
platformId: e5ce60f8-68e9-fc61-399b-f8950c21f00c
---

# Known issues and troubleshooting for hybrid FIDO2 security keys - Microsoft Entra ID | Microsoft Learn

This article covers frequently asked questions for Microsoft Entra hybrid joined devices and passwordless sign-in to on-premises resources. With this passwordless feature, you can enable Microsoft Entra authentication on Windows 10 devices for Microsoft Entra hybrid joined devices using FIDO2 security keys. Users can sign into Windows on their devices with modern credentials like FIDO2 keys and access traditional Active Directory Domain Services (AD DS) based resources with a seamless single sign-on (SSO) experience to their on-premises resources.

The following scenarios for users in a hybrid environment are supported:

- Sign in to Microsoft Entra hybrid joined devices using FIDO2 security keys and get SSO access to on-premises resources.
- Sign in to Microsoft Entra joined devices using FIDO2 security keys and get SSO access to on-premises resources.

To get started with FIDO2 security keys and hybrid access to on-premises resources, see the following articles:

- [Passwordless security keys](howto-authentication-passwordless-security-key)
- [Passwordless Windows 10](howto-authentication-passwordless-security-key-windows)
- [Passwordless on-premises](howto-authentication-passwordless-security-key-on-premises)

## Known issues

- Users are unable to sign in using FIDO2 security keys as Windows Hello Face is too quick and is the default sign-in mechanism
- Users aren't able to use FIDO2 security keys immediately after they create a Microsoft Entra hybrid joined machine
- Users are unable to get SSO to my NTLM network resource after signing in with a FIDO2 security key and receiving a credential prompt

### Users are unable to sign in using FIDO2 security keys as Windows Hello Face is too quick and is the default sign-in mechanism

Windows Hello Face is the intended best experience for a device where a user is enrolled. FIDO2 security keys are intended for use on shared devices or where Windows Hello for Business enrollment is a barrier.

If Windows Hello Face prevents the users from trying the FIDO2 security key sign-in scenario, users can turn off Hello Face sign in by removing Face Enrollment in **Settings &gt; Sign-In Options**.

### Users aren't able to use FIDO2 security keys immediately after they create a Microsoft Entra hybrid joined machine

After the domain-join and restart process on a clean install of a Microsoft Entra hybrid joined machine, you must sign in with a password and wait for policy to synchronize before you can use to use a FIDO2 security key to sign in.

This behavior is a known limitation for domain-joined devices, and isn't specific to FIDO2 security keys.

To check the current status, use the `dsregcmd /status` command. Check that both *AzureAdJoined* and *DomainJoined* show *YES*.

### Users are unable to get SSO to my NTLM network resource after signing in with a FIDO2 security key and receiving a credential prompt

Make sure that enough DCs are patched to respond in time to service your resource request. To check if you can see a server that is running the feature, review the output of `nltest /dsgetdc:<dc name> /keylist /kdc`

If you're able to see a DC with this feature, the user's password may have changed since they signed in, or there's another issue. Collect logs as detailed in the following section for the Microsoft support team to debug.

## Troubleshoot

There are two areas to troubleshoot - Window client issues, or deployment issues.

### Windows Client Issues

To collect data that helps troubleshoot issues with signing in to Windows or accessing on-premises resources from Windows 10 devices, complete the following steps:

1. Open the **Feedback hub** app. Make sure that your name is on the bottom left of the app, then select **Create a new feedback item**.

    For the feedback item type, choose *Problem*.
2. Select the *Security and Privacy* category, then the *FIDO* subcategory.
3. Toggle the check box for *Send attached files and diagnostics to Microsoft along with my feedback*.
4. Select *Recreate my problems*, then *Start capture*.
5. Lock and unlock the machine with FIDO2 security key. If the issue occurs, try to unlock with other credentials.
6. Return to **Feedback Hub**, select **Stop capture**, and submit your feedback.
7. Go to the *Feedback* page, then the *My Feedback* tab. Select your recently submitted feedback.
8. Select the *Share* button in the top-right corner to get a link to the feedback. Include this link when you open a support case, or reply to the engineer assigned to an existing support case.

The following events logs and registry key info is collected:

**Registry keys**

- *HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Microsoft\FIDO [\*]*
- *HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Microsoft\PassportForWork\* [\*]*
- *HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Policies\PassportForWork\* [\*]*

**Diagnostic information**

- Live kernel dump
- Collect AppX package information
- UIF context files

**Event logs**

- *%SystemRoot%\System32\winevt\Logs\Microsoft-Windows-AAD%40Operational.evtx*
- *%SystemRoot%\System32\winevt\Logs\Microsoft-Windows-WebAuthN%40Operational.evtx*
- *%SystemRoot%\System32\winevt\Logs\Microsoft-Windows-HelloForBusiness%40Operational.evtx*

### Deployment Issues

To troubleshoot issues with deploying the Microsoft Entra Kerberos server, use the logs for the new [AzureADHybridAuthenticationManagement](https://www.powershellgallery.com/packages/AzureADHybridAuthenticationManagement) PowerShell module.

#### Viewing the logs

The Microsoft Entra Kerberos server PowerShell cmdlets in the [AzureADHybridAuthenticationManagement](https://www.powershellgallery.com/packages/AzureADHybridAuthenticationManagement) module use the same logging as the standard Microsoft Entra Connect Wizard. To view information or error details from the cmdlets, complete the following steps:

1. On the machine where the [AzureADHybridAuthenticationManagement](https://www.powershellgallery.com/packages/AzureADHybridAuthenticationManagement) module was used, browse to `C:\ProgramData\AADConnect\`. This folder is hidden by default.
2. Open and view the most recent `trace-*.log` file located in the directory.

#### Viewing the Microsoft Entra Kerberos server Objects

To view the Microsoft Entra Kerberos server Objects and verify they are in good order, complete the following steps:

1. On the Microsoft Entra Connect Server or any other machine where the [AzureADHybridAuthenticationManagement](https://www.powershellgallery.com/packages/AzureADHybridAuthenticationManagement) module is installed, open PowerShell and navigate to `C:\Program Files\Microsoft Azure Active Directory Connect\AzureADKerberos\`
2. Run the following PowerShell commands to view the Microsoft Entra Kerberos server from both Microsoft Entra ID and on-premises AD DS.

    Replace *corp.contoso.com* with the name of your on-premises AD DS domain.

    ```powershell
    Import-Module ".\AzureAdKerberos.psd1"
    
    # Specify the on-premises AD DS domain.
    $domain = "corp.contoso.com"
    
    # Enter an Azure Active Directory Global Administrator username and password.
    $cloudCred = Get-Credential
    
    # Enter a Domain Admin username and password.
    $domainCred = Get-Credential
    
    # Get the Azure AD Kerberos Server Object
    Get-AzureADKerberosServer -Domain $domain -CloudCredential $cloudCred -DomainCredential
    $domainCred
    ```

The command outputs the properties of the Microsoft Entra Kerberos server from both Microsoft Entra ID and on-premises AD DS. Review the properties to verify that everything is in good order. Use the table below to verify the properties.

The first set of properties is from the objects in the on-premises AD DS environment. The second half (the properties that begin with *Cloud*\*) are from the Kerberos Server object in Microsoft Entra ID:

| Property | Description |
| --- | --- |
| Id | The unique *Id* of the AD DS domain controller object. |
| DomainDnsName | The DNS domain name of the AD DS domain. |
| ComputerAccount | The computer account object of the Microsoft Entra Kerberos server object (the DC). |
| UserAccount | The disabled user account object that holds the Microsoft Entra Kerberos server TGT encryption key. The DN of this account is *CN=krbtgt\_AzureAD,CN=Users,&lt;Domain-DN&gt;* |
| KeyVersion | The key version of the Microsoft Entra Kerberos server TGT encryption key. The version is assigned when the key is created. The version is then incremented every time the key is rotated. The increments are based on replication meta-data and will likely be greater than one. For example, the initial *KeyVersion* could be *192272*. The first time the key is rotated, the version could advance to *212621*. The important thing to verify is that the *KeyVersion* for the on-premises object and the *CloudKeyVersion* for the cloud object are the same. |
| KeyUpdatedOn | The date and time that the Microsoft Entra Kerberos server TGT encryption key was updated or created. |
| KeyUpdatedFrom | The DC where the Microsoft Entra Kerberos server TGT encryption key was last updated. |
| CloudId | The *Id* from the Microsoft Entra Object. Must match the *Id* above. |
| CloudDomainDnsName | The *DomainDnsName* from the Microsoft Entra Object. Must match the *DomainDnsName* above. |
| CloudKeyVersion | The *KeyVersion* from the Microsoft Entra Object. Must match the *KeyVersion* above. |
| CloudKeyUpdatedOn | The *KeyUpdatedOn* from the Microsoft Entra Object. Must match the *KeyUpdatedOn* above. |