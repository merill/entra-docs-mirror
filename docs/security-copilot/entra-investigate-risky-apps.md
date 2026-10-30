---
layout: Conceptual
title: Investigate app risk using Microsoft Security Copilot | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/security-copilot/entra-investigate-risky-apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: cilwerner
ms.author: cwerner
manager: pmwongera
description: Use Microsoft Security Copilot and Microsoft Entra skills to quickly investigate potential risky applications.
ms.reviewer: ptyagi
ms.date: 2025-09-23T00:00:00.0000000Z
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: entra
ms.custom: security-copilot
ms.collection: msec-ai-copilot
locale: en-us
document_id: 7593dd46-9dcf-8af9-756b-afe807f7f3b8
document_version_independent_id: 7593dd46-9dcf-8af9-756b-afe807f7f3b8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/security-copilot/entra-investigate-risky-apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot/entra-investigate-risky-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/security-copilot/entra-investigate-risky-apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 785220d0-e5ad-8077-3f52-f47b68b72945
---

# Investigate app risk using Microsoft Security Copilot | Microsoft Learn

[Microsoft Security Copilot](/en-us/security-copilot/microsoft-security-copilot) gets insights from your Microsoft Entra data through many different skills, such as Investigate identity risks with Microsoft Entra ID Protection and Explore Microsoft Entra audit log details. App risk skills allow identity admins and security analysts who manage applications or workload identities in Microsoft Entra to identify and understand risks through natural language prompts. By using prompts like, "*List risky app details for my tenant*", the analyst gets a better picture of the risk from application identities and can discover other application details in Microsoft Entra. Details can include permissions granted (especially high privileged permissions), unused apps in their tenant, and apps from outside their tenant.

Security Copilot then uses prompt context to respond, such as with a list of apps or permissions, then surface links to the Microsoft Entra admin center so that admins can see a full list and take the appropriate remediation actions for their risky apps. IT admins and security operations center (SOC) analysts can use these skills and others to gain the right context to help investigate and remediate identity-based incidents using natural language prompts.

This article describes how a SOC analyst or IT admin could use the Microsoft Entra skills to investigate a potential security incident.

Note

These app risk skills provide data on single tenant, third party SaaS, and multitenant apps that are applications or service principals in Microsoft Entra. Managed identities aren't currently in scope.

## Prerequisites

