---
layout: Conceptual
title: Govern on-premises service accounts - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/service-accounts-govern-on-premises
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn to create and run an account lifecycle process for on-premises service accounts
ms.topic: how-to
ms.date: 2023-02-10T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: f97a631f-f31a-c0b4-d7e7-178b0d05e506
document_version_independent_id: f5c5c004-5f6e-c3b1-2511-ded22a376fb1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/service-accounts-govern-on-premises.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/service-accounts-govern-on-premises
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/service-accounts-govern-on-premises.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: aaf49d4e-f093-fb52-4943-e4460c2e9d1e
---

# Govern on-premises service accounts - Microsoft Entra | Microsoft Learn

Active Directory offers four types of on-premises service accounts:

- Group-managed service accounts (gMSAs)
    - [Secure group managed service accounts](service-accounts-group-managed)
- Standalone managed service accounts (sMSAs)
    - [Secure standalone managed service accounts](service-accounts-standalone-managed)
- On-premises computer accounts
    - [Secure on-premises computer accounts with Active Directory](service-accounts-computer)
- User accounts functioning as service accounts
    - [Secure user-based service accounts in Active Directory](service-accounts-user-on-premises)

Part of service account governance includes:

- Protecting them, based on requirements and purpose
- Managing account lifecycle, and their credentials
- Assessing service accounts, based on risk and permissions
- Ensuring Active Directory (AD) and Microsoft Entra ID have no unused service accounts, with permissions

## New service account principles

When you create service accounts, consider the information in the following table.

| Principle | Consideration |
| --- | --- |
| Service account mapping | Connect the service account to a service, application, or script |
| Ownership | Ensure there's an account owner who requests and assumes responsibility |
| Scope | Define the scope, and anticipate usage duration |
| Purpose | Create service accounts for one purpose |
| Permissions | Apply the principle of least permission: - Don't assign permissions to built-in groups, such as administrators - Remove local machine permissions, where feasible - Tailor access, and use AD delegation for directory access - Use granular access permissions - Set account expiration and location restrictions on user-based service accounts |
| Monitor and audit use | - Monitor sign-in data, and ensure it matches the intended usage - Set alerts for anomalous usage |

### User account restrictions

For user accounts used as service accounts, apply the following settings:

- **Account expiration** - set the service account to automatically expire, after its review period, unless the account can continue
- **LogonWorkstations**- restrict service account sign-in permissions
    - If it runs locally and accesses resources on the machine, restrict it from signing in elsewhere
- **Can't change password** - set the parameter to **true** to prevent the service account from changing its own password

## Lifecycle management process

To help maintain service account security, manage them from inception to decommission. Use the following process:

1. Collect account usage information.
2. Move the service account and app to the configuration management database (CMDB).
3. Perform risk assessment or a formal review.
4. Create the service account and apply restrictions.
5. Schedule and perform recurring reviews.
6. Adjust permissions and scopes as needed.
7. Deprovision the account.

### Collect service account usage information

Collect relevant information for each service account. The following table lists the minimum information to collect. Obtain what's needed to validate each account.

| Data | Description |
| --- | --- |
| Owner | The user or group accountable for the service account |
| Purpose | The purpose of the service account |
| Permissions (scopes) | The expected permissions |
| CMDB links | The cross-link service account with the target script or application, and owners |
| Risk | The results of a security risk assessment |
| Lifetime | The anticipated maximum lifetime to schedule account expiration or recertification |

Make the account request self-service, and require the relevant information. The owner is an application or business owner, an IT team member, or an infrastructure owner. You can use Microsoft Forms for requests and associated information. If the account is approved, use Microsoft Forms to port it to a configuration management databases (CMDB) inventory tool.

### Service accounts and CMDB

Store the collected information in a CMDB application. Include dependencies on infrastructure, apps, and processes. Use this central repository to:

