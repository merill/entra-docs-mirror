---
layout: Conceptual
title: Configure the F5 BIG-IP Easy Button for Header-based and LDAP SSO - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/f5-big-ip-ldap-header-easybutton
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Learn to configure the F5 BIG-IP Access Policy Manager (APM) and Microsoft Entra ID for secure hybrid access to header-based applications that also require session augmentation through Lightweight Directory Access Protocol (LDAP) sourced attributes.
ms.topic: how-to
ms.date: 2024-04-19T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
ms.custom: not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 4d0edc9c-0389-71bf-0957-5dfb5a05b39d
document_version_independent_id: 41403fc0-5d47-287b-e6a7-9d73fe0e22e1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/f5-big-ip-ldap-header-easybutton.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/f5-big-ip-ldap-header-easybutton
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/f5-big-ip-ldap-header-easybutton.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 7d5a6d8e-84ac-fee6-5b23-712dbb9716e0
---

# Configure the F5 BIG-IP Easy Button for Header-based and LDAP SSO - Microsoft Entra ID | Microsoft Learn

In this article, you can learn to secure header and LDAP-based applications using Microsoft Entra ID, by using the F5 BIG-IP Easy Button Guided Configuration 16.1. Integrating a BIG-IP with Microsoft Entra ID provides many benefits:

