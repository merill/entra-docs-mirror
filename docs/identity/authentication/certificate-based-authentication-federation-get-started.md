---
layout: Conceptual
title: Certificate-based authentication with federation - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/certificate-based-authentication-federation-get-started
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to configure certificate-based authentication with federation in your environment
ms.custom: has-azure-ad-ps-ref, sfi-image-nochange
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: vraganathan
locale: en-us
document_id: 6f50b3f0-0af5-89f3-f29a-f73bf5bba678
document_version_independent_id: a4f5dae2-373d-38bb-dd1e-9fbbd7bb3703
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/certificate-based-authentication-federation-get-started.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/certificate-based-authentication-federation-get-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/certificate-based-authentication-federation-get-started.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
2PlusCloud:
- Azure
- M365
- Power
__autotagging_hash:
- D6943B2AB3A7C73128A90CB1EB88E96B5329FCFFEFBB136B97683BA389FC5A41
platformId: e5e02ac8-344c-c3b6-5090-0e98ccca6c60
---

# Certificate-based authentication with federation - Microsoft Entra ID | Microsoft Learn

Certificate-based authentication (CBA) with federation enables Microsoft Entra ID to authenticate you with a client certificate on a Windows, Android, or iOS device when connecting your Exchange online account to:

- Microsoft mobile applications such as Microsoft Outlook and Microsoft Word
- Exchange ActiveSync (EAS) clients

Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.

Note

As an alternative, organizations can deploy Microsoft Entra CBA without needing federation. For more information, see [Overview of Microsoft Entra certificate-based authentication against Microsoft Entra ID](concept-certificate-based-authentication).

This topic:

- Provides steps to configure and utilize CBA for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.
- Assumes that you already have a [public key infrastructure (PKI)](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740%28v=ws.11%29) and [AD FS](/en-us/entra/identity/hybrid/connect/how-to-connect-fed-whatis) configured.

## Requirements

To configure CBA with federation, the following statements must be true:

- CBA with federation is only supported for Federated environments for browser applications, native clients using modern authentication, or MSAL libraries. The one exception is Exchange Active Sync (EAS) for Exchange Online (EXO), which can be used for federated and managed accounts. To configure Microsoft Entra CBA without needing federation, see [How to configure Microsoft Entra certificate-based authentication](how-to-certificate-based-authentication).
- The root certificate authority and any intermediate certificate authorities must be configured in Microsoft Entra ID.
- Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an internet-facing URL.
- You must have at least one certificate authority configured in Microsoft Entra ID. You can find related steps in the Configure the certificate authorities section.
- For Exchange ActiveSync clients, the client certificate must have the user's routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field. Microsoft Entra ID maps the RFC822 value to the Proxy Address attribute in the directory.
- Your client device must have access to at least one certificate authority that issues client certificates.
- A client certificate for client authentication must have been issued to your client.

Important

The maximum size of a CRL for Microsoft Entra ID to successfully download and cache is 20MB, and the time required to download the CRL must not exceed 10 seconds. If Microsoft Entra ID can't download a CRL, certificate based authentications using certificates issued by the corresponding CA will fail. Best practices to ensure CRL files are within size constraints are to keep certificate lifetimes to within reasonable limits and to clean up expired certificates.

## Step 1: Select your device platform

As a first step, for the device platform you care about, you need to review the following:

- The Office mobile applications support
- The specific implementation requirements

The related information exists for the following device platforms:

- [Android](certificate-based-authentication-federation-android)
- [iOS](certificate-based-authentication-federation-ios)

## Step 2: Configure the certificate authorities

To configure your certificate authorities in Microsoft Entra ID, for each certificate authority, upload the following:

- The public portion of the certificate, in *.cer* format
- The internet-facing URLs where the Certificate Revocation Lists (CRLs) reside

The schema for a certificate authority looks as follows:

