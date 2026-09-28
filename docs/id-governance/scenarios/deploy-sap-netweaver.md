---
layout: Conceptual
title: Deploy SAP NetWeaver AS ABAP 7 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/scenarios/deploy-sap-netweaver
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id-governance
manager: dougeby
description: This article describes how to set up a lab environment with SAP ECC for testing.
ms.topic: install-set-up-deploy
ms.date: 2025-04-09T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: a51b303a-4f6d-9685-b39d-9e59298229a5
document_version_independent_id: a51b303a-4f6d-9685-b39d-9e59298229a5
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/scenarios/deploy-sap-netweaver.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/scenarios/deploy-sap-netweaver
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/scenarios/deploy-sap-netweaver.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/000aaee4-f890-4b0a-bd33-24fb2aefa882
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/57828563-e363-48c1-ac42-c4d23fb7ba52
platformId: 12689eda-1ad5-2590-8c91-657dafa6bd2e
---

# Deploy SAP NetWeaver AS ABAP 7 | Microsoft Learn

This document guides you in setting up a lab environment with SAP ECC for testing.

## Deploying SAP NetWeaver AS ABAP 7.51 on ASE test environment from the SAP Cloud Appliance Library

1. Navigate to the SAP Cloud Appliance Library: https://cal.sap.com/.
2. Create an account for yourself in the SAP CAL and log in to the SAP Cloud Appliance Library. https://calstatic.hana.ondemand.com/res/docEN/042bb15ad2324c3c9b7974dbde389640.html
3. Navigate to the [Appliance Templates - SAP Cloud Appliance Library](https://cal.sap.com/console/tenant_QMOV0I8VZP4H#/applianceTemplates) page
4. Search for the **7.51** appliance template and click the Create Appliance button to create a **SAP NetWeaver AS ABAP 7.51 SP02 on ASE** appliance.

[![Screenshot of SAP Appliance Templates.](media/deploy-sap-netweaver/sap-1.png)](media/deploy-sap-netweaver/sap-1.png#lightbox)

1. Choose Create a new account. Using the **Standard Authorization for Authorization** Type requires the following permissions: The standard authorization includes permissions to create and manage appliances. The roles required by the Microsoft Azure user who grants permissions to SAP Cloud Appliance Library are:

- Option 1: An administrator of the subscription, that is, your user has the role Owner and has access to scope /subscriptions/.
- Option 2: Your Microsoft Azure user has the roles Contributor and User Access Administrator and has access to scope /subscriptions/. You must also have the role of Global Administrator for the Azure Active Directory. Using the **Authorization with Application** for Authorization Type requires you to manually register an application in your Azure AD tenant and grant it the Contributor role to your subscription. You must create an application registration and assign the role Contributor to the corresponding application for your subscription. In this guide, we'll use **Authorization with Application**.

1. Click the Test Connection button. Enter the name of your appliance and choose a master password to access your SAP instance. Click Create to provision resources into Azure AD tenant
2. Download and store the private key needed to access the appliance.

[![Screenshot of private key generation.](media/deploy-sap-netweaver/sap-5.png)](media/deploy-sap-netweaver/sap-5.png#lightbox)

1. SAP CAL will start provisioning and activating resources into your subscription. It may take up to several hours to complete.
2. The next step is to log on into the SAP GUI, get a developer license, and install it to be able to save packages and update the SAP instance, e.g., publish a web service. Once you create the appliance in the SAP Cloud Appliance Library, the SAP system generates a temporary license key that is sufficient to log on to the system. As a first step, before using the system, you need to install a Minisap license as described in the Community Wiki page: How to request and install Minisap license keys.

Installing the Minisap license changes the installation number from INITIAL to DEMOSYSTEM. The developer access key for user DEVELOPER and installation number DEMOSYSTEM is already in the system, and you can start developing in the customer's name range (Z\*, Y\*).

## Exposing a Web Service for the SAP ECC 7.51 Connector

The Web Service Configuration Tool discovers the Web service through WSDL (Web Services Description Language) and retrieves its services, endpoints, and operations (BAPIs) it provides. Services, endpoints, and operations (BAPIs) are used by the Web Service Connector to access the SAP server and manipulate identities with Microsoft Identity Manager (MIM) 2016.

For a web service to be discovered, it must be exposed in SAP ECC 7.51. This article describes the process of exposing the web service from SAP ECC 7.51 workbench.

Log in to SAP ECC 7 and enter the ABAP workbench using Transaction Code SE80. This opens the Object Navigator screen, where you maintain different SAP application components like packages, viewing function groups, BSP programs, etc.

To create a web service utilized by Web Service Configuration Tool, you must first create a package so that all the objects can easily navigate through different systems.

1. From the dropdown, select Package, give the new package a name and press enter. The following screen appears if the object is not available in the system. Click Yes to proceed with the package creation.

[![Screenshot of create pack.](media/deploy-sap-netweaver/sap-7.png)](media/deploy-sap-netweaver/sap-7.png#lightbox)

1. Provide the required details with the **Create Package** screen and click the Create button. You can choose to specify the Application Component. This action restricts the scope of object created only to the application (SAP module, for ex: ABAP, MM, PS, LW, etc.) specified. Note: It's recommended that you don't specify the application component that makes the object global.

[![Screenshot of package creation.](media/deploy-sap-netweaver/sap-8.png)](media/deploy-sap-netweaver/sap-8.png#lightbox)

1. The system prompts for a transport request. Click the button next to Request to generate a new transport request.

[![Screenshot of request prompt.](media/deploy-sap-netweaver/sap-9.png)](media/deploy-sap-netweaver/sap-9.png#lightbox)

1. Create a new local request.

[![Screenshot of Workbench request.](media/deploy-sap-netweaver/sap-10.png)](media/deploy-sap-netweaver/sap-10.png#lightbox)

1. Double click on request name (NPL\*) to select it.

[![Screenshot of NPL.](media/deploy-sap-netweaver/sap-11.png)](media/deploy-sap-netweaver/sap-11.png#lightbox)

1. After workbench request is selected, click the Create button to create a package.

[![Screenshot of request creation.](media/deploy-sap-netweaver/sap-12.png)](media/deploy-sap-netweaver/sap-12.png#lightbox)

1. Once the package is created, under Object Name, to start creating the web service, right-click on the Package name, and select Create -&gt; Enterprise Service

[![Screenshot of object navigator.](media/deploy-sap-netweaver/sap-13.png)](media/deploy-sap-netweaver/sap-13.png#lightbox)

1. The screen to select Object Type is displayed. Select Service Provider as object type and click Continue.

[![Screenshot of object type creation.](media/deploy-sap-netweaver/sap-14.png)](media/deploy-sap-netweaver/sap-14.png#lightbox)

1. On the Kind of Service Provider screen, select Existing ABAP Objects (Inside Out) and press Continue. With inside out you start at the backend with an existing application and enable the service for a particular functionality. It means that you start with the implementation and move out towards the interface.

[![Screenshot of Kind of Service Provider.](media/deploy-sap-netweaver/sap-15.png)](media/deploy-sap-netweaver/sap-15.png#lightbox)

1. Provide the Service Definition name and description for the selected Object Type. Click Continue.

[![Screenshot of service definition.](media/deploy-sap-netweaver/sap-16.png)](media/deploy-sap-netweaver/sap-16.png#lightbox)

1. On the Endpoint Type screen, select Function Group and press Continue. You must choose Function Group since the Web Service configuration tool for MIM requires a single URL for all the selected BAPIs.

[![Screenshot of endpoint type.](media/deploy-sap-netweaver/sap-17.png)](media/deploy-sap-netweaver/sap-17.png#lightbox)

1. On the Endpoint Function Group screen, select the required Function Group name, and press Continue. The function group chosen in the example is already defined and encapsulates the BAPIs related to users.

[![Screenshot of endpoint function group.](media/deploy-sap-netweaver/sap-18.png)](media/deploy-sap-netweaver/sap-18.png#lightbox)

1. On the Function Group screen, select all the required BAPIs and add the BAPIs that aren't included in the function group. Click Continue. In this example, all BAPIs from SU\_USER function groups are selected. Consult your SAP administrator regarding the BAPIs to be used in your project.

[![Screenshot of function group.](media/deploy-sap-netweaver/sap-19.png)](media/deploy-sap-netweaver/sap-19.png#lightbox)

To implement basic user management scenarios, you may want to limit a list of BAPIs published to:

- BAPI\_USER\_GETLIST
- BAPI\_USER\_GETDETAILS
- BAPI\_USER\_CREATE1
- BAPI\_USER\_DELETE
- BAPI\_USER\_CHANGE

1. On the **Configure Service** screen, choose a profile for Security Settings. There are four profiles defined by SAP for selection. Select one profile as per requirement.

- Authentication with Certificates and Transport Guarantee
- Authentication with User and Password, No Transport Guarantee
- Authentication with User and Password and Transport Guarantee
- No Authentication and No Transport Guarantee

1. In this example, we use Authentication with User and Password and no Transport Guarantee (no HTTPs) option. Click Continue.

[![Screenshot of configure service.](media/deploy-sap-netweaver/sap-20.png)](media/deploy-sap-netweaver/sap-20.png#lightbox)

1. On the Transport screen, click on the icon next to Request/Task name, and select your Local Workbench request. Click Continue.

[![Screenshot of transport.](media/deploy-sap-netweaver/sap-21.png)](media/deploy-sap-netweaver/sap-21.png#lightbox)

1. On the **Finish** screen, click Complete button.

[![Screenshot of the finish screen.](media/deploy-sap-netweaver/sap-22.png)](media/deploy-sap-netweaver/sap-22.png#lightbox)

1. After the Web Service is created, you must change the Profile settings of the Service definition. Under Configuration Tab, select Stateful communication properties, and activate Stateful profile. Click the Save button (diskette icon) in the toolbar.

[![Screenshot of profile change.](media/deploy-sap-netweaver/sap-23.png)](media/deploy-sap-netweaver/sap-23.png#lightbox)

1. In the Repository Browser expand the ZSAPCONNECTORWS package, right click on the ZSAPCONNECTORWEBSERVICE service definition, and select Activate.

[![Screenshot of ZSAPCONNECTORWEBSERVICE service definition.](media/deploy-sap-netweaver/sap-24.png)](media/deploy-sap-netweaver/sap-24.png#lightbox)

## Configuring Web Service using SOA Manager

Follow the steps below to configure the Web Service.

1. Open the Transaction SOAMANAGER. Navigate to the Technical Administration tab and click SAP Client Settings.

[![Screenshot of technical administration.](media/deploy-sap-netweaver/sap-25.png)](media/deploy-sap-netweaver/sap-25.png#lightbox)

1. Expand the Web Service Navigator tray and enter a hostname of your SAP server and port number. Click Save.

[![Screenshot of host and port.](media/deploy-sap-netweaver/sap-26.png)](media/deploy-sap-netweaver/sap-26.png#lightbox)

1. Click Back and Navigate to Service Administration tab. Select Web Service Configuration link.

[![Screenshot of web service configuration.](media/deploy-sap-netweaver/sap-27.png)](media/deploy-sap-netweaver/sap-27.png#lightbox)

1. In the Object Name input field, type ZSAPCONNECTORWEBSERVICE and click Search.

[![Screenshot of search results.](media/deploy-sap-netweaver/sap-28.png)](media/deploy-sap-netweaver/sap-28.png#lightbox)

1. Click to select ZSAPCONNECTORWEBSERVICE Service Definition.
2. On the Configurations tab, click Create Service button.

[![Screenshot of configuration create service.](media/deploy-sap-netweaver/sap-29.png)](media/deploy-sap-netweaver/sap-29.png#lightbox)

1. On Configuration of New Binding for Service Definition page, enter the Service Name, the New Binding Name and click Next.

[![Screenshot of binding for service definition.](media/deploy-sap-netweaver/sap-30.png)](media/deploy-sap-netweaver/sap-30.png#lightbox)

1. On the Provider Security page, select the User ID/Password under Transport Channel Authentication, and click Next.

[![Screenshot of binding for service definition configuration.](media/deploy-sap-netweaver/sap-31.png)](media/deploy-sap-netweaver/sap-31.png#lightbox)

1. On the SOAP Protocol page, leave all settings by default, and click Next.

[![Screenshot of SOAP protocol page.](media/deploy-sap-netweaver/sap-32.png)](media/deploy-sap-netweaver/sap-32.png#lightbox)

1. On the Operation Settings page, click Finish.

[![Screenshot of operation settings finish screen.](media/deploy-sap-netweaver/sap-33.png)](media/deploy-sap-netweaver/sap-33.png#lightbox)

1. Once the Service is created click on web page icon to open WSDL generation parameters.

[![Screenshot of WSDL parameters.](media/deploy-sap-netweaver/sap-34.png)](media/deploy-sap-netweaver/sap-34.png#lightbox)

Configure WSDL Flavors as:

- WSP Version: No Policy
- SOAP Version: SOAP 1.1
- SOAP Style: Document
- WSDL Section: AllInOne

1. Click to save WSDL Flavor as: SOAP 1.1. Only

[![Screenshot of save.](media/deploy-sap-netweaver/sap-35.png)](media/deploy-sap-netweaver/sap-35.png#lightbox)

1. Find a WSDL URL for Service under WSDL Generation section and copy that link. Example: `http://vhcalnplci.dummy.nodomain:8000/sap/bc/srt/wsdl/flv\_10002A1011D1/bndg\_url/sap/bc/srt/rfc/sap/zsapconnectorwebservice/001/zsapconnectorws/zsapconnectorws?sapclient\=001`

[![Screenshot of WSDL URL.](media/deploy-sap-netweaver/sap-36.png)](media/deploy-sap-netweaver/sap-36.png#lightbox)

## Activating Web Service for SAP ECC 7.51 Connector

1. Log in to SAP ECC 7 and enter the ABAP workbench using Transaction Code SICF. Mention Hierarchy Type as Service and click Execute button.

[![Screenshot of hierarchy type.](media/deploy-sap-netweaver/sap-37.png)](media/deploy-sap-netweaver/sap-37.png#lightbox)

1. On the **Define Services** page, type ZSAPCONNECTORWS Service Name, and click Apply.
2. Select the ZSAPCONNECTORWS service and choose Activate Service.

[![Screenshot of activate service.](media/deploy-sap-netweaver/sap-38.png)](media/deploy-sap-netweaver/sap-38.png#lightbox)

1. Confirm Activation of ICF Service. Click Yes.

[![Screenshot of confirm activation.](media/deploy-sap-netweaver/sap-39.png)](media/deploy-sap-netweaver/sap-39.png#lightbox)

1. On the **Define Services** page, type WSDL Service Name, and click Apply. Choose to Activate Service for both WSDL services.

[![Screenshot of active services.](media/deploy-sap-netweaver/sap-40.png)](media/deploy-sap-netweaver/sap-40.png#lightbox)

1. Test the web service deployed using your favorite SOAP client tool to ensure that it does return proper data before configuring the Web Services Connector Template

## Connecting to Web Service from MIM or the ECMA2Host machine

1. To avoid publishing your SAP Web Service endpoint to the Internet, set up peering between your SAP demo lab network and your MIM or ECMA2Host machine. This setup allows you to reach your Web Service by its internal IP address.
2. Add the SAP host name and IP address into the hosts file on MIM or ECMA2Host machine.
3. Test opening the WSDL URL on the MIM or ECMA2Host machine from a browser to check connectivity to SAP Web Service.

The next step is to create a [webservice connector template](sap-template) to manage SAP ECC users using this SOAP endpoint and BAPIs published.