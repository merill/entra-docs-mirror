---
layout: Conceptual
title: 'Tutorial: Multifactor authentication for B2B - Microsoft Entra External ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/b2b-tutorial-require-mfa
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: In this tutorial, learn how to require multifactor authentication when you use Microsoft Entra B2B to collaborate with external users and partner organizations.
ms.topic: tutorial
ms.date: 2026-04-24T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 38883fa1-020d-1721-56fd-d92a99a2cef9
document_version_independent_id: ea2e2ce3-3316-d0bd-16b6-aa036a6af806
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/b2b-tutorial-require-mfa.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/b2b-tutorial-require-mfa
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/b2b-tutorial-require-mfa.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: d213cfc8-13fc-ec9d-4d3d-73e06abd7a28
---

# Tutorial: Multifactor authentication for B2B - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

When you collaborate with external B2B guest users, protect your apps with multifactor authentication policies. External users need more than just a username and password to access your resources. In Microsoft Entra ID, you can accomplish this goal with a Conditional Access policy that requires MFA for access. You can enforce MFA policies at the tenant, app, or individual guest user level, just like for members of your own organization. The resource tenant is responsible for Microsoft Entra multifactor authentication for users, even if the guest user's organization has multifactor authentication capabilities.

Example:

![Diagram showing a guest user signing into a company's apps.](media/tutorial-mfa/b2b-mfa-example.png)

1. An admin or employee at Company A invites a guest user to use a cloud or on-premises application that is configured to require MFA for access.
2. The guest user signs in with their own work, school, or social identity.
3. The user is asked to complete an MFA challenge.
4. The user sets up MFA with Company A and chooses their MFA option. The user is allowed access to the application.

Note

Microsoft Entra multifactor authentication is performed by the resource tenant to ensure predictability. When the guest user signs in, they see the resource tenant sign-in page displayed in the background, and their own home tenant sign-in page and company logo in the foreground.

In this tutorial, you will:

- Test the sign-in experience before setting up MFA.
- Create a Conditional Access policy that requires MFA for access to a cloud app in your environment. In this tutorial, we’ll use the Azure Resource Manager app to illustrate the process.
- Use the What If tool to simulate MFA sign-in.
- Test your Conditional Access policy.
- Clean up the test user and policy.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) to get started.

## Prerequisites

To complete the scenario in this tutorial, you need:

- **Access to Microsoft Entra ID P1 or P2 edition**, which includes Conditional Access policy capabilities. To enforce MFA, create a Microsoft Entra Conditional Access policy. MFA policies are always enforced at your organization, even if the partner doesn't have MFA capabilities.
- **A valid external email account** that you can add to your tenant directory as a guest user and use to sign in. If you don't know how to create a guest account, follow the steps in [Add a B2B guest user in the Microsoft Entra admin center](add-users-administrator).

## Create a test guest user in Microsoft Entra ID

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** and then **Invite external user**.

    [![Screenshot of where to select the new guest user option.](media/tutorial-mfa/tutorial-mfa-new-user.png)](media/tutorial-mfa/tutorial-mfa-new-user.png#lightbox)
4. Under **Identity** on the **Basics** tab, enter the email address of the external user. You can optionally include a display name and welcome message.

    ![Screenshot of where to enter the guest email.](media/tutorial-mfa/tutorial-mfa-new-user-identity.png)
5. You can optionally add further details to the user under the **Properties** and **Assignments** tabs.
6. Select **Review + invite** to automatically send the invitation to the guest user. A **Successfully invited user** message appears.
7. After you send the invitation, the user account is added to the directory as a guest.

## Test the sign-in experience before MFA setup

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) using your test user name and password.
2. Access the Microsoft Entra admin center using only your sign-in credentials. No other authentication is required.
3. Sign out of the Microsoft Entra admin center.

## Create a Conditional Access policy that requires MFA

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Name your policy, like **Require MFA for B2B portal access**. Create a meaningful standard for naming policies.
5. Under **Assignments**, select **Users or workload identities**.

    1. Under **Include**, choose **Select users and groups**, and then select **Guest or external users**. You can assign the policy to different [external user types](authentication-conditional-access#assign-conditional-access-policies-to-external-user-types), built-in directory roles, or users and groups.

    ![Screenshot showing selecting all guest users.](media/tutorial-mfa/tutorial-mfa-user-access.png)
6. Under **Target resources** &gt; **Resources (formerly cloud apps)** &gt; **Include** &gt; **Select resources**, choose **Azure Resource Manager**, and then **Select** the resource.

    [![Screenshot showing the Cloud apps page and the Select option.](media/tutorial-mfa/tutorial-mfa-app-access.png)](media/tutorial-mfa/tutorial-mfa-app-access.png#lightbox)
7. Under **Access controls** &gt; **Grant**, select **Grant access**, **Require multifactor authentication**, and select **Select**.

    ![Screenshot showing the option for requiring multifactor authentication.](media/tutorial-mfa/tutorial-mfa-grant-access.png)
8. Under **Enable policy**, select **On**.
9. Select **Create**.

## Use the What If option to simulate sign-in

The **Conditional Access What If policy tool** helps you understand the effects of Conditional Access policies in your environment. Instead of manually testing your policies with multiple sign-ins, you can use this tool to simulate a user's sign-in. The simulation predicts how this sign-in will affect your policies and generates a report. For more information, see [Use the What If tool to understand Conditional Access policies](/en-us/entra/identity/conditional-access/what-if-tool).

## Test your Conditional Access policy

1. Use your test user name and password to sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. You should see a request for more authentication methods. It can take some time for the policy to take effect.

    ![Screenshot of the 'More information required' message.](media/tutorial-mfa/mfa-required.png)

    Note

    You can also configure [cross-tenant access settings](cross-tenant-access-overview) to trust the MFA from the Microsoft Entra home tenant. This allows external Microsoft Entra users to use the MFA registered in their own tenant rather than register in the resource tenant.
3. Sign out.

## Clean up resources

When no longer needed, remove the test user and the test Conditional Access policy.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select the test user, and then select **Delete user**.
4. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](../identity/role-based-access-control/permissions-reference#conditional-access-administrator).
5. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
6. In the **Policy Name** list, select the context menu (…) for your test policy, then select **Delete**, and confirm by selecting **Yes**.