---
layout: Conceptual
title: Road to the cloud - Implement a cloud-first approach when moving identity and access management from Active Directory Domain Services (AD DS) to Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/road-to-the-cloud-implement
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Implement a cloud-first approach as part of planning your migration of IAM from Active Directory Domain Services (AD DS) to Microsoft Entra ID.
documentationCenter: ''
ms.topic: how-to
ms.date: 2025-07-30T00:00:00.0000000Z
ms.custom: references_regions
ms.subservice: architecture
locale: en-us
document_id: 02f78178-4507-7852-34f2-5d8199156664
document_version_independent_id: 94761671-6d51-7682-d28c-bd77403c4d19
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/road-to-the-cloud-implement.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/road-to-the-cloud-implement
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/road-to-the-cloud-implement.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 18bd143f-a021-df5c-f301-a53f883b7751
---

# Road to the cloud - Implement a cloud-first approach when moving identity and access management from Active Directory Domain Services (AD DS) to Microsoft Entra ID - Microsoft Entra | Microsoft Learn

It's mainly a process and policy-driven phase to stop, or limit as much as possible, adding new dependencies to Active Directory Domain Services (AD DS) and implement a cloud-first approach for new demand of IT solutions.

It's key at this point to identify the internal processes that would lead to adding new dependencies on AD DS. For example, most organizations would have a change management process that has to be followed before the implementation of new scenarios, features, and solutions. We strongly recommend making sure that these change approval processes are updated to:

- Include a step to evaluate whether the proposed change would add new dependencies on AD DS.
- Evaluate Microsoft Entra alternatives when possible.

## Attributes

You can enrich user attributes in Microsoft Entra ID to make more user attributes available for inclusion. Examples of common scenarios that require rich user attributes include:

- App provisioning: The data source of app provisioning is Microsoft Entra ID, and necessary user attributes must be in there.
- Application authorization: A token that Microsoft Entra ID issues can include claims generated from user attributes so that applications can make authorization decisions based on the claims in the token. It can also contain attributes coming from external data sources through a [custom claims provider](../identity-platform/custom-claims-provider-overview).
- Group membership population and maintenance: Dynamic membership groups enable dynamic population of groups based on user attributes, such as department information.

These two links provide guidance on making schema changes:

- [Understand the Microsoft Entra schema and custom expressions](../identity/hybrid/cloud-sync/concept-attributes)
- [Attributes synchronized by Microsoft Entra Connect](../identity/hybrid/connect/reference-connect-sync-attributes-synchronized)

These links provide more information on this topic but aren't specific to changing the schema:

- [Use Microsoft Entra schema extension attributes in claims - Microsoft identity platform](../identity-platform/schema-extensions)
- [What are custom security attributes in Microsoft Entra ID (preview)?](../fundamentals/custom-security-attributes-overview)
- [Customize Microsoft Entra attribute mappings in application provisioning](../identity/app-provisioning/customize-application-attributes)
- [Provide optional claims to Microsoft Entra apps - Microsoft identity platform](../identity-platform/optional-claims)

- [Attribute-based application provisioning with scoping filters](/en-us/entra/identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts) or [What is Microsoft Entra entitlement management](/en-us/entra/id-governance/entitlement-management-overview) (for application access)

## Groups

A cloud-first approach for groups involves creating new groups in the cloud. If you need them on-premises, [provision groups to Active Directory Domain Services (AD DS) by using Microsoft Entra Cloud Sync](/en-us/entra/identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory). Convert the Group Source of Authority (SOA) of existing on-premises groups to manage them from Microsoft Entra.

These links provide more information about groups:

