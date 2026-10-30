---
layout: Conceptual
title: What is identity provisioning with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/what-is-provisioning
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: Describes overview of identity provisioning.
ms.topic: overview
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid
locale: en-us
document_id: 8be579ee-c8ae-f9da-17e3-916ea6281317
document_version_independent_id: b093984d-6d12-9517-916e-b6fb7934a48a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/what-is-provisioning.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/what-is-provisioning
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/what-is-provisioning.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 11eb5cf5-b171-5c0f-80ef-c645a0e01a60
---

# What is identity provisioning with Microsoft Entra ID? - Microsoft Entra ID | Microsoft Learn

Today, businesses, and corporations are becoming more of a mixture of on-premises and cloud applications. Users require access to applications both on-premises and in the cloud. There's need to have a single identity across these various applications (on-premises and cloud).

Provisioning is the process of creating an object based on certain conditions, keeping the object up to date, and deleting the object when conditions are no longer met. For example, when a new user joins your organization, that user is entered in to the HR system. At that point, provisioning can create a corresponding user account in the cloud, in Active Directory, and different applications that the user needs access to. This allows the user to start work and have access to the applications and systems they need on day one.

![Diagram that shows cloud provisioning with Microsoft Entra ID.](media/what-is-provisioning/cloud-1.png)

With regard to Microsoft Entra ID, provisioning can be broken down in to the following key scenarios.

- **HR-driven provisioning**
- **App provisioning**
- **Directory provisioning**

## HR-driven provisioning

![Diagram that shows HR-driven provisioning with Cloud HR, On-premises HR, and Microsoft Entra ID.](media/what-is-provisioning/cloud-2.png)

Provisioning from HR to the cloud involves the creation of objects (users, roles, groups, and so on) based on the information that is in your HR system.

The most common scenario would be, when a new employee joins your company, they're entered into the HR system. Once that occurs, they're provisioned to the cloud. In this case, Microsoft Entra ID. Provisioning from HR can cover the following scenarios.

- **Hiring new employees** - When a new employee is added to cloud HR, a user account is automatically created in Active Directory, Microsoft Entra ID, and optionally Microsoft 365 and other SaaS applications supported by Microsoft Entra ID, with write-back of the email address to Cloud HR.
- **Employee attribute and profile updates** - When an employee record is updated in cloud HR (such as their name, title, or manager), their user account automatically updates in Active Directory, Microsoft Entra ID, and optionally Microsoft 365 and other SaaS applications supported by Microsoft Entra ID.
- **Employee terminations** - When an employee is terminated in cloud HR, their user account is automatically disabled in Active Directory, Microsoft Entra ID, and optionally Office 365 and other SaaS applications supported by Microsoft Entra ID.
- **Employee rehires** - When an employee is rehired in cloud HR, their old account can be automatically reactivated or re-provisioned (depending on your preference) to Active Directory, Microsoft Entra ID, and optionally Microsoft 365 and other SaaS applications supported by Microsoft Entra ID.

## App provisioning

![Diagram that shows App provisioning with On-premises apps, Non-Microsoft cloud apps, and Microsoft Entra ID.](media/what-is-provisioning/cloud-3.png)

In Microsoft Entra ID, the term **[app provisioning](../app-provisioning/user-provisioning)** refers to automatically creating user identities and roles in the cloud applications that users need access to. In addition to creating user identities, automatic provisioning includes the maintenance and removal of user identities as status or roles change. Common scenarios include provisioning a Microsoft Entra user into applications like [Dropbox](../saas-apps/dropboxforbusiness-provisioning-tutorial), [Salesforce](../saas-apps/salesforce-provisioning-tutorial), [ServiceNow](../saas-apps/servicenow-provisioning-tutorial), and more.

## Directory provisioning

![cloud provisioning](media/what-is-provisioning/cloud-4.png)

On-premises provisioning involves provisioning from on-premises sources (like Active Directory) to Microsoft Entra ID.

The most common scenario would be, when a user in Active Directory (AD) is provisioned into Microsoft Entra ID.

This has been accomplished by Microsoft Entra Connect Sync, Microsoft Entra Connect cloud provisioning and Microsoft Identity Manager.