---
layout: Conceptual
title: Configure Advanced F5 Kerberos Delegation for Multi-Tier SaaS Architectures - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/advance-kerbf5-tutorial
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
description: In this article, learn the steps you need to perform to integrate F5 with Microsoft Entra ID.
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 0bc8964e-8f20-01fe-55d8-9a5c6e02f08f
document_version_independent_id: da28c41f-d09c-d0a1-6682-cc9e57572e96
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/advance-kerbf5-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/advance-kerbf5-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/advance-kerbf5-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ee931cc7-f526-0386-e391-63ff59b7b225
---

# Configure Advanced F5 Kerberos Delegation for Multi-Tier SaaS Architectures - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate F5 with Microsoft Entra ID. When you integrate F5 with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to F5.
- Enable your users to be automatically signed-in to F5 with their Microsoft Entra accounts.
- Manage your accounts in one central location.

To learn more about SaaS app integration with Microsoft Entra ID, see [What is application access and single sign-on with Microsoft Entra ID](../enterprise-apps/what-is-single-sign-on).

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- F5 single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

F5 supports **SP and IDP** initiated SSO.

F5 SSO can be configured in three different ways:

- Configure F5 single sign-on for Advanced Kerberos application
- [Configure F5 single sign-on for Header Based application](f5-big-ip-headers-easy-button)
- [Configure F5 single sign-on for Kerberos application](kerbf5-tutorial)

## Adding F5 from the gallery

To configure the integration of F5 into Microsoft Entra ID, you need to add F5 from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. To add new application, select **New application**.
4. In the **Add from the gallery** section, type **F5** in the search box.
5. Select **F5** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides).

## Configure and test Microsoft Entra single sign-on for F5

Configure and test Microsoft Entra SSO with F5 using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in F5.

To configure and test Microsoft Entra SSO with F5, complete the following building blocks:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure F5-SSO**- to configure the single sign-on settings on application side.
    1. **Create F5 test user** - to have a counterpart of B.Simon in F5 that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **F5** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the edit/pen icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, enter the values for the following fields:

    a. In the **Identifier** text box, type a URL using the following pattern: `https://<YourCustomFQDN>.f5.com/`

    b. In the **Reply URL** text box, type a URL using the following pattern: `https://<YourCustomFQDN>.f5.com/`
