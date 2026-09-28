---
layout: Conceptual
title: Secure group managed service accounts - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/service-accounts-group-managed
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide to securing group managed service accounts (gMSAs)
ms.topic: how-to
ms.date: 2023-02-09T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 4b50bdb8-c331-4ce5-e391-e726f49a11d2
document_version_independent_id: f9b1d5db-9e91-ec5a-490c-d8ddbb71eb23
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/service-accounts-group-managed.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/service-accounts-group-managed
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/service-accounts-group-managed.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 036779f7-e1a3-7a00-e83f-5e14e547b840
---

# Secure group managed service accounts - Microsoft Entra | Microsoft Learn

Group managed service accounts (gMSAs) are domain accounts to help secure services. gMSAs can run on one server, or in a server farm, such as systems behind a network load balancing or Internet Information Services (IIS) server. After you configure your services to use a gMSA principal, account password management is handled by the Windows operating system (OS).

## Benefits of gMSAs

gMSAs are an identity solution with greater security that help reduce administrative overhead:

- **Set strong passwords** - 240-byte, randomly generated passwords: the complexity and length of gMSA passwords minimizes the likelihood of compromise by brute force or dictionary attacks
- **Cycle passwords regularly** - password management goes to the Windows OS, which changes the password every 30 days. Service and domain administrators don't need to schedule password changes, or manage service outages.
- **Support deployment to server farms** - deploy gMSAs to multiple servers to support load balanced solutions where multiple hosts run the same service
- **Support simplified service principal name (SPN) management**- set up an SPN with PowerShell, when you create an account.
    - In addition, services that support automatic SPN registrations might do so against the gMSA, if the gMSA permissions are set correctly.

## Using gMSAs

Use gMSAs as the account type for on-premises services unless a service, such as failover clustering, doesn't support it.

Important

Test your service with gMSAs before it goes to production. Set up a test environment to ensure the application uses the gMSA, then accesses resources. For more information, see [Support for group managed service accounts](/en-us/system-center/scom/support-group-managed-service-accounts?view=sc-om-2022&amp;preserve-view=true).

If a service doesn't support gMSAs, you can use a standalone managed service account (sMSA). An sMSA has the same functionality, but is intended for deployment on a single server.

If you can't use a gMSA or sMSA supported by your service, configure the service to run as a standard user account. Service and domain administrators are required to observe strong password management processes to help keep the account secure.

## Assess gMSA security posture

gMSAs are more secure than standard user accounts, which require ongoing password management. However, consider gMSA scope of access in relation to security posture. Potential security issues and mitigations for using gMSAs are shown in the following table:

| Security issue | Mitigation |
| --- | --- |
| gMSA is a member of privileged groups | - Review your group memberships. Create a PowerShell script to enumerate group memberships. Filter the resultant CSV file by gMSA file names - Remove the gMSA from privileged groups - Grant the gMSA rights and permissions it requires to run its service. See your service vendor. |
| gMSA has read/write access to sensitive resources | - Audit access to sensitive resources - Archive audit logs to a SIEM, such as Azure Log Analytics or Microsoft Sentinel - Remove unnecessary resource permissions if there's an unnecessary access level |

## Find gMSAs

### Managed Service Accounts container

To work effectively, gMSAs must be in the Managed Service Accounts container in Active Directory Users and Computers.

To find service MSAs not in the list, run the following commands:

```powershell

Get-ADServiceAccount -Filter *

# This PowerShell cmdlet returns managed service accounts (gMSAs and sMSAs). Differentiate by examining the ObjectClass attribute on returned accounts.

# For gMSA accounts, ObjectClass = msDS-GroupManagedServiceAccount

# For sMSA accounts, ObjectClass = msDS-ManagedServiceAccount

# To filter results to only gMSAs:

Get-ADServiceAccount –Filter * | where-object {$_.ObjectClass -eq "msDS-GroupManagedServiceAccount"}
```

## Manage gMSAs

To manage gMSAs, use the following Active Directory PowerShell cmdlets:

`Get-ADServiceAccount`

`Install-ADServiceAccount`

`New-ADServiceAccount`

`Remove-ADServiceAccount`

`Set-ADServiceAccount`

`Test-ADServiceAccount`

`Uninstall-ADServiceAccount`

Note

In Windows Server 2012, and later versions, the \*-ADServiceAccount cmdlets work with gMSAs. Learn more: [Get started with group managed service accounts](/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts).

## Move to a gMSA

gMSAs are a secure service account type for on-premises. It's recommended you use gMSAs, if possible. In addition, consider moving your services to Azure and your service accounts to Microsoft Entra ID.

Note

Before you configure your service to use the gMSA, see [Get started with group managed service accounts](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431%28v=ws.11%29).

To move to a gMSA:

1. Ensure the Key Distribution Service (KDS) root key is deployed in the forest. This is a one-time operation. See, [Create the Key Distribution Services KDS Root Key](/en-us/windows-server/security/group-managed-service-accounts/create-the-key-distribution-services-kds-root-key).
2. Create a new gMSA. See, [Getting Started with Group Managed Service Accounts](/en-us/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts).
3. Install the new gMSA on hosts that run the service.
4. Change your service identity to gMSA.
5. Specify a blank password.
6. Validate your service is working under the new gMSA identity.
7. Delete the old service account identity.