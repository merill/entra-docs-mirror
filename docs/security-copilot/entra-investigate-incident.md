---
layout: Conceptual
title: Investigate identity risk in Microsoft Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-investigate-incident
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Microsoft Security Copilot and Microsoft Entra skills to quickly investigate identity-based security incident.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: 239151d0-084e-b9c1-47b6-8055775e78ca
document_version_independent_id: 239151d0-084e-b9c1-47b6-8055775e78ca
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-investigate-incident.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-investigate-incident
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-investigate-incident.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/03921bea-3752-4ddc-98c2-5aa70db91565
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/09911d3e-3eb9-4c8d-ab86-ce80d8d36bbd
platformId: a1f39a02-b62c-6677-2b02-6597678c0e71
---

# Investigate identity risk in Microsoft Security Copilot | Microsoft Learn

[Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) gets insights from your Microsoft Entra data through many different skills, such as Get Entra Risky Users and Get Audit Logs. IT admins and security operations center (SOC) analysts can use these skills and others to gain the right context to help investigate and remediate identity-based incidents using natural language prompts.

This article describes how a SOC analyst or IT admin could use the Microsoft Entra skills to investigate a potential security incident.

## Prerequisites

- A tenant with Security Copilot enabled. Refer to [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot#option-2-provision-capacity-in-azure) for more information.

## Scenario and investigation

Natasha, a security operations center (SOC) analyst at Woodgrove Bank, receives an alert about a potential identity-based security incident. The alert indicates suspicious activity from a user account that has been flagged as a risky user. She starts her investigation and signs in to [Microsoft Security Copilot](https://securitycopilot.microsoft.com/) or the [Microsoft Entra admin center](https://entra.microsoft.com). In order to view user, group, risky user, sign-in logs, audit-logs, and diagnostic logs details, she signs in as at least a [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader). She can use Microsoft Security Copilot to activate this role if she is blocked due to a lack of permissions to perform certain actions:

- *Activate the {required role} so that I can perform {desired task}.*

### Get user details

Natasha starts by looking up details of the flagged user: karita@woodgrovebank.com. She reviews the user’s profile information such as job title, department, manager, and contact information. She also checks the user’s assigned roles, applications, and licenses to understand what applications and services the user has access to.

She uses the following prompts to get the information she needs:

- *Give me all user details for karita@woodgrovebank.com and extract the user Object ID.*
- *Is this user's account enabled?*
- *When was the password last changed or reset for karita@woodgrovebank.com?*
- *Does karita@woodgrovebank.com have any registered devices in Microsoft Entra?*
- *What are the authentication methods that are registered for karita@woodgrovebank.com if any?*

### Get risky user details

To understand why karita@woodgrovebank.com was flagged as a risky user, Natasha starts looking at the risky user details. She reviews the risk level of the user (low, medium, high, or hidden), the risk detail (for example, sign-in from unfamiliar location), and the risk history (changes in risk level over time). She also checks the risk detections and the recent risky sign-ins, looking for suspicious sign-in activity or impossible travel activity.

She uses the following prompts to get the information she needs:

- *What is the risk level, state, and risk details for karita@woodgrovebank.com?*
- *What is the risk history for karita@woodgrovebank.com?*
- *List the recent risky sign-ins for karita@woodgrovebank.com.*
- *List the risk detections details for karita@woodgrovebank.com.*

### Get sign-in logs details

Natasha then reviews the sign-in logs for the user and the sign-in status (success or failure), location (city, state, country), IP address, device information (device ID, operating system, browser), and sign-in risk level. She also checks the correlation ID for each sign-in event, which can be used for further investigation.

She uses the following prompts to get the information she needs:

- *Can you give me sign-in logs for karita@woodgrovebank.com for the past 48 hours? Put this information in a table format.*
- *Show me failed sign-ins for karita@woodgrovebank.com for the past 7 days and tell me what the IP addresses are.*

### Get audit logs details

Natasha checks the audit logs, looking for any unusual or unauthorized actions performed by the user. She checks the date and time of each action, the status (success or failure), the target object (for example, file, user, group), and the client IP address. She also checks the correlation ID for each action, which can be used for further investigation.

She uses the following prompts to get the information she needs:

- *Get Microsoft Entra audit logs for karita@woodgrovebank.com for the past 72 hours. Put information in table format.*
- *Show me audit logs for this event type.*

### Get group details

Natasha then reviews the groups that karita@woodgrovebank.com is a part of to see if Karita is a member of any unusual or sensitive groups. She reviews the group memberships and permissions associated with Karita's user ID. She checks the group type (security, distribution, or Office 365), membership type (assigned or dynamic), and the group’s owners in the group details. She also reviews the group’s roles to determine what permissions it has for managing resources.

She uses the following prompts to get the information she needs:

- *Get the Microsoft Entra user groups that karita@woodgrovebank.com is a member of. Put information in table format.*
- *Tell me more about the Finance Department group.*
- *Who are the owners of the Finance Department group?*
- *What roles does this group have?*

## Deactivate your role

After completing her tasks with Microsoft Security Copilot, Natasha needs to deactivate any elevated roles activated during her session to maintain security best practices. She uses the following prompt to deactivate her role:

- *I am done with my investigation or {desired task}, deactivate my access.*

## Remediate

By using Security Copilot, Natasha is able to gather comprehensive information about the user, sign-in activities, audit logs, risky user detections, group memberships, and system diagnostics. After completing her investigation, Natasha needs to take action to remediate the risky user or unblock them.

She reads about [risk remediation](/en-us/entra/id-protection/howto-identity-protection-remediate-unblock#risk-remediation), [unblocking users](/en-us/entra/id-protection/howto-identity-protection-remediate-unblock#unblocking-users), and [response playbooks](/en-us/security/operations/incident-response-playbooks) to determine possible actions to take next.