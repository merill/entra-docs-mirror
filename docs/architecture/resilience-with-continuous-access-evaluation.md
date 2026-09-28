---
layout: Conceptual
title: Build resilience by using Continuous Access Evaluation in Microsoft Entra ID - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/resilience-with-continuous-access-evaluation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: A guide for architects and IT administrators on using CAE
ms.topic: concept-article
ms.date: 2022-11-16T00:00:00.0000000Z
ms.subservice: architecture
locale: en-us
document_id: 275fd118-c488-d42a-daae-8434f5efc61e
document_version_independent_id: 2f4f29c1-0488-f161-549d-02f175ef9c9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/resilience-with-continuous-access-evaluation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/resilience-with-continuous-access-evaluation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/resilience-with-continuous-access-evaluation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 468ab0b8-e50c-dd9a-c56e-0f13bc6b2f48
---

# Build resilience by using Continuous Access Evaluation in Microsoft Entra ID - Microsoft Entra | Microsoft Learn

[Continuous Access Evaluation (CAE)](../identity/conditional-access/concept-continuous-access-evaluation) allows Microsoft Entra applications to subscribe to critical events that can then be evaluated and enforced. CAE includes evaluation of the following events:

- User account deleted or disabled
- Password for user changed
- MFA enabled for user
- Administrator explicitly revokes a token
- Elevated user risk detected

As a result, applications can reject unexpired tokens based on the events signaled by Microsoft Entra ID as depicted in the following diagram.

![conceptualiagram of CAE](media/resilience-with-cae/admin-resilience-continuous-access-evaluation.png)

## How does CAE help?

The CAE mechanism allows Microsoft Entra ID to issue longer-lived tokens while enabling applications to revoke access and force reauthentication only when needed. The net result of this pattern is fewer calls to acquire tokens, which means that the end-to-end flow is more resilient.

To use CAE, both the service and the client must be CAE-capable. Microsoft 365 services such as Exchange Online, Teams, and SharePoint Online support CAE. On the client side, browser-based experiences that use these Office 365 services (such as Outlook Web App) and specific versions of Office 365 native clients are CAE-capable. More Microsoft cloud services will become CAE-capable.

Microsoft is working with the industry to build [standards](https://openid.net/wg/sse/) that will allow third party applications to use CAE capability. You can also develop applications that are CAE-capable. For more information about CAE-capable application development, see [How to build resilience in your application](resilience-app-development-overview).

## How do I implement CAE?

- [Update your code to use CAE-enabled APIs](../identity-platform/app-resilience-continuous-access-evaluation).
- [Enable CAE](../identity/conditional-access/concept-continuous-access-evaluation) in the Microsoft Entra Security Configuration.
- Ensure that your organization is using [compatible versions](../identity/conditional-access/concept-continuous-access-evaluation) of Microsoft Office native applications.
- [Optimize your reauthentication prompts](../identity/authentication/concepts-azure-multi-factor-authentication-prompts-session-lifetime).