---
layout: Conceptual
title: Sign-ins to applications using SAML authentication - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/scenario-health-sign-ins-saml-auth
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn about the Microsoft Entra Health signals and alerts for sign-ins to applications that use SAML authentication
ms.topic: how-to
ms.date: 2025-07-31T00:00:00.0000000Z
ms.reviewer: sarbar
locale: en-us
document_id: 36cb76a7-319f-c7b1-8fc6-c4f5e2c50ed5
document_version_independent_id: 36cb76a7-319f-c7b1-8fc6-c4f5e2c50ed5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/scenario-health-sign-ins-saml-auth.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/scenario-health-sign-ins-saml-auth
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/scenario-health-sign-ins-saml-auth.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d82d32d7-4650-a596-e76e-82cec97ecb95
---

# Sign-ins to applications using SAML authentication - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Health monitoring provides a set of tenant-level health metrics you can monitor to help improve the health of your tenant. The Security Assertion Markup Language (SAML) authentication scenario monitors SAML 2.0 authentication attempts that the Microsoft Entra cloud service for your tenant successfully processed.

- [Learn how the Microsoft Identity platform uses the SAML protocol](../../identity-platform/saml-protocol-reference)
- [Use a SAML 2.0 IdP for single sign on](../hybrid/connect/how-to-connect-fed-saml-idp).
- This metric currently excludes WS-FED/SAML 1.1 apps integrated with Microsoft Entra ID.
- Alerts are not available for this scenario.

Important

Microsoft Entra Health scenario monitoring and alerts are currently in PREVIEW. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

There are different roles, permissions, and license requirements to view health monitoring signals and configure and receive alerts. We recommend using a role with least privilege access to align with the [Zero Trust guidance](/en-us/security/zero-trust/zero-trust-overview).

- A tenant with a [Microsoft Entra P1 or P2 license](../../fundamentals/get-started-premium) is required to view the Microsoft Entra health scenario monitoring signals.
- The [Reports Reader](../role-based-access-control/permissions-reference#reports-reader) role is the least privileged role required to view scenario monitoring signals.
- The `HealthMonitoringAlert.Read.All` permission is required to *view the alerts using the Microsoft Graph API*.
- For a full list of roles, see [Least privileged role by task](../role-based-access-control/delegate-by-task#microsoft-entra-health-least-privileged-roles).

## Investigate the signals and alerts

Investigating an alert starts with gathering data. With Microsoft Entra Health in the Microsoft Entra admin center, you can view the signal and alert details in one place. You can also view the signals and alerts using the Microsoft Graph API. For more information, see [How to investigate health scenario alerts](howto-investigate-health-scenario-alerts) for guidance on how to gather data using the Microsoft Graph API.

1. Sign into the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Reports Reader](../role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Health**. The page opens to the Service Level Agreement (SLA) Attainment page.
3. Select the **Health Monitoring** tab.
4. Select the **Sign-ins to applications using SAML authentication** scenario and then select an active alert from the page that opens.

    [![Screenshot of the SAML Health monitoring scenario.](media/scenario-health-sign-ins-saml-auth/saml-alert.png)](media/scenario-health-sign-ins-saml-auth/saml-alert.png#lightbox)
5. View the signal from the **View data graph** section to get familiar with the pattern and identify anomalies.
6. Review the sign-in logs.

    - [Review the sign-in log details](concept-sign-in-log-activity-details).
    - In the Microsoft Entra admin center, you might need to add the **Authentication protocol** column, then filter for **SAML 2.0** sign-ins to look for patterns in the sign-ins.

## Mitigate common issues

The following common issues could cause a spike or dip in sign-ins to applications using SAML authentication. In general, this alert fires if a new application was rolled out without being properly configured for SAML authentication. This list isn't exhaustive, but provides a starting point for investigation.

### Application is missing signing certificates

A decrease in SAML sign-ins could indicate users are blocked because the application is missing the signing certificate. The application object is considered corrupted, and users can't sign in to the application.

To investigate:

1. From the **Affected entities** section of the selected scenario, select **View**for applications.
    - A list of affected applications appears in a panel. Select the application to navigate directly to the application registration details.
2. Check the **Certificates and secrets**section of the application to ensure that the signing certificate is present and valid.
    - If the signing certificate is missing or expired, you need to update it with a valid certificate.
3. Browse to the **Enterprise applications** &gt; **Single sign-on** and select **Edit** in the **SAML Certificates** tile to update the certificate.
4. After updating the certificate and validating the configuration works, remove any old certificates that are no longer needed.

### Reply URL is missing or incorrect

A dip in SAML sign-ins could also indicate the SAML reply URL is missing or incorrect. Sign-in attempts are blocked because Microsoft doesn't know where to send the sign-in response.

To investigate:

1. From the **Affected entities** section of the selected scenario, select **View**for applications.
    - A list of affected applications appears in a panel. Select the application to navigate directly to the application registration details.
2. From **Enterprise applications** &gt; **Single sign-on** and review the **Basic SAML Configuration** tile and make sure the **Reply URL**is configured correctly.
    - If the reply URL is missing or incorrect, you need to update it with the correct URL.

### Application access is misconfigured

A dip in SAML sign-ins might mean the access permissions for the application are misconfigured, preventing users from signing in. This dip could affect a small number of users or a large group, depending on if the user or the application that doesn't have the correct permissions.

If the dip in sign-ins affects a small number of users:

1. From the **Affected entities** section of the selected scenario, select **View** for users.
2. Select a user to navigate directly to their profile where you can review their group memberships and role permissions.

If the dip in sign-ins affects a large group of users:

1. From the **Affected entities** section of the selected scenario, select the **View**link for any affected applications.
    - Confirm that the appropriate sign-sign on configurations and app permissions are in place.
2. Review any Conditional Access policies that might block access to the application.