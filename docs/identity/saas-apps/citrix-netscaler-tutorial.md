---
layout: Conceptual
title: Configure Citrix ADC SAML Connector for Microsoft Entra ID (Kerberos-based authentication) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/citrix-netscaler-tutorial
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
description: Learn how to configure single sign-on (SSO) between Microsoft Entra ID and Citrix ADC SAML Connector for Microsoft Entra ID by using Kerberos-based authentication.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: eca1c86b-0747-ce5b-1b7f-b215ce2f994d
document_version_independent_id: c347323f-f0e5-f99a-a9cc-9ae6585972bb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/citrix-netscaler-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/citrix-netscaler-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/citrix-netscaler-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 47f32b55-3ed9-88d3-f546-362d1998412d
---

# Configure Citrix ADC SAML Connector for Microsoft Entra ID (Kerberos-based authentication) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Citrix ADC SAML Connector for Microsoft Entra ID with Microsoft Entra ID. When you integrate Citrix ADC SAML Connector for Microsoft Entra ID with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Citrix ADC SAML Connector for Microsoft Entra ID.
- Enable your users to be automatically signed in to Citrix ADC SAML Connector for Microsoft Entra ID with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Citrix ADC SAML Connector for Microsoft Entra single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment. The article includes these scenarios:

- **SP-initiated** SSO for Citrix ADC SAML Connector for Microsoft Entra ID.
- **Just in time** user provisioning for Citrix ADC SAML Connector for Microsoft Entra ID.
- Kerberos-based authentication for Citrix ADC SAML Connector for Microsoft Entra ID.
- [Header-based authentication for Citrix ADC SAML Connector for Microsoft Entra ID](header-citrix-netscaler-tutorial#publish-the-web-server).

## Add Citrix ADC SAML Connector for Microsoft Entra ID from the gallery

To integrate Citrix ADC SAML Connector for Microsoft Entra ID with Microsoft Entra ID, first add Citrix ADC SAML Connector for Microsoft Entra ID to your list of managed SaaS apps from the gallery:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Citrix ADC SAML Connector for Microsoft Entra ID** in the search box.
4. In the results, select **Citrix ADC SAML Connector for Microsoft Entra ID**, and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Citrix ADC SAML Connector for Microsoft Entra ID

Configure and test Microsoft Entra SSO with Citrix ADC SAML Connector for Microsoft Entra ID by using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Citrix ADC SAML Connector for Microsoft Entra ID.

To configure and test Microsoft Entra SSO with Citrix ADC SAML Connector for Microsoft Entra ID, perform the following steps:

1. Configure Microsoft Entra SSO - to enable your users to use this feature.

    1. Create a Microsoft Entra test user - to test Microsoft Entra SSO with B.Simon.
    2. Assign the Microsoft Entra test user - to enable B.Simon to use Microsoft Entra SSO.
2. Configure Citrix ADC SAML Connector for Microsoft Entra SSO - to configure the SSO settings on the application side.

    1. Create Citrix ADC SAML Connector for Microsoft Entra test user - to have a counterpart of B.Simon in Citrix ADC SAML Connector for Microsoft Entra ID that's linked to the Microsoft Entra representation of the user.
3. Test SSO - to verify whether the configuration works.

## Configure Microsoft Entra SSO

To enable Microsoft Entra SSO by using the Azure portal, complete these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Citrix ADC SAML Connector for Microsoft Entra ID** application integration pane, under **Manage**, select **Single sign-on**.
3. On the **Select a single sign-on method** pane, select **SAML**.
4. On the **Set up Single Sign-On with SAML** pane, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png)
5. In the **Basic SAML Configuration** section, to configure the application in **IDP-initiated** mode, perform the following steps:

    1. In the **Identifier** text box, enter a URL that has the following pattern: `https://<YOUR_FQDN>`
    2. In the **Reply URL** text box, enter a URL that has the following pattern: `http(s)://<YOUR_FQDN>.of.vserver/cgi/samlauth`
6. To configure the application in **SP-initiated** mode, select **Set additional URLs** and perform the following step:

    - In the **Sign-on URL** text box, enter a URL that has the following pattern: `https://<YOUR_FQDN>/CitrixAuthService/AuthService.asmx`

    Note

    - The URLs that are used in this section aren't real values. Update these values with the actual values for Identifier, Reply URL, and Sign-on URL. Contact the [Citrix ADC SAML Connector for Microsoft Entra client support team](https://www.citrix.com/contact/technical-support.html) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
    - To set up SSO, the URLs must be accessible from public websites. You must enable the firewall or other security settings on the Citrix ADC SAML Connector for Microsoft Entra ID side to enable Microsoft Entra ID to post the token at the configured URL.
7. On the **Set up Single Sign-On with SAML** pane, in the **SAML Signing Certificate** section, for **App Federation Metadata Url**, copy the URL and save it in Notepad.

    ![Screenshot shows the Certificate download link.](common/certificatebase64.png)
