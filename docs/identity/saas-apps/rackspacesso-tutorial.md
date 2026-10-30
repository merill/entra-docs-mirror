---
layout: Conceptual
title: Configure Rackspace SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/rackspacesso-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Rackspace SSO.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 1497cdb6-3e0c-de54-9526-bb60d539c673
document_version_independent_id: 2b8bf8ef-a4af-9b0a-a7b2-cff4875012e0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/rackspacesso-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/rackspacesso-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/rackspacesso-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d4b286ff-c442-9270-c261-93aceae5abb9
---

# Configure Rackspace SSO for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Rackspace SSO with Microsoft Entra ID. When you integrate Rackspace SSO with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Rackspace SSO.
- Enable your users to be automatically signed-in to Rackspace SSO with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Rackspace SSO single sign-on enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra single sign-on in a test environment.

- Rackspace SSO supports **IDP** initiated SSO.

Note

Identifier of this application is a fixed string value so only one instance can be configured in one tenant.

## Add Rackspace SSO from the gallery

To configure the integration of Rackspace SSO into Microsoft Entra ID, you need to add Rackspace SSO from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Rackspace SSO** in the search box.
4. Select **Rackspace SSO** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Rackspace SSO

In this section, you configure and test Microsoft Entra single sign-on with Rackspace SSO based on a test user called **Britta Simon**. When using single sign-on with Rackspace, the Rackspace users are automatically created the first time they sign in to the Rackspace portal.

To configure and test Microsoft Entra single sign-on with Rackspace SSO, you need to perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure Rackspace SSO**- to configure the Single Sign-On settings on application side.
    1. **Set up Attribute Mapping in the Rackspace Control Panel** - to assign Rackspace roles to Microsoft Entra users.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Rackspace SSO** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, upload the **Service Provider metadata file** which you can download from the [URL](https://login.rackspace.com/federate/sp.xml) and perform the following steps:

    a. Select **Upload metadata file**.

    ![Screenshot shows Basic S A M L Configuration with the Upload metadata file link.](common/upload-metadata.png)

    b. Select **folder logo** to select the metadata file and select **Upload**.

    ![Screenshot shows a dialog box where you can select and upload a file.](common/browse-upload-metadata.png)

    c. Once the metadata file is successfully uploaded, the necessary URLs get auto populated automatically.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select **Download** to download the **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)

This file is uploaded to Rackspace to populate required Identity Federation configuration settings.

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Rackspace SSO

To configure single sign-on on **Rackspace SSO** side:

1. See the documentation at [Add an Identity Provider to the Control Panel](https://docs.rackspace.com/docs/rackspace-identity-federation-user-guide)
2. It will lead you through the steps to:
    1. Create a new Identity Provider.
    2. Specify an email domain that users will use to identify your company when signing in.
    3. Upload the **Federation Metadata XML** previously downloaded from the Azure control panel.

This will correctly configure the basic SSO settings needed for Azure and Rackspace to connect.

### Set up Attribute Mapping in the Rackspace control panel

Rackspace uses an **Attribute Mapping Policy** to assign Rackspace roles and groups to your single sign-on users. The **Attribute Mapping Policy** translates Microsoft Entra SAML claims into the user configuration fields Rackspace requires. More documentation can be found in the Rackspace [Attribute Mapping Basics documentation](https://docs.rackspace.com/docs/id-federation-map-policies-permissions-cloud). Some considerations:

- If you want to assign varying levels of Rackspace access using Microsoft Entra groups, you need to enable the Groups claim in the Azure **Rackspace SSO** Single Sign-on settings. The **Attribute Mapping Policy** will then be used to match those groups to desired Rackspace roles and groups:

    ![Screenshot shows the Groups claim settings.](common/sso-groups-claim.png)
- By default, Microsoft Entra ID sends the UID of Microsoft Entra groups in the SAML claim, versus the name of the Group. However, if you're synchronizing your on-premises Active Directory to Microsoft Entra ID, you have the option to send the actual names of the groups:

    ![Screenshot shows the Groups claim name settings.](common/sso-groups-claims-names.png)

The following example **Attribute Mapping Policy** demonstrates:

1. Setting the Rackspace user's name to the `user.name` SAML claim. Any claim can be used, but it's most common to set this to a field containing the user's email address.
2. Setting the Rackspace roles `admin` and `billing:admin` on a user by matching a Microsoft Entra group, by either Group Name or Group UID. A *substitution* of `"{0}"` in the `roles` field is used, and is replaced by the results of the `remote` rule expressions.
3. Using the `"{D}"`*default substitution* to let Rackspace retrieve additional SAML fields by looking for standard and well-known SAML claims in the SAML exchange.

```yaml
--- 
mapping:
    rules:
    - local:
        user:
          domain: "{D}"
          name: "{At(http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name)}"
          email: "{D}"
          roles:
              - "{0}"
          expire: "{D}"
      remote:
          - path: |
              (
                if (mapping:get-attributes('http://schemas.microsoft.com/ws/2008/06/identity/claims/groups')='7269f9a2-aabb-9393-8e6d-282e0f945985') then ('admin', 'billing:admin') else (),
                if (mapping:get-attributes('http://schemas.microsoft.com/ws/2008/06/identity/claims/groups')='MyAzureGroup') then ('admin', 'billing:admin') else ()
              )
            multiValue: true
  version: RAX-1
```

Tip

Ensure that you use a text editor that validates YAML syntax when editing your policy file.

See the Rackspace [Attribute Mapping Basics documentation](https://docs.rackspace.com/docs/id-federation-map-policies-permissions-cloud) for more examples.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Rackspace SSO for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Rackspace SSO tile in the My Apps, you should be automatically signed in to the Rackspace SSO for which you set up the SSO. For more information, see [Microsoft Entra My Apps](/en-us/azure/active-directory/manage-apps/end-user-experiences#azure-ad-my-apps).

You can also use the **Validate** button in the **Rackspace SSO** Single sign-on settings:

![Screenshot shows the SSO Validate Button.](common/sso-validate-sign-on.png)