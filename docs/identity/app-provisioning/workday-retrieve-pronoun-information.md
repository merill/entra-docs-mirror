---
layout: Conceptual
title: Retrieve pronoun information from Workday - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/workday-retrieve-pronoun-information
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to retrieve pronoun information from Workday
ms.topic: reference
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: arvinh, chmutali
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: a9bff001-f340-a3b8-18c9-1046d5d68c99
document_version_independent_id: 809ff0b3-bd73-8c66-e312-55cce28f522c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/workday-retrieve-pronoun-information.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/workday-retrieve-pronoun-information
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/workday-retrieve-pronoun-information.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 9d897e29-1ebe-40a2-9834-1dfd479fce80
---

# Retrieve pronoun information from Workday - Microsoft Entra ID | Microsoft Learn

This article describes how you can customize the following two HR-driven provisioning apps to fetch pronoun information from Workday.

- [Workday to on-premises Active Directory user provisioning](../saas-apps/workday-inbound-tutorial)
- [Workday to Microsoft Entra user provisioning](../saas-apps/workday-inbound-cloud-only-tutorial)

## About pronoun information in Workday

Workday introduced the ability for workers to [display pronoun information](https://community.workday.com/node/731178) in their worker profile in Workday 2021 R1 release. The ability to fetch pronoun data using Workday Web Services (WWS) API call was introduced in [Get_Workers API version 38.1](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v38.1/Get_Workers.html) in Workday 2022 R1 release.

Note

Links to certain Workday community notes and documents in this article require Workday community account credentials. Please check with your Workday administrator or partner to get the required access.

## Enabling pronoun data in Workday

This section describes the steps required to enable pronoun data in Workday. We recommend engaging your Workday administrator to complete the steps listed.

1. Ensure that pronoun display and sharing preferences are enabled as per Workday guidelines. Refer to the Workday documents:

    - [Steps: Set Up Gender Pronouns to Display on a Worker Profile * Human Capital Management * Reader * Administrator Guide (workday.com)](https://doc.workday.com/r/gJQvxHUyQOZv_31Vknf%7E3w/7gZPvVfbRhLiPissprv6lQ)
    - [Steps: Set Up Public Profile Preferences * Human Capital Management * Reader * Administrator Guide (workday.com)](https://doc.workday.com/r/gJQvxHUyQOZv_31Vknf%7E3w/FuENV1VTRTHWo_h93KIjJA)
2. Use Workday **Maintain Pronouns** task to define preferred pronoun data (HE/HIM, SHE/HER, and THEY/THEM) in your Workday tenant.
3. Use Workday **Maintain Localization Settings task -&gt; Personal Information** area to activate pronoun data for different countries/regions.
4. Select the Workday Integration System Security Group used with your Microsoft Entra integration. Update the [domain permissions for the security group](../saas-apps/workday-inbound-tutorial#configuring-domain-security-policy-permissions), so it has GET access for the Workday domain **Reports: Public Profile**.

![Screenshot of permissions to setup in Workday.](media/workday-pronoun-data/workday-pronoun-permissions.png)
5. Activate Pending Security Policy changes.
6. Select a worker in your Workday tenant for testing purposes. Set pronoun information for this worker using the **Edit Personal Information** task. Ensure that the worker has enabled pronoun display to all in their public profile preference.

![Screenshot of enabling pronoun display option.](media/workday-pronoun-data/enable-pronoun-display-preference.png)
7. Use Workday Studio to invoke [Get_Workers API version 38.1](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v38.1/Get_Workers.html) for the test user using the Workday Microsoft Entra integration system user. In the SOAP request header, specify the option Include\_Reference\_Descriptors\_In\_Response.

    ```
      <bsvc:Workday_Common_Header>
         <bsvc:Include_Reference_Descriptors_In_Response>true</bsvc:Include_Reference_Descriptors_In_Response>
      </bsvc:Workday_Common_Header> 
    ```
8. In the Get\_Workers response, view the pronoun information.

![Screenshot of Workday Get Workers API response.](media/workday-pronoun-data/get-workers-response-with-pronoun.png)

Note

If you are not able to retrieve pronoun data in the *Get\_Workers* response, then troubleshoot Workday domain security permissions. Ensure your integration security group has permission to the segmented security group that grants access to the pronoun data.

Once you confirm that pronoun data is available in the *Get\_Workers* response, go to the next step of updating your Microsoft Entra provisioning app configuration.

To retrieve pronouns from Workday, update your Microsoft Entra provisioning app to query Workday using v38.1 of the Workday Web Services. We recommend testing this configuration first in your test/sandbox environment before implementing the change in production.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Select your Workday to Active Directory / Microsoft Entra user provisioning application and go to **Provisioning** .
4. In the **Admin Credentials** section, update the **Tenant URL** to include the Workday Web Service version v38.1 as shown.

![Screenshot of Microsoft Entra admin center provisioning app with Workday version.](media/workday-pronoun-data/update-workday-version.png)
5. Open the **Attribute Mapping** page. Select the **Advanced Options** dropdown and then select **Edit target User attributes**.
6. If your provisioning app is configured to use the default WWS API version v21.1, then [reference this article to review and update the XPATHs for each attribute](workday-attribute-reference#xpath-values-for-workday-web-services-wws-api-v30).
7. Add a new attribute called **PreferredPronoun** with XPATH

    `/wd:Worker/wd:Worker_Data/wd:Personal_Data/wd:Personal_Information_Data/wd:Pronoun_Reference/@wd:Descriptor`
8. Save your changes.
9. You can now add a new attribute mapping to flow the Workday attribute **PreferredPronoun** to any attribute in AD/Microsoft Entra ID.
10. If you want to incorporate pronoun information as part of display name, you can update the attribute mapping for displayName attribute to use the expression.

    `Switch([PreferredPronoun], Join("", [PreferredNameData], " (", [PreferredPronoun], ")"), "", [PreferredNameData])`
11. If worker *Aaron Hall* has set his pronoun information in Workday as `HE/HIM`, the above expression sets the display name in Microsoft Entra ID as: *Aaron Hall (HE/HIM)*
12. Save your changes.
13. Test the configuration for one user with provisioning on demand.