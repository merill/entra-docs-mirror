---
layout: Conceptual
title: How to analyze activity logs with Microsoft Graph - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-analyze-activity-logs-with-microsoft-graph
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: monitoring-health
manager: dougeby
description: Learn how to access and analyze Microsoft Entra sign-in and audit logs with the Microsoft Graph reporting APIs.
ms.topic: how-to
ms.date: 2025-06-30T00:00:00.0000000Z
ms.reviewer: egreenberg
locale: en-us
document_id: 492a93a1-ed2f-bb28-0704-adbcc29caedd
document_version_independent_id: 492a93a1-ed2f-bb28-0704-adbcc29caedd
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/monitoring-health/howto-analyze-activity-logs-with-microsoft-graph.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/monitoring-health/howto-analyze-activity-logs-with-microsoft-graph
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/monitoring-health/howto-analyze-activity-logs-with-microsoft-graph.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: f62bd9bd-a680-bbb7-cbf9-a7231fc7623b
---

# How to analyze activity logs with Microsoft Graph - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra [reporting APIs](/en-us/graph/api/resources/azure-ad-auditlog-overview) provide you with programmatic access to the data through a set of REST APIs. You can call these APIs from many programming languages and tools.

This article describes how to analyze Microsoft Entra activity logs with Microsoft Graph Explorer and Microsoft Graph PowerShell.

## Prerequisites

- A working Microsoft Entra tenant with a Microsoft Entra ID P1 or P2 license associated with it.
- To consent to the required permissions, you need the [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator).

## Access reports using Microsoft Graph Explorer

With all the prerequisites configured, you can run activity log queries in Microsoft Graph. The Microsoft Graph API isn't designed for pulling large amounts of activity data. Pulling large amounts of activity data using the API might lead to issues with pagination and performance. For more information on Microsoft Graph queries for activity logs, see [Activity reports API overview](/en-us/graph/api/resources/azure-ad-auditlog-overview).

