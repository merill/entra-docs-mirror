---
layout: Conceptual
title: Security update to remove support for KDFv1 algorithm for authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/deprecation-key-derivation-function-version-1
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Removal of Key Derivation Function version 1 algorithm and proactive guidance for device administrators.
ms.topic: troubleshooting
ms.date: 2025-06-27T00:00:00.0000000Z
ms.reviewer: sgrandhi
locale: en-us
document_id: 72713874-ec8f-35a8-66c8-f519d57bf486
document_version_independent_id: 72713874-ec8f-35a8-66c8-f519d57bf486
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/deprecation-key-derivation-function-version-1.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/deprecation-key-derivation-function-version-1
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/deprecation-key-derivation-function-version-1.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 9e654c20-445e-7c42-91be-3733c790f00b
---

# Security update to remove support for KDFv1 algorithm for authentication - Microsoft Entra ID | Microsoft Learn

Microsoft is removing support for the Key Derivation Function version 1 (KDFv1) algorithm used for the authentication of Microsoft Entra joined or Microsoft Entra hybrid joined devices in builds of Windows released before July 2021.

The KDFv1 algorithm was historically used for device authentication in earlier versions of Windows. A critical security flaw was discovered that allowed unauthorized authentication, as outlined in [CVE-2021-33781](https://www.cve.org/CVERecord?id=CVE-2021-33781). To address this vulnerability, Microsoft issued a Windows security update in July 2021. All Windows builds released after July 2021 no longer use the KDFv1 algorithm.

As part of our ongoing commitment to enhancing security, Microsoft is incrementally rolling out a security update that blocks the use of the KDFv1 algorithm for authentication with Microsoft Entra.

## Effects of the security update

All Windows devices that authenticate using Microsoft Entra must have the security patch applied or be running builds of Windows released after July 2021. Unpatched Windows devices won't authenticate with Microsoft Entra once the rollout of this change completes.

### Error messages

Users on unpatched devices encounter the following error message when attempting to sign in:

> 
> Sign-in error code: 5000611
> 
> Failure reason: Symmetric Key Derivation Function version '1' is invalid. Update the device with the latest updates.

This error message is also present in the Microsoft Entra sign-in logs, allowing administrators to identify authentication failures due to the deprecated KDFv1 algorithm.

Note

Due to the incremental rollout of the security update, authentication failures on unpatched Windows devices may initially appear transient or intermittent. Early in the rollout retrying authentication will likely succeed. It is important to address these issues promptly by applying Windows security updates to maintain seamless authentication experiences.

## Actions required

Microsoft Entra administrators should proactively identify and address devices within their tenant that might be impacted by this security update. The following steps are recommended:

- Monitor Authentication Failures: Regularly check the Microsoft Entra sign-in logs for the error code 5000611 and the corresponding failure reason.
- Update Devices: If users report authentication failures with an error message referencing the KDFv1 algorithm, update their devices with the latest security updates for their Windows version.
- Search for Impacted Builds: Use the guidance provided in CVE Record CVE-2021-33781 to search for Windows devices within your tenant that might be running impacted builds.
- Communicate with Users: Inform users about the importance of keeping their devices updated and provide instructions on how to apply necessary updates.

### Proactive monitoring and updating

Proactively monitoring and updating devices is crucial to avoid any authentication disruptions. Microsoft Entra administrators can utilize the following strategies:

- Automated updates: Implement policies for automated updates to ensure all devices receive the latest security patches promptly.
- Regular audits: Conduct regular audits of your devices to ensure compliance with security update requirements.
- User training: Educate users about the significance of timely updates and how to check for and apply them.