---
layout: Conceptual
title: Configure SAP Fiori for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/sap-fiori-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and SAP Fiori.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: has-azure-ad-ps-ref, azure-ad-ref-level-one-done, sfi-image-nochange
locale: en-us
document_id: efe6b3e0-1d76-4af4-54af-0c51ff5492af
document_version_independent_id: 2c6e6802-ac18-799e-2d50-57e0e1bec8b4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/sap-fiori-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/sap-fiori-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/sap-fiori-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 368dbbb2-5634-d50c-dd7d-18a94c23364f
---

# Configure SAP Fiori for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate SAP Fiori with Microsoft Entra ID. When you integrate SAP Fiori with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to SAP Fiori.
- Enable your users to be automatically signed-in to SAP Fiori with their Microsoft Entra accounts.
- Manage your accounts in one central location.

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- SAP Fiori single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- SAP Fiori supports **SP** initiated SSO

Note

For SAP Fiori initiated iFrame Authentication, we recommend using the **IsPassive** parameter in the SAML AuthnRequest for silent authentication. For more details of the **IsPassive** parameter refer to [Microsoft Entra SAML single sign-on](../../identity-platform/single-sign-on-saml-protocol) information.

## Adding SAP Fiori from the gallery

To configure the integration of SAP Fiori into Microsoft Entra ID, you need to add SAP Fiori from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **SAP Fiori** in the search box.
4. Select **SAP Fiori** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for SAP Fiori

Configure and test Microsoft Entra SSO with SAP Fiori using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in SAP Fiori.

To configure and test Microsoft Entra SSO with SAP Fiori, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure SAP Fiori SSO**- to configure the single sign-on settings on application side.
    1. **Create SAP Fiori test user** - to have a counterpart of B.Simon in SAP Fiori that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Open a new web browser window and sign in to your SAP Fiori company site as an administrator.
2. Make sure that **http** and **https** services are active and that the relevant ports are assigned to transaction code **SMICM**.
3. Sign in to SAP Business Client for SAP system **T01**, where single sign-on is required. Then, activate HTTP Security Session Management.

    1. Go to transaction code **SICF\_SESSIONS**. All relevant profile parameters with current values are shown. They look like the following example:

        ```
        login/create_sso2_ticket = 2
        login/accept_sso2_ticket = 1
        login/ticketcache_entries_max = 1000
        login/ticketcache_off = 0  login/ticket_only_by_https = 0
        icf/set_HTTPonly_flag_on_cookies = 3
        icf/user_recheck = 0  http/security_session_timeout = 1800
        http/security_context_cache_size = 2500
        rdisp/plugin_auto_logout = 1800
        rdisp/autothtime = 60
        ```

        Note

        Adjust the parameters based on your organization requirements. The preceding parameters are given only as an example.
    2. If necessary, adjust parameters in the instance (default) profile of the SAP system and restart the SAP system.
    3. Double-select the relevant client to enable an HTTP security session.

        ![The Current Values of Relevant Profile Parameters page in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-profileparameter.png)
    4. Activate the following SICF services:

        ```
        /sap/public/bc/sec/saml2
        /sap/public/bc/sec/cdc_ext_service
        /sap/bc/webdynpro/sap/saml2
        /sap/bc/webdynpro/sap/sec_diag_tool (This is only to enable / disable trace)
        ```
4. Go to transaction code **SAML2** in Business Client for SAP system [**T01/122**]. The configuration UI opens in a new browser window. In this example, we use Business Client for SAP system 122.

    ![The SAP Fiori Business Client sign-in page](media/sapfiori-tutorial/tutorial-sapnetweaver-sapbusinessclient.png)
5. Enter your username and password, and then select **Log on**.

    ![The SAML 2.0 Configuration of ABAP System T01/122 page in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-userpwd.png)
