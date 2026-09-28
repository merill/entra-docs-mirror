---
layout: Conceptual
title: Configure Bonusly for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bonusly-provisioning-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure Microsoft Entra ID to automatically provision and de-provision user accounts to Bonusly.
ms.topic: how-to
ms.date: 2026-03-02T00:00:00.0000000Z
locale: en-us
document_id: 01690e01-fd98-75f3-3a51-6fc4c93a72de
document_version_independent_id: ffc163f8-f3d0-73c2-e085-ca6d68c914ff
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bonusly-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bonusly-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bonusly-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: e2bac3c4-1aab-7acf-7f7f-b155de31dc5d
---

# Configure Bonusly for automatic user provisioning with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

The objective of this article is to demonstrate the steps to be performed in Bonusly and Microsoft Entra ID to configure Microsoft Entra ID to automatically provision and de-provision users and/or groups to Bonusly.

Note

This article describes a connector built on top of the Microsoft Entra user Provisioning Service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Microsoft Entra ID](../app-provisioning/user-provisioning).

## Prerequisites

The scenario outlined in this article assumes that you already have the following:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A [Bonusly tenant](https://bonus.ly/pricing)
- A user account in Bonusly with Admin permissions

Note

The Microsoft Entra provisioning integration relies on the [Bonusly REST API](https://konghq.com/solutions/gateway/), which is available to Bonusly developers.

## Adding Bonusly from the gallery

Before configuring Bonusly for automatic user provisioning with Microsoft Entra ID, you need to add Bonusly from the Microsoft Entra application gallery to your list of managed SaaS applications.

**To add Bonusly from the Microsoft Entra application gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the search box, type **Bonusly**, select **Bonusly** from result panel then select **Add** button to add the application.

    ![Bonusly in the results list](common/search-new-app.png)

## Assigning users to Bonusly

Microsoft Entra ID uses a concept called "assignments" to determine which users should receive access to selected apps. In the context of automatic user provisioning, only the users and/or groups that have been "assigned" to an application in Microsoft Entra ID are synchronized.

Before configuring and enabling automatic user provisioning, you should decide which users and/or groups in Microsoft Entra ID need access to Bonusly. Once decided, you can assign these users and/or groups to Bonusly by following the instructions here:

- [Assign a user or group to an enterprise app](../enterprise-apps/assign-user-or-group-access-portal)

### Important tips for assigning users to Bonusly

- It's recommended that a single Microsoft Entra user is assigned to Bonusly to test the automatic user provisioning configuration. Additional users and/or groups may be assigned later.
- When assigning a user to Bonusly, you must select any valid application-specific role (if available) in the assignment dialog. Users with the **Default Access** role are excluded from provisioning.

## Configuring automatic user provisioning to Bonusly

This section guides you through the steps to configure the Microsoft Entra provisioning service to create, update, and disable users and/or groups in Bonusly based on user and/or group assignments in Microsoft Entra ID.

Tip

You may also choose to enable SAML-based single sign-on for Bonusly, following the instructions provided in the [Bonusly single sign-on article](bonus-tutorial). Single sign-on can be configured independently of automatic user provisioning, though these two features complement each other.

### To configure automatic user provisioning for Bonusly in Microsoft Entra ID:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Bonusly**.

    ![Enterprise applications blade](common/enterprise-applications.png)
3. In the applications list, select **Bonusly**.

    ![The Bonusly link in the Applications list](common/all-applications.png)
4. Select the **Provisioning** tab.

    ![Screenshot of the Bonusly - Provisioning tab. Under Manage, Provisioning is highlighted.](media/bonusly-provisioning-tutorial/provisioningtab.png)
5. Set **+ New configuration**.

    ![Screenshot of Provisioning tab automatic.](common/application-provisioning.png)
6. Under the **Admin Credentials** section, input the **Secret Token** of your Bonusly account as described in Step 6.

    ![Screenshot of the Admin credentials section. The Secret token box is empty, but the box is highlighted.](media/bonusly-provisioning-tutorial/secrettoken.png)
7. The **Secret Token** for your Bonusly account is located in **Admin &gt; Company &gt; Integrations**. In the **If you want to code** section, select **API &gt; Create New API Access Token** to create a new Secret Token.

    ![Screenshot of the Bonusly menu. Under Admin, Company is highlighted. Under Company, Integrations is highlighted.](media/bonusly-provisioning-tutorial/bonuslyintegrations.png)

    ![Screenshot of the If you want to code section of the Bonusly site, with A P I highlighted.](media/bonusly-provisioning-tutorial/bonsulyrestapi.png)

    ![Screenshot of the Bonusly site. The Services tab is open. Under Your A P I access tokens, Create new A P I access token is highlighted.](media/bonusly-provisioning-tutorial/createtoken.png)
8. On the following screen, type a name for the access token in the provided text box, then press **Create Api Key**. The new access token appears for a few seconds in a pop-up.

    ![Screenshot of the New access token page of the Bonusly site. An unlabeled box contains My Token, and the Create A P I key button is highlighted.](media/bonusly-provisioning-tutorial/token01.png)

    ![Screenshot of the Bonusly site. A notification is visible that displays New access token created, followed by an indecipherable token.](media/bonusly-provisioning-tutorial/token02.png)
9. Upon populating the fields shown in Step 5, select **Test Connection** to ensure Microsoft Entra ID can connect to Bonusly. If the connection fails, ensure your Bonusly account has Admin permissions and try again.

    ![Screenshot of the Admin Credentials section. The Text connection button is highlighted.](media/bonusly-provisioning-tutorial/testconnection.png)
10. Select **Create** to create your configuration.
11. Select **Properties** in the **Overview** page.
12. Select the pencil to edit the properties. Enable notification emails and provide an email to receive quarantine emails. Enable accidental deletions prevention. Select **Apply** to save the changes.

    ![Screenshot of Provisioning properties.](common/provisioning-properties.png)
13. Select **Attribute Mapping** in the left panel and select **users**.
14. Review the user attributes that are synchronized from Microsoft Entra ID to Bonusly in the **Attribute Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Bonusly for update operations. Select the **Save** button to commit any changes.

    ![Screenshot of the Attribute Mappings page. A table lists Microsoft Entra attributes, corresponding Bonusly attributes, and the matching status.](media/bonusly-provisioning-tutorial/userattributemapping.png)
15. To configure scoping filters, refer to the following instructions provided in the [Scoping filter article](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts).
16. Use [on-demand provisioning](../app-provisioning/provision-on-demand) to validate sync with a small number of users before deploying more broadly in your organization.
17. When you're ready to provision, select **Start Provisioning** from the **Overview** page.