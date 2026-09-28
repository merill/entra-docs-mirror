---
layout: Conceptual
title: Tutorial to configure Secure Hybrid Access with Microsoft Entra ID and Datawiza - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/datawiza-configure-sha
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: martinco
description: Learn to use Datawiza and Microsoft Entra ID to authenticate users and give them access to on-premises and cloud apps.
ms.topic: tutorial
ms.date: 2024-01-30T00:00:00.0000000Z
ms.reviewer: gasinh
ms.collection: M365-identity-device-management
ms.custom: kr2b-contr-experiment, not-enterprise-apps, sfi-image-nochange
locale: en-us
document_id: e0f2fda0-ce82-4930-64a0-ee3679295f63
document_version_independent_id: c3d057c9-c9a3-bda0-14f8-1749cb04bceb
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/datawiza-configure-sha.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/datawiza-configure-sha
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/datawiza-configure-sha.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: c00eb6d9-cd94-4f1a-dd4d-d8b51fee37e5
---

# Tutorial to configure Secure Hybrid Access with Microsoft Entra ID and Datawiza - Microsoft Entra ID | Microsoft Learn

In this tutorial, learn how to integrate Microsoft Entra ID with [Datawiza](https://www.datawiza.com/) for [hybrid access](../devices/concept-hybrid-join). [Datawiza Access Proxy (DAP)](https://www.datawiza.com) extends Microsoft Entra ID to enable single sign-on (SSO) and provide access controls to protect on-premises and cloud-hosted applications, such as Oracle E-Business Suite, Microsoft IIS, and SAP. With this solution, enterprises can transition from legacy web access managers (WAMs), such as Symantec SiteMinder, NetIQ, Oracle, and IBM, to Microsoft Entra ID without rewriting applications. Enterprises can use Datawiza as a no-code, or low-code, solution to integrate new applications to Microsoft Entra ID. This approach enables enterprises to implement their Zero Trust strategy while saving engineering time and reducing costs.

Learn more: [Zero Trust security](/en-us/azure/security/fundamentals/zero-trust)

## Datawiza with Microsoft Entra authentication Architecture

Datawiza integration includes the following components:

- **[Microsoft Entra ID](../../fundamentals/what-is-entra)** - Identity and access management service that helps users sign in and access external and internal resources
- **Datawiza Access Proxy (DAP)** - This service transparently passes identity information to applications through HTTP headers
- **Datawiza Cloud Management Console (DCMC)** - UI and RESTful APIs for administrators to manage the DAP configuration and access control policies

The following diagram illustrates the authentication architecture with Datawiza in a hybrid environment.

![Architecture diagram of the authentication process for user access to an on-premises application.](media/datawiza-configure-sha/datawiza-architecture-diagram.png)

1. The user requests access to the on-premises or cloud-hosted application. DAP proxies the request to the application.
2. DAP checks user authentication state. If there's no session token, or the session token is invalid, DAP sends the user request to Microsoft Entra ID for authentication.
3. Microsoft Entra ID sends the user request to the endpoint specified during DAP registration in the Microsoft Entra tenant.
4. DAP evaluates policies and attribute values to be included in HTTP headers forwarded to the application. DAP might call out to the identity provider to retrieve the information to set the header values correctly. DAP sets the header values and sends the request to the application.
5. The user is authenticated and is granted access.

## Prerequisites

To get started, you need:

- An Azure subscription
    - If you don't have one, you can get an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)
- A [Microsoft Entra tenant](../../fundamentals/create-new-tenant) linked to the Azure subscription
- [Docker](https://docs.docker.com/get-docker/) and [docker-compose](https://docs.docker.com/compose/install/)are required to run DAP
    - Your applications can run on platforms, such as a virtual machine (VM) or bare metal
- An on-premises or cloud-hosted application to transition from a legacy identity system to Microsoft Entra ID
    - In this example, DAP is deployed on the same server as the application
    - The application runs on localhost: 3001. DAP proxies traffic to the application via localhost: 9772
    - The traffic to the application reaches DAP, and is proxied to the application

## Configure Datawiza Cloud Management Console

1. Sign in to [Datawiza Cloud Management Console (DCMC)](https://console.datawiza.com/).
2. Create an application on DCMC and generate a key pair for the app: `PROVISIONING_KEY` and `PROVISIONING_SECRET`.
3. To create the app and generate the key pair, follow the instructions in [Datawiza Cloud Management Console](https://docs.datawiza.com/step-by-step/step2.html).
4. Register your application in Microsoft Entra ID with [One Click Integration With Microsoft Entra ID](https://docs.datawiza.com/tutorial/web-app-azure-one-click.html).

    ![Screenshot of the Automatic Generator feature on the Configure IdP dialog.](media/datawiza-configure-sha/configure-idp.png)
5. To use a web application, manually populate form fields: **Tenant ID**, **Client ID**, and **Client Secret**.

    Learn more: To create a web application and obtain values, go to docs.datawiza.com for [Microsoft Entra ID](https://docs.datawiza.com/idp/azure.html) documentation.

    ![Screenshot of the Configure IdP dialog with the Automatic Generator turned off.](media/datawiza-configure-sha/use-form.png)
6. Run DAP using either Docker or Kubernetes. The docker image is needed to create a sample header-based application.

- For Kubernetes, see [Deploy Datawiza Access Proxy with a Web App using Kubernetes](https://docs.datawiza.com/tutorial/web-app-AKS.html)
- For Docker, see [Deploy Datawiza Access Proxy With Your App](https://docs.datawiza.com/step-by-step/step3.html)
    - You can use the following sample docker image docker-compose.yml file:

```yaml
services:
   datawiza-access-broker:
   image: registry.gitlab.com/datawiza/access-broker
   container_name: datawiza-access-broker
   restart: always
   ports:
   - "9772:9772"
   environment:
   PROVISIONING_KEY: #############################################
   PROVISIONING_SECRET: ##############################################
   
   header-based-app:
   image: registry.gitlab.com/datawiza/header-based-app
   restart: always
ports:
- "3001:3001"
```

1. Sign in to the container registry.
2. Download the DAP images and the header-based application in this [Important Step](https://docs.datawiza.com/step-by-step/step3.html#important-step).
3. Run the following command: `docker-compose -f docker-compose.yml up`.
4. The header-based application has SSO enabled with Microsoft Entra ID.
5. In a browser, go to `http://localhost:9772/`.
6. A Microsoft Entra sign-in page appears.
7. Pass user attributes to the header-based application. DAP gets user attributes from Microsoft Entra ID and passes attributes to the application via a header or cookie.
8. To pass user attributes such as email address, first name, and last name to the header-based application, see [Pass User Attributes](https://docs.datawiza.com/step-by-step/step4.html).
9. To confirm configured user attributes, observe a green check mark next to each attribute.

![Screenshot of the home page with host, email, firstname, and lastname attributes.](media/datawiza-configure-sha/datawiza-application-home-page.png)

## Test the flow

1. Go to the application URL.
2. DAP redirects you to the Microsoft Entra sign-in page.
3. After authentication, you're redirected to DAP.
4. DAP evaluates policies, calculates headers, and sends you to the application.
5. The requested application appears.