6. In the **Provider Name** box, replace **T01122** with **http://T01122**, and then select **Save**.

    Note

    By default, the provider name is in the format &lt;sid&gt;&lt;client&gt;. Microsoft Entra ID expects the name in the format &lt;protocol&gt;://&lt;name&gt;. We recommend that you maintain the provider name as https://&lt;sid&gt;&lt;client&gt; so you can configure multiple SAP Fiori ABAP engines in Microsoft Entra ID.

    ![The updated provider name in the SAML 2.0 Configuration of ABAP System T01/122 page in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-providername.png)
7. Select **Local Provider tab** &gt; **Metadata**.
8. In the **SAML 2.0 Metadata** dialog box, download the generated metadata XML file and save it on your computer.

    ![The Download Metadata link in the SAP SAML 2.0 Metadata dialog box](media/sapfiori-tutorial/tutorial-sapnetweaver-generatesp.png)
9. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
10. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **SAP Fiori** &gt; **Single sign-on**.
11. On the **Select a single sign-on method** page, select **SAML**.
12. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Edit Basic SAML Configuration](common/edit-urls.png)
13. On the **Basic SAML Configuration** section, if you have **Service Provider metadata file**, perform the following steps:

    1. Select **Upload metadata file**.

        ![Upload metadata file](common/upload-metadata.png)
    2. Select **folder logo** to select the metadata file and select **Upload**.

        ![choose metadata file](common/browse-upload-metadata.png)
    3. When the metadata file is successfully uploaded, the **Identifier** and **Reply URL** values are automatically populated in the **Basic SAML Configuration** pane. In the **Sign on URL** box, enter a URL that has the following pattern: `https://<your company instance of SAP Fiori>`.

        Note

        Some customers have encountered an error of an incorrect Reply URL configured for their instance. If you receive any such error, use these PowerShell commands. First update the Reply URLs in the application object with the Reply URL, then update the service principal. Use the [Get-MgServicePrincipal](/en-us/powershell/module/microsoft.graph.applications/get-mgserviceprincipal) to get the Service Principal ID value.

        ```powershell
        $params = @{
           web = @{
              redirectUris = "<Your Correct Reply URL>"
           }
        }
        Update-MgApplication -ApplicationId "<Application ID>" -BodyParameter $params
        Update-MgServicePrincipal -ServicePrincipalId "<Service Principal ID>" -ReplyUrls "<Your Correct Reply URL>"
        ```
14. The SAP Fiori application expects the SAML assertions to be in a specific format. Configure the following claims for this application. To manage these attribute values, in the **Set up Single Sign-On with SAML** pane, select **Edit**.

    ![The User attributes pane](common/edit-attribute.png)
15. In the **User Attributes & Claims** pane, configure the SAML token attributes as shown in the preceding image. Then, complete the following steps:

    1. Select **Edit** to open the **Manage user claims** pane.
    2. In the **Transformation** list, select **ExtractMailPrefix()**.
    3. In the **Parameter 1** list, select **user.userprincipalname**.
    4. Select **Save**.

        ![The Manage user claims pane](media/sapfiori-tutorial/nameidattribute.png)

        ![The Transformation section in the Manage user claims pane](media/sapfiori-tutorial/nameidattribute1.png)
16. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

    ![The Certificate download link](common/metadataxml.png)
