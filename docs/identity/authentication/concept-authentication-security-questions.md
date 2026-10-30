---
layout: Conceptual
title: Security questions authentication method - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-security-questions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: Learn about using security questions in Microsoft Entra ID to help improve and secure sign-in events
ms.topic: concept-article
ms.date: 2026-02-18T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 433cd718-6243-a9ae-9d23-af3c7b6f97e3
document_version_independent_id: 036d02cf-ddea-979f-2ecd-7dcb25647b73
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/concept-authentication-security-questions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/concept-authentication-security-questions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/concept-authentication-security-questions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fa43931d-fae2-b0fa-b0e9-882803f4daa7
---

# Security questions authentication method - Microsoft Entra ID | Microsoft Learn

Security questions aren't used as an authentication method during a sign-in event. Instead, security questions can be used during the self-service password reset (SSPR) process to confirm who you are. Administrator accounts can't use security questions as verification method with SSPR.

Warning

**Security questions will be retired for Self‑Service Password Reset (SSPR) in March 2027.** After that date, users will no longer be able to reset passwords using security questions. Ensure users are set up with [supported authentication methods](tutorial-enable-sspr#select-authentication-methods-and-registration-options) in the Authentication methods policy.

This feature is being deprecated due to security risks and low reliability. Security questions are often guessable or susceptible to social engineering, increasing the risk of account takeover during SSPR. Stronger verification methods improve security and reduce reset failures and support escalations.

Prepare in advance to avoid user lockouts, helpdesk escalations, and failed password reset experiences once enforcement begins in March 2027.

When users register for SSPR, they're prompted to choose the authentication methods to use. If they choose to use security questions, they pick from a set of questions to prompt for and then provide their own answers.

![Screenshot of the Microsoft Entra admin center that shows authentication methods and options for security questions](media/concept-authentication-methods/security-questions-authentication-method.png)

Note

Security questions are stored privately and securely on a user object in the directory and can only be answered by users during registration. There's no way for an administrator to read or modify a user's questions or answers.

Security questions can be less secure than other methods because some people might know the answers to another user's questions. If you use security questions with SSPR, it's recommended to use them in along with another method. A user can be prompted to use the Microsoft Authenticator App or phone authentication to verify their identity during the SSPR process, and choose security questions only if they don't have their phone or registered device with them.

## Predefined questions

The following predefined security questions are available for use as a verification method with SSPR. All of these security questions are translated and localized into the full set of Microsoft 365 languages based on the user's browser locale:

- In what city did you meet your first spouse/partner?
- In what city did your parents meet?
- In what city does your nearest sibling live?
- In what city was your father born?
- In what city was your first job?
- In what city was your mother born?
- What city were you in on New Year's 2000?
- What is the last name of your favorite teacher in high school?
- What is the name of a college you applied to but didn't attend?
- What is the name of the place in which you held your first wedding reception?
- What is your father's middle name?
- What is your favorite food?
- What is your maternal grandmother's first and last name?
- What is your mother's middle name?
- What is your oldest sibling's birthday month and year? (for example, November 1985)
- What is your oldest sibling's middle name?
- What is your paternal grandfather's first and last name?
- What is your youngest sibling's middle name?
- What school did you attend for sixth grade?
- What was the first and last name of your childhood best friend?
- What was the first and last name of your first significant other?
- What was the last name of your favorite grade school teacher?
- What was the make and model of your first car or motorcycle?
- What was the name of the first school you attended?
- What was the name of the hospital in which you were born?
- What was the name of the street of your first childhood home?
- What was the name of your childhood hero?
- What was the name of your favorite stuffed animal?
- What was the name of your first pet?
- What was your childhood nickname?
- What was your favorite sport in high school?
- What was your first job?
- What were the last four digits of your childhood telephone number?
- When you were young, what did you want to be when you grew up?
- Who is the most famous person you have ever met?

## Custom security questions

For additional flexibility, you can define your own custom security questions. The maximum length of a custom security question is 200 characters.

Custom security questions aren't automatically localized like with the default security questions. All custom questions are displayed in the same language as they're entered in the administrative user interface, even if the user's browser locale is different. If you need localized questions, you should use the predefined questions.

## Security question requirements

For both default and custom security questions, the following requirements and limitations apply:

- The minimum answer character limit is three characters.
- The maximum answer character limit is 40 characters.
- Users can't answer the same question more than one time.
- Users can't provide the same answer to more than one question.
- Any character set can be used to define the questions and the answers, including Unicode characters.
- The number of questions defined must be greater than or equal to the number of questions that were required to register.