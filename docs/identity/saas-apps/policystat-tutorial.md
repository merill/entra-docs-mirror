---
layout: Conceptual
title: Configure PolicyStat for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/policystat-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and PolicyStat.
ms.topic: how-to
ms.date: 2026-06-09T00:00:00.0000000Z
locale: en-us
document_id: db7eddfb-65de-1d04-e900-8a3465ea86ea
document_version_independent_id: e91fc006-91e0-ff36-cb1c-3eb5746a87c1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/policystat-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/policystat-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/policystat-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fdd003ee-8d22-e722-4679-baf067aa92e5
---

# Configure PolicyStat for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate PolicyStat with Microsoft Entra ID. When you integrate PolicyStat with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to PolicyStat.
- Enable your users to be automatically signed-in to PolicyStat with their Microsoft Entra accounts.
- Manage your accounts in one central location.

PolicyStat is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- PolicyStat single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- PolicyStat supports **SP** initiated SSO.
- PolicyStat supports **Just In Time** user provisioning.

## Add PolicyStat from the gallery

To configure the integration of PolicyStat into Microsoft Entra ID, you need to add PolicyStat from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **PolicyStat** in the search box.
4. Select **PolicyStat** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for PolicyStat

Configure and test Microsoft Entra SSO with PolicyStat using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in PolicyStat.

To configure and test Microsoft Entra SSO with PolicyStat, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure PolicyStat SSO**- to configure the single sign-on settings on application side.
    1. **Create PolicyStat test user** - to have a counterpart of B.Simon in PolicyStat that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **PolicyStat** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    1. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`
    2. In the **Sign on URL** text box, type a URL using the following pattern: `https://<companyname>.policystat.com`

        Note

        These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [PolicyStat Client support team](https://rldatix.com/en-apac/customer-success/community/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. Your PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes. Select **Edit** icon to open **User Attributes** dialog.

    ![Screenshot that shows the &quot;User Attributes&quot; dialog with the &quot;Edit&quot; icon selected.](common/edit-attribute.png)
8. In addition to above, PolicyStat application expects few more attributes to be passed back in SAML response. In the **User Claims** section on the **User Attributes** dialog, perform the following steps to add SAML token attribute as shown in the below table:

    | Name | Source Attribute |
    | --- | --- |
    | uid | ExtractMailPrefix([mail]) |

    1. Select **Add new claim** to open the **Manage user claims** dialog.

        ![Screenshot that shows the &quot;User claims&quot; section with the &quot;Add new claim&quot; and &quot;Save&quot; actions highlighted.](common/new-save-attribute.png)

        ![Screenshot that shows the &quot;Manage user claims&quot; dialog with the &quot;Name&quot;, &quot;Transformation&quot;, and &quot;Parameter&quot; text boxes highlighted, and the &quot;Save&quot; button selected.](media/policystat-tutorial/claims.png)
    2. In the **Name** textbox, type the attribute name shown for that row.
    3. Leave the **Namespace** blank.
    4. Select Source as **Transformation**.
    5. From the **Transformation** list, type the attribute value shown for that row.
    6. From the **Parameter 1** list, type the attribute value shown for that row.
    7. Select **Save**.
9. On the **Set up PolicyStat** section, copy the appropriate URL(s) as per your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure PolicyStat SSO

1. In a different web browser window, log in to your PolicyStat company site as an administrator.
2. Select the **Admin** tab, and then select **Single Sign-On Configuration** in left navigation pane.

    ![Administrator Menu](media/policystat-tutorial/admin.png)
3. Select **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:

    ![Screenshot that shows the &quot;Your I D P Metadata&quot; action selected.](media/policystat-tutorial/metadata.png)

    1. Open your downloaded metadata file, copy the content, and then paste it into the **Your Identity Provider Metadata** textbox.
    2. Select **Save Changes**.
4. Select **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps using the **CLAIM NAMES** found in your Azure configuration:

    1. In the **Username Attribute** textbox, type the username claim value you're passing over as the key username attribute. The default value in Azure is UPN, but if you already have accounts in PolicyStat, you need to match those username values to avoid duplicate accounts or update the existing accounts in PolicyStat to the UPN value. To update existing usernames in bulk, please contact RLDatix PolicyStat Support https://websupport.rldatix.com/support-form/. Default value to enter to pass the UPN **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`** .
    2. In the **First Name Attribute** textbox, type the First Name Attribute claim name from Azure **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`**.
    3. In the **Last Name Attribute** textbox, type the Last Name Attribute claim name from Azure **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`**.
    4. In the **Email Attribute** textbox, type the Email Attribute claim name from Azure **`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`**.
    5. Select **Save Changes**.
5. In the **Setup** section, select **Enable Single Sign-on Integration**.

    ![Single Sign-On Configuration](media/policystat-tutorial/attributes.png)

### Create PolicyStat test user

In this section, a user called Britta Simon is created in PolicyStat. PolicyStat supports just-in-time user provisioning, which is enabled by default. There's no action item for you in this section. If a user doesn't already exist in PolicyStat, a new one is created after authentication.

Note

You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Microsoft Entra user accounts.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to PolicyStat Sign-on URL where you can initiate the login flow.
- Go to PolicyStat Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the PolicyStat tile in the My Apps, this option redirects to PolicyStat Sign-on URL. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).