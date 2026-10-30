---
layout: Conceptual
title: Configure Microsoft Entra multifactor authentication and SSO for Oracle PeopleSoft applications using Datawiza Access Proxy - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/datawiza-sso-oracle-peoplesoft
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Enable Microsoft Entra multifactor authentication and SSO for Oracle PeopleSoft application using Datawiza Access Proxy
ms.topic: how-to
ms.date: 2024-01-30T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
ms.custom: not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: 3ba9c4ed-af7f-a4ae-e2f1-0cb7356dfd04
document_version_independent_id: 216f53b8-b258-322a-ffa0-df0bd60f868c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/datawiza-sso-oracle-peoplesoft.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/datawiza-sso-oracle-peoplesoft
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/datawiza-sso-oracle-peoplesoft.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 762652f4-04c0-8a73-6869-0bfc1d58cc79
---

# Configure Microsoft Entra multifactor authentication and SSO for Oracle PeopleSoft applications using Datawiza Access Proxy - Microsoft Entra ID | Microsoft Learn

In this tutorial, learn how to enable Microsoft Entra single sign-on (SSO) and Microsoft Entra multifactor authentication for an Oracle PeopleSoft application using Datawiza Access Proxy (DAP).

Learn more: [Datawiza Access Proxy](https://www.datawiza.com/)

Benefits of integrating applications with Microsoft Entra ID using DAP:

- [Embrace proactive security with Zero Trust](https://www.microsoft.com/security/business/zero-trust) - a security model that adapts to modern environments and embraces hybrid workplace, while it protects people, devices, apps, and data
- [Microsoft Entra single sign-on](https://azure.microsoft.com/solutions/active-directory-sso/#overview) - secure and seamless access for users and apps, from any location, using a device
- [How it works: Microsoft Entra multifactor authentication](../authentication/concept-mfa-howitworks) - users are prompted during sign-in for forms of identification, such as a code on their cellphone or a fingerprint scan
- [What is Conditional Access?](../conditional-access/overview) - policies are if-then statements, if a user wants to access a resource, then they must complete an action
- [Easy authentication and authorization in Microsoft Entra ID with no-code Datawiza](https://www.microsoft.com/security/blog/2022/05/17/easy-authentication-and-authorization-in-azure-active-directory-with-no-code-datawiza/) - use web applications such as: Oracle JDE, Oracle E-Business Suite, Oracle Siebel, and home-grown apps
- Use the [Datawiza Cloud Management Console (DCMC)](https://console.datawiza.com) - manage access to applications in public clouds and on-premises

## Scenario description

This scenario focuses on Oracle PeopleSoft application integration using HTTP authorization headers to manage access to protected content.

In legacy applications, due to the absence of modern protocol support, a direct integration with Microsoft Entra SSO is difficult. Datawiza Access Proxy (DAP) bridges the gap between the legacy application and the modern ID control plane, through protocol transitioning. DAP lowers integration overhead, saves engineering time, and improves application security.

## Scenario architecture

The scenario solution has the following components:

- **Microsoft Entra ID** - identity and access management service that helps users sign in and access external and internal resources
- **Datawiza Access Proxy (DAP)** - container-based reverse-proxy that implements OpenID Connect (OIDC), OAuth, or Security Assertion Markup Language (SAML) for user sign-in flow. It passes identity transparently to applications through HTTP headers.
- **Datawiza Cloud Management Console (DCMC)** - administrators manage DAP with UI and RESTful APIs to configure DAP and access control policies
- **Oracle PeopleSoft application** - legacy application to be protected by Microsoft Entra ID and DAP

Learn more: [Datawiza and Microsoft Entra authentication architecture](datawiza-configure-sha#datawiza-with-azure-ad-authentication-architecture)

## Prerequisites

Ensure the following prerequisites are met.

- An Azure subscription
    - If you don't have one, you can get an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- A Microsoft Entra tenant linked to the Azure subscription
    - See, [Quickstart: Create a new tenant in Microsoft Entra ID](../../fundamentals/create-new-tenant)
- Docker and Docker Compose
    - Go to docs.docker.com to [Get Docker](https://docs.docker.com/get-docker) and [Install Docker Compose](https://docs.docker.com/compose/install)
- User identities synchronized from an on-premises directory to Microsoft Entra ID, or created in Microsoft Entra ID and flowed back to an on-premises directory
    - See, [Microsoft Entra Connect Sync: Understand and customize synchronization](../hybrid/connect/how-to-connect-sync-whatis)
- An account with Microsoft Entra ID and the Application Administrator role
    - See, [Microsoft Entra built-in roles, all roles](../role-based-access-control/permissions-reference#application-administrator)
- An Oracle PeopleSoft environment
- (Optional) An SSL web certificate to publish services over HTTPS. You can use default Datawiza self-signed certs for testing.

## Getting started with DAP

To integrate Oracle PeopleSoft with Microsoft Entra ID:

1. Sign in to [Datawiza Cloud Management Console (DCMC)](https://console.datawiza.com/).
2. The Welcome page appears.
3. Select the orange **Getting started** button.

    ![Screenshot of the Getting Started button.](media/datawiza-sso-oracle-peoplesoft/getting-started-button.png)
4. In the **Name** and **Description** fields, enter information.

    ![Screenshot of the Name field under Deployment Name.](media/datawiza-sso-oracle-peoplesoft/deployment-details.png)
5. Select **Next**.
6. The Add Application dialog appears.
7. For **Platform**, select **Web**.
8. For **App Name**, enter a unique application name.
9. For **Public Domain**, for example use `https://ps-external.example.com`. For testing, you can use localhost DNS. If you aren't deploying DAP behind a load balancer, use the Public Domain port.
10. For **Listen Port**, select the port that DAP listens on.
11. For **Upstream Servers**, select the Oracle PeopleSoft implementation URL and port to be protected.
12. Select **Next**.
13. On the **Configure IdP** dialog, enter information.

Note

DCMC has one-click integration to help complete Microsoft Entra configuration. DCMC calls the Microsoft Graph API to create an application registration on your behalf in your Microsoft Entra tenant. Learn more at docs.datawiza.com in [One Click Integration with Microsoft Entra ID](https://docs.datawiza.com/tutorial/web-app-azure-one-click.html#preview)

1. Select **Create**.

![Screenshot of entries under Configure IDP.](media/datawiza-sso-oracle-peoplesoft/configure-idp.png)

1. The DAP deployment page appears.
2. Make a note of the deployment Docker Compose file. The file includes the DAP image, the Provisioning Key and Provision Secret, which pulls the latest configuration and policies from DCMC.

## SSO and HTTP headers

DAP gets user attributes from the identity provider (IdP) and passes them to the upstream application with a header or cookie.

The Oracle PeopleSoft application needs to recognize the user. Using a name, the application instructs DAP to pass the values from the IdP to the application through the HTTP header.

1. In Oracle PeopleSoft, from the left navigation, select **Applications**.
2. Select the **Attribute Pass** subtab.
3. For **Field**, select **email**.
4. For **Expected**, select **PS\_SSO\_UID**.
5. For **Type**, select **Header**.

    ![Screenshot of the Attribute Pass feature with Field, Expected and Type entries.](media/datawiza-sso-oracle-peoplesoft/attribute-pass.png)

    Note

    This configuration uses Microsoft Entra user principal name as the sign-in username for Oracle PeopleSoft. To use another user identity, go to the **Mappings** tab.

    ![Screenshot of user principal name.](media/datawiza-sso-oracle-peoplesoft/user-principal-name.png)

## SSL Configuration

1. Select the **Advanced tab**.

    ![Screenshot of the Advanced tab under Application Detail.](media/datawiza-sso-oracle-peoplesoft/advanced-configuration.png)
2. Select **Enable SSL**.
3. From the **Cert Type** dropdown, select a type.

    ![Screenshot of the Cert Type dropdown with available options, Self-signed and Upload.](media/datawiza-sso-oracle-peoplesoft/cert-type-new.png)
4. For testing the configuration, there's a self-signed certificate.

    ![Screenshot of the Cert Type option with Self Signed selected.](media/datawiza-sso-oracle-peoplesoft/self-signed-cert.png)

    Note

    You can upload a certificate from a file.

    ![Screenshot of the File Based entry for Select Option under Advanced Settings.](media/datawiza-sso-oracle-peoplesoft/cert-upload-new.png)
5. Select **Save**.

## Enable Microsoft Entra multifactor authentication

To provide more security for sign-ins, you can enforce Microsoft Entra multifactor authentication.

Learn more: [Tutorial: Secure user sign-in events with Microsoft Entra multifactor authentication](../authentication/tutorial-enable-azure-mfa)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Overview** &gt; **Properties** tab.
3. Under **Security defaults**, select **Manage security defaults**.
4. On the **Security defaults** pane, toggle the dropdown menu to select **Enabled**.
5. Select **Save**.

## Enable SSO in the Oracle PeopleSoft console

To enable SSO in the Oracle PeopleSoft environment:

1. Sign in to the PeopleSoft Console `http://{your-peoplesoft-fqdn}:8000/psp/ps/?cmd=start` using Admin credentials, for example, PS/PS.
2. Add a default public access user to PeopleSoft.
3. From the main menu, navigate to **PeopleTools &gt; Security &gt; User Profiles &gt; User Profiles &gt; Add a New Value**.
4. Select **Add a new value**.
5. Create user **PSPUBUSER**.
6. Enter the password.

    ![Screenshot of the PS PUBUSER User ID and change-password option.](media/datawiza-sso-oracle-peoplesoft/create-user.png)
7. Select the **ID** tab.
8. For **ID Type**, select **None**.

    ![Screenshot of the None option for ID Type on the ID tab.](media/datawiza-sso-oracle-peoplesoft/id-type.png)
9. Navigate to **PeopleTools &gt; Web Profile &gt; Web Profile Configuration &gt; Search &gt; PROD &gt; Security**.
10. Under **Public Users**, select the **Allow Public Access** box.
11. For **User ID**, enter **PSPUBUSER**.
12. Enter the password.

    ![Screenshot of Allow Public Access, User ID, and Password options.](media/datawiza-sso-oracle-peoplesoft/web-profile-config.png)
13. Select **Save**.
14. To enable SSO, navigate to **PeopleTools &gt; Security &gt; Security Objects &gt; Signon PeopleCode**.
15. Select the **Sign on PeopleCode** page.
16. Enable **OAMSSO\_AUTHENTICATION**.
17. Select **Save**.
18. To configure PeopleCode using the PeopleTools application designer, navigate to **File &gt; Open &gt; Definition: Record &gt; Name: `FUNCLIB_LDAP`**.
19. Open **FUNCLIB\_LDAP**.

    ![Screenshot of the Open Definition dialog.](media/datawiza-sso-oracle-peoplesoft/selection-criteria.png)
20. Select the record.
21. Select **LDAPAUTH &gt; View PeopleCode**.
22. Search for the `getWWWAuthConfig()` function `Change &defaultUserId = ""; to &defaultUserId = PSPUBUSER`.
23. Confirm the user Header is `PS_SSO_UID` for `OAMSSO_AUTHENTICATION` function.
24. Save the record definition.

    ![Screenshot of the record definition.](media/datawiza-sso-oracle-peoplesoft/record-definition.png)

## Test an Oracle PeopleSoft application

To test an Oracle PeopleSoft application, validate application headers, policy, and overall testing. If needed, use header and policy simulation to validate header fields and policy execution.

To confirm Oracle PeopleSoft application access occurs correctly, a prompt appears to use a Microsoft Entra account for sign-in. Credentials are checked and the Oracle PeopleSoft appears.