- Improved governance: See, [Zero Trust framework to enable remote work](https://www.microsoft.com/security/blog/2020/04/02/announcing-microsoft-zero-trust-assessment-tool/)and learn more about Microsoft Entra pre-authentication
    - See also, [What is Conditional Access?](../conditional-access/overview) to learn about how it helps enforce organizational policies
- Full single sign-on (SSO) between Microsoft Entra ID and BIG-IP published services
- Manage identities and access from one control plane, the [Microsoft Entra admin center](https://entra.microsoft.com)

To learn about more benefits, see [F5 BIG-IP and Microsoft Entra integration](f5-integration).

## Scenario description

This scenario focuses on the classic, legacy application using **HTTP authorization headers** sourced from LDAP directory attributes, to manage access to protected content.

Because it's legacy, the application lacks modern protocols to support a direct integration with Microsoft Entra ID. You can modernize the app, but it's costly, requires planning, and introduces risk of potential downtime. Instead, you can use an F5 BIG-IP Application Delivery Controller (ADC) to bridge the gap between the legacy application and the modern ID control plane, with protocol transitioning.

Having a BIG-IP in front of the app enables overlay of the service with Microsoft Entra pre-authentication and header-based SSO, improving the overall security posture of the application.

## Scenario architecture

The secure hybrid access solution for this scenario has:

- **Application** - BIG-IP published service to be protected by Microsoft Entra ID secure hybrid access (SHA)
- **Microsoft Entra ID** - Security Assertion Markup Language (SAML) identity provider (IdP) that verifies user credentials, Conditional Access, and SAML-based SSO to the BIG-IP. With SSO, Microsoft Entra ID provides the BIG-IP with required session attributes.
- **HR system** - LDAP-based employee database as the source of truth for application permissions
- **BIG-IP** - Reverse proxy and SAML service provider (SP) to the application, delegating authentication to the SAML IdP, before performing header-based SSO to the back-end application

SHA for this scenario supports SP and IdP initiated flows. The following image illustrates the SP initiated flow.

![Diagram of the secure hybrid access SP-initiated flow.](media/f5-big-ip-easy-button-ldap/sp-initiated-flow.png)

1. User connects to application endpoint (BIG-IP)
2. BIG-IP APM access policy redirects user to Microsoft Entra ID (SAML IdP)
3. Microsoft Entra ID pre-authenticates user and applies enforced Conditional Access policies
4. User is redirected to BIG-IP (SAML SP) and SSO is performed using issued SAML token
5. BIG-IP requests more attributes from LDAP based HR system
6. BIG-IP injects Microsoft Entra ID and HR system attributes as headers in request to application
7. Application authorizes access with enriched session permissions

## Prerequisites

Prior BIG-IP experience isn't necessary, but you need:

- An [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn/), or a higher-tier subscription
- A BIG-IP or [deploy a BIG-IP Virtual Edition (VE) in Azure](f5-bigip-deployment-guide)
- Any of the following F5 BIG-IP licenses:
    - F5 BIG-IP® Best bundle
    - F5 BIG-IP Access Policy Manager™ (APM) standalone license
    - F5 BIG-IP Access Policy Manager™ (APM) add-on license on a BIG-IP F5 BIG-IP® Local Traffic Manager™ (LTM)
    - 90-day BIG-IP product [Free Trial](https://www.f5.com/trial/big-ip-trial.php)
- User identities [synchronized](../hybrid/connect/how-to-connect-sync-whatis) from an on-premises directory to Microsoft Entra ID
- One of the following roles: Cloud Application Administrator, or Application Administrator.
- An [SSL Web certificate](f5-bigip-deployment-guide#ssl-profile) for publishing services over HTTPS, or use default BIG-IP certificates while testing
- A header-based application or [set up a simple IIS header app](/en-us/previous-versions/iis/6.0-sdk/ms525396%28v=vs.90%29) for testing
- A user directory that supports LDAP, such as Windows Active Directory Lightweight Directory Services (AD LDS), OpenLDAP, and so on.

## BIG-IP configuration

This tutorial uses Guided Configuration 16.1 with an Easy Button template. With the Easy Button, admins don't go back and forth between Microsoft Entra ID and a BIG-IP to enable services for SHA. The deployment and policy management is handled between the APM Guided Configuration wizard and Microsoft Graph. This integration between BIG-IP APM and Microsoft Entra ID ensures applications support identity federation, SSO, and Microsoft Entra Conditional Access, reducing administrative overhead.

Note

Replace example strings or values in this guide with those for your environment.

## Register Easy Button

Before a client or service can access Microsoft Graph, it's trusted by the [Microsoft identity platform.](../../identity-platform/quickstart-register-app)

This first step creates a tenant app registration to authorize the **Easy Button** access to Graph. With these permissions, the BIG-IP can push the configurations to establish a trust between a SAML SP instance for published application, and Microsoft Entra ID as the SAML IdP.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations** &gt; **New registration**.
3. Enter a display name for your application. For example, F5 BIG-IP Easy Button.
4. Specify who can use the application &gt; **Accounts in this organizational directory only**.
5. Select **Register**.
6. Navigate to **API permissions** and authorize the following Microsoft Graph **Application permissions**:

    - Application.Read.All
    - Application.ReadWrite.All
    - Application.ReadWrite.OwnedBy
    - Directory.Read.All
    - Group.Read.All
    - IdentityRiskyUser.Read.All
    - Policy.Read.All
    - Policy.ReadWrite.ApplicationConfiguration
    - Policy.ReadWrite.ConditionalAccess
    - User.Read.All
7. Grant admin consent for your organization.
8. On **Certificates & Secrets**, generate a new **client secret**. Make a note of this secret.
9. On **Overview**, note the **Client ID** and **Tenant ID**.

## Configure the Easy Button

Initiate the APM **Guided Configuration** to launch the **Easy Button** template.

1. Navigate to **Access &gt; Guided Configuration &gt; Microsoft Integration** and select **Microsoft Entra Application**.
2. Review the list of steps and select **Next**
3. To publish your application, follow the steps.

    ![Screenshot of the configuration flow on Guided Configuration.](media/f5-big-ip-easy-button-ldap/config-steps-flow.png#lightbox)

### Configuration Properties

The **Configuration Properties** tab creates a BIG-IP application config and SSO object. The **Azure Service Account Details** section represents the client you registered in your Microsoft Entra tenant earlier, as an application. These settings allow a BIG-IP OAuth client to register a SAML SP in your tenant, with the SSO properties you would configure manually. Easy Button does this action for every BIG-IP service published and enabled for SHA.

Some of these settings are global, therefore can be reused to publish more applications, reducing deployment time and effort.

1. Enter a unique **Configuration Name** so admins can distinguish between Easy Button configurations.
2. Enable **Single Sign-On (SSO) & HTTP Headers**.
3. Enter the **Tenant ID**, **Client ID**, and **Client Secret** you noted when registering the Easy Button client in your tenant.
4. Confirm the BIG-IP can connect to your tenant.
5. Select **Next**.

### Service Provider

The Service Provider settings define the properties for the SAML SP instance of the application protected through SHA.

1. Enter **Host**, the public fully qualified domain name (FQDN) of the application being secured.
2. Enter **Entity ID**, the identifier Microsoft Entra ID uses to identify the SAML SP requesting a token. Use the optional **Security Settings** to specify whether Microsoft Entra ID encrypts issued SAML assertions. Encrypting assertions between Microsoft Entra ID and the BIG-IP APM provides assurance the content tokens can’t be intercepted, and personal or corporate data can't be compromised.
3. From the **Assertion Decryption Private Key** list, select **Create New**

    ![Screenshot of the Create New option under Assertion Decryption Private Key, on Security Settings.](media/f5-big-ip-oracle/configure-security-create-new.png)
4. Select **OK**. The **Import SSL Certificate and Keys** dialog opens in a new tab.
5. Select **PKCS 12 (IIS)** to import your certificate and private key. After provisioning, close the browser tab to return to the main tab.

    ![Screenshot of Import Type, Certificate and Key Name, Certificate Key Source, and Password entries](media/f5-big-ip-oracle/import-ssl-certificates-and-keys.png)
6. Check **Enable Encrypted Assertion**.
7. If you enabled encryption, select your certificate from the **Assertion Decryption Private Key** list. BIG-IP APM uses this certificate private key to decrypt Microsoft Entra assertions.
8. If you enabled encryption, select your certificate from the **Assertion Decryption Certificate** list. BIG-IP uploads this certificate to Microsoft Entra ID to encrypt the issued SAML assertions.

    ![Screenshot of Assertion Decryption Private Key and Assertion Decryption Certificate entries, on Security Settings.](media/f5-big-ip-easy-button-ldap/service-provider-security-settings.png)

### Microsoft Entra ID

This section contains properties to manually configure a new BIG-IP SAML application in your Microsoft Entra tenant. Easy Button has application templates for Oracle PeopleSoft, Oracle E-business Suite, Oracle JD Edwards, SAP ERP, and an SHA template for other apps.

For this scenario, select **F5 BIG-IP APM Microsoft Entra ID Integration &gt; Add**.

#### Azure Configuration

1. Enter **Display Name** of the app that the BIG-IP creates in your Microsoft Entra tenant, and the icon that users see on [MyApps portal](https://myapplications.microsoft.com/).
2. Make no entry for **Sign On URL (optional)**.
3. To locate the certificate you imported, select the **Refresh** icon next to the **Signing Key** and **Signing Certificate**.
4. Enter the certificate password in **Signing Key Passphrase**.
5. Enable **Signing Option** (optional) to ensure BIG-IP accepts tokens and claims signed by Microsoft Entra ID.

    ![Screenshot of Signing Key, Signing Certificate, and Signing Key Passphrase entries on SAML Signing Certificate.](media/f5-big-ip-easy-button-ldap/azure-configuration-sign-certificates.png)
6. **User and User Groups** are dynamically queried from your Microsoft Entra tenant and authorize access to the application. Add a user or group for testing, otherwise access is denied.

    ![Screenshot of the Add option on User and User Groups.](media/f5-big-ip-easy-button-ldap/azure-configuration-add-user-groups.png)

#### User Attributes & Claims

When a user authenticates, Microsoft Entra ID issues a SAML token with a default set of claims and attributes uniquely identifying the user. The **User Attributes & Claims** tab shows the default claims to issue for the new application. It also lets you configure more claims.

For this example, include one more attribute:

1. For **Claim Name** enter **employeeid**.
2. For **Source Attribute** enter **user.employeeid**.

    ![Screenshot of the employeeid value under Additional Claims, on User Attributes and Claims.](media/f5-big-ip-easy-button-ldap/user-attributes-claims.png)

#### Additional User Attributes

On the **Additional User Attributes** tab, you can enable session augmentation for distributed systems such as Oracle, SAP, and other JAVA-based implementations requiring attributes stored in other directories. Attributes fetched from an LDAP source can be injected as more SSO headers to control access based on roles, Partner IDs, and so on.

1. Enable the **Advanced Settings** option.
2. Check the **LDAP Attributes** check box.
3. In Choose Authentication Server, select **Create New**.
4. Depending on your setup, select either **Use pool** or **Direct** Server Connection mode to provide the **Server Address** of the target LDAP service. If using a single LDAP server, select **Direct**.
5. For **Service Port** enter 389, 636 (Secure), or another port your LDAP service uses.
6. For **Base Search DN** enter the distinguished name of the location containing the account the APM authenticates with, for LDAP service queries.

    ![Screenshot of LDAP Server Properties entries on Additional User Attributes.](media/f5-big-ip-easy-button-ldap/additional-user-attributes.png)
7. For **Search DN** enter the distinguished name of the location containing the user account objects that the APM queries via LDAP.
8. Set both membership options to **None** and add the name of the user object attribute to be returned from the LDAP directory. For this scenario: **eventroles**.

    ![Screenshot of LDAP Query Properties entries.](media/f5-big-ip-easy-button-ldap/user-properties-ldap.png)

#### Conditional Access Policy

Conditional Access policies are enforced after Microsoft Entra pre-authentication to control access based on device, application, location, and risk signals.

The **Available Policies** view lists Conditional Access policies that don't include user actions.

The **Selected Policies** view shows policies targeting all resources. These policies can't be deselected or moved to the Available Policies list because they're enforced at a tenant level.

To select a policy to be applied to the application being published:

1. In the **Available Policies** list, select a policy.
2. Select the right arrow and move it to the **Selected Policies** list.

    Note

    Selected policies have an **Include** or **Exclude** option checked. If both options are checked, the selected policy is not enforced.

    ![Screenshot of excluded policies, under Selected Policies, on Conditional Access Policy.](media/f5-big-ip-kerberos-easy-button/conditional-access-policy.png)

    Note

    The policy list is enumerated once, when you initially select this tab. Use the **Refresh** button to manually force the wizard to query your tenant. This button appears when the application is deployed.

### Virtual Server Properties

A virtual server is a BIG-IP data plane object represented by a virtual IP address listening for client requests to the application. Received traffic is processed and evaluated against the APM profile associated with the virtual server, before directed according to policy.

1. Enter the **Destination Address**, an available IPv4/IPv6 address the BIG-IP can use to receive client traffic. There should be a corresponding record in domain name server (DNS), which enables clients to resolve the external URL of your BIG-IP published application to this IP, instead of the application. Using a test PC localhost DNS is acceptable for testing.
2. For **Service Port** enter 443 and HTTPS.
3. Check **Enable Redirect Port** and then enter **Redirect Port** to redirects incoming HTTP client traffic to HTTPS.
4. The Client SSL Profile enables the virtual server for HTTPS, so client connections are encrypted over Transport Layer Security (TLS). Select the **Client SSL Profile** you created or leave the default while testing.

    ![Screenshot of Destination Address, Service Port, and Common entries under General Properties on Virtual Server Properties.](media/f5-big-ip-easy-button-ldap/virtual-server.png)

### Pool Properties

The **Application Pool** tab has the services behind a BIG-IP represented as a pool, with one or more application servers.

1. Choose from **Select a Pool**. Create a new pool or select one.
2. Choose the **Load Balancing Method** such as Round Robin.
3. For **Pool Servers** select a node or specify an IP and port for the server hosting the header-based application.

    ![Screenshot of IP Address/Node Name and Port entries under Application Pool, on Pool Properties.](media/f5-big-ip-oracle/application-pool.png)

Note

Our back-end application sits on HTTP port 80. Switch to 443 if yours is HTTPS.

### Single sign-on and HTTP Headers

Enabling SSO allows users to access BIG-IP published services without entering credentials. The **Easy Button wizard** supports Kerberos, OAuth Bearer, and HTTP authorization headers for SSO.

Use the following list to configure options.

- **Header Operation:** Insert
- **Header Name:** upn
- **Header Value:** %{session.saml.last.identity}
- **Header Operation:** Insert
- **Header Name:** employeeid
- **Header Value:** %{session.saml.last.attr.name.employeeid}
- **Header Operation:** Insert
- **Header Name:** eventroles
- **Header Value:** %{session.ldap.last.attr.eventroles}

    ![Screenshot of SSO Headers entries under SSO Headers on SSO and HTTP Headers.](media/f5-big-ip-easy-button-ldap/sso-headers.png)

Note

APM session variables in curly brackets are case-sensitive. For example, if you enter OrclGUID and the Microsoft Entra attribute name is orclguid, an attribute mapping failure occurs.

### Session management settings

The BIG-IPs session management settings define the conditions under which user sessions are terminated or allowed to continue, limits for users and IP addresses, and corresponding user info. Refer to the F5 article [K18390492: Security | BIG-IP APM operations guide](https://support.f5.com/csp/article/K18390492) for details on these settings.

What isn’t covered is Single Log Out (SLO) functionality, which ensures sessions between the IdP, the BIG-IP, and the user agent terminate as users sign out. When the Easy Button instantiates a SAML application in your Microsoft Entra tenant, it populates the sign-out URL with the APM SLO endpoint. An IdP-initiated sign-out from the Microsoft Entra My Apps portal terminates the session between the BIG-IP and a client.

The SAML federation metadata for the published application is imported from your tenant, which provides the APM with the SAML sign out endpoint for Microsoft Entra ID. This action ensures an SP-initiated sign out terminates the session between a client and Microsoft Entra ID. The APM needs to know when a user signs out of the application.

If the BIG-IP webtop portal is used to access published applications, then APM processes sign-out to call the Microsoft Entra sign-out endpoint. But, consider a scenario wherein the BIG-IP webtop portal isn’t used. The user can't instruct the APM to sign out. Even if the user signs out of the application, the BIG-IP is oblivious. Therefore, consider SP-initiated sign out to ensure sessions terminate securely. You can add an SLO function to an application Sign-out button, so it can redirect your client to the Microsoft Entra SAML or BIG-IP sign-out endpoint. The URL for SAML sign-out endpoint for your tenant is in **App Registrations &gt; Endpoints**.

If you can't make a change to the app, then consider having the BIG-IP listen for the application sign-out call, and upon detecting the request have it trigger SLO. Refer to the [Oracle PeopleSoft SLO guidance](f5-big-ip-oracle-peoplesoft-easy-button#peoplesoft-single-logout) to learn about BIG-IP iRules. For more information about using BIG-IP iRules, see:

- [K42052145: Configuring automatic session termination based on a URI-referenced file name](https://support.f5.com/csp/article/K42052145)
- [K12056: Overview of the Log-out URI Include option](https://support.f5.com/csp/article/K12056)

## Summary

This last step provides a breakdown of your configurations.

Select **Deploy** to commit settings and verify the application is in your tenant list of Enterprise applications.

Your application is published and accessible via SHA, either with its URL or through Microsoft application portals. For increased security, organizations using this pattern can block direct access to the application. This action forces a strict path through the BIG-IP.