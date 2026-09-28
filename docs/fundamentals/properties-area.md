---
layout: Conceptual
title: Add your organization's privacy information - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/properties-area
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Add your organization's privacy information, privacy contact, and technical contact to your directory.
ms.topic: how-to
ms.date: 2025-04-30T00:00:00.0000000Z
ms.custom: template-how-to, ge-structured-content-pilot, sfi-ga-nochange
locale: en-us
document_id: 7b3e93f8-497b-2547-d9d5-751a70447fbe
document_version_independent_id: ccb8f6fe-2335-3819-9e0d-080a7ebbf7bb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/properties-area.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/properties-area
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/properties-area.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 24fbf150-0caa-0c25-6615-61768446968b
---

# Add your organization's privacy information - Microsoft Entra | Microsoft Learn

## Overview

This article explains how an administrator can add privacy-related info to an organization's directory through the Microsoft Entra admin center.

Add both your global privacy contact and your organization's privacy statement, so your internal employees and external guests can review your policies. Because each business creates and tailors its own privacy statements, contact a lawyer for assistance.

Note

For information about viewing or deleting personal data, please review Microsoft's guidance on the [Windows data subject requests for the GDPR](/en-us/microsoft-365/compliance/gdpr-dsr-windows) site. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Add your privacy information

You can find your privacy and technical information in the **Properties** area of the Microsoft Entra admin center.

### To access the properties area and add your privacy information

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Billing Administrator](../identity/role-based-access-control/permissions-reference#billing-administrator).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Properties**.

    [![Screenshot showing the properties area highlighting the privacy info area.](media/properties-area/properties-area.png)](media/properties-area/properties-area.png#lightbox)
3. Add your privacy info for your users:

- **Technical contact.** Type the email address for the person to contact for technical support within your organization.
- **Global privacy contact.** Type the email address for the person to contact for inquiries about personal data privacy. This person is also who Microsoft contacts if there's a data breach related to Microsoft Entra services. If there's no person listed here, Microsoft contacts your Global Administrators. For Microsoft 365 related privacy incident notifications, see [Microsoft 365 Message center FAQs](/en-us/microsoft-365/admin/manage/message-center?preserve-view=true&amp;view=o365-worldwide#frequently-asked-questions).
- **Privacy statement URL.** Type the link to your organization's document that describes how your organization handles both internal and external guests' data privacy.

    Important

    If you don't include either your own privacy statement or your privacy contact, your external guests will see text in the **Review Permissions** box that says, **&lt;*your org name*&gt; has not provided links to their terms for you to review**. For example, a guest user will see this message when they receive an invitation to access an organization through B2B collaboration.

    ![Screenshot showing the B2B Collaboration Review Permissions box with message.](media/properties-area/no-privacy-statement-or-contact.png)

1. Select **Accept**.