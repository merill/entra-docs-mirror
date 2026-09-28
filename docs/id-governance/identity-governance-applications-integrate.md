---
layout: Conceptual
title: Integrate your applications for identity governance and establishing a baseline of reviewed access - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/identity-governance-applications-integrate
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: Microsoft Entra ID Governance allows you to balance your organization's need for security and employee productivity with the right processes and visibility.  You can integrate your existing business critical third party on-premises and cloud-based applications with Microsoft Entra ID for identity governance scenarios.
editor: markwahl-msft
ms.topic: how-to
ms.date: 2024-11-25T00:00:00.0000000Z
ms.reviewer: markwahl-msft
locale: en-us
document_id: 517abae2-e8ef-3239-2ecc-43a3651740c4
document_version_independent_id: df95debd-61fe-c33d-87d0-6118c5f228e0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/identity-governance-applications-integrate.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/identity-governance-applications-integrate
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/identity-governance-applications-integrate.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: c276ad96-7241-f3c7-a22e-4f849444b093
---

# Integrate your applications for identity governance and establishing a baseline of reviewed access - Microsoft Entra ID Governance | Microsoft Learn

Once you've [established the policies](identity-governance-applications-define) for who should have access to an application, you can [connect your application to Microsoft Entra ID](../identity/enterprise-apps/what-is-application-management) and then [deploy the policies](identity-governance-applications-deploy) for governing access to them.

Microsoft Entra ID Governance can be integrated with many applications, including SAP R/3, SAP S/4HANA, and those using [standards](../architecture/auth-sync-overview) such as OpenID Connect, SAML, SCIM, SQL, LDAP, SOAP, and REST. Through these standards, you can use Microsoft Entra ID with many popular SaaS applications and on-premises applications, including applications that your organization developed. This deployment plan covers how to connect your application to Microsoft Entra ID and enable identity governance features to be used for that application.

In order for Microsoft Entra ID Governance to be used for an application, the application must first be integrated with Microsoft Entra ID and represented in your directory. An application being integrated with Microsoft Entra ID means one of two requirements must be met:

- The application relies upon Microsoft Entra ID for federated SSO, and Microsoft Entra ID controls authentication token issuance. If Microsoft Entra ID is the only identity provider for the application, then only users assigned to one of the application's roles in Microsoft Entra ID can sign into the application. Those users that lose their application role assignment can no longer get a new token to sign in to the application.
- The application relies upon user or group lists that are provided to the application by Microsoft Entra ID. This fulfillment could be done through a provisioning protocol such as SCIM, by the application querying Microsoft Entra ID via Microsoft Graph, or the application using AD Kerberos to obtain a user's group memberships.

