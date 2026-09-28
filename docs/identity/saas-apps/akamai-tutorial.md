---
layout: Conceptual
title: Configure Akamai for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/akamai-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Akamai.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: db7ee04d-5eda-eb78-0063-cbe60c380674
document_version_independent_id: b3d0b1e3-0cb1-2744-b520-fd54799fc1d7
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/akamai-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/akamai-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/akamai-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 5cb6ec73-1c09-d51f-fa7a-39ef55b809a1
---

# Configure Akamai for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Akamai with Microsoft Entra ID. When you integrate Akamai with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Akamai.
- Enable your users to be automatically signed-in to Akamai with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Microsoft Entra ID and Akamai Enterprise Application Access integration allows seamless access to legacy applications hosted in the cloud or on-premises. The integrated solution takes advantages of all the modern capabilities of Microsoft Entra ID like [Microsoft Entra Conditional Access](../conditional-access/overview), [Microsoft Entra ID Protection](../../id-protection/overview-identity-protection), and [Microsoft Entra ID Governance](../../id-governance/identity-governance-overview) for legacy applications access without app modifications or agents installation.

The following image describes, where Akamai EAA fits into the broader Hybrid Secure Access scenario.

![Akamai EAA fits into the broader Hybrid Secure Access scenario](media/header-akamai-tutorial/introduction-1.png)

## Key Authentication Scenarios

Apart from Microsoft Entra native integration support for modern authentication protocols like OpenID Connect, SAML and WS-Fed, Akamai EAA extends secure access for legacy-based authentication apps for both internal and external access with Microsoft Entra ID, enabling modern scenarios (such as password-less access) to these applications. This includes:

- Header-based authentication apps
- Remote Desktop
- SSH (Secure Shell)
- Kerberos authentication apps
- VNC (Virtual Network Computing)
- Anonymous auth or no inbuilt authentication apps
- NTLM authentication apps (protection with dual prompts for the user)
- Forms-Based Application (protection with dual prompts for the user)

## Integration Scenarios

Microsoft and Akamai EAA partnership allows the flexibility to meet your business requirements by supporting multiple integration scenarios based on your business requirement. These integration scenarios could be used to provide zero-day coverage across all applications and gradually classify and configure appropriate policy classifications.

#### Integration Scenario 1

Akamai EAA is configured as a single application on the Microsoft Entra ID. Admin can configure the Conditional Access policy on the Application and once the conditions are satisfied users can gain access to the Akamai EAA Portal.

**Pros**:

- You need to only configure IDP once.

**Cons**:

- Users end up having two applications portals.
- Single Common Conditional Access policy coverage for all Applications.

![Integration Scenario 1](media/header-akamai-tutorial/scenario-1.png)

#### Integration Scenario 2

Akamai EAA Application is set up individually on the Azure portal. Admin can configure Individual Conditional Access policy on the Application(s) and once the conditions are satisfied users can directly be redirected to the specific application.

**Pros**:

- You can define individual Conditional Access Policies.
- All Apps are represented on the 0365 Waffle and myApps.microsoft.com Panel.

**Cons**:

- You need to configure multiple IDP.

![Integration Scenario 2](media/header-akamai-tutorial/scenario-2.png)

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Akamai single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Akamai supports IDP initiated SSO.

Important

All the setup steps in the following procedure are the same for **Integration Scenario 1** and **Scenario 2**. For the **Integration scenario 2** you have to set up Individual IDP in the Akamai EAA and the Authentication configuration URL property needs to be modified to point to the application URL.

![Screenshot of the General tab for AZURESSO-SP in Akamai Enterprise Application Access. The Authentication configuration URL field is highlighted.](media/header-akamai-tutorial/important.png)

## Add Akamai from the gallery

To configure the integration of Akamai into Microsoft Entra ID, you need to add Akamai from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Akamai** in the search box.
4. Select **Akamai** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra SSO for Akamai

Configure and test Microsoft Entra SSO with Akamai using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Akamai.

