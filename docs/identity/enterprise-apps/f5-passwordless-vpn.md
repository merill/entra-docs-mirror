---
layout: Conceptual
title: Configure F5 BIG-IP SSL-VPN solution in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/f5-passwordless-vpn
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Tutorial to configure F5 BIG-IP based secure socket layer virtual private network (SSL-VPN) solution with Microsoft Entra ID for secure hybrid access (SHA).
ms.topic: how-to
ms.date: 2024-04-19T00:00:00.0000000Z
ms.collection: M365-identity-device-management
ms.reviewer: v-nisba, gasinh
ms.custom: not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: bbfdfb4a-0d91-835f-8bfa-c0e8e24be74c
document_version_independent_id: 87467a52-a5ac-22c8-e375-ee5c3c5bd57f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/f5-passwordless-vpn.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/f5-passwordless-vpn
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/f5-passwordless-vpn.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 5843a824-38b3-e52a-37a8-d2a39ae2fe04
---

# Configure F5 BIG-IP SSL-VPN solution in Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this tutorial, learn how to integrate F5 BIG-IP based secure socket layer virtual private network (SSL-VPN) with Microsoft Entra ID for secure hybrid access (SHA).

Enabling a BIG-IP SSL-VPN for Microsoft Entra single sign-on (SSO) provides many benefits, including:

- Zero Trust governance through Microsoft Entra preauthentication and Conditional Access.
    - [Conditional Access](../conditional-access/overview)
