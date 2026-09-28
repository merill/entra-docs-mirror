---
layout: Conceptual
title: Configure BeyondTrust Remote Support for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/bomgarremotesupport-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and BeyondTrust Remote Support.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: d6503f86-e458-5662-f0ab-4ca8747726d3
document_version_independent_id: fc25025e-2da7-c708-d1c2-e32cbee3ccf9
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/bomgarremotesupport-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/bomgarremotesupport-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/bomgarremotesupport-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0f40743a-1518-76f1-1aa8-079e30209f5f
---

# Configure BeyondTrust Remote Support for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate BeyondTrust Remote Support with Microsoft Entra ID. When you integrate BeyondTrust Remote Support with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to BeyondTrust Remote Support.
- Enable your users to be automatically signed-in to BeyondTrust Remote Support with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- BeyondTrust Remote Support single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- BeyondTrust Remote Support supports **SP** initiated SSO
- BeyondTrust Remote Support supports **Just In Time** user provisioning

## Adding BeyondTrust Remote Support from the gallery

To configure the integration of BeyondTrust Remote Support into Microsoft Entra ID, you need to add BeyondTrust Remote Support from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **BeyondTrust Remote Support** in the search box.
4. Select **BeyondTrust Remote Support** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for BeyondTrust Remote Support

Configure and test Microsoft Entra SSO with BeyondTrust Remote Support using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in BeyondTrust Remote Support.

To configure and test Microsoft Entra SSO with BeyondTrust Remote Support, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure BeyondTrust Remote Support SSO**- to configure the single sign-on settings on application side.
    - **Create BeyondTrust Remote Support test user** - to have a counterpart of B.Simon in BeyondTrust Remote Support that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **BeyondTrust Remote Support** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Identifier** box, type a URL using the following pattern: `https://<HOSTNAME>.bomgar.com`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<HOSTNAME>.bomgar.com/saml/sso`

    c. In the **Sign-on URL** text box, type a URL using the following pattern: `https://<HOSTNAME>.bomgar.com/saml`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-On URL. You get these values explained later in the article.
6. BeyondTrust Remote Support application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/default-attributes.png)
7. In addition to above, BeyondTrust Remote Support application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.

    | Name | Source Attribute |
    | --- | --- |
    | Username | user.userprincipalname |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.mail |
    | Groups | user.groups |

    Note

    When assigning Microsoft Entra groups for the BeyondTrust Remote Support application, the ‘Groups returned in claim’ option will need to be modified from None to SecurityGroup. The Groups are imported into the application as their Object IDs. The Object ID of the Microsoft Entra group can be found by checking the Properties in the Microsoft Entra ID interface. This are required to reference and assign Microsoft Entra groups to the correct group policies.
8. When setting the Unique User Identifier, this value must be set to NameID-Format: **Persistent**. We require this to be a Persistent identifier to correctly identify and associate the user into the correct group policies for permissions. Select the edit icon to open the **User Attributes & Claims** dialog to edit the Unique User Identifier value.
9. On the **Manage Claim** section, select the **Choose name identifier format** and set the value to **Persistent** and select **Save**.

    ![User Attributes and Claims](media/bomgarremotesupport-tutorial/attribute-unique-user-identifier.png)
10. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
11. On the **Set up BeyondTrust Remote Support** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure BeyondTrust Remote Support SSO

1. In a different web browser window, sign in to BeyondTrust Remote Support as an Administrator.
2. Navigate to **Users & Security** &gt; **Security Providers**.
3. Select **Edit** icon in the **SAML Providers**.

    ![SAML Providers edit icon](media/bomgarremotesupport-tutorial/saml-providers.png)
4. Expand the **Service Provider Settings** section.
5. Select **Download Service Provider Metadata** or you can copy the **Entity ID** and **ACS URL** values and use these values in the **Basic SAML Configuration** section.

    ![Download Service Provider Metadata](media/bomgarremotesupport-tutorial/service-provider-metadata.png)
6. Under the Identity Provider Settings section, select **Upload Identity Provider Metadata** and locate the Metadata XML file that you have downloaded.
7. The **Entity ID**, **Single Sign-On Service URL** and **Server Certificate** will automatically be uploaded, and the **SSO URL Protocol Binding** will need to be changed to **HTTP POST**.

    ![Screenshot shows the Identity Provider Settings section where you perform these actions.](media/bomgarremotesupport-tutorial/identity-provider.png)
8. Select **Save**.

### Create BeyondTrust Remote Support test user

In this section, a user called Britta Simon is created in BeyondTrust Remote Support. BeyondTrust Remote Support supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in BeyondTrust Remote Support, a new one is created after authentication.

Follow the below procedure, which is mandatory for configuring the BeyondTrust Remote Support.

We is configuring the User Provision Settings here. The values used in this section is referenced from the **User Attributes & Claims** section. We configured this to be the default values which are already imported at the time of creation, however, the value can be customized if necessary.

![Screenshot shows the User Provision Settings where you can configure user values.](media/bomgarremotesupport-tutorial/user-attribute.png)

Note

The groups and e-mail attribute aren't necessary for this implementation. If utilizing Microsoft Entra groups and assigning them to BeyondTrust Remote Support Group Policies for permissions, the Object ID of the group will need to be referenced via its properties in the Azure portal and placed in the ‘Available Groups’ section. Once this has been completed, the Object ID/AD Group will now be available for assignment to a group policy for permissions.

![Screenshot shows the I T section with Membership type, Source, Type, and Object I D.](media/bomgarremotesupport-tutorial/config-user-2.png)

![Screenshot shows the Basic Settings page for a group policy.](media/bomgarremotesupport-tutorial/group-policy.png)

Note

Alternatively, a default group policy can be set on the SAML2 Security Provider. By defining this option, this will assign all users who authenticate through SAML the permissions specified within the group policy. The General Members policy is included within BeyondTrust Remote Support/Privileged Remote Access with limited permissions, which can be used to test authentication and assign users to the correct policies. Users aren't populate into the SAML2 Users list via /login &gt; Users & Security until the first successful authentication attempt. Additional information on Group policies can be found at the following link: `https://www.beyondtrust.com/docs/remote-support/getting-started/admin/group-policies.htm`

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to BeyondTrust Remote Support Sign-on URL where you can initiate the login flow.
- Go to BeyondTrust Remote Support Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the BeyondTrust Remote Support tile in the My Apps, this option redirects to BeyondTrust Remote Support Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).