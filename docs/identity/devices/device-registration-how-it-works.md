---
layout: Conceptual
title: How Microsoft Entra device registration works - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/device-registration-how-it-works
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Microsoft Entra device registration flows for managed and federated domains.
ms.topic: concept-article
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: 
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8cb105c7-df5f-ad21-d5c0-32f6e48ab5fc
document_version_independent_id: a6baa965-434d-0392-0edd-3cf6850467a4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/device-registration-how-it-works.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/device-registration-how-it-works
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/device-registration-how-it-works.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 907e4b81-eba8-2fba-f846-107e0bef5e6d
---

# How Microsoft Entra device registration works - Microsoft Entra ID | Microsoft Learn

Device Registration is a prerequisite to cloud-based authentication. Commonly, devices are Microsoft Entra ID or Microsoft Entra hybrid joined to complete device registration. This article provides details of how Microsoft Entra join and Microsoft Entra hybrid join work in managed and federated environments. For more information about how Microsoft Entra authentication works on these devices, see the article [Primary refresh tokens](concept-primary-refresh-token#detailed-flows).

## Microsoft Entra joined in Managed environments

[![Microsoft Entra joined  device flow in a managed environment](media/device-registration-how-it-works/device-registration-azure-ad-managed.png)](media/device-registration-how-it-works/device-registration-azure-ad-managed.png#lightbox)

| Phase | Description |
| --- | --- |
| A | The most common way Microsoft Entra joined devices register is during the out-of-box-experience (OOBE) where it loads the Microsoft Entra join web application in the Cloud Experience Host (CXH) application. The application sends a GET request to the Microsoft Entra OpenID configuration endpoint to discover authorization endpoints. Microsoft Entra ID returns the OpenID configuration, which includes the authorization endpoints, to application as JSON document. |
| B | The application builds a sign-in request for the authorization end point and collects user credentials. |
| C | After the user provides their user principal name (UPN), the application sends a GET request to Microsoft Entra ID to discover corresponding realm information for the user. This information determines if the environment is managed or federated. Microsoft Entra ID returns the information in a JSON object. The application determines the environment is managed (nonfederated).The last step in this phase has the application create an authentication buffer and if in OOBE, temporarily caches it for automatic sign-in at the end of OOBE. The application POSTs the credentials to Microsoft Entra ID where they're validated. Microsoft Entra ID returns an ID token with claims. |
| D | The application looks for mobile device management (MDM) terms of use (the mdm\_tou\_url claim). If present, the application retrieves the terms of use from the claim's value, present the contents to the user, and waits for the user to accept the terms of use. This step is optional and skipped if the claim isn't present or if the claim value is empty. |
| E | The application sends a device registration discovery request to the Azure Device Registration Service (DRS). Azure DRS returns a discovery data document, which returns tenant-specific URIs to complete device registration. |
| F | The application creates TPM bound (preferred) RSA 2048 bit key-pair known as the device key (dkpub/dkpriv). The application creates a certificate request using dkpub and the public key and signs the certificate request with using dkpriv. Next, the application derives second key pair from the TPM's storage root key. This key is the transport key (tkpub/tkpriv). |
| G | The application sends a device registration request to Azure DRS that includes the ID token, certificate request, tkpub, and attestation data. Azure DRS validates the ID token, creates a device ID, and creates a certificate based on the included certificate request. Azure DRS then writes a device object in Microsoft Entra ID and sends the device ID and the device certificate to the client. |
| H | Device registration completes by receiving the device ID and the device certificate from Azure DRS. The device ID is saved for future reference (viewable from `dsregcmd.exe /status`), and the device certificate is installed in the Personal store of the computer. With device registration complete, the process continues with MDM enrollment. |

## Microsoft Entra joined in Federated environments

[![Microsoft Entra joined  device flow in a federated environment](media/device-registration-how-it-works/device-registration-azure-ad-federated.png)](media/device-registration-how-it-works/device-registration-azure-ad-federated.png#lightbox)

| Phase | Description |
| --- | --- |
| A | The most common way Microsoft Entra joined devices register is during the out-of-box-experience (OOBE) where it loads the Microsoft Entra join web application in the Cloud Experience Host (CXH) application. The application sends a GET request to the Microsoft Entra OpenID configuration endpoint to discover authorization endpoints. Microsoft Entra ID returns the OpenID configuration, which includes the authorization endpoints, to application as JSON document. |
| B | The application builds a sign-in request for the authorization end point and collects user credentials. |
| C | After the user provides their user name (in UPN format), the application sends a GET request to Microsoft Entra ID to discover corresponding realm information for the user. This information determines if the environment is managed or federated. Microsoft Entra ID returns the information in a JSON object. The application determines the environment is federated.The application redirects to the AuthURL value (on-premises STS sign-in page) in the returned JSON realm object. The application collects credentials through the STS web page. |
| D | The application POST the credential to the on-premises STS, which might require extra factors of authentication. The on-premises STS authenticates the user and returns a token. The application POSTs the token to Microsoft Entra ID for authentication. Microsoft Entra ID validates the token and returns an ID token with claims. |
| E | The application looks for MDM terms of use (the mdm\_tou\_url claim). If present, the application retrieves the terms of use from the claim's value, present the contents to the user, and waits for the user to accept the terms of use. This step is optional and skipped if the claim isn't present or if the claim value is empty. |
| F | The application sends a device registration discovery request to the Azure Device Registration Service (DRS). Azure DRS returns a discovery data document, which returns tenant-specific URIs to complete device registration. |
| G | The application creates TPM bound (preferred) RSA 2048 bit key-pair known as the device key (dkpub/dkpriv). The application creates a certificate request using dkpub and the public key and signs the certificate request with using dkpriv. Next, the application derives second key pair from the TPM's storage root key. This key is the transport key (tkpub/tkpriv). |
| H | The application sends a device registration request to Azure DRS that includes the ID token, certificate request, tkpub, and attestation data. Azure DRS validates the ID token, creates a device ID, and creates a certificate based on the included certificate request. Azure DRS then writes a device object in Microsoft Entra ID and sends the device ID and the device certificate to the client. |
| I | Device registration completes by receiving the device ID and the device certificate from Azure DRS. The device ID is saved for future reference (viewable from `dsregcmd.exe /status`), and the device certificate is installed in the Personal store of the computer. With device registration complete, the process continues with MDM enrollment. |

## Microsoft Entra hybrid joined in Managed environments

[![Screenshot of Microsoft Entra hybrid joined device flow in a managed environment.](media/device-registration-how-it-works/device-registration-hybrid-azure-ad-managed.png)](media/device-registration-how-it-works/device-registration-hybrid-azure-ad-managed.png#lightbox)

| Phase | Description |
| --- | --- |
| A | The user signs in to a domain joined Windows 10 or newer computer using domain credentials. This credential can be user name and password or smart card authentication. The user sign-in triggers the Automatic Device Join task. The Automatic Device Join tasks is triggered on domain join and retried every hour. It doesn't solely depend on the user sign-in. |
| B | The task queries Active Directory using the LDAP protocol for the keywords attribute on the service connection point stored in the configuration partition in Active Directory (`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=corp,DC=contoso,DC=com`). The value returned in the keywords attribute determines if device registration is directed to Azure Device Registration Service (DRS) or the enterprise device registration service hosted on-premises. |
| C | For the managed environment, the task creates an initial authentication credential in the form of a self-signed certificate. The task writes the certificate to the userCertificate attribute on the computer object in Active Directory using LDAP. |
| D | The computer can't authenticate to Azure DRS until a device object representing the computer that includes the certificate on the userCertificate attribute is created in Microsoft Entra ID. Microsoft Entra Connect detects an attribute change. On the next synchronization cycle, Microsoft Entra Connect sends the userCertificate, object GUID, and computer SID to Azure DRS. Azure DRS uses the attribute information to create a device object in Microsoft Entra ID. |
| E | The Automatic Device Join task triggers with each user sign-in or every hour, and tries to authenticate the computer to Microsoft Entra ID using the corresponding private key of the public key in the userCertificate attribute. Microsoft Entra authenticates the computer and issues an ID token to the computer. |
| F | The task creates TPM bound (preferred) RSA 2048 bit key-pair known as the device key (dkpub/dkpriv). The application creates a certificate request using dkpub and the public key and signs the certificate request with using dkpriv. Next, the application derives second key pair from the TPM's storage root key. This key is the transport key (tkpub/tkpriv). |
| G | The task sends a device registration request to Azure DRS that includes the ID token, certificate request, tkpub, and attestation data. Azure DRS validates the ID token, creates a device ID, and creates a certificate based on the included certificate request. Azure DRS then updates the device object in Microsoft Entra ID and sends the device ID and the device certificate to the client. |
| H | Device registration completes by receiving the device ID and the device certificate from Azure DRS. The device ID is saved for future reference (viewable from `dsregcmd.exe /status`), and the device certificate is installed in the Personal store of the computer. With device registration complete, the task exits. |

## Microsoft Entra hybrid joined in Federated environments

[![Microsoft Entra hybrid joined device flow in a managed environment](media/device-registration-how-it-works/device-registration-hybrid-azure-ad-federated.png)](media/device-registration-how-it-works/device-registration-hybrid-azure-ad-federated.png#lightbox)

| Phase | Description |
| --- | --- |
| A | The user signs in to a domain joined Windows 10 or newer computer using domain credentials. This credential can be user name and password or smart card authentication. The user sign-in triggers the Automatic Device Join task. The Automatic Device Join tasks is triggered on domain join and retried every hour. It doesn't solely depend on the user sign-in. |
| B | The task queries Active Directory using the LDAP protocol for the keywords attribute on the service connection point stored in the configuration partition in Active Directory (`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=corp,DC=contoso,DC=com`). The value returned in the keywords attribute determines if device registration is directed to Azure Device Registration Service (DRS) or the enterprise device registration service hosted on-premises. |
| C | For the federated environments, the computer authenticates the enterprise device registration endpoint using Windows Integrated Authentication. The enterprise device registration service creates and returns a token that includes claims for the object GUID, computer SID, and domain joined state. The task submits the token and claims to Microsoft Entra ID where they're validated. Microsoft Entra ID returns an ID token to the running task. |
| D | The application creates TPM bound (preferred) RSA 2048 bit key-pair known as the device key (dkpub/dkpriv). The application creates a certificate request using dkpub and the public key and signs the certificate request with using dkpriv. Next, the application derives second key pair from the TPM's storage root key. This key is the transport key (tkpub/tkpriv). |
| E | To provide SSO for on-premises federated application, the task requests an enterprise PRT from the on-premises STS. Windows Server 2016 running the Active Directory Federation Services role validate the request and return it the running task. |
| F | The task sends a device registration request to Azure DRS that includes the ID token, certificate request, tkpub, and attestation data. Azure DRS validates the ID token, creates a device ID, and creates a certificate based on the included certificate request. Azure DRS then writes a device object in Microsoft Entra ID and sends the device ID and the device certificate to the client. Device registration completes by receiving the device ID and the device certificate from Azure DRS. The device ID is saved for future reference (viewable from `dsregcmd.exe /status`), and the device certificate is installed in the Personal store of the computer. With device registration complete, the task exits. |
| G | If Microsoft Entra Connect device writeback is enabled, Microsoft Entra Connect requests updates from Microsoft Entra ID at its next synchronization cycle (device writeback is required for hybrid deployment using certificate trust). Microsoft Entra ID correlates the device object with a matching synchronized computer object. Microsoft Entra Connect receives the device object that includes the object GUID and computer SID and writes the device object to Active Directory. |