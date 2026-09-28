---
layout: Conceptual
title: Emergency rotation of the AD FS certificates - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-emergency-ad-fs-certificate-rotation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article explains how to revoke and update AD FS certificates immediately.
ms.custom: no-azure-ad-ps-ref
ms.topic: how-to
ms.date: 2025-09-18T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: d07e307c-6490-c054-d29f-38c760253f78
document_version_independent_id: 7327bf78-d008-3b5b-2f7c-70b84c25e9d8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-emergency-ad-fs-certificate-rotation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-emergency-ad-fs-certificate-rotation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-emergency-ad-fs-certificate-rotation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2ce2ea8f-6f0c-ec58-3e12-f11f27302bde
---

# Emergency rotation of the AD FS certificates - Microsoft Entra ID | Microsoft Learn

If you need to rotate the Active Directory Federation Services (AD FS) certificates immediately, you can follow the steps in this article.

Important

Rotating certificates in the AD FS environment revokes the old certificates immediately, and the time it usually takes for your federation partners to consume your new certificate is bypassed. The action might also result in a service outage as trusts update to use the new certificates. The outage should be resolved after all the federation partners have the new certificates.

Note

We highly recommend that you use a Hardware Security Module (HSM) to protect and secure certificates. For more information, see the [Hardware Security Module](/en-us/windows-server/identity/ad-fs/deployment/best-practices-securing-ad-fs#hardware-security-module-hsm) section in the best practices for securing AD FS.

## Determine your Token Signing Certificate thumbprint

To revoke the old Token Signing Certificate that AD FS is currently using, you need to determine the thumbprint of the token-signing certificate. From your ADFS Server do the following:

1. Connect to the Microsoft Entra PowerShell module:

    `Connect-Entra -Scopes 'Domain.Read.All'`.
2. Document both your on-premises and cloud Token Signing Certificate thumbprint and expiration dates by running:

    - `Get-AdfsCertificate -CertificateType token-signing`
    - `Get-EntraFederationProperty -DomainName <your_domain.com> | FL Source, SigningCertificate`.
3. Copy the thumbprint. You'll use it later to remove the existing certificates.

You can also get the thumbprint by using AD FS Management. Go to **Service** &gt; **Certificates**, right-click the certificate, select **View certificate**, and then select **Details**.

## Determine whether AD FS renews the certificates automatically

By default, AD FS is configured to generate token signing and token decryption certificates automatically. It does so both during the initial configuration and when the certificates are approaching their expiration date.

You can run the following PowerShell command: `Get-AdfsProperties | FL AutoCert*, Certificate*`.

The `AutoCertificateRollover` property describes whether AD FS is configured to renew token signing and token decrypting certificates automatically. Do either of the following:

- If `AutoCertificateRollover` is set to `TRUE`, generate a new self-signed certificate.
- If `AutoCertificateRollover` is set to `FALSE`, generate new certificates manually.

## If AutoCertificateRollover is set to TRUE, generate a new self-signed certificate

In this section, you create *two* token-signing certificates. The first uses the `-urgent` flag, which replaces the current primary certificate immediately. The second is used for the secondary certificate.

Important

You're creating two certificates because Microsoft Entra ID holds on to information about the previous certificate. By creating a second one, you're forcing Microsoft Entra ID to release information about the old certificate and replace it with information about the second one.

If you don't create the second certificate and update Microsoft Entra ID with it, it might be possible for the old token-signing certificate to authenticate users.

To generate the new token-signing certificates, do the following:

1. Ensure that you're logged in to the primary AD FS server.
2. Open Windows PowerShell as an administrator.
3. Make sure that `AutoCertificateRollover` is set to `True` by running in PowerShell:

    `Get-AdfsProperties | FL AutoCert*, Certificate*`
4. To generate a new token signing certificate, run:

    `Update-ADFSCertificate -CertificateType Token-Signing -Urgent`
5. Verify the update by running:

    `Get-ADFSCertificate -CertificateType Token-Signing`
6. Now generate the second token signing certificate by running:

    `Update-ADFSCertificate -CertificateType Token-Signing`
7. You can verify the update by running the following command again:

    `Get-ADFSCertificate -CertificateType Token-Signing`

## If AutoCertificateRollover is set to FALSE, generate new certificates manually

If you're not using the default automatically generated, self-signed token signing and token decryption certificates, you must renew and configure these certificates manually. Doing so involves creating two new token-signing certificates and importing them. Then, you promote one to primary, revoke the old certificate, and configure the second certificate as the secondary certificate.

First, you must obtain two new certificates from your certificate authority and import them into the local machine personal certificate store on each federation server. For instructions, see [Import a Certificate](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754489%28v=ws.11%29).

Important

You're creating two certificates because Microsoft Entra ID holds on to information about the previous certificate. By creating a second one, you're forcing Microsoft Entra ID to release information about the old certificate and replace it with information about the second one.

If you don't create the second certificate and update Microsoft Entra ID with it, it might be possible for the old token-signing certificate to authenticate users.

### Configure a new certificate as a secondary certificate

Next, configure one certificate as the secondary AD FS token signing or decryption certificate and then promote it to the primary.

1. After you've imported the certificate, open the **AD FS Management** console.
2. Expand **Service**, and then select **Certificates**.
3. On the **Actions** pane, select **Add Token-Signing Certificate**.
4. Select the new certificate from the list of displayed certificates, and then select **OK**.

### Promote the new certificate from secondary to primary

Now that you've imported the new certificate and configured it in AD FS, you need to set it as the primary certificate.

1. Open the **AD FS Management** console.
2. Expand **Service**, and then select **Certificates**.
3. Select the secondary token signing certificate.
4. On the **Actions** pane, select **Set As Primary**. At the prompt, select **Yes**.
5. After you've promoted the new certificate as the primary certificate, you should remove the old certificate because it can still be used. For more information, see the Remove your old certificates section.

### To configure the second certificate as a secondary certificate

Now that you've added the first certificate, made it primary, and removed the old one, you can import the second certificate. Configure the certificate as the secondary AD FS token signing certificate by doing the following:

1. After you've imported the certificate, open the **AD FS Management** console.
2. Expand **Service**, and then select **Certificates**.
3. On the **Actions** pane, select **Add Token-Signing Certificate**.
4. Select the new certificate from the list of displayed certificates, and then select **OK**.

## Update Microsoft Entra ID with the new token-signing certificate

1. Connect to Microsoft Entra ID by running the following command:

    `Connect-Entra -Scopes 'Domain.Read.All'`
2. Enter your [Hybrid Identity Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator) credentials.
3. Optionally, verify whether an update is required by checking the current certificate information in Microsoft Entra ID. To do so, run the following command:

    `Get-EntraFederationProperty -DomainName <your_domain.com> | FL Source, SigningCertificate` and convert the Base64 Encoded cert to a readable format to check the certificate expiration and thumbprint.
4. To update the certificate information in Microsoft Entra ID, run the following command: `Update-MgDomainFederationConfiguration -DomainId <your_domain.com> -InternalDomainFederationId <hex_domainID>`.

    Important

    You can get the **-InternalDomainFederationId** value by running the following command:

    `Get-EntraFederationProperty -DomainName your_domain.com`

    ![Screenshot shows output of the Get-EntraFederationProperty cmdlet.](media/how-to-connect-install-multiple-domains/entra-fed-property.png)

## Replace SSL certificates

If you need to replace your token-signing certificate because of a compromise, you should also revoke and replace the Secure Sockets Layer (SSL) certificates for AD FS and your Web Application Proxy (WAP) servers.

Revoking your SSL certificates must be done at the certificate authority (CA) that issued the certificate. These certificates are often issued by third-party providers, such as GoDaddy. For an example, see [Revoke a certificate | SSL Certificates - GoDaddy Help US](https://www.godaddy.com/help/revoke-a-certificate-4747). For more information, see [How certificate revocation works](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee619754%28v=ws.10%29).

After the old SSL certificate has been revoked and a new one issued, you can replace the SSL certificates. For more information, see [Replace the SSL certificate for AD FS](/en-us/windows-server/identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap#replacing-the-ssl-certificate-for-ad-fs).

## Remove your old certificates

After you've replaced your old certificates, you should remove the old certificate because it can still be used. To do so:

1. Ensure that you're logged in to the primary AD FS server.
2. Open Windows PowerShell as an administrator.
3. To remove the old token signing certificate, run:

    `Remove-ADFSCertificate -CertificateType Token-Signing -thumbprint <thumbprint>`

## Update federation partners who can consume federation metadata

If you've renewed and configure a new token signing or token decryption certificate, you must make sure that all your federation partners have picked up the new certificates. This list includes resource organization or account organization partners that are represented in AD FS by relying party trusts and claims provider trusts.

## Update federation partners who can't consume federation metadata

If your federation partners can't consume your federation metadata, you must manually send them the public key of your new token-signing / token-decrypting certificate. Send your new certificate public key (.cer file or .p7b if you want to include the entire chain) to all your resource organization or account organization partners (represented in your AD FS by relying party trusts and claims provider trusts). Have the partners implement changes on their side to trust the new certificates.

## Revoke the refresh tokens via PowerShell

Now you want to revoke the refresh tokens for users who might have them and force them to log in again and get new tokens. This logs users out of their phones, current webmail sessions, and other places that are using tokens and refresh tokens. For more information, see [Revoke-EntraUserAllRefreshToken](/en-us/powershell/module/microsoft.entra.authentication/revoke-entrauserallrefreshtoken). Also see [Revoke user access in Microsoft Entra ID](../../users/users-revoke-access).