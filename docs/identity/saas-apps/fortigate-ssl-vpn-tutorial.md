---
layout: Conceptual
title: Configure FortiGate SSL VPN for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/fortigate-ssl-vpn-tutorial
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
description: Learn the steps you need to perform to integrate FortiGate SSL VPN with Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 675b6583-259f-1135-6443-b9aa40258163
document_version_independent_id: 28e01c75-b130-260c-4aa6-75a1cba20558
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/fortigate-ssl-vpn-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/fortigate-ssl-vpn-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/fortigate-ssl-vpn-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 307670e3-f616-0a40-c465-f0d3fa2660c6
---

# Configure FortiGate SSL VPN for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate FortiGate SSL VPN with Microsoft Entra ID. When you integrate FortiGate SSL VPN with Microsoft Entra ID, you can:

- Use Microsoft Entra ID to control who can access FortiGate SSL VPN.
- Enable your users to be automatically signed in to FortiGate SSL VPN with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Azure portal.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A FortiGate SSL VPN with single sign-on (SSO) enabled.

## Article description

In this article, you configure and test Microsoft Entra SSO in a test environment.

FortiGate SSL VPN supports SP-initiated SSO.

## Add FortiGate SSL VPN from the gallery

To configure the integration of FortiGate SSL VPN into Microsoft Entra ID, you need to add FortiGate SSL VPN from the gallery to your list of managed SaaS apps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **FortiGate SSL VPN** in the search box.
4. Select **FortiGate SSL VPN** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for FortiGate SSL VPN

You'll configure and test Microsoft Entra SSO with FortiGate SSL VPN by using a test user named B.Simon. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the corresponding SAML SSO user group in FortiGate SSL VPN.

To configure and test Microsoft Entra SSO with FortiGate SSL VPN, you complete these high-level steps:

1. **Configure Microsoft Entra SSO**to enable the feature for your users.
    1. **Create a Microsoft Entra test user** to test Microsoft Entra single sign-on.
    2. **Grant access to the test user** to enable Microsoft Entra single sign-on for that user.
2. **Configure FortiGate SSL VPN SSO**on the application side.
    1. **Create a FortiGate SAML SSO user group** as a counterpart to the Microsoft Entra representation of the user.
3. **Test SSO** to verify that the configuration works.

### Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Azure portal:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **FortiGate SSL VPN** application integration page, in the **Manage** section, select **single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the **Edit** button for **Basic SAML Configuration** to edit the settings:

    ![Screenshot of showing Basic SAML configuration page.](media/fortigate-ssl-vpn-tutorial/saml-configuration.png)
5. On the **Set up Single Sign-On with SAML** page, enter the following values:

    a. In the **Identifier** box, enter a URL in the pattern `https://<FortiGate IP or FQDN address>:<Custom SSL VPN port>/remote/saml/metadata`.

    b. In the **Reply URL** box, enter a URL in the pattern `https://<FortiGate IP or FQDN address>:<Custom SSL VPN port>/remote/saml/login`.

    c. In the **Sign on URL** box, enter a URL in the pattern `https://<FortiGate IP or FQDN address>:<Custom SSL VPN port>/remote/saml/login`.

    d. In the **Logout URL** box, enter a URL in the pattern `https://<FortiGate IP or FQDN address>:<Custom SSL VPN port>/remote/saml/logout`.

    Note

    These values are just patterns. You need to use the actual **Sign on URL**, **Identifier**, **Reply URL**, and **Logout URL** that's configured on the FortiGate. FortiGate support needs to supply the correct values for the environment.
6. The FortiGate SSL VPN application expects SAML assertions in a specific format, which requires you to add custom attribute mappings to the configuration. The following screenshot shows the list of default attributes.

    ![Screenshot of showing Attributes and Claims section.](media/fortigate-ssl-vpn-tutorial/claims.png)
7. The claims required by FortiGate SSL VPN are shown in the following table. The names of these claims must match the names used in the **Perform FortiGate command-line configuration** section of this article. Names are case-sensitive.

    | Name | Source attribute |
    | --- | --- |
    | username | user.userprincipalname |
    | group | user.groups |

    To create these more claims:

    a. Next to **User Attributes & Claims**, select **Edit**.

    b. Select **Add new claim**.

    c. For **Name**, enter **username**.

    d. For **Source attribute**, select **user.userprincipalname**.

    e. Select **Save**.

    Note

    **User Attributes & Claims** allow only one group claim. To add a group claim, delete the existing group claim **user.groups [SecurityGroup]** already present in the claims to add the new claim or edit the existing one to **All groups**.

    f. Select **Add a group claim**.

    g. Select **All groups**.

    h. Under **Advanced options**, select the **Customize the name of the group claim** check box.

    i. For **Name**, enter **group**.

    j. Select **Save**.
8. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, select the **Download** link next to **Certificate (Base64)** to download the certificate and save it on your computer:

    ![Screenshot that shows the certificate download link.](common/certificatebase64.png)
9. In the **Set up FortiGate SSL VPN** section, copy the appropriate URL or URLs, based on your requirements:

    ![Screenshot that shows the configuration URLs.](common/copy-configuration-urls.png)

#### Create a Microsoft Entra test user

In this section, you create a test user named B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

#### Grant access to the test user

In this section, you enable B.Simon to use single sign-on by granting that user access to FortiGate SSL VPN.

