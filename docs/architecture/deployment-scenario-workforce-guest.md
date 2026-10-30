---
layout: Conceptual
title: Microsoft Entra Suite deployment scenario - Workforce and guest lifecycle - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/deployment-scenario-workforce-guest
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Configure Microsoft Entra Suite products for hiring new remote employees and providing them with secure and seamless access to apps and resources.
ms.reviewer: gasinh
ms.topic: concept-article
ms.date: 2024-06-13T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, sfi-image-nochange
ms.subservice: architecture
locale: en-us
document_id: fd3abaf0-2e52-17f3-b85f-e94cc277a202
document_version_independent_id: fd3abaf0-2e52-17f3-b85f-e94cc277a202
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/deployment-scenario-workforce-guest.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/deployment-scenario-workforce-guest
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/deployment-scenario-workforce-guest.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 0449c3b6-8d92-4541-ce5a-1bfe8836969a
---

# Microsoft Entra Suite deployment scenario - Workforce and guest lifecycle - Microsoft Entra | Microsoft Learn

The Microsoft Entra Suite deployment scenarios provide you with detailed guidance on how to combine and test these Microsoft Entra Suite products:

- [Microsoft Entra ID Protection](../id-protection/overview-identity-protection)
- [Microsoft Entra ID Governance](../id-governance/identity-governance-overview)
- [Microsoft Entra Verified ID (premium capabilities)](../verified-id/decentralized-identifier-overview)
- [Microsoft Entra Internet Access](../global-secure-access/concept-internet-access)
- [Microsoft Entra Private Access](../global-secure-access/concept-private-access)

In these guides, we describe scenarios that show the value of the Microsoft Entra Suite and how its capabilities work together.

- [Microsoft Entra deployment scenarios introduction](deployment-scenario-intro)
- [Microsoft Entra deployment scenario - Modernize remote access to on-premises apps with MFA per app](deployment-scenario-remote-access)
- [Microsoft Entra deployment scenario - Secure internet access based on business needs](deployment-scenario-internet-access)

## Scenario overview

In this guide, we describe how to configure Microsoft Entra Suite products for a scenario in which the fictional organization, Contoso, wants to hire new remote employees and provide them with secure and seamless access to necessary apps and resources. They want to invite and collaborate with external users (such as partners, vendors, or customers) and provide them with access to relevant apps and resources.

Contoso uses [Microsoft Entra Verified ID](../verified-id/decentralized-identifier-overview) to issue and verify digital proofs of identity and status for new remote employees (based on human resources data) and external users (based on email invitations). Digital wallets store identity proof and status to allow access to apps and resources. As an extra security measure, Contoso might verify identity with Face Check facial recognition based on the picture that the credential stores.

They use Microsoft Entra ID Governance to create and grant access packages for employees and external users based on verifiable credentials.

- For employees, they base access packages on job function and department. Access packages include cloud and on-premises apps and resources to which employees need access.
- For external collaborators, they base access packages on invitation to define external user roles and permissions. The access packages include only apps and resources to which external users need access.

Employees and external users can request access packages through a self-service portal where they provide digital proofs as identity verification. With single sign-on and multifactor authentication, employee and external user Microsoft Entra accounts provide access to apps and resources that their access packages include. Contoso verifies credentials and grants access packages without requiring manual approvals or provisioning.

Contoso uses Microsoft Entra ID Protection and Conditional Access to monitor and protect accounts from risky sign-ins and user behavior. They enforce appropriate access controls based on location, device, and risk level.

## Configure prerequisites

To successfully deploy and test the solution, configure the prerequisites that we describe in this section.

### Configure Microsoft Entra Verified ID

For this scenario, complete these prerequisite steps to configure Microsoft Entra Verified ID with Quick setup (Preview):

1. Register a custom domain (required for Quick setup) by following the steps in the [Add your custom domain](../fundamentals/add-custom-domain) article.
2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator).

    - Select **Verified ID**.
    - Select **Setup**.
    - Select **Get started**.
