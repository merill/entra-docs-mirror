---
layout: Conceptual
title: Onboard new remote employees using ID verification - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/remote-onboarding-new-employees-id-verification
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: A design pattern describing how to onboard new employees remotely
services: decentralized-identity
ms.topic: concept-article
ms.date: 2024-12-17T00:00:00.0000000Z
locale: en-us
document_id: 90f88ff8-d746-b817-9796-d63901893af3
document_version_independent_id: 4c244c82-2fb5-9716-14e5-46fe46141cd1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/remote-onboarding-new-employees-id-verification.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/remote-onboarding-new-employees-id-verification
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/remote-onboarding-new-employees-id-verification.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19011fa1-e010-495a-a1ea-74b88af5b9b1
- https://authoring-docs-microsoft.poolparty.biz/devrel/2624a017-7337-44fa-9494-a407bb0e59fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3dc5b4eb-8015-403d-9d1b-ae51b20067fe
- https://authoring-docs-microsoft.poolparty.biz/devrel/a438284e-c3c3-4c36-ab0b-aa7c244b912c
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: eb1fec8b-c926-c2f2-e225-3ba5fb8c4bf0
---

# Onboard new remote employees using ID verification - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Enterprises onboarding users face significant challenges onboarding remote users who aren't yet inside the trust boundary. Microsoft Entra Verified ID can help customers facing these scenarios because it can use government-issued, ID-based attestations as a way to establish trust.

## When to use this pattern

- You have a modern Human resources (HR) system with API support.
- Your HR system allows programmatic integration to query the HR system to perform accurate user profile matching.
- Your organization is in the process of adopting passwordless technologies.

## Solution

1. A custom portal for new employee onboarding.
2. A backend job provides new hires with a uniquely identifiable link to the employee onboarding portal from (A) that represents the new hire’s specific process. For this use case, the account for the new hire should already be provisioned in Microsoft Entra ID. Consider using [Lifecycle Workflows](../id-governance/what-are-lifecycle-workflows) as the triggering point of this flow.
3. New hires select the link to the portal in (A) and are guided through a wizard-like experience:

    1. New hires are redirected to acquire a verified ID from the identity verification partner. To learn more about the identity verification partners: https://aka.ms/verifiedidisv
    2. New hires present the Verified ID acquired in step 1.
    3. System receives the claims from the identity verification partner, performs the new hire user account lookup, and validates the information.
    4. System executes the onboarding logic to locate the Microsoft Entra account of the user, and [generate a temporary access pass using MS Graph](/en-us/graph/api/resources/temporaryaccesspassauthenticationmethod?view=graph-rest-1.0&amp;preserve-view=true).

    ![Diagram showing a high-level flow.](media/remote-onboarding-new-employees-id-verification/high-level-flow-diagram.png)

## Issues and considerations

- The link used to initiate the process needs to meet some criteria:
    - The link should be specific to each remote employee.
    - The link should be valid for only a short period of time.
    - It should become invalid after a user finishes going through the flow.
    - The link should be designed to correlate to a unique HR record identifier.
- A Microsoft Entra account should be precreated for every user. The account should be used as part of the site's request validation process.
- Administrators frequently deal with discrepancies between users' information held in a company's IT systems, like human resource applications or identity management solutions, and the information the users provide. For example, an employee might have "James" as their first name but their profile has their name as “Jim”. For those scenarios:
    - At the beginning of the HR process, candidates must use their name exactly as it appears in government-issued documents. Taking this approach simplifies validation logic.
    - Design validation logic to include attributes that are more likely to have an exact match against the HR system. Common attributes include street address, date of birth, nationality, national/regional identification number (if applicable), in addition to first and last name.
    - As a fallback, plan for human review to work through ambiguous/non-conclusive results. This process might include temporarily storing the attributes presented in the VC or a phone call with the user.
- Multinational organizations may need to work with different identity proofing partners based on the region of the user.
- Assume that the initial interaction between the user and the onboarding partner is untrusted. The onboarding portal should generate detailed logs for all requests processed that could be used for auditing purposes.