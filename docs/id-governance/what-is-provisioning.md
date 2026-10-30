---
layout: Conceptual
title: What is provisioning with Microsoft Entra ID? - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/what-is-provisioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Describes overview of identity provisioning and the ILM scenarios.
ms.topic: overview
ms.date: 2024-12-30T00:00:00.0000000Z
locale: en-us
document_id: 08b460bb-0ca9-e410-9101-5f463e712859
document_version_independent_id: b04fa4ce-6090-8c20-7da8-8389da2bc410
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/what-is-provisioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/what-is-provisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/what-is-provisioning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 2b0b8c87-c29f-eb4f-843a-4cc787f84597
---

# What is provisioning with Microsoft Entra ID? - Microsoft Entra ID Governance | Microsoft Learn

Provisioning and deprovisioning are the processes that ensure consistency of digital identities across multiple systems. These processes are typically used as part of [identity lifecycle management](scenarios/govern-the-employee-lifecycle).

**Provisioning** is the processes of creating an identity in a target system based on certain conditions. **De-provisioning** is the process of removing the identity from the target system, when conditions are no longer met. **Synchronization** is the process of keeping the provisioned object, up to date, so that the source object and target object are similar.

For example, when a new employee joins your organization, that employee is entered in to the HR system. At that point, provisioning **from** HR **to** Microsoft Entra ID can create a corresponding user account in Microsoft Entra ID. Applications which query Microsoft Entra ID can see the account for that new employee. If there are applications that don't use Microsoft Entra ID, then provisioning **from** Microsoft Entra ID **to** those applications' databases, ensures that the user can access all of the applications that the user needs access to. This process allows the user to start work and have access to the applications and systems they need on day one. Similarly, when their properties, such as their department or employment status, change in the HR system, synchronization of those updates from the HR system to Microsoft Entra ID ensures consistency. Furthermore, this synchronization extends to other applications and target databases.

Microsoft Entra ID currently provides three areas of automated provisioning. They are:

- Provisioning from an external non-directory authoritative system of record to Microsoft Entra ID, via **HR-driven provisioning**
- Provisioning from Microsoft Entra ID to applications, via **App provisioning**
- Provisioning between Microsoft Entra ID and Active Directory Domain Services, via **inter-directory provisioning**

![Diagram of the identity lifecycle management.](media/what-is-provisioning/provisioning.png)

## HR-driven provisioning

![Diagram of the HR provisioning.](media/what-is-provisioning/cloud-2a.png)

Provisioning from HR to Microsoft Entra ID involves the creation of objects, typically user identities representing each employee, but in some cases other objects representing departments or other structures, based on the information that is in your HR system.

The most common scenario would be, when a new employee joins your company, they're entered into the HR system. Once that occurs, they're automatically provisioned as a new user in Microsoft Entra ID, without needing administrative involvement for each new hire. In general, provisioning from HR can cover the following scenarios.

- **Hiring new employees** - When a new employee is added to an HR system, a user account is automatically created in Active Directory, Microsoft Entra ID, and optionally in the directories for other applications supported by Microsoft Entra ID, with write-back of the email address to the HR system.
- **Employee attribute and profile updates** - When an employee record is updated in that HR system (such as their name, title, or manager), their user account is automatically updated in Active Directory, Microsoft Entra ID, and optionally other applications supported by Microsoft Entra ID.
- **Employee terminations** - When an employee is terminated in HR, their user account is automatically blocked from sign in or removed in Active Directory, Microsoft Entra ID, and in other applications.
- **Employee rehires** - When an employee is rehired in cloud HR, their old account can be automatically reactivated or reprovisioned (depending on your preference).

There are three deployment options for HR-driven provisioning with Microsoft Entra ID:

1. For organizations with a single subscription to Workday or SuccessFactors, and don't use Active Directory
2. For organizations with a single subscription to Workday or SuccessFactors, and have both Active Directory and Microsoft Entra ID
3. For organizations with multiple HR systems, or an on-premises HR system such as SAP HCM, Oracle E-Business Suite or PeopleSoft

For more information, see [What is HR driven provisioning?](../identity/app-provisioning/what-is-hr-driven-provisioning)

## App provisioning

![Diagram that shows the app provisioning flow.](media/what-is-provisioning/cloud-3b.png)

In Microsoft Entra ID, the term **[app provisioning](../identity/app-provisioning/user-provisioning)** refers to automatically creating copies of user identities in the applications that users need access to, for applications that have their own data store, distinct from Microsoft Entra ID or Active Directory. In addition to creating user identities, app provisioning includes the maintenance and removal of user identities from those apps, as the user's status or roles change. Common scenarios include provisioning a Microsoft Entra user into applications like [Dropbox](../identity/saas-apps/dropboxforbusiness-provisioning-tutorial), [Salesforce](../identity/saas-apps/salesforce-provisioning-tutorial), [ServiceNow](../identity/saas-apps/servicenow-provisioning-tutorial), as each of these applications have their own user repository distinct from Microsoft Entra ID.

Microsoft Entra ID also supports provisioning users into applications hosted on-premises or in a virtual machine, without having to open up any firewalls. If your application supports [SCIM](https://aka.ms/scimoverview), or you've built a SCIM gateway to connect to your legacy application, you can use the Microsoft Entra provisioning agent to [directly connect](../identity/app-provisioning/on-premises-scim-provisioning) with your application and automate provisioning and deprovisioning. If you have legacy applications that don't support SCIM and rely on an [LDAP](../identity/app-provisioning/on-premises-ldap-connector-configure) user store or a [SQL](../identity/app-provisioning/on-premises-sql-connector-configure) database, or that have a [SOAP or REST API](../identity/app-provisioning/on-premises-web-services-connector), Microsoft Entra ID can support those as well.

For more information, see [What is app provisioning?](../identity/app-provisioning/user-provisioning)

## Inter-directory provisioning

![Diagram that shows the inter-directory provisioning](media/what-is-provisioning/cloud-4a.png)

Many organizations rely upon both Active Directory and Microsoft Entra ID, and may have applications connected to Active Directory, such as on-premises file servers.

As many organizations historically have deployed HR-driven provisioning on-premises, they may already have user identities for all their employees in Active Directory. The most common scenario for inter-directory provisioning is when a user already in Active Directory is provisioned into Microsoft Entra ID. This provisioning is usually accomplished by Microsoft Entra Connect Sync or Microsoft Entra Connect cloud provisioning.

In addition, organizations may wish to also provision to on-premises systems from Microsoft Entra ID. For example, an organization may have guests in the Microsoft Entra directory, but those guests need access to on-premises Windows Integrated Authentication (WIA) based web applications via the app proxy. This scenario requires the provisioning of on-premises AD accounts for those users in Microsoft Entra ID.

For more information, see [What is inter-directory provisioning?](../identity/hybrid/what-is-inter-directory-provisioning)