1. Browse to **Entra ID** &gt; **Enterprise apps**.
2. In the applications list, select **FortiGate SSL VPN**.
3. On the app's overview page, in the **Manage** section, select **Users and groups**.
4. Select **Add user**, then select **Users and groups** in the **Added Assignment** dialog.
5. In the **Users and groups** dialog box, select **B.Simon** in the **Users** list, and then select the **Select** button at the bottom of the screen.
6. If you're expecting any role value in the SAML assertion, in the **Select Role** dialog box, select the appropriate role for the user from the list. Select the **Select** button at the bottom of the screen.
7. In the **Add Assignment** dialog box, select **Assign**.

#### Create a security group for the test user

In this section, you create a security group in Microsoft Entra ID for the test user. FortiGate uses this security group to grant the user network access via the VPN.

1. In the Microsoft Entra admin center, navigate to **Entra ID** &gt; **Groups** &gt; **New group**.
2. In the **New Group**properties, complete these steps:
    1. In the **Group type** list, select **Security**.
    2. In the **Group name** box, enter **FortiGateAccess**.
    3. In the **Group description** box, enter **Group for granting FortiGate VPN access**.
    4. For the **Microsoft Entra roles can be assigned to the group (Preview)** settings, select **No**.
    5. In the **Membership type** box, select **Assigned**.
    6. Under **Members**, select **No members selected**.
    7. In the **Users and groups** dialog box, select **B.Simon** from the **Users** list, and then select the **Select** button at the bottom of the screen.
    8. Select **Create**.
3. After you're back in the **Groups** section in Microsoft Entra ID, find the **FortiGate Access** group and note the **Object Id**. You'll need it later.

### Configure FortiGate SSL VPN SSO

#### Upload the Base64 SAML Certificate to the FortiGate appliance

After you completed the SAML configuration of the FortiGate app in your tenant, you downloaded the Base64-encoded SAML certificate. You need to upload this certificate to the FortiGate appliance:

1. Sign in to the management portal of your FortiGate appliance.
2. In the left pane, select **System**.
3. Under **System**, select **Certificates**.
4. Select **Import** &gt; **Remote Certificate**.
5. Browse to the certificate downloaded from the FortiGate app deployment in the Azure tenant, select it, and then select **OK**.

After the certificate is uploaded, take note of its name under **System** &gt; **Certificates** &gt; **Remote Certificate**. By default, it's named REMOTE\_Cert\_*N*, where *N* is an integer value.

#### Complete FortiGate command-line configuration

Although you can configure SSO from the GUI since FortiOS 7.0, the CLI configurations apply to all versions and are therefore shown here.

To complete these steps, you need the values you recorded earlier:

| FortiGate SAML CLI setting | Equivalent Azure configuration |
| --- | --- |
| SP entity ID (`entity-id`) | Identifier (Entity ID) |
| SP single sign-on URL (`single-sign-on-url`) | Reply URL (Assertion Consumer Service URL) |
| SP Single sign out URL (`single-logout-url`) | Sign out URL |
| IdP Entity ID (`idp-entity-id`) | Microsoft Entra Identifier |
| IdP single sign-on URL (`idp-single-sign-on-url`) | Azure sign in URL |
| IdP Single sign out URL (`idp-single-logout-url`) | Azure sign out URL |
| IdP certificate (`idp-cert`) | Base64 SAML certificate name (REMOTE\_Cert\_N) |
| Username attribute (`user-name`) | username |
| Group name attribute (`group-name`) | group |

Note

The Sign-on URL under Basic SAML Configuration isn't used in the FortiGate configurations. It's used to trigger SP-initiated single sign-on to redirect the user to the SSL VPN portal page.

1. Establish an SSH session to your FortiGate appliance, and sign in with a FortiGate Administrator account.
2. Run these commands and substitute the `<values>` with the information that you collected previously:

    ```console
    config user saml
      edit azure
        set cert <FortiGate VPN Server Certificate Name>
        set entity-id < Identifier (Entity ID)Entity ID>
        set single-sign-on-url < Reply URL Reply URL>
        set single-logout-url <Logout URL>
        set idp-entity-id <Azure AD Identifier>
        set idp-single-sign-on-url <Azure Login URL>
        set idp-single-logout-url <Azure Logout URL>
        set idp-cert <Base64 SAML Certificate Name>
        set user-name username
        set group-name group
      next
    end
    ```

#### Configure FortiGate for group matching

In this section, you configure FortiGate to recognize the Object ID of the security group that includes the test user. This configuration allows FortiGate to make access decisions based on the group membership.

To complete these steps, you need the Object ID of the FortiGateAccess security group that you created earlier in this article.

1. Establish an SSH session to your FortiGate appliance, and sign in with a FortiGate Administrator account.
2. Run these commands:

    ```console
    config user group
      edit FortiGateAccess
        set member azure
        config match
          edit 1
            set server-name azure
            set group-name <Object Id>
          next
        end
      next
    end
    ```

#### Create a FortiGate VPN Portals and Firewall Policy

In this section, you configure a FortiGate VPN Portals and Firewall Policy that grants access to the FortiGateAccess security group you created earlier in this article.

Refer to [Configuring SAML SSO sign in for SSL VPN with Microsoft Entra ID acting as SAML IdP for instructions](https://docs.fortinet.com/document/fortigate-public-cloud/7.0.0/azure-administration-guide/584456/configuring-saml-sso-login-for-ssl-vpn-web-mode-with-azure-ad-acting-as-saml-idp).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- In Step 5) of the Azure SSO configuration, \**Test single sign-on with your App*, select the **Test** button. this option redirects to FortiGate VPN Sign-on URL where you can initiate the sign in flow.
- Go to FortiGate VPN Sign-on URL directly and initiate the sign in flow from there.
- You can use Microsoft My Apps. When you select the FortiGate VPN tile in the My Apps, this option redirects to FortiGate VPN Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).