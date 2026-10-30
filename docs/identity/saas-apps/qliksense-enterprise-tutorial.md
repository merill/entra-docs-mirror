---
layout: Conceptual
title: Configure Qlik Sense Enterprise Client-Managed for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/qliksense-enterprise-tutorial
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
description: Learn how to configure single sign-on between Microsoft Entra ID and Qlik Sense Enterprise Client-Managed.
ms.topic: how-to
ms.date: 2025-05-20T00:00:00.0000000Z
locale: en-us
document_id: 725a7b74-1b0f-1ba6-8d23-661dc31e0e38
document_version_independent_id: 8f34c027-02af-98ef-ad1b-401883d727b0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/qliksense-enterprise-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/qliksense-enterprise-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/qliksense-enterprise-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d4d4a7b4-0fda-82bf-1417-89d7e666b41d
---

# Configure Qlik Sense Enterprise Client-Managed for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Qlik Sense Enterprise Client-Managed with Microsoft Entra ID. When you integrate Qlik Sense Enterprise Client-Managed with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Qlik Sense Enterprise.
- Enable your users to be automatically signed-in to Qlik Sense Enterprise with their Microsoft Entra accounts.
- Manage your accounts in one central location.

There are two versions of Qlik Sense Enterprise. While this article covers integration with the client-managed releases, a different process is required for Qlik Sense Enterprise SaaS (Qlik Cloud version).

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Qlik Sense Enterprise single sign-on (SSO) enabled subscription.
- Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Microsoft Entra ID. For more information, see [Azure built-in roles](../role-based-access-control/permissions-reference).

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Qlik Sense Enterprise supports **SP** initiated SSO.
- Qlik Sense Enterprise supports **just-in-time provisioning**

## Add Qlik Sense Enterprise from the gallery

To configure the integration of Qlik Sense Enterprise into Microsoft Entra ID, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Qlik Sense Enterprise** in the search box.
4. Select **Qlik Sense Enterprise** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Qlik Sense Enterprise

Configure and test Microsoft Entra SSO with Qlik Sense Enterprise using a test user called **Britta Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Qlik Sense Enterprise.

To configure and test Microsoft Entra SSO with Qlik Sense Enterprise, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with Britta Simon.
    2. **Assign the Microsoft Entra test user** - to enable Britta Simon to use Microsoft Entra single sign-on.
2. **Configure Qlik Sense Enterprise SSO**- to configure the single sign-on settings on application side.
    1. **Create Qlik Sense Enterprise test user** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Qlik Sense Enterprise** application integration page, find the **Manage** section and select **Single sign-on**.
3. On the **Select a Single sign-on method** page, select **SAML**.
4. On the **Set up Single Sign-On with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows to edit Basic S A M L Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier** textbox, type a URL using one of the following patterns:

    | Identifier |
    | --- |
    | `https://<Fully Qualified Domain Name>.qlikpoc.com` |
    | `https://<Fully Qualified Domain Name>.qliksense.com` |

    b. In the **Reply URL** textbox, type a URL using the following pattern:

    `https://<Fully Qualified Domain Name>:443{/virtualproxyprefix}/samlauthn/`

    c. In the **Sign on URL** textbox, type a URL using the following pattern: `https://<Fully Qualified Domain Name>:443{/virtualproxyprefix}/hub`

    Note

    These values aren't real. Update these values with the actual Identifier, Reply URL and Sign on URL which are explained later in this article or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values. The default port for the URLs is 443 but you can customize it per your Organization need.
6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, find **Federation Metadata XML** from the given options as per your requirement and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/metadataxml.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Qlik Sense Enterprise SSO

1. Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.
2. In the QMC, select the **Virtual Proxies** menu item.

    ![Screenshot shows Virtual proxies selected from CONFIGURE SYSTEM.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png)
3. At the bottom of the screen, select the **Create new** button.

    ![Screenshot shows the Create new option.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png)
4. The Virtual proxy edit screen appears. On the right side of the screen is a menu for making configuration options visible.

    ![Screenshot shows Identification selected from Properties.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png)
5. With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.

    ![Screenshot shows Edit virtual proxy Identification section where you can enter the values described.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png)

    a. The **Description** field is a friendly name for the virtual proxy configuration. Enter a value for a description.

    b. The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Microsoft Entra single sign-on. Enter a unique prefix name for this virtual proxy.

    c. **Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.

    d. The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication. This name must be unique.