- A tenant with Security Copilot enabled. Refer to [Get started with Microsoft Security Copilot](/en-us/copilot/security/get-started-security-copilot#option-2-provision-capacity-in-azure) for more information.

## Scenario and investigation

Jason, an IT admin at Woodgrove Bank, is proactively trying to identify and understand any risky apps in their tenant. He starts his assessment and signs in to [Microsoft Security Copilot](https://securitycopilot.microsoft.com/) or the [Microsoft Entra admin center](https://entra.microsoft.com). To view application and service principal details, he signs in as at least a [Security Reader](/en-us/entra/identity/role-based-access-control/permissions-reference#security-reader) and a Microsoft Entra role assignment of [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or similar Microsoft Entra administrator role that has permissions to manage application/workload identities in Microsoft Entra. He can use Microsoft Security Copilot to activate this role if he is blocked due to a lack of permissions to perform certain actions:

- *Activate the {required role} so that I can perform {desired task}.*

Identity admins using [Security Copilot as a part of the Microsoft Entra admin center](entra-security-scenarios#microsoft-security-copilot-scenarios-in-microsoft-entra-overview) can choose from a set of app risk starter prompts that appear at the top of the Security Copilot window. Select from suggested prompts that may appear after a response. App risk starter prompts will appear in application-related admin center blades: **Enterprise apps**, **App Registrations**, and **Identity Protection Risky workload identities**.

![Screenshot that shows starter prompts in Security Copilot.](media/copilot-security-entra-investigate-risky-apps/starter-prompts.png)

### Explore Microsoft Entra risky service principals

Jason starts his investigations by asking natural language questions to get a better picture of the risk "hot spots". This uses [ID Protection risky workload identity](../id-protection/concept-workload-identity-risk) data as an initial filter on the scale of apps in their tenant based on our Microsoft detections. These service principals carry an elevated risk of compromise.

He uses any of the following prompts to get the information he needs:

- *Show me risky apps.*
- *Are any apps at risk of being malicious or compromised?*
- *List 5 apps with High Risk Level. Format the table as follows: Display Name | ID | Risk State*
- *List the apps with Risk State "Confirmed compromise".*
- *Show me the details of risky app with ID {ServicePrincipalObjectId} (or App ID {ApplicationId})*

Important

You must use an account that is authorized to administer ID Protection for this skill to return risk information. Your tenant must also be licensed for [Workload Identities Premium](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-workload-id#office-StandaloneSKU-k3hubfz).

### Explore Microsoft Entra service principals

To get more information about these service principals identified as risky, Jason asks for more information from Microsoft Entra, including information like the owner.

He uses the following prompts to get the information he needs:

- *Tell me more about these service principals (from previous response).*
- *Give me details about service principal with {DisplayName} (or {ServicePrincipalId}).*
- *Give me a list of owners for these apps?*

### Explore Microsoft Entra applications

Jason also wants to understand more about the applications globally, such as details about the publisher and publisher verification status.

Jason uses the following prompts to retrieve selected application properties:

- *Tell me more about the application {DisplayName} or {AppId}.*
- *Tell me more about these apps (from previous response).*

### View the permissions granted on a Microsoft Entra service principal

Jason continues his assessment and wants to know what permissions were granted to all or one of the apps to find the potential impact if compromised. This is normally difficult to evaluate across some of the different types of permissions and administrator roles but Copilot simplifies it in a list in context of the investigation. This skill retrieves Delegated permissions, Application permissions, and Microsoft Entra administrator roles for a given Microsoft Entra service principal.

Jason can also identify high privilege permissions granted on a service principal, based on Microsoft's risk assessment. These are currently scoped to application permissions that generally enable tenant-wide access without user context and highly privileged Microsoft Entra administrator roles.

Important

This skill currently only looks at [API permissions](../identity-platform/permissions-consent-overview) and [Microsoft Entra administrator roles](../identity/role-based-access-control/permissions-reference). It doesn't currently look at non-directory permissions granted in places like Azure RBAC or other authorization systems. High privileged permissions are limited to a static list of maintained by Microsoft that might evolve over time and it isn't currently viewable or customizable by customers.

He uses the following prompts to get the permissions information he needs:

- *Which permissions are granted to the app with ID {ServicePrincipalId} or app ID {AppId}?*
- *What permissions do the above risky apps have (from previous response)?*
- *Which permissions granted to this app are highly privileged?*

### Explore unused Microsoft Entra applications

Jason realizes he has another "low hanging fruit" opportunity: to reduce risk by removing unused apps. These are quick wins because:

1. Removing an unused app addresses many other risks with a single remediation action.
2. You can often address unused apps aggressively through central action while keeping the risk of outage or business disruption low, since users aren't actually using the apps.

Using the Copilot prompts integrated with the existing [Microsoft Entra recommendation for unused apps](../identity/monitoring-health/recommendation-remove-unused-apps), Jason pulls the relevant data to investigate further or work with his team to improve their tenant security posture. The response includes links to specific apps for easier remediation. The analyst can also ask about a specific app's details directly in Security Copilot.

Note

The Copilot response returns a list of app registration or applications that are unused in past 90 days, which haven't been issued any tokens in that timeframe.

He uses the following prompts to get the information he needs:

- *Show me unused apps.*
- *How many unused apps do I have?*

### Explore Microsoft Entra applications or service principals with expiring credentials

Jason sees another opportunity to renew an application credentials prior to their expiry date to maintain uninterrupted operations and minimizing the risk of any downtime resulting from outdated credentials. Application and service principal credentials can include certificates and other types of secrets that need to be registered with that application or service principal. These credentials are used to prove the identity of the application or service principal.

Using the Copilot prompts integrated with the existing [Microsoft Entra recommendation for renew expiring app credential](../identity/monitoring-health/recommendation-renew-expiring-application-credential) and [Microsoft Entra recommendation for renew expiring service principal credential](../identity/monitoring-health/recommendation-renew-expiring-service-principal-credential), Jason pulls the relevant data to reduce the outage risk from expiring credentials and update or rotate them as needed. The response includes links to specific apps for easier remediation. The analyst can also ask about a specific app's details directly in Security Copilot.

Note

The Copilot response returns a list of applications or service principals that have credentials on them expiring within the next 30 days. The following credentials are exempted from this recommendation:

- Credentials that were identified as expiring but have since been removed from the application registration.
- Credentials whose expiration date has lapsed show as **completed** in the list of **Impacted resources**.

He uses the following prompts to get the information he needs:

- *Which enterprise applications have credentials about to expire?*
- *Show me service principals with credentials that are expiring soon.*
- *Show me applications with credentials that are expiring soon.*

### Explore Microsoft Entra Applications outside my tenant

Jason would also like to look into the risk factor of external apps or multitenant apps with a presence in his tenant that are registered in another organization's tenant. Since the security posture of these apps is impacted by the posture of the owning tenant, it's especially important to review these to identify risks and opportunities for surface area reduction. Copilot can return a list of service principals within the current tenant with a multitenant app registration outside of the user's tenant or details on if a particular service principal is registered outside the tenant.

He uses the following prompts to get the information he needs:

- *Show me apps outside my tenant.*
- *How many apps are from outside my tenant?*

## Remediate

By using Security Copilot, Jason is able to gather comprehensive risk and basic information about the applications and service principals in their Microsoft Entra tenant. After Jason completes his assessment, he takes action to remediate the risky applications. Security Copilot surfaces links to the Microsoft Entra admin center in responses for administrators to take the appropriate remediation actions.

He reads about [managing access and security for applications](../identity/enterprise-apps/tutorial-manage-access-security), [security workload identities](../id-protection/concept-workload-identity-risk), [protecting against consent phishing](../identity/enterprise-apps/protect-against-consent-phishing), and [response playbooks](/en-us/security/operations/incident-response-playbook-compromised-malicious-app) to determine possible actions to take next.