---
layout: Conceptual
title: Configure Jobscience for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/jobscience-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Jobscience.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 5b33462c-7842-6a98-7adc-05a25e3de357
document_version_independent_id: 8b85902b-093d-8eb7-1ea0-2827b944516e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/jobscience-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/jobscience-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/jobscience-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 07ff1b90-6f60-db48-2bd0-34368adc0b13
---

# Configure Jobscience for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Jobscience with Microsoft Entra ID.

Integrating Jobscience with Microsoft Entra ID provides you with the following benefits:

- You can control in Microsoft Entra ID who has access to Jobscience
- You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Microsoft Entra accounts
- You can manage your accounts in one central location - the Azure portal

If you want to know more details about SaaS app integration with Microsoft Entra ID, see [what is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A Jobscience single sign-on enabled subscription

Note

To test the steps in this article, we don't recommend using a production environment.

To test the steps in this article, you should follow these recommendations:

- don't use your production environment, unless it's necessary.
- If you don't have a Microsoft Entra trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description

In this article, you test Microsoft Entra single sign-on in a test environment. The scenario outlined in this article consists of two main building blocks:

1. Adding Jobscience from the gallery
2. Configuring and testing Microsoft Entra single sign-on

## Adding Jobscience from the gallery

To configure the integration of Jobscience into Microsoft Entra ID, you need to add Jobscience from the gallery to your list of managed SaaS apps.

**To add Jobscience from the gallery, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Jobscience** in the search box.
4. Select **Jobscience** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configuring and testing Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with Jobscience based on a test user called "Britta Simon."

For single sign-on to work, Microsoft Entra ID needs to know what the counterpart user in Jobscience is to a user in Microsoft Entra ID. In other words, a link relationship between a Microsoft Entra user and the related user in Jobscience needs to be established.

In Jobscience, assign the value of the **user name** in Microsoft Entra ID as the value of the **Username** to establish the link relationship.

To configure and test Microsoft Entra single sign-on with Jobscience, you need to complete the following building blocks:

1. **Configuring Microsoft Entra Single Sign-On** - to enable your users to use this feature.
2. **Creating a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
3. **Creating a Jobscience test user** - to have a counterpart of Britta Simon in Jobscience that's linked to the Microsoft Entra representation of user.
4. **Assigning the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
5. **Testing Single Sign-On** - to verify whether the configuration works.

### Configuring Microsoft Entra single sign-on

In this section, you enable Microsoft Entra single sign-on in the Azure portal and configure single sign-on in your Jobscience application.

**To configure Microsoft Entra single sign-on with Jobscience, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Jobscience** application integration page, select **Single sign-on**.

    ![Screenshot shows Single sign-on selected under Manage.](media/jobscience-tutorial/tutorial_general_04.png)
3. On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.
4. In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.my.salesforce.com`

    Note

    This value isn't real. Update this value with the actual Sign-On URL. Get this value by [Jobscience Client support team](https://www.bullhorn.com/technical-support/) or from the SSO profile you create which is explained later in the article.
5. On the **SAML Signing Certificate** section, select **Certificate (Base64)** and then save the certificate file on your computer.
6. Select the **Save** button.
7. On the **Jobscience Configuration** section, select **Configure Jobscience** to open **Configure sign-on** window. Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**
8. Log in to your Jobscience company site as an administrator.
9. Go to **Setup**.

    ![Screenshot shows the Setup item for your company.](media/jobscience-tutorial/ic784358.png)
10. On the left navigation pane, in the **Administer** section, select **Domain Management** to expand the related section, and then select **My Domain** to open the **My Domain** page.

    ![My Domain](media/jobscience-tutorial/ic767825.png)
11. To verify that your domain has been set up correctly, make sure that it's in "**Step 4 Deployed to Users**" and review your "**My Domain Settings**".

    ![Domain Deployed to User](media/jobscience-tutorial/ic784377.png)
12. On the Jobscience company site, select **Security Controls**, and then select **Single Sign-On Settings**.

    ![Screenshot shows Single Sign-On Settings selected from Security Controls.](media/jobscience-tutorial/ic784364.png)
13. In the **Single Sign-On Settings** section, perform the following steps:

    ![Single Sign-On Settings](media/jobscience-tutorial/ic781026.png)

    a. Select **SAML Enabled**.

    b. Select **New**.
14. On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:

    ![SAML Single Sign-On Setting](media/jobscience-tutorial/ic784365.png)

    a. In the **Name** textbox, type a name for your configuration.

    b. In **Issuer** textbox, paste the value of **SAML Entity ID**.

    c. In the **Entity Id** textbox, type `https://salesforce-jobscience.com`

    d. Select **Browse** to upload your Microsoft Entra certificate.

    e. As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.

    f. As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.

    g. In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**.

    h. In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**.

    i. Select **Save**.
15. On the left navigation pane, in the **Administer** section, select **Domain Management** to expand the related section, and then select **My Domain** to open the **My Domain** page.

    ![My Domain](media/jobscience-tutorial/ic767825.png)
16. On the **My Domain** page, in the **Login Page Branding** section, select **Edit**.

    ![Screenshot shows the Login Page Branding section with the Edit button.](media/jobscience-tutorial/ic767826.png)
17. On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed. Select it, and then select **Save**.

    ![Screenshot shows the Login Page Branding section with PPE and Save selected.](media/jobscience-tutorial/ic784366.png)
18. To get the SP initiated Single Sign on Login URL select the **Single Sign On settings** in the **Security Controls** menu section.

    ![Screenshot shows Administer Security Controls with Single Sign-On Settings selected.](media/jobscience-tutorial/ic784368.png)

    Select the SSO profile you have created in the step above. This page shows the Single Sign on URL for your company (for example, `https://companyname.my.salesforce.com?so=companyid`.

Tip

You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you're setting up the app! After adding this app from the **Active Directory &gt; Enterprise Applications** section, simply select the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom. You can read more about the embedded documentation feature here: [Microsoft Entra ID embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)

### Creating a Microsoft Entra test user

The objective of this section is to create a test user called Britta Simon.

![Create Microsoft Entra user](media/jobscience-tutorial/tutorial_general_100.png)

**To create a test user in Microsoft Entra ID, perform the following steps:**

1. In the Microsoft Entra admin center, navigate to **Entra ID** &gt; **Users**.

    ![Screenshot shows Users and groups selected from the Manage menu, with All users selected.](media/jobscience-tutorial/create_aaduser_02.png)
2. To open the **User** dialog, select **Add** on the top of the dialog.

    ![Screenshot shows the Add button to open the User dialog box.](media/jobscience-tutorial/create_aaduser_03.png)
3. On the **User** dialog page, perform the following steps:

    ![Screenshot shows the User dialog box where you can enter the values in this step.](media/jobscience-tutorial/create_aaduser_04.png)

    a. In the **Name** textbox, type **BrittaSimon**.

    b. In the **User name** textbox, type the **email address** of BrittaSimon.

    c. Select **Show Password** and write down the value of the **Password**.

    d. Select **Create**.

### Creating a Jobscience test user

In order to enable Microsoft Entra users to log in to Jobscience, they must be provisioned into Jobscience. In the case of Jobscience, provisioning is a manual task.

Note

You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Microsoft Entra user accounts.

**To configure user provisioning, perform the following steps:**

1. Log in to your **Jobscience** company site as administrator.
2. Go to Setup.

    ![Screenshot shows the Setup item.](media/jobscience-tutorial/ic784358.png)
3. Go to **Manage Users** &gt; **Users**.

    ![Users](media/jobscience-tutorial/ic784369.png)
4. Select **New User**.

    ![All Users](media/jobscience-tutorial/ic784370.png)
5. On the **Edit User** dialog, perform the following steps:

    ![User Edit](media/jobscience-tutorial/ic784371.png)

    a. In the **First Name** textbox, type a first name of the user like Britta.

    b. In the **Last Name** textbox, type a last name of the user like Simon.

    c. In the **Alias** textbox, type an alias name of the user like brittas.

    d. In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.

    e. In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.

    f. In the **Nick Name** textbox, type a nick name of user like Simon.

    g. Select **Save**.

Note

The Microsoft Entra account holder receives an email and follows a link to confirm their account before it becomes active.

### Assigning the Microsoft Entra test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.

![Screenshot shows an account display name.](media/jobscience-tutorial/tutorial_general_200.png)

**To assign Britta Simon to Jobscience, perform the following steps:**

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Jobscience**.

    ![Screenshot shows Jobscience selected.](media/jobscience-tutorial/tutorial_jobscience_app.png)
3. In the menu on the left, select **Users and groups**.

    ![Screenshot shows Users and Groups selected menu.](media/jobscience-tutorial/tutorial_general_202.png)
4. Select **Add** button. Then select **Users and groups** on **Add Assignment** dialog.

    ![Screenshot shows the Add button, used to add assignments.](media/jobscience-tutorial/tutorial_general_203.png)
5. On **Users and groups** dialog, select **Britta Simon** in the Users list.
6. Select **Select** button on **Users and groups** dialog.
7. Select **Assign** button on **Add Assignment** dialog.

### Testing single sign-on

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).