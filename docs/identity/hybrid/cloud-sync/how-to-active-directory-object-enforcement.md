---
layout: Conceptual
title: Microsoft Entra AD object enforcement (Preview) - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-active-directory-object-enforcement
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: dhanyahk
ms.author: dhanyahk
ms.service: entra-id
manager: mwongerapk
description: Configure the AD enforcement preview so that synced Active Directory objects can only be modified by the Microsoft Entra Cloud Sync provisioning service.
ms.subservice: hybrid-cloud-sync
ms.topic: how-to
ms.custom: msecd-doc-authoring-1023
ms.date: 2026-08-11T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5bdb42f3-a379-6c8a-59e2-40a69350a5ad
document_version_independent_id: 5bdb42f3-a379-6c8a-59e2-40a69350a5ad
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-active-directory-object-enforcement.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-active-directory-object-enforcement
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-active-directory-object-enforcement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
platformId: ae9c555c-4bb9-6b85-d2e6-74511cf971cc
---

# Microsoft Entra AD object enforcement (Preview) - Microsoft Entra ID | Microsoft Learn

Microsoft Entra Cloud Sync can provision cloud users and groups to on-premises Active Directory (AD). AD object enforcement lets you protect specific provisioned users and groups so that modifications can only be performed through the Microsoft Entra provisioning service. This article explains how to enable the enforcement engine, configure its shared policy, and mark users and groups for enforcement.

Before you begin, make sure your domain controllers, provisioning agent, AD schema, and administrative access meet the prerequisites.

## Prerequisites

Make sure the following prerequisites are already in place before you start the configuration steps.

