---
layout: Conceptual
title: Configure Microsoft Entra on-premises app provisioning to Azure Databricks with Private Link Workspace - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/azure-databricks-with-private-link-workspace-provisioning-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: app-provisioning
manager: pmwongera
description: This article describes how to use the Microsoft Entra provisioning service to provision users into Azure Databricks with Private Link Workspace.
ms.topic: how-to
ms.date: 2024-12-30T00:00:00.0000000Z
locale: en-us
document_id: b4ba76d7-6737-8906-aa12-8249e2f0d319
document_version_independent_id: 34c0ac94-289a-c897-ad40-2c0358410380
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/azure-databricks-with-private-link-workspace-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/azure-databricks-with-private-link-workspace-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/azure-databricks-with-private-link-workspace-provisioning-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/545d40c6-c50c-444b-b422-1c707eeab28e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/b908d601-32e8-445a-b044-a507b5d1689e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 41b9e009-d46c-7d1e-1079-cfda5877c803
---

# Configure Microsoft Entra on-premises app provisioning to Azure Databricks with Private Link Workspace - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra provisioning service supports a [SCIM 2.0](https://techcommunity.microsoft.com/t5/identity-standards-blog/provisioning-with-scim-getting-started/ba-p/880010) client that can be used to automatically provision users into cloud or on-premises applications. This article outlines how you can use the Microsoft Entra provisioning service to provision users into Azure Databricks workspaces with no public access.

[![Diagram that shows SCIM architecture.](media/azure-databricks-with-private-link-workspace-provisioning-tutorial/scim-architecture.png)](media/azure-databricks-with-private-link-workspace-provisioning-tutorial/scim-architecture.png#lightbox)

## Prerequisites

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - One of the following roles: - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator) - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications). with Microsoft Entra ID Governance and Microsoft Entra ID P1 or Premium P2 (or EMS E3 or E5). To find the right license for your requirements, see [Compare generally available features of Microsoft Entra ID](https://www.microsoft.com/security/business/microsoft-entra-pricing).

- Administrator role for installing the agent. This task is a one-time effort and should be an account with at least the [Hybrid Identity Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator) role.
- Administrator role for configuring the application in the cloud [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator), [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator), or [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).
- A computer with at least 3 GB of RAM, to host a provisioning agent. The computer should have Windows Server 2016 or a later version of Windows Server, with connectivity to the target application, and with outbound connectivity to login.microsoftonline.com, other Microsoft Online Services and Azure domains. An example is a Windows Server 2016 virtual machine hosted in Azure IaaS or behind a proxy.

## Download, install, and configure the Microsoft Entra Connect Provisioning Agent Package

If you have already downloaded the provisioning agent and configured it for another on-premises application, then continue reading in the next section.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Cloud sync**.

    [![Screenshot of new UX screen.](media/azure-databricks-with-private-link-workspace-provisioning-tutorial/azure-entra-connect-new-ux.png)](media/azure-databricks-with-private-link-workspace-provisioning-tutorial/azure-entra-connect-new-ux.png#lightbox)
3. On the left, select **Agent**.
4. Select **Download on-premises agent**, and select **Accept terms & download**.

Note

Please use different provisioning agents for on-premises application provisioning and Microsoft Entra Connect cloud sync / HR-driven provisioning. All three scenarios shouldn't be managed on the same agent.

1. Open the provisioning agent installer, agree to the terms of service, and select **next**.
2. When the provisioning agent wizard opens, continue to the **Select Extension** tab and select **On-premises application provisioning** when prompted for the extension you want to enable.
3. The provisioning agent uses the operating system's web browser to display a popup window for you to authenticate to Microsoft Entra ID, and potentially also your organization's identity provider. If you're using Internet Explorer as the browser on Windows Server, then you may need to add Microsoft web sites to your browser's trusted site list to allow JavaScript to run correctly.
4. Provide credentials for a Microsoft Entra administrator when you're prompted to authorize. The user is required to have at least the [Hybrid Identity Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#hybrid-identity-administrator) role.
5. Select **Confirm** to confirm the setting. Once installation is successful, you can select **Exit**, and also close the Provisioning Agent Package installer.

## Provisioning to SCIM-enabled Workspace

Once the agent is installed, no further configuration is necessary on-premises, and all provisioning configurations are then managed.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. Add the **On-premises SCIM app** from the [gallery](../enterprise-apps/add-application-portal).
4. From the left hand menu, navigate to the **Provisioning** option and select **Get started**.
5. Select **Automatic** from the dropdown list and expand the **On-Premises Connectivity** option.
6. Select the agent that you installed from the dropdown list and select **Assign Agent(s)**.
7. Now either wait 10 minutes or restart the **Microsoft Entra Connect Provisioning Agent** before proceeding to the next step & testing the connection.
8. In the **Tenant URL** field, provide the SCIM endpoint URL for your application. The URL is typically unique to each target application and must be resolvable by DNS. An example for a scenario where the agent is installed on the same host as the application is `https://localhost:8585/scim`

    ![Screenshot that shows assigning an agent.](media/azure-databricks-with-private-link-workspace-provisioning-tutorial/on-premises-assign-agents.png)
9. Create an Admin Token in Azure Databricks User Settings Console and enter the same in the **Secret Token** field
10. Select **Test Connection**, and save the credentials. The application SCIM endpoint must be actively listening for inbound provisioning requests, otherwise the test fails. Use the steps [here](../app-provisioning/on-premises-ecma-troubleshoot#troubleshoot-test-connection-issues) if you run into connectivity issues.

Note

If the test connection fails, you see the request made. Please note that while the URL in the test connection error message is truncated, the actual request sent to the application contains the entire URL provided above.

1. Configure any [attribute mappings](../app-provisioning/customize-application-attributes) or [scoping](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts) rules required for your application.
2. Add users to scope by [assigning users and groups](../enterprise-apps/add-application-portal-assign-users) to the application.
3. Test provisioning a few users [on demand](../app-provisioning/provision-on-demand).
4. Add more users into scope by assigning them to your application.
5. Go to the **Provisioning** pane, and select **Start provisioning**.
6. Monitor using the [provisioning logs](../monitoring-health/concept-provisioning-logs).

The following video provides an overview of on-premises provisioning.

## More requirements

- Ensure your [SCIM](https://techcommunity.microsoft.com/t5/identity-standards-blog/provisioning-with-scim-getting-started/ba-p/880010) implementation meets the [Microsoft Entra SCIM requirements](../app-provisioning/use-scim-to-provision-users-and-groups). Microsoft Entra ID offers open-source [reference code](https://github.com/AzureAD/SCIMReferenceCode/wiki) that developers can use to bootstrap their SCIM implementation.
- Support the /schemas endpoint to reduce configuration required.