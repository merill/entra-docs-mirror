---
layout: Conceptual
title: Configure SAP HANA for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/saphana-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAP HANA.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6dfbc478-857d-93fe-8a6f-03259c627a78
document_version_independent_id: bec33d45-4291-873e-b741-67f799fbc00f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/saphana-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/saphana-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/saphana-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d3579643-b983-b452-dc1e-bdd11233b4d5
---

# Configure SAP HANA for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAP HANA with Microsoft Entra ID. When you integrate SAP HANA with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SAP HANA.
- Enable your users to be automatically signed-in to SAP HANA with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- A SAP HANA subscription that's single sign-on (SSO) enabled
- A HANA instance that's running on any public IaaS, on-premises, Azure VM, or SAP large instances in Azure
- The XSA Administration web interface, and HANA Studio installed on the HANA instance

Note

We don't recommend using a production environment of SAP HANA to test the steps in this article. Test the integration first in the development or staging environment of the application, and then use the production environment.

To test the steps in this article, follow these recommendations:

- A Microsoft Entra subscription. If you don't have a Microsoft Entra environment, you can get one-month trial [here](https://azure.microsoft.com/pricing/free-trial/)
- SAP HANA single sign-on enabled subscription

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- SAP HANA supports **IDP** initiated SSO.
- SAP HANA supports **just-in-time** user provisioning.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Adding SAP HANA from the gallery

To configure the integration of SAP HANA into Microsoft Entra ID, you need to add SAP HANA from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAP HANA** in the search box.
4. Select **SAP HANA** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SAP HANA

Configure and test Microsoft Entra SSO with SAP HANA using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SAP HANA.

To configure and test Microsoft Entra SSO with SAP HANA, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure SAP HANA SSO**- to configure the single sign-on settings on application side.
    1. **Create SAP HANA test user** - to have a counterpart of Britta Simon in SAP HANA that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAP HANA** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    In the **Reply URL** text box, type a URL using the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    Note

    The Reply URL value isn't real. Update the value with the actual Reply URL. Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) to get the values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. SAP HANA application expects the SAML assertions in a specific format. Configure the following claims for this application. You can manage the values of these attributes from the **User Attributes** section on application integration page. On the **Set up Single Sign-On with SAML** page, select **Edit** button to open **User Attributes** dialog.

    ![Screenshot that shows the &quot;User Attributes&quot; section with the &quot;Edit&quot; icon selected.](common/edit-attribute.png)
7. In the **User attributes** section on the **User Attributes & Claims** dialog, perform the following steps:

    a. Select **Edit icon** to open the **Manage user claims** dialog.

    ![Screenshot that shows the &quot;User Attributes &amp; Claims&quot; dialog with the &quot;Edit&quot; icon selected.](media/saphana-tutorial/tutorial_usermail.png)

    ![image](media/saphana-tutorial/tutorial_usermailedit.png)

    b. From the **Transformation** list, select **ExtractMailPrefix()**.

    c. From the **Parameter 1** list, select **user.mail**.

    d. Select **Save**.
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAP HANA SSO

1. To configure single sign-on on the SAP HANA side, sign in to your **HANA XSA Web Console** by going to the respective HTTPS endpoint.

    Note

    In the default configuration, the URL redirects the request to a sign-in screen, which requires the credentials of an authenticated SAP HANA database user. The user who signs in must have permissions to perform SAML administration tasks.
2. In the XSA Web Interface, go to **SAML Identity Provider**. From there, select the **+** button on the bottom of the screen to display the **Add Identity Provider Info** pane. Then take the following steps:

    ![Add Identity Provider](media/saphana-tutorial/sap1.png)

    a. In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML (which you downloaded) into the **Metadata** box.

    ![Screenshot that shows the &quot;Add Identity Provider Info&quot; pane with the &quot;Metadata&quot; and &quot;Name&quot; boxes highlighted.](media/saphana-tutorial/sap-2.png)

    b. If the contents of the XML document are valid, the parsing process extracts the information that's required for the **Subject, Entity ID, and Issuer** fields in the **General data** screen area. It also extracts the information that's necessary for the URL fields in the **Destination** screen area, for example, the **Base URL and SingleSignOn URL (\*)** fields.

    ![Add Identity Provider settings](media/saphana-tutorial/sap3.png)

    c. In the **Name** box of the **General Data** screen area, enter a name for the new SAML SSO identity provider.

    Note

    The name of the SAML IDP is mandatory and must be unique. It appears in the list of available SAML IDPs that's displayed when you select SAML as the authentication method for SAP HANA XS applications to use. For example, you can do this in the **Authentication** screen area of the XS Artifact Administration tool.
3. Select **Save** to save the details of the SAML identity provider and to add the new SAML IDP to the list of known SAML IDPs.

    ![Save button](media/saphana-tutorial/sap4.png)
4. In HANA Studio, within the system properties of the **Configuration** tab, filter the settings by **saml**. Then adjust the **assertion\_timeout** from **10 sec** to **120 sec**.

    ![assertion_timeout setting](media/saphana-tutorial/sap7.png)

### Create SAP HANA test user

To enable Microsoft Entra users to sign in to SAP HANA, you must provision them in SAP HANA. SAP HANA supports **just-in-time provisioning**, which is by enabled by default.

If you need to create a user manually, take the following steps:

Note

You can change the external authentication that the user uses. They can authenticate with an external system such as Kerberos. For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).

1. Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator, and then enable the DB-User for SAML SSO.
2. Select the invisible check box to the left of **SAML**, and then select the **Configure** link.
3. Select **Add** to add the SAML IDP. Select the appropriate SAML IDP, and then select **OK**.
4. Add the **External Identity** (in this case, BrittaSimon). Then select **OK**.

    Note

    You must populate the **External Identity** field for the user, and that value needs to match the **NameID** field in the SAML token from Microsoft Entra ID. The **Any** checkbox shouldn't be checked, as this option requires the IDP to send a **SPProviderID** property in the NameID Field, which is currently not supported by Microsoft Entra ID. For more information, see [Single Sign-On Using SAML 2.0](https://help.sap.com/viewer/b3ee5778bc2e4a089d3299b82ec762a7/2.0.05/en-US/db6db355bb571014b56eb25057daec5f.html).
5. For testing purposes, assign all **XS** roles to the user.

    ![Assigning roles](media/saphana-tutorial/sap6.png)

    Tip

    You should give permissions that are appropriate for your use cases only.
6. Save the user.

### Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the SAP HANA for which you set up the SSO
- You can use Microsoft My Apps. When you select the SAP HANA tile in the My Apps, you should be automatically signed in to the SAP HANA for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).