---
layout: Conceptual
title: 'Microsoft Entra Connect: What is the ADConnectivityTool PowerShell Module - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-adconnectivitytools
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This document introduces the new ADConnectivity PowerShell module and how it can be used to help troubleshoot.
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
locale: en-us
document_id: 9c790975-a14e-c0da-ef47-8d111f693049
document_version_independent_id: b0efbcd4-59a0-d2fd-f26d-e230a1aa0ca5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-adconnectivitytools.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-adconnectivitytools
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-adconnectivitytools.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 0db46fd7-878a-7645-b1cc-943d06dcce6a
---

# Microsoft Entra Connect: What is the ADConnectivityTool PowerShell Module - Microsoft Entra ID | Microsoft Learn

The ADConnectivity tool is a PowerShell module that is used in one of the following:

- During installation, when a network connectivity problem prevents the successful validation of the Active Directory credentials.
- Post installation by a user who calls the functions from a PowerShell session.

The tool is located in: **C:\Program Files\Microsoft Entra Connect\Tools\ADConnectivityTool.psm1**.

## ADConnectivityTool during installation

On the **Connect your directories** page, in the Microsoft Entra Connect Wizard, if a network issue occurs, the ADConnectivityTool will automatically use one of its functions to determine what is going on. The following items can be considered network issues:

- The name of the Forest the user provided was typed wrongly, or said Forest doesn’t exist
- UDP port 389 is closed in the Domain Controllers associated with the Forest the user provided
- The credentials provided in the ‘AD forest account’ window doesn’t have privileges to retrieve the Domain Controllers associated with the target Forest
- Any of the TCP ports 53, 88 or 389 are closed in the Domain Controllers associated with the Forest the user provided
- Both UDP 389 and a TCP port (or ports) are closed
- DNS couldn't be resolved for the provided Forest and\or its associated Domain Controllers

Whenever any of these issues are found, a related error message is displayed in the Microsoft Entra Connect Wizard:

![Error](media/how-to-connect-adconnectivitytools/error1.png)

For example, when we're attempting to add a directory on the **Connect your directories** screen, Microsoft Entra Connect needs to verify this and expects to be able to communicate with a domain controller over port 389. If it can't, we'll see the error that is shown in the screenshot.

What is actually happening behind the scenes, is that Microsoft Entra Connect is calling the `Start-NetworkConnectivityDiagnosisTools` function. This function is called when the validation of credentials fails due to a network connectivity issue.

Finally, a detailed log file is generated whenever the tool is called from the wizard. The log is located in **C:\ProgramData\AADConnect\ADConnectivityTool-&lt;date&gt;-&lt;time&gt;.log**

## ADConnectivityTools post installation

After Microsoft Entra Connect is installed, any of the functions in the ADConnectivityTools PowerShell module can be used.

You can find reference information on the functions in the [ADConnectivityTools Reference](reference-connect-adconnectivitytools)

### Start-ConnectivityValidation

We're going to call out this function because it can **only** be called manually once the ADConnectivityTool.psm1 is imported into PowerShell.

This function executes the same logic that the Microsoft Entra Connect Wizard runs to validate the provided AD Credentials. However, it provides a much more verbose explanation about the problem and a suggested solution.

The connectivity validation consists of the following steps:

- Get Domain FQDN (fully qualified domain name) object
- Validate that, if the user selected ‘Create new AD account’, these credentials belong to the Enterprise Administrators group
- Get Forest FQDN object
- Confirm that at least one domain associated with the previously obtained Forest FQDN object is reachable
- Verify that the functional level of the forest is Windows Server 2003 or greater.

The user is able to add a Directory if all these actions were executed successfully.

If the user runs this function, after a problem is solved (or if no problem exists at all), the output will indicate for the user to go back to the Microsoft Entra Connect Wizard and try inserting the credentials again.