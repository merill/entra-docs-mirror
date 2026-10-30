---
layout: Conceptual
title: Configure HiBob to Active Directory hybrid user provisioning - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/hibob-to-active-directory-user-provisioning-tutorial
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
description: Learn how to configure the Microsoft Active Directory (Hybrid) integration in HiBob to provision and update users in on-premises Active Directory.
ms.topic: how-to
ms.date: 2026-09-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7a34863b-467b-f5d2-9148-8c24105f7987
document_version_independent_id: 7a34863b-467b-f5d2-9148-8c24105f7987
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/hibob-to-active-directory-user-provisioning-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/hibob-to-active-directory-user-provisioning-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/hibob-to-active-directory-user-provisioning-tutorial.md
platformId: 8d6df3be-65f3-ec78-5960-ef8c7a4c3f99
---

# Configure HiBob to Active Directory hybrid user provisioning - Microsoft Entra ID | Microsoft Learn

This article describes how to configure HiBob (Bob) to on-premises Active Directory hybrid user provisioning.

The integration is intended for organizations where on-premises Active Directory is connected to Microsoft Entra ID. HiBob acts as the source for employee lifecycle data, while Microsoft Entra continues to manage identities and access. The integration helps automate user lifecycle management, reduce manual administration, and keep HR and identity data synchronized.

