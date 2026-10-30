---
layout: Conceptual
title: 'Tutorial:  Set up password hash sync as backup for AD FS in Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/tutorial-phs-backup
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to turn on password hash sync as a backup for Azure Directory Federation Services (AD FS) in Microsoft Entra Connect.
ms.topic: tutorial
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8d89bd51-4704-40bb-bbf2-be6e62bf5082
document_version_independent_id: 51576011-64fe-5510-caee-58427f3529de
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/tutorial-phs-backup.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/tutorial-phs-backup
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/tutorial-phs-backup.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: caac30f4-13d4-fb7e-3a83-9ef20cfc7b59
---

# Tutorial:  Set up password hash sync as backup for AD FS in Microsoft Entra Connect - Microsoft Entra ID | Microsoft Learn

This tutorial walks you through the steps to set up password hash sync as a backup and failover for Azure Directory Federation Services (AD FS) in Microsoft Entra Connect. The tutorial also demonstrates how to set password hash sync as the primary authentication method if AD FS fails or becomes unavailable.

Note

Although these steps usually are taken in an emergency or outage situation, we recommend that you test these steps and verify your procedures before an outage occurs.

## Prerequisites

This tutorial builds on [Tutorial: Use federation for hybrid identity in a single Active Directory forest](tutorial-federation). Completing the tutorial is a prerequisite to completing the steps in this tutorial.

Note

If you don't have access to a Microsoft Entra Connect server or the server doesn't have internet access, you can contact [Microsoft Support](https://support.microsoft.com/contactus/) to assist with the changes to Microsoft Entra ID.

## Enable password hash sync in Microsoft Entra Connect

In [Tutorial: Use federation for hybrid identity in a single Active Directory forest](tutorial-federation), you created a Microsoft Entra Connect environment that's using federation.

Your first step in setting up your backup for federation is to turn on password hash sync and set Microsoft Entra Connect to sync the hashes:

1. Double-click the Microsoft Entra Connect icon that was created on the desktop during installation.
2. Select **Configure**.
3. In **Additional tasks**, select **Customize synchronization options**, and then select **Next**.

    ![Screenshot that shows the Additional tasks pane, with Customize synchronization options selected.](media/tutorial-phs-backup/backup2.png)
4. Enter the username and password for the [Hybrid Identity Administrator account you created](tutorial-federation#create-a-hybrid-identity-administrator-account-in-azure-ad) in the tutorial to set up federation.
5. In **Connect your directories**, select **Next**.
6. In **Domain and OU filtering**, select **Next**.
7. In **Optional features**, select **Password hash synchronization**, and then select **Next**.

    ![Screenshot that shows the Optional features pane, with Password hash synchronization selected.](media/tutorial-phs-backup/backup1.png)
8. In **Ready to configure**, select **Configure**.
9. When configuration is finished, select **Exit**.

That's it! You're done. Password hash sync will now occur, and it can be used as a backup if AD FS becomes unavailable.

## Switch to password hash sync

Important

- Before you switch to password hash sync, create a backup of your AD FS environment. You can create a backup by using the [AD FS Rapid Restore Tool](/en-us/windows-server/identity/ad-fs/operations/ad-fs-rapid-restore-tool#how-to-use-the-tool).
- It takes some time for the password hashes to sync to Microsoft Entra ID. It might be up to three hours before the sync finishes and you can start authenticating by using the password hashes.

Next, switch over to password hash synchronization. Before you start, consider in which conditions you should make the switch. Don't make the switch for temporary reasons, like a network outage, a minor AD FS problem, or a problem that affects a subset of your users.

If you decide to make the switch because fixing the problem will take too long, complete these steps:

1. In Microsoft Entra Connect, select **Configure**.
2. Select **Change user sign-in**, and then select **Next**.
3. Enter the username and password for the [Hybrid Identity Administrator account you created](tutorial-federation#create-a-hybrid-identity-administrator-account-in-azure-ad) in the tutorial to set up federation.
4. In **User sign-in**, select **Password hash synchronization**, and then select the **Do not convert user accounts** checkbox.
5. Leave the default **Enable single sign-on** selected and select **Next**.
6. In **Enable single sign-on**, select **Next**.
7. In **Ready to configure**, select **Configure**.
8. When configuration is finished, select **Exit**.

Users can now use their passwords to sign in to Azure and Azure services.

## Sign in with a user account to test sync

1. In a new web browser window, go to https://myapps.microsoft.com.
2. Sign in with a user account that was created in your new tenant.

    For the username, use the format `user@domain.onmicrosoft.com`. Use the same password the user uses to sign in to on-premises Active Directory.

    ![Screenshot that shows a successful message when testing the sign-in.](media/tutorial-federation/verify1.png)

## Switch back to federation

Now, switch back to federation:

1. In Microsoft Entra Connect, select **Configure**.
2. Select **Change user sign-in**, and then select **Next**.
3. Enter the username and password for your Hybrid Identity Administrator account.
4. In **User sign-in**, select **Federation with AD FS**, and then select **Next**.
5. In **Domain Administrator credentials**, enter the contoso\Administrator username and password, and then select **Next.**
6. In **AD FS farm**, select **Next**.
7. In **Microsoft Entra domain**, select the domain and select **Next**.
8. In **Ready to configure**, select **Configure**.
9. When configuration is finished, select **Next**.

    ![Screenshot that shows the Configuration complete pane.](media/tutorial-phs-backup/backup4.png)
10. In **Verify federation connectivity**, select **Verify**. You might need to configure DNS records (add A and AAAA records) for verification to finish successfully.

    ![Screenshot that shows the Verify federation connectivity dialog and the Verify button.](media/tutorial-phs-backup/backup5.png)
11. Select **Exit**.

## Reset the AD FS and Azure trust

The final task is to reset the trust between AD FS and Azure:

1. In Microsoft Entra Connect, select **Configure**.
2. Select **Manage federation**, and then select **Next**.
3. Select **Reset Microsoft Entra ID trust**, and then select **Next**.

    ![Screenshot that shows the Manage federation pane, with Reset Microsoft Entra ID selected.](media/tutorial-phs-backup/backup6.png)
4. In **Connect to Microsoft Entra ID**, enter the username and password for your Hybrid Identity Administrator account.
5. In **Connect to AD FS**, enter the contoso\Administrator username and password, and then select **Next.**
6. In **Certificates**, select **Next**.
7. Repeat the steps in Sign in with a user account to test sync.

You've successfully set up a hybrid identity environment that you can use to test and to get familiar with what Azure has to offer.