17. On the **Set up SAP Fiori** section, copy the appropriate URL(s) based on your requirement.

    ![Copy configuration URLs](common/copy-configuration-urls.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure SAP Fiori SSO

1. Sign in to the SAP system and go to transaction code **SAML2**. A new browser window opens with the SAML configuration page.
2. To configure endpoints for a trusted identity provider (Microsoft Entra ID), select the **Trusted Providers** tab.

    ![The Trusted Providers tab in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-samlconfig.png)
3. Select **Add**, and then select **Upload Metadata File** from the context menu.

    ![The Add and Upload Metadata File options in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-uploadmetadata.png)
4. Upload the metadata file that you downloaded. Select **Next**.

    ![Select the metadata file to upload in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-metadatafile.png)
5. On the next page, in the **Alias** box, enter the alias name. For example, **aadsts**. Select **Next**.

    ![The Alias box in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-aliasname.png)
6. Make sure that the value in the **Digest Algorithm** box is **SHA-256**. Select **Next**.

    ![Verify the Digest Algorithm value in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-identityprovider.png)
7. Under **Single Sign-On Endpoints**, select **HTTP POST**, and then select **Next**.

    ![Single Sign-On Endpoints options in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-httpredirect.png)
8. Under **Single Logout Endpoints**, select **HTTP Redirect**, and then select **Next**.

    ![Single Logout Endpoints options in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-httpredirect1.png)
9. Under **Artifact Endpoints**, select **Next** to continue.

    ![Artifact Endpoints options in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-artifactendpoint.png)
10. Under **Authentication Requirements**, select **Finish**.

    ![Authentication Requirements options and the Finish option in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-authentication.png)
11. Select **Trusted Provider** &gt; **Identity Federation** (at the bottom of the page). Select **Edit**.

    ![The Trusted Provider and Identity Federation tabs in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-trustedprovider.png)
12. Select **Add**.

    ![The Add option on the Identity Federation tab](media/sapfiori-tutorial/tutorial-sapnetweaver-addidentityprovider.png)
13. In the **Supported NameID Formats** dialog box, select **Unspecified**. Select **OK**.

    ![The Supported NameID Formats dialog box and options in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-nameid.png)

    The values for **User ID Source** and **User ID Mapping Mode** determine the link between the SAP user and the Microsoft Entra claim.

    **Scenario 1**: SAP user to Microsoft Entra user mapping

    1. In SAP, under **Details of NameID Format "Unspecified"**, note the details:

        ![Screenshot that shows the 'Details of NameID Format &quot;Unspecified&quot;' dialog box in S A P.](media/sapfiori-tutorial/nameiddetails.png)
    2. In the Azure portal, under **User Attributes & Claims**, note the required claims from Microsoft Entra ID.

        ![Screenshot that shows the &quot;User Attributes &amp; Claims&quot; dialog box.](media/sapfiori-tutorial/claimsaad1.png)

    **Scenario 2**: Select the SAP user ID based on the configured email address in SU01. In this case, the email ID should be configured in SU01 for each user who requires SSO.

    1. In SAP, under **Details of NameID Format "Unspecified"**, note the details:

        ![The Details of NameID Format &quot;Unspecified&quot; dialog box in SAP](media/sapfiori-tutorial/tutorial-sapnetweaver-nameiddetails1.png)
    2. In the Azure portal, under **User Attributes & Claims**, note the required claims from Microsoft Entra ID.

        ![The User Attributes and Claims dialog box in the Azure portal](media/sapfiori-tutorial/claimsaad2.png)
14. Select **Save**, and then select **Enable** to enable the identity provider.

    ![The Save and Enable options in SAP](media/sapfiori-tutorial/configuration1.png)
15. Select **OK** when prompted.

    ![The OK option in SAML 2.0 Configuration dialog box in SAP](media/sapfiori-tutorial/configuration2.png)

### Create SAP Fiori test user

In this section, you create a user named Britta Simon in SAP Fiori. Work with your in-house SAP team of experts or your organization SAP partner to add the user in the SAP Fiori platform.

## Test SSO

1. After the identity provider Microsoft Entra ID is activated in SAP Fiori, try to access one of the following URLs to test single sign-on (you shouldn't be prompted for a username and password):

    - `https://<sap-url>/sap/bc/bsp/sap/it00/default.htm`
    - `https://<sap-url>/sap/bc/bsp/sap/it00/default.htm`

    Note

    Replace `<sap-url>` with the actual SAP host name.
2. The test URL should take you to the following test application page in SAP. If the page opens, Microsoft Entra single sign-on is successfully set up.

    ![The standard test application page in SAP](media/sapfiori-tutorial/testingsso.png)
3. If you're prompted for a username and password, enable trace to help diagnose the issue. Use the following URL for the trace:

    `https://<sap-url>/sap/bc/webdynpro/sap/sec_diag_tool?sap-client=122&sap-language=EN#`.