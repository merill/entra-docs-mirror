---
layout: Conceptual
title: Secure resources with Microsoft Entra multifactor authentication and ADFS - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/authentication/howto-mfa-adfs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: Justinha
ms.author: justinha
ms.service: entra-id
ms.subservice: authentication
manager: dougeby
description: This is the Microsoft Entra multifactor authentication page that describes how to get started with Microsoft Entra multifactor authentication and AD FS in the cloud.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: michmcla
ms.custom: sfi-image-nochange
locale: en-us
document_id: d879929f-9ca3-547a-8792-8922f2054adf
document_version_independent_id: 063b05fb-bc56-a988-2f69-78dbc199fe5c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/authentication/howto-mfa-adfs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/authentication/howto-mfa-adfs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/authentication/howto-mfa-adfs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f94dc1af-62b7-3181-db03-d0b881bf7d0b
---

# Secure resources with Microsoft Entra multifactor authentication and ADFS - Microsoft Entra ID | Microsoft Learn

If your organization is federated with Microsoft Entra ID, use Microsoft Entra multifactor authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Microsoft Entra ID. Use the following procedures to secure Microsoft Entra resources with either Microsoft Entra multifactor authentication or Active Directory Federation Services.

Note

Set the domain setting [federatedIdpMfaBehavior](/en-us/graph/api/resources/internaldomainfederation?view=graph-rest-beta&amp;preserve-view=true#federatedidpmfabehavior-values) to `enforceMfaByFederatedIdp` (recommended) or **SupportsMFA** to `$True`. The **federatedIdpMfaBehavior** setting overrides **SupportsMFA** when both are set.

## Secure Microsoft Entra resources using AD FS

To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully. This claim is passed on to Microsoft Entra ID. Follow this procedure to walk through the steps:

1. Open AD FS Management.
2. On the left, select **Relying Party Trusts**.
3. Right-select on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.

    ![ADFS Console - Relying Party Trusts](media/howto-mfa-adfs/trustedip1.png)
4. On Issuance Transform Rules, select **Add Rule**.

    ![Editing Issuance Transform Rules](media/howto-mfa-adfs/trustedip2.png)
5. On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and select **Next**.

    ![Screenshot shows Add Transform Claim Rule Wizard where you select a Claim rule template.](media/howto-mfa-adfs/trustedip3.png)
6. Give your rule a name.
7. Select **Authentication Methods References** as the Incoming claim type.
8. Select **Pass through all claim values**.

    ![Screenshot shows Add Transform Claim Rule Wizard where you select Pass through all claim values.](media/howto-mfa-adfs/configurewizard.png)
9. Select **Finish**. Close the AD FS Management console.

## Trusted IPs for federated users

Trusted IPs allow administrators to bypass two-step verification for specific IP addresses, or for federated users who have requests originating from within their own intranet. The following sections describe how to configure the bypass using Trusted IPs. This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.

This example uses Microsoft 365 for our Relying Party Trusts.

### Configure the AD FS claims rules

The first thing we need to do is to configure the AD FS claims. Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.

1. Open AD FS Management.
2. On the left, select **Relying Party Trusts**.
3. Right-select on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**

    ![ADFS Console - Edit Claim Rules](media/howto-mfa-adfs/trustedip1.png)
4. On Issuance Transform Rules, select **Add Rule.**

    ![Adding a Claim Rule](media/howto-mfa-adfs/trustedip2.png)
5. On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and select **Next**.

    ![Screenshot shows Add Transform Claim Rule Wizard where you select Pass Through or Filter an Incoming Claim.](media/howto-mfa-adfs/trustedip3.png)
6. In the box next to Claim rule name, give your rule a name. For example: InsideCorpNet.
7. From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.

    ![Adding Inside Corporate Network claim](media/howto-mfa-adfs/trustedip4.png)
8. Select **Finish**.
9. On Issuance Transform Rules, select **Add Rule**.
10. On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and select **Next**.
11. In the box under Claim rule name: enter *Keep Users Signed In*.
12. In the Custom rule box, enter:

    ```ad
        c:[Type == "https://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c); 
    ```

    ![Create custom claim to keep users signed in](media/howto-mfa-adfs/trustedip5.png)
13. Select **Finish**.
14. Select **Apply**.
15. Select **Ok**.
16. Close AD FS Management.

### Configure Microsoft Entra multifactor authentication Trusted IPs with federated users

Now that the claims are in place, we can configure trusted IPs.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Authentication Policy Administrator](../role-based-access-control/permissions-reference#authentication-policy-administrator).
2. Browse to **Conditional Access** &gt; **Named locations**.
3. From the **Conditional Access - Named locations** blade, select **Configure MFA trusted IPs**

    ![Microsoft Entra Conditional Access named locations Configure MFA trusted IPs](media/howto-mfa-adfs/trustedip6.png)
4. On the Service Settings page, under **trusted IPs**, select **Skip multifactor-authentication for requests from federated users on my intranet**.
5. Select **save**.

That's it! At this point, federated Microsoft 365 users should only have to use MFA when a claim originates from outside the corporate intranet.