8. In the **Set up Citrix ADC SAML Connector for Microsoft Entra ID** section, copy the relevant URLs based on your requirements.

    ![Screenshot shows to copy configuration URLs.](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Citrix ADC SAML Connector for Microsoft Entra SSO

Select a link for steps for the kind of authentication you want to configure:

- Configure Citrix ADC SAML Connector for Microsoft Entra SSO for Kerberos-based authentication
- [Configure Citrix ADC SAML Connector for Microsoft Entra SSO for header-based authentication](header-citrix-netscaler-tutorial#publish-the-web-server)

### Publish the web server

To create a virtual server:

1. Select **Traffic Management** &gt; **Load Balancing** &gt; **Services**.
2. Select **Add**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Services pane.](media/citrix-netscaler-tutorial/service.png)
3. Set the following values for the web server that's running the applications:

    - **Service Name**
    - **Server IP/ Existing Server**
    - **Protocol**
    - **Port**

### Configure the load balancer

To configure the load balancer:

1. Go to **Traffic Management** &gt; **Load Balancing** &gt; **Virtual Servers**.
2. Select **Add**.
3. Set the following values as described in the following screenshot:

    - **Name**
    - **Protocol**
    - **IP Address**
    - **Port**
4. Select **OK**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Basic Settings pane.](media/citrix-netscaler-tutorial/basic.png)

### Bind the virtual server

To bind the load balancer with the virtual server:

1. In the **Services and Service Groups** pane, select **No Load Balancing Virtual Server Service Binding**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Load Balancing Virtual Server Service Binding pane.](media/citrix-netscaler-tutorial/binding.png)
2. Verify the settings as shown in the following screenshot, and then select **Close**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Verify the virtual server services binding.](media/citrix-netscaler-tutorial/verify.png)

### Bind the certificate

To publish this service as TLS, bind the server certificate, and then test your application:

1. Under **Certificate**, select **No Server Certificate**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Server Certificate pane.](media/citrix-netscaler-tutorial/certificate.png)
2. Verify the settings as shown in the following screenshot, and then select **Close**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Verify the certificate.](media/citrix-netscaler-tutorial/verify-certificate.png)

## Citrix ADC SAML Connector for Microsoft Entra SAML profile

To configure the Citrix ADC SAML Connector for Microsoft Entra SAML profile, complete the following sections.

### Create an authentication policy

To create an authentication policy:

1. Go to **Security** &gt; **AAA – Application Traffic** &gt; **Policies** &gt; **Authentication** &gt; **Authentication Policies**.
2. Select **Add**.
3. On the **Create Authentication Policy** pane, enter or select the following values:

    - **Name**: Enter a name for your authentication policy.
    - **Action**: Enter **SAML**, and then select **Add**.
    - **Expression**: Enter **true**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Create Authentication Policy pane.](media/citrix-netscaler-tutorial/policy.png)
4. Select **Create**.

### Create an authentication SAML server

To create an authentication SAML server, go to the **Create Authentication SAML Server** pane, and then complete the following steps:

1. For **Name**, enter a name for the authentication SAML server.
2. Under **Export SAML Metadata**:

    1. Select the **Import Metadata** check box.
    2. Enter the federation metadata URL from the Azure SAML UI that you copied earlier.
3. For **Issuer Name**, enter the relevant URL.
4. Select **Create**.

![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Create Authentication SAML Server pane.](media/citrix-netscaler-tutorial/authentication.png)

### Create an authentication virtual server

To create an authentication virtual server:

1. Go to **Security** &gt; **AAA - Application Traffic** &gt; **Policies** &gt; **Authentication** &gt; **Authentication Virtual Servers**.
2. Select **Add**, and then complete the following steps:

    1. For **Name**, enter a name for the authentication virtual server.
    2. Select the **Non-Addressable** check box.
    3. For **Protocol**, select **SSL**.
    4. Select **OK**.
3. Select **Continue**.

### Configure the authentication virtual server to use Microsoft Entra ID

Modify two sections for the authentication virtual server:

1. On the **Advanced Authentication Policies** pane, select **No Authentication Policy**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Advanced Authentication Policies pane.](media/citrix-netscaler-tutorial/advanced.png)
2. On the **Policy Binding** pane, select the authentication policy, and then select **Bind**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Policy Binding pane](media/citrix-netscaler-tutorial/policy-binding.png)
3. On the **Form Based Virtual Servers** pane, select **No Load Balancing Virtual Server**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Form Based Virtual Servers pane.](media/citrix-netscaler-tutorial/virtual-server.png)
4. For **Authentication FQDN**, enter a fully qualified domain name (FQDN) (required).
5. Select the load balancing virtual server that you want to protect with Microsoft Entra authentication.
6. Select **Bind**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Load Balancing Virtual Server Binding pane.](media/citrix-netscaler-tutorial/load.png)

    Note

    Be sure to select **Done** on the **Authentication Virtual Server Configuration** pane.
7. To verify your changes, in a browser, go to the application URL. You should see your tenant sign-in page instead of the unauthenticated access that you would have seen previously.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - A sign-in page in a web browser.](media/citrix-netscaler-tutorial/sign.png)

## Configure Citrix ADC SAML Connector for Microsoft Entra SSO for Kerberos-based authentication