1. Start [Microsoft Graph Explorer tool](https://aka.ms/ge).
2. Select your profile and then select **Modify permissions**.
3. Consent to the following required permissions:

    - `AuditLog.Read.All`
    - `Directory.Read.All`
4. Use one of the following queries to start using Microsoft Graph for accessing activity logs:

    - GET `https://graph.microsoft.com/v1.0/auditLogs/directoryAudits`
    - GET `https://graph.microsoft.com/v1.0/auditLogs/signIns`
    - GET `https://graph.microsoft.com/v1.0/auditLogs/provisioning`
    - GET `https://graph.microsoft.com/beta/auditLogs/signUps`

    ![Screenshot of an activity log GET query in Microsoft Graph.](media/howto-analyze-activity-logs-with-microsoft-graph/graph-sample-get-query.png)

### Fine-tune your queries

To search for specific activity log entries, use the $filter and createdDateTime query parameters with one of the available properties. Some of the following queries use the `beta` endpoint. The beta endpoint is subject to change and isn't recommended for production use.

- [Sign-in log properties](/en-us/graph/api/resources/signin#properties)
- [Sign-up log properties (preview)](/en-us/graph/api/resources/selfservicesignup#properties)
- [Audit log properties](/en-us/graph/api/resources/directoryaudit#properties)

#### Sample sign-in queries

Try using the following queries for sign-in activity:

- For sign-in attempts where Conditional Access failed:

    - GET `https://graph.microsoft.com/v1.0/auditLogs/signIns?$filter=conditionalAccessStatus eq 'failure'`
    - Consider using a date filter so the request doesn't time out.
- To find sign-ins to a specific application during a specific time frame:

    - GET `https://graph.microsoft.com/v1.0/auditLogs/signIns?$filter=(createdDateTime ge 2024-01-13T14:13:32Z and createdDateTime le 2024-01-14T17:43:26Z) and appId eq 'APP ID'`
- For non-interactive sign-ins:

    - GET `https://graph.microsoft.com/beta/auditLogs/signIns?$filter=(createdDateTime ge 2024-01-13T14:13:32Z and createdDateTime le 2024-01-14T17:43:26Z) and signInEventTypes/any(t: t eq 'nonInteractiveUser')`
- For service principal sign-ins:

    - GET `https://graph.microsoft.com/beta/auditLogs/signIns?$filter=(createdDateTime ge 2024-01-13T14:13:32Z and createdDateTime le 2024-01-14T17:43:26Z) and signInEventTypes/any(t: t eq 'servicePrincipal')`
- For managed identity sign-ins:

    - GET `https://graph.microsoft.com/beta/auditLogs/signIns?$filter=(createdDateTime ge 2024-01-13T14:13:32Z and createdDateTime le 2024-01-14T17:43:26Z) and signInEventTypes/any(t: t eq 'managedIdentity')`
- To get the authentication method of a user:

    - GET `https://graph.microsoft.com/beta/users/{userObjectId}/authentication/methods`
    - Requires `UserAuthenticationMethod.Read.All` permission
- To see the user registration details report:

    - GET `https://graph.microsoft.com/beta/reports/authenticationMethods/userRegistrationDetails`
    - Requires `UserAuthenticationMethod.Read.All` permission
- For the registration details of specific user:

    - GET `https://graph.microsoft.com/beta/reports/authenticationMethods/userRegistrationDetails/{userId}`
    - Requires `UserAuthenticationMethod.Read.All` permission

#### Sample sign-up queries (preview)

Try using the following queries for sign-up activity in your [external tenant](../../external-id/tenant-configurations):

- To find sign-up attempts that failed or were interrupted during a specific step, such as user object creation:

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=status/errorCode ne 0 and signUpStage eq 'userCreation'`
- To find sign-up attempts that failed during email validation:

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=status/errorCode eq 1002013 and signUpStage eq 'credentialValidation'`

    Note

    Error code 1002013 indicates an expected (and successful) interrupt of the sign-up flow. [Learn more](howto-troubleshoot-sign-up-errors#sign-up-error-codes)
- For sign-ups during a date range:

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=(createdDateTime ge 2024-01-13T14:13:32Z and createdDateTime le 2024-01-14T17:43:26Z)`
- For sign-ups for a specific application:

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=appId eq 'AppId'`
- For local account sign-ups:

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=signUpIdentityProvider eq 'Email OTP' or signUpIdentityProvider eq 'Email Password'`
- For social account sign-ups (Google in this example):

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=signUpIdentityProvider eq 'Google'`
- To see entries for a specific user, for example `user@contoso.com`:

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=signUpIdentity/signUpIdentifier eq 'user@contoso.com'`
- To find entries matching a specific correlation ID:

    - GET `https://graph.microsoft.com/beta/auditLogs/signUps?$filter=correlationId eq 'CorrelationId'`
- To find the sign-in log entries corresponding to a specific sign-up using the correlation ID:

    - GET `https://graph.microsoft.com/v1.0/auditLogs/signIns?$filter=correlationId eq 'CorrelationId'`

### Related APIs

Once you're familiar with the standard sign-in and audit logs, try exploring these other APIs:

- [Identity Protection APIs](/en-us/graph/api/resources/identityprotection-overview)
- [Provisioning logs API](/en-us/graph/api/resources/provisioningobjectsummary)

## Access reports using Microsoft Graph PowerShell

You can use PowerShell to access the Microsoft Entra reporting API. For more information, see [Microsoft Graph PowerShell overview](/en-us/powershell/microsoftgraph/overview).

Microsoft Graph PowerShell cmdlets:

- **Audit logs:**`Get-MgAuditLogDirectoryAudit`
- **Sign-in logs:**`Get-MgAuditLogSignIn`
- **Provisioning logs:**`Get-MgAuditLogProvisioning`
- Explore the full list of [reporting-related Microsoft Graph PowerShell cmdlets](/en-us/powershell/module/microsoft.graph.reports/).

## Common errors

**Error: Neither tenant is B2C or tenant doesn't have premium license**: Accessing sign-in reports requires a Microsoft Entra ID P1 or P2 license. If you see this error message while accessing sign-ins, make sure that your tenant is licensed with a Microsoft Entra ID P1 license.

**Error: User isn't in the allowed roles**: If you see this error message while trying to access audit logs or sign-ins using the API, make sure that your account is part of the **Security Reader** or **Reports Reader** role in your Microsoft Entra tenant.

**Error: Application missing Microsoft Entra ID 'Read directory data' or 'Read all audit log data' permission**: The application must have either the `AuditLog.Read.All` or `Directory.Read.All` permission to access the activity logs with Microsoft Graph.