---
layout: Conceptual
title: Solutions to automate identity provisioning to applications - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/automate-provisioning-to-applications-solutions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Learn to design solutions to automatically provision identities based on various scenarios.
ms.topic: overview
ms.date: 2022-09-29T00:00:00.0000000Z
ms.custom: it-pro, kr2b-contr-experiment, sfi-image-nochange
ms.subservice: architecture
locale: en-us
document_id: 53a27a13-93e8-55cf-f382-cafd97b60700
document_version_independent_id: 26c98c27-8363-c663-a271-09c3ac138d33
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/automate-provisioning-to-applications-solutions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/automate-provisioning-to-applications-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/automate-provisioning-to-applications-solutions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f460646f-b133-36d6-2bb4-a58061d6faf5
---

# Solutions to automate identity provisioning to applications - Microsoft Entra | Microsoft Learn

This article presents solutions that enable you to:

- Connect identities with your system of record
- Synchronize identities between Active Directory Domain Services (AD DS) and Microsoft Entra ID
- Automate provisioning of users into non-Microsoft applications

## Connect identities with your system of record

In most designs, the human resources (HR) system is the source-of-authority for newly created digital identities. The HR system is often the starting point for many provisioning processes. For example, if a new user joins a company, they have a record in the HR system. That user likely needs an account to access Microsoft 365 services such as Teams and SharePoint, or non-Microsoft applications.

### Synchronizing identities with cloud HR

The Microsoft Entra provisioning service enables organizations to [bring identities from popular HR systems](../identity/app-provisioning/what-is-hr-driven-provisioning) (examples: [Workday](../identity/saas-apps/workday-inbound-tutorial) and [SuccessFactors](../identity/saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial)), into Microsoft Entra ID directly, or into AD DS. This provisioning capability enables new hires to access the resources they need from the first day of work.

### On-premises HR + joining multiple data sources

To create a full user profile for an employee identity, organizations often merge information from multiple HR systems, databases, and other user data stores. MIM provides a rich set of [connectors](/en-us/microsoft-identity-manager/supported-management-agents) and integration solutions interoperating with heterogeneous platforms both on-premises and in the cloud.

