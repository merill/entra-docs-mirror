---
layout: Conceptual
title: Upload hardware OATH tokens in CSV format - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-mfa-upload-oath-tokens
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn how to upload hardware OATH tokens in Microsoft Entra ID by using CSV file and Global Administrator role.
services: active-directory
ms.topic: how-to
ms.date: 2025-12-11T00:00:00.0000000Z
ms.reviewer: lvandenende, edwardd
ms.collection: M365-identity-device-management
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 31e44aa6-20c9-18bc-bed7-dc0f6cb70469
document_version_independent_id: 31e44aa6-20c9-18bc-bed7-dc0f6cb70469
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/how-to-mfa-upload-oath-tokens.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/how-to-mfa-upload-oath-tokens
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/how-to-mfa-upload-oath-tokens.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 768b0953-1b1f-f737-ff36-0fb9d7aa73b4
---

# Upload hardware OATH tokens in CSV format - Microsoft Entra ID | Microsoft Learn

Hardware OATH tokens typically come with a secret key, or seed, preprogrammed in the token. Before a user can sign in to their work or school account in Microsoft Entra ID by using a hardware OATH token, an administrator needs to add the token to the tenant.

The recommended way to add the token is by using Microsoft Graph with a least privileged administrator role. An updated process that uses a least privileged role is in preview. For more information, see [Hardware OATH tokens (preview)](concept-authentication-oath-tokens#hardware-oath-tokens-preview).

As an alternative to using Microsoft Graph APIs, tenants with a Microsoft Entra ID Premium license can have a Global Administrator input these keys into Microsoft Entra ID. If you upload tokens in CSV format, they aren't compatible with the new features in preview. To use the Hardware OATH tokens preview instead of CSV upload, see [How to manage OATH tokens in Microsoft Entra ID (Preview)](how-to-mfa-manage-oath-tokens).

## CSV format

Secret keys are limited to 128 characters, which isn't compatible with some tokens. The secret key can only contain the characters *a-z* or *A-Z* and digits *2-7*, and must be encoded in *Base32*.

Programmable OATH time-based one-time passcode (TOTP) hardware tokens that can be reseeded can also be set up with Microsoft Entra ID in the software token setup flow.

[![Screenshot of OATH token management.](media/concept-authentication-methods/oath-tokens.png)](media/concept-authentication-methods/oath-tokens.png#lightbox)

Once tokens are acquired, a Global Administrator must upload them in a comma-separated values (CSV) file format. The file should include the UPN, serial number, secret key, time interval, manufacturer, and model, as shown in the following example:

```csv
upn,serial number,secret key,time interval,manufacturer,model
Helga@contoso.com,1234567,2234567abcdef2234567abcdef,60,Contoso,HardwareKey
```

Note

Make sure you include the header row in your CSV file.

Once properly formatted as a CSV file, the Global Administrator can then sign in to the Microsoft Entra admin center, navigate to **Entra ID** &gt; **Multifactor authentication** &gt; **OATH tokens**, and upload the resulting CSV file.

Depending on the size of the CSV file, it can take a few minutes to process. Select the **Refresh** button to get the current status. If there are any errors in the file, you can download a CSV file that lists any errors for you to resolve. The field names in the downloaded CSV file are different than the uploaded version.

Users can have a combination of up to five OATH hardware tokens or authenticator applications, such as the Microsoft Authenticator app, configured for use at any time. Hardware OATH tokens can't be assigned to guest users in the resource tenant.

Important

Make sure to only assign each token to a single user. A single token can't be assigned to multiple users.

## Troubleshooting a failure during upload processing

At times, there may be conflicts or issues that occur with the processing of an upload of the CSV file. If any conflict or issue occurs, you get notified like this:

![Screenshot of upload error example.](media/concept-authentication-methods/upload-error-example.png)

To determine the error message, be sure and select **View Details**. The **Hardware token status** blade opens and provides the summary of the status of the upload. It shows if there's a failure, or multiple failures, as in the following example:

![Screenshot of hardware token status example.](media/concept-authentication-methods/hardware-token-status.png)

To determine the cause of the failure listed, make sure to select the checkbox next to the status you want to view, which activates the **Download** option. This option downloads a CSV file that contains the error identified.

![Screenshot of download status example.](media/concept-authentication-methods/download-status-example.png)

The downloaded file is named **Failures\_filename.csv**, where *filename* is the name of the file uploaded. The file is saved to your default downloads directory for your browser.

This example shows the error identified as a user who doesn't currently exist in the tenant directory:

![Screenshot of error reason example.](media/concept-authentication-methods/error-reason-example.png)

After you fix the errors listed, upload the CSV again until it processes successfully. The status information for each attempt remains for 30 days. To remove the CSV, select the checkbox next to the status, then select **Delete status**.