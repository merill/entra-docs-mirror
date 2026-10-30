---
layout: Conceptual
title: Microsoft Entra Global Secure Access operations guide - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/overview-operations
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Overview and navigation for the post-deployment operations guide suite for Microsoft Entra Global Secure Access.
ms.topic: overview
ms.date: 2026-05-04T00:00:00.0000000Z
ms.reviewer: jricketts
ai-usage: ai-assisted
locale: en-us
document_id: d3ab3440-5e6e-0eed-8674-eb419aa134b1
document_version_independent_id: d3ab3440-5e6e-0eed-8674-eb419aa134b1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/overview-operations.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/overview-operations
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/overview-operations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 504ecf37-46ff-e632-ef7d-d09f64334143
---

# Microsoft Entra Global Secure Access operations guide - Global Secure Access | Microsoft Learn

This operations guide suite provides prescriptive, post-deployment procedures for running Microsoft Entra Global Secure Access in an enterprise environment. The guides cover day-to-day alerting, health checks, integration, automation, and metrics—focusing on operational tasks that keep the service reliable, secure, and performant.

## Who this guide is for

- **IT administrators and network security engineers** responsible for Global Secure Access configuration and maintenance
- **Platform operations and monitoring engineers** who manage health checks, automation, and dashboards
- **Security leadership** reviewing operational metrics and service value

This guide assumes Global Secure Access is already deployed and configured. For deployment and initial setup, see the [Global Secure Access deployment guide](/en-us/entra/architecture/gsa-deployment-guide-intro). For broader identity-layer security investigations and incident response, see the [Microsoft Entra Security Operations Guide](https://aka.ms/AzureADSecOps).

## Overview

The operational practices in these guides align with the Information Technology Infrastructure Library (ITIL) service management processes and the National Institute of Standards and Technology (NIST) Cybersecurity Framework. Rather than teaching these frameworks, the guides apply their principles directly: alert-first monitoring (NIST Detect), structured change management (ITIL), configuration backup and failover testing (NIST Recover), and continuous improvement through metrics-driven reviews.

The guide suite groups content by Global Secure Access capability, plus a shared common guide for cross-cutting topics.

### Shared operations

| Guide | What it covers |
| --- | --- |
| [Common operations](how-to-operations-common) | RACI matrix (responsible, accountable, consulted, informed) for roles and responsibilities, change management process, metrics and reporting framework, continuous improvement |
| [Security operations for network access](how-to-security-operations) | Security monitoring, detection patterns, Sentinel analytics rules, and cross-signal investigation guidance for Global Secure Access |
| [PowerShell samples](powershell-samples) | Automation samples for operations monitoring, configuration backup compliance, role assignment reviews, alert noise analysis, and recovery |

### Capability-specific operations

Each capability guide follows a consistent structure: Alerting and monitoring, Maintenance and health checks, Integration and automation, Operational metrics, and Troubleshooting quick reference.

| Guide | What it covers |
| --- | --- |
| [Private Access operations](how-to-operate-private-access) | Connector health, application segment management, ZTNA-specific alerting, Graph API automation for connector and app management |
| [Internet Access operations](how-to-operate-internet-access) | Web filtering policy management, Transport Layer Security (TLS) inspection, URL categorization, threat blocking metrics |
| [Remote Networks operations](how-to-operate-remote-networks) | GRE/IPsec tunnel monitoring, branch site capacity management, customer-premises equipment (CPE) device health, tunnel failover testing |
| [Microsoft Traffic operations](how-to-operate-microsoft-traffic) | Microsoft 365 traffic profile management, compliant network enforcement, Microsoft 365 endpoint coverage, service performance monitoring |

### Templates and checklists

| Template | Purpose |
| --- | --- |
| [Daily health check](reference-daily-health-check) | Consolidated daily checklist covering all Global Secure Access capabilities |
| [Private Access health check](reference-private-access-health-check) | Capability-specific checklist for Private Access connectors and application segments |
| [Change request template](reference-change-request-template) | Structured template for Global Secure Access configuration change requests |
| [Communication plan template](reference-communication-plan) | Template for communicating planned changes to stakeholders |

## Getting started with operations

If you completed deployment, follow this sequence:

1. **Establish your team**—Assign roles using the [RACI matrix](how-to-operations-common#raci-matrix). Ensure at least two people cover each role.
2. **Configure alerting**—Set up the critical alerts listed in the [Security operations for network access](how-to-security-operations) guide and each capability guide: [Private Access](how-to-operate-private-access#alerting-and-monitoring), [Internet Access](how-to-operate-internet-access#alerting-and-monitoring), [Remote Networks](how-to-operate-remote-networks#alerting-and-monitoring), and [Microsoft Traffic](how-to-operate-microsoft-traffic#alerting-and-monitoring). Don't rely on dashboards for issue detection.
3. **Establish baselines**—Collect a 30-day performance baseline for traffic volume, latency, and usage. Calibrate alert thresholds against this baseline. Each capability guide includes Kusto Query Language (KQL) queries for baseline establishment.
4. **Set up automation**—Start with configuration backups and alert notifications. Expand to the full automation playbook list over time.
5. **Schedule recurring checks**—Implement the daily, weekly, and monthly checklists from each capability guide.
6. **Begin reporting**—Start with weekly operational team reports. Add monthly management reports after the first month.