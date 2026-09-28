---
layout: Conceptual
title: Configure E Sales Manager Remix for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/esalesmanagerremix-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and E Sales Manager Remix.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 47ef3f1e-3c47-d153-da31-33a9be8d7d12
document_version_independent_id: c822b63c-8766-f057-e296-13f1f51899e2
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/esalesmanagerremix-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/esalesmanagerremix-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/esalesmanagerremix-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: faf886bb-66cb-6dee-0775-c17b560ac84d
---

# Configure E Sales Manager Remix for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Microsoft Entra ID with E Sales Manager Remix.

By integrating Microsoft Entra ID with E Sales Manager Remix, you get the following benefits:

- You can control in Microsoft Entra ID who has access to E Sales Manager Remix.
- You can enable your users to get signed in automatically to E Sales Manager Remix (single sign-on, or SSO) with their Microsoft Entra accounts.
- You can manage your accounts in one central location, the Azure portal.

To learn more about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID?](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

To configure Microsoft Entra integration with E Sales Manager Remix, you need the following items:

- A Microsoft Entra subscription
- An E Sales Manager Remix SSO-enabled subscription

Note

When you test the steps in this article, we recommend that you do *not* use a production environment.

To test the steps in this article, follow these recommendations:

- don't use your production environment, unless it's necessary.
- If you don't have a Microsoft Entra trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).

## Scenario description

In this article, you test Microsoft Entra single sign-on in a test environment.

The scenario outlined in this article consists of two main building blocks:

- Adding E Sales Manager Remix from the gallery
- Configuring and testing Microsoft Entra single sign-on

## Add E Sales Manager Remix from the gallery

To configure the integration of Microsoft Entra ID with E Sales Manager Remix, add E Sales Manager Remix from the gallery to your list of managed SaaS apps by doing the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. To add a new application, select **New application** at the top of the window.

    ![The New application button](media/esalesmanagerremix-tutorial/tutorial_general_03.png)
4. In the search box, type **E Sales Manager Remix**, select **E Sales Manager Remix** in the results list, and then select **Add**.

    ![E Sales Manager Remix in the results list](media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_addfromgallery.png)

## Configure and test Microsoft Entra single sign-on

In this section, you configure and test Microsoft Entra single sign-on with E Sales Manager Remix, based on a test user called "Britta Simon."

For single sign-on to work, Microsoft Entra ID needs to identify the E Sales Manager Remix user and its counterpart in Microsoft Entra ID. In other words, a link relationship between a Microsoft Entra user and the same user in E Sales Manager Remix must be established.

To configure and test Microsoft Entra single sign-on with E Sales Manager Remix, complete the building blocks in the next five sections:

### Configure Microsoft Entra single sign-on

Enable Microsoft Entra single sign-on in the Azure portal and configure single sign-on in your E Sales Manager Remix application by doing the following:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **E Sales Manager Remix** application integration page, select **Single sign-on**.

    ![The &quot;Single sign-on&quot; link](media/esalesmanagerremix-tutorial/tutorial_general_04.png)
3. In the **Single sign-on** window, in the **Single Sign-on Mode** box, select **SAML-based Sign-on**.
4. Under **E Sales Manager Remix Domain and URLs**, do the following:

    a. In the **Sign-on URL** box, type a URL in the following format: *https://&lt;Server-Based-URL&gt;/&lt;sub-domain&gt;/esales-pc*.

    b. In the **Identifier** box, type a URL in the following format: *https://&lt;Server-Based-URL&gt;/&lt;sub-domain&gt;/*.

    c. Note the **Identifier** value for later use in this article.

    Note

    The preceding values aren't real. Update them with the actual sign-in URL and identifier. To obtain the values, contact [E Sales Manager Remix Client support team](mailto:esupport@softbrain.co.jp).
5. Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.
6. Select the **View and edit all other user attributes** check box, and then select the **emailaddress** attribute.

    ![The User Attributes window](media/esalesmanagerremix-tutorial/configure1.png)

    The **Edit Attribute** window opens.
7. Copy the **Namespace** and **Name** values. Generate the value in the pattern *&lt;Namespace&gt;/&lt;Name&gt;*, and save it for later use in this article.

    ![The Edit Attribute window](media/esalesmanagerremix-tutorial/configure2.png)
8. Under **E Sales Manager Remix Configuration**, select **Configure E Sales Manager Remix**.

    The **Configure sign-on** window opens.
9. In the **Quick Reference** section, copy the sign-out URL and the SAML single sign-on service URL.
10. Select **Save**.

    ![The Save button](media/esalesmanagerremix-tutorial/tutorial_general_400.png)
11. Sign in to your E Sales Manager Remix application as an administrator.
12. At the top right, select **To Administrator Menu**.

    ![The &quot;To Administrator Menu&quot; command](media/esalesmanagerremix-tutorial/configure4.png)
13. In the left pane, select **System settings** &gt; **Cooperation with external system**.

    ![The &quot;System settings&quot; and &quot;Cooperation with external system&quot; links](media/esalesmanagerremix-tutorial/configure5.png)
14. In the **Cooperation with external system** window, select **SAML**.

    ![The &quot;Cooperation with external system&quot; window](media/esalesmanagerremix-tutorial/configure6.png)
15. Under **SAML authentication setting**, do the following:

    ![The &quot;SAML authentication setting&quot; section](media/esalesmanagerremix-tutorial/configure3.png)

    a. Select the **PC version** check box.

    b. In the **Collaboration item** section, in the drop-down list, select **email**.

    c. In the **Collaboration item** box, paste the claim value that you copied earlier (that is, **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`**).

    d. In the **Issuer (entity ID)** box, paste the identifier value that you copied earlier from the **E Sales Manager Remix Domain and URLs** section.

    e. To upload your downloaded certificate, select **File selection**.

    f. In the **ID provider login URL** box, paste the SAML single sign-on service URL that you copied earlier.

    g. In **Identity Provider Logout URL** box, paste the sign-out URL value that you copied earlier.

    h. Select **Setting complete**.

Tip

As you're setting up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com). After you've added the app in the **Active Directory** &gt; **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation in the **Configuration** section at the bottom. For more information about the embedded documentation feature, see [Microsoft Entra ID embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).

### Create a Microsoft Entra test user

In this section, you create test user.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Create an E Sales Manager Remix test user

1. Sign on to your E Sales Manager Remix application as an administrator.
2. Select **To Administrator Menu** from the menu at the top right.

    ![E Sales Manager Remix Configuration](media/esalesmanagerremix-tutorial/configure4.png)
3. Select **Your company's settings** &gt; **Maintenance of departments and employees**, and then select **Employees registered**.

    ![The &quot;Employees registered&quot; tab](media/esalesmanagerremix-tutorial/user1.png)
4. In the **New employee registration** section, do the following:

    ![The &quot;New employee registration&quot; section](media/esalesmanagerremix-tutorial/user2.png)

    a. In the **Employee Name** box, type the name of the user (for example, **Britta**).

    b. Complete the remaining required fields.

    c. If you enable SAML, the administrator can't sign in from the sign-in page. Grant administrator sign-in privileges to the user by selecting the **Admin Login** check box.

    d. Select **Registration**.
5. In the future, to sign in as an administrator, sign in as the user who has administrator permissions and then, at the top right, select **To Administrator Menu**.

    ![The &quot;To Administrator Menu&quot; command](media/esalesmanagerremix-tutorial/configure4.png)

### Assign the Microsoft Entra test user

In this section, you enable user Britta Simon to use Azure single sign-on by granting access to E Sales Manager Remix. To do so, do the following:

![Assign the user role](media/esalesmanagerremix-tutorial/tutorial_general_200.png)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. In the **Applications** list, select **E Sales Manager Remix**.

    ![The E Sales Manager Remix link](media/esalesmanagerremix-tutorial/tutorial_esalesmanagerremix_app.png)
4. In the left pane, select **Users and groups**.

    ![The &quot;Users and groups&quot; link](media/esalesmanagerremix-tutorial/tutorial_general_202.png)
5. Select **Add** and then, in the **Add Assignment** pane, select **Users and groups**.

    ![The Add Assignment pane](media/esalesmanagerremix-tutorial/tutorial_general_203.png)
6. In the **Users and groups** window, in the **Users** list, select **Britta Simon**.
7. Select the **Select** button.
8. In the **Add Assignment** window, select **Assign**.

### Test single sign-on

In this section, you test your Microsoft Entra single sign-on configuration by using the Access Panel.

When you select the E Sales Manager Remix tile in the Access Panel, you should be signed in automatically to your E Sales Manager Remix application.

For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).