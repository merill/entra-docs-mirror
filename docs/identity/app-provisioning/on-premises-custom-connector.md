---
layout: Conceptual
title: Microsoft Entra provisioning to applications using custom connectors - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/on-premises-custom-connector
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: This document describes how to configure Microsoft Entra ID to provision users with external systems that offer REST and SOAP APIs.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.reviewer: arvinh
locale: en-us
document_id: 25a8251c-104f-3bda-3fc4-d370822e8b9d
document_version_independent_id: 7fb1d006-a11e-28de-d3fe-0dcc1e621255
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/on-premises-custom-connector.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/on-premises-custom-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/on-premises-custom-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fecfc034-c4c2-43e6-be47-948bd4addcea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/16cf36da-59bd-4744-91e9-295292c63e5e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 1378a7bc-906a-d052-b1b3-62c25522542a
---

# Microsoft Entra provisioning to applications using custom connectors - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID includes connectivity to provision into applications that support the following protocols and interfaces:

- [SCIM 2.0](on-premises-scim-provisioning)
- [SQL](tutorial-ecma-sql-connector)
- [LDAP](on-premises-ldap-connector-configure)
- [REST](on-premises-web-services-connector)
- [SOAP](on-premises-web-services-connector)
- [PowerShell](on-premises-powershell-connector)

For connectivity to applications that don't support one of the aforementioned protocols and interfaces, customers and [partners](/en-us/archive/technet-wiki/1589.fim-2010-mim-2016-management-agents-from-partners) have built custom [ECMA 2.0](/en-us/previous-versions/windows/desktop/forefront-2010/hh859557%28v=vs.100%29) connectors for use with Microsoft Identity Manager (MIM) 2016. ECMA2 connectors can be used to provision into apps with the Microsoft Entra provisioning agent and Extensible Connectivity(ECMA) Connector host, without needing MIM sync deployed.

## Exporting and importing a MIM connector

If you have a custom ECMA 2.0 connector in MIM, you can export its configuration by following the instructions [here](on-premises-migrate-microsoft-identity-manager#export-a-connector-configuration-from-mim-sync). You need to save the XML file, the DLL, and related software for your connector.

To import your connector, you can use the instructions [here](on-premises-migrate-microsoft-identity-manager#import-a-connector-configuration). You need to copy the DLL for your connector, and any of its prerequisite DLLs, to that same ECMA subdirectory of the Service directory. After the xml import, continue through the wizard and ensure that all the required fields are populated.

## Updating a custom connector DLL

When updating a connector with a newer build, ensure that the DLL is updated in all the required locations. Use these steps to properly update your custom connector DLL:

1. Close the Microsoft ECMA2Host Configuration Wizard.
2. Stop the Microsoft ECMA2Host service.
3. Manually update the custom connector DLL into each of the following folders.
    1. ECMA
    2. ECMA &gt; Cache &gt; {connector name}
    3. ECMA &gt; Cache &gt; {connector name} &gt; AutosyncService
4. Start the Microsoft ECMA2Host service.

Note

If multiple connectors are using the same custom DLL, complete step 3.ii and 3.iii for each connector.

## Troubleshooting

Custom connectors built for MIM rely on the [ECMA framework](/en-us/previous-versions/windows/desktop/forefront-2010/hh859557%28v=vs.100%29). If you're having difficulties importing and using a connector, please ensure that you're following best practices:

- Ensuring that methods in your connector are declared as public
- Excluding prefixes from method names. For example:
    - **Correct:** public Schema GetSchema (KeyedCollection&lt;string, ConfigParameter&gt; configParameters)
    - **Incorrect:** Schema PrefixGetSchema.GetSchema (KeyedCollection&lt;string, ConfigParameter&gt; configParameters)

The following table includes capabilities of the ECMA framework that differ between MIM and the Microsoft Entra provisioning agent. For a list of known limitations for the Microsoft Entra provisioning service and on-premises application provisioning, see [here](known-issues#on-premises-application-provisioning).

| **Capability** | **Comments** |
| --- | --- |
| Object type | Provisioning agent permits one object type |
| Partitions | Provisioning agent permits one partition |
| Hierarchies | Not used by provisioning agent |
| Full export | Not used by provisioning agent |
| ExportPasswordInFirstPass | Not supported |
| Normalizations | Not used by provisioning agent |
| Concurrent operations | Not used by provisioning agent |
| DeleteAddAsReplace | Not used by provisioning agent |