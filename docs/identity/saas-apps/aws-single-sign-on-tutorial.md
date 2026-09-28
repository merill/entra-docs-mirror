---
layout: Conceptual
title: Configure AWS IAM Identity Center (successor to AWS Single Sign-On) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/aws-single-sign-on-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and AWS IAM Identity Center (successor to AWS Single Sign-On).
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f8e131bf-99d7-a850-a597-ac02b9f6c3a9
document_version_independent_id: a27625d3-cf35-ffaf-5734-d1a2bbcdd60c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/aws-single-sign-on-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/aws-single-sign-on-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/aws-single-sign-on-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0052d985-9e6a-bda3-47d8-170ef40a6ce4
---

# Configure AWS IAM Identity Center (successor to AWS Single Sign-On) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate AWS IAM Identity Center (successor to AWS Single Sign-On) with Microsoft Entra ID. When you integrate AWS IAM Identity Center with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to AWS IAM Identity Center.
- Enable your users to be automatically signed-in to AWS IAM Identity Center with their Microsoft Entra accounts.
- Manage your accounts in one central location.

**Note:** When using AWS Organizations, it's important to delegate another account as the Identity Center Administration account, enable the IAM Identity Center on it, and set up the Entra ID SSO with that account, not the root management account. This ensures a more secure and manageable setup.

AWS IAM Identity Center is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ |  | ✅ |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- An AWS Organizations setup with another account delegated as the Identity Center Administration account.
- AWS IAM Identity Center enabled on the delegated Identity Center Administration account.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

**Note:** Ensure you delegated another account as the Identity Center Administration account and enabled IAM Identity Center on it before proceeding with the following steps.

- AWS IAM Identity Center supports **SP and IDP** initiated SSO.
- AWS IAM Identity Center supports [**Automated user provisioning**](aws-single-sign-on-provisioning-tutorial).

## Add AWS IAM Identity Center from the gallery

To configure the integration of AWS IAM Identity Center into Microsoft Entra ID, you need to add AWS IAM Identity Center from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **AWS IAM Identity Center** in the search box.
4. Select **AWS IAM Identity Center** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for AWS IAM Identity Center

Configure and test Microsoft Entra SSO with AWS IAM Identity Center using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in AWS IAM Identity Center.

To configure and test Microsoft Entra SSO with AWS IAM Identity Center, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure AWS IAM Identity Center SSO**- to configure the single sign-on settings on application side.
    1. **Create AWS IAM Identity Center test user** - to have a counterpart of B.Simon in AWS IAM Identity Center that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **AWS IAM Identity Center** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. If you have **Service Provider metadata file**, on the **Basic SAML Configuration** section, perform the following steps:

    a. Select **Upload metadata file**.

    b. Select **folder logo** to select the metadata file which is explained to download in **Configure AWS IAM Identity Center SSO** section and select **Add**.

    ![image2](common/browse-upload-metadata.png)

    c. Once the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values get auto populated in Basic SAML Configuration section.

    Note

    If the **Identifier** and **Reply URL** values aren't getting auto populated, then fill in the values manually according to your requirement.

    Note

    When changing identity provider in AWS (that is, from AD to external provider such as Microsoft Entra ID) the AWS metadata changes and need to be reuploaded to Azure for SSO to function correctly.
6. If you don't have **Service Provider metadata file**, perform the following steps on the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<REGION>.signin.aws.amazon.com/platform/saml/<ID>`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<REGION>.signin.aws.amazon.com/platform/saml/acs/<ID>`
7. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://portal.sso.<REGION>.amazonaws.com/saml/assertion/<ID>`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [AWS IAM Identity Center Client support team](mailto:aws-sso-partners@amazon.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
8. AWS IAM Identity Center application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

    ![image](common/edit-attribute.png)

    Note

    If ABAC is enabled in AWS IAM Identity Center, the additional attributes may be passed as session tags directly into AWS accounts.
