---
layout: Conceptual
title: Configure Check Point Remote Secure Access VPN for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/check-point-remote-access-vpn-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Check Point Remote Secure Access VPN.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 8a2770cd-75e6-f55d-4c5d-f7e65ab7f161
document_version_independent_id: 37aa0777-7d3a-5367-50d6-d64aa63db982
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/check-point-remote-access-vpn-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/check-point-remote-access-vpn-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/check-point-remote-access-vpn-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9219b0a8-7f85-c854-0533-96aeff8930ca
---

# Configure Check Point Remote Secure Access VPN for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Check Point Remote Secure Access VPN with Microsoft Entra ID. When you integrate Check Point Remote Secure Access VPN with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Check Point Remote Secure Access VPN.
- Enable your users to be automatically signed-in to Check Point Remote Secure Access VPN with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Check Point Remote Secure Access VPN single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Check Point Remote Secure Access VPN supports **SP** initiated SSO.

## Adding Check Point Remote Secure Access VPN from the gallery

To configure the integration of Check Point Remote Secure Access VPN into Microsoft Entra ID, you need to add Check Point Remote Secure Access VPN from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Check Point Remote Secure Access VPN** in the search box.
4. Select **Check Point Remote Secure Access VPN** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Check Point Remote Secure Access VPN

Configure and test Microsoft Entra SSO with Check Point Remote Secure Access VPN using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Check Point Remote Secure Access VPN.

To configure and test Microsoft Entra SSO with Check Point Remote Secure Access VPN, perform the following steps:

1. **Configure Microsoft Entra SSO** - to enable your users to use this feature.

    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Check Point Remote Secure Access VPN SSO** - to enable your users to use this feature.

    1. **Create Check Point Remote Secure Access VPN test user** - to have a counterpart of B.Simon in Check Point Remote Secure Access VPN that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Check Point Remote Secure Access VPN** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, enter the values for the following fields:

    1. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<GATEWAY_IP>/saml-vpn/spPortal/ACS/ID/<IDENTIFIER_UID>`
    2. In the **Reply URL** text box, type a URL using the following pattern: `https://<GATEWAY_IP>/saml-vpn/spPortal/ACS/Login/<IDENTIFIER_UID>`
    3. In the **Sign on URL** text box, type a URL using the following pattern: `https://<GATEWAY_IP>/saml-vpn/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL. Contact [Check Point Remote Secure Access VPN Client support team](mailto:support@checkpoint.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Check Point Remote Secure Access VPN** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Check Point Remote Secure Access VPN SSO

### Configure an External User Profile object

Note

This section is needed only if you don't want to use an on-premises Active Directory (LDAP).

**Configure a generic user profile in the Legacy SmartDashboard**:

1. In SmartConsole, go to **Manage & Settings &gt; Blades**.
2. In the **Mobile Access** section, select **Configure in SmartDashboard**. The Legacy SmartDashboard opens.
3. In the Network **Objects** pane, and select **Users**.
4. Right-click an empty space and select **New &gt; External User Profile &gt; Match all users**.
5. Configure the **External User Profile** properties:

    1. On the **General Properties** page:

        - In the **External User Profile** name field, leave the default name `generic`\*
        - In the **Expiration Date** field, set the applicable date
    2. On the **Authentication** page:

        - From the **Authentication Scheme** drop-down list, select `undefined`
    3. On the **Location**, **Time**, and **Encryption** pages:

        - Configure other applicable settings
    4. Select **OK**.
6. From the top toolbar, select **Update** (or press Ctrl + S).
7. Close SmartDashboard.
8. In SmartConsole, install the Access Control Policy.

### Configure Remote Access VPN

1. Open the object of the applicable Security Gateway.
2. On the General Properties page, enable the **IPSec VPN** Software Blade.
3. From the left tree, select the **IPSec VPN** page.
4. In the section **This Security Gateway participates in the following VPN communities**, select **Add** and select **Remote Access Community**.
5. From the left tree, select **VPN clients &gt; Remote Access**.
6. Enable **Support Visitor Mode**.
7. From the left tree, select **VPN clients &gt; Office Mode**.
8. Select **Allow Office Mode** and select the applicable Office Mode Method.
9. From the left tree, select **VPN Clients &gt; SAML Portal Settings**.
10. Make sure the Main URL contains the fully qualified domain name of the gateway. This domain name should end with a DNS suffix registered by your organization. For example: `https://gateway1.company.com/saml-vpn`
11. Make sure the certificate is trusted by the end users’ browser.
12. Select **OK**.

### Configure an Identity Provider object

1. Do the following steps for each Security Gateway that participates in Remote Access VPN.
2. In SmartConsole, in the **Gateways & Servers** view, select **New &gt; More &gt; User/Identity &gt; Identity Provider**.
3. Perform the following steps in **New Identity Provider** window.

    ![screenshot for Identity Provider section.](media/check-point-remote-access-vpn-tutorial/new-identity-provider.png)

    a. In the **Gateway** field, select the Security Gateway, which needs to perform the SAML authentication.

    b. In the **Service** field, select **Remote Access VPN** from the dropdown.

    c. Copy **Identifier(Entity ID)** value, paste this value into the **Identifier** text box in the **Basic SAML Configuration** section.

    d. Copy **Reply URL** value, paste this value into the **Reply URL** text box in the **Basic SAML Configuration** section.

    e. Select **Import Metadata File** to upload the downloaded **Federation Metadata XML**.

    Note

    Alternatively you can also select **Insert Manually** to paste manually the **Entity ID** and **Login URL** values into the corresponding fields, and to upload the **Certificate File**.

    f. Select **OK**.

