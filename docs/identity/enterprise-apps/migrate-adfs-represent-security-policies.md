---
layout: Conceptual
title: 'Represent AD FS security policies in Microsoft Entra ID: Mappings and examples - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migrate-adfs-represent-security-policies
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to map AD FS security policies to Microsoft Entra ID when migrating app authentication, including authorization and multifactor authentication rules.
ms.topic: concept-article
ms.date: 2023-05-31T00:00:00.0000000Z
ms.reviewer: gasinh
ms.custom: sfi-image-nochange
locale: en-us
document_id: c1f2c375-fc1e-2c3b-4f24-ec6b07556393
document_version_independent_id: 2b318a13-c2c0-a96c-bc8b-eb684551ad7c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migrate-adfs-represent-security-policies.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migrate-adfs-represent-security-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migrate-adfs-represent-security-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 65e1adb9-0d3e-f00b-e892-586982c7cd1f
---

# Represent AD FS security policies in Microsoft Entra ID: Mappings and examples - Microsoft Entra ID | Microsoft Learn

In this article, you'll learn how to map authorization and multifactor authentication rules from AD FS to Microsoft Entra ID when moving your app authentication. Find out how to meet your app owner's security requirements while making the app migration process easier with mappings for each rule.

When moving your app authentication to Microsoft Entra ID, create mappings from existing security policies to their equivalent or alternative variants available in Microsoft Entra ID. Ensuring that these mappings can be done while meeting security standards required by your app owners makes the rest of the app migration easier.

For each rule example, we show what the rule looks like in AD FS, the AD FS rule language equivalent code, and how this maps to Microsoft Entra ID.

## Map authorization rules

The following are examples of various types of authorization rules in AD FS, and how you map them to Microsoft Entra ID.

### Example 1: Permit access to all users

Permit Access to All Users in AD FS:

![Screenshot shows how to edit access to all users.](media/migrate-adfs-represent-security-policies/permit-access-to-all-users-1.png)

This maps to Microsoft Entra ID in one of the following ways:

1. Set **Assignment required** to **No**.

    Note

    Setting **Assignment required** to **Yes** requires that users are assigned to the application to gain access. When set to **No**, all users have access. This switch doesn't control what users see in the **My Apps** experience.
2. In the **Users and groups tab**, assign your application to the **All Users** automatic group. You must [enable Dynamic Groups](../users/groups-create-rule) in your Microsoft Entra tenant for the default **All Users** group to be available.

    ![Screenshot shows My SaaS Apps in Microsoft Entra ID.](media/migrate-adfs-represent-security-policies/permit-access-to-all-users-3.png)

### Example 2: Allow a group explicitly

Explicit group authorization in AD FS:

![Screenshot shows the Edit Rule dialog box for the Allow domain admins claim rule.](media/migrate-adfs-represent-security-policies/allow-a-group-explicitly-1.png)

To map this rule to Microsoft Entra ID:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com/#home), [create a user group](/en-us/entra/fundamentals/how-to-manage-groups) that corresponds to the group of users from AD FS.
2. Assign app permissions to the group:

    ![Screenshot shows how to add an assignment to the app.](media/migrate-adfs-represent-security-policies/allow-a-group-explicitly-2.png)

### Example 3: Authorize a specific user

Explicit user authorization in AD FS:

![Screenshot shows the Edit Rule dialog box for the Allow a specific user Claim rule with an Incoming claim type of Primary S I D.](media/migrate-adfs-represent-security-policies/authorize-a-specific-user-1.png)

To map this rule to Microsoft Entra ID:

- In the [Microsoft Entra admin center](https://entra.microsoft.com/#home), add a user to the app through the Add Assignment tab of the app as shown below:

    ![Screenshot shows My SaaS apps in Azure.](media/migrate-adfs-represent-security-policies/authorize-a-specific-user-2.png)

## Map multifactor authentication rules

An on-premises deployment of [Multifactor Authentication (MFA)](../authentication/concept-mfa-howitworks) and AD FS still works after the migration because you're federated with AD FS. However, consider migrating to Azure's built-in MFA capabilities that are tied into Microsoft Entra Conditional Access policies.

The following are examples of types of MFA rules in AD FS, and how you can map them to Microsoft Entra ID based on different conditions.

MFA rule settings in AD FS:

![Screenshot shows Conditions for Microsoft Entra ID in the Microsoft Entra admin center.](media/migrate-adfs-represent-security-policies/mfa-settings-common-for-all-examples.png)

### Example 1: Enforce MFA based on users/groups

The users/groups selector is a rule that allows you to enforce MFA on a per-group (Group SID) or per-user (Primary SID) basis. Apart from the users/groups assignments, all other checkboxes in the AD FS MFA configuration UI function as extra rules that are evaluated after the users/groups rule is enforced.

[Common Conditional Access policy: Require MFA for all users](../conditional-access/policy-all-users-mfa-strength)

### Example 2: Enforce MFA for unregistered devices

Specify MFA rules for unregistered devices in Microsoft Entra:

[Common Conditional Access policy: Require a compliant device, Microsoft Entra hybrid joined device, or multifactor authentication for all users](../conditional-access/policy-alt-all-users-compliant-hybrid-or-mfa)

## Map Emit attributes as Claims rule

Emit attributes as Claims rule in AD FS:

![Screenshot shows the Edit Rule dialog box for Emit attributes as Claims.](media/migrate-adfs-represent-security-policies/map-emit-attributes-as-claims-rule-1.png)

To map the rule to Microsoft Entra ID:

1. In the [Microsoft Entra admin center](https://entra.microsoft.com/#home), select **Enterprise Applications** and then **Single sign-on** to view the SAML-based sign-on configuration:

    [![Screenshot shows the Single sign-on page for your Enterprise Application.](media/migrate-adfs-represent-security-policies/map-emit-attributes-as-claims-rule-2.png)](media/migrate-adfs-represent-security-policies/map-emit-attributes-as-claims-rule-2.png#lightbox)
2. Select **Edit** (highlighted) to modify the attributes:

    ![Screenshot shows the page to edit User Attributes and Claims.](media/migrate-adfs-represent-security-policies/map-emit-attributes-as-claims-rule-3.png)

## Map built-In access control policies

Built-in access control policies in AD FS 2016:

![Screenshot shows Microsoft Entra ID built in access control.](media/migrate-adfs-represent-security-policies/map-built-in-access-control-policies-1.png)

To implement built-in policies in Microsoft Entra ID, use a [new Conditional Access policy](../authentication/tutorial-enable-azure-mfa?bc=/azure/active-directory/conditional-access/breadcrumb/toc.json&amp;toc=/azure/active-directory/conditional-access/toc.json) and configure the access controls, or use the custom policy designer in AD FS 2016 to configure access control policies. The Rule Editor has an exhaustive list of Permit and Except options that can help you make all kinds of permutations.

![Screenshot shows Microsoft Entra ID built in access control policies.](media/migrate-adfs-represent-security-policies/map-built-in-access-control-policies-2.png)

In this table, we've listed some useful Permit and Except options and how they map to Microsoft Entra ID.

| Option | How to configure Permit option in Microsoft Entra ID? | How to configure Except option in Microsoft Entra ID? |
| --- | --- | --- |
| From specific network | Maps to [Named Location](../conditional-access/concept-assignment-network) in Microsoft Entra | Use the **Exclude** option for [trusted locations](../conditional-access/concept-assignment-network#trusted-locations) |
| From specific groups | [Set a User/Groups Assignment](assign-user-or-group-access-portal) | Use the **Exclude** option in Users and Groups |
| From Devices with Specific Trust Level | Set this from the **Device State** control under Assignments -&gt; Conditions | Use the **Exclude** option under Device State Condition and Include **All devices** |
| With Specific Claims in the Request | This setting can't be migrated | This setting can't be migrated |

Here's an example of how to configure the Exclude option for trusted locations in the Microsoft Entra admin center:

![Screenshot of mapping access control policies.](media/migrate-adfs-represent-security-policies/map-built-in-access-control-policies-3.png)

## Transition users from AD FS to Microsoft Entra ID

### Sync AD FS groups in Microsoft Entra ID

When you map authorization rules, apps that authenticate with AD FS may use Active Directory groups for permissions. In such a case, use [Microsoft Entra Connect](https://entra.microsoft.com/#view/Microsoft_AAD_Connect_Provisioning/AADConnectMenuBlade/%7E/GetStarted) to sync these groups with Microsoft Entra ID before migrating the applications. Make sure that you verify those groups and membership before migration so that you can grant access to the same users when the application is migrated.

For more information, see [Prerequisites for using Group attributes synchronized from Active Directory](../hybrid/connect/how-to-connect-fed-group-claims).

### Set up user self-provisioning

Some SaaS applications support the ability to Just-in-Time (JIT) provision users when they first sign in to the application. In Microsoft Entra ID, app provisioning refers to automatically creating user identities and roles in the cloud ([SaaS](https://azure.microsoft.com/overview/what-is-saas/)) applications that users need to access. Users that are migrated already have an account in the SaaS application. Any new users added after the migration need to be provisioned. Test [SaaS app provisioning](../app-provisioning/user-provisioning) once the application is migrated.

### Sync external users in Microsoft Entra ID

Your existing external users can be set up in these two ways in AD FS:

- **External users with a local account within your organization**—You continue to use these accounts in the same way that your internal user accounts work. These external user accounts have a principle name within your organization, although the account's email may point externally.

As you progress with your migration, you can take advantage of the benefits that [Microsoft Entra B2B](../../external-id/what-is-b2b) offers by migrating these users to use their own corporate identity when such an identity is available. This streamlines the process of signing in for those users, as they're often signed in with their own corporate sign-in. Your organization's administration is easier as well, by not having to manage accounts for external users.

- **Federated external Identities**—If you're currently federating with an external organization, you have a few approaches to take:
    - [Add Microsoft Entra B2B collaboration users in the Microsoft Entra admin center](../../external-id/add-users-administrator). You can proactively send B2B collaboration invitations from the Microsoft Entra administrative portal to the partner organization for individual members to continue using the apps and assets they're used to.
    - [Create a self-service B2B sign-up workflow](../../external-id/self-service-portal) that generates a request for individual users at your partner organization using the B2B invitation API.

No matter how your existing external users are configured, they likely have permissions that are associated with their account, either in group membership or specific permissions. Evaluate whether these permissions need to be migrated or cleaned up.

Accounts within your organization that represent an external user need to be disabled once the user has been migrated to an external identity. The migration process should be discussed with your business partners, as there may be an interruption in their ability to connect to your resources.