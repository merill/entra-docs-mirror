---
layout: Conceptual
title: Tutorial - Issue a Microsoft Entra Verified ID credential for directory-based claims - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/how-to-use-quickstart-verifiedemployee
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: In this tutorial, you learn how to issue verifiable credentials, from directory based claims, by using a sample app.
ms.topic: tutorial
ms.date: 2025-01-31T00:00:00.0000000Z
locale: en-us
document_id: 0978f65e-4e06-a4e3-d682-bed270ad8a44
document_version_independent_id: bb93b86c-c6ec-d46f-7ff5-0b0555853e89
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/how-to-use-quickstart-verifiedemployee.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/how-to-use-quickstart-verifiedemployee
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/how-to-use-quickstart-verifiedemployee.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 54065104-18cc-5ae4-1b15-563d07cb662d
---

# Tutorial - Issue a Microsoft Entra Verified ID credential for directory-based claims - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Employees with accounts in your Microsoft Entra ID environment can have Verifiable Credentials of the type VerifiedEmployee, created with claims sourced from their user profiles. In this tutorial, you create a credential with claims sourced from a user's profile in Microsoft Entra ID.

You can create VerifiedEmployee credentials using the [Quick setup](verifiable-credentials-configure-tenant-quick) or the [advanced setup](verifiable-credentials-configure-tenant). If you use the quick setup, the VerifiedEmployee credential is automatically created for you in a workforce tenant. If you use the advanced setup, you need to manually create the VerifiedEmployee credential as explained in this guide.