To configure and test Microsoft Entra SSO with Akamai, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    - **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    - **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Akamai SSO**- to configure the single sign-on settings on application side.
    - **Setting up IDP**
    - **Header Based Authentication**
    - **Remote Desktop**
    - **SSH**
    - **Kerberos Authentication**
    - **Create Akamai test user** - to have a counterpart of B.Simon in Akamai that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Akamai** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<Yourapp>.login.go.akamai-access.com/saml/sp/response`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https:// <Yourapp>.login.go.akamai-access.com/saml/sp/response`

    Note

    These values aren't real. Update these values with the actual Identifier and Reply URL. Contact [Akamai Client support team](https://www.akamai.com/us/en/contact-us/) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
7. On the **Set up Akamai** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Akamai SSO

### Setting up IDP

**AKAMAI EAA IDP Configuration**

1. Sign in to **Akamai Enterprise Application Access** console.
2. On the **Akamai EAA console**, Select **Identity** &gt; **Identity Providers** and select **Add Identity Provider**.

    ![Screenshot of the Akamai EAA console Identity Providers window. Select Identity Providers on the Identity menu and select Add Identity Provider.](media/header-akamai-tutorial/configure-1.png)
3. On the **Create New Identity Provider** perform the following steps:

    a. Specify the **Unique Name**.

    b. Choose **Third Party SAML** and select **Create Identity Provider and Configure**.

### Configure Akamai general settings

In the **General** tab, enter the following information:

1. **Identity Intercept** - Specify the name of the domain (SP base URL–is used for Microsoft Entra Configuration).

    Note

    You can choose to have your own custom domain (requires a DNS entry and a Certificate). In this example we're going to use the Akamai Domain.
2. **Akamai Cloud Zone** - Select the Appropriate cloud zone.
3. **Certificate Validation** - Check Akamai Documentation (optional).

### Configure Akamai authentication settings

In the **Authentication Configuration** section, configure the following SAML settings:

1. URL – Specify the URL same as your identity intercept ( this is where users are redirect after authentication).
2. Logout URL : Update the logout URL.
3. Sign SAML Request: default unchecked.
4. For the IDP Metadata File, add the Application in the Microsoft Entra ID Console.

    ![Screenshot of the Akamai EAA console Authentication configuration showing settings for URL, Logout URL, Sign SAML Request, and IDP Metadata File.](media/header-akamai-tutorial/configure-4.png)

### Configure Akamai session settings

Leave the settings as default.

![Screenshot of the Akamai EAA console Session settings dialog.](media/header-akamai-tutorial/session-settings.png)

### Configure directories in Akamai

In the **Directories** tab, skip the directory configuration.

### Customize the Akamai sign-in UI

You could add customization to IDP. In the **Customization** tab, there are settings for **Customize UI**, **Language settings**, and **Themes**.

### Configure advanced Akamai SSO settings