3. If you have multiple domains registered for your Microsoft Entra tenant, select the one that you would like to use for Verified ID.
4. After the setup process is complete, you see a default workplace credential available to edit and offer to employees of your tenant on their **My Account** page.

    [![Screenshot of Verified ID, Overview.](media/deployment-scenario-workforce-guest/verifiable-credentials-setup-complete-inline.png)](media/deployment-scenario-workforce-guest/verifiable-credentials-setup-complete-expanded.png#lightbox)
5. Sign in to the test user's **My Account** with their Microsoft Entra credentials. Select **Get my Verified ID** to issue a verified workplace credential.

    [![Screenshot of My Account, Overview with a red ellipse highlighting the Get my Verified ID control.](media/deployment-scenario-workforce-guest/verifiable-credentials-my-account-issue-inline.png)](media/deployment-scenario-workforce-guest/verifiable-credentials-my-account-issue-expanded.png#lightbox)

### Add trusted external organization (B2B)

Follow these prerequisite steps to add a trusted external organization (B2B) for the scenario.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator).
2. Browse to **Entra ID** &gt; **External Identities** &gt; **Cross-tenant access settings**. Select **Organizational settings**.
3. Select **Add organization**.
4. Enter the organization's full domain name (or tenant ID).
5. Select the organization in the search results. Select **Add**.
6. Confirm the new organization (that inherits its access settings from default settings) in **Organizational settings**.

    [![Screenshot of Organizational settings with red boxes highlighting Inherited from default in the Inbound access and Outbound access columns.](media/deployment-scenario-workforce-guest/org-specific-settings-inherited-inline.png)](media/deployment-scenario-workforce-guest/org-specific-settings-inherited-expanded.png#lightbox)

### Create catalog

Follow these steps to create an Entitlement management catalog for the scenario.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Catalogs**.
3. Select **+New catalog**.

    [![Screenshot of New access review, Enterprise applications, All applications, Identity Governance, New catalog.](media/deployment-scenario-workforce-guest/identity-governance-catalogs-inline.png)](media/deployment-scenario-workforce-guest/identity-governance-catalogs-expanded.png#lightbox)
4. Enter a unique name and description for the catalog . Requestors see this information in an access package's details.
5. To create access packages in this catalog only for internal users, select **Enabled for external users** &gt; **No**.

    ![Screenshot of New catalog with No selected for the Enabled for external users control.](media/deployment-scenario-workforce-guest/identity-governance-new-catalog.png)
6. On **Catalog**, open the catalog to which you want to add resources. Select **Resources** &gt; **+Add resources**.
7. Select **Type**, then **Groups and Teams**, **Applications**, or **SharePoint sites**.
8. Select one or more resources of the type that you want to add to the catalog. Select **Add**.

## Create access packages

To successfully deploy and test the solution, configure the access packages that we describe in this section.

### Access package for remote users (internal)

Follow these steps to create an access package in entitlement management with Verified ID for remote (internal) users.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. Select **New access package**.
4. For **Basics**, give the access package a name (such as *Finance Apps for Remote Users*). Specify the catalog that you previously created.
5. For **Resource roles**, select a resource type (for example: Groups and Teams, Applications, SharePoint sites). Select one or more resources.
6. In **Role**, select the role to which you want users assigned for each resource.

    [![Screenshot of Resources roles with a red box highlighting the Role column.](media/deployment-scenario-workforce-guest/resource-roles-inline.png)](media/deployment-scenario-workforce-guest/resource-roles.png#lightbox)
7. For **Requests**, select **For users in your directory**.
8. In **Select users and groups**, select **For Users in your directory**. Select **+ Add users and groups**. Select an existing group entitled to request the access package.
9. Scroll to **Required Verified Ids**.
10. Select **+ Add issuer**. Select an issuer from the Microsoft Entra Verified ID network. Ensure that you select an issuer from an existing verified identity in the guest wallet.
11. **Optional:** In **Approval**, specify whether users require approval when they request the access package.
12. **Optional:** In **Requestor information**, select **Questions**. Enter a question (known as the display string) that you want to ask the requestor. To add localization options, select **Add localization**.
13. For **Lifecycle**, specify when a user's assignment to the access package expires. Specify whether users can extend their assignments. For **Expiration**, set **Access package assignments** expiration to **On date**, **Number of days**, **Number of hours**, or **Never**.
14. In **Access Reviews**, select **Yes**.
15. In **Starting on**, select the current date. Set **Review Frequency** to **Quarterly**. Set **Duration (in Days)** to 21.

### Access package for guests (B2B)

Follow these steps to create an access package in entitlement management with Verified ID for guests (B2B).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. Select **New access package**.
4. For **Basics**, give the access package a name (such as *Finance Apps for Remote Users*). Specify the catalog that you previously created.
5. For **Resource roles**, select a resource type (for example: Groups and Teams, Applications, SharePoint sites). Select one or more resources.
6. In **Role**, select the role to which you want users assigned for each resource.

    [![Screenshot of Resources roles with a red box highlighting the Role column.](media/deployment-scenario-workforce-guest/resource-roles-inline.png)](media/deployment-scenario-workforce-guest/resource-roles.png#lightbox)
7. For **Requests**, select **For users not in your directory**.
8. Select **Specific connected organizations**. To select from a list of connected organizations that you previously added, select **Add directory**.
9. Enter the name or domain name to search for a previously connected organization.
10. Scroll to **Required Verified Ids**.
11. Select **+ Add issuer**. Select an issuer from the Microsoft Entra Verified ID network. Ensure that you select an issuer from an existing verified identity in the guest wallet.
12. **Optional:** In **Approval**, specify whether users require approval when they request the access package.
13. **Optional:** In **Requestor information**, select **Questions**. Enter a question (known as the display string) that you want to ask the requestor. To add localization options, select **Add localization**.
14. For **Lifecycle**, specify when a user's assignment to the access package expires. Specify whether users can extend their assignments. For **Expiration,** set **Access package assignments** expiration to **On date**, **Number of days**, **Number of hours**, or **Never**.
15. In **Access Reviews**, select **Yes**.
16. In **Starting on**, select the current date. Set **Review Frequency** to **Quarterly**. Set **Duration (in Days)** to 21.
17. Select **Specific reviewers**. Select **Self Review**.

    ![Screenshot of New access package.](media/deployment-scenario-workforce-guest/new-access-package.png)

## Create a sign-in risk-based Conditional Access policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Enter a policy name such as *Protect applications for remote high-risk sign-in users*.
5. For **Assignments**, select **Users**.

    1. For **Include**, select a remote user group or select all users.
    2. For **Exclude**, select **Users and groups**. Select your organization's emergency access or break-glass accounts.
    3. Select **Done**.
6. For **Cloud apps or actions** &gt; **Include**, select the applications to target this policy.
7. For **Conditions** &gt; **Sign-in risk**, set **Configure** to **Yes**. For **Select the sign-in risk level this policy will apply to**, select **High** and **Medium**.

    1. Select **Done**.
8. For **Access controls** &gt; **Grant**.

    1. Select **Grant access** &gt; **Require multifactor authentication**.
9. For **Session**, select **Sign-in frequency**. Select **Every time**.
10. Confirm settings. Select **Enable policy**.

    [![Screenshot of Conditional Access Policies, New, Sign-in risk. A red box emphasizes User risk and Sign-in risk.](media/deployment-scenario-workforce-guest/conditional-access-policies-new-inline.png)](media/deployment-scenario-workforce-guest/conditional-access-policies-new-expanded.png#lightbox)

## Request access package

After you configure an access package with a Verified ID requirement, end-users who are within the scope of the policy can request access in their **My Access** portal. While approvers review requests for approval, they can see the claims of the verified credentials that requestors present.

1. As a remote user or guest, sign in to `myaccess.microsoft.com`.
2. Search for the access package that you previously created (such as *Finance Apps for Remote Users*). You can browse the listed packages or use the search bar. Select **Request**.
3. The system displays an information banner with a message such as, *To request access to this access package you need to present your Verifiable Credentials*. Select **Request Access**. To launch Microsoft Authenticator, scan the QR Code with your phone. Share your credentials.

    ![Screenshot of My Access, Available, Access packages, Present Verified ID, QR Code.](media/deployment-scenario-workforce-guest/present-verified-id.png)
4. After you share your credentials, continue with the approval workflow.
5. **Optional:** Follow the [Simulating risk detections in Microsoft Entra ID Protection](../id-protection/howto-identity-protection-simulate-risk) instructions. You might need to try multiple times to raise the user risk to medium or high.
6. Try accessing the application that you previously created for the scenario to confirm blocked access. You might need to wait up to one hour for block enforcement.
7. Use sign in logs to validate blocked access by the Conditional Access policy that you created earlier. Open non-interactive sign in logs from the *ZTNA Network Access Client -- Private* application. View logs from the Private Access application name that you previously created as the **Resource name**.