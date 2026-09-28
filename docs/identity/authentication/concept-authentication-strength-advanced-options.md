---
layout: Conceptual
title: Create and Manage Custom Conditional Access Authentication Strengths - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-strength-advanced-options
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how admins can create custom authentication strengths with advanced options for passkey (FIDO2) security keys and certificate-based authentication.
ms.topic: how-to
ms.date: 2026-06-26T00:00:00.0000000Z
ms.reviewer: inbarc
ms.custom: sfi-image-nochange
locale: en-us
document_id: 15fceb88-05e3-df67-6a00-3f72d50d391b
document_version_independent_id: 15fceb88-05e3-df67-6a00-3f72d50d391b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-strength-advanced-options.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-strength-advanced-options
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-strength-advanced-options.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: f28b1974-f0ab-e72f-5ff9-354f2f9a9a79
---

# Create and Manage Custom Conditional Access Authentication Strengths - Microsoft Entra ID | Microsoft Learn

An authentication strength is a Microsoft Entra Conditional Access control that specifies combinations of authentication methods for access to a resource. As an administrator, you can create up to 15 custom authentication strengths to exactly suit your requirements.

## Prerequisites

- To use Conditional Access, your tenant needs to have Microsoft Entra ID P1 license. If you don't have this license, you can start a [free trial](https://www.microsoft.com/security/business/get-started/start-free-trial).