MIM offers [rule extension](/en-us/previous-versions/windows/desktop/forefront-2010/ms698810%28v=vs.100%29?redirectedfrom=MSDN) and [workflow capabilities](https://microsoft.github.io/MIMWAL/) features for advanced scenarios requiring data transformation and consolidation from multiple sources. These connectors, rule extensions, and workflow capabilities enable organizations to aggregate user data in the MIM Metaverse to form a single identity for each user. The identity can be [provisioned into downstream systems](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-supported-platforms) such as AD DS.

![Systems of record model](media/automate-user-provisioning-to-applications-solutions/system-of-record.png)

## Synchronize identities between Active Directory Domain Services (AD DS) and Microsoft Entra ID

As customers move applications to the cloud, and integrate with Microsoft Entra ID, users often need accounts in Microsoft Entra ID, and Microsoft Windows Server Active Directory to access the applications for their work. Here are five common scenarios in which objects need to be synchronized between Microsoft Windows Server Active Directory and Microsoft Entra ID.

The scenarios are divided by the direction of synchronization needed, and are listed, one through five. Use the table following the scenarios to determine what technical solution provides the synchronization.

Use the numbered sections in the next two section to cross reference the following table.

**Synchronize identities from AD DS into Microsoft Entra ID**

1. For users in Microsoft Windows Server Active Directory that need access to Office 365 or other applications that are connected to Microsoft Entra ID, Microsoft Entra Connect cloud sync is the first solution to explore. It provides a lightweight solution to create users in Microsoft Entra ID, manage password rests, and synchronize groups. Configuration and management are primarily done in the cloud, minimizing your on-premises footprint. It provides high availability and automatic failover, ensuring password resets and synchronization continue, even if there's an issue with on-premises servers.
2. For complex, large-scale Microsoft Windows Server Active Directory to Azure AD Sync requirements such as synchronizing large groups (over 50,000 members), and device sync, use Microsoft Entra Connect Sync.

**Synchronize identities from Microsoft Entra ID into AD DS**

As customers transition identity management to the cloud, more users and groups are created directly in Microsoft Entra ID. However, they still need a presence on-premises in AD DS to access various resources.

1. When an external user from a partner organization is created in Microsoft Entra ID using B2B, MIM can automatically provision them [into AD DS](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-graph-b2b-scenario) and give those guests access to [on-premises Windows-Integrated Authentication or Kerberos-based applications](../external-id/hybrid-cloud-to-on-premises). Alternatively, customers can user [PowerShell scripts](https://github.com/Azure-Samples/B2B-to-AD-Sync) to automate the creation of guest accounts on-premises.
2. When a group is created in Microsoft Entra ID, it can be automatically synchronized to AD DS using [Microsoft Entra Connect Sync](../identity/hybrid/connect/how-to-connect-group-writeback-v2).
3. When users need access to cloud apps that still rely on legacy access protocols (for example, LDAP and Kerberos/NTLM), [Microsoft Entra Domain Services](https://azure.microsoft.com/services/active-directory-ds/) synchronizes identities between Microsoft Entra ID and a managed Microsoft Windows Server Active Directory domain.

| No. | What | From | To | Technology |
| --- | --- | --- | --- | --- |
| 1 | Users, groups | AD DS | Microsoft Entra ID | [Microsoft Entra Connect cloud sync](../identity/hybrid/cloud-sync/what-is-cloud-sync) |
| 2 | Users, groups, devices | AD DS | Microsoft Entra ID | [Microsoft Entra Connect Sync](../identity/hybrid/connect/whatis-azure-ad-connect) |
| 3 | Groups | Microsoft Entra ID | AD DS | [Microsoft Entra Connect Sync](../identity/hybrid/connect/how-to-connect-group-writeback-v2) |
| 4 | Guest accounts | Microsoft Entra ID | AD DS | [MIM](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016-graph-b2b-scenario), [PowerShell](https://github.com/Azure-Samples/B2B-to-AD-Sync) |
| 5 | Users, groups | Microsoft Entra ID | Managed Microsoft Windows Server Active Directory | [Microsoft Entra Domain Services](https://azure.microsoft.com/services/active-directory-ds/) |

The table depicts common scenarios and the recommended technology.

## Automate provisioning users into non-Microsoft applications

After identities are in Microsoft Entra ID through HR-provisioning or Microsoft Entra Connect cloud sync / Microsoft Entra Connect Sync, the employee can use the identity to access Teams, SharePoint, and Microsoft 365 applications. However, employees still need access to many Microsoft applications to perform their work.

![Automation decision matrix](media/automate-user-provisioning-to-applications-solutions/automate-provisioning-decision-matrix.png)

### Automate provisioning to apps and clouds that support the SCIM standard

Microsoft Entra ID supports the System for Cross-Domain Identity Management (SCIM) ([SCIM 2.0](https://aka.ms/scimoverview)) standard and integrates with hundreds of popular software as a service (SaaS) applications such as [Dropbox](../identity/saas-apps/dropboxforbusiness-provisioning-tutorial) and [Atlassian](../identity/saas-apps/atlassian-cloud-provisioning-tutorial) or other clouds such as [Amazon Web Services (AWS)](../identity/saas-apps/aws-single-sign-on-provisioning-tutorial), [Google Cloud](../identity/saas-apps/g-suite-provisioning-tutorial). Application developers can use the System for Cross-Domain Identity Management (SCIM) user management API to automate provisioning users and groups between Microsoft Entra ID and your application.

![SCIM standard](media/automate-user-provisioning-to-applications-solutions/automate-provisioning-scim-standard.png)

In addition to the pre-integrated gallery applications, Microsoft Entra ID supports provisioning to SCIM enabled line of business applications, whether hosted [on-premises](../identity/app-provisioning/on-premises-scim-provisioning) or in the cloud. The Microsoft Entra provisioning service creates users and groups in these applications, and manages updates such as when a user is promoted or leaves the company).

Learn more about [provisioning to SCIM enabled applications](../identity/app-provisioning/use-scim-to-provision-users-and-groups)

### Automate provisioning to on-premises applications

Many applications don't support the SCIM standard, and customers have historically used connectors developed for MIM to connect to them. The Microsoft Entra provisioning service supports reusing connectors built for MIM, without needing a MIM sync deployment. This opens up connectivity to a wide range of on-premises and SaaS applications.

| Protocol | Connector |
| --- | --- |
| LDAP | [LDAP](../identity/app-provisioning/on-premises-ldap-connector-configure) |
| SQL | [SQL](../identity/app-provisioning/tutorial-ecma-sql-connector) |
| REST | [Web Services](../identity/app-provisioning/on-premises-web-services-connector) |
| Simple Object Access Protocol (SOAP) | [Web Services](../identity/app-provisioning/on-premises-web-services-connector) |
| Flat-file | [PowerShell](../identity/app-provisioning/on-premises-powershell-connector) |
| Custom | [Custom ECMA connectors](../identity/app-provisioning/on-premises-custom-connector) |

Learn more about [on-premises application provisioning](../identity/app-provisioning/user-provisioning)

### Use integrations developed by partners

Microsoft partners have developed SCIM gateways that allow you to synchronize users between Microsoft Entra ID and various systems such as mainframes, HR systems, and legacy databases. In the following image, the SCIM Gateways are built and managed by partners.

![Agent with SCIM gateway](media/automate-user-provisioning-to-applications-solutions/provisioning-agent-with-scim-gateway.png)

Learn more about [partner driven integrations](../identity/app-provisioning/partner-driven-integrations)

### Manage local app passwords

Many applications have a local authentication store and a UI that only checks the user's supplied credentials against that store. As a result, these applications can't support Multi Factor Authentication (MFA) through Microsoft Entra ID and pose a security risk. Microsoft recommends enabling single sign-on and multifactor authentication for all your applications. Based on our studies, your account is more than 99.9% less likely to be compromised if you [use multifactor authentication](https://aka.ms/securitysteps). However, in cases where the application can't externalize authentication, customers can use MIM to sync password changes to these applications.

![Provision access from org data](media/automate-user-provisioning-to-applications-solutions/provision-access-based-on-org-data.png)

Learn more about the [MIM password change notification service](/en-us/microsoft-identity-manager/infrastructure/mim2016-password-management)

### Define and provision access for a user based on organizational data

MIM enables you to import organizational data such as job codes and locations. That information can then be used to automatically set up access rights for that user.

![Manage local app passwords](media/automate-user-provisioning-to-applications-solutions/manage-local-app-passwords.png)

### Automate common business workflows

After users are provisioned into Microsoft Entra ID, use Lifecycle Workflows (LCW) to automate appropriate actions at key moments in a user's lifecycle such as joiner, mover, and leaver. These custom workflows can be triggered by Microsoft Entra LCW automatically, or on demand to enable or disable accounts, generate Temporary Access Passes, update Teams or group membership, send automated emails, and trigger a logic app. This can help organizations ensure:

- **Joiner:** When a user joins the organization, they're ready to go on day one. They have the correct access to the information and applications they need. They have the required hardware necessary to do their job.
- **Leaver:** When users leave the company for various reasons (termination, separation, leave of absence or retirement), have their access revoked in a timely manner.

Learn more about [Microsoft Entra Lifecycle Workflows](../id-governance/what-are-lifecycle-workflows)

Note

For scenarios not covered by LCW, customers can use the extensibility of [Logic Applications](/en-us/azure/logic-apps/logic-apps-overview).

### Reconcile changes made directly in the target system

Organizations often need a complete audit trail of what users have access to applications containing data subject to regulation. To provide an audit trail, any access provided to a user directly must be traceable through the system of record. MIM provides the reconciliation capabilities to detect changes made directly in a target system and roll back the changes. In addition to detecting changes in target applications, MIM can import identities from third-party applications to Microsoft Entra ID. These applications often augment the set of user records that originated in the HR system.

### Next steps

1. Automate provisioning with any of your applications that are in the [Microsoft Entra app gallery](../identity/saas-apps/tutorial-list), support [SCIM](../identity/app-provisioning/use-scim-to-provision-users-and-groups), [SQL](../identity/app-provisioning/on-premises-sql-connector-configure), or [LDAP](../identity/app-provisioning/on-premises-ldap-connector-configure).
2. Evaluate [Microsoft Entra Connect cloud sync](../identity/hybrid/cloud-sync/what-is-cloud-sync) for synchronization between AD DS and Microsoft Entra ID
3. Use the [Microsoft Identity Manager](/en-us/microsoft-identity-manager/microsoft-identity-manager-2016) for complex provisioning scenarios