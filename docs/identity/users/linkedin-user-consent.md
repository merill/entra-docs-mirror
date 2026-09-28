---
layout: Conceptual
title: LinkedIn data sharing and consent - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/linkedin-user-consent
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Explains how LinkedIn integration shares data via Microsoft apps in Microsoft Entra ID
ms.topic: how-to
ms.date: 2024-12-19T00:00:00.0000000Z
ms.reviewer: beengen
ms.custom: it-pro
locale: en-us
document_id: bf26cd9c-86e3-b7cf-0b54-abc397a1971b
document_version_independent_id: 82750e67-f9b0-77f3-c353-fbb323e09558
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/linkedin-user-consent.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/linkedin-user-consent
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/linkedin-user-consent.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aec7dc3e-0dad-4b82-accf-63218d8767d5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f260444a-7ec6-4768-8e41-ad2438092724
platformId: 600a652c-6e24-c8b3-52cc-daf3ecc1947e
---

# LinkedIn data sharing and consent - Microsoft Entra ID | Microsoft Learn

## Overview

You can enable users in your organization in Microsoft Entra ID, part of Microsoft Entra, to consent to connect their Microsoft work or school account with their LinkedIn account. After a user connects their accounts, information and highlights from LinkedIn are available in some Microsoft apps and services. Users can also expect their networking experience on LinkedIn to be improved and enriched with information from Microsoft.

To see LinkedIn information in Microsoft apps and services, users must consent to connect their own Microsoft and LinkedIn accounts. Users are prompted to connect their accounts the first time they select to see someone's LinkedIn information on a profile card in Outlook, OneDrive, or SharePoint Online. LinkedIn account connections aren't fully enabled for your users until they consent to the experience and to connect their accounts.

Note

For information about viewing or deleting personal data, please review Microsoft's guidance on the [Windows data subject requests for the GDPR](/en-us/microsoft-365/compliance/gdpr-dsr-windows) site. For general information about GDPR, see the [GDPR section of the Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy/gdpr-overview) and the [GDPR section of the Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## Benefits of sharing LinkedIn information

Access to LinkedIn information within Microsoft apps and services makes it easier for your users to connect, engage, and build professional relationships with colleagues, customers, and partners inside and outside your organization. New users can get up to speed faster by connecting with colleagues, learning more about them, and easily accessing more information.

The image shows an example of how LinkedIn information appears on the profile card in Microsoft apps:

![Screenshot of enabling LinkedIn integration in your organization.](media/linkedin-user-consent/display-example.png)

## Enable and announce LinkedIn integration

You must be a Microsoft Entra Admin to manage the setting for your organization. You can enable it for all users, or for a specific set of users.

1. To enable or disable the integration, follow the steps in [Consent to LinkedIn integration for your Microsoft Entra organization](linkedin-integration).
2. When you announce the LinkedIn integration in your organization, point your users to the FAQ about [LinkedIn information in Microsoft apps and services](https://support.office.com/article/about-linkedin-information-and-features-in-microsoft-apps-and-services-dc81cc70-4d64-4755-9f1c-b9536e34d381). The article provides information about where LinkedIn information shows up, [data sharing and privacy](https://support.microsoft.com/office/your-data-ae9c08a7-4d06-45b5-a065-320a97bc1400), [how to connect accounts](https://support.microsoft.com/office/connect-your-linkedin-and-work-or-school-accounts-c7c245f2-fa56-4c9b-ba20-3fceb23c5772) and more.

You must announce LinkedIn integration to your users and provide them all the information related to [data sharing and privacy with LinkedIn integration](https://support.microsoft.com/office/your-data-ae9c08a7-4d06-45b5-a065-320a97bc1400).

## User consent for data access in Microsoft and LinkedIn

Data that is accessed from LinkedIn isn't stored permanently in Microsoft services. Data that is accessed from Microsoft isn't stored permanently with LinkedIn.

When users connect their accounts, information and insights from LinkedIn are available in some Microsoft apps, like the profile card. Users can also expect their networking experience on LinkedIn to be improved and enriched with information from Microsoft. When users in your organization connect their LinkedIn and Microsoft work or school accounts, they have two options:

- Give permission for data to be accessed from both accounts. This means that they give permission for their Microsoft or work account to access data from their LinkedIn account, and for [their LinkedIn account to access data from their Microsoft work or school account](https://www.linkedin.com/help/linkedin/answer/84077).
- Give permission for only the LinkedIn data to be accessed by their Microsoft work and school account.

Users can disconnect accounts and remove data access permissions at any time, and [users can control how their own LinkedIn profile is viewed](https://www.linkedin.com/help/linkedin/answer/83), including whether their profile can be viewed in Microsoft apps.

### LinkedIn account data

When you connect your Microsoft and LinkedIn accounts, you allow LinkedIn to provide the following data to Microsoft:

- Profile data - includes LinkedIn identity, contact information, and the information you share with others on your [LinkedIn profile](https://www.linkedin.com/help/linkedin/answer/15493).
- Interests data - includes interests on LinkedIn, such as people and topics you follow, courses groups, and content you like and share.
- Subscriptions data - includes subscriptions to LinkedIn applications and services along with associated data.
- Connections data - includes your [LinkedIn network](https://www.linkedin.com/help/linkedin/answer/110) including profiles and contact information of your 1st-degree connections.

Data that is accessed from LinkedIn isn't stored permanently in Microsoft services. For more information about Microsoft’s use of personal data, see the [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement/).

### Microsoft work or school account data

When you connect your Microsoft and LinkedIn accounts, you allow Microsoft to provide the following data to LinkedIn:

- Profile data - includes information like your first name, last name, profile photo, email address, manager, and people that you manage.
- Calendar data - includes meetings in your calendars, their times, locations, and attendees' contact information. Information about the meeting, like agenda, content, or meeting title isn't included in the calendar data.
- Interests data - includes the interests associated with your account, based on your use of Microsoft services, such as Cortana and Bing for Business.
- Subscriptions data - includes subscriptions provided by your organization to Microsoft apps and services, such as Microsoft 365.
- Contacts data - includes contact lists in Outlook, Skype, and other Microsoft account services, including the contact information for people you frequently communicate or collaborate with. Contacts are periodically imported, stored, and used by LinkedIn, for example to suggest connections, help organize contacts, and show updates about contacts.

Data that is accessed from Microsoft isn't stored permanently with LinkedIn. For more information on LinkedIn’s use of personal data, see the [LinkedIn Privacy Policy](https://www.linkedin.com/legal/privacy-policy). For LinkedIn services, data transfer, and storage, data can flow from the European Union to the United States and back, and your privacy is protected as described in [European Union data transfers](https://www.linkedin.com/help/linkedin/answer/62533).