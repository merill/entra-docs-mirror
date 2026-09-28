---
layout: Conceptual
title: Workload identities - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/workload-identities-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Understand the concepts and supported scenarios for using workload identity in Microsoft Entra.
ms.topic: overview
ms.date: 2026-05-08T00:00:00.0000000Z
ms.reviewer: arluca, ilanas, hosamsh
ms.custom: aaddev
locale: en-us
document_id: 4d9de149-e0b9-bb06-cb00-b6c178e8c053
document_version_independent_id: a001ee9e-85da-ed3a-4de9-8945b3336ced
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/workload-identities-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/workload-identities-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/workload-identities-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
platformId: 1c60d93a-2bbf-7c20-9865-c3de353acde0
---

# Workload identities - Microsoft Entra Workload ID | Microsoft Learn

A workload identity is an identity you assign to a software workload (such as an application, service, script, or container) to authenticate and access other services and resources. The terminology is inconsistent across the industry, but generally a workload identity is something you need for your software entity to authenticate with some system. For example, in order for GitHub Actions to access Azure subscriptions the action needs a workload identity which has access to those subscriptions. A workload identity could also be an AWS service role attached to an EC2 instance with read-only access to an Amazon S3 bucket.

In Microsoft Entra, workload identities are applications, service principals, and managed identities.

An [application](../identity-platform/app-objects-and-service-principals?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json) is an abstract entity, or template, defined by its application object. The application object is the *global* representation of your application for use across all tenants. The application object describes how tokens are issued, the resources the application needs to access, and the actions that the application can take.

A [service principal](../identity-platform/app-objects-and-service-principals?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json) is the *local* representation, or application instance, of a global application object in a specific tenant. An application object is used as a template to create a service principal object in every tenant where the application is used. The service principal object defines what the app can actually do in a specific tenant, who can access the app, and what resources the app can access.

A [managed identity](../identity/managed-identities-azure-resources/overview?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json) is a special type of service principal that eliminates the need for developers to manage credentials.

Here are some ways that workload identities in Microsoft Entra ID are used:

- An app that enables a web app to access Microsoft Graph based on admin or user consent. This access could be either on behalf of the user or on behalf of the application.
- A managed identity used by a developer to provision their service with access to an Azure resource such as Azure Key Vault or Azure Storage.
- A service principal used by a developer to enable a CI/CD pipeline to deploy a web app from GitHub to Azure App Service.

## Workload identities, other machine identities, and human identities

At a high level, there are two types of identities: human and machine/non-human identities. Workload identities and device identities together make up a group called machine (or non-human) identities. Workload identities represent software workloads while device identities represent devices such as desktop computers, mobile, IoT sensors, and IoT managed devices. Machine identities are distinct from human identities, which represent people such as employees (internal workers and front line workers) and external users (customers, consultants, vendors, and partners).

![Diagram that shows different types of machine and human identities.](media/workload-identities-overview/identity-types.svg)

## Need for securing workload identities

More and more, solutions are reliant on non-human entities to complete vital tasks and the number of non-human identities is increasing dramatically. Recent cyber attacks show that adversaries are increasingly targeting non-human identities over human identities.

Human users typically have a single identity used to access a broad range of resources. Unlike a human user, a software workload may deal with multiple credentials to access different resources and those credentials need to be stored securely. It’s also hard to track when a workload identity is created or when it should be revoked. Enterprises risk their applications or services being exploited or breached because of difficulties in securing workload identities.

![Diagram that shows pain points in securing workload identities.](media/workload-identities-overview/pain-points.png)

Most identity and access management solutions on the market today are focused only on securing human identities and not workload identities. Microsoft Entra Workload ID helps resolve these issues when securing workload identities.

## Key scenarios

Here are some ways you can use workload identities.

Secure access with adaptive policies:

- Apply Conditional Access policies to service principals owned by your organization using [Conditional Access for workload identities](../identity/conditional-access/workload-identity?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json).
- Enable real-time enforcement of Conditional Access location and risk policies using [Continuous access evaluation for workload identities](../identity/conditional-access/concept-continuous-access-evaluation-workload?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json).
- Manage [custom security attributes for an app](../identity/enterprise-apps/custom-security-attributes-apps?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json)

Intelligently detect compromised identities:

- Detect risks (like leaked credentials), contain threats, and reduce risk to workload identities using [Microsoft Entra ID Protection](../id-protection/concept-workload-identity-risk?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json).

Simplify lifecycle management:

- Access Microsoft Entra protected resources without needing to manage secrets for workloads that run on Azure using [managed identities](../identity/managed-identities-azure-resources/overview?toc=/azure/active-directory/workload-identities?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json).
- Access Microsoft Entra protected resources without needing to manage secrets using [workload identity federation](workload-identity-federation) for supported scenarios such as GitHub Actions, workloads running on Kubernetes, or workloads running in compute platforms outside of Azure.
- Review service principals and applications that are assigned to privileged directory roles in Microsoft Entra ID using [access reviews for service principals](../id-governance/privileged-identity-management/pim-create-roles-and-resource-roles-review?toc=/azure/active-directory/workload-identities/toc.json&amp;bc=/azure/active-directory/workload-identities/breadcrumb/toc.json).

## Agent identities for AI workloads

AI agents — autonomous software systems that reason, make decisions, and take actions on behalf of users or organizations — represent a distinct category of machine identity with unique security requirements. Unlike traditional workloads that execute predetermined logic, AI agents make dynamic decisions and adapt behavior, which requires purpose-built identity constructs with stronger governance controls.

[Microsoft Entra Agent ID](../agent-id/what-is-microsoft-entra-agent-id) provides these constructs through agent identities. Agent identities offer enforced human sponsorship, lifecycle governance from provisioning through deactivation, and at-scale management that apply centralized security policies across all agent instances of a given type. For more information, see [Microsoft Entra security for AI overview](../agent-id/security-for-ai-overview).