If neither of those criteria are met for an application, for example when the application doesn't rely upon Microsoft Entra ID, then identity governance can still be used. However, there may be some limitations using identity governance without meeting the criteria. For instance, users that aren't in your Microsoft Entra ID, or aren't assigned to the application roles in Microsoft Entra ID, won't be included in access reviews of the application, until you assign them to the application roles. For more information, see [Preparing for an access review of users' access to an application](access-reviews-application-preparation).

## Integrate the application with Microsoft Entra ID to ensure only authorized users can access the application

The integrating of an application process begins when you configure that application to rely upon Microsoft Entra ID for user authentication, with a federated single sign-on (SSO) protocol connection, and then add provisioning. The most commonly used protocols for SSO are [SAML and OpenID Connect](../identity-platform/v2-protocols). You can read more about the tools and process to [discover and migrate application authentication to Microsoft Entra ID](../identity/enterprise-apps/migrate-adfs-apps-phases-overview).

Next, if the application implements a provisioning protocol, then you should configure Microsoft Entra ID to provision users to the application, so that Microsoft Entra ID can signal to the application when a user has been granted access or a user's access has been removed. These provisioning signals permit the application to make automatic corrections, such as to reassign content created by an employee who has left to their manager.

1. Check if your application is on the [list of enterprise applications](../identity/enterprise-apps/view-applications-portal) or [list of app registrations](../identity-platform/app-objects-and-service-principals). If the application is already present in your tenant, then skip to step 5 in this section.
2. If your application is a SaaS application that isn't already registered in your tenant, check for available applications in the [application gallery](../identity/enterprise-apps/overview-application-gallery) that can be integrated for federated SSO. If it's in the gallery, then use the tutorials to integrate the application with Microsoft Entra ID.

    1. Follow the [tutorial](../identity/saas-apps/tutorial-list) to configure the application for federated SSO with Microsoft Entra ID.
    2. if the application supports provisioning, [configure the application for provisioning](../identity/app-provisioning/configure-automatic-user-provisioning-portal).
    3. When complete, skip to the next section in this article. If the SaaS application isn't in the gallery, then [ask the SaaS vendor to onboard](../identity/enterprise-apps/v2-howto-app-gallery-listing).
3. If this is a private or custom application, you can also select a single sign-on integration that's most appropriate, based on the location and capabilities of the application.

    - If this application is on SAP Business Technology Platform (BTP), then configure Microsoft Entra integration with SAP Cloud Identity Services. For more information, see [Microsoft Entra SSO integration with SAP BTP](../identity/saas-apps/sap-hana-cloud-platform-tutorial) and [Managing access to SAP BTP](https://community.sap.com/t5/technology-blogs-by-members/identity-and-access-management-with-microsoft-entra-part-i-managing-access/ba-p/13873276).
    - If this application is in the public cloud, and it supports single sign-on, then configure single sign-on directly from Microsoft Entra ID to the application.

        | Application supports | Next steps |
        | --- | --- |
        | OpenID Connect | [Add an OpenID Connect OAuth application](../identity/saas-apps/openidoauth-tutorial) |
        | SAML 2.0 | Register the application and configure the application with [the SAML endpoints and certificate of Microsoft Entra ID](../identity-platform/saml-protocol-reference) |
        | SAML 1.1 | [Add a SAML-based application](../identity/saas-apps/saml-tutorial) |
    - If this is a SAP application that uses the SAP GUI, then integrate Microsoft Entra for single-sign on using the [integration with SAP Secure Login Service](https://community.sap.com/t5/technology-blogs-by-members/sap-gui-mfa-with-microsoft-entra-part-i-integration-with-sap-secure-login/ba-p/13605383) or [integration with Microsoft Entra Private Access](https://community.sap.com/t5/technology-blogs-by-members/sap-gui-mfa-with-microsoft-entra-part-ii-integration-with-microsoft-entra/ba-p/13691141).
    - Otherwise, if this is an on-premises or IaaS hosted application that supports single sign-on, then configure single sign-on from Microsoft Entra ID to the application through the application proxy.

        | Application supports | Next steps |
        | --- | --- |
        | SAML 2.0 | Deploy the [application proxy](/en-us/entra/identity/app-proxy) and configure an application for [SAML SSO](../identity/app-proxy/conceptual-sso-apps) |
        | Integrated Windows Auth (IWA) | Deploy the [application proxy](/en-us/entra/identity/app-proxy), configure an application for [Integrated Windows authentication SSO](../identity/app-proxy/how-to-configure-sso-with-kcd), and set firewall rules to prevent access to the application's endpoints except via the proxy. |
        | header-based authentication | Deploy the [application proxy](/en-us/entra/identity/app-proxy) and configure an application for [header-based SSO](../identity/app-proxy/application-proxy-configure-single-sign-on-with-headers) |
4. If your application is on SAP BTP, then you can use Microsoft Entra groups to maintain the membership of each role. For more information on assigning the groups to the BTP role collections, see [Managing access to SAP BTP](https://community.sap.com/t5/technology-blogs-by-members/identity-and-access-management-with-microsoft-entra-part-i-managing-access/ba-p/13873276).
5. If your application has multiple roles, each user has only one role in the application, and the application relies upon Microsoft Entra ID to send a user's single application-specific role as a claim of a user signing into the application, then configure those app roles in Microsoft Entra ID on your application, and then assign each user to the application role. You can use the [app roles UI](../identity-platform/howto-add-app-roles-in-apps#app-roles-ui) to add those roles to the application manifest. If you're using the Microsoft Authentication Libraries, there is a [code sample](../identity-platform/sample-v2-code) for how to use app roles inside your application for access control. If a user could have multiple roles simultaneously, then you may wish to implement the application to check security groups, either in the token claims or available via Microsoft Graph, instead of using app roles from the app manifest for access control.
6. If the application supports provisioning, then [configure provisioning](../identity/app-provisioning/configure-automatic-user-provisioning-portal) of assigned users and groups from Microsoft Entra ID to that application. If this is a private or custom application, you can also select the integration that's most appropriate, based on the location and capabilities of the application.

    - If this application relies upon SAP Cloud Identity Services, then configure provisioning of users via SCIM into SAP Cloud Identity Services.

        | Application supports | Next steps |
        | --- | --- |
        | SAP Cloud Identity Services | [Configure Microsoft Entra ID to provision users into SAP Cloud Identity Services](../identity/saas-apps/sap-cloud-platform-identity-authentication-provisioning-tutorial) |
    - If this application is in the public cloud and supports SCIM, then configure provisioning of users via SCIM.

        | Application supports | Next steps |
        | --- | --- |
        | SCIM | Configure an application with SCIM [for user provisioning](../identity/app-provisioning/use-scim-to-provision-users-and-groups) |
    - If this application uses AD, then configure group writeback, and either update the application to use the Microsoft Entra ID-created groups, or nest the Microsoft Entra ID-created groups into the applications' existing AD security groups.

        | Application supports | Next steps |
        | --- | --- |
        | Kerberos | Configure Microsoft Entra Cloud Sync [group writeback to AD](../identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory), create groups in Microsoft Entra ID, and [write those groups to AD](entitlement-management-group-writeback) |
    - Otherwise, if this is an on-premises or IaaS hosted application, and isn't integrated with AD, then configure provisioning to that application, either via SCIM or to the underlying database or directory of the application.

        | Application supports | Next steps |
        | --- | --- |
        | SCIM | configure an application with the [provisioning agent for on-premises SCIM-based apps](../identity/app-provisioning/on-premises-scim-provisioning) |
        | local user accounts, stored in a SQL database | configure an application with the [provisioning agent for on-premises SQL-based applications](../identity/app-provisioning/on-premises-sql-connector-configure) |
        | local user accounts, stored in an LDAP directory | configure an application with the [provisioning agent for on-premises LDAP-based applications](../identity/app-provisioning/on-premises-ldap-connector-configure) |
        | local user accounts, managed through a SOAP or REST API | configure an application with the [provisioning agent with the web services connector](../identity/app-provisioning/on-premises-web-services-connector) |
        | local user accounts, managed through a MIM connector | configure an application with the [provisioning agent with a custom connector](../identity/app-provisioning/on-premises-custom-connector) |
        | SAP ECC with NetWeaver AS ABAP 7.0 or later | configure an application with the [provisioning agent with a SAP ECC configured web services connector](../identity/app-provisioning/on-premises-sap-connector-configure) |
7. If your application uses Microsoft Graph to query groups from Microsoft Entra ID, then [consent](../identity-platform/application-consent-experience) to the applications to have the appropriate permissions to read from your tenant.
8. Set that access to **the application is only permitted for users assigned to the application**. This setting prevents users from inadvertently seeing the application in MyApps, and attempting to sign into the application, prior to Conditional Access policies being enabled.

## Perform an initial access review

If this is a new application your organization hasn't used before, and therefore no one has pre-existing access, or if you've already been performing access reviews for this application, then skip to the [next section](identity-governance-applications-deploy).

However, if the application was already in your environment, users may have gained access in the past through manual or out-of-band processes. You should review those users to confirm their access is still necessary and appropriate. We recommend performing an access review of the users who already have access to the application, before enabling policies for more users to be able to request access. This review sets a baseline where all users are reviewed at least once to ensure they're authorized for continued access.

1. Follow the steps in [Preparing for an access review of users' access to an application](access-reviews-application-preparation).
2. If the application wasn't using Microsoft Entra ID or AD, but does support a provisioning protocol or had an underlying SQL or LDAP database, bring in any [existing users and create application role assignments](identity-governance-applications-existing-users) for them.
3. If the application wasn't using Microsoft Entra ID or AD, and doesn't support a provisioning protocol, then [obtain a list of users from the application and create application role assignments for each of them](identity-governance-applications-not-provisioned-users).
4. If the application was using AD security groups, then you need to review the membership of those security groups.
5. If the application had its own directory or database and wasn't integrated for provisioning, then once the review is complete, you may need to manually update the application's internal database or directory to remove those users who were denied.
6. If the application was using AD security groups, and those groups were created in AD, then once the review is complete, you need to manually update the AD groups to remove memberships of those users who were denied. Subsequently, to have denied access rights removed automatically, you can either update the application to use an AD group that was created in Microsoft Entra ID and [written back to Microsoft Entra ID](../identity/hybrid/cloud-sync/how-to-configure-entra-to-active-directory), or move the membership from the AD group to the Microsoft Entra group, and [nest the written back group as the only member of the AD group](../identity/hybrid/cloud-sync/govern-on-premises-groups).
7. Once the review has been completed and the application access updated, or if no users have access, then continue on to the next steps to deploy Conditional Access and entitlement management policies for the application.

Using custom data provided resources (preview), you can include access rights from applications in Microsoft Entra ID access reviews by uploading their access data directly prior to an access review. For more information, see [Include custom data provided resource in the catalog for catalog user Access Reviews (Preview)](custom-data-resource-access-reviews).

Now that you have a baseline that ensures existing access has been reviewed, then you can [deploy the organization's policies](identity-governance-applications-deploy) for ongoing access and any new access requests.