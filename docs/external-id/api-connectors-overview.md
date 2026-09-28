---
layout: Conceptual
title: About API connectors in self-service sign-up flows - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/api-connectors-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Use Microsoft Entra API connectors to customize and extend your self-service sign-up user flows by using web APIs.
ms.topic: concept-article
ms.date: 2026-04-17T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: d77e3d80-069d-25a3-439f-f8cce48cccab
document_version_independent_id: b3f802de-92d5-a29f-6479-79e2f4e736af
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/api-connectors-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/api-connectors-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/api-connectors-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: be242f36-2a8e-2e12-beba-af667128ed04
---

# About API connectors in self-service sign-up flows - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

## Overview

As a developer or IT administrator, you can use [API connectors](self-service-sign-up-add-api-connector#create-an-api-connector) to integrate your [self-service sign-up user flows](self-service-sign-up-overview) with web APIs to customize the sign-up experience and integrate with external systems. For example, with API connectors, you can:

- [**Integrate with a custom approval workflow**](self-service-sign-up-add-approvals). Connect to a custom approval system for managing and limiting account creation.
- [**Perform identity verification**](code-samples-self-service-sign-up#identity-verification). Use an identity verification service to add an extra level of security to account creation decisions.
- **Validate user input data**. Validate against malformed or invalid user data. For example, you can validate user-provided data against existing data in an external data store or list of permitted values. If invalid, you can ask a user to provide valid data or block the user from continuing the sign-up flow.
- **Overwrite user attributes**. Reformat or assign a value to an attribute collected from the user. For example, if a user enters the first name in all lowercase or all uppercase letters, you can format the name with only the first letter capitalized.
- **Run custom business logic**. You can trigger downstream events in your cloud systems to send push notifications, update corporate databases, manage permissions, audit databases, and perform other custom actions.

An API connector provides Microsoft Entra ID with the information needed to call an API endpoint by defining the HTTP endpoint URL and authentication for the API call. Once you configure an API connector, you can enable it for a specific step in a user flow. When a user reaches that step in the sign-up flow, the API connector is invoked and sent as an HTTP POST request to your API, with user information (claims) as key-value pairs in a JSON body. The API response can affect user flow execution. For example, the API response can block a user from signing up, ask the user to reenter information, or overwrite and append user attributes.

## Where you can enable an API connector in a user flow

There are two places in a user flow where you can enable an API connector:

- After federating with an identity provider during sign-up
- Before creating the user

Important

In both of these cases, the API connectors are invoked during user **sign-up**, not sign-in.

### After federating with an identity provider during sign-up

An API connector at this step in the sign-up process is invoked immediately after the user authenticates with an identity provider (for example, Google, Facebook, and Microsoft Entra ID). This step precedes the [attribute collection page](self-service-sign-up-user-flow#select-the-layout-of-the-attribute-collection-form), which is the form presented to the user to collect user attributes. This step isn't invoked if a user is registering with a local account. The following are examples of API connector scenarios you might enable at this step:

- Use the email or federated identity that the user provided to look up claims in an existing system. Return these claims from the existing system, prefill the attribute collection page, and make them available to return in the token.
- Implement an allow or blocklist based on social identity.

### Before creating the user

An API connector at this step in the sign-up process is invoked after the attribute collection page, if one is included. This step is always invoked before a user account is created. The following are examples of scenarios you might enable at this point during sign-up:

- Validate user input data and ask a user to resubmit data.
- Block a user sign-up based on data entered by the user.
- Perform identity verification.
- Query external systems for existing data about the user to return it in the application token or store it in Microsoft Entra ID.