- [Passwordless authentication](https://www.microsoft.com/security/business/identity/passwordless) to the VPN service
- Identity and access management from a single control plane, the [Microsoft Entra admin center](https://entra.microsoft.com)

To learn about more benefits, see

- [F5 BIG-IP integration with Microsoft Entra ID](f5-integration)
- [SSO in Microsoft Entra ID](what-is-single-sign-on)

    Note

    Classic VPNs remain network orientated, often providing little to no fine-grained access to corporate applications. We encourage a more identity-centric approach to achieve Zero Trust. Learn more: [Five steps for integrating all your apps with Microsoft Entra ID](../../fundamentals/five-steps-to-full-application-integration).

## Scenario description

In this scenario, the BIG-IP Access Policy Manager (APM) instance of the SSL-VPN service is configured as a Security Assertion Markup Language (SAML) service provider (SP) and Microsoft Entra ID is the trusted SAML identity provider (IdP). Single sign-on (SSO) from Microsoft Entra ID is through claims-based authentication to the BIG-IP APM, a seamless virtual private network (VPN) access experience.

![Diagram of integration architecture.](media/f5-passwordless-vpn/ssl-vpn-architecture.png)

Note

Replace example strings or values in this guide with those in your environment.

## Prerequisites

Prior experience or knowledge of F5 BIG-IP isn't necessary, however, you need:

- A Microsoft Entra subscription
    - If you don't have one, you can get an [Azure free account](https://azure.microsoft.com/trial/get-started-active-directory/)
- User identities [synchronized from their on-premises directory](../hybrid/connect/how-to-connect-sync-whatis) to Microsoft Entra ID
- One of the following roles: Cloud Application Administrator, or Application Administrator
- BIG-IP infrastructure with client traffic routing to and from the BIG-IP
    - Or [deploy a BIG-IP Virtual Edition into Azure](f5-bigip-deployment-guide)
- A record for the BIG-IP published VPN service in a public domain name server (DNS)
    - Or a test client localhost file while testing
- The BIG-IP provisioned with the needed SSL certificates for publishing services over HTTPS

To improve the tutorial experience, you can learn industry-standard terminology on the F5 BIG-IP [Glossary](https://www.f5.com/services/resources/glossary).

## Add F5 BIG-IP from the Microsoft Entra gallery

Set up a SAML federation trust between the BIG-IP to allow the Microsoft Entra BIG-IP to hand off the preauthentication and [Conditional Access](../conditional-access/overview) to Microsoft Entra ID, before it grants access to the published VPN service.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **All applications**, then select **New application**.
3. In the gallery, search for *F5* and select **F5 BIG-IP APM Microsoft Entra ID integration**.
4. Enter a name for the application.
5. Select **Add** then **Create**.
6. The name, as an icon, appears in the Microsoft Entra admin center and Office 365 portal.

## Configure Microsoft Entra SSO

1. With F5 application properties, go to **Manage** &gt; **Single sign-on**.
2. On the **Select a single sign-on method** page, select **SAML**.
3. Select **No, I'll save later**.
4. On the **Setup single sign-on with SAML** menu, select the pen icon for **Basic SAML Configuration**.
5. Replace the **Identifier URL** with your BIG-IP published service URL. For example, `https://ssl-vpn.contoso.com`.
6. Replace the **Reply URL**, and the SAML endpoint path. For example, `https://ssl-vpn.contoso.com/saml/sp/profile/post/acs`.

    Note

    In this configuration, the application operates in an IdP-initiated mode: Microsoft Entra ID issues a SAML assertion before redirecting to the BIG-IP SAML service.
7. For apps that don't support IdP-initiated mode, for the BIG-IP SAML service, specify the **Sign-on URL**, for example, `https://ssl-vpn.contoso.com`.
8. For the Logout URL, enter the BIG-IP APM Single logout (SLO) endpoint prepended by the host header of the service being published. For example, `https://ssl-vpn.contoso.com/saml/sp/profile/redirect/slr`

    Note

    An SLO URL ensures a user session terminates, at BIG-IP and Microsoft Entra ID, after the user signs out. BIG-IP APM has an option to terminate all sessions when calling an application URL. Learn more on the F5 article, [K12056: Overview of the Logout URI Include option](https://support.f5.com/csp/article/K12056).

![Screenshot of basic SAML configuration URLs.](media/f5-passwordless-vpn/basic-saml-configuration.png).

Note

From TMOS v16, the SAML SLO endpoint has changed to /saml/sp/profile/redirect/slo.

1. Select **Save**
2. Skip the SSO test prompt.
3. In **User Attributes & Claims** properties, observe the details.

    ![Screenshot of user attributes and claims properties.](media/f5-passwordless-vpn/user-attributes-claims.png)

You can add other claims to your BIG-IP published service. Claims defined in addition to the default set are issued if they're in Microsoft Entra ID. Define directory [roles or group](../hybrid/connect/how-to-connect-fed-group-claims) memberships against a user object in Microsoft Entra ID, before they can be issued as a claim.

SAML signing certificates created by Microsoft Entra ID have a lifespan of three years.

### Microsoft Entra authorization

By default, Microsoft Entra ID issues tokens to users with granted access to a service.

1. In the application configuration view, select **Users and groups**.
2. Select **+ Add user**.
3. In the **Add Assignment** menu, select **Users and groups**.
4. In the **Users and groups** dialog, add the user groups authorized to access the VPN
5. Select **Select** &gt; **Assign**.

    ![Screenshot of the Add User option.](media/f5-passwordless-vpn/add-user-link.png)

You can set up BIG-IP APM to publish the SSL-VPN service. Configure it with corresponding properties to complete the trust for SAML preauthentication.

## BIG-IP APM configuration

### SAML federation

To complete federating the VPN service with Microsoft Entra ID, create the BIG-IP SAML service provider and corresponding SAML IDP objects.

1. Go to **Access** &gt; **Federation** &gt; **SAML Service Provider** &gt; **Local SP Services**.
2. Select **Create**.

    ![Screenshot of the Create option on the Local SP Services page.](media/f5-passwordless-vpn/bigip-saml-configuration.png)
3. Enter a **Name** and the **Entity ID** defined in Microsoft Entra ID.
4. Enter the Host fully qualified domain name (FQDN) to connect to the application.

    ![Screenshot of Name and Entity entries.](media/f5-passwordless-vpn/create-new-saml-sp.png)

    Note

    If the entity ID isn't an exact match of the hostname of the published URL, configure SP **Name** settings, or perform this action if it isn't in hostname URL format. If entity ID is `urn:ssl-vpn:contosoonline`, provide the external scheme and hostname of the application being published.
5. Scroll down to select the new **SAML SP object**.
6. Select **Bind/UnBind IDP Connectors**.

    ![Screenshot of the Bind Unbind IDP Connections option on the Local SP Services page.](media/f5-passwordless-vpn/federation-local-sp-service.png)
7. Select **Create New IDP Connector**.
8. From the drop-down menu, select **From Metadata**

    ![Screenshot of the From Metadata option on the Edit SAML IdPs page.](media/f5-passwordless-vpn/create-new-idp-connector.png)
9. Browse to the federation metadata XML file you downloaded.
10. For the APM object, provide an **Identity Provider Name** that represents the external SAML IdP.
11. To select the new Microsoft Entra external IdP connector, select **Add New Row**.

    ![Screenshot of SAML IdP Connectors option on the Edit SAML IdP page.](media/f5-passwordless-vpn/external-idp-connector.png)
12. Select **Update**.
13. Select **OK**.

    ![Screenshot of the Common, VPN Azure link on the Edit SAML IdPs page.](media/f5-passwordless-vpn/saml-idp-using-sp.png)

### Webtop configuration

Enable the SSL-VPN to be offered to users via the BIG-IP web portal.

1. Go to **Access** &gt; **Webtops** &gt; **Webtop Lists**.
2. Select **Create**.
3. Enter a portal name.
4. Set the type to **Full**, for example, `Contoso_webtop`.
5. Complete the remaining preferences.
6. Select **Finished**.

    ![Screenshot of name and type entries in General Properties.](media/f5-passwordless-vpn/webtop-configuration.png)

### VPN configuration

VPN elements control aspects of the overall service.

1. Go to **Access** &gt; **Connectivity/VPN** &gt; **Network Access (VPN)** &gt; **IPV4 Lease Pools**
2. Select **Create**.
3. Enter a name for the IP address pool allocated to VPN clients. For example, Contoso\_vpn\_pool.
4. Set type to **IP Address Range**.
5. Enter a start and end IP.
6. Select **Add**.
7. Select **Finished**.

    ![Screenshot of name and member list entries in General Properties.](media/f5-passwordless-vpn/vpn-configuration.png)

A Network access list provisions the service with IP and DNS settings from the VPN pool, user routing permissions, and can launch applications.

1. Go to **Access** &gt; **Connectivity/VPN: Network Access (VPN)** &gt; **Network Access Lists**.
2. Select **Create**.
3. Provide a name for the VPN access list and caption, for example, Contoso-VPN.
4. Select **Finished**.

    ![Screenshot of name entry in General Properties, and caption entry in Customization Settings for English.](media/f5-passwordless-vpn/vpn-configuration-network-access-list.png)
5. From the top ribbon, select **Network Settings**.
6. For **Supported IP version**: IPV4.
7. For **IPV4 Lease Pool**, select the VPN pool created, for example, Contoso\_vpn\_pool

    ![Screenshot of the IPV4 Lease Pool entry in General Settings.](media/f5-passwordless-vpn/contoso-vpn-pool.png)

    Note

    Use the Client Settings options to enforce restrictions for how client traffic is routed in an established VPN.
8. Select **Finished**.
9. Go to the **DNS/Hosts** tab.
10. For **IPV4 Primary Name Server**: Your environment DNS IP
11. For **DNS Default Domain Suffix**: The domain suffix for this VPN connection. For example, contoso.com

Note

See the F5 article, [Configuring Network Access Resources](https://techdocs.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-network-access-11-5-0/2.html) for other settings.

A BIG-IP connection profile is required to configure VPN client-type settings the VPN service needs to support. For example, Windows, OSX, and Android.

1. Go to **Access** &gt; **Connectivity/VPN** &gt; **Connectivity** &gt; **Profiles**
2. Select **Add**.
3. Enter a profile name.
4. Set the parent profile to **/Common/connectivity**, for example, Contoso\_VPN\_Profile.

    ![Screenshot of Profile Name and Parent Name entries in Create New Connectivity Profile.](media/f5-passwordless-vpn/create-connectivity-profile.png)

## Access profile configuration

An access policy enables the service for SAML authentication.

1. Go to **Access** &gt; **Profiles/Policies** &gt; **Access Profiles (Per-Session Policies)**.
2. Select **Create**.
3. Enter a profile name and for the profile type.
4. Select **All**, for example, Contoso\_network\_access.
5. Scroll down and add at least one language to the **Accepted Languages** list
6. Select **Finished**.

    ![Screenshot of Name, Profile Type, and Language entries on New Profile.](media/f5-passwordless-vpn/general-properties.png)
7. In the new access profile, on the Per-Session Policy field, select **Edit**.
8. The visual policy editor opens in a new tab.

    ![Screenshot of the Edit option on Access Profiles, presession policies.](media/f5-passwordless-vpn/per-session-policy.png)
9. Select the **+** sign.
10. In the menu, select **Authentication** &gt; **SAML Auth**.
11. Select **Add Item**.
12. In the SAML authentication SP configuration, select the VPN SAML SP object you created
13. Select **Save**.

    ![Screenshot of the AAA Server entry under SAML Authentication SP, on the Properties tab.](media/f5-passwordless-vpn/saml-authentication.png)
14. For the Successful branch of SAML auth, select **+** .
15. From the Assignment tab, select **Advanced Resource Assign**.
16. Select **Add Item**.
17. In the pop-up, select **New Entry**
18. Select **Add/Delete**.
19. In the window, select **Network Access**.
20. Select the Network Access profile you created.

    ![Screenshot of the Add new entry button on Resource Assignment, on the Properties tab.](media/f5-passwordless-vpn/add-new-entry.png)
21. Go to the **Webtop** tab.
22. Add the Webtop object you created.

    ![Screenshot of the created webtop on the Webtop tab.](media/f5-passwordless-vpn/add-webtop-object.png)
23. Select **Update**.
24. Select**Save**.
25. To change the Successful branch, select the link in the upper **Deny** box.
26. The Allow label appears.
27. **Save**.

    ![Screenshot of the Deny option on Access Policy.](media/f5-passwordless-vpn/vizual-policy-editor.png)
28. Select **Apply Access Policy**
29. Close the visual policy editor tab.

    ![Screenshot of the Apply Access Policy option.](media/f5-passwordless-vpn/access-policy-manager.png)

## Publish the VPN service

The APM requires a front-end virtual server to listen for clients connecting to the VPN.

1. Select **Local Traffic** &gt; **Virtual Servers** &gt; **Virtual Server List**.
2. Select **Create**.
3. For the VPN virtual server, enter a **Name**, for example, VPN\_Listener.
4. Select an unused **IP Destination Address** with routing to receive client traffic.
5. Set the Service Port to **443 HTTPS**.
6. For **State**, ensure **Enabled** is selected.

    ![Screenshot of Name and Destination Address or Mask entries on General Properties.](media/f5-passwordless-vpn/new-virtual-server.png)
7. Set the **HTTP Profile** to **http**.
8. Add the SSL Profile (Client) for the public SSL certificate you created.

    ![Screenshot of HTTP Profile entry for client, and SSL Profile selected entries for client.](media/f5-passwordless-vpn/ssl-profile.png)
9. To use the created VPN objects, under Access Policy, set the **Access Profile** and **Connectivity Profile**.

    ![Screenshot of Access Profile and Connectivity Profile entries on Access Policy.](media/f5-passwordless-vpn/access-policy.png)
10. Select **Finished**.

Your SSL-VPN service is published and accessible via SHA, either with its URL or through Microsoft application portals.