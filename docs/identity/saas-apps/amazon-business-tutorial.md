---
layout: Conceptual
title: Configure Amazon Business for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/amazon-business-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Amazon Business.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 4b612c20-6995-2ae5-5d73-ef54ccf4afa2
document_version_independent_id: cfda3f69-819a-8e44-718e-e718e8eb0806
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/amazon-business-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/amazon-business-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/amazon-business-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: e0d66240-571b-4f98-9d71-2c6adc9bc02a
---

# Configure Amazon Business for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Amazon Business with Microsoft Entra ID. When you integrate Amazon Business with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Amazon Business.
- Enable your users to be automatically signed-in to Amazon Business with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An Amazon Business single sign-on (SSO) enabled subscription. Go to the [Amazon Business](https://business.amazon.com) page to create an Amazon Business account.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in an existing Amazon Business account.

- Amazon Business supports **SP and IDP** initiated SSO.
- Amazon Business supports **Just In Time** user provisioning.
- Amazon Business supports [Automated user provisioning](amazon-business-provisioning-tutorial).

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Amazon Business from the gallery

To configure the integration of Amazon Business into Microsoft Entra ID, you need to add Amazon Business from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Amazon Business** in the search box.
4. Select **Amazon Business** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Amazon Business

Configure and test Microsoft Entra SSO with Amazon Business using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Amazon Business.

To configure and test Microsoft Entra SSO with Amazon Business, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Amazon Business SSO**- to configure the single sign-on settings on application side.
    1. **Create Amazon Business test user** - to have a counterpart of B.Simon in Amazon Business that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Amazon Business** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure in **IDP** initiated mode, perform the following steps:

    1. In the **Identifier (Entity ID)** text box, type one of the following URLs:

        | URL | Region |
        | --- | --- |
        | `https://www.amazon.com` | North America |
        | `https://www.amazon.co.jp` | East Asia |
        | `https://www.amazon.de` | Europe |
    2. In the **Reply URL** text box, type a URL using one of the following patterns:

        | URL | Region |
        | --- | --- |
        | `https://www.amazon.com/bb/feature/sso/action/3p_redirect?idpid={idpid}` | North America |
        | `https://www.amazon.co.jp/bb/feature/sso/action/3p_redirect?idpid={idpid}` | East Asia |
        | `https://www.amazon.de/bb/feature/sso/action/3p_redirect?idpid={idpid}` | Europe |

        Note

        The Reply URL value isn't real. Update this value with the actual Reply URL. You get the `<idpid>` value from the Amazon Business SSO configuration section, which is explained later in the article. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. If you want to configure the application in **SP** initiated mode, you need to add the full URL provided in the Amazon Business configuration to the **Sign-on URL** in the **Set additional URLs** section.
7. The following screenshot shows the list of default attributes. Edit the attributes by selecting the **pencil** icon in the **User Attributes & Claims** section.

    ![Screenshot shows User Attributes &amp; Claims with default values such as Givenname user.givenname and Emailaddress user.mail.](media/amazon-business-tutorial/map-attribute.png)
8. Edit Attributes and copy **Namespace** value of these attributes into the Notepad.

    ![Screenshot shows User Attributes &amp; Claims with columns for Claim name and value.](media/amazon-business-tutorial/attribute.png)
9. In addition to above, Amazon Business application expects few more attributes to be passed back in SAML response. In the **User Attributes & Claims** section on the **Group Claims** dialog, perform the following steps:

    1. Select the **pen** next to **Groups returned in claim**.

        ![Screenshot shows User Attributes &amp; Claims with the icon for Groups returned in claim selected.](media/amazon-business-tutorial/claim.png)
    2. In the **Group Claims** dialog, select **All Groups** from the radio list.
    3. Select **Group ID** as **Source attribute**.
    4. Check **Customize the name of the group claim** checkbox and enter the group name according to your Organization requirement.
    5. Select **Save**.
10. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![The Certificate download link](common/copy-metadataurl.png)
11. On the **Set up Amazon Business** section, copy the appropriate URLs based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

### Assign the Microsoft Entra Security Group in the Azure portal

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Amazon Business**.
3. In the applications list, type and select **Amazon Business**.
4. In the menu on the left, select **Users and groups**.
5. Select the **Added user**.
6. Search for the Security Group you want to use, then select the group to add it to the Select members section. Select **Select**, then select **Assign**.

    ![Search Security Group](media/amazon-business-tutorial/assign-group.png)

    Note

    Check the notifications in the menu bar to be notified that the Group was successfully assigned to the Enterprise application.

## Configure Amazon Business SSO

1. In a different web browser window, sign in to your up Amazon Business company site as an administrator
2. Select the **User Profile** and select **Business Settings**.

    ![User Profile](media/amazon-business-tutorial/user-profile.png)
3. On the **System integrations** wizard, select **Single Sign-On (SSO)**.

    ![Single Sign-On (SSO)](media/amazon-business-tutorial/sso-settings.png)
4. On the **Set up SSO** wizard, select the provider according to your Organizational requirements and select **Next**.

    Note

    Although Microsoft ADFS is a listed option, it won't work with Microsoft Entra SSO.
5. On the **New user account defaults** wizard, select the **Default Group** and then select **Default Buying Role** according to user role in your Organization and select **Next**.

    ![Screenshot shows New user account defaults with Microsoft S S O, Requisitioner, and Next selected.](media/amazon-business-tutorial/group.png)
6. On the **Upload your metadata file** wizard, choose **Paste XML Link** option to paste the **App Federation Metadata URL** value, and select **Validate**.

    Note

    Alternatively, you can also upload the **Federation Metadata XML** file by selecting the **Upload XML File** option.
7. After uploading the downloaded metadata file, the fields in the **Connection data** section populates automatically. After that select **Next**.
8. On the **Upload your Attribute statement** wizard, select **Skip**.

    ![Screenshot shows Upload your Attribute statement, which allows you to browse to an attribute statement, but in this case, select Skip.](media/amazon-business-tutorial/upload-attribute.png)
9. On the **Attribute mapping** wizard, add the requirement fields by selecting the **+ Add a field** option. Add the attribute values including the namespace, which you have copied from the **User Attributes & Claims** section of Azure portal into the **SAML AttributeName** field, and select **Next**.

    ![Screenshot shows Attribute mapping, where you can edit your Amazon data SAML attribute names.](media/amazon-business-tutorial/attribute-mapping.png)
10. On the **Amazon connection data** wizard, please confirm your IDP has configured and select **Continue**.

    ![Screenshot shows Amazon connection data, where you can select next to continue.](media/amazon-business-tutorial/amazon-connect.png)
11. Check the **Status** of the steps that have been configured and select **Start testing**.
12. On the **Test SSO Connection** wizard, select **Test**.

    ![Screenshot shows Test S S O Connection with the Test button.](media/amazon-business-tutorial/test.png)
13. On the **IDP initiated URL** wizard, before you select **Activate**, copy the value, which is assigned to **idpid** and paste into the **idpid** parameter in the **Reply URL** in the **Basic SAML Configuration** section.

    ![Screenshot shows I D P initiated U R L where you can get a U R L necessary for testing and then select Activate.](media/amazon-business-tutorial/activate.png)
14. On the **Are you ready to switch to active SSO?** wizard, check **I have fully tested SSO and am ready to go live** checkbox and select **Switch to active**.

    ![Screenshot shows the Are you ready to switch to active S S O confirmation where you can select Switch to active.](media/amazon-business-tutorial/switch-active.png)
15. Finally in the **SSO Connection Details** section the **Status** is shown as **Active**.

    Note

    If you want to configure the application in **SP** initiated mode, complete the following step, paste the sign-on URL from the screenshot above in the **Sign-on URL** text box of the **Set additional URLs** section. Use the following format:

    `https://www.amazon.<TLD>/bb/feature/sso/action/start?domain_hint=<UNIQUE_ID>`

### Create Amazon Business test user

In this section, a user called B.Simon is created in Amazon Business. Amazon Business supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in Amazon Business, a new one is created after authentication.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to Amazon Business Sign-on URL where you can initiate the sign-in flow.
- Go to the Amazon Business Single Sign-on URL directly and initiate the sign-in flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the Amazon Business for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the Amazon Business tile in the My Apps, if configured in SP mode you would be redirected to the application sign-on page for initiating the sign-in flow and if configured in IDP mode, you should be automatically signed in to the Amazon Business for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Reconfiguring Service Provider Settings from ADFS to Microsoft Entra ID

1. Prepare Microsoft Entra ID Environment

    1. Verify Microsoft Entra ID Premium Subscription Ensure you have a Microsoft Entra ID Premium subscription, which is required for single sign-on (SSO) and other advanced features.
2. Register the Application in Microsoft Entra ID

    1. Navigate to Microsoft Entra ID in the Azure portal.
    2. Select "App registrations" &gt; "New registration".
    3. Fill in the required details:
        1. Name: Enter a meaningful name for the application.
        2. Supported account types: Choose the appropriate option for your environment.
        3. Redirect URI: Enter the necessary redirect URIs (usually your application’s sign-in URL).
3. Configure Microsoft Entra ID SSO

    1. Set Up single sign-on in Microsoft Entra ID.
    2. In the Azure portal, go to Microsoft Entra ID &gt; Enterprise applications.
    3. Select your application from the list.
    4. Under "Manage", select "Single sign-on".
    5. Choose "SAML" as the Single Sign-On method.
    6. Edit the Basic SAML Configuration:
        1. Identifier (Entity ID): Enter the SP Entity ID.
        2. Reply URL (Assertion Consumer Service URL): Enter the SP ACS URL.
        3. Sign on URL: Enter the application sign-on URL if applicable.
4. Configure User Attributes & Claims

    1. In the SAML-based Sign-On settings, select "User Attributes & Claims".
    2. Edit and configure claims to match those required by your SP. Typically, this includes:
        1. NameIdentifier
        2. Email
        3. GivenName
        4. Surname
        5. etc.
5. Download Microsoft Entra ID SSO Metadata
6. In the SAML Signing Certificate section, download the Federation Metadata XML. This is used to configure your SP.
7. Reconfigure Service Provider (SP)

    1. Update SP to Use Microsoft Entra ID Metadata
    2. Access your SP’s configuration settings.
    3. Update the IdP metadata URL or upload the Microsoft Entra ID Metadata XML.
    4. Update the Assertion Consumer Service (ACS) URL, Entity ID, and any other required fields to match the Microsoft Entra ID configuration.
8. Configure SAML Certificates
9. Ensure that the SP is configured to trust the signing certificate from Microsoft Entra ID. This can be found in the SAML Signing Certificate section of the Microsoft Entra ID SSO configuration.
10. Test SSO Configuration
11. Initiate a test login from the SP.
12. Verify that the authentication redirects to Microsoft Entra ID and successfully logs in the user.
13. Check the claims being passed to ensure they match what the SP expects.
14. Update DNS and Network Settings (If Applicable). If your SP or application uses DNS settings specific to ADFS, you might need to update these settings to point to Microsoft Entra ID endpoints.
15. Roll out and Monitor

    1. Communicate with Users Notify your users of the change and provide any necessary instructions or documentation.
    2. Monitor Authentication Logs Keep an eye on the Microsoft Entra ID sign-in logs to monitor for any authentication issues and address them promptly.