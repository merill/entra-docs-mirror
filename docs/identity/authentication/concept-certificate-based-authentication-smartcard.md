---
layout: Conceptual
title: Windows smart card sign-in using Microsoft Entra certificate-based authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-certificate-based-authentication-smartcard
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to enable Windows smart card sign-in using Microsoft Entra certificate-based authentication
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: vimrang
ms.custom: has-adal-ref
locale: en-us
document_id: add7ba93-5dec-f033-c42a-ce94a7a461f3
document_version_independent_id: a5cfa4c8-ee72-0bf7-8523-f2e75f92e5ef
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-certificate-based-authentication-smartcard.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-certificate-based-authentication-smartcard
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-certificate-based-authentication-smartcard.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 52241235-d3b2-f769-e4d4-ff31eb1714fc
---

# Windows smart card sign-in using Microsoft Entra certificate-based authentication - Microsoft Entra ID | Microsoft Learn

Microsoft Entra users can authenticate using X.509 certificates on their smart cards directly against Microsoft Entra ID at Windows sign-in. There's no special configuration needed on the Windows client to accept the smart card authentication.

## User experience

Follow these steps to set up Windows smart card sign-in:

1. Join the machine to either Microsoft Entra ID or a hybrid environment (hybrid join).
2. Configure Microsoft Entra CBA in your tenant as described in [Configure Microsoft Entra CBA](how-to-certificate-based-authentication).
3. Make sure the user is either on managed authentication or using [Staged Rollout](../hybrid/connect/how-to-connect-staged-rollout).
4. Present the physical or virtual smart card to the test machine.
5. Select the smart card icon, enter the PIN, and authenticate the user.

    ![Screenshot of smart card sign-in.](media/concept-certificate-based-authentication/smartcard.png)

Users will get a primary refresh token (PRT) from Microsoft Entra ID after the successful sign-in. Depending on the CBA configuration, the PRT will contain the multifactor claim.

## Expected behavior of Windows sending user UPN to Microsoft Entra CBA

| Sign-in | Microsoft Entra join | Hybrid join |
| --- | --- | --- |
| First sign-in | Pull from certificate | AD UPN or x509Hint |
| Subsequent sign-in | Pull from certificate | Cached Microsoft Entra UPN |

### Windows rules for sending UPN for Microsoft Entra joined devices

Windows will first use a principal name and if not present then RFC822Name from the SubjectAlternativeName (SAN) of the certificate being used to sign into Windows. If neither are present, the user must additionally supply a User Name Hint. For more information, see [User Name Hint](/en-us/windows/security/identity-protection/smart-cards/smart-card-group-policy-and-registry-settings#allow-user-name-hint)

### Windows rules for sending UPN for Microsoft Entra hybrid joined devices

Hybrid Join sign-in must first successfully sign-in against the Active Directory(AD) domain. The users AD UPN is sent to Microsoft Entra ID. In most cases, the Active Directory UPN value is the same as the Microsoft Entra UPN value and is synchronized with Microsoft Entra Connect.

Some customers may maintain different and sometimes may have non-routable UPN values in Active Directory (such as user@woodgrove.local) In these cases the value sent by Windows may not match the users Microsoft Entra UPN. To support these scenarios where Microsoft Entra ID can't match the value sent by Windows, a subsequent lookup is performed for a user with a matching value in their **onPremisesUserPrincipalName** attribute. If the sign-in is successful, Windows will cache the users Microsoft Entra UPN and is sent in subsequent sign-ins.

Note

In all cases, a user supplied username login hint (X509UserNameHint) will be sent if provided. For more information, see [User Name Hint](/en-us/windows/security/identity-protection/smart-cards/smart-card-group-policy-and-registry-settings#allow-user-name-hint)

Important

If a user supplies a username login hint (X509UserNameHint), the value provided **MUST** be in UPN Format.

For more information about the Windows flow, see [Certificate Requirements and Enumeration (Windows)](/en-us/windows/security/identity-protection/smart-cards/smart-card-certificate-requirements-and-enumeration).

## Supported Windows platforms

The Windows smart card sign-in works with the latest preview build of Windows 11. The functionality is also available for these earlier Windows versions after you apply one of the following updates [KB5017383](https://support.microsoft.com/topic/september-20-2022-kb5017383-os-build-22000-1042-preview-62753265-68e9-45d2-adcb-f996bf3ad393):

- [Windows 11 - kb5017383](https://support.microsoft.com/topic/september-20-2022-kb5017383-os-build-22000-1042-preview-62753265-68e9-45d2-adcb-f996bf3ad393)
- [Windows 10 - kb5017379](https://support.microsoft.com/topic/20-september-2022-kb5017379-os-build-17763-3469-preview-50a9b9e2-745d-49df-aaae-19190e10d307)
- [Windows Server 20H2- kb5017380](https://support.microsoft.com/topic/20-september-2022-kb5017380-os-builds-19042-2075-19043-2075-og-19044-2075-preview-59ab550c-105e-4481-b440-c37f07bf7897)
- [Windows Server 2022 - kb5017381](https://support.microsoft.com/topic/20-september-2022-kb5017381-os-build-20348-1070-preview-dc843fea-bccd-4550-9891-a021ae5088f0)
- [Windows Server 2019 - kb5017379](https://support.microsoft.com/topic/20-september-2022-kb5017379-os-build-17763-3469-preview-50a9b9e2-745d-49df-aaae-19190e10d307)

## Supported browsers

| Edge | Chrome | Safari | Firefox |
| --- | --- | --- | --- |
| ✅ | ✅ | ✅ | ✅ |

Note

Microsoft Entra CBA supports both certificates on-device as well as external storage like security keys on Windows.

## Windows Out of the box experience (OOBE)

Windows OOBE should allow the user to login using an external smart card reader and authenticate against Microsoft Entra CBA. Windows OOBE by default should have the necessary smart card drivers or the smart card drivers previously added to the Windows image before OOBE setup.

## Restrictions and caveats

- Microsoft Entra CBA is supported on Windows devices that are hybrid or Microsoft Entra joined.
- Users must be in a managed domain or using Staged Rollout and can't use a federated authentication model.