For detailed product-specific guidance, select the **Help docs** link from the [Microsoft Active Directory (Hybrid) integration in the Bob Marketplace](https://www.hibob.com/marketplace/adhybrid/overview).

## Prerequisites

Before you begin, make sure that you have:

- A HiBob tenant and permission to install and configure Bob Marketplace integrations.
- A Microsoft Entra tenant connected to the target Active Directory environment.
- A [Microsoft Entra ID P1, Microsoft Entra ID P2, or Microsoft Entra ID Governance license](../../id-governance/licensing-fundamentals#api-driven-provisioning). You need enough licenses for every identity that the integration sources through API-driven provisioning.
- The [Microsoft Entra provisioning agent](../hybrid/cloud-sync/how-to-install) installed and configured for the target Active Directory domain.
- The Active Directory domain name and organizational unit (OU) in which HiBob should create or update users.
- A Microsoft Entra account with the [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator)or Global Administrator role to grant consent to the following API permissions:
    - Application.ReadWrite.OwnedBy
    - SynchronizationData-User.Upload.OwnedBy
    - ProvisioningLog.Read.All
- A test employee record that you can use to validate attribute mappings and provisioning behavior.

The following sections provide the high-level steps for configuring the integration in the Bob Marketplace.

Note

The steps and interface labels in this article describe the configuration experience in the HiBob administration portal. The experience might change as the product is updated.

## How the integration works

The HiBob integration leverages [Microsoft Entra API-driven provisioning](../app-provisioning/inbound-provisioning-api-concepts) to provision users to Active Directory. HiBob applies the mappings configured in the integration to create a bulk SCIM payload and sends the payload to the API endpoint of the provisioning job. Microsoft Entra processes the payload by using the provisioning job's scope and attribute mappings, and then the Microsoft Entra provisioning agent writes the changes to Active Directory.

[![Sequence diagram showing end-to-end flow from HiBob to Active Directory.](media/hibob-to-active-directory-user-provisioning-tutorial/hibob-to-active-directory-flow.png)](media/hibob-to-active-directory-user-provisioning-tutorial/hibob-to-active-directory-flow.png#lightbox)

1. An HR administrator creates an employee profile or updates employee data in HiBob.
2. HiBob applies the attribute mappings configured in the integration and creates a SCIM payload that represents the employee change.
3. HiBob sends the SCIM payload to the API endpoint for the Microsoft Entra API-driven provisioning job.
4. The provisioning job determines whether the employee is in scope and maps the SCIM attributes to the configured Active Directory attributes.
5. The provisioning job sends the create or update operation to the Microsoft Entra provisioning agent.
6. The provisioning agent creates or updates the user account in the configured Active Directory domain and OU.
7. Active Directory returns the result to the provisioning agent.
8. The provisioning agent reports the operation status to the Microsoft Entra provisioning job, where administrators can review it in the provisioning logs.
9. HiBob queries the Microsoft Entra provisioning logs for the status of the submitted request.
10. Microsoft Entra returns the provisioning status, which HiBob makes available in the integration's synchronization records.

## Configuration steps

### Step 1 - Establish the connection

In this step, a HiBob administrator adds the integration, authorizes access to the Microsoft tenant, and specifies the target Active Directory environment.

1. Sign in to HiBob as an administrator.
2. Go to **Marketplace**.
3. Open the **Identity and Access** category, or use the search box to find **Microsoft Active Directory Hybrid**.
4. Open the integration and review its overview and requirements.
5. Select **Connect**, and then select **Add connection**.
6. Enter a descriptive name for the connection.
7. Select **Authorize**.
8. Sign in with a Microsoft Entra account that has the Privileged Role Administrator or Global Administrator role.
9. The *HiBob Hybrid AD Integration*App will request the following permissions. Review and grant the requested permissions.
    - Application.ReadWrite.OwnedBy
    - SynchronizationData-User.Upload.OwnedBy
    - ProvisioningLog.Read.All
10. Wait for HiBob to confirm that the Microsoft tenant connection is established.
11. Enter the target Active Directory domain name.
12. Enter the OU that should contain users managed by the integration.
13. Confirm that the Microsoft Entra provisioning agent is installed and connected to the target Active Directory environment.
14. Select **Next**.

The authorization process securely connects HiBob to the Microsoft tenant. Establishing the connection can take several minutes.

### Step 2 - Configure provisioning scope and attribute mappings

In this step, the administrator defines which employees are in scope and maps HiBob fields to Active Directory attributes. HiBob uses these mappings to transform employee data into the SCIM payload that it sends to the API endpoint for the Microsoft Entra API-driven provisioning job.

1. On the provisioning settings page, configure **Who to provision**.
2. Review the default mappings from HiBob employee fields to Active Directory attributes.
3. For each mapping, verify the HiBob source field and the corresponding Active Directory target attribute.
4. Add mappings for any additional employee data that should flow to Active Directory.

    Note

    To use [Entra ID Governance Lifecycle Workflows](../../id-governance/what-are-lifecycle-workflows), send the `Start date` and `End date`/`Termination date` information to Active Directory and [through Entra Connect Sync or Cloud Sync](../../id-governance/how-to-lifecycle-workflow-sync-attributes) to Microsoft Entra ID.
5. Change or remove optional mappings that aren't required by your organization.
6. Review the mappings that HiBob identifies as required for Active Directory synchronization. Required mappings can't be removed, but the source or target might be configurable.
7. Select **Next**.

Caution

Changing an identifier or other required mapping can affect user matching and updates. Test mapping changes with a limited set of users before enabling broad provisioning.

### Step 3 - Configure synchronization and approval rules

In this step, the administrator decides how automatically HiBob should send employee lifecycle changes to Active Directory.

HiBob provides the following synchronization approaches:

- **Automatic synchronization** - Sends eligible changes directly to Active Directory. Use this option when the organization wants faster processing with minimal administrator involvement.
- **Approval-required synchronization** - Places selected changes in an approval queue before they're sent to Active Directory. Use this option when the organization requires more control over sensitive identity changes.

To configure approval-required synchronization:

1. Choose whether approval is required when a new employee account is created.
2. Select the employee fields whose updates require approval, such as department or another sensitive business attribute.
3. Configure the users or groups that should receive approval notifications.
4. Review the settings, and then save the connection.

Routine updates can remain automated, while higher-risk changes can require review.

### Step 4 - Test user provisioning

After the connection is saved, test the provisioning flow with a test employee before enabling the integration for a broader population.

1. In HiBob, open the test employee record.
2. Create or update an employee value that is included in the attribute mappings.
3. If you're testing approval-required synchronization, update a field that requires approval. For example, change the employee's department and specify the effective date.
4. Return to **Marketplace** and locate the Microsoft Active Directory Hybrid integration.
5. Select **Manage**, and then open the connection that you created.
6. If approval is required, open the approval queue.
7. Review the employee, trigger type, changed field, previous value, new value, and effective date.
8. Select **Approve** to send the change to Active Directory, or select **Decline** to reject it.

Approvers can process changes individually or, when available, approve or decline changes in bulk.

After approving a change, confirm that the user was created or updated in the expected Active Directory domain and OU with the expected attribute values.

### Step 5 - Monitor provisioning

The connection management page provides a central location for reviewing configuration and provisioning activity.

Use the connection page to:

- Review the provisioning settings and attribute mappings configured in the wizard.
- Trigger a manual synchronization when needed.
- Review pending items in the approval queue.
- Review the audit history to identify who approved or declined a change and what action was taken.
- Review synchronization records to determine whether each operation succeeded or failed.
- Filter or export records when those options are available.

If a provisioning operation fails, review the synchronization record for the affected employee. Verify the connection authorization, provisioning-agent status, target domain and OU, provisioning scope, and attribute mappings.

## Troubleshooting

### Connectivity issues between HiBob, Microsoft Entra tenant and Active Directory

Take the following actions:

- Confirm that the Microsoft Entra account used for authorization has the required permissions.
- Retry authorization and complete any consent prompts.
- Confirm that the Microsoft Entra tenant is associated with the target hybrid Active Directory environment.

### Users aren't created or updated

In the HiBob administration portal:

- Verify the Active Directory domain and OU settings.
- Confirm that the employee is included in the **Who to provision** scope.
- Review required and custom attribute mappings.
- Check the synchronization records for a failure entry.

If the HiBob synchronization records don't clearly identify the cause of the failure, review the Microsoft Entra provisioning logs:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Find and select the **HiBob to Active Directory user provisioning** app.
4. Confirm that the Microsoft Entra provisioning agent is running and connected.
5. Select **Provisioning logs**.
6. Find the failed provisioning operation and review its status information and error details.

### Custom Active Directory schema attributes don't appear in the mapping list

Let's say you have a custom attribute in your Active Directory and it is not showing up in the mapping drop-down, then add the custom attribute to the target attribute schema of the provisioning app before you configure the mapping in HiBob:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Find and select the **HiBob to Active Directory user provisioning** app.
4. Select **Provisioning**, and then select **Edit provisioning**.
5. Expand **Mappings**, and then select the attribute mapping.
6. Select **Edit Active Directory attribute list**.
7. Add the custom Active Directory attribute to the list, and then save your changes.
8. Return to the HiBob configuration screen and confirm that the custom attribute appears in the mapping list.

### A change remains pending

In the HiBob administration portal:

1. Open the integration's approval queue.
2. Confirm that the changed field is configured to require approval.
3. Approve or decline the request.
4. Verify that approval notifications are sent to the intended reviewers.