### Create a Kerberos delegation account for Citrix ADC SAML Connector for Microsoft Entra ID

1. Create a user account (in this example, we use *AppDelegation*).

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Properties pane.](media/citrix-netscaler-tutorial/properties.png)
2. Set up a HOST SPN for this account.

    Example: `setspn -S HOST/AppDelegation.IDENTT.WORK identt\appdelegation`

    In this example:

    - `IDENTT.WORK` is the domain FQDN.
    - `identt` is the domain NetBIOS name.
    - `appdelegation` is the delegation user account name.
3. Configure delegation for the web server as shown in the following screenshot:

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Delegation under Properties pane.](media/citrix-netscaler-tutorial/delegation.png)

    Note

    In the screenshot example, the internal web server name running the Windows Integrated Authentication (WIA) site is *CWEB2*.

### Citrix ADC SAML Connector for Microsoft Entra AAA KCD (Kerberos delegation accounts)

To configure the Citrix ADC SAML Connector for Microsoft Entra AAA KCD account:

1. Go to **Citrix Gateway** &gt; **AAA KCD (Kerberos Constrained Delegation) Accounts**.
2. Select **Add**, and then enter or select the following values:

    - **Name**: Enter a name for the KCD account.
    - **Realm**: Enter the domain and extension in uppercase.
    - **Service SPN**: `http/<host/fqdn>@<DOMAIN.COM>`.

        Note

        `@DOMAIN.COM` is required and must be uppercase. Example: `http/cweb2@IDENTT.WORK`.
    - **Delegated User**: Enter the delegated user name.
    - Select the **Password for Delegated User** check box, and enter and confirm a password.
3. Select **OK**.

### Citrix traffic policy and traffic profile

To configure the Citrix traffic policy and traffic profile:

1. Go to **Security** &gt; **AAA - Application Traffic** &gt; **Policies** &gt; **Traffic Policies, Profiles and Form SSO ProfilesTraffic Policies**.
2. Select **Traffic Profiles**.
3. Select **Add**.
4. To configure a traffic profile, enter or select the following values.

    - **Name**: Enter a name for the traffic profile.
    - **Single Sign-on**: Select **ON**.
    - **KCD Account**: Select the KCD account you created in the preceding section.
5. Select **OK**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Configure Traffic Profile pane.](media/citrix-netscaler-tutorial/traffic.png)
6. Select **Traffic Policy**.
7. Select **Add**.
8. To configure a traffic policy, enter or select the following values:

    - **Name**: Enter a name for the traffic policy.
    - **Profile**: Select the traffic profile you created in the preceding section.
    - **Expression**: Enter **true**.
9. Select **OK**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Configure Traffic Policy pane](media/citrix-netscaler-tutorial/traffic-policy.png)

### Bind a traffic policy to a virtual server in Citrix

To bind a traffic policy to a virtual server by using the GUI:

1. Go to **Traffic Management** &gt; **Load Balancing** &gt; **Virtual Servers**.
2. In the list of virtual servers, select the virtual server to which you want to bind the rewrite policy, and then select **Open**.
3. On the **Load Balancing Virtual Server** pane, under **Advanced Settings**, select **Policies**. All policies that are configured for your NetScaler instance appear in the list.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Load Balancing Virtual Server pane.](media/citrix-netscaler-tutorial/balancing.png)

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Policies dialog box.](media/citrix-netscaler-tutorial/dialog.png)
4. Select the check box next to the name of the policy you want to bind to this virtual server.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Load Balancing Virtual Server Traffic Policy Binding pane.](media/citrix-netscaler-tutorial/pane.png)
5. In the **Choose Type** dialog box:

    1. For **Choose Policy**, select **Traffic**.
    2. For **Choose Type**, select **Request**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Choose Type pane.](media/citrix-netscaler-tutorial/choose.png)
6. When the policy is bound, select **Done**.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - Policies pane.](media/citrix-netscaler-tutorial/policies.png)
7. Test the binding by using the WIA website.

    ![Screenshot of Citrix ADC SAML Connector for Microsoft Entra configuration - A test page in a web browser](media/citrix-netscaler-tutorial/test.png)

### Create Citrix ADC SAML Connector for Microsoft Entra test user

In this section, a user called B.Simon is created in Citrix ADC SAML Connector for Microsoft Entra ID. Citrix ADC SAML Connector for Microsoft Entra ID supports just-in-time user provisioning, which is enabled by default. There's no action for you to take in this section. If a user doesn't already exist in Citrix ADC SAML Connector for Microsoft Entra ID, a new one is created after authentication.

Note

If you need to create a user manually, contact the [Citrix ADC SAML Connector for Microsoft Entra client support team](https://www.citrix.com/contact/technical-support.html).

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Citrix ADC SAML Connector for Microsoft Entra Sign-on URL where you can initiate the login flow.
- Go to Citrix ADC SAML Connector for Microsoft Entra Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Citrix ADC SAML Connector for Microsoft Entra ID tile in the My Apps, this option redirects to Citrix ADC SAML Connector for Microsoft Entra Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).