In the **Advanced settings** tab, accept the default values. Refer to the [Akamai EAA documentation](https://techdocs.akamai.com/eaa) for more details.

### Deploy the Akamai configuration

Deploy the identity provider after you finish configuring the previous settings.

1. In the **Deployment** tab, select Deploy Identity Provider.
2. Verify the deployment was successful.

### Header Based Authentication

Akamai Header Based Authentication

1. Choose **Custom HTTP** form the Add Applications Wizard.

    ![Screenshot of the Akamai EAA console Add Applications wizard showing CustomHTTP listed in the Access Apps section.](media/header-akamai-tutorial/configure-5.png)
2. Enter **Application Name** and **Description**.

    ![Screenshot of a Custom HTTP App dialog showing settings for Application Name and Description.](media/header-akamai-tutorial/configure-6.png)

    ![Screenshot of the Akamai EAA console General tab showing general settings for MYHEADERAPP.](media/header-akamai-tutorial/configure-7.png)

    ![Screenshot of the Akamai EAA console showing settings for Certificate and Location.](media/header-akamai-tutorial/configure-8.png)

#### Authentication

1. Select **Authentication** tab.

    ![Screenshot of the Akamai EAA console with the Authentication tab selected.](media/header-akamai-tutorial/configure-9.png)
2. Select **Assign identity provider**.

#### Services

Select Save and Go to Authentication.

![Screenshot of the Akamai EAA console Services tab for MYHEADERAPP showing the Save and go to AdvancedSettings button in the bottom right corner.](media/header-akamai-tutorial/configure-11.png)

#### Advanced Settings

In Advanced Settings, configure the custom header mapping and then continue to deployment.

1. Under the **Customer HTTP Headers**, specify the **CustomerHeader** and **SAML Attribute**.

    ![Screenshot of the Akamai EAA console Advanced Settings tab showing the SSO Logged URL field highlighted under Authentication.](media/header-akamai-tutorial/configure-12.png)
2. Select **Save and go to Deployment** button.

    ![Screenshot of the Akamai EAA console Advanced Settings tab showing the Save and go to Deployment button in the bottom right corner.](media/header-akamai-tutorial/configure-13.png)

#### Deploy the Application

When configuration is complete, deploy the application.

1. Select **Deploy Application** button.

    ![Screenshot of the Akamai EAA console Deployment tab showing the Deploy application button.](media/header-akamai-tutorial/configure-14.png)
2. Verify the Application was deployed successfully.

    ![Screenshot of the Akamai EAA console Deployment tab showing the Application status message: &quot;Application Successfully Deployed&quot;.](media/header-akamai-tutorial/configure-15.png)
3. End-User Experience.

    ![Screenshot of the opening screen for myapps.microsoft.com with a background image and a Sign in dialog.](media/header-akamai-tutorial/end-user-1.png)

    ![Screenshot showing part of an Apps window with icons for Add-in, HRWEB, Akamai - CorpApps, Expense, Groups, and Access reviews.](media/header-akamai-tutorial/end-user-2.png)
4. Conditional Access.

    ![Screenshot of the message: Approve sign in request. We've sent a notification to your mobile device. Please respond to continue.](media/header-akamai-tutorial/conditional-access-1.png)

    ![Screenshot of an Applications screen showing an icon for the MyHeaderApp.](media/header-akamai-tutorial/conditional-access-2.png)

#### Remote Desktop

To configure a Remote Desktop application in Akamai EAA, perform the following steps:

1. Choose **RDP** from the ADD Applications Wizard.

    ![Screenshot of the Akamai EAA console Add Applications wizard showing RDP listed among the apps in the Access Apps section.](media/header-akamai-tutorial/configure-16.png)
2. Enter **Application Name**, such as *SecretRDPApp*.
3. Select a **Description**, such as *Protect RDP Session using Microsoft Entra Conditional Access*.
4. Specify the Connector that's servicing this.

    ![Screenshot of the Akamai EAA console showing settings for Certificate and Location. Associated connectors is set to USWST-CON1.](media/header-akamai-tutorial/configure-19.png)

#### Authentication

In the **Authentication** tab, select **Save and go to Services**.

#### Services

Select **Save and go to Advanced Settings**.

![Screenshot of the Akamai EAA console Services tab for SECRETRDPAPP showing the Save and go to AdvancedSettings button in the bottom right corner.](media/header-akamai-tutorial/configure-21.png)

#### Advanced Settings

1. Select **Save and go to Deployment**.

    ![Screenshot of the Akamai EAA console Advanced Settings tab for SECRETRDPAPP showing the settings for Remote desktop configuration.](media/header-akamai-tutorial/configure-22.png)

    ![Screenshot of the Akamai EAA console Advanced Settings tab for SECRETRDPAPP showing the settings for Authentication and Health check configuration.](media/header-akamai-tutorial/configure-23.png)

    ![Screenshot of the Akamai EAA console Custom HTTP headers settings for SECRETRDPAPP with the Save and go to Deployment button in the bottom right corner.](media/header-akamai-tutorial/configure-24.png)
2. End-User Experience

    ![Screenshot of a myapps.microsoft.com window with a background image and a Sign in dialog.](media/header-akamai-tutorial/end-user-3.png)

    ![Screenshot of the myapps.microsoft.com Apps window with icons for Add-in, HRWEB, Akamai - CorpApps, Expense, Groups, and Access reviews.](media/header-akamai-tutorial/end-user-2.png)
3. Conditional Access

    ![Screenshot of the Conditional Access message: Approve sign in request. We've sent a notification to your mobile device. Please respond to continue.](media/header-akamai-tutorial/conditional-access-4.png)

    ![Screenshot of an Applications screen showing icons for the MyHeaderApp and SecretRDPApp.](media/header-akamai-tutorial/conditional-access-5.png)

    ![Screenshot of  Windows Server 2012 RS screen showing generic user icons. The icons for administrator, user0, and user1 show that they are Signed in.](media/header-akamai-tutorial/conditional-access-6.png)
4. Alternatively, you can also directly Type the RDP Application URL.

#### SSH

To configure SSH access through Akamai EAA, complete the following steps:

1. Go to Add Applications, Choose **SSH**.

    ![Screenshot of the Akamai EAA console Add Applications wizard showing SSH listed among the apps in the Access Apps section.](media/header-akamai-tutorial/configure-25.png)
2. Enter **Application Name** and **Description**, such as *Microsoft Entra modern authentication to SSH*.
3. Configure Application Identity.

    a. Specify Name / Description.

    b. Specify Application Server IP/FQDN and port for SSH.

    c. Specify SSH username / passphrase \*Check Akamai EAA.

    d. Specify the External host Name.

    e. Specify the Location for the connector and choose the connector.

#### Authentication

In the **Authentication** tab, select **Save and go to Services**.

#### Services

Select **Save and go to Advanced Settings**.

![Screenshot of the Akamai EAA console Services tab for SSH-SECURE showing the Save and go to AdvancedSettings button in the bottom right corner.](media/header-akamai-tutorial/configure-29.png)

#### Advanced Settings

Select Save and to go Deployment.

![Screenshot of the Akamai EAA console Advanced Settings tab for SSH-SECURE showing the settings for Authentication and Health check configuration.](media/header-akamai-tutorial/configure-30.png)

![Screenshot of the Akamai EAA console Custom HTTP headers settings for SSH-SECURE with the Save and go to Deployment button in the bottom right corner.](media/header-akamai-tutorial/configure-31.png)

#### Deployment

After you finish configuring the SSH application, deploy it.

1. Select **Deploy application**.

    ![Screenshot of the Akamai EAA console Deployment tab for SSH-SECURE showing the Deploy application button.](media/header-akamai-tutorial/configure-32.png)
2. End-User Experience

    ![Screenshot of a myapps.microsoft.com window Sign in dialog.](media/header-akamai-tutorial/end-user-3.png)

    ![Screenshot of the Apps window for myapps.microsoft.com showing icons for Add-in, HRWEB, Akamai - CorpApps, Expense, Groups, and Access reviews.](media/header-akamai-tutorial/end-user-4.png)
3. Conditional Access

    ![Screenshot showing the message: Approve sign in request. We've sent a notification to your mobile device. Please respond to continue.](media/header-akamai-tutorial/conditional-access-4.png)

    ![Screenshot of an Applications screen showing icons for MyHeaderApp, SSH Secure, and SecretRDPApp.](media/header-akamai-tutorial/conditional-access-7.png)

    ![Screenshot of a command window for ssh-secure-go.akamai-access.com showing a Password prompt.](media/header-akamai-tutorial/conditional-access-8.png)

    ![Screenshot of a command window for ssh-secure-go.akamai-access.com showing information about the application and displaying a prompt for commands.](media/header-akamai-tutorial/conditional-access-9.png)

### Kerberos Authentication

In the following example we publish an internal web server at `http://frp-app1.superdemo.live` and enable SSO using KCD.

#### General Tab

The following screenshot shows the General tab settings for the Kerberos application.

![Screenshot of the Akamai EAA console General tab for MYKERBOROSAPP.](media/header-akamai-tutorial/general-tab.png)

#### Authentication Tab

In the **Authentication** tab, assign the Identity Provider.

#### Services Tab

The following screenshot shows the Services tab configuration for the Kerberos application.

![Screenshot of the Akamai EAA console Services tab for MYKERBOROSAPP.](media/header-akamai-tutorial/services-tab.png)

#### Advanced Settings

Review the Advanced Settings values shown in the following example.

![Screenshot of the Akamai EAA console Advanced Settings tab for MYKERBOROSAPP showing settings for Related Applications and Authentication.](media/header-akamai-tutorial/advance-settings-2.png)

Note

The Service Principal Name (SPN) for the Web Server has been set in SPN@Domain format, for example: `HTTP/frp-app1.superdemo.live@SUPERDEMO.LIVE` for this demo. Leave rest of the settings to default.

#### Deployment Tab

The following screenshot shows the Deployment tab for the Kerberos application.

![Screenshot of the Akamai EAA console Deployment tab for MYKERBOROSAPP showing the Deploy application button.](media/header-akamai-tutorial/deployment-tab.png)

#### Adding Directory

To add an Active Directory source, complete the following steps:

1. Select **AD** from the dropdown.

    ![Screenshot of the Akamai EAA console Directories window showing a Create New Directory dialog with AD selected in the drop down for Directory Type.](media/header-akamai-tutorial/configure-33.png)
2. Provide the necessary data.

    ![Screenshot of the Akamai EAA console SUPERDEMOLIVE window with settings for DirectoryName, Directory Service, Connector, and Attribute mapping.](media/header-akamai-tutorial/configure-34.png)
3. Verify the Directory Creation.

    ![Screenshot of the Akamai EAA console Directories window showing that the directory superdemo.live has been added.](media/header-akamai-tutorial/directory-domain.png)
4. Add the Groups/OUs who would require access.

    ![Screenshot of the settings for the directory superdemo.live. The icon that you select for adding Groups or OUs is highlighted.](media/header-akamai-tutorial/add-group.png)
5. In this example, the group is called EAAGroup and has one member.

    ![Screenshot of the Akamai EAA console GROUPS ON SUPERDEMOLIVE DIRECTORY window. The EAAGroup with 1 User is listed under Groups.](media/header-akamai-tutorial/eaagroup.png)
6. Add the Directory to your Identity Provider by selecting **Identity** &gt; **Identity Providers** and select the **Directories** Tab and Select **Assign directory**.

### Configure KCD Delegation for EAA Walkthrough

#### Step 1: Create an Account

Create the delegation account in Active Directory as follows:

1. In the example, we use an account called **EAADelegation**. You can perform this using the **Active Directory users and computer** Snappin.

    Note

    The user name has to be in a specific format based on the **Identity Intercept Name**. In this example, the Identity Intercept Name is **corpapps.login.go.akamai-access.com**
2. User logon Name is:`HTTP/corpapps.login.go.akamai-access.com`

    ![Screenshot showing EAADelegation Properties with First name set to &quot;EAADelegation&quot; and User logon name set to HTTP/corpapps.login.go.akamai-access.com.](media/header-akamai-tutorial/eaadelegation.png)

#### Step 2: Configure the Service Principal Name (SPN) for this account

Use the following command to register the SPN for the delegation account:

1. Based on this sample the SPN is as below.
2. setspn -s **Http/corpapps.login.go.akamai-access.com eaadelegation**

    ![Screenshot of an Administrator Command Prompt showing the results of the command setspn -s Http/corpapps.login.go.akamai-access.com eaadelegation.](media/header-akamai-tutorial/spn.png)

#### Step 3: Configure Delegation

Next, configure delegation settings for the EAADelegation account.

1. For the EAADelegation account select the Delegation tab.

    ![Screenshot of an Administrator Command Prompt showing the command for configuring the SPN.](media/header-akamai-tutorial/delegation.png)

    - Specify use any authentication Protocol.
    - Select Add and Add the App Pool Account for the Kerberos Website. It should automatically resolve to correct SPN if configured correctly.

#### Step 4: Create a Keytab File for AKAMAI EAA

Use the ktpass command to create a keytab file for Akamai EAA.

1. Here's the generic Syntax.
2. ktpass /out ActiveDirectorydomain.keytab /princ `HTTP/yourloginportalurl@ADDomain.com` /mapuser serviceaccount@ADdomain.com /pass +rdnPass /crypto All /ptype KRB5\_NT\_PRINCIPAL
3. Example explained

    | Snippet | Explanation |
    | --- | --- |
    | Ktpass /out EAADemo.keytab | // Name of the output Keytab file |
    | /princ HTTP/corpapps.login.go.akamai-access.com@superdemo.live | // HTTP/yourIDPName@YourdomainName |
    | /mapuser eaadelegation@superdemo.live | // EAA Delegation account |
    | /pass RANDOMPASS | // EAA Delegation account Password |
    | /crypto All ptype KRB5\_NT\_PRINCIPAL | // consult Akamai EAA documentation |
    |  |  |
4. Ktpass /out EAADemo.keytab /princ HTTP/corpapps.login.go.akamai-access.com@superdemo.live /mapuser eaadelegation@superdemo.live /pass RANDOMPASS /crypto All ptype KRB5\_NT\_PRINCIPAL

    ![Screenshot of an Administrator Command Prompt showing the results of the command for creating a Keytab File for AKAMAI EAA.](media/header-akamai-tutorial/administrator.png)

#### Step 5: Import Keytab in the AKAMAI EAA Console

After you create the keytab file, import it into the Akamai EAA console.

1. Select **System** &gt; **Keytabs**.

    ![Screenshot of the Akamai EAA console showing Keytabs being selected from the System menu.](media/header-akamai-tutorial/keytabs.png)
2. In the Keytab Type choose **Kerberos Delegation**.

    ![Screenshot of the Akamai EAA console EAAKEYTAB screen showing the Keytab settings. The Keytab Type is set to Kerberos Delegation.](media/header-akamai-tutorial/keytab-delegation.png)
3. Ensure the Keytab shows up as Deployed and Verified.

    ![Screenshot of the Akamai EAA console KEYTABS screen listing the EAA Keytab as &quot;Keytab deployed and verified&quot;.](media/header-akamai-tutorial/keytabs-2.png)
4. User Experience

    ![Screenshot of the Sign in dialog at myapps.microsoft.com.](media/header-akamai-tutorial/end-user-3.png)

    ![Screenshot of the Apps window for myapps.microsoft.com showing App icons.](media/header-akamai-tutorial/end-user-4.png)
5. Conditional Access

    ![Screenshot showing an Approve sign in request message. the message.](media/header-akamai-tutorial/conditional-access-4.png)

    ![Screenshot of an Applications screen showing icons for MyHeaderApp, SSH Secure, SecretRDPApp, and myKerberosApp.](media/header-akamai-tutorial/conditional-access-10.png)

    ![Screenshot of the splash screen for the myKerberosApp. The message &quot;Welcome superdemo\user1&quot; is displayed over a background image.](media/header-akamai-tutorial/conditional-access-11.png)

### Create Akamai test user

In this section, you create a user called B.Simon in Akamai. Work with [Akamai Client support team](https://www.akamai.com/us/en/contact-us/) to add the users in the Akamai platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, and you should be automatically signed in to the Akamai for which you set up the SSO.
- You can use Microsoft My Apps. When you select the Akamai tile in the My Apps, you should be automatically signed in to the Akamai for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).