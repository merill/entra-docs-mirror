---
layout: Conceptual
title: Azure Active Directory B2C deployment plans - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/b2c-deployment-plans
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Azure Active Directory B2C deployment guide for planning, implementation, and monitoring
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.reviewer: gasinh
ms.subservice: architecture
locale: en-us
document_id: 9a2a1e7b-4ccd-02da-03a6-0d5967452aa8
document_version_independent_id: 15eb0bec-4438-a03b-768e-308b79f87baf
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/b2c-deployment-plans.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/b2c-deployment-plans
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/b2c-deployment-plans.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: e3c6b97b-49b7-b036-cbcd-1d70dbc0cb67
---

# Azure Active Directory B2C deployment plans - Microsoft Entra | Microsoft Learn

Important

Effective May 1, 2025, Azure Active Directory B2C (Azure AD B2C) is no longer available for new customers to purchase. To learn more, see [Is Azure AD B2C still available to purchase?](/en-us/azure/active-directory-b2c/faq?tabs=app-reg-ga#azure-ad-b2c-end-of-sale) in our FAQ.

Azure Active Directory B2C (Azure AD B2C) is an identity and access management solution that can ease integration with your infrastructure. Use the following guidance to help understand requirements and compliance throughout an Azure AD B2C deployment.

## Plan an Azure AD B2C deployment

### Requirements

- Assess the primary reason to turn off systems
    - See, [What is Azure Active Directory B2C?](/en-us/azure/active-directory-b2c/overview)
- For a new application, plan the design of the Customer Identity Access Management (CIAM) system
    - See, [Planning and design](/en-us/azure/active-directory-b2c/best-practices#planning-and-design)
- Identify customer locations and create a tenant in the corresponding datacenter
    - See, [Tutorial: Create an Azure Active Directory B2C tenant](/en-us/azure/active-directory-b2c/tutorial-create-tenant)
- Confirm your application types and supported technologies:
    - [Overview of the Microsoft Authentication Library (MSAL)](../identity-platform/msal-overview)
    - [Develop with open-source languages, frameworks, databases, and tools in Azure](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
    - For back-end services, use the [client credentials](../identity-platform/msal-authentication-flows#client-credentials) flow
- To migrate from an identity provider (IdP):
    - [Seamless migration](/en-us/azure/active-directory-b2c/user-migration#seamless-migration)
    - Go to [`user-migration`](https://github.com/azure-ad-b2c/user-migration)
- Select protocols
    - If you use Kerberos, Microsoft Windows NT LAN Manager (NTLM), and Web Services Federation (WS-Fed), see the video, [Application and identity migration to Azure AD B2C](https://www.bing.com/videos/search?q=application+migration+in+azure+ad+b2c&amp;docid=608034225244808069&amp;mid=E21B87D02347A8260128E21B87D02347A8260128&amp;view=detail&amp;FORM=VIRE)

After migration, your applications can support modern identity protocols such as Open Authorization (OAuth) 2.0 and OpenID Connect (OIDC).

### Stakeholders

Technology project success depends on managing expectations, outcomes, and responsibilities.

- Identify the application architect, technical program manager, and owner
- Create a distribution list (DL) to communicate with the Microsoft account or engineering teams
    - Ask questions, get answers, and receive notifications
- Identify a partner or resource outside your organization to support you

Learn more: [Include the right stakeholders](deployment-plans)

### Communications

Communicate proactively and regularly with your users about pending and current changes. Inform them about how the experience changes, when it changes, and provide a contact for support.

### Timelines

Help set realistic expectations and make contingency plans to meet key milestones:

- Pilot date
- Launch date
- Dates that affect delivery
- Dependencies

## Implement an Azure AD B2C deployment

- **Deploy applications and user identities** - Deploy client application and migrate user identities
- **Client application onboarding and deliverables** - Onboard the client application and test the solution
- **Security** - Enhance the identity solution security
- **Compliance** - Address regulatory requirements
- **User experience** - Enable a user-friendly service

### Deploy authentication and authorization

- Before your applications interact with Azure AD B2C, register them in a tenant you manage
    - See, [Tutorial: Create an Azure Active Directory B2C tenant](/en-us/azure/active-directory-b2c/tutorial-create-tenant)
- For authorization, use the Identity Experience Framework (IEF) sample user journeys
    - See, [Azure Active Directory B2C: Custom CIAM User Journeys](https://github.com/azure-ad-b2c/samples#local-account-policy-enhancements)
- Use policy-based control for cloud-native environments
    - Go to `openpolicyagent.org` to learn about [Open Policy Agent (OPA)](https://www.openpolicyagent.org/)

Learn more with the Microsoft Identity PDF, [Gaining expertise with Azure AD B2C](https://aka.ms/learnaadb2c), a course for developers.

### Checklist for personas, permissions, delegation, and calls

- Identify the personas that access to your application
- Define how you manage system permissions and entitlements today, and in the future
- Confirm you have a permission store and if there are permissions to add to the directory
- Define how you manage delegated administration
    - For example, your customers' customers management
- Verify your application calls an API Manager (APIM)
    - There might be a need to call from the IdP before the application is issued a token

### Deploy applications and user identities

Azure AD B2C projects start with one or more client applications.

- The [new App registrations experience for Azure Active Directory B2C](/en-us/azure/active-directory-b2c/app-registrations-training-guide)
    - Refer to [Azure Active Directory B2C code samples](/en-us/azure/active-directory-b2c/integrate-with-app-code-samples) for implementation
- Set up your user journey based on custom user flows
    - [Comparing user flows and custom policies](/en-us/azure/active-directory-b2c/user-flow-overview#comparing-user-flows-and-custom-policies)
    - [Add an identity provider to your Azure Active Directory B2C tenant](/en-us/azure/active-directory-b2c/add-identity-provider)
    - [Migrate users to Azure AD B2C](/en-us/azure/active-directory-b2c/user-migration)
    - [Azure Active Directory B2C: Custom CIAM User Journeys](https://github.com/azure-ad-b2c/samples) for advanced scenarios

### Application deployment checklist

- Applications included in the CIAM deployment
- Applications in use
    - For example, web applications, APIs, single-page web apps (SPAs), or native mobile applications
- Authentication in use:
    - For example, forms federated with Security Assertion Markup Language (SAML), or federated with OIDC
    - If OIDC, confirm the response type: code or id\_token
- Determine where front-end and back-end applications are hosted: on-premises, cloud, or hybrid-cloud
- Confirm the platforms or languages in use:
    - For example ASP.NET, Java, and Node.js
    - See, [Quickstart: Set up sign in for an ASP.NET application using Azure AD B2C](/en-us/azure/active-directory-b2c/quickstart-web-app-dotnet)
- Verify where user attributes are stored
    - For example, Lightweight Directory Access Protocol (LDAP) or databases

### User identity deployment checklist

- Confirm the number of users accessing applications
- Determine the IdP types needed:
    - For example, Facebook, local account, and Active Directory Federation Services (AD FS)
    - See, [Active Directory Federation Services](/en-us/windows-server/identity/ad-fs/ad-fs-overview)
- Outline the claim schema required from your application, Azure AD B2C, and IdPs if applicable
    - See, [ClaimsSchema](/en-us/azure/active-directory-b2c/claimsschema)
- Determine the information to collect during sign-in and sign-up
    - [Set up a sign-up and sign-in flow in Azure Active Directory B2C](/en-us/azure/active-directory-b2c/add-sign-up-and-sign-in-policy?pivots=b2c-user-flow)

### Client application onboarding and deliverables

Use the following checklist for onboarding an application

| Area | Description |
| --- | --- |
| Application target user group | Select among end customers, business customers, or a digital service. Determine a need for employee sign-in. |
| Application business value | Understand the business need or goal to determine the best Azure AD B2C solution and integration with other client applications. |
| Your identity groups | Cluster identities into groups with requirements, such as business-to-consumer (B2C), business-to-business (B2B) business-to-employee (B2E), and business-to-machine (B2M) for IoT device sign-in and service accounts. |
| Identity provider (IdP) | See, [Select an identity provider](/en-us/azure/active-directory-b2c/add-identity-provider#select-an-identity-provider). For example, for a customer-to-customer (C2C) mobile app use an easy sign-in process. B2C with digital services has compliance requirements. Consider email sign-in. |
| Regulatory constraints | Determine a need for remote profiles or privacy policies. |
| Sign-in and sign-up flow | Confirm email verification or email verification during sign-up. For check-out processes, see [How it works: Microsoft Entra multifactor authentication](../identity/authentication/concept-mfa-howitworks). See the video [Azure AD B2C user migration using Microsoft Graph API](https://www.youtube.com/watch?v=c8rN1ZaR7wk&amp;list=PL3ZTgFEc7LyuJ8YRSGXBUVItCPnQz3YX0&amp;index=4). |
| Application and authentication protocol | Implement client applications such as Web application, single-page application (SPA), or native. Authentication protocols for client application and Azure AD B2C: OAuth, OIDC, and SAML. See the video [Protecting Web APIs with Microsoft Entra ID](https://www.youtube.com/watch?v=r2TIVBCm7v4&amp;list=PL3ZTgFEc7LyuJ8YRSGXBUVItCPnQz3YX0&amp;index=9). |
| User migration | Confirm if you'll [migrate users to Azure AD B2C](/en-us/azure/active-directory-b2c/user-migration): Just-in-time (JIT) migration and bulk import/export. See the video [Azure AD B2C user migration strategies](https://www.youtube.com/watch?v=lCWR6PGUgz0&amp;list=PL3ZTgFEc7LyuJ8YRSGXBUVItCPnQz3YX0&amp;index=2). |

Use the following checklist for delivery.

| Area | Description |
| --- | --- |
| Protocol information | Gather the base path, policies, and metadata URL of both variants. Specify attributes such as sample sign-in, client application ID, secrets, and redirects. |
| Application samples | See, [Azure Active Directory B2C code samples](/en-us/azure/active-directory-b2c/integrate-with-app-code-samples). |
| Penetration testing | Inform your operations team about pen tests, then test user flows including the OAuth implementation. See, [Penetration testing](/en-us/azure/security/fundamentals/pen-testing) and [Penetration testing rules of engagement](https://www.microsoft.com/msrc/pentest-rules-of-engagement). |
| Unit testing | Unit test and generate tokens. See, [Microsoft identity platform and OAuth 2.0 Resource Owner Password Credentials](../identity-platform/v2-oauth-ropc). If you reach the Azure AD B2C token limit, see [Azure AD B2C: File Support Requests](/en-us/azure/active-directory-b2c/find-help-open-support-ticket). Reuse tokens to reduce investigation on your infrastructure. [Set up a resource owner password credentials flow in Azure Active Directory B2C](/en-us/azure/active-directory-b2c/add-ropc-policy?pivots=b2c-user-flow&amp;tabs=app-reg-ga). You shouldn't use ROPC flow to authenticate users in your apps. |
| Load testing | Learn about [Azure AD B2C service limits and restrictions](/en-us/azure/active-directory-b2c/service-limits). Calculate the expected authentications and user sign-ins per month. Assess high load traffic durations and business reasons: holiday, migration, and event. Determine expected peak rates for sign-up, traffic, and geographic distribution, for example per second. |

### Security

Use the following checklist to enhance application security.

- Authentication method, such as multifactor authentication:
    - Multifactor authentication is recommended for users that trigger high-value transactions or other risk events. For example, banking, finance, and check-out processes.
    - See, [What authentication and verification methods are available in Microsoft Entra ID?](../identity/authentication/overview-authentication)
- Confirm use of anti-bot mechanisms
- Assess the risk of attempts to create a fraudulent account or sign-in
    - See, [Tutorial: Configure Microsoft Dynamics 365 Fraud Protection with Azure Active Directory B2C](/en-us/azure/active-directory-b2c/partner-dynamics-365-fraud-protection)
- Confirm needed conditional postures as part of sign-in or sign-up

#### Conditional Access and Microsoft Entra ID Protection

- The modern security perimeter now extends beyond an organization's network. The perimeter includes user and device identity.
    - See, [What is Conditional Access?](../identity/conditional-access/overview)
- Enhance the security of Azure AD B2C with Microsoft Entra ID Protection
    - See, [ID Protection and Conditional Access in Azure AD B2C](/en-us/azure/active-directory-b2c/conditional-access-identity-protection-overview)

### Compliance

To help comply with regulatory requirements and enhance back-end system security you can use virtual networks (VNets), IP restrictions, Web Application Firewall, and so on. Consider the following requirements:

- Your regulatory compliance requirements
    - For example, Payment Card Industry Data Security Standard (PCI DSS)
    - Go to pcisecuritystandards.org to learn more about the [PCI Security Standards Council](https://www.pcisecuritystandards.org/)
- Data storage into a separate database store
    - Determine whether this information can't be written into the directory

### User experience

Use the following checklist to help define user experience requirements.

- Identify integrations to extend CIAM capabilities and build seamless end-user experiences
    - [Azure Active Directory B2C independent software vendor (ISV) partners](/en-us/azure/active-directory-b2c/partner-gallery)
- Use screenshots and user stories to show the application end-user experience
    - For example, screenshots of sign-in, sign-up, sign-up/sign-in (SUSI), profile edit, and password reset
- Look for hints passed through by using query string parameters in your CIAM solution
- For high user experience customization, consider a using front-end developer
- In Azure AD B2C, you can customize HTML and CSS
    - See, [Guidelines for using JavaScript](/en-us/azure/active-directory-b2c/javascript-and-page-layout?pivots=b2c-custom-policy#guidelines-for-using-javascript)
- Implement an embedded experience by using iframe support:
    - See, [Embedded sign-up or sign-in experience](/en-us/azure/active-directory-b2c/embedded-login?pivots=b2c-custom-policy)
    - For a single-page application, use a second sign-in HTML page that loads into the `<iframe>` element

## Monitoring auditing, and logging

Use the following checklist for monitoring, auditing, and logging.

- Monitoring
    - [Monitor Azure AD B2C with Azure Monitor](/en-us/azure/active-directory-b2c/azure-monitor)
    - See the video [Monitoring and reporting Azure AD B2C using Azure Monitor](https://www.youtube.com/watch?v=Mu9GQy-CbXI&amp;list=PL3ZTgFEc7LyuJ8YRSGXBUVItCPnQz3YX0&amp;index=1)
- Auditing and logging
    - [Accessing Azure AD B2C audit logs](/en-us/azure/active-directory-b2c/view-audit-logs)

## Resources

- [Register a Microsoft Graph application](/en-us/azure/active-directory-b2c/microsoft-graph-get-started)
- [Manage Azure AD B2C with Microsoft Graph](/en-us/azure/active-directory-b2c/microsoft-graph-operations)
- [Deploy custom policies with Azure Pipelines](/en-us/azure/active-directory-b2c/deploy-custom-policies-devops)
- [Manage Azure AD B2C custom policies with Azure PowerShell](/en-us/azure/active-directory-b2c/manage-custom-policies-powershell)