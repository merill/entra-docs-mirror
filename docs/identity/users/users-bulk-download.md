---
layout: Conceptual
title: Download a list of users in the Azure portal (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/users-bulk-download
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Download user records in bulk in the Azure admin center in Microsoft Entra ID.
ms.date: 2025-08-19T00:00:00.0000000Z
ms.topic: how-to
ms.custom: it-pro, sfi-image-nochange
ms.reviewer: yukarppa
locale: en-us
document_id: 7800fcb4-d251-f271-bc12-9377cd0407fa
document_version_independent_id: 319b62fc-cea7-1add-559b-bb2a35b3a0ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/users-bulk-download.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/users-bulk-download
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/users-bulk-download.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 894580ed-52f0-da72-ef5e-4b787bb6c74e
---

# Download a list of users in the Azure portal (Preview) - Microsoft Entra ID | Microsoft Learn

## Overview

Microsoft Entra ID, part of Microsoft Entra, supports bulk user list download operations.

## Required permissions

Both admin and standard users can download user lists.

## To download a list of users

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Select Microsoft Entra ID.
3. Select **Users** &gt; **All users** &gt; **Download users**. By default, all user profiles are exported.
4. On the **Download users** page, select **Start** to receive a CSV file listing user profile properties. If there are errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error.

    ![Screenshot of selecting where you want to list the users you want to download.](media/users-bulk-download/bulk-download.png)

Note

The download file will contain the filtered list of users based on the scope of the filters applied.

The following user attributes are included:

- `userPrincipalName`
- `displayName`
- `surname`
- `mail`
- `givenName`
- `objectId`
- `userType`
- `jobTitle`
- `department`
- `accountEnabled`
- `usageLocation`
- `streetAddress`
- `state`
- `country`
- `physicalDeliveryOfficeName`
- `city`
- `postalCode`
- `telephoneNumber`
- `mobile`
- `authenticationAlternativePhoneNumber`
- `authenticationEmail`
- `alternateEmailAddress`
- `ageGroup`
- `consentProvidedForMinor`
- `legalAgeGroupClassification`

## Check status

You can see the status of your pending bulk requests in the **Bulk operation results** page.

[![Screenshot showing status in the Bulk Operations Results page.](media/users-bulk-download/bulk-center.png)](media/users-bulk-download/bulk-center.png#lightbox)

If you experience errors, you can download and view the results file on the **Bulk operation results** page. The file contains the reason for each error. The file submission must match the provided template and include the exact column names. For more information about bulk operations limitations, see Bulk download service limits.

## Bulk download service limits

Note

When performing bulk operations, such as import or create, you can encounter a problem if the bulk operation doesn't complete within the hour. To work around this issue, we recommend splitting the number of records processed per batch. For example, before starting an export you could limit the result set by filtering on a group type or user name to reduce the size of the results. By refining your filters, essentially you limit the data returned by the bulk operation. For more information, see [Bulk operations service limitations](../../fundamentals/bulk-operations-service-limitations).

## Improved bulk user download in Microsoft Entra admin center (Preview)

The enhanced bulk user download experience includes:

**Customizable columns for export**: Previously, user exports included only a fixed set of predefined attributes. With this update, admins can customize their User List View columns, and the export will mirror those selected columns. This gives IT admins greater control and relevance in the data they download.

**Expanded attribute coverage**: 27 new user attributes are now added to the exportable list, enabling deeper insights and more tailored exports. See full list of these newly exportable attributes:

1. Assigned licenses
2. Authorization info
3. Employee ID
4. Employee hire date
5. Employee org data
6. Employee type
7. Extension attributes
8. External user state change date time
9. Fax number
10. IM addresses
11. Last password change date time
12. Last interactive sign-in date
13. Last non-interactive sign-in date
14. On-premises SAM account name
15. On-premises distinguished name
16. On-premises domain name
17. On-premises immutable ID
18. On-premises last sync date time
19. On-premises provisioning errors
20. On-premises security identifier
21. On-premises user principal name
22. Password policies
23. Password profile
24. Preferred data location
25. Preferred language
26. Proxy addresses
27. Sign in sessions valid from date time

Note

Columns derived from complex properties are exported as the entire complex property. For example, downloading the **Last interactive sign-in date** column results in the entire signInActivity property, along with all its related data fields, to be included in the CSV file.

### Performance improvements

The bulk download process is now up to 12 to 15 times faster, improving experience and efficiency for large user lists. This improvement also eliminates the service limitation that exists today which creates issues if the bulk operation doesn’t complete within 1 hour.

### User experience

1. Select the **Download users (Preview)** button from the command bar on the **All users** page.

    ![Screenshot of the Download users option](media/users-bulk-download/download-users.png)
2. When the context pane opens, select **Start download** and when that succeeds, select **File is ready! Click here to download** to download the CSV.

    ![Screenshot of download button that starts the download](media/users-bulk-download/start-download.png)
3. On the left menu, go to **Bulk operation results (Preview)** to view the status of your bulk download request. Only the preview download results will appear in this preview tab.

    [![Screenshot of checking the status in the Bulk Operations Results page.](media/users-bulk-download/bulk-download-results.png)](media/users-bulk-download/bulk-center.png#lightbox)