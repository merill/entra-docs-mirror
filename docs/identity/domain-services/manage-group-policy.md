---
layout: HowTo
title: Create and manage group policy in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/domain-services/manage-group-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: domain-services
manager: dougeby
description: Learn how to edit the built-in Group Policy Objects (GPOs) and create your own custom policies in a Microsoft Entra Domain Services managed domain.
ms.date: 2025-02-25T00:00:00.0000000Z
ms.topic: how-to
ms.custom:
- ge-structured-content-pilot
- sfi-image-nochange
locale: en-us
document_id: f6670151-45dd-1dca-42dd-7b8e25517878
document_version_independent_id: 48a8ef9d-e878-76d8-08b0-e0ac19056daa
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/domain-services/manage-group-policy.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: HowTo
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/domain-services/manage-group-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/domain-services/manage-group-policy.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: fb4dbb14-787a-ca31-7c4f-fc3ec47bc33f
---

# Create and manage group policy in Microsoft Entra Domain Services - Microsoft Entra ID | Microsoft Learn

Settings for user and computer objects in Microsoft Entra Domain Services are often managed using Group Policy Objects (GPOs). Domain Services includes built-in GPOs for the *AADDC Users* and *AADDC Computers* containers. You can customize these built-in GPOs to configure Group Policy as needed for your environment. Members of the *AAD DC Administrators* group have Group Policy administration privileges in the Domain Services domain, and can also create custom GPOs and organizational units (OUs). For more information on what Group Policy is and how it works, see [Group Policy overview](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831791%28v=ws.11%29).

In a hybrid environment, group policies configured in an on-premises AD DS environment aren't synchronized to Domain Services. To define configuration settings for users or computers in Domain Services, edit one of the default GPOs or create a custom GPO.

This article shows you how to install the Group Policy Management tools, then edit the built-in GPOs and create custom GPOs. We recommend that you back up GPOs after you make any changes to them. For more information about how to back up and restore GPOs, see [Backup, restore, migrate, and copy Group Policy Objects](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-backup-restore).

If you are interested in server management strategy, including machines in Azure and [hybrid connected](/en-us/azure/azure-arc/servers/overview), consider reading about the [guest configuration](/en-us/azure/governance/machine-configuration/overview) feature of [Azure Policy](/en-us/azure/governance/policy/overview).

## Prerequisites

To complete this article, you need the following resources and privileges:

- An active Azure subscription.
    - If you don't have an Azure subscription, [create an account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A Microsoft Entra tenant associated with your subscription, either synchronized with an on-premises directory or a cloud-only directory.
    - If needed, [create a Microsoft Entra tenant](/en-us/azure/active-directory/fundamentals/sign-up-organization) or [associate an Azure subscription with your account](/en-us/azure/active-directory/fundamentals/how-subscriptions-associated-directory).
- A Microsoft Entra Domain Services managed domain enabled and configured in your Microsoft Entra tenant.
    - If needed, complete the tutorial to [create and configure a Microsoft Entra Domain Services managed domain](tutorial-create-instance).
- A Windows Server management VM that is joined to the Domain Services managed domain.
    - If needed, complete the tutorial to [create a Windows Server VM and join it to a managed domain](join-windows-vm).
- A user account that's a member of the *AAD DC Administrators* group in your Microsoft Entra tenant.

Note

You can use Group Policy Administrative Templates by copying the new templates to the management workstation. Copy the *.admx* files into `%SYSTEMROOT%\PolicyDefinitions` and copy the locale-specific *.adml* files to `%SYSTEMROOT%\PolicyDefinitions\[Language-CountryRegion]`, where `Language-CountryRegion` matches the language and region of the *.adml* files.

For example, copy the English, United States version of the *.adml* files into the `\en-us` folder.

## Install Group Policy Management tools