- [Create or edit a dynamic group and get status in Microsoft Entra ID](../identity/users/groups-create-rule)
- [Use self-service groups for user-initiated group management](../identity/users/groups-self-service-management)
- [Attribute-based application provisioning with scoping filters](../identity/app-provisioning/define-conditional-rules-for-provisioning-user-accounts) or [What is Microsoft Entra entitlement management?](../id-governance/entitlement-management-overview) (for application access)
- [Compare groups](/en-us/microsoft-365/admin/create-groups/compare-groups)
- [Restrict guest access permissions in Microsoft Entra ID](../identity/users/users-restrict-guest-permissions)

## Users

If there are users in your organization that do not have application dependencies to Active Directory, you can take a cloud-first approach by provisioning those users directly to Microsoft Entra ID. If there are users that do not require access to Active Directory, but have Active Directory accounts provisioned to them, their source of authority can be changed allowing you to clean their Active Directory account.

## Devices

Client workstations are traditionally joined to Active Directory and managed via Group Policy objects (GPOs) or device management solutions such as Microsoft Configuration Manager. Your teams will establish a new policy and process to prevent newly deployed workstations from being domain joined. Key points include:

- Mandate [Microsoft Entra join](../identity/devices/concept-directory-join) for new Windows client workstations to achieve "no more domain join."
- Manage workstations from the cloud by using unified endpoint management (UEM) solutions such as [Intune](/en-us/mem/intune/fundamentals/what-is-intune).

[Windows Autopilot](/en-us/autopilot/windows-autopilot) can help you establish a streamlined onboarding and device provisioning, which can enforce these directives.

[Windows Local Administrator Password Solution (LAPS)](../identity/devices/howto-manage-local-admin-passwords) enables a cloud-first solution to manage the passwords of local administrator accounts.

For more information, see [Learn more about cloud-native endpoints](/en-us/mem/solutions/cloud-native-endpoints/cloud-native-endpoints-overview).

## Applications

Traditionally, application servers are often joined to an on-premises Active Directory domain so that they can use Windows Integrated Authentication (Kerberos or NTLM), directory queries through LDAP, and server management through GPO or Microsoft Configuration Manager.

The organization has a process to evaluate Microsoft Entra alternatives when it's considering new services, apps, or infrastructure. Directives for a cloud-first approach to applications should be as follows. (New on-premises applications or legacy applications should be a rare exception when no modern alternative exists.)

- Provide a recommendation to change the procurement policy and application development policy to require modern protocols (OIDC/OAuth2 and SAML) and authenticate by using Microsoft Entra ID. New apps should also support [Microsoft Entra app provisioning](../identity/app-provisioning/what-is-hr-driven-provisioning) and have no dependency on LDAP queries. Exceptions require explicit review and approval.

    Important

    Depending on the anticipated demands of applications that require legacy protocols, you can choose to deploy [Microsoft Entra Domain Services](/en-us/entra/identity/domain-services/overview) when more current alternatives won't work.
- Provide a recommendation to create a policy to prioritize use of cloud-native alternatives. The policy should limit deployment of new application servers to the domain. Common cloud-native scenarios to replace domain member servers include:

    - File servers:

        - SharePoint or OneDrive provides collaboration support across Microsoft 365 solutions and built-in governance, risk, security, and compliance.
        - [Azure Files](/en-us/azure/storage/files/storage-files-introduction) offers fully managed file shares in the cloud that are accessible via the industry-standard SMB or NFS protocol. Customers can use native [Microsoft Entra authentication to Azure Files](/en-us/azure/virtual-desktop/create-profile-container-azure-ad) over the internet without line of sight to a domain controller.
        - Microsoft Entra ID works with third-party applications in the Microsoft [application gallery](/en-us/microsoft-365/enterprise/integrated-apps-and-azure-ads).
    - Print servers:

        - If your organization has a mandate to procure [Universal Print](/en-us/universal-print/)-compatible printers, see [Partner integrations](/en-us/universal-print/fundamentals/universal-print-partner-integrations).
        - Bridge with the [Universal Print connector](/en-us/universal-print/fundamentals/universal-print-connector-overview) for incompatible printers.