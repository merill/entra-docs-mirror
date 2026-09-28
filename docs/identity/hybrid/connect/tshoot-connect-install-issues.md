---
layout: Conceptual
title: Troubleshoot Microsoft Entra Connect install issues' - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tshoot-connect-install-issues
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This topic provides steps for how to troubleshoot issues with installing Microsoft Entra Connect.
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5fd98138-68c1-7fad-84bd-bd69e923c875
document_version_independent_id: a2f0519b-5f7c-3752-539e-ea8dfdc99e0e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tshoot-connect-install-issues.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tshoot-connect-install-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tshoot-connect-install-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 8fa39bda-4440-2390-fdfe-ee5994a2f2d2
---

# Troubleshoot Microsoft Entra Connect install issues' - Microsoft Entra ID | Microsoft Learn

## **Recommended Steps**

Check which [Microsoft Entra Connect installation type](how-to-connect-install-select-installation) is suitable for you. If you meet the criteria of express installation, then we highly recommend you to go with the express installation. The express installation gives you minimal options needed to finish the installation, and there's less likelihood of any issues.

However, if you don’t meet the express installation criteria and must do the custom installation then here are some best practices you can follow to avoid common issues. For the sake of simplicity only selective options are mentioned here:

- Ensure you're an administrator on the machine on which you're installing Microsoft Entra Connect. Sign-in to the machine with same administrator credentials.
- Let all the options to be default on the following page, except for “Use an existing SQL Server”, if you want to use existing SQL Server. Here are [more details](how-to-connect-install-custom) about how to use custom installation options.

    ![Use Existing SQL Server](media/tshoot-connect-install-issues/tshoot-connect-install-issues/useexistingsqlserver.png)
- On the following page, pick option “Create new AD account", to avoid any permission issues with existing account.

    ![AD Forest Account](media/tshoot-connect-install-issues/tshoot-connect-install-issues/createnewaccount.png)

### **Common Issues**

- [Connectivity issues with on-premises Active Directory](reference-connect-adconnectivitytools).
- [Connectivity issues with online Microsoft Entra ID](tshoot-connect-connectivity).
- [Permission issues with on-premises Active Directory](how-to-connect-configure-ad-ds-connector-account).

## **Recommended Documents**

- [Prerequisites for Microsoft Entra Connect](how-to-connect-install-prerequisites)
- [Select which installation type to use for Microsoft Entra Connect](how-to-connect-install-select-installation)
- [Getting started with Microsoft Entra Connect using express settings](how-to-connect-install-express)
- [Custom installation of Microsoft Entra Connect](how-to-connect-install-custom)
- [Microsoft Entra Connect: Upgrade from a previous version to the latest](how-to-upgrade-previous-version)
- [Microsoft Entra Connect: What is staging server?](plan-connect-topologies#staging-server)
- [What is the `ADConnectivityTool` PowerShell module?](how-to-connect-adconnectivitytools)