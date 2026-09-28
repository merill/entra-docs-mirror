---
layout: Conceptual
title: Review recommendations for Access reviews - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/review-recommendations-access-reviews
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Learn how to review access of group members with review recommendations in Microsoft Entra access reviews.
editor: markwahl-msft
ms.subservice: access-reviews
ms.topic: how-to
ms.date: 2026-03-12T00:00:00.0000000Z
ms.reviewer: mwahl
locale: en-us
document_id: 3c7365b9-3554-3d24-f607-2be3b0e43b82
document_version_independent_id: c782bdfc-2a5e-8bea-aff0-9d0c8e7efbeb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/review-recommendations-access-reviews.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/review-recommendations-access-reviews
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/review-recommendations-access-reviews.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ebf95d8c-a7ad-d7b5-75fd-f292a412e744
---

# Review recommendations for Access reviews - Microsoft Entra ID Governance | Microsoft Learn

Decision makers who review users' access and perform access reviews can use system based recommendations to help them decide whether to continue their access or deny their access to resources. For more information about how to use review recommendations, see [Enable decision helpers](create-access-review#next-settings).

## Prerequisites

Creating a review with user-to-group affiliation recommendation requires a Microsoft Entra ID Governance license.

For more information, see [License requirements](access-reviews-overview#license-requirements).

## Inactive user recommendations

A user is considered 'inactive' if they haven't signed into the tenant within the last 30 days. This behavior is adjusted for reviews of application assignments, which check each user's last activity in the app as opposed to the entire tenant. When inactive user recommendations are enabled for an access review, the last sign-in date for each user is evaluated once the review starts, and any user that hasn't signed in within 30 days is given a recommended action of Deny. Additionally, when these decision helpers are enabled, reviewers are able to see the last sign-in date for all users being reviewed. This sign-in date, and the resulting recommendation, is determined when the review begins and isn't updated while the review is in-progress.

## User-to-Group Affiliation

An easier and more accurate review experience empowers IT admins and reviewers to make more informed decisions. This Machine Learning based recommendation opens the journey to automate access reviews, which enable intelligent automation, and reduces access rights attestation fatigue.

User-to-Group Affiliation is defined as two or more users who share similar characteristics in an organization's reporting structure.

This recommendation detects user affiliation with other users within the group, based on organization's reporting-structure similarity. The recommendation relies on a scoring mechanism, which is calculated by computing the user’s average distance from the remaining users in the group. Users who are distant from all the other group members based on their organization's chart, are considered to have "low affiliation" within the group.

If the creator of the access review enables the decision helper, reviewers can receive User-to-Group Affiliation recommendations for group access reviews.

Note

This feature is only available for users in your directory. A user should have a manager attribute and should be a part of an organizational hierarchy for the User-to-Group Affiliation to work.

Groups with more than 600 users aren't supported.

The following image has an example of an organization's reporting structure in a cosmetics company:

[![Screenshot of an org example chart for access reviews.](media/review-recommendations-group-access-reviews/org-chart-example.png)](media/review-recommendations-group-access-reviews/org-chart-example.png#lightbox)

Based on the reporting structure in the example image, users who are a statistically significant distance away from other users within the group, would get a "*Deny*" recommendation by the system if the User-to-Group Affiliation recommendation was selected by the reviewer for group access reviews.

For example, Phil who works within the Personal care division is in a group with Debby, Irwin, and Emily who all work within the Cosmetics division. The group is called *Fresh Skin*. If an Access Review for the group Fresh Skin is performed, based on the reporting structure and distance away from the other group members, Phil would be considered to have low affiliation. The system creates a **Deny** recommendation in the group access review.