9. On the **Set-up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)
10. On the **Set up AWS IAM Identity Center** section, copy the appropriate URL(s) based on your requirement.

    ![Screenshot shows to copy configuration appropriate URL.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure AWS IAM Identity Center SSO

1. In a different web browser window, sign in to your AWS IAM Identity Center company site as an administrator
2. Go to the **Services -&gt; Security, Identity, & Compliance -&gt; AWS IAM Identity Center**.
3. In the left navigation pane, choose **Settings**.
4. On the **Settings** page, find **Identity source**, select **Actions** pull-down menu, and select Change **identity source**.

    ![Screenshot for Identity source change service.](media/aws-single-sign-on-tutorial/settings.png)
5. On the Change identity source page, choose **External identity provider**.

    ![Screenshot for selecting external identity provider section.](media/aws-single-sign-on-tutorial/external-identity-provider.png)
6. Perform the below steps in the **Configure external identity provider** section:

    ![Screenshot for download and upload metadata section.](media/aws-single-sign-on-tutorial/upload-metadata.png)

    a. In the **Service provider metadata** section, find **AWS SSO SAML metadata**, select **Download metadata file** to download the metadata file and save it on your computer and use this metadata file to upload on Azure portal.

    b. Copy **AWS access portal sign-in URL** value, paste this value into the **Sign on URL** text box in the **Basic SAML Configuration section**.

    c. In the **Identity provider metadata** section, select **Choose file** to upload the metadata file that you downloaded.

    d. Choose **Next: Review**.
7. In the text box, type **ACCEPT** to change the identity source.

    ![Screenshot for Confirming the configuration.](media/aws-single-sign-on-tutorial/accept.png)
8. Select **Change identity source**.

### Create AWS IAM Identity Center test user

1. Open the **AWS IAM Identity Center console**.
2. In the left navigation pane, choose **Users**.
3. On the Users page, choose **Add user**.
4. On the Add user page, follow these steps:

    a. In the **Username** field, enter B.Simon.

    b. In the **Email address** field, enter the `username@companydomain.extension`. For example, `B.Simon@contoso.com`.

    c. In the **Confirmed email address** field, reenter the email address from the previous step.

    d. In the First name field, enter `Britta`.

    e. In the Last name field, enter `Simon`.

    f. In the Display name field, enter `B.Simon`.

    g. Choose **Next**, and then **Next** again.

    Note

    Make sure the username and email address entered in AWS IAM Identity Center matches the user’s Microsoft Entra sign-in name. This helps you avoid any authentication problems.
5. Choose **Add user**.
6. Next, you assign the user to your AWS account. To do so, in the left navigation pane of the AWS IAM Identity Center console, choose **AWS accounts**.
7. On the AWS Accounts page, select the AWS organization tab, check the box next to the AWS account you want to assign to the user. Then choose **Assign users**.
8. On the Assign Users page, find, and check the box next to the user B.Simon. Then choose **Next: Permission sets**.
9. Under the select permission sets section, check the box next to the permission set you want to assign to the user B.Simon. If you don’t have an existing permission set, choose **Create new permission set**.

    Note

    Permission sets define the level of access that users and groups have to an AWS account. To learn more about permission sets, see the **AWS IAM Identity Center Multi Account Permissions** page.
10. Choose **Finish**.

Note

AWS IAM Identity Center also supports automatic user provisioning, you can find more details [here](aws-single-sign-on-provisioning-tutorial) on how to configure automatic user provisioning.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

#### SP initiated:

- Select **Test this application**, this option redirects to AWS IAM Identity Center sign-in URL where you can initiate the login flow.
- Go to AWS IAM Identity Center sign-in URL directly and initiate the login flow from there.

#### IDP initiated:

- Select **Test this application**, and you should be automatically signed in to the AWS IAM Identity Center for which you set up the SSO.

You can also use Microsoft My Apps to test the application in any mode. When you select the AWS IAM Identity Center tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the AWS IAM Identity Center for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).