| Prerequisite | Details |
| --- | --- |
| Microsoft Entra license | A Microsoft Entra tenant with the licenses required for provisioning users and groups to AD. See [License requirements](overview-provision-entra-id-to-active-directory#license-requirements). |
| AD role | Domain Admin, to run the PowerShell script that installs the policy and to manage the policy object. Use this privilege only while installing or changing the policy. Remove or deactivate the privileged access when you're finished, following your organization's just-in-time privileged-access process. |
| Supported domain controller OS on every writable DC | Windows Server 2022 or Windows Server 2025. Because enforcement must be enabled on every writable domain controller, confirm that all of them can run a supported OS. If any writable domain controller can't be brought to a supported OS, it can't participate, and enforcement can't be configured for the domain. |
| Provisioning agent host | A domain-joined server that meets the [Cloud Sync agent requirements](how-to-prerequisites#cloud-provisioning-agent-requirements). We recommend Windows Server 2025 or Windows Server 2022. The agent doesn't have to run on a domain controller. |
| No domain functional level requirement | Enforcement doesn't require raising the domain or forest functional level. It's an operational requirement to enable every writable domain controller, not a functional-level setting. |
| Schema | Uses the existing `msDS-ObjectSoa` attribute, present since the Windows Server 2016 schema. No schema extension is required. |
| Domain controller inventory | An inventory of all writable domain controllers in the domain. To enumerate them, run `Get-ADDomainController -Filter * | Where-Object { -not $_.IsReadOnly }` or see [View the list of domain controllers](/en-us/powershell/module/activedirectory/get-addomaincontroller). |
| Provisioning to AD configured | A Microsoft Entra ID to AD configuration that provisions the users or groups you want to enforce. See [Tutorial: Govern access to an on-premises app from Microsoft Entra ID](tutorial-users-groups-provisioning-walkthrough). |

For the full list of provisioning agent prerequisites, see [Prerequisites for provisioning from Microsoft Entra ID to Active Directory](how-to-prerequisites-provision-entra-to-active-directory).

Important

AD user and group enforcement is in **PREVIEW**. The preview spans two parts that you configure together: the **Active Directory enforcement engine** on your domain controllers and the **Microsoft Entra Cloud Sync** configuration that marks users and groups for enforcement. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features in preview.

## How AD object enforcement works

Enforcement is evaluated by Active Directory **at the point of a Lightweight Directory Access Protocol (LDAP) write, on whichever domain controller processes that write**. When a change targets a user or group that's marked for enforcement, the domain controller checks whether the calling identity is authorized by the policy. If it isn't, the change is blocked (Enforced mode) or logged (Audit mode) before any *drift* between the object's state in Microsoft Entra and its state in AD can occur.

Two pieces work together:

- A domain-wide **source of authority (SOA) policy** that lists the security identifiers (SIDs) authorized to change enforced objects, and the current mode (Enforced or Audit). The policy is stored in a `SOA-Policies` container created under `CN=System,DC=<your domain>`.
- A per-object marker, the [`msDS-ObjectSoa`](/en-us/openspecs/windows_protocols/ms-ada2/426118f6-06ea-4ea0-adbe-03556bb58c9c) attribute, that you set through Cloud Sync. The policy applies only to objects that have this attribute set.

| Mode | Behavior |
| --- | --- |
| **Enforced** | Only SIDs allowed by the policy can change enforced users and groups. The policy blocks LDAP modify and modify DN operations and restores from the Recycle Bin. The policy still permits LDAP Add operations, even when the add contains the `msDS-ObjectSoa` attribute. Delete operations are permitted during public preview. |
| **Audit** | Changes are allowed per your existing AD role-based access control (RBAC). The policy writes an event to the **Directory Service** log when an unauthorized identity changes an enforced object. Use Audit mode to discover out-of-band changes before you switch to Enforced. To see the events, enable Security Diagnostics logging (see View enforcement events in the event log). |

AD object enforcement is **additive** to your existing AD RBAC model. It places an additional restriction on top of your current access control without granting any additional access.

Warning

**Enforcement applies only to users and groups you mark, and protection for a marked object is complete only when every writable domain controller is enabled.** Enforcement isn't a single domain-wide switch: it takes effect only for objects that have the `msDS-ObjectSoa` attribute set. For each marked object, the policy is honored only on domain controllers that run a supported operating system, have the update installed, and have the feature enabled. If even one writable domain controller isn't enabled, an unauthorized change directed at that domain controller succeeds and bypasses the control for that object. Plan to update and enable **all** writable domain controllers before you rely on enforcement.

## Plan your rollout

The high-level configuration is:

1. Install the update and enable the feature on every writable domain controller.
2. Install the policy in Enforced or Audit mode.
3. Mark the users and groups you want to protect.

## Update and enable every writable domain controller

Bring the enforcement engine online across the domain. Repeat the update and enablement on **every writable domain controller.**

On each writable domain controller, install the latest cumulative Windows Server update, then deploy the matching Group Policy (KIR) package to turn the feature on. The minimum version of `C:\Windows\System32\ntdsai.dll` is **10.0.20348.5257** for Windows Server 2022 and **10.0.26100.32995** for Windows Server 2025. To verify the installed version, run `(Get-Item C:\Windows\System32\ntdsai.dll).VersionInfo.FileVersion` on the domain controller.

1. On every writable domain controller, install the latest cumulative Windows Server update.
2. Restart the domain controller if the update prompts you to.
3. Enable the feature on all writable domain controllers by deploying the matching Group Policy package, which uses a Known Issue Rollback (KIR) enablement model. For step-by-step guidance on enabling the feature across all writable domain controllers, see [Use Group Policy to deploy a Known Issue Rollback](/en-us/troubleshoot/windows-client/group-policy/use-group-policy-to-deploy-known-issue-rollback). Download the matching package:

    - Windows Server 2022: [Group Policy package for Windows Server 2022](https://aka.ms/ADEnforcementGPMSI2022)
    - Windows Server 2025: [Group Policy package for Windows Server 2025](https://aka.ms/ADEnforcementGPMSI2025)
4. Restart each domain controller after enablement.

After the primary domain controller emulator (PDCe) is updated and enabled, it automatically creates the `SOA-Policies` container under `CN=System,DC=<your domain>`, which then replicates to all domain controllers. Confirm that the container exists (substitute your actual domain name). It can take a few minutes to appear and replicate.

## Install the policy in Enforced or Audit mode

The `Set-CloudSyncSOAPolicy.ps1` script creates the `Cloud` policy object inside the `SOA-Policies` container and adds the provisioning agent's group managed service account (GMSA) SID to the policy's allow list. If the `SOA-Policies` container doesn't exist yet, the script creates it.

The script reads the agent's GMSA from the locally installed provisioning agent service. **Run it on the machine where the Cloud Sync provisioning agent is installed.**

1. Install the Microsoft Entra Cloud Sync provisioning agent. For installation instructions, see [Install the Microsoft Entra Cloud Sync provisioning agent](how-to-install).
2. Sign in to the machine where the provisioning agent is installed.
3. Download the [`Set-CloudSyncSOAPolicy.ps1`](https://github.com/AzureAD/EntraIDGovernance/blob/main/Set-CloudSyncSOAPolicy.ps1) PowerShell script from the AzureAD/EntraIDGovernance repository on GitHub.
4. Open PowerShell as an administrator.
5. Change directory to the folder that contains the script.
6. Run the script. Specify `Enforced` as the mode (use `Audit` for a "what-if" rollout):

    ```powershell
    .\Set-CloudSyncSOAPolicy.ps1 -EnforcementMode Enforced -Credential (Get-Credential -Message "Enter Domain Admin credentials (format: DOMAIN\Username)")
    ```
7. Confirm that the `Cloud` policy is configured with the keyword **Enforced** (or **Audit**). Allow time for the new object to replicate across the domain.

    [![Screenshot of ADSI Edit showing the CN=Cloud policy object under the CN=SOA-Policies container.](media/how-to-ad-group-enforcement/soa-policies-container.png)](media/how-to-ad-group-enforcement/soa-policies-container.png#lightbox)

## Mark users and groups for enforcement

The attribute mapping differs for groups and users. Configure the applicable mapping for each object type that you want to protect.

### Mark groups for enforcement

Mark groups for enforcement by setting the `msDS-ObjectSoa` attribute to `Cloud` through the Cloud Sync attribute mapping.

1. In your group provisioning to AD configuration, edit the attribute mappings.
2. Add `msDS-ObjectSoa` as a target attribute with the value `Cloud`. Choose one of the following:
    - **Constant mapping** (recommended for most customers): sets the property for all groups in scope of the provisioning job.
    - **Expression mapping**: limits the groups for which the property is set, based on conditional logic.
3. Assign the groups you want to protect to the provisioning scope.
4. Provision the group on demand or by starting the sync cycle.

For details on configuring group provisioning to AD, see [Configure Microsoft Entra ID to Active Directory provisioning](how-to-configure-entra-to-active-directory).

### Mark users for enforcement

Mark users for enforcement by setting the `msDS-ObjectSoa` attribute to `Cloud` through the Cloud Sync attribute mapping. In a Microsoft Entra ID to AD configuration, the default user attribute mappings already include `msDS-ObjectSoa` mapped to the constant `Cloud`, so users provisioned by that configuration are marked automatically.

To confirm or configure the mapping:

1. In your Microsoft Entra ID to AD configuration, edit the **user** attribute mappings.
2. Confirm `msDS-ObjectSoa` is present as a target attribute with the value `Cloud`. If you need to limit which users are marked, use an **Expression** mapping instead of a **Constant** mapping.
3. Assign the users you want to protect to the provisioning scope.
4. Provision the users on demand or by starting the sync cycle. See [Configure provisioning to Active Directory](how-to-configure-entra-to-active-directory).

For details on user attribute mappings, see [Configure provisioning to Active Directory](how-to-configure-entra-to-active-directory#user-attribute-mappings).

## Verify the enforcement attribute

Use ADSI Edit on a domain controller to confirm that the policy applies to each on-premises user or group that you marked:

1. Open **ADSI Edit**.
2. Select **View** &gt; **Advanced Features**.
3. Navigate to the user or group, then open **Properties**.
4. Confirm that the `msDS-ObjectSoa` property is set to `Cloud`.

The following screenshot shows the attribute set on a group:

[![Screenshot of an Active Directory group's Attribute Editor tab in ADSI Edit, showing the msDS-ObjectSoa attribute set.](media/how-to-ad-group-enforcement/verify-msds-objectsoa-attribute.png)](media/how-to-ad-group-enforcement/verify-msds-objectsoa-attribute.png#lightbox)

## What administrators see when a change is blocked

In **Enforced** mode, an unauthorized attempt to modify an enforced user or group is blocked at the LDAP write layer and returns a specific error indicating that the object is managed by a cloud SOA policy. The change is never committed, so there's no drift to reconcile. The error is distinct from a generic "Access Denied," so administrators can tell that the change was intentionally blocked and that the object must be managed through Microsoft Entra. The exact wording varies by tool (Active Directory Users and Computers, PowerShell, or an LDAP client), but the meaning is the same.

In **Audit** mode, the same change is allowed and an event is written to the **Directory Service** log indicating that the change would have been blocked.

## Switch between Enforced and Audit modes

To change the mode, run `Set-CloudSyncSOAPolicy.ps1` again with the new value for `-EnforcementMode`:

```powershell
.\Set-CloudSyncSOAPolicy.ps1 -EnforcementMode Audit -Credential (Get-Credential -Message "Enter Domain Admin credentials (format: DOMAIN\Username)")
```

## Break-glass accounts

You can authorize additional identities to change enforced users and groups on-premises, for example an emergency administrator account to use when cloud provisioning is unavailable. You do this by adding the account's SID to the policy.

1. Open **ADSI Edit**.
2. Navigate to **CN=SOA-Policies** &gt; **CN=Cloud**.
3. Open the **Attribute Editor**.
4. Edit the `msDS-Settings` attribute and add the SID of the break-glass account.

    [![Screenshot of ADSI Edit showing the msDS-Settings attribute under CN=SOA-Policies being edited in the Multi-valued String Editor with a SID value.](media/how-to-ad-group-enforcement/add-break-glass-sid.png)](media/how-to-ad-group-enforcement/add-break-glass-sid.png#lightbox)

Keep the following limits and behaviors in mind:

- **Keep the allow list as small as possible.** For the strongest governance posture, allow only the provisioning agent SID and avoid adding break-glass accounts unless you have a specific operational need. The policy supports a maximum of **64 SIDs**.
- **SIDs are validated when the policy loads.** A single invalid or stale SID causes the **entire policy to fail to load**, which leaves no identities authorized. Watch the **Directory Service** log for a policy-load error and correct the SID.
- **Account changes are an operational risk.** If an authorized account is removed or recreated and its SID changes, update `msDS-Settings` accordingly. Document this in your operational runbooks.

## View enforcement events in the event log

To see audit events for unauthorized changes:

1. Set the Security Diagnostics value to `1` in the registry. For more information, see [AD and LDS diagnostic event logging](/en-us/troubleshoot/windows-server/active-directory/configure-ad-and-lds-event-logging).
2. Open Event Viewer and view the **Directory Service** event log.

With Security Diagnostics at the default value of `0`, only policy-load events are logged; individual block and audit events aren't recorded.

## Troubleshoot the enforcement policy

If AD object enforcement doesn't behave as expected (for example, on-premises changes that should be blocked are still processed), use the `Check-CloudSyncSOAPolicy.ps1` script to confirm that enforcement is enabled on a domain controller.

1. Download the [`Check-CloudSyncSOAPolicy.ps1`](https://github.com/AzureAD/EntraIDGovernance/blob/main/Check-CloudSyncSOAPolicy.ps1) script from the AzureAD/EntraIDGovernance repository on GitHub.
2. Sign in to the domain controller you want to validate.
3. Open PowerShell as an administrator.
4. Change directory to the folder that contains the script.
5. Run the script. It reports whether the AD object enforcement policy is enabled on that domain controller.

If a change that should be blocked still succeeds, check the following:

- The change was written to a domain controller that **isn't** updated and enabled. Confirm that **every writable domain controller** has the update and the Group Policy package, and was restarted afterward. To find which domain controller a client uses, run `nltest /dsgetdc:<your domain>`.
- The policy is in **Audit** mode rather than **Enforced**.
- The `SOA-Policies` container exists under `CN=System,DC=<your domain>`.
- The `msDS-ObjectSoa` attribute is set on the target user or group. If it isn't, confirm the applicable user or group attribute mapping and run a provisioning cycle.

If an authorized change is unexpectedly blocked, confirm that the acting account's SID is present in the policy's `msDS-Settings` attribute and that the change replicated to the domain controller processing the write.

## Test the policy

Use these example test cases to validate the configuration:

- Update the membership of an enforced group on-premises with an unauthorized account. The change should be blocked.
- Update an attribute of an enforced user on-premises with an unauthorized account. The change should be blocked.
- Switch the policy to **Audit** and repeat the test. The change is allowed, and an event appears in the **Directory Service** event log.
- Add a SID to the policy as a break-glass account and make an update with that account. The change should succeed.
- Attempt the same unauthorized change against each writable domain controller to confirm enforcement is consistent across the domain.

## Known behavior and limitations in this preview

- Converting the source of authority of a user or group in Microsoft Entra doesn't automatically lock down the object in AD. Complete the steps in this article to mark the object as enforced through provisioning to AD.
- Enforcement doesn't prevent deletions.
- Enforcement protects each marked object's attributes and, for groups, membership. Nesting an enforced group into an unenforced group isn't restricted.
- Existing limitations of user and group provisioning to AD continue to apply during this preview.
- Enforcement is only in effect on domain controllers where it's enabled. Enable the feature on every writable domain controller; otherwise a change written to a domain controller that isn't enabled is processed.