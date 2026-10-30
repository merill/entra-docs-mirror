---
layout: Conceptual
title: Create and use password policies in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/password-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how and why to use fine-grained password policies to secure and control account passwords in a Domain Services managed domain.
ms.assetid: 1a14637e-b3d0-4fd9-ba7a-576b8df62ff2
ms.topic: how-to
ms.date: 2025-02-05T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 2eb4c941-c464-75cb-7a98-39c3a58be1b5
document_version_independent_id: e93b1a8f-3de2-309e-5a0b-923e2fa15e0b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/password-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/password-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/password-policy.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: b5155835-aba2-263f-7805-bb0907152425
---

# Create and use password policies in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

To manage user security in Microsoft Entra Domain Services, you can define fine-grained password policies that control account lockout settings or minimum password length and complexity. A default fine grained password policy is created and applied to all users in a Domain Services managed domain. To provide granular control and meet specific business or compliance needs, additional policies can be created and applied to specific users or groups.

This article shows you how to create and configure a fine-grained password policy in Domain Services using the Active Directory Administrative Center.

Note

Password policies are only available for managed domains created using the Resource Manager deployment model.

## Before you begin

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, complete the tutorial to [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
    - The managed domain must have been created using the Resource Manager deployment model.
- A Windows Server management VM that is joined to the managed domain.
    - If needed, complete the tutorial to [create a management VM](tutorial-create-management-vm).
- A user account that's a member of the *Microsoft Entra DC administrators* group in your Microsoft Entra tenant.

## Default password policy settings

Fine-grained password policies (FGPPs) let you apply specific restrictions for password and account lockout policies to different users in a domain. For example, to secure privileged accounts you can apply stricter account lockout settings than regular non-privileged accounts. You can create multiple FGPPs within a managed domain and specify the order of priority to apply them to users.

For more information about password policies and using the Active Directory Administration Center, see the following articles:

- [Learn about fine-grained password policies](/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770394%28v=ws.10%29)
- [Configure fine-grained password policies using AD Administration Center](/en-us/windows-server/identity/ad-ds/get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-#fine_grained_pswd_policy_mgmt)

Policies are distributed through group association in a managed domain, and any changes you make are applied at the next user sign-in. Changing the policy doesn't unlock a user account that's already locked out.

Password policies behave a little differently depending on how the user account they're applied to was created. There are two ways a user account can be created in Domain Services:

- The user account can be synchronized in from Microsoft Entra ID. This includes cloud-only user accounts created directly in Azure, and hybrid user accounts synchronized from an on-premises AD DS environment using Microsoft Entra Connect.
    - The majority of user accounts in Domain Services are created through the synchronization process from Microsoft Entra ID.
- The user account can be manually created in a managed domain, and doesn't exist in Microsoft Entra ID.

All users, regardless of how they're created, have the following account lockout policies applied by the default password policy in Domain Services:

- **Account lockout duration:** 30
- **Number of failed logon attempts allowed:** 5
- **Reset failed logon attempts count after:** 2 minutes
- **Maximum password age (lifetime):** 90 days

With these default settings, user accounts are locked out for 30 minutes if five invalid passwords are used within 2 minutes. Accounts are automatically unlocked after 30 minutes.

Account lockouts only occur within the managed domain. User accounts are only locked out in Domain Services, and only due to failed sign-in attempts against the managed domain. User accounts that were synchronized in from Microsoft Entra ID or on-premises aren't locked out in their source directories, only in Domain Services.

If you have a Microsoft Entra password policy that specifies a maximum password age greater than 90 days, that password age is applied to the default policy in Domain Services. You can configure a custom password policy to define a different maximum password age in Domain Services. Take care if you have a shorter maximum password age configured in a Domain Services password policy than in Microsoft Entra ID or an on-premises AD DS environment. In that scenario, a user's password may expire in Domain Services before they're prompted to change in Microsoft Entra ID or an on-premises AD DS environment.

For user accounts created manually in a managed domain, the following additional password settings are also applied from the default policy. These settings don't apply to user accounts synchronized in from Microsoft Entra ID, as a user can't update their password directly in Domain Services.

- **Minimum password length (characters):** 7
- **Passwords must meet complexity requirements**

You can't modify the account lockout or password settings in the default password policy. Instead, members of the *AAD DC Administrators* group can create custom password policies and configure it to override (take precedence over) the default built-in policy, as shown in the next section.

## Create a custom password policy

As you build and run applications in Azure, you may want to configure a custom password policy. For example, you could create a policy to set different account lockout policy settings.

Custom password policies are applied to groups in a managed domain. This configuration effectively overrides the default policy.

To create a custom password policy, you use the Active Directory Administrative Tools from a domain-joined VM. The Active Directory Administrative Center lets you view, edit, and create resources in a managed domain, including OUs.

Note

To create a custom password policy in a managed domain, you must be signed in to a user account that's a member of the *AAD DC Administrators* group.

1. From the Start screen, select **Administrative Tools**. A list of available management tools is shown that were installed in the tutorial to [create a management VM](tutorial-create-management-vm).
2. To create and manage OUs, select **Active Directory Administrative Center** from the list of administrative tools.
3. In the left pane, choose your managed domain, such as *aaddscontoso.com*.
4. Open the **System** container, then the **Password Settings Container**.

    A built-in password policy for the managed domain is shown. You can't modify this built-in policy. Instead, create a custom password policy to override the default policy.

    ![Create a password policy in the Active Directory Administrative Center](media/password-policy/create-password-policy-adac.png)
5. In the **Tasks** panel on the right, select **New &gt; Password Settings**.
6. In the **Create Password Settings** dialog, enter a name for the policy, such as *MyCustomFGPP*.
7. When multiple password policies exist, the policy with the highest precedence, or priority, is applied to a user. The lower the number, the higher the priority. The default password policy has a priority of *200*.

    Set the precedence for your custom password policy to override the default, such as *1*.
8. Edit other password policy settings as desired. Account lockout settings apply to all users, but only take effect within the managed domain and not in Microsoft Entra itself.

    ![Create a custom fine-grained password policy](media/password-policy/custom-fgpp.png)
9. Uncheck **Protect from accidental deletion**. If this option is selected, you can't save the FGPP.
10. In the **Directly Applies To** section, select the **Add** button. In the **Select Users or Groups** dialog, select the **Locations** button.

    ![Select the users and groups to apply the password policy to](media/password-policy/fgpp-applies-to.png)
11. In the **Locations** dialog, expand the domain name, such as *aaddscontoso.com*, then select an OU, such as **AADDC Users**. If you have a custom OU that contains a group of users you wish to apply, select that OU.

    ![Select the OU that the group belongs to](media/password-policy/fgpp-container.png)
12. Type the name of the user or group you wish to apply the policy to. Select **Check Names** to validate the account.

    ![Search for and select the group to apply FGPP](media/password-policy/fgpp-apply-group.png)
13. Click **OK** to save your custom password policy.