To create and configure Group Policy Object (GPOs), you need to install the Group Policy Management tools. These tools can be installed as a feature in Windows Server. For more information on how to install the administrative tools on a Windows client, see install [Remote Server Administration Tools (RSAT)](/en-us/windows-server/remote/remote-server-administration-tools#BKMK_Thresh).

1. Sign in to your management VM. For steps on how to connect using the Microsoft Entra admin center, see [Connect to a Windows Server VM](join-windows-vm#connect-to-the-windows-server-vm).
2. **Server Manager** should open by default when you sign in to the VM. If not, on the **Start** menu, select **Server Manager**.
3. In the *Dashboard* pane of the **Server Manager** window, select **Add Roles and Features**.
4. On the **Before You Begin** page of the *Add Roles and Features Wizard*, select **Next**.
5. For the *Installation Type*, leave the **Role-based or feature-based installation** option checked and select **Next**.
6. On the **Server Selection** page, choose the current VM from the server pool, such as *myvm.aaddscontoso.com*, then select **Next**.
7. On the **Server Roles** page, click **Next**.
8. On the **Features** page, select the **Group Policy Management** feature.

    ![Install the 'Group Policy Management' from the Features page](media/entra-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
9. On the **Confirmation** page, select **Install**. It may take a minute or two to install the Group Policy Management tools.
10. When feature installation is complete, select **Close** to exit the **Add Roles and Features** wizard.

## Open the Group Policy Management Console and edit an object

Default Group Policy Objects (GPOs) exist for users and computers in a managed domain. With the Group Policy Management feature installed from the previous section, let's view and edit an existing GPO. In the next section, you create a custom GPO.

Note

To administer Group Policy in a managed domain, you must be signed in to a user account that's a member of the *AAD DC Administrators* group.

1. From the Start screen, select **Administrative Tools**. A list of available management tools is shown, including **Group Policy Management** installed in the previous section.
2. To open the Group Policy Management Console (GPMC), choose **Group Policy Management**.

    ![The Group Policy Management Console opens ready to edit group policy objects](media/entra-domain-services-admin-guide/gp-management-console.png)

There are two built-in Group Policy Objects (GPOs) in a managed domain - one for the *AADDC Computers* container, and one for the *AADDC Users* container. You can customize these GPOs to configure group policy as needed within your managed domain.

1. In the **Group Policy Management** console, expand the **Forest: aaddscontoso.com** node. Next, expand the **Domains** nodes.

    Two built-in containers exist for *AADDC Computers* and *AADDC Users*. Each of these containers has a default GPO applied to them.

    ![Built-in GPOs applied to the default 'AADDC Computers' and 'AADDC Users' containers](media/entra-domain-services-admin-guide/builtin-gpos.png)
2. These built-in GPOs can be customized to configure specific group policies on your managed domain. Right-select one of the GPOs, such as *AADDC Computers GPO*, then choose **Edit...**.

    ![Choose the option to 'Edit' one of the built-in GPOs](media/entra-domain-services-admin-guide/edit-builtin-gpo.png)
3. The Group Policy Management Editor tool opens to let you customize the GPO, such as *Account Policies*:

    ![Screenshot of the Group Policy Management Editor.](media/entra-domain-services-admin-guide/gp-editor.png)

    When done, choose **File &gt; Save** to save the policy. Computers refresh Group Policy by default every 90 minutes and apply the changes you made.

## Create a custom Group Policy Object

To group similar policy settings, you often create additional GPOs instead of applying all of the required settings in the single, default GPO. With Domain Services, you can create or import your own custom Group Policy Objects and link them to a custom OU. If you need to first create a custom OU, see [create a custom OU in a managed domain](create-ou).

1. In the **Group Policy Management** console, select your custom organizational unit (OU), such as *MyCustomOU*. Right-select the OU and choose **Create a GPO in this domain, and Link it here...**:

    ![Create a custom GPO in the Group Policy Management console](media/entra-domain-services-admin-guide/gp-create-gpo.png)
2. Specify a name for the new GPO, such as *My custom GPO*, then select **OK**. You can optionally base this custom GPO on an existing GPO and set of policy options.

    ![Specify a name for the new custom GPO](media/entra-domain-services-admin-guide/gp-specify-gpo-name.png)
3. The custom GPO is created and linked to your custom OU. To now configure the policy settings, right-select the custom GPO and choose **Edit...**:

    ![Choose the option to 'Edit' your custom GPO](media/entra-domain-services-admin-guide/gp-gpo-created.png)
4. The **Group Policy Management Editor** opens to let you customize the GPO:

    ![Customize GPO to configure settings as required](media/entra-domain-services-admin-guide/gp-customize-gpo.png)

    When done, choose **File &gt; Save** to save the policy. Computers refresh Group Policy by default every 90 minutes and apply the changes you made.