6. Select **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type a URL using the following pattern: `https://<YourCustomFQDN>.f5.com/`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [F5 Client support team](https://support.f5.com/csp/knowledge-center/software/BIG-IP?module=BIG-IP%20APM45) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
7. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
8. On the **Set up F5** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure F5 SSO

- [Configure F5 single sign-on for Header Based application](f5-big-ip-headers-easy-button)
- [Configure F5 single sign-on for Kerberos application](kerbf5-tutorial)

### Configure F5 single sign-on for Advanced Kerberos application

1. Open a new web browser window and sign into your F5 (Advanced Kerberos) company site as an administrator and perform the following steps:
2. You need to import the Metadata Certificate into the F5 (Advanced Kerberos) which is used later in the setup process. Go to **System &gt; Certificate Management &gt; Traffic Certificate Management &gt;&gt; SSL Certificate List**. Select **Import** of the right-hand corner.

    ![Screenshot that highlights the Import button for importing the Metadata Certificate.](media/advance-kerbf5-tutorial/configure01.png)
3. To setup the SAML IDP, go to **Access &gt; Federation &gt; SAML Service Provider &gt; Create &gt; From Metadata**.

    ![Screenshot that highlights how to create the SAML IDP from metadata.](media/advance-kerbf5-tutorial/configure02.png)

    ![Screenshot that shows the Create New SAML IdP Connector screen.](media/advance-kerbf5-tutorial/configure03.png)

    ![F5 (Advanced Kerberos) configuration](media/advance-kerbf5-tutorial/configure04.png)

    ![Screenshot that shows the Single Sign On Service Settings screen.](media/advance-kerbf5-tutorial/configure05.png)
4. Specify the Certificate uploaded from Task 3

    ![Screenshot that shows the Edit SAML IdP Connector screen.](media/advance-kerbf5-tutorial/configure06.png)

    ![Screenshot that shows the Single Logout Service Settings screen.](media/advance-kerbf5-tutorial/configure07.png)
5. To setup the SAML SP, go to **Access &gt; Federation &gt; SAML Service Federation &gt; Local SP Services &gt; Create**.

    ![Screenshot that shows the screen where you create a local SP service.](media/advance-kerbf5-tutorial/configure08.png)
6. Select **OK**.
7. Select the SP Configuration and Select **Bind/UnBind IdP Connectors**.

    ![Screenshot that shows the SAML Service Provider.](media/advance-kerbf5-tutorial/configure09.png)
8. Select **Add New Row** and Select the **External IdP connector** created in previous step.

    ![Screenshot that highlights the Add New Row button.](media/advance-kerbf5-tutorial/configure10.png)
9. For configuring Kerberos SSO, **Access &gt; Single Sign-on &gt; Kerberos**

    Note

    you need the Kerberos Delegation Account to be created and specified. Refer KCD Section ( Refer Appendix for Variable References)

    - Username Source `session.saml.last.attr.name.http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    - User Realm Source `session.logon.last.domain`

    ![Screenshot that highlights Access &gt; Single Sign On.](media/advance-kerbf5-tutorial/configure11.png)
10. For configuring Access Profile, **Access &gt; Profile/Policies &gt; Access Profile (per session policies)**.

    ![Screenshot that highlights the Properties tab under the Profiles/Policies menu option.](media/advance-kerbf5-tutorial/configure12.png)

    ![Screenshot that shows the SSO/Auth Domains tab.](media/advance-kerbf5-tutorial/configure13.png)

    Select the **Access Policy** tab to view **General Properties** and **AAA Servers**. For **Visual Policy Editor**, select a policy for a profile to edit, in this example, **KerbApp200**.

    ![Screenshot that shows the Properties tab on the Access Policy.](media/advance-kerbf5-tutorial/configure15.png)

    ![Screenshot that shows the properties for Variable Assign.](media/advance-kerbf5-tutorial/configure16.png)

    - session.logon.last.usernameUPN expr {[mcget {session.saml.last.identity}]}
    - session.ad.lastactualdomain TEXT superdemo.live

        Edit the query properties to specify the server *superdemo.live* and **SearchFilter** value **(userPrincipalName=%{session.logon.last.usernameUPN})**.
    - (userPrincipalName=%{session.logon.last.usernameUPN})

        Select **Branch Rules** to add a branch rule and **Properties** to view properties.

    ![Screenshot that shows the custom variable and custom expression text boxes.](media/advance-kerbf5-tutorial/configure19.png)

    - session.logon.last.username expr { "[mcget {session.ad.last.attr.sAMAccountName}]" }

    ![Screenshot that shows the values in the SSO Token Name and SSO Token Password fields.](media/advance-kerbf5-tutorial/configure20.png)

    - mcget {session.logon.last.username}
    - mcget {session.logon.last.password}
11. For adding new node, go to **Local Traffic &gt; Nodes &gt; Node List &gt; +**.

    ![Screenshot that highlights Local Traffic &gt; Nodes.](media/advance-kerbf5-tutorial/configure21.png)
12. To create a new Pool, go to **Local Traffic &gt; Pools &gt; Pool List &gt; Create**.

    ![Screenshot that highlights Local Traffic &gt; Pools.](media/advance-kerbf5-tutorial/configure22.png)
13. To create a new virtual server, go to **Local Traffic &gt; Virtual Servers &gt; Virtual Server List &gt; +**.

    ![Screenshot that highlights Local Traffic &gt; Virtual Servers.](media/advance-kerbf5-tutorial/configure23.png)
14. Specify the Access Profile Created in Previous Step.

    ![Screenshot that shows where you specify the access profile that you created.](media/advance-kerbf5-tutorial/configure24.png)

### Setting up Kerberos Delegation

Note

For more details refer [here](https://www.f5.com/pdf/deployment-guides/kerberos-constrained-delegation-dg.pdf)

- **Step 1: Create a Delegation Account**

    - Example

    ```
    Domain Name : superdemo.live
    Sam Account Name : big-ipuser
    
    New-ADUser -Name "APM Delegation Account" -UserPrincipalName host/big-ipuser.superdemo.live@superdemo.live -SamAccountName "big-ipuser" -PasswordNeverExpires $true -Enabled $true -AccountPassword (Read-Host -AsSecureString "Password!1234")
    ```
- **Step 2: Set SPN (on the APM Delegation Account)**

    - Example

    ```
    setspn –A host/big-ipuser.superdemo.live big-ipuser
    ```
- **Step 3: SPN Delegation ( for the App Service Account)**

    - Set up the appropriate Delegation for the F5 Delegation Account.
    - In the example below, APM Delegation account is being configured for KCD for FRP-App1.superdemo.live app.

        ![Screenshot that shows the APM Delegation Account Properties &gt; Delegation tab.](media/advance-kerbf5-tutorial/configure25.png)

1. Provide the details as mentioned in the above reference document under [this](https://techdocs.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-authentication-single-sign-on-12-1-0/2.html)
2. Appendix- SAML – F5 BIG-IP Variable mappings shown below:

    ![Screenshot that shows the Overview &gt; Active Sessions tab.](media/advance-kerbf5-tutorial/configure26.png)

    ![Screenshot that shows the variables and session keys.](media/advance-kerbf5-tutorial/configure27.png)
3. Below is the whole list of default SAML Attributes. GivenName is represented using the following string. `session.saml.last.attr.name.http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`

| Session | Attribute |
| --- | --- |
| eb46b6b6.session.saml.last.assertionID | `<TENANT ID>` |
| eb46b6b6.session.saml.last.assertionIssueInstant | `<ID>` |
| eb46b6b6.session.saml.last.assertionIssuer | `https://sts.windows.net/<TENANT ID>`/ |
| eb46b6b6.session.saml.last.attr.name.http://schemas.microsoft.com/claims/authnmethodsreferences | `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password` |
| eb46b6b6.session.saml.last.attr.name.http://schemas.microsoft.com/identity/claims/displayname | user0 |
| eb46b6b6.session.saml.last.attr.name.http://schemas.microsoft.com/identity/claims/identityprovider | `https://sts.windows.net/<TENANT ID>/` |
| eb46b6b6.session.saml.last.attr.name.http://schemas.microsoft.com/identity/claims/objectidentifier | `<TENANT ID>` |
| eb46b6b6.session.saml.last.attr.name.http://schemas.microsoft.com/identity/claims/tenantid | `<TENANT ID>` |
| eb46b6b6.session.saml.last.attr.name.http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress | `user0@superdemo.live` |
| eb46b6b6.session.saml.last.attr.name.http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname | user0 |
| eb46b6b6.session.saml.last.attr.name.http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name | `user0@superdemo.live` |
| eb46b6b6.session.saml.last.attr.name.http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname | 0 |
| eb46b6b6.session.saml.last.audience | `https://kerbapp.superdemo.live` |
| eb46b6b6.session.saml.last.authNContextClassRef | urn:oasis:names:tc:SAML:2.0:ac:classes:Password |
| eb46b6b6.session.saml.last.authNInstant | `<ID>` |
| eb46b6b6.session.saml.last.identity | `user0@superdemo.live` |
| eb46b6b6.session.saml.last.inResponseTo | `<TENANT ID>` |
| eb46b6b6.session.saml.last.nameIDValue | `user0@superdemo.live` |
| eb46b6b6.session.saml.last.nameIdFormat | urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress |
| eb46b6b6.session.saml.last.responseDestination | `https://kerbapp.superdemo.live/saml/sp/profile/post/acs` |
| eb46b6b6.session.saml.last.responseId | `<TENANT ID>` |
| eb46b6b6.session.saml.last.responseIssueInstant | `<ID>` |
| eb46b6b6.session.saml.last.responseIssuer | `https://sts.windows.net/<TENANT ID>/` |
| eb46b6b6.session.saml.last.result | 1 |
| eb46b6b6.session.saml.last.samlVersion | 2.0 |
| eb46b6b6.session.saml.last.sessionIndex | `<TENANT ID>` |
| eb46b6b6.session.saml.last.statusValue | urn:oasis:names:tc:SAML:2.0:status:Success |
| eb46b6b6.session.saml.last.subjectConfirmDataNotOnOrAfter | `<ID>` |
| eb46b6b6.session.saml.last.subjectConfirmDataRecipient | `https://kerbapp.superdemo.live/saml/sp/profile/post/acs` |
| eb46b6b6.session.saml.last.subjectConfirmMethod | urn:oasis:names:tc:SAML:2.0:cm:bearer |
| eb46b6b6.session.saml.last.validityNotBefore | `<ID>` |
| eb46b6b6.session.saml.last.validityNotOnOrAfter | `<ID>` |

### Create F5 test user

In this section, you create a user called B.Simon in F5. Work with [F5 Client support team](https://support.f5.com/csp/knowledge-center/software/BIG-IP?module=BIG-IP%20APM45) to add the users in the F5 platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration using the Access Panel.

When you select the F5 tile in the Access Panel, you should be automatically signed in to the F5 for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).