```csharp
    class TrustedCAsForPasswordlessAuth
    {
       CertificateAuthorityInformation[] certificateAuthorities;
    }

    class CertificateAuthorityInformation

    {
        CertAuthorityType authorityType;
        X509Certificate trustedCertificate;
        string crlDistributionPoint;
        string deltaCrlDistributionPoint;
        string trustedIssuer;
        string trustedIssuerSKI;
    }

    enum CertAuthorityType
    {
        RootAuthority = 0,
        IntermediateAuthority = 1
    }
```

For the configuration, you can use [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph):

1. Start Windows PowerShell with administrator privileges.
2. Install [Microsoft Graph PowerShell](/en-us/powershell/microsoftgraph/installation):

    ```powershell
        Install-Module Microsoft.Graph
    ```

As a first configuration step, you need to establish a connection with your tenant. As soon as a connection to your tenant exists, you can review, add, delete, and modify the trusted certificate authorities that are defined in your directory.

### Connect

To establish a connection with your tenant, use [Connect-MgGraph](/en-us/powershell/microsoftgraph/authentication-commands#using-connect-mggraph):

```powershell
    Connect-MgGraph
```

### Retrieve

To retrieve the trusted certificate authorities that are defined in your directory, use [Get-MgOrganizationCertificateBasedAuthConfiguration](/en-us/powershell/module/microsoft.graph.identity.signins/get-mgorganizationcertificatebasedauthconfiguration).

```powershell
    Get-MgOrganizationCertificateBasedAuthConfiguration
```

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

To add, modify, or remove a CA, use the Microsoft Entra admin center:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Entra ID** &gt; **Identity Secure Score** &gt; **Certificate authorities**.
3. To upload a CA, select **Upload**:

    1. Select the CA file.
    2. Select **Yes** if the CA is a root certificate, otherwise select **No**.
    3. For **Certificate Revocation List URL**, set the internet-facing URL for the CA base CRL that contains all revoked certificates. If the URL isn't set, authentication with revoked certificates won't fail.
    4. For **Delta Certificate Revocation List URL**, set the internet-facing URL for the CRL that contains all revoked certificates since the last base CRL was published.
    5. Select **Add**.

        ![Screenshot of how to upload certification authority file.](media/how-to-certificate-based-authentication/upload-certificate-authority.png)
4. To delete a CA certificate, select the certificate and select **Delete**.
5. Select **Columns** to add or delete columns.

## Step 3: Configure revocation

To revoke a client certificate, Microsoft Entra ID fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it. The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid. The CRL is periodically referenced to revoke access to certificates that are a part of the list.

If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated. To invalidate the authorization token, set the **StsRefreshTokensValidFrom** field for this particular user using Windows PowerShell. You must update the **StsRefreshTokensValidFrom** field for each user you want to revoke access for.

To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokensValidFrom** and ensure the certificate in question is in the CRL.

The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokensValidFrom** field.

```https
# Authenticate to Microsoft Graph
Connect-MgGraph -Scopes "User.Read.All"

# Get the user
$user = Get-MgUser -UserPrincipalName "test@contoso.com"

# Get the StsRefreshTokensValidFrom property
$user.StsRefreshTokensValidFrom
```

The date you set must be in the future. If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set. If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).

## Step 4: Test your configuration

### Testing your certificate

As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.

If your sign-in is successful, then you know that:

- The user certificate has been provisioned to your test device
- AD FS is configured correctly

### Testing Office mobile applications

1. On your test device, install an Office mobile application (for example, OneDrive).
2. Launch the application.
3. Enter your username, and then select the user certificate you want to use.

You should be successfully signed in.

### Testing Exchange ActiveSync client applications

To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.

The EAS profile must contain the following information:

- The user certificate to be used for authentication
- The EAS endpoint (for example, outlook.office365.com)

An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Microsoft Intune or by manually placing the certificate in the EAS profile on the device.

### Testing EAS client applications on Android

1. Configure an EAS profile in the application that satisfies the requirements in the prior section.
2. Open the application, and verify that mail is synchronizing.