6. Select the Authentication menu option to make it visible. The Authentication screen appears.

    ![Screenshot shows Edit virtual proxy Authentication section where you can enter the values described.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png)

    a. The **Anonymous access mode** dropdown list determines if anonymous users may access Qlik Sense through the virtual proxy. The default option is **No anonymous user**.

    b. The **Authentication method** dropdown list determines the authentication scheme the virtual proxy uses. Select SAML from the dropdown list. More options appear as a result.

    c. In the **SAML host URI field**, input the host name that users enter to access Qlik Sense through this SAML virtual proxy. The host name is the URI of the Qlik Sense server.

    d. In the **SAML entity ID**, enter the same value entered for the SAML host URI field.

    e. The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Microsoft Entra Configuration** section. **Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Microsoft Entra ID and Qlik Sense server. **Please refer to the instructions above if the file has yet to be edited.** If the file has been edited select the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.

    f. Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Microsoft Entra ID sends to the Qlik Sense server. Schema reference information is available in the Azure app screens post configuration. To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.

    g. Enter the value for the **user directory** that's attached to users when they authenticate to Qlik Sense server through Microsoft Entra ID. Hardcoded values must be surrounded by **square brackets []**. To use an attribute sent in the Microsoft Entra SAML assertion, enter the name of the attribute in this text box **without** square brackets.

    h. The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration. If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.

    i. The SAML attribute mapping section allows for other attributes like groups to be sent to Qlik Sense for use in security rules.
7. Select the **LOAD BALANCING** menu option to make it visible. The Load Balancing screen appears.

    ![Screenshot shows the Virtual proxy edit screen for LOAD BALANCING where you can select Add new server node.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png)
8. Select the **Add new server node** button, select engine node or nodes Qlik Sense send sessions to for load balancing purposes, and select the **Add** button.

    ![Screenshot shows the Add server nodes to load balance on dialog button where you can Add servers.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png)
9. Select the Advanced menu option to make it visible. The Advanced screen appears.

    ![Screenshot shows the Edit virtual proxy Advanced screen.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png)

    The Host allowlist identifies host names that are accepted when connecting to the Qlik Sense server. **Enter the host name that users will specify when connecting to Qlik Sense server.** The host name is the same value as the SAML host URI without the `https://`.
10. Select the **Apply** button.

    ![Screenshot shows the Apply button.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png)
11. Select OK to accept the warning message that states proxy linked to the virtual proxy is restarted.

    ![Screenshot shows the Apply changes to virtual proxy confirmation message.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png)
12. On the right side of the screen, the Associated items menu appears. Select the **Proxies** menu option.

    ![Screenshot shows Proxies selected from Associated items.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png)
13. The proxy screen appears. Select the **Link** button at the bottom to link a proxy to the virtual proxy.

    ![Screenshot shows the Link button.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png)
14. Select the proxy node that supports this virtual proxy connection and select the **Link** button. After linking, the proxy is listed under associated proxies.

    ![Screenshot shows Select proxy services.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png)

    ![Screenshot shows Associated proxies in the Virtual proxy associated items dialog box.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png)
15. After about five to 10 seconds, the Refreshed QMC message appears. Select the **Refresh QMC** button.

    ![Screenshot shows the message Your session has ended.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png)
16. When the QMC refreshes, select the **Virtual proxies** menu item. The new SAML virtual proxy entry is listed in the table on the screen. Single select the virtual proxy entry.

    ![Screenshot shows Virtual proxies with a single entry.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png)
17. At the bottom of the screen, the Download SP metadata button activates. Select the **Download SP metadata** button to save the metadata to a file.

    ![Screenshot shows the Download S P metadata button.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png)
18. Open the sp metadata file. Observe the **entityID** entry and the **AssertionConsumerService** entry. These values are equivalent to the **Identifier**, **Sign on URL** and the **Reply URL** in the Microsoft Entra application configuration. Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Microsoft Entra application configuration if they aren't matching, then you should replace them in the Microsoft Entra App configuration wizard.

    ![Screenshot shows a plain text editor with an EntityDescriptor with entityID and AssertionConsumerService called out.](media/qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png)

### Create Qlik Sense Enterprise test user

Qlik Sense Enterprise supports **just-in-time provisioning**, Users automatically added to the 'USERS' repository of Qlik Sense Enterprise as they use the SSO feature. In addition, clients can use the QMC and create a UDC (User Directory Connector) for prepopulating users in Qlik Sense Enterprise from their LDAP of choice such as Active Directory, and others.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Qlik Sense Enterprise Sign-on URL where you can initiate the sign-in flow.
- Go to Qlik Sense Enterprise Sign-on URL directly and initiate the sign-in flow from there.
- You can use Microsoft My Apps. When you select the Qlik Sense Enterprise tile in the My Apps, this option redirects to Qlik Sense Enterprise Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).