Issuing a VerifiedEmployee credential is now supported in [MyAccount](https://myaccount.microsoft.com). Instructions to enable it in Verified ID are available in the [quick setup guide](verifiable-credentials-configure-tenant-quick#myaccount-available-now-to-simplify-issuance-of-workplace-credentials). Configuring a sample to issue VerifiedEmployee credentials is only necessary if you would like to handle issuance in your own app.

In this article, you learn how to:

- Create a user in the directory.
- Set up the user for Microsoft Authenticator.
- Create a Verified employee credential.
- Configure the samples to issue and verify your VerifiedEmployee credential.

## Prerequisites

- [Set up a tenant for Microsoft Entra Verified ID Credentials](verifiable-credentials-configure-tenant).
- Complete the tutorial for [issuance](verifiable-credentials-configure-issuer) and [verification](verifiable-credentials-configure-verifier) of verifiable credentials.
- A mobile phone with Microsoft Authenticator that can be used as the test user account.

## Configure your test user account

1. [Create a new user](../fundamentals/how-to-create-delete-users#create-a-new-user) to use in your testing.
2. Sign in with your new user. The user name would be something like meganb@yourtenant.onmicrosoft.com. You must change your password.

### Set up your test user for Microsoft Authenticator

Your test user needs to have Microsoft Authenticator set up for the account. To enable Authenticator on the test user account, follow these steps:

1. On your mobile test device, open Microsoft Authenticator, go to the Authenticator tab at the bottom and tap **+** sign to **Add account**. Select **Work or school account**.
2. At the prompt, select **Sign in**. Don't select "Scan QR code".
3. Sign in with the test user’s credentials in the Microsoft Entra tenant.
4. Authenticator launches https://aka.ms/mfasetup in the browser on your mobile device. You need to sign in again with your test user's credentials.
5. In the **Set up your account in the app**, select **Pair your account to the app by clicking this link**. The Microsoft Authenticator app opens and you see your test user as an added account.

If https://aka.ms/mfasetup launches without prompting you to sign in, that means Microsoft Authenticator is already set up for another user on this device. When already configured with a user, Authenticator signs you in automatically. Sign out the browser and then set up authenticator again. If you zoom in on the page, you find the **Sign out** button at the top right corner.

## Create a Verified employee credential

When you select + Add credential in the portal, you get the option to launch two quickstarts. Select **Verified employee** and select Next.

![Screenshot of the quickstart start screen.](media/how-to-use-quickstart-verifiedemployee/verifiable-credentials-configure-verifiedemployee-quickstart.png)

In the next screen, you enter some of the Display definitions, like logo URL, text and background color. Since the credential is a managed credential with directory based claims, rules definitions are predefined and can't be changed. You don't need to enter rule definition details. The credential type is **VerifiedEmployee** and the claims from the user’s profile are preset. Select Create to create the credential.

![Screenshot of the created credential, verified employee, card styling section.](media/how-to-use-quickstart-verifiedemployee/verifiable-credentials-configure-verifiedemployee-styling.png)

## Claims schema for Verified employee credential

All of the claims in the Verified employee credential come from attributes in the [user's profile](/en-us/graph/api/resources/user) in Microsoft Entra ID for the issuing tenant. You can't modify the set of claims. All claims, except photo, come from the Microsoft Graph Query [https://graph.microsoft.com/v1.0/me](/en-us/graph/api/user-get). The photo claim comes from the value returned from the Microsoft Graph Query [https://graph.microsoft.com/v1.0/me/photo/$value.](/en-us/graph/api/profilephoto-get)

| Claim | Directory attribute | Value |
| --- | --- | --- |
| `revocationId` | `userPrincipalName` | The UPN of the user is added as a claim named `revocationId` and gets indexed. |
| `displayName` | `displayName` | The displayName of the user |
| `givenName` | `givenName` | First name of the user |
| `surname` | `surname` | Last name of the user |
| `jobTitle` | `jobTitle` | The user's job title. This attribute doesn't have a value by default in the user's profile. If the user's profile has no value specified, there's no `jobTitle` claim in the issued VC. |
| `preferredLanguage` | `preferredLanguage` | Should follow [ISO 639-1](https://en.wikipedia.org/wiki/ISO_639-1) and contain a value like `en-us`. There's no default value specified. If there's no value, no claim is included in the issued VC. |
| `mail` | `mail` | The user's email address. The `mail` value isn't the same as the UPN. It's also an attribute that doesn't have a value by default. |
| `photo` | `photo` | The uploaded photo for the user. The image type should be JPEG and the maximum size is 2 MB. When presenting the photo claim to a verifier, the photo claim is in the UrlEncode(Base64Encode(photo)) format. To use the photo, the verifier application has to Base64Decode(UrlDecode(photo)). |

See full Microsoft Entra user profile [properties reference](/en-us/graph/api/resources/user).

Important

If attribute values change in the user's Microsoft Entra profile, the VC isn't automatically reissued. You must reissue it manually. Issuance would be the same as the issuance process when working with the samples.

## Configure the samples to issue and verify your VerifiedEmployee credential

Verifiable Credentials for directory based claims can be issued and verified just like any other credentials you create. All you need is your issuer DID for your tenant, the credential type, and the manifest url to your credential. The easiest way to find these values for a Managed Credential is to view the credential in the portal, select **Issue credential** and you get a header named **Custom issue**. These steps bring up a textbox with a skeleton JSON payload for the Request Service API.

![Screenshot of the custom issuance request section.](media/how-to-use-quickstart-verifiedemployee/verifiable-credentials-configure-verifiedemployee-custom-issue.png)

In this screen, you have values that you can copy and paste to your sample deployment’s configuration files. Issuer’s DID is the authority value.

- **authority** - Issuer's DID
- **type** - the credential type is always `VerifiedEmployee` when looking at a verified employee credential
- **manifest** - the credential manifest URL

The configuration file depends on the sample in-use.

- **Dotnet** - [appsettings.json](https://github.com/Azure-Samples/active-directory-verifiable-credentials-dotnet/blob/main/1-asp-net-core-api-idtokenhint/appsettings.json)
- **Node** - [config.json](https://github.com/Azure-Samples/active-directory-verifiable-credentials-node/blob/main/1-node-api-idtokenhint/config.json)
- **python** - [config.json](https://github.com/Azure-Samples/active-directory-verifiable-credentials-python/blob/main/1-python-api-idtokenhint/config.json)
- **Java** - values are set as environment variables in [run.cmd](https://github.com/Azure-Samples/active-directory-verifiable-credentials-java/blob/main/1-java-api-idtokenhint/run.cmd) and [run.sh](https://github.com/Azure-Samples/active-directory-verifiable-credentials-java/blob/main/1-java-api-idtokenhint/run.sh) or docker-run.cmd/docker-run.sh when using docker.

## Remarks

Note

This schema is fixed and it isn't supported to add or remove claims in the schema. The attestation flow for directory based claims is also fixed and it's unsupported to try to change it to become a custom credential with ID token hint attestation flow, for example.