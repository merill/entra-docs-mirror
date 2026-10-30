---
layout: FAQ
title: Microsoft Entra CBA FAQ - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/certificate-based-authentication-faq
summary: >
  <p>This article addresses frequently asked questions about how Microsoft Entra certificate-based authentication (CBA) works.

  Check back for updated content.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Frequently asked questions and answers for Microsoft Entra certificate-based authentication (CBA).
ms.custom: no-azure-ad-ps-ref - sfi-image-nochange
ms.topic: faq
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: vimrang
locale: en-us
document_id: 4f1688ea-d81d-e3e3-d218-aaf929898feb
document_version_independent_id: e061ad3d-0957-1773-a397-e5fa505a8144
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/certificate-based-authentication-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/certificate-based-authentication-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/certificate-based-authentication-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4154ee21-1258-d4e9-78cc-c5b86d0ce97d
---

# Microsoft Entra CBA FAQ - Microsoft Entra ID | Microsoft Learn

This article addresses frequently asked questions about how Microsoft Entra certificate-based authentication (CBA) works. Check back for updated content.

## Why don't I see an option to sign in to Microsoft Entra ID by using certificates after I enter my username?

An administrator must turn on CBA for the tenant to make the option to sign in by using a certificate available to users. For more information, see [Step 3: Configure the authentication binding policy](how-to-certificate-based-authentication#step-3-configure-an-authentication-binding-policy).

## Where can I get more diagnostic information after a user sign-in fails?

On the error page, select **More Details** for more information to help your tenant admin. The tenant admin can check the sign-in logs to investigate the error. For example, if a user certificate is revoked and is on the certification revocation list (CRL), authentication fails as intended.

## How do we turn on Microsoft Entra CBA?

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with at least the [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator) role assigned.
2. Go to **Entra ID** &gt; **Authentication methods** &gt; **Policies**.
3. Select the **Certificate-based authentication** policy.
4. On the **Enable and Target** tab, select **Enable**.

## Is Microsoft Entra CBA a free feature?

Microsoft Entra CBA is a free feature.

Every edition of Microsoft Entra ID includes Microsoft Entra CBA.

For more information about features in each Microsoft Entra edition, see [Microsoft Entra pricing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

## Does Microsoft Entra CBA support an alternate ID as the username instead of userPrincipalName?

No. Currently, sign-in by using a non-UPN value, such as an alternate email, isn't supported.

## Can I have more than one CRL distribution point for a certificate authority?

No, only one CRL distribution point (CDP) is supported per certificate authority (CA).

## Can I use a non-HTTP URL for a CDP?

No. CDP supports only HTTP URLs.

## How do I find the CRL for a CA, or how do I troubleshoot the error "AADSTS2205015: The Certificate Revocation List (CRL) failed signature validation"?

Download the CRL and compare the CA certificate and the CRL information to validate that the `crlDistributionPoint` value is valid for the CA you want to add. You can configure the CRL to the corresponding CA by matching the CA's issuer subject key identifier (SKI) to the authority key identifier (AKI) of the CRL (CA Issuer SKI == CRL AKI).

The following table and figure show how to map information from the CA certificate to the attributes of the downloaded CRL.

| CA certificate info | = | Downloaded CRL info |
| --- | --- | --- |
| Subject | = | Issuer |
| Subject Key Identifier (SKI) | = | Authority Key Identifier (KeyID) |

![Screenshot that compares CA certificate fields with CRL information.](media/how-to-certificate-based-authentication/certificate-crl-compare.png)

## How do I validate the CA configuration?

It's important to ensure that the Certificate Authority configuration in the trust store results in Microsoft Entra's ability to both validate the certificate authority trust chain. Additionally, it should successfully acquire the certificate revocation list (CRL) from the configured certificate authority CRL distribution point (CDP). To assist with this task, it's recommended to install the [MSIdentity Tools](https://aka.ms/msid) PowerShell module and run [Test-MsIdCBATrustStoreConfiguration](https://github.com/AzureAD/MSIdentityTools/wiki/Test-MsIdCBATrustStoreConfiguration). This PowerShell cmdlet will review the Microsoft Entra tenant certificate authority configuration and surface errors/warnings for common mis-configuration issues.

## Do changes to the authentication methods policy take effect immediately?

The policy is cached. After a policy update, it might take up to an hour for the changes to take effect.

## Why do I see the CBA option after it fails?

The authentication method policy always shows all available authentication methods to the user so that they can retry sign-in by using any method they prefer.

Microsoft Entra ID doesn't hide available methods based on the success or failure of a sign-in.

## Why does CBA loop after it fails?

The browser caches the certificate after the certificate picker appears. If the user retries authentication, the cached certificate is automatically used. The user should close the browser, and then reopen a new session to try CBA again.

## Why doesn't identity proof to register other authentication methods appear as an option when I use single-factor certificates?

A user is considered capable of multifactor authentication (MFA) when the user is in scope for CBA in the authentication methods policy. This policy requirement means that a user can't use identity proof as part of their authentication to register other available methods.

## How can I use single-factor certificates to complete MFA?

We support single-factor CBA to get MFA. CBA single-factor with passwordless phone sign-in and CBA single-factor with FIDO2 are the two supported combinations to get MFA by using single-factor certificates.

For more information, see [MFA with single-factor certificates](concept-certificate-based-authentication-technical-deep-dive#mfa-authentication-flow-by-using-single-factor-certificates-and-passwordless-sign-in).

## The certificateUserIds update fails because it's an existing value. How can an admin query all the user objects that have the same value?

Tenant admins can run Microsoft Graph queries to find all the users that have a specific `certificateUserIds` value. For more information, see [`certificateUserIds` Graph queries](concept-certificate-based-authentication-certificateuserids#update-certificateuserids-using-microsoft-graph-queries).

For example, this command returns all user objects that have the value `bob@contoso.com` in `certificateUserIds`:

```http
GET  https://graph.microsoft.com/v1.0/users?$filter=certificateUserIds/any(x:x eq 'bob@contoso.com')
```

## Can Microsoft Entra CBA be used on Microsoft Surface Hub?

Yes. CBA works out-of-the-box for most combinations of smart card and smart card reader. If the combination smart card and smart card reader requires other drivers, you must install the drivers before you can use the combination smart card and smart card reader on Surface Hub.