## Create a custom authentication strength

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](../role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Authentication strengths**.
3. Select **New authentication strength**.
4. For **Name**, provide a descriptive name for your new authentication strength.
5. For **Description**, you can provide an optional description.
6. Select the available methods that you want to allow. For example, to create a custom authentication strength that requires QR code sign-in for a group of users such as frontline workers, expand **Single factor authentication**, and then select **QR code**.
7. Select **Next** and review the policy configuration.

![Screenshot that shows a custom authentication strength with QR code selected.](media/concept-authentication-strengths/authentication-strength-custom.png)

## Update and delete custom authentication strengths

You can edit a custom authentication strength. If a Conditional Access policy references that authentication strength, you can't delete it, and you need to confirm any edit.

To check if a Conditional Access policy references an authentication strength, go to the **Conditional Access policies** column.

## Configure advanced options for passkeys (FIDO2)

You can restrict the usage of passkeys (FIDO2) based on their Authenticator Attestation GUIDs (AAGUIDs). You can use this capability to require a FIDO2 security key from a specific manufacturer for access to a resource:

1. After you create a custom authentication strength, select **Passkeys (FIDO2)** &gt; **Advanced options**.

    ![Screenshot that shows the link for advanced options for passkeys.](media/concept-authentication-strengths/key.png)
2. Next to **Add AAGUID**, select the plus sign (**+**), copy the AAGUID value, and then select **Save**.

    ![Screenshot that shows how to add an Authenticator Attestation GUID.](media/concept-authentication-strengths/guid.png)

## Configure advanced options for certificate-based authentication

In the [authentication binding policy](how-to-certificate-based-authentication#step-3-configure-an-authentication-binding-policy), you can configure whether certificates are bound in the system to single-factor or multifactor authentication protection levels, based on the certificate issuer or policy object identifier (OID). You can also require single-factor or multifactor authentication certificates for specific resources, based on a Conditional Access authentication strength policy.

By using advanced options for authentication strength, you can require a specific certificate issuer or policy OID to further restrict sign-ins to an application.

For example, assume that an organization named Contoso issues smart cards to employees with three different types of multifactor certificates. One certificate is for confidential clearance, another is for secret clearance, and a third is for top-secret clearance. Each one is distinguished by properties of the certificate, such as issuer or policy OID. Contoso wants to ensure that only users who have the appropriate multifactor certificate can access data for each classification.

The next sections show how to configure advanced options for certificate-based authentication (CBA) by using the Microsoft Entra admin center and Microsoft Graph.

### Microsoft Entra admin center

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an administrator.
2. Browse to **Entra ID** &gt; **Authentication methods** &gt; **Authentication strengths**.
3. Select **New authentication strength**.
4. For **Name**, provide a descriptive name for your new authentication strength.
5. For **Description**, you can provide an optional description.
6. Below the option for certificate-based authentication (either single-factor or multifactor), select **Advanced options**.

    ![Screenshot that shows the link for advanced options for certificate-based authentication.](media/concept-authentication-strength-advanced-options/certificate-advanced-options.png)
7. Select or enter the certificate issuers, and enter the allowed policy OIDs.

    You can configure certificate issuers by selecting them in the **Certificate issuers from the certificate authorities in your tenant** dropdown list. The dropdown list shows all certificate authorities from the tenant, whether they're single-factor or multifactor.

    For scenarios where the certificate that you want to use is not uploaded to the certificate authorities in your tenant, you can enter certificate issuers in the **Other Certificate Issuers by SubjectkeyIdentifier** box. One such example is external user scenarios, where the user could be authenticating in the home tenant and the authentication strength is being enforced on the resource tenant.

    ![Screenshot that shows the configuration options for certificate issuers and policy object identifiers.](media/concept-authentication-strength-advanced-options/or-other-issuer.png)

    These conditions apply:

    - If you configure both attributes (certificate issuers and policy OIDs), the user must use a certificate that has at least one of the issuers *and* one of the policy OIDs from the list to satisfy the authentication strength.
    - If you configure only the certificate issuers attribute, the user must use a certificate that has at least one of the issuers to satisfy the authentication strength.
    - If you configure only the policy OIDs attribute, the user must use a certificate that has at least one of the policy OIDs to satisfy the authentication strength.

    Note

    You can configure a maximum of five issuers and five OIDs for an authentication strength.
8. Select **Next** to review the configuration, and then select **Create**.

### Microsoft Graph

To create a new Conditional Access authentication strength policy by using `combinationConfigurations` for a certificate, use this code:

```json
POST  /beta/identity/conditionalAccess/authenticationStrength/policies
{
    "displayName": "CBA Restriction",
    "description": "CBA Restriction with both IssuerSki and OIDs",
    "allowedCombinations": [
        " x509CertificateMultiFactor "
    ],
    "combinationConfigurations": [
        {
            "@odata.type": "#microsoft.graph.x509CertificateCombinationConfiguration",
            "appliesToCombinations": [
                "x509CertificateMultiFactor"
            ],
            "allowedIssuerSkis": ["9A4248C6AC8C2931AB2A86537818E92E7B6C97B6"],
            "allowedPolicyOIDs": [
                "1.2.3.4.6",
                "1.2.3.4.5.6"
            ]
        }
    ]
}
```

To add new `combinationConfiguration` information to an existing policy, use this code:

```json
POST beta/identity/conditionalAccess/authenticationStrength/policies/{authenticationStrengthPolicyId}/combinationConfigurations

{
    "@odata.type": "#microsoft.graph.x509CertificateCombinationConfiguration",
    "allowedIssuerSkis": [
        "9A4248C6AC8C2931AB2A86537818E92E7B6C97B6"
    ],
    "allowedPolicyOIDs": [],
    "appliesToCombinations": [
        "x509CertificateSingleFactor "
    ]
}
```

## Understand limitations

### Advanced options for passkeys (FIDO2)

Advanced options for passkeys (FIDO2) aren't supported for external users whose home tenant and resource tenant are located in different Microsoft clouds.

### Advanced options for certificate-based authentication

- A user can use only one certificate in each browser session. After the user signs in with a certificate, it's cached in the browser for the duration of the session. The user isn't prompted to choose another certificate if it doesn't meet the authentication strength requirements. The user needs to sign out and sign back in to restart the session, and then choose the relevant certificate.
- Certificate authorities and user certificates should conform to the X.509 v3 standard. Specifically, to enforce CBA restrictions for issuer subject key identifiers (SKIs), certificates need valid authority key identifiers (AKIs).

    ![Screenshot that shows an authority key identifier.](media/concept-authentication-strength-advanced-options/subject-key-identifier.png)

    Note

    If the certificate doesn't conform, user authentication might succeed but not satisfy the issuer SKI restrictions for the authentication strength policy.
- During sign-in, Microsoft Entra ID considers the first five policy OIDs from the user certificate and compares them with the policy OIDs configured in the authentication strength policy. If the user certificate has more than five policy OIDs, Microsoft Entra ID takes into account the first five policy OIDs (in lexical order) that match the authentication strength requirements.
- For business-to-business users, let's take an example where Contoso invites users from another organization (Fabrikam) to its tenant. In this case, Contoso is the resource tenant and Fabrikam is the home tenant. Access depends on the cross-tenant access setting:

    - When the cross-tenant access setting is **Off**, it means Contoso doesn't accept MFA that the home tenant performed. Certificate-based authentication on the resource tenant isn't supported.
    - When cross-tenant access setting is **On**, Fabrikam and Contoso tenants are on the same Microsoft cloud (the Azure commercial cloud platform or the Azure for US Government cloud platform). In addition, Contoso trusts MFA that was performed on the home tenant. In this case:
        - The admin can restrict access to a specific resource by using the policy OIDs or the **Other Certificate Issuers by SubjectkeyIdentifier** setting in the custom authentication strength policy.
        - The admin can restrict access to specific resources by using the **Other Certificate Issuers by SubjectkeyIdentifier** setting in the custom authentication strength policy.
    - When the cross-tenant access setting is **On**, Fabrikam and Contoso aren't on the same Microsoft cloud. For example, Fabrikam's tenant is on the Azure commercial cloud platform and Contoso's tenant is on the Azure for US Government cloud platform. The admin can't restrict access to specific resources by using the issuer ID or policy OIDs in the custom authentication strength policy.

## Troubleshoot advanced options for authentication strengths

### Users can't use their passkey (FIDO2) to sign in

A Conditional Access administrator can restrict access to specific security keys. When a user tries to sign in with a key that they can't use, a "You can't get there from here" message appears. The user has to restart the session and sign in with a different passkey (FIDO2).

![Screenshot of a sign-in error when a user is using a restricted passkey.](media/troubleshoot-authentication-strengths/restricted-security-key.png)

### You need to check the certificate issuer or policy OID

You can confirm that the personal certificate properties match the configuration in the advanced options for authentication strengths:

1. On the user's device, sign in as an administrator.
2. Select **Run**, type **certmgr.msc**, and then select the Enter key.
3. Select **Personal** &gt; **Certificates**, right-click the certificate, and then go to the **Details** tab.

![Screenshot that shows selections for checking a certificate issuer or policy OID.](media/concept-authentication-strength-advanced-options/certificate-manager-msc.png)