---
layout: Conceptual
title: Microsoft Entra ID Governance integrations - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/apps
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This page provides an overview of the Microsoft Entra ID Governance integrations available to automate provisioning and governance controls.
ms.topic: overview
ms.date: 2025-12-03T00:00:00.0000000Z
ms.reviewer: amycolannino
locale: en-us
document_id: 15a149be-d5f7-7577-4958-57397ec4dd6e
document_version_independent_id: 740014ab-3744-5a25-b167-5b665b57843f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/apps.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/apps.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac4b7417-d4c2-43d4-94bf-f22fa1416b34
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68876bab-7da4-4e70-b295-395b3a255a1f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 071a64b2-f191-b44f-48a6-7fc26c61bb75
---

# Microsoft Entra ID Governance integrations - Microsoft Entra ID Governance | Microsoft Learn

[Microsoft Entra ID Governance](identity-governance-applications-prepare) allows you to balance your organization's need for security and employee productivity with the right processes and visibility. This page provides an overview of the hundreds of Microsoft Entra ID Governance integrations available. These application integrations are used to automate [identity lifecycle management](scenarios/govern-the-employee-lifecycle) and implement governance controls across your organization. Through these rich integrations, you can automate providing users [access to applications](entitlement-management-overview), perform [periodic reviews](access-reviews-overview) of who has access to an application, and secure them with capabilities such as multifactor authentication.

## Featured integrations

Some of the popular integrations include the applications in the following table. For more integrations, see Microsoft Entra ID Governance.

