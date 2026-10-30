---
layout: Conceptual
title: Secure private application access with Privileged Identity Management and Global Secure Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-global-access-with-pim
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Add just-in-time privileged access for critical servers and applications using Privileged Identity Management (PIM) with Microsoft Entra Private Access.
ms.subservice: entra-private-access
ms.topic: how-to
ms.date: 2026-03-25T00:00:00.0000000Z
ms.reviewer: katabish
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 14fa7ecd-8db7-6ffb-9427-6c649e0b2954
document_version_independent_id: 14fa7ecd-8db7-6ffb-9427-6c649e0b2954
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-global-access-with-pim.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-global-access-with-pim
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-global-access-with-pim.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d5321f31-a36c-484d-a808-69f9088f4f84
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6032d191-3b2e-4df1-9108-c955546973aa
platformId: 55937cc6-7470-3b42-648e-0202978622a2
---

# Secure private application access with Privileged Identity Management and Global Secure Access - Global Secure Access | Microsoft Learn

## Overview

Microsoft Entra Private Access provides secure access to private applications. Private Access includes built-in capabilities for maintaining a secure environment. Microsoft Entra Private Access does this by controlling access to private apps and preventing unauthorized or compromised devices from accessing critical resources. For general corporate access, see [Microsoft Entra Private Access](concept-private-access).

For the scenario where you need to control access to specific *critical* resources, such as highly valued servers and applications, Microsoft recommends that you add an extra security layer by enforcing just-in-time privileged access on top of their already secured private access.

This article discusses how to use Microsoft Entra Private Access to enable Privileged Identity Management (PIM) with Global Secure Access. For details about enabling (PIM), see [What is Microsoft Entra Privileged Identity Management?](/en-us/entra/id-governance/privileged-identity-management/pim-configure).

## Ensure secure access to your high value private applications

Customers should consider configuring PIM using Global Secure Access to enable:

**Enhanced Security:** PIM allows for just-in-time privileged access, reducing the risk of excessive, unnecessary, or misused access permissions within your environment. This enhanced security aligns with the [Zero Trust](https://www.microsoft.com/security/business/zero-trust) principle, ensuring that users have access only when they need it.

**Compliance and Auditing**: Using PIM with Microsoft Global Secure Access can help ensure that your organization meets compliance requirements by providing detailed tracking and logging of privileged access requests. For details about PIM licensing, see [Microsoft Entra ID Governance licensing fundamentals](../id-governance/licensing-fundamentals)

## Prerequisites

- [Microsoft Entra ID license that includes Privileged Identity Management (PIM)](../fundamentals/licensing)
- [Microsoft Entra Private Access](concept-private-access)

## Secure private access

To successfully implement secure private access, you must complete these three steps:

1. Configure and assign groups
2. Activate privileged access
3. Follow compliance guidance

## Step 1: Configure and assign groups

To begin, configure and assign groups by creating a Microsoft Entra ID group, onboard it as a PIM managed group, update group assignments with eligible membership, and specify access for user and devices.

1. Sign in to [Microsoft Entra](https://entra.microsoft.com/) as at least a [Privileged Role Administrator](../id-governance/privileged-identity-management/pim-configure).
2. Browse to **Microsoft Entra ID** &gt; **Groups** &gt; **All groups**.

    [![Screenshot of the All groups screen.](media/pim-global-secure-access/all-groups.png)](media/pim-global-secure-access/all-groups.png#lightbox)
3. Select **New group**.
4. In the **Group type**, select **Security**.
5. Provide a group name; for example, `FinReport-SeniorAnalyst-SecureAccess`.

    - This group name example indicates the application (FinReport), the role (SeniorAnalyst), and the nature of the group (SecureAccess), Choose a name that reflects the group's function or the assets it protects.
6. In the **Membership type** option, select **Assigned**.
7. Select **Create**.

    [![Screenshot of the New group screen.](media/pim-global-secure-access/new-group.png)](media/pim-global-secure-access/new-group.png#lightbox)

### Onboard the group to PIM

1. Sign in to [Microsoft Entra](https://entra.microsoft.com/) as at least a [Privileged Role Administrator](../id-governance/privileged-identity-management/pim-configure).
2. Browse to **ID Governance** &gt; **Privileged Identity Management**.
3. Select **Groups**, then **Discover groups**.
4. Select the group that you created; for example, `FinReport-SeniorAnalyst-SecureAccess`, then select **Manage groups**.
5. When prompted for onboarding, select **OK**.

### Update PIM policy role settings (optional step)

1. Select **Setting**, then select **Member**.
2. Adjust any other settings you want in the **Activation** tab.
3. Set the **Activation Max Duration**; for example, 0.5 hours.
4. In the **On activation** option, require **Azure MFA**, and select **Update**.

### Assign eligible membership

1. Select **Assignments**, then **Add assignments**.

    [![Screenshot of the Add assignments option.](media/pim-global-secure-access/add-assignments.png)](media/pim-global-secure-access/add-assignments.png#lightbox)
2. In the **Role** option, select **Member**, then select **Next**.
3. Add the selected members that you would like to include for the role.
4. In the **Assignment Type** option, select **Eligible**, then select **Assign**.

### Quick Access assignment

1. Sign in to [Microsoft Entra](https://entra.microsoft.com/) as at least a [Privileged Role Administrator](../id-governance/privileged-identity-management/pim-configure).
2. Browse to **Global Secure Access** &gt; **Quick Access** &gt; **Users and groups**.
3. Select **Add user/group**, then specify the group that you created; for example, `FinReport-SeniorAnalyst-SecureAccess`.

Note

This scenario is most effective when you choose **Per-app Access**, as **Quick Access** is used here for reference only. Apply the same steps if you choose **Enterprise Applications**.

### Client-side experience

Even if a user and their device meet security requirements, attempting to access a privileged resource results in an error. This error occurs because Microsoft Entra Private Access recognizes that the user hasn't been assigned access to the application.

[![Screenshot of the client experience error message.](media/pim-global-secure-access/client-experience.png)](media/pim-global-secure-access/client-experience.png#lightbox)

## Step 2: Activate privileged access

Next, we activate group membership using the Microsoft Entra admin center, and then attempt to connect with the new role activated.

1. Sign in to [Microsoft Entra](https://entra.microsoft.com/).
2. Browse to **ID Governance** &gt; **Privileged Identity Management**.
3. Select **My roles** &gt; **Groups** to see all eligible assignments.

    [![Screenshot of My role groups screen.](media/pim-global-secure-access/my-roles-groups.png)](media/pim-global-secure-access/my-roles-groups.png#lightbox)
4. Select **Activate**, then type the reason in the **Reason** box. You can also choose to adjust the parameters of the session, then select **Activate**.

    [![Screenshot of the Activate member screen.](media/pim-global-secure-access/activate-member.png)](media/pim-global-secure-access/activate-member.png#lightbox)
5. Once the role is activated, you receive a confirmation from the portal.

    [![Screenshot of the member being activated in the portal.](media/pim-global-secure-access/member-activated.png)](media/pim-global-secure-access/member-activated.png#lightbox)

### Reattempt to connect with role activated

Browse any of the published resources, as you should be able to successfully connect to them.

[![Screenshot of connecting to published resource.](media/pim-global-secure-access/identify-remote-computer.png)](media/pim-global-secure-access/identify-remote-computer.png#lightbox)

### Deactivate the role

If the work is completed ahead of the time you allocated, you can choose to deactivate the role. This action terminates the role membership.

1. Sign in to [Microsoft Entra](https://entra.microsoft.com/).
2. Browse to **ID Governance** &gt; **Privileged Identity Management**.
3. Select **My roles**, then **Groups**.
4. Select **Deactivate**.

    [![Screenshot of Deactivate member screen.](media/pim-global-secure-access/deactivate-member.png)](media/pim-global-secure-access/deactivate-member.png#lightbox)
5. A confirmation is sent to you once the role is deactivated.

## Step 3: Follow compliance guidance

This final step enables you to successfully maintain a history of access requests and activations. The standard log format helps to meet tracking and logging compliance guidance and provide an audit trail.

[![Screenshot of the Audit log details screen.](media/pim-global-secure-access/audit-log-details.png)](media/pim-global-secure-access/audit-log-details.png#lightbox)