---
layout: Conceptual
title: Configure F5 BIG-IP Easy Button for SSO to Oracle JD Edwards using Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/f5-big-ip-oracle-jd-edwards-easy-button
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: celested
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn to implement SHA with header-based single sign-on to Oracle JD Edwards using F5’s BIG-IP Easy Button guided configuration
ms.topic: how-to
ms.date: 2025-03-25T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 36828b99-0703-e1cf-0fb6-e07700767d7d
document_version_independent_id: 7e68d542-dc8a-2503-6717-09b3d8ef7a92
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/f5-big-ip-oracle-jd-edwards-easy-button.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/f5-big-ip-oracle-jd-edwards-easy-button
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/f5-big-ip-oracle-jd-edwards-easy-button.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: a668482e-3133-6edc-d8aa-d355a0172a7c
---

# Configure F5 BIG-IP Easy Button for SSO to Oracle JD Edwards using Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, learn to secure Oracle JD Edwards (JDE) using Microsoft Entra ID, through F5’s BIG-IP Easy Button guided configuration.

Integrating a BIG-IP with Microsoft Entra ID provides many benefits, including:

- [Improved Zero Trust governance](https://www.microsoft.com/security/blog/2020/04/02/announcing-microsoft-zero-trust-assessment-tool/) through Microsoft Entra preauthentication and [Conditional Access](../conditional-access/overview)
- Full SSO between Microsoft Entra ID and BIG-IP published services
- Manage Identities and access from a single control plane, the [Azure portal](https://portal.azure.com/)

To learn about all the benefits, see the article on [F5 BIG-IP and Microsoft Entra integration](../enterprise-apps/f5-integration) and [what is application access and single sign-on with Microsoft Entra ID](/en-us/azure/active-directory/active-directory-appssoaccess-whatis).

## Scenario description

This scenario looks at the classic **Oracle JDE application** using **HTTP authorization headers** to manage access to protected content.

Being legacy, the application lacks modern protocols to support a direct integration with Microsoft Entra ID. The application can be modernized, but it's costly, requires careful planning, and introduces risk of potential downtime. Instead, an F5 BIG-IP Application Delivery Controller (ADC) is used to bridge the gap between the legacy application and the modern ID control plane, through protocol transitioning.

Having a BIG-IP in front of the app enables us to overlay the service with Microsoft Entra preauthentication and header-based SSO, significantly improving the overall security posture of the application.

## Scenario architecture

The secure hybrid access (SHA) solution for this scenario is made up of several components:

**Oracle JDE Application:** BIG-IP published service to be protected by Microsoft Entra SHA.

**Microsoft Entra ID:** Security Assertion Markup Language (SAML) Identity Provider (IdP) responsible for verification of user credentials, Conditional Access, and SAML based SSO to the BIG-IP. Through SSO, Microsoft Entra ID provides the BIG-IP with any required session attributes.

**BIG-IP:** Reverse proxy and SAML service provider (SP) to the application, delegating authentication to the SAML IdP before performing header-based SSO to the Oracle service.

SHA for this scenario supports both SP and IdP initiated flows. The following image illustrates the SP initiated flow.

![Secure hybrid access - SP initiated flow](media/f5-big-ip-easy-button-oracle-jde/sp-initiated-flow.png)

| Steps | Description |
| --- | --- |
| 1 | User connects to application endpoint (BIG-IP) |
| 2 | BIG-IP APM access policy redirects user to Microsoft Entra ID (SAML IdP) |
| 3 | Microsoft Entra ID preauthenticates user and applies any enforced Conditional Access policies |
| 4 | User is redirected back to BIG-IP (SAML SP) and SSO is performed using issued SAML token |
| 5 | BIG-IP injects Microsoft Entra attributes as headers in request to the application |
| 6 | Application authorizes request and returns payload |

## Prerequisites

Prior BIG-IP experience isn’t necessary, but you need:

- A Microsoft Entra ID Free subscription or above
- An existing BIG-IP or [deploy a BIG-IP Virtual Edition (VE) in Azure](../enterprise-apps/f5-bigip-deployment-guide)
- Any of the following F5 BIG-IP license SKUs

    - F5 BIG-IP® Best bundle
    - F5 BIG-IP Access Policy Manager™ (APM) standalone license
    - F5 BIG-IP Access Policy Manager™ (APM) add-on license on an existing BIG-IP F5 BIG-IP® Local Traffic Manager™ (LTM)
    - 90-day BIG-IP full feature [trial license](https://www.f5.com/trial/big-ip-trial.php).
- User identities [synchronized](../hybrid/connect/how-to-connect-sync-whatis) from an on-premises directory to Microsoft Entra ID or created directly within Microsoft Entra ID and flowed back to your on-premises directory
- An account with Microsoft Entra Application Administrator [permissions](/en-us/azure/active-directory/users-groups-roles/directory-assign-admin-roles#application-administrator)
- An [SSL Web certificate](../enterprise-apps/f5-bigip-deployment-guide#ssl-profile) for publishing services over HTTPS, or use default BIG-IP certs while testing
- An existing Oracle JDE environment

## BIG-IP configuration methods

There are many methods to configure BIG-IP for this scenario, including two template-based options and an advanced configuration. This article covers the latest Guided Configuration 16.1 offering an Easy button template. With the Easy Button, admins no longer go back and forth between Microsoft Entra ID and a BIG-IP to enable services for SHA. The deployment and policy management is handled directly between the APM’s Guided Configuration wizard and Microsoft Graph. This rich integration between BIG-IP APM and Microsoft Entra ID ensures that applications can quickly, easily support identity federation, SSO, and Microsoft Entra Conditional Access, reducing administrative overhead.

Note

All example strings or values referenced throughout this guide should be replaced with those for your actual environment.

## Register the F5 BIG-IP Easy Button in Microsoft Entra ID

Before a client or service can access Microsoft Graph, it must be trusted by the [Microsoft identity platform.](../../identity-platform/quickstart-register-app)

This first step creates a tenant app registration that's used to authorize the **Easy Button** access to Graph. Through these permissions, the BIG-IP is allowed to push the configurations required to establish a trust between a SAML SP instance for published application, and Microsoft Entra ID as the SAML IdP.

1. Sign in to the [Azure portal](https://portal.azure.com/) using an account with Application Administrative rights.
2. From the left navigation pane, select the **Microsoft Entra ID** service.
3. Under Manage, select **App registrations** &gt; **New registration**.
4. Enter a display name for your application, such as `F5 BIG-IP Easy Button`.
5. Specify who can use the application &gt; **Accounts in this organizational directory only**.
6. Select **Register** to complete the initial app registration.
7. Navigate to **API permissions** and authorize the following Microsoft Graph **Application permissions**:

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
8. Grant admin consent for your organization
9. Go to **Certificates & Secrets**, generate a new **Client secret** and note it down
10. Go to **Overview**, note the **Client ID** and **Tenant ID**

## Configure the F5 BIG-IP Easy Button settings

Initiate the APM's **Guided Configuration** to launch the **Easy Button** Template.

1. Navigate to **Access &gt; Guided Configuration &gt; Microsoft Integration** and select **Microsoft Entra Application**.
2. Under **Configuring the solution using the below steps will create the required objects**, review the list of configuration steps and select **Next**.
3. Under **Guided Configuration**, follow the sequence of steps required to publish your application.

### Configure Easy Button configuration properties

The **Configuration Properties** tab creates a BIG-IP application config and SSO object. Consider the **Azure Service Account Details** section to represent the client you registered in your Microsoft Entra tenant earlier, as an application. These settings allow a BIG-IP's OAuth client to individually register a SAML SP directly in your tenant, along with the SSO properties you would normally configure manually. Easy Button does this for every BIG-IP service being published and enabled for SHA.

Some of these are global settings can be reused for publishing more applications, further reducing deployment time and effort.

1. Provide a unique **Configuration Name** that enables an admin to easily distinguish between Easy Button configurations
2. Enable **Single Sign-On (SSO) & HTTP Headers**
3. Enter the **Tenant Id, Client ID**, and **Client Secret** you noted down from your registered application
4. Before you select **Next**, confirm the BIG-IP can successfully connect to your tenant.

    ![Screenshot for Configuration General and Service Account properties](media/f5-big-ip-easy-button-oracle-jde/configuration-general-and-service-account-properties.png)

### Configure service provider settings

The Service Provider settings define the properties for the SAML SP instance of the application protected through SHA.

1. Enter **Host**. This is the public FQDN of the application being secured
2. Enter **Entity ID**. This is the identifier Microsoft Entra ID will use to identify the SAML SP requesting a token

    ![Screenshot for Service Provider settings](media/f5-big-ip-easy-button-oracle-jde/service-provider-settings.png)

    Next, under optional **Security Settings** specify whether Microsoft Entra ID should encrypt issued SAML assertions. Encrypting assertions between Microsoft Entra ID and the BIG-IP APM provides assurance that the content tokens can’t be intercepted, and personal or corporate data be compromised.
3. From the **Assertion Decryption Private Key** list, select **Create New**

    ![Screenshot for Configure Easy Button- Create New import](media/f5-big-ip-easy-button-oracle-jde/configure-security-create-new.png)
4. Select **OK**. This opens the **Import SSL Certificate and Keys** dialog in a new tab
5. Select **PKCS 12 (IIS)** to import your certificate and private key. Once provisioned close the browser tab to return to the main tab.

    ![Screenshot for Configure Easy Button- Import new cert](media/f5-big-ip-easy-button-oracle-jde/import-ssl-certificates-and-keys.png)
6. Check **Enable Encrypted Assertion**
7. If you have enabled encryption, select your certificate from the **Assertion Decryption Private Key** list. This is the private key for the certificate that BIG-IP APM uses to decrypt Microsoft Entra assertions
8. If you have enabled encryption, select your certificate from the **Assertion Decryption Certificate** list. This is the certificate that BIG-IP uploads to Microsoft Entra ID for encrypting the issued SAML assertions.

    ![Screenshot for Service Provider security settings](media/f5-big-ip-easy-button-oracle-jde/service-provider-security-settings.png)

### Configure Microsoft Entra ID settings

The Microsoft Entra ID configuration defines all properties that you would normally use to manually configure a new BIG-IP SAML application within your Microsoft Entra tenant. Easy Button provides a set of pre-defined application templates for Oracle PeopleSoft, Oracle E-business Suite, Oracle JD Edwards, SAP ERP and generic SHA template for any other apps.

For this scenario, in the **Azure Configuration** page, select **JD Edwards Protected by F5 BIG-IP** &gt; **Add**.

#### Configure Azure application settings

1. Enter **Display Name** of app that the BIG-IP creates in your Microsoft Entra tenant, and the icon that the users see on MyApps portal
2. In the **Sign On URL (optional)** enter the public FQDN of the JDE application being secured.

    ![Screenshot for Azure configuration add display info](media/f5-big-ip-easy-button-oracle-jde/azure-configuration-add-display-info.png)
3. Select the refresh icon next to the **Signing Key** and **Signing Certificate** to locate the certificate you imported earlier
4. Enter the certificate’s password in **Signing Key Passphrase**
5. Enable **Signing Option** (optional). This ensures that BIG-IP only accepts tokens and claims that are signed by Microsoft Entra ID

    ![Screenshot for Azure configuration - Add signing certificates info](media/f5-big-ip-easy-button-oracle-jde/azure-configuration-sign-certificates.png)
6. **User and User Groups** are dynamically queried from your Microsoft Entra tenant and used to authorize access to the application. Add a user or group that you can use later for testing, otherwise all access is denied

    ![Screenshot for Azure configuration - Add users and groups](media/f5-big-ip-easy-button-oracle-jde/azure-configuration-add-user-groups.png)

#### Configure user attributes and claims

When a user successfully authenticates, Microsoft Entra ID issues a SAML token with a default set of claims and attributes uniquely identifying the user. The **User Attributes & Claims** tab shows the default claims to issue for the new application. It also lets you configure more claims.

![Screenshot for user attributes and claims](media/f5-big-ip-easy-button-oracle-jde/user-attributes-claims.png)

You can include additional Microsoft Entra attributes if necessary, but the Oracle JDE scenario only requires the default attributes.

#### Configure additional user attributes

The **Additional User Attributes** tab can support a variety of distributed systems requiring attributes stored in other directories for session augmentation. Attributes fetched from an LDAP source can then be injected as additional SSO headers to further control access based on roles, Partner IDs, and so on.

![Screenshot for additional user attributes](media/f5-big-ip-easy-button-oracle-jde/additional-user-attributes.png)

Note

This feature has no correlation to Microsoft Entra ID but is another source of attributes.

#### Configure a Conditional Access policy

Conditional Access policies are enforced post Microsoft Entra pre-authentication, to control access based on device, application, location, and risk signals.

The **Available Policies** view, by default, will list all Conditional Access policies that don't include user-based actions.

The **Selected Policies** view, by default, displays all policies targeting All resources. These policies can't be deselected or moved to the Available Policies list as they're enforced at a tenant level.

To select a policy to be applied to the application being published:

1. Select the desired policy in the **Available Policies** list
2. Select the right arrow and move it to the **Selected Policies** list

    The selected policies should either have an **Include** or **Exclude** option checked. If both options are checked, the policy isn't enforced.

    ![Screenshot for Conditional Access policies](media/f5-big-ip-easy-button-oracle-jde/conditional-access-policy.png)

Note

The policy list is enumerated only once when first switching to this tab. A refresh button is available to manually force the wizard to query your tenant, but this button is displayed only when the application has been deployed.

### Configure virtual server properties

A virtual server is a BIG-IP data plane object represented by a virtual IP address listening for client requests to the application. Any received traffic is processed and evaluated against the APM profile associated with the virtual server, before being directed according to the policy results and settings.

1. Enter **Destination Address**. This is any available IPv4/IPv6 address that the BIG-IP can use to receive client traffic. A corresponding record should also exist in DNS, enabling clients to resolve the external URL of your BIG-IP published application to this IP, instead of the application itself. Using a test PC's localhost DNS is fine for testing.
2. Enter **Service Port** as *443* for HTTPS
3. Check **Enable Redirect Port** and then enter **Redirect Port**. It redirects incoming HTTP client traffic to HTTPS
4. The Client SSL Profile enables the virtual server for HTTPS, so that client connections are encrypted over TLS. Select the **Client SSL Profile** you created as part of the prerequisites or leave the default whilst testing

    ![Screenshot for Virtual server](media/f5-big-ip-easy-button-oracle-jde/virtual-server.png)

### Configure pool properties

The **Application Pool tab** details the services behind a BIG-IP, represented as a pool containing one or more application servers.

1. Choose from **Select a Pool**. Create a new pool or select an existing one
2. Choose the **Load Balancing Method** as *Round Robin*
3. For **Pool Servers** select an existing node or specify an IP and port for the servers hosting the Oracle JDE application.

    ![Screenshot for Application pool](media/f5-big-ip-easy-button-oracle-jde/application-pool.png)

#### Configure single sign-on and HTTP headers

The **Easy Button wizard** supports Kerberos, OAuth Bearer, and HTTP authorization headers for SSO to published applications. As the Oracle JDE application expects headers, enable **HTTP Headers** and enter the following properties.

- **Header Operation:** replace
- **Header Name:** JDE\_SSO\_UID
- **Header Value:** %{session.sso.token.last.username}

![Screenshot for SSO and HTTP headers](media/f5-big-ip-easy-button-oracle-jde/sso-and-http-headers.png)

Note

APM session variables defined within curly brackets are CASE sensitive. For example, if you enter OrclGUID when the Microsoft Entra attribute name is being defined as orclguid, it causes an attribute mapping failure

### Configure session management settings

The BIG-IPs session management settings are used to define the conditions under which user sessions are terminated or allowed to continue, limits for users and IP addresses, and corresponding user info. Refer to [F5 BIG-IP APM session management settings](https://support.f5.com/csp/article/K18390492) for details on these settings.

What isn’t covered here however is Single Log-Out (SLO) functionality, which ensures all sessions between the IdP, the BIG-IP, and the user agent are terminated as users sign off. When the Easy Button instantiates a SAML application in your Microsoft Entra tenant, it also populates the Logout Url with the APM’s SLO endpoint. That way IdP initiated sign-outs from the Microsoft Entra My Apps portal also terminate the session between the BIG-IP and a client.

Along with this the SAML federation metadata for the published application is also imported from your tenant, providing the APM with the SAML logout endpoint for Microsoft Entra ID. This ensures SP initiated sign outs terminate the session between a client and Microsoft Entra ID. But for this to be truly effective, the APM needs to know exactly when a user signs-out of the application.

If the BIG-IP webtop portal is used to access published applications then a sign-out from there would be processed by the APM to also call the Microsoft Entra sign-out endpoint. But consider a scenario where the BIG-IP webtop portal isn’t used, then the user has no way of instructing the APM to sign out. Even if the user signs-out of the application itself, the BIG-IP is technically oblivious to this. So for this reason, SP initiated sign-out needs careful consideration to ensure sessions are securely terminated when no longer required. One way of achieving this would be to add an SLO function to your applications sign out button, so that it can redirect your client to either the Microsoft Entra SAML or BIG-IP sign-out endpoint. The URL for SAML sign-out endpoint for your tenant can be found in **App Registrations &gt; Endpoints**.

If making a change to the app is a no go, then consider having the BIG-IP listen for the application's sign-out call, and upon detecting the request have it trigger SLO. Refer to our [Oracle PeopleSoft SLO guidance](../enterprise-apps/f5-big-ip-oracle-peoplesoft-easy-button#peoplesoft-single-logout) for using BIG-IP irules to achieve this. More details on using BIG-IP iRules to achieve this is available in the F5 knowledge article [Configuring automatic session termination (logout) based on a URI-referenced file name](https://support.f5.com/csp/article/K42052145) and [Overview of the Logout URI Include option](https://support.f5.com/csp/article/K12056).

## Summary

The Review and Deploy step provides a breakdown of your configurations. Select **Deploy** to commit all settings and verify that the application now exists in your tenants list of Enterprise applications.