| Category | Application |
| --- | --- |
| HR | [SuccessFactors - User Provisioning](../identity/saas-apps/sap-successfactors-inbound-provisioning-tutorial) |
| HR | [Workday - User Provisioning](../identity/saas-apps/workday-inbound-cloud-only-tutorial) |
| HR | [API-driven connector from any HR source](../identity/app-provisioning/inbound-provisioning-api-concepts)[Rippling HCM to Microsoft Entra ID/Active Directory provisioning](../identity/saas-apps/rippling-hcm-microsoft-entra-id-integration-tutorial)[HiBob to Microsoft Entra ID/Active Directory provisioning](../identity/saas-apps/hibob-to-active-directory-user-provisioning-tutorial)[Oracle HCM API-driven connector](../identity/saas-apps/oracle-hcm-provisioning-tutorial)[Darwinbox to Microsoft Entra ID](../identity/saas-apps/darwinbox-entra-integration-tutorial)[SAP HCM to Microsoft Entra ID](../identity/saas-apps/sap-hcm-microsoft-entra-identity-provisioning) |
| HR | Student information systems via [School Data Sync](/en-us/schooldatasync/school-data-sync-overview) |
| [LDAP directory](../identity/app-provisioning/on-premises-ldap-connector-configure) | OpenLDAPMicrosoft Active Directory Lightweight Directory Services389 Directory ServerApache Directory ServerIBM Tivoli DSIsode DirectoryNetIQ eDirectoryNovell eDirectoryOpen DJOpen DSOracle (previously Sun ONE) Directory Server Enterprise EditionRadiantOne Virtual Directory Server (VDS) |
| [SQL database](../identity/app-provisioning/tutorial-ecma-sql-connector) | Microsoft SQL Server and Azure SQLIBM DB2 10.xIBM DB2 9.xOracle 10g and 11gOracle 12c and 18cMySQL 5.xMySQL 8.xPostgres |
| Cloud platform | [AWS IAM Identity Center](../identity/saas-apps/aws-single-sign-on-provisioning-tutorial) |
| Cloud platform | [Google Cloud Platform - User Provisioning](../identity/saas-apps/g-suite-provisioning-tutorial) |
| Business applications | Multiple. With Microsoft Entra integrations to [Pathlock](https://pathlock.com/applications/microsoft-entra-id-governance/) and to other partner products, customers can take advantage of additional risk and fine-grained separation-of-duties checks enforced in those products, with access packages in Microsoft Entra ID Governance. |
| Business applications | SAP applications integrated with [SAP Cloud Identity Services](../identity/saas-apps/sap-cloud-platform-identity-authentication-provisioning-tutorial), including SAP Ariba Applications, SAP Concur, SAP S/4HANA Cloud, SAP S/4HANA On-Premise, among others |
| Business applications | Applications on SAP BTP [using role collections](https://community.sap.com/t5/technology-blogs-by-members/identity-and-access-management-with-microsoft-entra-part-i-managing-access/ba-p/13873276) |
| CRM | [Salesforce - User Provisioning](../identity/saas-apps/salesforce-provisioning-tutorial) |
| ITSM | [ServiceNow](../identity/saas-apps/servicenow-provisioning-tutorial) |

## Microsoft Entra ID Governance application integrations

The following list provides key integrations between Microsoft Entra ID Governance and various applications, including both automated provisioning and SSO just-in-time provisioning integrations. For a full list of applications that Microsoft Entra ID integrates with specifically for SSO, see: [SaaS App configuration guides for Microsoft Entra ID](../identity/saas-apps/tutorial-list).

Microsoft Entra ID Governance can be integrated with many other applications, using standards such as OpenID Connect, SAML, SCIM, SQL, and LDAP. If you're using an application that isn't listed, and it's a SaaS, then [ask the SaaS vendor to onboard](../identity/enterprise-apps/v2-howto-app-gallery-listing). For integration with other applications, see [integrating applications with Microsoft Entra ID](identity-governance-applications-integrate).

| Application | Automated provisioning | Single Sign On (SSO) |
| --- | --- | --- |
| [10,000 ft Plans](../identity/saas-apps/10000ftplans-tutorial) |  | ● |
| [15five](../identity/saas-apps/15five-provisioning-tutorial) | ● | ● |
| [123FormBuilder](../identity/saas-apps/123formbuilder-tutorial) |  | ● |
| [389 directory server (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [4me](../identity/saas-apps/4me-provisioning-tutorial) | ● | ● |
| [8x8](../identity/saas-apps/8x8-provisioning-tutorial) | ● | ● |
| [A Cloud Guru](../identity/saas-apps/a-cloud-guru-tutorial) |  | ● |
| [ABBYY FlexiCapture Cloud](../identity/saas-apps/abbyy-flexicapture-cloud-tutorial) |  | ● |
| [Abintegro](../identity/saas-apps/abintegro-tutorial) |  | ● |
| [Academy Attendance](../identity/saas-apps/academy-attendance-tutorial) |  | ● |
| [Acadia](../identity/saas-apps/acadia-tutorial) |  | ● |
| [Accenture Academy](../identity/saas-apps/accenture-academy-tutorial) |  | ● |
| [Acoustic Connect](../identity/saas-apps/acoustic-connect-tutorial) |  | ● |
| [Acunetix 360](../identity/saas-apps/acunetix-360-provisioning-tutorial) | ● | ● |
| [Adaptive Shield](../identity/saas-apps/adaptive-shield-tutorial) |  | ● |
| [Adobe Captivate Prime](../identity/saas-apps/adobecaptivateprime-tutorial) |  | ● |
| [Adobe Creative Cloud](../identity/saas-apps/adobe-identity-management-tutorial) |  | ● |
| [Adobe Experience Manager](../identity/saas-apps/adobeexperiencemanager-tutorial) |  | ● |
| [Adobe Identity Management (OIDC)](../identity/saas-apps/adobe-identity-management-provisioning-oidc-tutorial) | ● | ● |
| [Adobe Identity Management (SAML)](../identity/saas-apps/adobe-identity-management-provisioning-saml-tutorial) | ● | ● |
| [Adobe Sign](../identity/saas-apps/adobe-echosign-tutorial) |  | ● |
| [Adoddle cSaas Platform](../identity/saas-apps/adoddle-csaas-platform-tutorial) |  | ● |
| [Agiloft Contract Management Suite](../identity/saas-apps/agiloft-tutorial) |  | ● |
| [Aha!](../identity/saas-apps/aha-tutorial) |  | ● |
| [Airbase](../identity/saas-apps/airbase-provisioning-tutorial) | ● | ● |
| [Airstack](../identity/saas-apps/airstack-provisioning-tutorial) | ● |  |
| [Airtable](../identity/saas-apps/airtable-provisioning-tutorial) | ● | ● |
| [Akamai Enterprise Application Access](../identity/saas-apps/akamai-enterprise-application-access-provisioning-tutorial) | ● | ● |
| [Alation Data Catalog](../identity/saas-apps/alation-data-catalog-tutorial) |  | ● |
| [Albert](../identity/saas-apps/albert-provisioning-tutorial) | ● |  |
| [Alchemer](../identity/saas-apps/alchemer-tutorial) |  | ● |
| [AlertMedia](../identity/saas-apps/alertmedia-provisioning-tutorial) | ● | ● |
| [AlexisHR](../identity/saas-apps/alexishr-provisioning-tutorial) | ● | ● |
| [Allbound SSO](../identity/saas-apps/allbound-sso-tutorial) |  | ● |
| [Allocadia](../identity/saas-apps/allocadia-tutorial) |  | ● |
| [Ally.io](../identity/saas-apps/ally-tutorial) |  | ● |
| [Alohi](../identity/saas-apps/alohi-provisioning-tutorial) | ● | ● |
| [Altamira HRM](../identity/saas-apps/altamira-hrm-tutorial) |  | ● |
| [Alvao](../identity/saas-apps/alvao-provisioning-tutorial) | ● |  |
| [Amazon Business](../identity/saas-apps/amazon-business-provisioning-tutorial) | ● | ● |
| [Amazon Managed Grafana](../identity/saas-apps/amazon-managed-grafana-tutorial) |  | ● |
| [Amazon Web Services (AWS) - Role Provisioning](../identity/saas-apps/amazon-web-service-tutorial) | ● | ● |
| [Amplitude](../identity/saas-apps/amplitude-tutorial) |  | ● |
| [ANAQUA](../identity/saas-apps/anaqua-tutorial) |  | ● |
| [Andromeda](../identity/saas-apps/andromedascm-tutorial) |  | ● |
| [Apache Directory Server (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [Apex Portal](../identity/saas-apps/apexportal-tutorial) |  | ● |
| [Appaegis Isolation Access Cloud](../identity/saas-apps/appaegis-isolation-access-cloud-provisioning-tutorial) | ● | ● |
| [AppBlade](../identity/saas-apps/appblade-tutorial) |  | ● |
| [AppDynamics](../identity/saas-apps/appdynamics-tutorial) |  | ● |
| [Appian](../identity/saas-apps/appian-tutorial) |  | ● |
| [Appinux](../identity/saas-apps/appinux-tutorial) |  | ● |
| [Applitools Eyes](../identity/saas-apps/applitools-eyes-tutorial) |  | ● |
| [AppNeta Performance Monitor](../identity/saas-apps/appneta-tutorial) |  | ● |
| [ARC Facilities](../identity/saas-apps/arc-facilities-tutorial) |  | ● |
| [Arc Publishing - SSO](../identity/saas-apps/arc-tutorial) |  | ● |
| [ArcGIS Enterprise](../identity/saas-apps/arcgisenterprise-tutorial) |  | ● |
| [Archie](../identity/saas-apps/archie-tutorial) |  | ● |
| [Ardoq](../identity/saas-apps/ardoq-provisioning-tutorial) | ● | ● |
| [ARES for Enterprise](../identity/saas-apps/ares-for-enterprise-tutorial) |  | ● |
| [Aruba User Experience Insight](../identity/saas-apps/aruba-user-experience-insight-tutorial) |  | ● |
| [Asana](../identity/saas-apps/asana-provisioning-tutorial) | ● | ● |
| [AskSpoke](../identity/saas-apps/askspoke-provisioning-tutorial) | ● | ● |
| [Asset Bank](../identity/saas-apps/assetbank-tutorial) |  | ● |
| [Asset Planner](../identity/saas-apps/asset-planner-tutorial) |  | ● |
| [AssetSonar](../identity/saas-apps/assetsonar-tutorial) |  | ● |
| [Astra Schedule](../identity/saas-apps/astra-schedule-tutorial) |  | ● |
| [Astro](../identity/saas-apps/astro-provisioning-tutorial) | ● | ● |
| [Atea](../identity/saas-apps/atea-provisioning-tutorial) | ● |  |
| [Atlassian Cloud](../identity/saas-apps/atlassian-cloud-provisioning-tutorial) | ● | ● |
| [Atmos](../identity/saas-apps/atmos-provisioning-tutorial) | ● |  |
| [Atomic Learning](../identity/saas-apps/atomiclearning-tutorial) |  | ● |
| [ATP SpotLight and ChronicX](../identity/saas-apps/atp-spotlight-and-chronicx-tutorial) |  | ● |
| [AuditBoard](../identity/saas-apps/auditboard-provisioning-tutorial) | ● |  |
| [Authomize](../identity/saas-apps/authomize-tutorial) |  | ● |
| [Autodesk SSO](../identity/saas-apps/autodesk-sso-provisioning-tutorial) | ● | ● |
| [AwardSpring](../identity/saas-apps/awardspring-tutorial) |  | ● |
| [AWS ClientVPN](../identity/saas-apps/aws-clientvpn-tutorial) |  | ● |
| [AWS IAM Identity Center](../identity/saas-apps/aws-single-sign-on-provisioning-tutorial) | ● | ● |
| [Axiad Cloud](../identity/saas-apps/axiad-cloud-provisioning-tutorial) | ● | ● |
| [Azure Databricks SCIM Connector](/en-us/azure/databricks/administration-guide/users-groups/scim/aad) | ● |  |
| [Balsamiq Wireframes](../identity/saas-apps/balsamiq-wireframes-tutorial) |  | ● |
| [BambooHR](../identity/saas-apps/bamboo-hr-tutorial) |  | ● |
| [Banyan Security Zero Trust Remote Access Platform](../identity/saas-apps/banyan-command-center-tutorial) |  | ● |
| [Bealink](../identity/saas-apps/bealink-tutorial) |  | ● |
| [Beekeeper Microsoft Entra Data Connector](../identity/saas-apps/beekeeper-azure-ad-data-connector-tutorial) |  | ● |
| [Benchling](../identity/saas-apps/benchling-tutorial) |  | ● |
| [BenQ IAM](../identity/saas-apps/benq-iam-provisioning-tutorial) | ● | ● |
| [Bentley - Automatic User Provisioning](../identity/saas-apps/bentley-automatic-user-provisioning-tutorial) | ● |  |
| [Better Stack](../identity/saas-apps/better-stack-provisioning-tutorial) | ● |  |
| [BeyondTrust Remote Support](../identity/saas-apps/bomgarremotesupport-tutorial) |  | ● |
| [BIC Cloud Design](../identity/saas-apps/bic-cloud-design-provisioning-tutorial) | ● | ● |
| [BigPanda](../identity/saas-apps/bigpanda-tutorial) |  | ● |
| [BIS](../identity/saas-apps/bis-provisioning-tutorial) | ● | ● |
| [BitaBIZ](../identity/saas-apps/bitabiz-provisioning-tutorial) | ● | ● |
| [Bitly](../identity/saas-apps/bitly-tutorial) |  | ● |
| [Bizagi Studio for Digital Process Automation](../identity/saas-apps/bizagi-studio-for-digital-process-automation-provisioning-tutorial) | ● | ● |
| [Blackboard Learn - Shibboleth](../identity/saas-apps/blackboard-learn-shibboleth-tutorial) |  | ● |
| [Blackboard Learn](../identity/saas-apps/blackboard-learn-tutorial) |  | ● |
| [BLDNG APP](../identity/saas-apps/bldng-app-provisioning-tutorial) | ● |  |
| [Blink](../identity/saas-apps/blink-provisioning-tutorial) | ● | ● |
| [Blinq](../identity/saas-apps/blinq-provisioning-tutorial) | ● |  |
| [Blockbax](../identity/saas-apps/blockbax-tutorial) |  | ● |
| [BlogIn](../identity/saas-apps/blogin-provisioning-tutorial) | ● | ● |
| [Blue Ocean Brain](../identity/saas-apps/blue-ocean-brain-tutorial) |  | ● |
| [Bonusly](../identity/saas-apps/bonusly-provisioning-tutorial) | ● | ● |
| [BorrowBox](../identity/saas-apps/borrowbox-tutorial) |  | ● |
| [Box](../identity/saas-apps/box-userprovisioning-tutorial) | ● | ● |
| [Boxcryptor](../identity/saas-apps/boxcryptor-provisioning-tutorial) | ● | ● |
| [Bpanda](../identity/saas-apps/bpanda-provisioning-tutorial) | ● |  |
| [BrainStorm Platform](../identity/saas-apps/brainstorm-platform-tutorial) |  | ● |
| [Brandfolder](../identity/saas-apps/brandfolder-tutorial) |  | ● |
| [Bright Pattern Omnichannel Contact Center](../identity/saas-apps/bright-pattern-omnichannel-contact-center-tutorial) |  | ● |
| [Brightidea](../identity/saas-apps/brightidea-tutorial) |  | ● |
| [Briq](../identity/saas-apps/briq-tutorial) |  | ● |
| [Britive](../identity/saas-apps/britive-provisioning-tutorial) | ● | ● |
| [Brivo Onair Identity Connector](../identity/saas-apps/brivo-onair-identity-connector-provisioning-tutorial) | ● |  |
| [Broadcom DX SaaS](../identity/saas-apps/broadcom-dx-saas-tutorial) |  | ● |
| [BrowserStack Single Sign-on](../identity/saas-apps/browserstack-single-sign-on-provisioning-tutorial) | ● | ● |
| [Bugsnag](../identity/saas-apps/bugsnag-tutorial) |  | ● |
| [BullseyeTDP](../identity/saas-apps/bullseyetdp-provisioning-tutorial) | ● | ● |
| [Burp Suite Enterprise Edition](../identity/saas-apps/burp-suite-enterprise-edition-tutorial) |  | ● |
| [Bustle B2B Transport Systems](../identity/saas-apps/bustle-b2b-transport-systems-provisioning-tutorial) | ● |  |
| [Bynder](../identity/saas-apps/bynder-tutorial) |  | ● |
| [C3M Cloud Control](../identity/saas-apps/c3m-cloud-control-tutorial) |  | ● |
| [Canva](../identity/saas-apps/canva-provisioning-tutorial) | ● | ● |
| [Canvas LMS](../identity/saas-apps/canvas-lms-tutorial) |  | ● |
| [Capriza Platform](../identity/saas-apps/capriza-tutorial) |  | ● |
| [Cato Networks Provisioning](../identity/saas-apps/cato-networks-provisioning-tutorial) | ● |  |
| [CBRE ServiceInsight](../identity/saas-apps/cbre-serviceinsight-tutorial) |  | ● |
| [CCH Tagetik](../identity/saas-apps/cch-tagetik-tutorial) |  | ● |
| [Cequence Application Security Platform](../identity/saas-apps/cequence-application-security-tutorial) |  | ● |
| [Cerby](../identity/saas-apps/cerby-provisioning-tutorial) | ● | ● |
| [Ceridian Dayforce HCM](../identity/saas-apps/ceridiandayforcehcm-tutorial) |  | ● |
| [Cerner Central](../identity/saas-apps/cernercentral-provisioning-tutorial) | ● | ● |
| [Certify](../identity/saas-apps/certify-tutorial) |  | ● |
| [Chaos](../identity/saas-apps/chaos-provisioning-tutorial) | ● |  |
| [Chatwork](../identity/saas-apps/chatwork-provisioning-tutorial) | ● | ● |
| [Check Point Infinity Portal](../identity/saas-apps/checkpoint-infinity-portal-tutorial) |  | ● |
| [CheckProof](../identity/saas-apps/checkproof-provisioning-tutorial) | ● | ● |
| [Cheetah For Benelux](../identity/saas-apps/cheetah-for-benelux-tutorial) |  | ● |
| [Chengliye Smart SMS Platform](../identity/saas-apps/chengliye-smart-sms-platform-tutorial) |  | ● |
| [ChronicX®](../identity/saas-apps/chronicx-tutorial) |  | ● |
| [Chronus SAML](../identity/saas-apps/chronus-saml-tutorial) |  | ● |
| [Cinode](../identity/saas-apps/cinode-provisioning-tutorial) | ● |  |
| [Cisco Cloud](../identity/saas-apps/ciscocloud-tutorial) |  | ● |
| [Cisco Expressway](../identity/saas-apps/cisco-expressway-tutorial) |  | ● |
| [Cisco Intersight](../identity/saas-apps/cisco-intersight-tutorial) |  | ● |
| [Cisco Secure Firewall - Secure Client](../identity/saas-apps/cisco-secure-firewall-secure-client) |  | ● |
| [Cisco Umbrella](../identity/saas-apps/cisco-umbrella-tutorial) |  | ● |
| [Cisco Unified Communications Manager](../identity/saas-apps/cisco-unified-communications-manager-tutorial) |  | ● |
| [Cisco Unity Connection](../identity/saas-apps/cisco-unity-connection-tutorial) |  | ● |
| [Cisco User Management for Secure Access](../identity/saas-apps/cisco-user-management-for-secure-access-provisioning-tutorial) | ● | ● |
| [Cisco Webex Meetings](../identity/saas-apps/cisco-webex-tutorial) |  | ● |
| [Cisco Webex](../identity/saas-apps/cisco-webex-provisioning-tutorial) | ● | ● |
| [Citrix ADC SAML Connector for Microsoft Entra ID](../identity/saas-apps/citrix-netscaler-tutorial) |  | ● |
| [ClarivateWOS](../identity/saas-apps/clarivatewos-tutorial) |  | ● |
| [Clarizen One](../identity/saas-apps/clarizen-one-provisioning-tutorial) | ● | ● |
| [Claromentis](../identity/saas-apps/claromentis-tutorial) |  | ● |
| [Cleanmail](../identity/saas-apps/alinto-protect-provisioning-tutorial) | ● |  |
| [Cleanmail Swiss](../identity/saas-apps/cleanmail-swiss-provisioning-tutorial) | ● |  |
| [Clebex](../identity/saas-apps/clebex-provisioning-tutorial) | ● | ● |
| [Cloud Service PICCO](../identity/saas-apps/cloud-service-picco-tutorial) |  | ● |
| [CMD+CTRL Base Camp](../identity/saas-apps/cmd-ctrl-base-camp-tutorial) |  | ● |
| [Coda](../identity/saas-apps/coda-provisioning-tutorial) | ● | ● |
| [Code42](../identity/saas-apps/code42-provisioning-tutorial) | ● | ● |
| [Cofense Recipient Sync](../identity/saas-apps/cofense-provision-tutorial) | ● |  |
| [Coggle](../identity/saas-apps/coggle-tutorial) |  | ● |
| [Cognidox](../identity/saas-apps/cognidox-tutorial) |  | ● |
| [Cognism](../identity/saas-apps/cognism-tutorial) |  | ● |
| [CoLab](../identity/saas-apps/colab-tutorial) |  | ● |
| [Collaborative Innovation](../identity/saas-apps/collaborativeinnovation-tutorial) |  | ● |
| [Collibra](../identity/saas-apps/collibra-tutorial) |  | ● |
| [Colloquial](../identity/saas-apps/colloquial-provisioning-tutorial) | ● | ● |
| [Comeet Recruiting Software](../identity/saas-apps/comeet-recruiting-software-provisioning-tutorial) | ● | ● |
| [Communifire](../identity/saas-apps/communifire-tutorial) |  | ● |
| [Community Spark](../identity/saas-apps/community-spark-tutorial) |  | ● |
| [Compliance Genie](../identity/saas-apps/compliance-genie-tutorial) |  | ● |
| [Condeco](../identity/saas-apps/condeco-tutorial) |  | ● |
| [Confirmit Horizons](../identity/saas-apps/confirmit-horizons-tutorial) |  | ● |
| [Connecter](../identity/saas-apps/connecter-provisioning-tutorial) | ● |  |
| [Contentful](../identity/saas-apps/contentful-provisioning-tutorial) | ● | ● |
| [Contentkalender](../identity/saas-apps/contentkalender-tutorial) |  | ● |
| [Contentsquare SSO](../identity/saas-apps/contentsquare-sso-tutorial) |  | ● |
| [Contentstack](../identity/saas-apps/contentstack-provisioning-tutorial) | ● | ● |
| [ContractS CLM](../identity/saas-apps/holmes-cloud-provisioning-tutorial) | ● |  |
| [Contrast Security](../identity/saas-apps/contrast-security-tutorial) |  | ● |
| [Convene](../identity/saas-apps/convene-tutorial) |  | ● |
| [Couchbase Capella - SSO](../identity/saas-apps/couchbase-capella-sso-tutorial) |  | ● |
| [Couchbase Server - SSO](../identity/saas-apps/couchbase-server-sso-tutorial) |  | ● |
| [Coupa Risk Assess](../identity/saas-apps/coupa-risk-assess-tutorial) |  | ● |
| [Coupa](../identity/saas-apps/coupa-tutorial) |  | ● |
| [courses.work](../identity/saas-apps/courseswork-tutorial) |  | ● |
| [Crayon](../identity/saas-apps/crayon-tutorial) |  | ● |
| [CultureHQ](../identity/saas-apps/culturehq-provisioning-tutorial) | ● | ● |
| [Curator](../identity/saas-apps/curator-tutorial) |  | ● |
| [Cybozu](../identity/saas-apps/cybozu-provisioning-tutorial) | ● | ● |
| [CybSafe](../identity/saas-apps/cybsafe-provisioning-tutorial) | ● |  |
| [Dagster Cloud](../identity/saas-apps/dagster-cloud-provisioning-tutorial) | ● | ● |
| [Databook](../identity/saas-apps/databook-tutorial) |  | ● |
| [DataCamp](../identity/saas-apps/datacamp-tutorial) |  | ● |
| [Datadog](../identity/saas-apps/datadog-provisioning-tutorial) | ● | ● |
| [Datava Enterprise Service Platform](../identity/saas-apps/datava-enterprise-service-platform-tutorial) |  | ● |
| [deBroome Brand Portal](../identity/saas-apps/debroome-brand-portal-tutorial) |  | ● |
| [Degreed](../identity/saas-apps/degreed-tutorial) |  | ● |
| [Delivery Solutions](../identity/saas-apps/delivery-solutions-tutorial) |  | ● |
| [Deputy](../identity/saas-apps/deputy-tutorial) |  | ● |
| [Descartes](../identity/saas-apps/descartes-tutorial) |  | ● |
| [Dialpad](../identity/saas-apps/dialpad-provisioning-tutorial) | ● |  |
| [Diffchecker](../identity/saas-apps/diffchecker-provisioning-tutorial) | ● | ● |
| [DigiCert](../identity/saas-apps/digicert-tutorial) |  | ● |
| [Digital Pigeon](../identity/saas-apps/digital-pigeon-tutorial) |  | ● |
| [Directory Services Protector](../identity/saas-apps/directory-services-protector-tutorial) |  | ● |
| [Directory Services](../identity/saas-apps/directory-services-tutorial) |  | ● |
| [directprint.io Cloud Print Administration](../identity/saas-apps/directprint-io-cloud-print-administration-tutorial) |  | ● |
| [Directprint.io](../identity/saas-apps/directprint-io-provisioning-tutorial) | ● | ● |
| [Displayr](../identity/saas-apps/displayr-tutorial) |  | ● |
| [Docker Business](../identity/saas-apps/docker-tutorial) |  | ● |
| [Documo](../identity/saas-apps/documo-provisioning-tutorial) | ● | ● |
| [DocuSign](../identity/saas-apps/docusign-provisioning-tutorial) | ● | ● |
| [Domo](../identity/saas-apps/domo-tutorial) |  | ● |
| [Dotcom-Monitor](../identity/saas-apps/dotcom-monitor-tutorial) |  | ● |
| [Dovetale](../identity/saas-apps/dovetale-tutorial) |  | ● |
| [Dozuki](../identity/saas-apps/dozuki-tutorial) |  | ● |
| [Draup, Inc](../identity/saas-apps/draup-inc-tutorial) |  | ● |
| [Drawboard Projects](../identity/saas-apps/drawboard-projects-tutorial) |  | ● |
| [Drift](../identity/saas-apps/drift-tutorial) |  | ● |
| [Dropbox Business](../identity/saas-apps/dropboxforbusiness-provisioning-tutorial) | ● | ● |
| [Druva](../identity/saas-apps/druva-provisioning-tutorial) | ● | ● |
| [Dynamic Signal](../identity/saas-apps/dynamic-signal-provisioning-tutorial) | ● | ● |
| [Dynatrace](../identity/saas-apps/dynatrace-tutorial) |  | ● |
| [EAComposer](../identity/saas-apps/eacomposer-tutorial) |  | ● |
| [EasySSO for Bamboo](../identity/saas-apps/easysso-for-bamboo-tutorial) |  | ● |
| [EasySSO for Confluence](../identity/saas-apps/easysso-for-confluence-tutorial) |  | ● |
| [EasySSO for Jira](../identity/saas-apps/easysso-for-jira-tutorial) |  | ● |
| [EBSCO](../identity/saas-apps/ebsco-tutorial) |  | ● |
| [Eccentex AppBase for Azure](../identity/saas-apps/eccentex-appbase-for-azure-tutorial) |  | ● |
| [eCornell](../identity/saas-apps/ecornell-tutorial) |  | ● |
| [EduBrite LMS](../identity/saas-apps/edubrite-lms-tutorial) |  | ● |
| [edX for Business SAML Integration](../identity/saas-apps/edx-for-business-saml-integration-tutorial) |  | ● |
| [Egnyte](../identity/saas-apps/egnyte-provisioning-tutorial) | ● | ● |
| [Egress](../identity/saas-apps/egress-tutorial) |  | ● |
| [eKincare](../identity/saas-apps/ekincare-tutorial) |  | ● |
| [Eletive](../identity/saas-apps/eletive-provisioning-tutorial) | ● |  |
| [Elia](../identity/saas-apps/elia-provisioning-tutorial) | ● | ● |
| [Elium](../identity/saas-apps/elium-provisioning-tutorial) | ● | ● |
| [Embed Signage](../identity/saas-apps/embed-signage-provisioning-tutorial) | ● | ● |
| [Employee Advocacy by Sprout Social](../identity/saas-apps/bambubysproutsocial-tutorial) |  | ● |
| [Enterprise Advantage](../identity/saas-apps/enterprise-advantage-tutorial) |  | ● |
| [Envoy](../identity/saas-apps/envoy-provisioning-tutorial) | ● | ● |
| [Equifax Workforce Solutions](../identity/saas-apps/equifax-workforce-solutions-tutorial) |  | ● |
| [ETU Skillsims](../identity/saas-apps/etu-skillsims-tutorial) |  | ● |
| [Evercate](../identity/saas-apps/evercate-provisioning-tutorial) | ● |  |
| [Exium](../identity/saas-apps/exium-provisioning-tutorial) | ● | ● |
| [EZOfficeInventory](../identity/saas-apps/ezofficeinventory-tutorial) |  | ● |
| [EZRentOut](../identity/saas-apps/ezrentout-tutorial) |  | ● |
| [Facebook Work Accounts](../identity/saas-apps/facebook-work-accounts-provisioning-tutorial) | ● | ● |
| [FAX.PLUS](../identity/saas-apps/fax-plus-tutorial) |  | ● |
| [Federated Directory](../identity/saas-apps/federated-directory-provisioning-tutorial) | ● |  |
| [Fexa](../identity/saas-apps/fexa-tutorial) |  | ● |
| [Figma](../identity/saas-apps/figma-provisioning-tutorial) | ● | ● |
| [FileCloud](../identity/saas-apps/filecloud-tutorial) |  | ● |
| [FileOrbis](../identity/saas-apps/fileorbis-tutorial) |  | ● |
| [FilesAnywhere](../identity/saas-apps/filesanywhere-tutorial) |  | ● |
| [Finvari](../identity/saas-apps/finvari-tutorial) |  | ● |
| [FiscalNote](../identity/saas-apps/fiscalnote-tutorial) |  | ● |
| [Fivetran](../identity/saas-apps/fivetran-tutorial) |  | ● |
| [Flexera One](../identity/saas-apps/flexera-one-tutorial) |  | ● |
| [Flipsnack SAML](../identity/saas-apps/flipsnack-saml-tutorial) |  | ● |
| [Flock Safety](../identity/saas-apps/flock-safety-tutorial) |  | ● |
| [Flock](../identity/saas-apps/flock-provisioning-tutorial) | ● | ● |
| [Folloze](../identity/saas-apps/folloze-tutorial) |  | ● |
| [Foodee](../identity/saas-apps/foodee-provisioning-tutorial) | ● | ● |
| [Forcepoint Cloud Security Gateway - User Authentication](../identity/saas-apps/forcepoint-cloud-security-gateway-provisioning-tutorial) | ● | ● |
| [ForeSee CX Suite](../identity/saas-apps/foreseecxsuite-tutorial) |  | ● |
| [Forms and Workflow](../identity/saas-apps/forms-workflow-provisioning-tutorial) | ● |  |
| [Fortes Change Cloud](../identity/saas-apps/fortes-change-cloud-provisioning-tutorial) | ● | ● |
| [FortiGate SSL VPN](../identity/saas-apps/fortigate-ssl-vpn-tutorial) |  | ● |
| [FortiSASE](../identity/saas-apps/fortisase-sia-tutorial) |  | ● |
| [Fountain](../identity/saas-apps/fountain-tutorial) |  | ● |
| [FourKites SAML2.0 SSO for Tracking](../identity/saas-apps/fourkites-tutorial) |  | ● |
| [Frankli.io](../identity/saas-apps/frankli-io-provisioning-tutorial) | ● |  |
| [Freight Audit](../identity/saas-apps/freight-audit-tutorial) |  | ● |
| [Freightender SSO for TRP (Tender Response Platform)](../identity/saas-apps/freightender-sso-for-trp-tender-response-platform-tutorial) |  | ● |
| [Fresh Relevance](../identity/saas-apps/fresh-relevance-tutorial) |  | ● |
| [Freshservice Provisioning](../identity/saas-apps/freshservice-provisioning-tutorial) | ● | ● |
| [FTAPI](../identity/saas-apps/ftapi-tutorial) |  | ● |
| [Fulcrum](../identity/saas-apps/fulcrum-tutorial) |  | ● |
| [Fullstory SAML](../identity/saas-apps/fullstory-saml-tutorial) |  | ● |
| [Funnel Leasing](../identity/saas-apps/funnel-leasing-provisioning-tutorial) | ● | ● |
| [Fuze](../identity/saas-apps/fuze-provisioning-tutorial) | ● | ● |
| [GaggleAMP](../identity/saas-apps/gaggleamp-tutorial) |  | ● |
| [Genesys Cloud for Azure](../identity/saas-apps/purecloud-by-genesys-provisioning-tutorial) | ● | ● |
| [getAbstract](../identity/saas-apps/getabstract-provisioning-tutorial) | ● | ● |
| [Getty Images](../identity/saas-apps/getty-images-tutorial) |  | ● |
| [GitHub Enterprise Cloud - Enterprise Account](../identity/saas-apps/github-enterprise-cloud-enterprise-account-tutorial) |  | ● |
| [GitHub Enterprise Managed User (OIDC)](../identity/saas-apps/github-enterprise-managed-user-oidc-provisioning-tutorial) | ● | ● |
| [GitHub Enterprise Managed User](../identity/saas-apps/github-enterprise-managed-user-provisioning-tutorial) | ● | ● |
| [GitHub Enterprise Server](../identity/saas-apps/github-enterprise-server-provisioning-tutorial) | ● | ● |
| [GitHub](../identity/saas-apps/github-provisioning-tutorial) | ● | ● |
| [Global Relay Identity Sync](../identity/saas-apps/global-relay-identity-sync-provisioning-tutorial) | ● |  |
| [GlobalOne](../identity/saas-apps/globalone-tutorial) |  | ● |
| [GlobeSmart](../identity/saas-apps/globesmart-tutorial) |  | ● |
| [goFLUENT](../identity/saas-apps/gofluent-tutorial) |  | ● |
| [GoLinks](../identity/saas-apps/golinks-provisioning-tutorial) | ● | ● |
| [Gong](../identity/saas-apps/gong-provisioning-tutorial) | ● |  |
| [Google G Suite](../identity/saas-apps/g-suite-provisioning-tutorial) | ● | ● |
| [GoProfiles](../identity/saas-apps/goprofiles-tutorial) |  | ● |
| [GoSearch](../identity/saas-apps/gosearch-tutorial) |  | ● |
| [GoTo](../identity/saas-apps/goto-provisioning-tutorial) | ● | ● |
| [Graebel Single Sign On with globalCONNECT](../identity/saas-apps/graebel-single-sign-on-with-globalconnect-tutorial) |  | ● |
| [Grammarly](../identity/saas-apps/grammarly-provisioning-tutorial) | ● | ● |
| [Granite](../identity/saas-apps/granite-tutorial) |  | ● |
| [GreenOrbit](../identity/saas-apps/greenorbit-tutorial) |  | ● |
| [Grok Learning](../identity/saas-apps/grok-learning-tutorial) |  | ● |
| [GroupTalk](../identity/saas-apps/grouptalk-provisioning-tutorial) | ● |  |
| [Grovo](../identity/saas-apps/grovo-tutorial) |  | ● |
| [Gtmhub](../identity/saas-apps/gtmhub-provisioning-tutorial) | ● |  |
| [Guru](../identity/saas-apps/guru-tutorial) |  | ● |
| [H5mag](../identity/saas-apps/h5mag-provisioning-tutorial) | ● |  |
| [Hackerone](../identity/saas-apps/hackerone-tutorial) |  | ● |
| [HappyFox](../identity/saas-apps/happyfox-tutorial) |  | ● |
| [Harness](../identity/saas-apps/harness-provisioning-tutorial) | ● | ● |
| [hCaptcha Enterprise](../identity/saas-apps/hcaptcha-enterprise-tutorial) |  | ● |
| [Headspace](../identity/saas-apps/headspace-provisioning-tutorial) | ● | ● |
| [HelloID](../identity/saas-apps/helloid-provisioning-tutorial) | ● |  |
| [Help Scout](../identity/saas-apps/helpscout-tutorial) |  | ● |
| [Helper Helper](../identity/saas-apps/helper-helper-tutorial) |  | ● |
| [Heroku](../identity/saas-apps/heroku-tutorial) |  | ● |
| [HeyBuddy](../identity/saas-apps/heybuddy-tutorial) |  | ● |
| [Hightail](../identity/saas-apps/hightail-tutorial) |  | ● |
| [Hive Learning](../identity/saas-apps/hive-learning-tutorial) |  | ● |
| [Hive](../identity/saas-apps/hive-tutorial) |  | ● |
| [Hootsuite](../identity/saas-apps/hootsuite-provisioning-tutorial) | ● | ● |
| [Hopsworks.ai](../identity/saas-apps/hopsworks-ai-tutorial) |  | ● |
| [Hornbill](../identity/saas-apps/hornbill-tutorial) |  | ● |
| [Hosted Graphite](../identity/saas-apps/hostedgraphite-tutorial) |  | ● |
| [HowNow WebApp SSO](../identity/saas-apps/hownow-webapp-sso-tutorial) |  | ● |
| [Howspace](../identity/saas-apps/howspace-provisioning-tutorial) | ● |  |
| [Hoxhunt](../identity/saas-apps/hoxhunt-provisioning-tutorial) | ● | ● |
| [HSB ThoughtSpot](../identity/saas-apps/hsb-thoughtspot-tutorial) |  | ● |
| [Humbol](../identity/saas-apps/humbol-provisioning-tutorial) | ● |  |
| [Hype](../identity/saas-apps/hype-tutorial) |  | ● |
| [Hypervault](../identity/saas-apps/hypervault-provisioning-tutorial) | ● |  |
| [IamIP Platform](../identity/saas-apps/iamip-patent-platform-tutorial) |  | ● |
| [IBM DB2 (SQL connector)](../identity/app-provisioning/tutorial-ecma-sql-connector) | ● |  |
| [IBM Domino (via MIM)](/en-us/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-domino) | ● |  |
| [IBM Tivoli Directory Server (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [IBMid](../identity/saas-apps/ibmid-tutorial) |  | ● |
| [Ideagen Cloud](../identity/saas-apps/ideagen-cloud-provisioning-tutorial) | ● |  |
| [Ideo](../identity/saas-apps/ideo-provisioning-tutorial) | ● | ● |
| [Igloo Software](../identity/saas-apps/igloo-software-tutorial) |  | ● |
| [iGrafx Platform](../identity/saas-apps/igrafx-platform-tutorial) |  | ● |
| [iHASCO Training](../identity/saas-apps/ihasco-training-tutorial) |  | ● |
| [iLMS](../identity/saas-apps/ilms-tutorial) |  | ● |
| [Imagen](../identity/saas-apps/imagen-tutorial) |  | ● |
| [Infogix Data3Sixty Govern](../identity/saas-apps/infogix-tutorial) |  | ● |
| [Infor CloudSuite](../identity/saas-apps/infor-cloudsuite-provisioning-tutorial) | ● | ● |
| [InformaCast](../identity/saas-apps/informacast-provisioning-tutorial) | ● | ● |
| [Informatica Intelligent Data Management Cloud](../identity/saas-apps/informatica-intelligent-data-management-cloud-tutorial) |  | ● |
| [Innotas](../identity/saas-apps/innotas-tutorial) |  | ● |
| [Innovation Hub](../identity/saas-apps/innovationhub-tutorial) |  | ● |
| [Insider](../identity/saas-apps/insider-tutorial) |  | ● |
| [Insight4GRC](../identity/saas-apps/insight4grc-provisioning-tutorial) | ● | ● |
| [InSightly SAML](../identity/saas-apps/insightly-saml-provisioning-tutorial) | ● | ● |
| [Insightsfirst](../identity/saas-apps/insightsfirst-tutorial) |  | ● |
| [Insite LMS](../identity/saas-apps/insite-lms-provisioning-tutorial) | ● |  |
| [InstaVR Viewer](../identity/saas-apps/instavr-viewer-tutorial) |  | ● |
| [International SOS Assistance Products](../identity/saas-apps/international-sos-assistance-products-tutorial) |  | ● |
| [introDus Pre and Onboarding Platform](../identity/saas-apps/introdus-pre-and-onboarding-platform-provisioning-tutorial) | ● |  |
| [IntSights](../identity/saas-apps/intsights-tutorial) |  | ● |
| [Invision](../identity/saas-apps/invision-provisioning-tutorial) | ● | ● |
| [InviteDesk](../identity/saas-apps/invitedesk-provisioning-tutorial) | ● |  |
| [IP Platform](../identity/saas-apps/ip-platform-tutorial) |  | ● |
| [iPass SmartConnect](../identity/saas-apps/ipass-smartconnect-provisioning-tutorial) | ● | ● |
| [iQualify LMS](../identity/saas-apps/iqualify-tutorial) |  | ● |
| [Iris Intranet](../identity/saas-apps/iris-intranet-provisioning-tutorial) | ● | ● |
| [IriusRisk](../identity/saas-apps/iriusrisk-tutorial) |  | ● |
| [ISG GovernX Federation](../identity/saas-apps/isg-governx-federation-tutorial) |  | ● |
| [Island](../identity/saas-apps/island-provisioning-tutorial) | ● | ● |
| [Isode directory server (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [IT-Conductor](../identity/saas-apps/it-conductor-tutorial) |  | ● |
| [Ivanti Service Manager (ISM)](../identity/saas-apps/ivanti-service-manager-tutorial) |  | ● |
| [Javelo](../identity/saas-apps/javelo-tutorial) |  | ● |
| [JFrog Artifactory](../identity/saas-apps/jfrog-artifactory-tutorial) |  | ● |
| [Jive](../identity/saas-apps/jive-provisioning-tutorial) | ● | ● |
| [Jooto](../identity/saas-apps/jooto-tutorial) |  | ● |
| [Jostle](../identity/saas-apps/jostle-provisioning-tutorial) | ● | ● |
| [Joyn FSM](../identity/saas-apps/joyn-fsm-provisioning-tutorial) | ● |  |
| [Juno Journey](../identity/saas-apps/juno-journey-provisioning-tutorial) | ● | ● |
| [Kairos Business](../identity/saas-apps/kairos-business-tutorial) |  | ● |
| [Kanbanize](../identity/saas-apps/kanbanize-tutorial) |  | ● |
| [Keepabl](../identity/saas-apps/keepabl-provisioning-tutorial) | ● | ● |
| [Keeper Password Manager & Digital Vault](../identity/saas-apps/keeper-password-manager-digitalvault-provisioning-tutorial) | ● | ● |
| [Kendis - Microsoft Entra Integration](../identity/saas-apps/kendis-scaling-agile-platform-tutorial) |  | ● |
| [Keystone](../identity/saas-apps/keystone-provisioning-tutorial) | ● | ● |
| [Khoros Care](../identity/saas-apps/khoros-care-tutorial) |  | ● |
| [Kindling](../identity/saas-apps/kindling-tutorial) |  | ● |
| [Kintone](../identity/saas-apps/kintone-provisioning-tutorial) | ● | ● |
| [Kion](../identity/saas-apps/cloudtamer-io-tutorial) |  | ● |
| [Kisi Physical Security](../identity/saas-apps/kisi-physical-security-provisioning-tutorial) | ● | ● |
| [Kiteworks](../identity/saas-apps/kiteworks-tutorial) |  | ● |
| [Klaxoon SAML](../identity/saas-apps/klaxoon-saml-provisioning-tutorial) | ● | ● |
| [Klaxoon](../identity/saas-apps/klaxoon-provisioning-tutorial) | ● | ● |
| [Klue](../identity/saas-apps/klue-tutorial) |  | ● |
| [Kno2fy](../identity/saas-apps/kno2fy-provisioning-tutorial) | ● | ● |
| [KnowBe4 Security Awareness Training](../identity/saas-apps/knowbe4-security-awareness-training-provisioning-tutorial) | ● | ● |
| [Knowledge Anywhere LMS](../identity/saas-apps/knowledge-anywhere-lms-tutorial) |  | ● |
| [Knowledge Work](../identity/saas-apps/knowledge-work-tutorial) |  | ● |
| [KnowledgeOwl](../identity/saas-apps/knowledgeowl-tutorial) |  | ● |
| [Kofax TotalAgility](../identity/saas-apps/kofax-totalagility-tutorial) |  | ● |
| [Kpifire](../identity/saas-apps/kpifire-provisioning-tutorial) | ● | ● |
| [KPN Grip](../identity/saas-apps/kpn-grip-provisioning-tutorial) | ● |  |
| [Krisp Technologies](../identity/saas-apps/krisp-technologies-tutorial) |  | ● |
| [Kumolus](../identity/saas-apps/kumolus-tutorial) |  | ● |
| [LabLog](../identity/saas-apps/lablog-tutorial) |  | ● |
| [LambdaTest Single Sign on](../identity/saas-apps/lambda-test-single-sign-on-tutorial) |  | ● |
| [LanSchool Air](../identity/saas-apps/lanschool-air-provisioning-tutorial) | ● | ● |
| [LaunchDarkly](../identity/saas-apps/launchdarkly-tutorial) |  | ● |
| [LawVu](../identity/saas-apps/lawvu-provisioning-tutorial) | ● | ● |
| [LDAP](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [Lean](../identity/saas-apps/lean-tutorial) |  | ● |
| [Leapsome](../identity/saas-apps/leapsome-provisioning-tutorial) | ● | ● |
| [LearnUpon](../identity/saas-apps/learnupon-tutorial) |  | ● |
| [Ledgy](../identity/saas-apps/ledgy-tutorial) |  | ● |
| [Lessonly](../identity/saas-apps/lessonly-tutorial) |  | ● |
| [Lexonis TalentScape](../identity/saas-apps/lexonis-talentscape-provisioning-tutorial) | ● | ● |
| [LimbleCMMS](../identity/saas-apps/limblecmms-provisioning-tutorial) | ● |  |
| [LinkedIn Elevate](../identity/saas-apps/linkedinelevate-provisioning-tutorial) | ● | ● |
| [LinkedIn Learning](../identity/saas-apps/linkedinlearning-tutorial) |  | ● |
| [LinkedIn Sales Navigator](../identity/saas-apps/linkedinsalesnavigator-provisioning-tutorial) | ● | ● |
| [LinkedIn Talent Solutions](../identity/saas-apps/linkedin-talent-solutions-tutorial) |  | ● |
| [Litmos](../identity/saas-apps/litmos-provisioning-tutorial) | ● | ● |
| [LogicGate](../identity/saas-apps/logicgate-provisioning-tutorial) | ● |  |
| [Looker Analytics Platform](../identity/saas-apps/looker-analytics-platform-tutorial) |  | ● |
| [Looop](../identity/saas-apps/looop-provisioning-tutorial) | ● |  |
| [Lucid (All Products)](../identity/saas-apps/lucid-all-products-provisioning-tutorial) | ● | ● |
| [Lucidchart](../identity/saas-apps/lucidchart-provisioning-tutorial) | ● | ● |
| [Lusha](../identity/saas-apps/lusha-tutorial) |  | ● |
| [LUSID](../identity/saas-apps/lusid-provisioning-tutorial) | ● | ● |
| [Lynda.com](../identity/saas-apps/lynda-tutorial) |  | ● |
| [M-Files](../identity/saas-apps/m-files-provisioning-tutorial) | ● | ● |
| [Mailosaur](../identity/saas-apps/mailosaur-tutorial) |  | ● |
| [Mapiq](../identity/saas-apps/mapiq-tutorial) |  | ● |
| [Maptician](../identity/saas-apps/maptician-provisioning-tutorial) | ● | ● |
| [Marker.io](../identity/saas-apps/marker-io-tutorial) |  | ● |
| [Markit Procurement Service](../identity/saas-apps/markit-procurement-service-provisioning-tutorial) | ● |  |
| [MDComune Business](../identity/saas-apps/mdcomune-business-tutorial) |  | ● |
| [MediusFlow](../identity/saas-apps/mediusflow-provisioning-tutorial) | ● |  |
| [Mend.io](../identity/saas-apps/mend-io-tutorial) |  | ● |
| [Mercell](../identity/saas-apps/mercell-tutorial) |  | ● |
| [MerchLogix](../identity/saas-apps/merchlogix-provisioning-tutorial) | ● | ● |
| [Meta Networks Connector](../identity/saas-apps/meta-networks-connector-provisioning-tutorial) | ● | ● |
| [Metatask](../identity/saas-apps/metatask-tutorial) |  | ● |
| [Mevisio](../identity/saas-apps/mevisio-tutorial) |  | ● |
| [MIC SAAS Portal](../identity/saas-apps/mic-saas-portal-tutorial) |  | ● |
| [MicroFocus Novell eDirectory (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [Microsoft 365](/en-us/microsoft-365/admin/manage/manage-group-licenses?view=o365-worldwide&amp;preserve-view=true) | ● | ● |
| [Microsoft Active Directory Lightweight Directory Server (ADAM) (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [Microsoft Azure SQL (SQL connector)](../identity/app-provisioning/tutorial-ecma-sql-connector) | ● |  |
| [Microsoft Azure](/en-us/azure/role-based-access-control/role-assignments-portal) | ● | ● |
| [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/manage-admins) | ● | ● |
| [Microsoft Dynamics 365 Commerce](/en-us/dynamics365/commerce/dev-itpro/arch-auth-flow) |  | ● |
| [Microsoft Dynamics 365 finance and operations](/en-us/dynamics365/guidance/implementation-guide/security-strategy-product-oa) |  | ● |
| [Microsoft Entra Domain Services](../identity/domain-services/synchronization) | ● | ● |
| [Microsoft Intune](/en-us/intune/intune-service/fundamentals/role-based-access-control#microsoft-entra-roles-with-intune-access) | ● | ● |
| [Microsoft SharePoint Server on-premises](../identity/saas-apps/sharepoint-on-premises-tutorial) |  | ● |
| [Microsoft SQL Server (SQL connector)](../identity/app-provisioning/tutorial-ecma-sql-connector) | ● |  |
| [Microsoft Viva Engage](/en-us/viva/engage/manage-viva-engage-groups/create-a-dynamic-group) | ● | ● |
| [Microsoft Windows Server Active Directory](../identity/hybrid/cloud-sync/govern-on-premises-groups) | ● | ● |
| [Mindtickle](../identity/saas-apps/mindtickle-provisioning-tutorial) | ● | ● |
| [Miro](../identity/saas-apps/miro-provisioning-tutorial) | ● | ● |
| [Mixpanel](../identity/saas-apps/mixpanel-provisioning-tutorial) | ● | ● |
| [MobileIron](../identity/saas-apps/mobileiron-provisioning-tutorial) | ● | ● |
| [Monday.com](../identity/saas-apps/mondaycom-provisioning-tutorial) | ● | ● |
| [MongoDB Atlas - SSO](../identity/saas-apps/mongodb-cloud-tutorial) |  | ● |
| [MongoDB Atlas](../identity/saas-apps/mongodb-cloud-tutorial) |  | ● |
| [Moqups](../identity/saas-apps/moqups-provisioning-tutorial) | ● | ● |
| [Movement by project44](../identity/saas-apps/movement-by-project44-tutorial) |  | ● |
| [Moveworks](../identity/saas-apps/moveworks-tutorial) |  | ● |
| [Mural Identity](../identity/saas-apps/mural-identity-provisioning-tutorial) | ● | ● |
| [MX3 Diagnostics](../identity/saas-apps/mx3-diagnostics-connector-provisioning-tutorial) | ● |  |
| [My IBISWorld](../identity/saas-apps/my-ibisworld-tutorial) |  | ● |
| [myPolicies](../identity/saas-apps/mypolicies-provisioning-tutorial) | ● | ● |
| [MySQL (SQL connector)](../identity/app-provisioning/tutorial-ecma-sql-connector) | ● |  |
| [MyVR](../identity/saas-apps/myvr-tutorial) |  | ● |
| [Navan](../identity/saas-apps/navan-tutorial) |  | ● |
| [NAVEX IRM (Lockpath/Keylight)](../identity/saas-apps/navex-irm-keylight-lockpath-tutorial) |  | ● |
| [NetIQ eDirectory (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [NetMotion Mobility](../identity/saas-apps/netmotion-mobility-tutorial) |  | ● |
| [Netpresenter Next](../identity/saas-apps/netpresenter-provisioning-tutorial) | ● |  |
| [Netskope User Authentication](../identity/saas-apps/netskope-administrator-console-provisioning-tutorial) | ● | ● |
| [Netsparker Enterprise](../identity/saas-apps/netsparker-enterprise-provisioning-tutorial) | ● | ● |
| [Neustar UltraDNS](../identity/saas-apps/neustar-ultradns-tutorial) |  | ● |
| [New Relic by Organization](../identity/saas-apps/new-relic-by-organization-provisioning-tutorial) | ● | ● |
| [Nimblex](../identity/saas-apps/nimblex-tutorial) |  | ● |
| [Nimbus](../identity/saas-apps/nimbus-tutorial) |  | ● |
| [Nitro Productivity Suite](../identity/saas-apps/nitro-productivity-suite-tutorial) |  | ● |
| [Nomadesk](../identity/saas-apps/nomadesk-tutorial) |  | ● |
| [NordPass](../identity/saas-apps/nordpass-provisioning-tutorial) | ● | ● |
| [Notion](../identity/saas-apps/notion-provisioning-tutorial) | ● | ● |
| [Novatus](../identity/saas-apps/novatus-tutorial) |  | ● |
| [Novell eDirectory (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [Nuclino](../identity/saas-apps/nuclino-tutorial) |  | ● |
| [O'Reilly Learning Platform](../identity/saas-apps/oreilly-learning-platform-provisioning-tutorial) | ● | ● |
| [OfficeSpace Software](../identity/saas-apps/officespace-software-provisioning-tutorial) | ● | ● |
| [Olfeo SAAS](../identity/saas-apps/olfeo-saas-provisioning-tutorial) | ● | ● |
| [OneDesk](../identity/saas-apps/onedesk-tutorial) |  | ● |
| [Oneflow](../identity/saas-apps/oneflow-provisioning-tutorial) | ● | ● |
| [Oneteam](../identity/saas-apps/oneteam-tutorial) |  | ● |
| [OneTrust Privacy Management Software](../identity/saas-apps/onetrust-tutorial) |  | ● |
| [Onshape](../identity/saas-apps/onshape-tutorial) |  | ● |
| [Onyxia](../identity/saas-apps/onyxia-tutorial) |  | ● |
| [Open DJ (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [Open DS (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [OpenAthens](../identity/saas-apps/openathens-tutorial) |  | ● |
| [OpenLDAP](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [OpenText Directory Services](../identity/saas-apps/open-text-directory-services-provisioning-tutorial) | ● | ● |
| [OptiTurn](../identity/saas-apps/optiturn-tutorial) |  | ● |
| [Oracle Access Manager for Oracle E-Business Suite](../identity/saas-apps/oracle-access-manager-for-oracle-ebs-tutorial) |  | ● |
| [Oracle Access Manager for Oracle Retail Merchandising](../identity/saas-apps/oracle-access-manager-for-oracle-retail-merchandising-tutorial) |  | ● |
| [Oracle Cloud Infrastructure Console](../identity/saas-apps/oracle-cloud-infrastructure-console-provisioning-tutorial) | ● | ● |
| [Oracle Database (SQL connector)](../identity/app-provisioning/tutorial-ecma-sql-connector) | ● |  |
| [Oracle E-Business Suite](../identity/app-provisioning/on-premises-web-services-connector) | ● | ● |
| [Oracle Fusion ERP](../identity/saas-apps/oracle-fusion-erp-provisioning-tutorial) | ● | ● |
| [Oracle IDCS for E-Business Suite](../identity/saas-apps/oracle-idcs-for-ebs-tutorial) |  | ● |
| [Oracle IDCS for JD Edwards](../identity/saas-apps/oracle-idcs-for-jd-edwards-tutorial) |  | ● |
| [Oracle IDCS for PeopleSoft](../identity/saas-apps/oracle-idcs-for-peoplesoft-tutorial) |  | ● |
| [Oracle PeopleSoft ERP](../identity/app-provisioning/on-premises-web-services-connector) | ● | ● |
| [Oracle SunONE Directory Server Enerprise Edition (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [Othership Workplace Scheduler](../identity/saas-apps/othership-workplace-scheduler-tutorial) |  | ● |
| [OutSystems](../identity/saas-apps/outsystems-tutorial) |  | ● |
| [Overdrive](../identity/saas-apps/overdrive-books-tutorial) |  | ● |
| [PagerDuty](../identity/saas-apps/pagerduty-tutorial) |  | ● |
| [Palantir Foundry](../identity/saas-apps/palantir-foundry-tutorial) |  | ● |
| [Palo Alto Networks - Admin UI](../identity/saas-apps/paloaltoadmin-tutorial) |  | ● |
| [Palo Alto Networks - Captive Portal](../identity/saas-apps/paloaltonetworks-captiveportal-tutorial) |  | ● |
| [Palo Alto Networks - GlobalProtect](../identity/saas-apps/palo-alto-networks-globalprotect-tutorial) |  | ● |
| [Palo Alto Networks Cloud Identity Engine - Cloud Authentication Service](../identity/saas-apps/palo-alto-networks-cloud-identity-engine-provisioning-tutorial) | ● | ● |
| [Palo Alto Networks SCIM Connector](../identity/saas-apps/palo-alto-networks-scim-connector-provisioning-tutorial) | ● | ● |
| [PandaDoc](../identity/saas-apps/pandadoc-tutorial) |  | ● |
| [Panopto](../identity/saas-apps/panopto-tutorial) |  | ● |
| [Panorays](../identity/saas-apps/panorays-tutorial) |  | ● |
| [PaperCut Cloud Print Management](../identity/saas-apps/papercut-cloud-print-management-provisioning-tutorial) | ● |  |
| [Papirfly SSO](../identity/saas-apps/papirfly-sso-tutorial) |  | ● |
| [Parkable](../identity/saas-apps/parkable-tutorial) |  | ● |
| [Parkalot - Car park management](../identity/saas-apps/parkalot-car-park-management-tutorial) |  | ● |
| [Parsable](../identity/saas-apps/parsable-provisioning-tutorial) | ● |  |
| [Peakon](../identity/saas-apps/peakon-provisioning-tutorial) | ● | ● |
| [Perimeter 81](../identity/saas-apps/perimeter-81-tutorial) |  | ● |
| [Peripass](../identity/saas-apps/peripass-provisioning-tutorial) | ● |  |
| [Personify Inc](../identity/saas-apps/personify-inc-provisioning-tutorial) | ● | ● |
| [Pingboard](../identity/saas-apps/pingboard-provisioning-tutorial) | ● | ● |
| [PKSHA ChatAgent](../identity/saas-apps/pksha-chatagent-tutorial) |  | ● |
| [Plandisc](../identity/saas-apps/plandisc-provisioning-tutorial) | ● |  |
| [PlanMyLeave](../identity/saas-apps/planmyleave-tutorial) |  | ● |
| [Playvox](../identity/saas-apps/playvox-provisioning-tutorial) | ● |  |
| [Pluto](../identity/saas-apps/pluto-tutorial) |  | ● |
| [Podbean](../identity/saas-apps/podbean-tutorial) |  | ● |
| [PolicyStat](../identity/saas-apps/policystat-tutorial) |  | ● |
| [PoliteMail - SSO](../identity/saas-apps/politemail-sso-tutorial) |  | ● |
| [Postgres (SQL connector)](../identity/app-provisioning/tutorial-ecma-sql-connector) | ● |  |
| [Postman](../identity/saas-apps/postman-provisioning-tutorial) | ● | ● |
| [Preciate](../identity/saas-apps/preciate-provisioning-tutorial) | ● |  |
| [PressReader](../identity/saas-apps/pressreader-tutorial) |  | ● |
| [PrinterLogic SaaS](../identity/saas-apps/printer-logic-saas-provisioning-tutorial) | ● | ● |
| [PrinterLogic](../identity/saas-apps/printerlogic-saas-tutorial) |  | ● |
| [Printix](../identity/saas-apps/printix-tutorial) |  | ● |
| [Priority Matrix](../identity/saas-apps/priority-matrix-provisioning-tutorial) | ● |  |
| [Prisma Cloud SSO](../identity/saas-apps/prisma-cloud-tutorial) |  | ● |
| [ProcessUnity](../identity/saas-apps/processunity-tutorial) |  | ● |
| [ProdPad](../identity/saas-apps/prodpad-provisioning-tutorial) | ● | ● |
| [productboard](../identity/saas-apps/productboard-tutorial) |  | ● |
| [Productive](../identity/saas-apps/productive-tutorial) |  | ● |
| [ProductPlan](../identity/saas-apps/productplan-tutorial) |  | ● |
| [ProjectPlace](../identity/saas-apps/projectplace-tutorial) |  | ● |
| [Promapp](../identity/saas-apps/promapp-provisioning-tutorial) | ● |  |
| [Proofpoint Security Awareness Training](../identity/saas-apps/proofpoint-security-awareness-training-tutorial) |  | ● |
| [Proware](../identity/saas-apps/proware-provisioning-tutorial) | ● | ● |
| [Proxyclick](../identity/saas-apps/proxyclick-provisioning-tutorial) | ● | ● |
| [PurelyHR](../identity/saas-apps/purelyhr-tutorial) |  | ● |
| [pymetrics](../identity/saas-apps/pymetrics-tutorial) |  | ● |
| [QA](../identity/saas-apps/cloud-academy-sso-provisioning-tutorial) | ● | ● |
| [Qiita Team](../identity/saas-apps/qiita-team-tutorial) |  | ● |
| [Qmarkets Idea & Innovation Management](../identity/saas-apps/qmarkets-idea-innovation-management-tutorial) |  | ● |
| [QReserve](../identity/saas-apps/qreserve-tutorial) |  | ● |
| [Qualtrics](../identity/saas-apps/qualtrics-tutorial) |  | ● |
| [Quarem](../identity/saas-apps/quarem-provisioning-tutorial) | ● | ● |
| [QuickHelp](../identity/saas-apps/quickhelp-tutorial) |  | ● |
| [Qumu Cloud](../identity/saas-apps/qumucloud-tutorial) |  | ● |
| [Radancy's Employee Referrals](../identity/saas-apps/radancys-employee-referrals-tutorial) |  | ● |
| [Radiant IOT Portal](../identity/saas-apps/radiant-iot-portal-tutorial) |  | ● |
| [RadiantOne Virtual Directory Server (VDS) (LDAP connector)](../identity/app-provisioning/on-premises-ldap-connector-configure) | ● |  |
| [raum\]für\[raum](../identity/saas-apps/raumfurraum-tutorial) |  | ● |
| [Reach 360](../identity/saas-apps/reach-360-tutorial) |  | ● |
| [ReadCube Papers](../identity/saas-apps/readcube-papers-tutorial) |  | ● |
| [Real Links](../identity/saas-apps/real-links-provisioning-tutorial) | ● | ● |
| [Recnice](../identity/saas-apps/recnice-provisioning-tutorial) | ● |  |
| [Redocly](../identity/saas-apps/redocly-tutorial) |  | ● |
| [Reprints Desk - Article Galaxy](../identity/saas-apps/reprints-desk-article-galaxy-tutorial) |  | ● |
| [Rescana](../identity/saas-apps/rescana-tutorial) |  | ● |
| [Resource Central – SAML SSO for Meeting Room Booking System](../identity/saas-apps/resource-central-tutorial) |  | ● |
| [Retail Zipline](../identity/saas-apps/retail-zipline-tutorial) |  | ● |
| [RevSpace](../identity/saas-apps/revspace-tutorial) |  | ● |
| [Reward Gateway](../identity/saas-apps/reward-gateway-provisioning-tutorial) | ● | ● |
| [Rewatch](../identity/saas-apps/rewatch-tutorial) |  | ● |
| [RFPIO](../identity/saas-apps/rfpio-provisioning-tutorial) | ● | ● |
| [Rhombus Systems](../identity/saas-apps/rhombus-systems-provisioning-tutorial) | ● | ● |
| [RightCrowd Workforce Management](../identity/saas-apps/rightcrowd-workforce-management-tutorial) |  | ● |
| [RingCentral](../identity/saas-apps/ringcentral-provisioning-tutorial) | ● | ● |
| [Rise.com](../identity/saas-apps/risecom-tutorial) |  | ● |
| [Robin](../identity/saas-apps/robin-provisioning-tutorial) | ● | ● |
| [RocketReach SSO](../identity/saas-apps/rocketreach-sso-tutorial) |  | ● |
| [RoleMapper](../identity/saas-apps/rolemapper-tutorial) |  | ● |
| [Rollbar](../identity/saas-apps/rollbar-provisioning-tutorial) | ● | ● |
| [Rootly](../identity/saas-apps/rootly-provisioning-tutorial) | ● | ● |
| [Rouse Sales](../identity/saas-apps/rouse-sales-provisioning-tutorial) | ● |  |
| [RSA Archer Suite](../identity/saas-apps/rsa-archer-suite-tutorial) |  | ● |
| [RStudio Connect SAML Authentication](../identity/saas-apps/rstudio-connect-tutorial) |  | ● |
| [S4 - Digitsec](../identity/saas-apps/s4-digitsec-tutorial) |  | ● |
| [Saba Cloud](../identity/saas-apps/saba-cloud-tutorial) |  | ● |
| [SafeGuard Cyber](../identity/saas-apps/safeguard-cyber-provisioning-tutorial) | ● | ● |
| [Salesforce Sandbox](../identity/saas-apps/salesforce-sandbox-provisioning-tutorial) | ● | ● |
| [Salesforce](../identity/saas-apps/salesforce-provisioning-tutorial) | ● | ● |
| [Samanage](../identity/saas-apps/samanage-provisioning-tutorial) | ● | ● |
| [SAML SSO for Bamboo by resolution GmbH](../identity/saas-apps/bamboo-tutorial) |  | ● |
| [SAML SSO for Bitbucket by resolution GmbH](../identity/saas-apps/bitbucket-tutorial) |  | ● |
| [SAML SSO for Jira by resolution GmbH](../identity/saas-apps/samlssojira-tutorial) |  | ● |
| [SAML-based apps](../identity/enterprise-apps/add-application-portal-setup-sso) |  | ● |
| [Samsara](../identity/saas-apps/samsara-tutorial) |  | ● |
| [SAP Analytics Cloud](../identity/saas-apps/sap-analytics-cloud-provisioning-tutorial) | ● | ● |
| [SAP Ariba Spend Management solutions](../identity/saas-apps/sap-ariba-spend-management-solutions-provisioning-tutorial) | ● | ● |
| [SAP Business ByDesign](../identity/saas-apps/sapbusinessbydesign-tutorial) |  | ● |
| [SAP Business Technology Platform (BTP)](../identity/saas-apps/sap-hana-cloud-platform-tutorial) |  | ● |
| [SAP Cloud for Customer](../identity/saas-apps/sap-customer-cloud-tutorial) |  | ● |
| [SAP Cloud Identity Services](../identity/saas-apps/sap-cloud-platform-identity-authentication-provisioning-tutorial) | ● | ● |
| [SAP Concur](../identity/saas-apps/sap-concur-provisioning-tutorial) | ● | ● |
| [SAP Fieldglass](../identity/saas-apps/fieldglass-tutorial) |  | ● |
| [SAP Fiori](../identity/saas-apps/sap-fiori-tutorial) |  | ● |
| [SAP HANA](../identity/saas-apps/sap-hana-provisioning-tutorial) |  | ● |
| [SAP Litmos](../identity/saas-apps/litmos-tutorial) |  | ● |
| [SAP NetWeaver](../identity/app-provisioning/on-premises-sap-connector-configure) | ● | ● |
| [SAP R/3 and ERP Central Component (ECC)](../identity/app-provisioning/on-premises-sap-connector-configure) | ● | ● |
| [SAP S/4HANA](../identity/saas-apps/sap-s4hana-provisioning-tutorial) | ● | ● |
| [SAP SuccessFactors to Active Directory](../identity/saas-apps/sap-successfactors-inbound-provisioning-tutorial) | ● | ● |
| [SAP SuccessFactors to Microsoft Entra ID](../identity/saas-apps/sap-successfactors-inbound-provisioning-cloud-only-tutorial) | ● | ● |
| [SAP SuccessFactors Writeback](../identity/saas-apps/sap-successfactors-writeback-tutorial) | ● | ● |
| [Sapient](../identity/saas-apps/sapient-tutorial) |  | ● |
| [SAS Viya](../identity/saas-apps/sas-viya-sso-provisioning-tutorial) | ● | ● |
| [Sauce Labs - Mobile and Web Testing](../identity/saas-apps/saucelabs-mobileandwebtesting-tutorial) |  | ● |
| [Sauce Labs](../identity/saas-apps/sauce-labs-tutorial) |  | ● |
| [Saviynt](../identity/saas-apps/saviynt-tutorial) |  | ● |
| [SchoolStream ASA](../identity/saas-apps/schoolstream-asa-provisioning-tutorial) | ● | ● |
| [Sciforma](../identity/saas-apps/sciforma-tutorial) |  | ● |
| [Scilife Microsoft Entra SSO](../identity/saas-apps/scilife-azure-ad-sso-tutorial) |  | ● |
| [SCIM-based apps in the cloud](../identity/app-provisioning/use-scim-to-provision-users-and-groups) | ● |  |
| [SCIM-based apps on-premises](../identity/app-provisioning/on-premises-scim-provisioning) | ● |  |
| [SciQuest Spend Director](../identity/saas-apps/sciquest-spend-director-tutorial) |  | ● |
| [ScreenPal](../identity/saas-apps/screencast-tutorial) |  | ● |
| [ScreenSteps](../identity/saas-apps/screensteps-provisioning-tutorial) | ● | ● |
| [SDS & Chemical Information Management](../identity/saas-apps/sds-chemical-information-management-tutorial) |  | ● |
| [Second Nature AI](../identity/saas-apps/second-nature-ai-tutorial) |  | ● |
| [Secure Deliver](../identity/saas-apps/securedeliver-tutorial) |  | ● |
| [SecureLogin](../identity/saas-apps/secure-login-provisioning-tutorial) | ● |  |
| [SeekOut](../identity/saas-apps/seekout-tutorial) |  | ● |
| [Segment](../identity/saas-apps/segment-provisioning-tutorial) | ● | ● |
| [SendSafely](../identity/saas-apps/sendsafely-tutorial) |  | ● |
| [Sentry](../identity/saas-apps/sentry-provisioning-tutorial) | ● | ● |
| [ServiceChannel](../identity/saas-apps/servicechannel-tutorial) |  | ● |
| [ServiceNow](../identity/saas-apps/servicenow-provisioning-tutorial) | ● | ● |
| [ServusConnect](../identity/saas-apps/servusconnect-tutorial) |  | ● |
| [ShareCal](../identity/saas-apps/sharecal-tutorial) |  | ● |
| [ShareVault](../identity/saas-apps/sharevault-tutorial) |  | ● |
| [SharingCloud](../identity/saas-apps/sharingcloud-tutorial) |  | ● |
| [ShipHazmat](../identity/saas-apps/shiphazmat-tutorial) |  | ● |
| [Shmoop For Schools](../identity/saas-apps/shmoopforschools-tutorial) |  | ● |
| [Shopify Plus](../identity/saas-apps/shopify-plus-provisioning-tutorial) | ● | ● |
| [Showpad](../identity/saas-apps/showpad-tutorial) |  | ● |
| [Sigma Computing](../identity/saas-apps/sigma-computing-provisioning-tutorial) | ● | ● |
| [Signagelive](../identity/saas-apps/signagelive-provisioning-tutorial) | ● | ● |
| [SignalFx](../identity/saas-apps/signalfx-tutorial) |  | ● |
| [Signiant Media Shuttle](../identity/saas-apps/signiant-media-shuttle-tutorial) |  | ● |
| [Sigstr](../identity/saas-apps/sigstr-tutorial) |  | ● |
| [Simple In/Out](../identity/saas-apps/simple-in-out-provisioning-tutorial) | ● |  |
| [SIS Enterprise](../identity/saas-apps/sis-enterprise-tutorial) |  | ● |
| [Sketch](../identity/saas-apps/sketch-tutorial) |  | ● |
| [Skilljar](../identity/saas-apps/skilljar-tutorial) |  | ● |
| [Skills Base](../identity/saas-apps/skillsbase-tutorial) |  | ● |
| [Skopenow](../identity/saas-apps/skopenow-tutorial) |  | ● |
| [SKYSITE](../identity/saas-apps/skysite-tutorial) |  | ● |
| [Slack](../identity/saas-apps/slack-provisioning-tutorial) | ● | ● |
| [Smallstep SSH](../identity/saas-apps/smallstep-ssh-provisioning-tutorial) | ● |  |
| [Smart360](../identity/saas-apps/smart360-tutorial) |  | ● |
| [SmartDraw](../identity/saas-apps/smartdraw-tutorial) |  | ● |
| [Smartfile](../identity/saas-apps/smartfile-provisioning-tutorial) | ● | ● |
| [SmartHub INFER](../identity/saas-apps/smarthub-infer-tutorial) |  | ● |
| [Smartlook](../identity/saas-apps/smartlook-tutorial) |  | ● |
| [Smartplan](../identity/saas-apps/smartplan-tutorial) |  | ● |
| [Smartsheet](../identity/saas-apps/smartsheet-provisioning-tutorial) | ● |  |
| [Snackmagic](../identity/saas-apps/snackmagic-tutorial) |  | ● |
| [Snowflake](../identity/saas-apps/snowflake-provisioning-tutorial) | ● | ● |
| [Softeon WMS](../identity/saas-apps/softeon-tutorial) |  | ● |
| [Software AG Cloud](../identity/saas-apps/software-ag-cloud-tutorial) |  | ● |
| [Soloinsight-CloudGate SSO](../identity/saas-apps/soloinsight-cloudgate-sso-provisioning-tutorial) | ● | ● |
| [SoSafe](../identity/saas-apps/sosafe-provisioning-tutorial) | ● | ● |
| [SpaceIQ](../identity/saas-apps/spaceiq-provisioning-tutorial) | ● | ● |
| [SpectrumU](../identity/saas-apps/spectrumu-tutorial) |  | ● |
| [Speexx](../identity/saas-apps/speexx-tutorial) |  | ● |
| [Splashtop Secure Workspace](../identity/saas-apps/splashtop-secure-workspace-tutorial) |  | ● |
| [Splashtop](../identity/saas-apps/splashtop-provisioning-tutorial) | ● | ● |
| [SquaREcruit](../identity/saas-apps/squarecruit-tutorial) |  | ● |
| [SSO for Jama Connect®](../identity/saas-apps/sso-for-jama-connect-tutorial) |  | ● |
| [Stackby](../identity/saas-apps/stackby-tutorial) |  | ● |
| [Stage and Screen](../identity/saas-apps/stage-and-screen-tutorial) |  | ● |
| [StarLeaf](../identity/saas-apps/starleaf-provisioning-tutorial) | ● |  |
| [Starmind](../identity/saas-apps/starmind-provisioning-tutorial) | ● | ● |
| [Stonebranch Universal Automation Center (SaaS Cloud)](../identity/saas-apps/stonebranch-universal-automation-center-saas-cloud-tutorial) |  | ● |
| [Storegate](../identity/saas-apps/storegate-provisioning-tutorial) | ● |  |
| [Stormboard](../identity/saas-apps/stormboard-tutorial) |  | ● |
| [Striim Cloud](../identity/saas-apps/striim-cloud-tutorial) |  | ● |
| [Striim Platform](../identity/saas-apps/striim-platform-tutorial) |  | ● |
| [Superluminal](../identity/saas-apps/superluminal-tutorial) |  | ● |
| [Supermood](../identity/saas-apps/supermood-tutorial) |  | ● |
| [Supply Chain Catalyst](../identity/saas-apps/supply-chain-catalyst-tutorial) |  | ● |
| [SURFconext](../identity/saas-apps/surfconext-tutorial) |  | ● |
| [SurveyMonkey Enterprise](../identity/saas-apps/surveymonkey-enterprise-provisioning-tutorial) | ● | ● |
| [Swit](../identity/saas-apps/swit-provisioning-tutorial) | ● | ● |
| [Symantec Web Security Service (WSS)](../identity/saas-apps/symantec-web-security-service) | ● | ● |
| [Syndio](../identity/saas-apps/syndio-tutorial) |  | ● |
| [Synerise AI Growth Operating System](../identity/saas-apps/synerise-ai-growth-ecosystem-tutorial) |  | ● |
| [Syniverse Customer Portal](../identity/saas-apps/syniverse-customer-portal-tutorial) |  | ● |
| [Tableau Cloud](../identity/saas-apps/tableau-online-provisioning-tutorial) | ● | ● |
| [Tailscale](../identity/saas-apps/tailscale-provisioning-tutorial) | ● |  |
| [Talent Palette](../identity/saas-apps/talent-palette-tutorial) |  | ● |
| [Talentech](../identity/saas-apps/talentech-provisioning-tutorial) | ● |  |
| [Tanium SSO](../identity/saas-apps/tanium-sso-provisioning-tutorial) | ● | ● |
| [Tap App Security](../identity/saas-apps/tap-app-security-provisioning-tutorial) | ● | ● |
| [TargetProcess](../identity/saas-apps/target-process-tutorial) |  | ● |
| [TASC (beta)](../identity/saas-apps/tasc-beta-tutorial) |  | ● |
| [Taskize Connect](../identity/saas-apps/taskize-connect-provisioning-tutorial) | ● | ● |
| [Team Today](../identity/saas-apps/team-today-provisioning-tutorial) | ● |  |
| [TeamAlert SSO](../identity/saas-apps/teamalert-sso-tutorial) |  | ● |
| [Teamgo](../identity/saas-apps/teamgo-provisioning-tutorial) | ● | ● |
| [TeamSlide](../identity/saas-apps/teamslide-tutorial) |  | ● |
| [TeamSticker by Communitio](../identity/saas-apps/teamsticker-by-communitio-tutorial) |  | ● |
| [TeamViewer](../identity/saas-apps/teamviewer-provisioning-tutorial) | ● | ● |
| [Templafy OpenID Connect](../identity/saas-apps/templafy-openid-connect-provisioning-tutorial) | ● | ● |
| [Templafy SAML2](../identity/saas-apps/templafy-saml-2-provisioning-tutorial) | ● | ● |
| [TencentCloud IDaaS](../identity/saas-apps/tencent-cloud-idaas-tutorial) |  | ● |
| [Tendium](../identity/saas-apps/tendium-tutorial) |  | ● |
| [Terraform Cloud](../identity/saas-apps/terraform-cloud-tutorial) |  | ● |
| [Terraform Enterprise](../identity/saas-apps/terraform-enterprise-tutorial) |  | ● |
| [TerraTrue](../identity/saas-apps/terratrue-provisioning-tutorial) | ● | ● |
| [tesma](../identity/saas-apps/tesma-tutorial) |  | ● |
| [TestingBot](../identity/saas-apps/testingbot-tutorial) |  | ● |
| [TextExpander](../identity/saas-apps/textexpander-tutorial) |  | ● |
| [Textline](../identity/saas-apps/textline-tutorial) |  | ● |
| [TextMagic](../identity/saas-apps/textmagic-tutorial) |  | ● |
| [TheOrgWiki](../identity/saas-apps/theorgwiki-provisioning-tutorial) | ● |  |
| [Thoropass](../identity/saas-apps/thoropass-tutorial) |  | ● |
| [ThousandEyes](../identity/saas-apps/thousandeyes-provisioning-tutorial) | ● | ● |
| [ThreatQ Platform](../identity/saas-apps/threatq-platform-tutorial) |  | ● |
| [Thrive LXP](../identity/saas-apps/thrive-lxp-provisioning-tutorial) | ● | ● |
| [Tic-Tac Mobile](../identity/saas-apps/tic-tac-mobile-provisioning-tutorial) | ● |  |
| [TicketManager](../identity/saas-apps/ticketmanager-tutorial) |  | ● |
| [TimeClock 365 SAML](../identity/saas-apps/timeclock-365-saml-provisioning-tutorial) | ● | ● |
| [TimeClock 365](../identity/saas-apps/timeclock-365-provisioning-tutorial) | ● | ● |
| [TimeLive](../identity/saas-apps/timelive-tutorial) |  | ● |
| [TimeOffManager](../identity/saas-apps/timeoffmanager-tutorial) |  | ● |
| [TIMU](../identity/saas-apps/timu-tutorial) |  | ● |
| [TiViTz](../identity/saas-apps/tivitz-tutorial) |  | ● |
| [TonicDM](../identity/saas-apps/tonicdm-tutorial) |  | ● |
| [Torii](../identity/saas-apps/torii-provisioning-tutorial) | ● | ● |
| [Tracker Software Technologies](../identity/saas-apps/tracker-software-technologies-tutorial) |  | ● |
| [TrackVia](../identity/saas-apps/trackvia-tutorial) |  | ● |
| [Training Platform](../identity/saas-apps/training-platform-tutorial) |  | ● |
| [TransPerfect GlobalLink Dashboard](../identity/saas-apps/transperfect-globallink-dashboard-tutorial) |  | ● |
| [Tranxfer](../identity/saas-apps/tranxfer-tutorial) |  | ● |
| [TravelPerk](../identity/saas-apps/travelperk-provisioning-tutorial) | ● | ● |
| [Tribeloo](../identity/saas-apps/tribeloo-provisioning-tutorial) | ● | ● |
| [Trisotech Digital Enterprise Server](../identity/saas-apps/trisotechdigitalenterpriseserver-tutorial) |  | ● |
| [TrueChoice](../identity/saas-apps/truechoice-tutorial) |  | ● |
| [TrustWorks](../identity/saas-apps/trustworks-tutorial) |  | ● |
| [Twilio Sendgrid](../identity/saas-apps/twilio-sendgrid-tutorial) |  | ● |
| [Twingate](../identity/saas-apps/twingate-provisioning-tutorial) | ● |  |
| [Uber](../identity/saas-apps/uber-provisioning-tutorial) | ● |  |
| [Udemy Business SAML](../identity/saas-apps/udemy-business-saml-tutorial) |  | ● |
| [UKG Pro](../identity/saas-apps/ultipro-tutorial) |  | ● |
| [uni-tel A/S](../identity/saas-apps/uni-tel-as-provisioning-tutorial) | ● |  |
| [UNIFI](../identity/saas-apps/unifi-provisioning-tutorial) | ● | ● |
| [uniFlow Online](../identity/saas-apps/uniflow-online-provisioning-tutorial) | ● | ● |
| [Unite Us](../identity/saas-apps/unite-us-tutorial) |  | ● |
| [Upwork Enterprise](../identity/saas-apps/upwork-enterprise-tutorial) |  | ● |
| [User Interviews](../identity/saas-apps/user-interviews-tutorial) |  | ● |
| [V-Client](../identity/saas-apps/v-client-provisioning-tutorial) | ● | ● |
| [Vault Platform](../identity/saas-apps/vault-platform-provisioning-tutorial) | ● | ● |
| [Vbrick Rev Cloud](../identity/saas-apps/vbrick-rev-cloud-provisioning-tutorial) | ● | ● |
| [Velpic SAML](../identity/saas-apps/velpicsaml-tutorial) |  | ● |
| [Velpic](../identity/saas-apps/velpic-provisioning-tutorial) | ● | ● |
| [Vera Suite](../identity/saas-apps/vera-suite-tutorial) |  | ● |
| [Verity](../identity/saas-apps/verity-tutorial) |  | ● |
| [Veza](../identity/saas-apps/veza-tutorial) |  | ● |
| [VIDA](../identity/saas-apps/vida-tutorial) |  | ● |
| [Vidyard](../identity/saas-apps/vidyard-tutorial) |  | ● |
| [Virtual Risk Manager - USA](../identity/saas-apps/virtual-risk-manager-usa-tutorial) |  | ● |
| [Visibly](../identity/saas-apps/visibly-provisioning-tutorial) | ● | ● |
| [Visitly](../identity/saas-apps/visitly-provisioning-tutorial) | ● | ● |
| [Visma](../identity/saas-apps/visma-tutorial) |  | ● |
| [VMware Identity Service](../identity/saas-apps/vmware-identity-service-tutorial) |  | ● |
| [Vonage](../identity/saas-apps/vonage-provisioning-tutorial) | ● | ● |
| [Voyance](../identity/saas-apps/voyance-tutorial) |  | ● |
| [Vtiger CRM (SAML)](../identity/saas-apps/vtiger-crm-saml-tutorial) |  | ● |
| [WalkMe SAML2.0](../identity/saas-apps/walkme-saml-tutorial) |  | ● |
| [WATS](../identity/saas-apps/wats-provisioning-tutorial) | ● |  |
| [Way We Do](../identity/saas-apps/waywedo-tutorial) |  | ● |
| [Web Cargo Air](../identity/saas-apps/web-cargo-air-provisioning-tutorial) | ● | ● |
| [WebCE](../identity/saas-apps/webce-tutorial) |  | ● |
| [Webroot Security Awareness Training](../identity/saas-apps/webroot-security-awareness-training-provisioning-tutorial) | ● |  |
| [WebTMA](../identity/saas-apps/webtma-tutorial) |  | ● |
| [WEDO](../identity/saas-apps/wedo-provisioning-tutorial) | ● | ● |
| [Weekdone](../identity/saas-apps/weekdone-tutorial) |  | ● |
| [Whimsical](../identity/saas-apps/whimsical-provisioning-tutorial) | ● | ● |
| [WiggleDesk](../identity/saas-apps/wiggledesk-provisioning-tutorial) | ● | ● |
| [WireWheel](../identity/saas-apps/wirewheel-tutorial) |  | ● |
| [Wistia](../identity/saas-apps/wistia-tutorial) |  | ● |
| [Wiz SSO](../identity/saas-apps/wiz-sso-tutorial) |  | ● |
| [Wootric](../identity/saas-apps/wootric-tutorial) |  | ● |
| [Workable](../identity/saas-apps/workable-tutorial) |  | ● |
| [Workday to Active Directory](../identity/saas-apps/workday-inbound-tutorial) | ● | ● |
| [Workday to Microsoft Entra ID](../identity/saas-apps/workday-inbound-cloud-only-tutorial) | ● | ● |
| [Workday Writeback](../identity/saas-apps/workday-writeback-tutorial) | ● | ● |
| [Workday](../identity/saas-apps/workday-tutorial) |  | ● |
| [Workgrid](../identity/saas-apps/workgrid-provisioning-tutorial) | ● | ● |
| [Workpath](../identity/saas-apps/workpath-tutorial) |  | ● |
| [Workplace from Meta](../identity/saas-apps/workplace-by-facebook-provisioning-tutorial) | ● | ● |
| [Workshop](../identity/saas-apps/workshop-tutorial) |  | ● |
| [Workteam](../identity/saas-apps/workteam-provisioning-tutorial) | ● | ● |
| [Worthix App](../identity/saas-apps/worthix-app-tutorial) |  | ● |
| [Wrike](../identity/saas-apps/wrike-provisioning-tutorial) | ● | ● |
| [Xledger](../identity/saas-apps/xledger-provisioning-tutorial) | ● |  |
| [XM Fax and XM SendSecure](../identity/saas-apps/xm-fax-and-xm-send-secure-provisioning-tutorial) | ● | ● |
| [Yardi eLearning](../identity/saas-apps/yardielearning-tutorial) |  | ● |
| [YardiOne](../identity/saas-apps/yardione-provisioning-tutorial) | ● | ● |
| [Yellowbox](../identity/saas-apps/yellowbox-provisioning-tutorial) | ● |  |
| [Yonyx Interactive Guides](../identity/saas-apps/yonyx-tutorial) |  | ● |
| [YOU at College](../identity/saas-apps/you-at-college-tutorial) |  | ● |
| [Zapier](../identity/saas-apps/zapier-provisioning-tutorial) | ● |  |
| [Zendesk](../identity/saas-apps/zendesk-provisioning-tutorial) | ● | ● |
| [Zenya](../identity/saas-apps/zenya-provisioning-tutorial) | ● | ● |
| [Zero](../identity/saas-apps/zero-provisioning-tutorial) | ● | ● |
| [Zip](../identity/saas-apps/zip-provisioning-tutorial) | ● | ● |
| [Zoho One](../identity/saas-apps/zoho-one-provisioning-tutorial) | ● | ● |
| [Zoom for Government](../identity/saas-apps/zoom-for-government-tutorial) |  | ● |
| [Zoom](../identity/saas-apps/zoom-provisioning-tutorial) | ● | ● |
| [Zscaler B2B User Portal](../identity/saas-apps/zscaler-b2b-user-portal-tutorial) |  | ● |
| [Zscaler Beta](../identity/saas-apps/zscaler-beta-provisioning-tutorial) | ● | ● |
| [Zscaler Internet Access ZSCloud](../identity/saas-apps/zscaler-internet-access-zscloud-tutorial) |  | ● |
| [Zscaler Internet Access ZSNet](../identity/saas-apps/zscaler-internet-access-zsnet-tutorial) |  | ● |
| [Zscaler Internet Access ZSOne](../identity/saas-apps/zscaler-internet-access-zsone-tutorial) |  | ● |
| [Zscaler Internet Access ZSThree](../identity/saas-apps/zscaler-internet-access-zsthree-tutorial) |  | ● |
| [Zscaler Internet Access ZSTwo](../identity/saas-apps/zscaler-internet-access-zstwo-tutorial) |  | ● |
| [Zscaler One](../identity/saas-apps/zscaler-one-provisioning-tutorial) | ● | ● |
| [Zscaler Private Access](../identity/saas-apps/zscaler-private-access-provisioning-tutorial) | ● | ● |
| [Zscaler Three](../identity/saas-apps/zscaler-three-provisioning-tutorial) | ● | ● |
| [Zscaler Two](../identity/saas-apps/zscaler-two-provisioning-tutorial) | ● | ● |
| [Zscaler ZSCloud](../identity/saas-apps/zscaler-zscloud-provisioning-tutorial) | ● | ● |
| [Zscaler](../identity/saas-apps/zscaler-provisioning-tutorial) | ● | ● |
| [Zylo](../identity/saas-apps/zylo-tutorial) |  | ● |

## Partner driven integrations

There's also a healthy partner ecosystem, further expanding the breadth and depth of integrations available with Microsoft Entra ID Governance. Explore the [partner integrations](../identity/app-provisioning/partner-driven-integrations) available, including connectors for:

- Epic
- Cerner
- IBM RACF
- IBM i (AS/400)
- Aurion People & Payroll