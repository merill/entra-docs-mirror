---
layout: Conceptual
title: Resources for migrating apps to Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/migration-resources
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Resources to help you migrate application access and authentication to Microsoft Entra ID.
ms.topic: how-to
ms.date: 2024-05-27T00:00:00.0000000Z
ms.reviewer: gasinh
ms.custom: not-enterprise-apps
locale: en-us
document_id: becd4be8-7585-a953-5bda-07e4f219665e
document_version_independent_id: 677bec1d-3372-5d2d-dac8-d141acaea606
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/migration-resources.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/migration-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/migration-resources.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: 55f2c5db-47f7-06d8-0368-5a392e1086f4
---

# Resources for migrating apps to Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

Resources to help you migrate application access and authentication to Microsoft Entra ID.

| Resource | Description |
| --- | --- |
| [Migrating your apps to Microsoft Entra ID](https://aka.ms/migrateapps/whitepaper) | This article is an introduction to a series of articles that describe how to plan for migration in four clearly-outlined phases: discovery, classification, migration, and ongoing management. You're guided through how to think about the process and break down your project into easy-to-consume pieces. Throughout the series are links to important resources that help you along the way. |
| [Developer tutorial: AD FS to Microsoft Entra application migration playbook for developers](https://aka.ms/adfsplaybook) | This set of ASP.NET code samples and accompanying tutorials help you learn how to safely and securely migrate your applications integrated with Active Directory Federation Services (AD FS) to Microsoft Entra ID. This tutorial is focused towards developers who not only need to learn how to configure apps on both AD FS and Microsoft Entra ID, but also become aware and confident of changes their code base will require in this process. |
| [Tool: Active Directory Federation Services Migration Readiness Script](https://aka.ms/migrateapps/adfstools) | This is a script you can run on your on-premises Active Directory Federation Services (AD FS) server to determine the readiness of apps for migration to Microsoft Entra ID. |
| [Deployment plan: Migrating from AD FS to password hash sync](https://aka.ms/ADFSTOPHSDPDownload) | With password hash synchronization, hashes of user passwords are synchronized from on-premises Active Directory to Microsoft Entra ID. This allows Microsoft Entra ID to authenticate users without interacting with the on-premises Active Directory. |
| [Deployment plan: Migrating from AD FS to pass-through authentication](https://aka.ms/ADFSTOPTADPDownload) | Microsoft Entra pass-through authentication helps users sign in to both on-premises and cloud-based applications by using the same password. This feature provides your users with a better experience since they have one less password to remember. It also reduces IT help desk costs because users are less likely to forget how to sign in when they only need to remember one password. When people sign in using Microsoft Entra ID, this feature validates users' passwords directly against your on-premises Active Directory. |
| [Deployment plan: Enabling single sign-on to a SaaS app with Microsoft Entra ID](https://aka.ms/SSODPDownload) | Single sign-on (SSO) helps you access all the apps and resources you need to do business, while signing in only once, using a single user account. For example, after a user has signed in, the user can move from Microsoft Office, to SalesForce, to Box without authenticating (for example, typing a password) a second time. |
| [Deployment plan: Extending apps to Microsoft Entra ID with Application Proxy](../app-proxy/conceptual-deployment-plan) | Providing access from employee laptops and other devices to on-premises applications has traditionally involved virtual private networks (VPNs) or demilitarized zones (DMZs). Not only are these solutions complex and hard to make secure, but they're costly to set up and manage. Microsoft Entra application proxy makes it easier to access on-premises applications. |
| [Other deployment plans](../../architecture/deployment-plans) | Find more deployment plans for deploying features such as Microsoft Entra multifactor authentication, Conditional Access, user provisioning, seamless SSO, self-service password reset, and more! |
| [Migrating apps from Symantec SiteMinder to Microsoft Entra ID](https://azure.microsoft.com/mediahandler/files/resourcefiles/migrating-applications-from-symantec-siteminder-to-azure-active-directory/Migrating-applications-from-Symantec-SiteMinder-to-Azure-Active-Directory.pdf) | Get step by step guidance on application migration and integration options with an example that walks you through migrating applications from Symantec SiteMinder to Microsoft Entra ID. |
| [Identity governance for applications](../../id-governance/identity-governance-applications-prepare) | This guide outlines what you need to do if you're migrating identity governance for an application from a previous identity governance technology, to connect Microsoft Entra ID to that application. |
| [Active Directory Federation Services (AD FS) decommission guide](/en-us/windows-server/identity/ad-fs/decommission/adfs-decommission-guide) | This guide explains the prerequisites for decommissioning, including migrating user authentication and applications to Microsoft Entra ID. It also provides step-by-step instructions for decommissioning the AD FS servers, including removing load balancer entries, uninstalling WAP and AD FS servers, and deleting SSL certificates and databases. |
| [Phases of migrating apps from ADFS to Microsoft Entra ID](migrate-adfs-apps-phases-overview) | This set of articles illustrates the five phases of a typical migration of an application from ADFS to Microsoft Entra ID. |
| [Migrate identity management scenarios from SAP IDM to Microsoft Entra](../app-provisioning/migrate-from-sap-idm) | If you've been using SAP Identity Management (IDM), then you can migrate identity management scenarios from SAP IDM to Microsoft Entra. |
| [Migrating Identity and Access Management scenarios to Microsoft Entra from Microsoft Identity Manager](/en-us/microsoft-identity-manager/migrate-entra-id) | This document provides guidance on migration options and approaches for moving Identity and Access Management (IAM) scenarios from Microsoft Identity Manager to Microsoft Entra cloud-hosted services. |