### Configure the Identity Provider as an authentication method

1. Open the object of the applicable Security Gateway.
2. On the **VPN Clients &gt; Authentication** page:

    a. Clear the checkbox **Allow older clients to connect to this gateway**.

    b. Add a new object or edit an existing realm.

    ![screenshot for to Add a new object.](media/check-point-remote-access-vpn-tutorial/add-new-object.png)
3. Enter a name and a display name, and add/edit an authentication method: In case the Login Option is used on GWs who participate in MEP, in order to allow smooth user experience the Name should start with `SAMLVPN_` prefix.

    ![screenshot about Login Option.](media/check-point-remote-access-vpn-tutorial/login-option.png)
4. Select the option **Identity Provider**, select the green `+` button and select the applicable Identity Provider object.

    ![screenshot to select the applicable Identity Provider object.](media/check-point-remote-access-vpn-tutorial/green-button.png)
5. In the Multiple Logon Options window: From the left pane, select **User Directories** and then select **Manual configuration**. There are two options:

    1. If you don't want to use an on-premises Active Directory (LDAP), select only External User Profiles and select OK.
    2. If you do want to use an on-premises Active Directory (LDAP), select only LDAP users and in the LDAP Lookup Type select email. Then select OK.

    ![Screenshot of manual configuration.](media/check-point-remote-access-vpn-tutorial/manual-configuration.png)
6. Configure the required settings in the management database:

    1. Close SmartConsole.
    2. Connect with the GuiDBEdit Tool to the Management Server (see [sk13009](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails&amp;solutionid=sk13009)).
    3. In the top left pane, go to **Edit &gt; Network Objects**.
    4. In the top right pane, select the **Security Gateway object**.
    5. In the bottom pane, go to **realms\_for\_blades** &gt; **vpn**.
    6. If you don't want to use an on-premises Active Directory (LDAP), set **do\_ldap\_fetch** to **false** and **do\_generic\_fetch** to **true**. Then select **OK**. If you do want to use an on-premises Active Directory (LDAP), set **do\_ldap\_fetch** to **true** and **do\_generic\_fetch** to **false**. Then select **OK**.
    7. Repeat steps 4 to 6 for all applicable Security Gateways.
    8. Save all changes by selecting **File** &gt; **Save All**.
7. Close the GuiDBEdit Tool.
8. Each Security Gateway and each Software Blade have separate settings. Review the settings in each Security Gateway and each Software Blade that use authentication (VPN, Mobile Access, and Identity Awareness).

    - Make sure to select the option **LDAP users** only for Software Blades that use LDAP.
    - Make sure to select the option **External user profiles** only for Software Blades that don't use LDAP.
9. Install the Access Control Policy on each Security Gateway.

### VPN RA Client Installation and configuration

1. Install the VPN client.
2. Set the Identity Provider browser mode (optional).

    By default, the Windows client uses its embedded browser and the macOS client uses Safari to authenticate on the Identity Provider's portal. For Windows clients, change this behavior to use Internet Explorer instead:

    1. On the client machine, open a plain-text editor as an Administrator.
    2. Open the `trac.defaults` file in the text editor.

        - On 32-bit Windows:

            `%ProgramFiles%\CheckPoint\Endpoint Connect\trac.defaults`
        - On 64-bit Windows:

            `%ProgramFiles(x86)%\CheckPoint\Endpoint Connect\trac.defaults`
    3. Change the `idp_browser_mode` attribute value from `embedded` to `IE`.
    4. Save the file.
    5. Restart the Check Point Endpoint Security VPN client service.

    Open the Windows Command Prompt as an Administrator and run these commands:

    `# net stop TracSrvWrapper`

    `# net start TracSrvWrapper`
3. Start authentication with browser running in background:

    1. On the client machine, open a plain-text editor as an Administrator.
    2. Open the `trac.defaults` file in the text editor.

        - On 32-bit Windows:

            `%ProgramFiles%\CheckPoint\Endpoint Connect\trac.defaults`
        - On 64-bit Windows:

            `%ProgramFiles(x86)%\CheckPoint\Endpoint Connect\trac.defaults`
        - On macOS:

            `/Library/Application Support/Checkpoint/Endpoint Security/Endpoint Connect/trac.defaults`
    3. Change the value of `idp_show_browser_primary_auth_flow` to `false`.
    4. Save the file.
    5. Restart the Check Point Endpoint Security VPN client service.

        - On Windows clients, open the Windows Command Prompt as an Administrator and run these commands:

            `# net stop TracSrvWrapper`

            `# net start TracSrvWrapper`
        - On macOS clients, run:

            `sudo launchctl stop com.checkpoint.epc.service`

            `sudo launchctl start com.checkpoint.epc.service`

### Create Check Point Remote Secure Access VPN test user

In this section, you create a user called Britta Simon in Check Point Remote Secure Access VPN. Work with [Check Point Remote Secure Access VPN support team](mailto:support@checkpoint.com) to add the users in the Check Point Remote Secure Access VPN platform. Users must be created and activated before you use single sign-on.

## Test SSO

1. Open the VPN client and select **Connect to...**.

    ![screenshot for Connect to.](media/check-point-remote-access-vpn-tutorial/connect.png)
2. Select **Site** from the dropdown and select **Connect**.

    ![screenshot for selecting site.](media/check-point-remote-access-vpn-tutorial/site.png)
3. In Microsoft Entra login pop up, sign in using Microsoft Entra credentials which you have created in the **Create a Microsoft Entra test user** section.