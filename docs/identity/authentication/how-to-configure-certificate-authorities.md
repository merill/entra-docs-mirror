---
layout: Conceptual
title: How to configure certificate authorities for Microsoft Entra certificate-based authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-configure-certificate-authorities
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Topic that shows how to configure certificate authorities for Microsoft Entra certificate-based authentication.
ms.topic: how-to
ms.date: 2025-07-02T00:00:00.0000000Z
ms.reviewer: vraganathan
ms.custom: has-adal-ref, has-azure-ad-ps-ref, sfi-ga-nochange
locale: en-us
document_id: 0656e6a6-0628-6ef6-453e-a3cea733f629
document_version_independent_id: 0656e6a6-0628-6ef6-453e-a3cea733f629
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-configure-certificate-authorities.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-configure-certificate-authorities
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-configure-certificate-authorities.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7404ee51-5a53-2ff0-e25e-31b234f04213
---

# How to configure certificate authorities for Microsoft Entra certificate-based authentication - Microsoft Entra ID | Microsoft Learn

The best way to configure the certificate authorities (CAs) is with the PKI-based trust store. You can delegate configuration with a PKI-based trust store to least privileged roles. For more information see, [Step 1: Configure the certificate authorities with PKI-based trust store](how-to-certificate-based-authentication#step-1-configure-the-cas-with-a-pki-based-trust-store).

As an alternative, a Global Administrator can follow steps in this topic to configure CAs by using the Microsoft Entra admin center, or Microsoft Graph REST APIs and the supported software development kits (SDKs), such as Microsoft Graph PowerShell.

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

The public key infrastructure (PKI) infrastructure or PKI admin should be able to provide the list of issuing CAs.

To make sure you configured all the CAs, open the user certificate and click **Certification path** tab. Make sure every CA until the root is uploaded to the Microsoft Entra ID trust store. Microsoft Entra certificate-based authentication (CBA) fails if there are missing CAs.

### Configure certificate authorities using the Microsoft Entra admin center

To configure certificate authorities to enable CBA in the Microsoft Entra admin center, complete the following steps:

Important

Microsoft recommends that you use roles with the fewest permissions. This practice helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios or when you can't use an existing role.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Entra ID** &gt; **Identity Secure Score** &gt; **Certificate authorities**.
3. To upload a CA, select **Upload**:

    1. Select the CA file.
    2. Select **Yes** if the CA is a root certificate, otherwise select **No**.
    3. For **Certificate Revocation List URL**, set the internet-facing URL for the CA base CRL that contains all revoked certificates. If the URL isn't set, authentication with revoked certificates doesn't fail.
    4. For **Delta Certificate Revocation List URL**, set the internet-facing URL for the CRL that contains all revoked certificates since the last base CRL was published.
    5. Select **Add**.

        ![Screenshot of how to upload certificate authority file.](media/how-to-certificate-based-authentication/upload-certificate-authority.png)
4. To delete a CA certificate, select the certificate and select **Delete**.
5. Select **Columns** to add or delete columns.

Note

Upload of a new CA fails if any existing CA expired. You should delete any expired CA, and retry to upload the new CA.

### Configure certificate authorities (CA) using PowerShell

Only one CRL Distribution Point (CDP) for a trusted CA is supported. The CDP can only be HTTP URLs. Online Certificate Status Protocol (OCSP) or Lightweight Directory Access Protocol (LDAP) URLs aren't supported.

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

### Add

Note

Upload of new CAs will fail when any of the existing CAs are expired. Tenant Admin should delete the expired CAs and then upload the new CA.

Follow the preceding steps to add a CA in the Microsoft Entra admin center.

**AuthorityType**

- Use 0 to indicate a Root certificate authority
- Use 1 to indicate an Intermediate or Issuing certificate authority

**crlDistributionPoint**

Download the CRL and compare the CA certificate and the CRL information. Make sure the crlDistributionPoint value in the preceding PowerShell example is valid for the CA you want to add.

The following table and graphic show how to map information from the CA certificate to the attributes of the downloaded CRL.

| CA Certificate Info | = | Downloaded CRL Info |
| --- | --- | --- |
| Subject | = | Issuer |
| Subject Key Identifier | = | Authority Key Identifier (KeyID) |

![Compare CA Certificate with CRL Information.](media/how-to-certificate-based-authentication/certificate-crl-compare.png)

Tip

The value for crlDistributionPoint in the preceding example is the http location for the CA’s Certificate Revocation List (CRL). This value can be found in a few places:

- In the CRL Distribution Point (CDP) attribute of a certificate issued from the CA.

If the issuing CA runs Windows Server:

- On the [Properties](/en-us/windows-server/networking/core-network-guide/cncg/server-certs/configure-the-cdp-and-aia-extensions-on-ca1#to-configure-the-cdp-and-aia-extensions-on-ca1) of the CA in the certificate authority Microsoft Management Console (MMC).
- On the CA by running `certutil -cainfo cdp`. For more information, see [certutil](/en-us/windows-server/administration/windows-commands/certutil#-cainfo).

For more information, see [Understanding the certificate revocation process](concept-certificate-based-authentication-certificate-revocation-list#enforce-crl-validation-for-cas).

### Configure certificate authorities using the Microsoft Graph APIs

Microsoft Graph APIs can be used to configure certificate authorities. To update the Microsoft Entra Certificate Authority trust store, follow the steps at [certificatebasedauthconfiguration MSGraph commands](/en-us/graph/api/resources/certificatebasedauthconfiguration).

### Validate Certificate Authority configuration

Make sure the configuration allows Microsoft Entra CBA to:

- Validate the CA trust chain
- Get the certificate revocation list (CRL) from the configured certificate authority CRL distribution point (CDP)

To validate the CA configuration, install the [MSIdentity Tools](https://azuread.github.io/MSIdentityTools/) PowerShell module, and run [Test-MsIdCBATrustStoreConfiguration](https://github.com/AzureAD/MSIdentityTools/wiki/Test-MsIdCBATrustStoreConfiguration). This PowerShell cmdlet reviews the Microsoft Entra tenant CA configuration. It reports errors and warnings for common misconfigurations.