- Assess risk
- Configure the service account with restrictions
- Ascertain functional and security dependencies
- Conduct regular reviews for security and continued need
- Contact the owner to review, retire, and change the service account

#### Example HR scenario

An example is a service account that runs a website with permissions to connect to Human Resources SQL databases. The information in the service account CMDB, including examples, is in the following table:

| Data | Example |
| --- | --- |
| Owner, Deputy | Name, Name |
| Purpose | Run the HR webpage and connect to HR databases. Impersonate end users when accessing databases. |
| Permissions, scopes | HR-WEBServer: sign in locally; run web pageHR-SQL1: sign in locally; read permissions on HR databasesHR-SQL2: sign in locally; read permissions on Salary database only |
| Cost center | 123456 |
| Risk assessed | Medium; Business Impact: Medium; private information; Medium |
| Account restrictions | Sign in to: only aforementioned servers; Can't change password; MBI-Password Policy; |
| Lifetime | Unrestricted |
| Review cycle | Biannually: By owner, security team, or privacy team |

### Service account risk assessments or formal reviews

If your account is compromised by an unauthorized source, assess the risks to associated applications, services, and infrastructure. Consider direct and indirect risks:

- Resources an unauthorized user can gain access to
    - Other information or systems the service account can access
- Permissions the account can grant
    - Indications or signals when permissions change

After the risk assessment, documentation likely shows that risks affect account:

- Restrictions
- Lifetime
- Review requirements
    - Cadence and reviewers

### Create a service account and apply account restrictions

Note

Create a service account after the risk assessment, and document the findings in a CMDB. Align account restrictions with risk assessment findings.

Consider the following restrictions, although some might not be relevant to your assessment.

- For user accounts used as service accounts, define a realistic end date
    - Use the **Account Expires** flag to set the date
    - Learn more: [Set-ADAccountExpiration](/en-us/powershell/module/activedirectory/set-adaccountexpiration)
- See, [Set-ADUser (Active Directory)](/en-us/powershell/module/activedirectory/set-aduser)
- Password policy requirements
    - See, [Password and account lockout policies on Microsoft Entra Domain Services managed domains](/en-us/entra/identity/domain-services/password-policy)
- Create accounts in an organizational unit location that ensures only some users will manage it
    - See, [Delegating Administration of Account OUs and Resource OUs](/en-us/windows-server/identity/ad-ds/plan/delegating-administration-of-account-ous-and-resource-ous)
- Set up and collect auditing that detects service account changes:
    - See, [Audit Directory Service Changes](/en-us/windows/security/threat-protection/auditing/audit-directory-service-changes), and
    - Go to manageengine.com for [How to audit Kerberos authentication events in AD](https://www.manageengine.com/products/active-directory-audit/how-to/audit-kerberos-authentication-events.html)
- Grant account access more securely before it goes into production

### Service account reviews

Schedule regular service account reviews, especially those classified Medium and High Risk. Reviews can include:

- Owner attestation of the need for the account, with justification of permissions and scopes
- Privacy and security team reviews that include upstream and downstream dependencies
- Audit data review
- Ensure the account is used for its stated purpose

### Deprovision service accounts

Deprovision service accounts at the following junctures:

- Retirement of the script or application for which the service account was created
- Retirement of the script or application function, for which the service account was used
- Replacement of the service account for another

To deprovision:

1. Remove permissions and monitoring.
2. Examine sign-ins and resource access of related service accounts to ensure no potential effect on them.
3. Prevent account sign-in.
4. Ensure the account is no longer needed (there's no complaint).
5. Create a business policy that determines the amount of time that accounts are disabled.
6. Delete the service account.

- **MSAs** - see, [Uninstall-ADServiceAccount](/en-us/powershell/module/activedirectory/uninstall-adserviceaccount?view=winserver2012-ps&amp;preserve-view=true)
    - Use PowerShell, or delete it manually from the managed service account container
- **Computer or user accounts** - manually delete the account from Active Directory