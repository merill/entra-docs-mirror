---
layout: Conceptual
title: Microsoft Entra Suite deployment scenario - Secure internet access - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/architecture/deployment-scenario-internet-access
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: janicericketts
ms.author: jricketts
ms.service: entra
manager: martinco
description: Configure Microsoft Entra Suite products for strict default internet access policies to control internet access according to business requirements.
ms.reviewer: gasinh
ms.topic: concept-article
ms.date: 2024-06-13T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
ms.subservice: architecture
locale: en-us
document_id: fea1754a-837f-7a7b-2cb8-bc35a7acb11a
document_version_independent_id: fea1754a-837f-7a7b-2cb8-bc35a7acb11a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/architecture/deployment-scenario-internet-access.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: architecture/deployment-scenario-internet-access
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/architecture/deployment-scenario-internet-access.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: 3280fdf0-d42b-1761-3026-d2541310b68f
---

# Microsoft Entra Suite deployment scenario - Secure internet access - Microsoft Entra | Microsoft Learn

The Microsoft Entra Suite deployment scenarios provide you with detailed guidance on how to combine and test these Microsoft Entra Suite products:

- [Microsoft Entra ID Protection](../id-protection/overview-identity-protection)
- [Microsoft Entra ID Governance](../id-governance/identity-governance-overview)
- [Microsoft Entra Verified ID (premium capabilities)](../verified-id/decentralized-identifier-overview)
- [Microsoft Entra Internet Access](../global-secure-access/concept-internet-access)
- [Microsoft Entra Private Access](../global-secure-access/concept-private-access)

In these guides, we describe scenarios that show the value of the Microsoft Entra Suite and how its capabilities work together.

- [Microsoft Entra deployment scenarios introduction](deployment-scenario-intro)
- [Microsoft Entra deployment scenario - Workforce and guest onboarding, identity, and access lifecycle governance across all your apps](deployment-scenario-workforce-guest)
- [Microsoft Entra deployment scenario - Modernize remote access to on-premises apps with MFA per app](deployment-scenario-remote-access)

## Scenario overview

In this guide, we describe how to configure Microsoft Entra Suite products for a scenario in which the fictional organization, Contoso, has strict default internet access policies and wants to control internet access according to business requirements.

In an example scenario for which we describe how to configure its solution, a Marketing department user requires access to social networking sites that Contoso prohibits for all users. Users can request access in [My Access](../id-governance/my-access-portal-overview). Upon approval, they become a member of a group that grants them access to social networking sites.

In another example scenario and corresponding solution, a SOC analyst needs to access a group of high-risk internet destinations for a specific time to investigate an incident. The SOC analyst can make that request in My Access. Upon approval, they become a member of a group that grants them access to high-risk internet destinations.

You can replicate these high-level steps for the Contoso solution as described in this scenario.

1. Sign up for Microsoft Entra Suite. Enable and configure [Microsoft Entra Internet Access](../global-secure-access/concept-internet-access) for desired network and security settings.
2. Deploy [Microsoft Global Secure Access clients](../global-secure-access/concept-clients) on users' devices. Enable Microsoft Entra Internet Access.
3. Create a security profile and web content filtering policies with a restrictive baseline policy that blocks specific web categories and web destinations for all users.
4. Create a security profile and web content filtering policies that allow access to social networking sites.
5. Create a security profile that enables the Hacking web category.
6. Use [Microsoft Entra ID Governance](../id-governance/identity-governance-overview)to allow users requesting access to access packages such as:
    - Marketing department users can request access to social networking sites with a quarterly access review.
    - SOC team members can request access to high-risk internet destinations with a time limit of eight hours.
7. Create and link two [Conditional Access policies](../identity/conditional-access/plan-conditional-access) using the Global Secure Access security profile session control. Scope the policy to groups of users for enforcement.
8. Confirm that traffic is appropriately granted with traffic logs in Global Secure Access. Ensure that Marketing department users can access the access package in the My Access portal.

These are the benefits of using these solutions together:

- **Least privilege access to internet destinations**. Reduce internet resource access to only what the user requires for their job role through the joiner/mover/leaver cycle. This approach reduces end user and device compromise risk.
- **Simplified and unified management**. Manage network and security functions from a single cloud-based console, reducing complexity and cost of maintaining multiple solutions and appliances.
- **Enhanced security and visibility**. Enforce granular and adaptive access policies based on user and device identity and context, as well as app and data sensitivity and location. Enriched logs and analytics provide gain insights into network and security posture to more quickly detect and respond to threats.
- **Improved user experience and productivity**. Provide fast and seamless access to necessary apps and resources without compromising security or performance.

## Requirements

This section defines the requirements for the scenario solution.

### Permissions

Administrators who interact with Global Secure Access features require the Global Secure Access Administrator and Application Administrator roles.

Conditional Access policy configuration requires the Conditional Access Administrator or Security Administrator role. Some features might require more roles.

Identity Governance configuration requires at least the Identity Governance Administrator role.

### Licenses

To implement all the steps in this scenario, you need Global Secure Access and Microsoft Entra ID Governance licenses. You can [purchase licenses or obtain trial licenses](https://www.microsoft.com/security/business/microsoft-entra-pricing). To learn more about Global Secure Access licensing, see the licensing section of [What is Global Secure Access](../global-secure-access/overview-what-is-global-secure-access).

### Users and devices prerequisites

To successfully deploy and test this scenario, configure for these prerequisites:

1. Microsoft Entra tenant with Microsoft Entra ID P1 license. [Purchase licenses or obtain trial licenses](https://www.microsoft.com/security/business/microsoft-entra-pricing).
    - One user with at least Global Secure Access Administrator and Application Administrator roles to configure Microsoft's Security Service Edge
    - At least one user as client test user in your tenant
2. One Windows client device with this configuration:
    - Windows 10/11 64-bit version
    - Microsoft Entra joined or hybrid joined
    - Internet connected
3. Download and install Global Secure Access Client on client device. The [Global Secure Access Client for Windows](../global-secure-access/how-to-install-windows-client) article describes prerequisites and installation.

## Configure Global Secure Access

In this section, we activate Global Secure Access through the Microsoft Entra admin center. We then set up the required initial configurations for the scenario.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator).
2. Browse to **Global Secure Access** &gt; **Get started** &gt; **Activate Global Secure Access in your tenant**. Select **Activate** to enable SSE features.
3. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding**. Toggle on **Private access profile**. Traffic forwarding enables you to configure the type of network traffic to tunnel through Microsoft's Security Service Edge Solution services. Set up [traffic forwarding profiles](../global-secure-access/concept-traffic-forwarding)to manage traffic types.
    - The **Microsoft 365 access profile** is for Microsoft Entra Internet Access for Microsoft 365.
    - The **Private access profile** is for Microsoft Entra Private Access.
    - The **Internet access profile** is for Microsoft Entra Internet Access. Microsoft's Security Service Edge solution only captures traffic on client devices with Global Secure Access Client installation.

        [![Screenshot of traffic forwarding showing enabled Private Access profile control.](media/deployment-scenario-internet-access/private-access-traffic-profile.png)](media/deployment-scenario-internet-access/private-access-traffic-profile-expanded.png#lightbox)

### Install Global Secure Access client

Microsoft Entra Internet Access for Microsoft 365 and Microsoft Entra Private Access use the Global Secure Access client on Windows devices. This client acquires and forwards network traffic to Microsoft's Security Service Edge solution. Perform these installation and configuration steps:

1. Ensure that the Windows device is Microsoft Entra joined or hybrid joined.
2. Sign in to the Windows device with a Microsoft Entra user with local admin privileges.
3. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator)
4. Browse to **Global Secure Access** &gt; **Connect** &gt; **Client Download**. Select **Download client**. Complete the installation.

    [![Screenshot of Client download showing the Windows Download Client control.](media/deployment-scenario-internet-access/client-download-inline.png)](media/deployment-scenario-internet-access/client-download-expanded.png#lightbox)
5. In the Window taskbar, the Global Secure Access Client first appears as disconnected. After a few seconds, when prompted for credentials, enter test user's credentials.
6. In the Window taskbar, hover over the Global Secure Access Client icon and verify **Connected** status.

### Create security groups

In this scenario, we use two security groups to assign security profiles using Conditional Access policies. In the Microsoft Entra admin center, create security groups with these names:

- Internet Access -- Allow Social Networking sites
- Internet Access -- Allow Hacking sites

Don't add any members to these groups. Later in this article, we configure Identity Governance to add members on request.

## Block access with baseline profile

In this section, we block access to inappropriate sites for all users in the organization with a baseline profile.

### Create baseline web filtering policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator)
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Web content filtering policies** &gt; **Create policy** &gt; [**Configure Global Secure Access content filtering**](../global-secure-access/how-to-configure-web-content-filtering).

    [![Screenshot of Web content filtering policies with a red box highlighting the Create policy control to create baseline web filtering policy.](media/deployment-scenario-internet-access/web-content-filtering-policies-baseline-inline.png)](media/deployment-scenario-internet-access/web-content-filtering-policies-baseline-expanded.png#lightbox)
3. On **Create a web content filtering policy** &gt; **Basics**, complete these fields:

    - **Name**: Baseline Internet Access Block Rule
    - **Description**: Add a description
    - **Action**: Block

        [![Screenshot of Enterprise applications, Create Global Secure Access application, Web content filtering policies, Create a web content filtering policy.](media/deployment-scenario-internet-access/create-web-content-filtering-policy-basics-baseline-inline.png)](media/deployment-scenario-internet-access/create-web-content-filtering-policy-basics-baseline-expanded.png#lightbox)
4. Select **Next**.
5. On **Create a web content filtering policy** &gt; **Policy Rules**, select **Add Rule**.

    ![Screenshot of Web content filtering policies, Create a web content filtering policy, Policy Rules with a red box highlighting the Add Rule control.](media/deployment-scenario-internet-access/create-web-content-filtering-policy-rules-baseline.png)
6. In **Add Rule**, complete these fields:

    - **Name**: Baseline blocked web categories
    - **Destination type:** webCategory
7. **Search**: Select the following categories. Confirm that they are in **Selected items**.

    - **Alcohol and Tobacco**
    - **Criminal Activity**
    - **Gambling**
    - **Hacking**
    - **Illegal Software**
    - **Social Networking**

        ![Screenshot of Update rule, Add a rule to your policy, with Baseline blocked web categories in Name text box.](media/deployment-scenario-internet-access/create-web-content-filtering-policy-add-rule-baseline.png)
8. Select **Add**.
9. On **Create a web content filtering policy** &gt; **Policy Rules**, confirm your selections.

    [![Screenshot of Enterprise applications, Create Global Secure Access application, Web content filtering policies, Create a web content filtering policy, Policy Rules.](media/deployment-scenario-internet-access/create-web-content-filtering-policy-review-baseline-inline.png)](media/deployment-scenario-internet-access/create-web-content-filtering-policy-review-baseline-expanded.png#lightbox)
10. Select **Next**.
11. On **Create a web content filtering policy** &gt; **Review**, confirm your policy configuration.
12. Select **Create policy**.

    [![Screenshot of Global Secure Access, Security profiles, Review tab for baseline policy.](media/deployment-scenario-internet-access/security-profiles-create-policy-review-baseline-inline.png)](media/deployment-scenario-internet-access/security-profiles-create-policy-review-baseline-expanded.png#lightbox)
13. To confirm policy creation, view it in **Manage web content filtering policies**.

### Configure baseline security profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator)
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**.
3. Select **Baseline Profile**.
4. On **Basics**, set **State** to enabled.
5. Select **Save**.
6. On **Edit Baseline Profile**, select **Link policies**. Select **Link a policy**. Select **Existing policy**. Complete these fields:
    - **Link a policy:** Select **Policy name** and **Baseline Internet Access Block Rule**
    - **Priority**: 100
    - **State**: Enabled
7. Select **Add**.
8. On **Create a profile** &gt; **Link policies**, confirm **Baseline Internet Access Block Rule** is listed.
9. Close the baseline security profile.

## Allow access to social networking sites

In this section, we create a security profile that allows access to social networking sites for users that request it.

### Create social networking web filtering policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator)
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Web content filtering policies** &gt; **Create policy** &gt; [**Configure Global Secure Access content filtering**](../global-secure-access/how-to-configure-web-content-filtering).

    [![Screenshot of Enterprise applications, Create Global Secure Access application, Web content filtering policies, Create a web content filtering policy.](media/deployment-scenario-internet-access/create-web-content-filtering-policy-basics-baseline-inline.png)](media/deployment-scenario-internet-access/create-web-content-filtering-policy-basics-baseline-expanded.png#lightbox)
3. On **Create a web content filtering policy** &gt; **Basics**, complete these fields:

    - **Name**: Allow Social Networking sites
    - **Description:** Add a description
    - **Action**: Allow
4. Select **Next**.
5. On **Create a web content filtering policy** &gt; **Policy Rules**, select **Add Rule**.
6. In **Add Rule**, complete these fields:

    - **Name**: Social networking
    - **Destination type**: webCategory
    - **Search**: Social
7. Select **Social Networking**
8. Select **Add**.
9. On **Create a web content filtering policy** &gt; **Policy Rules**, select **Next**.
10. On **Create a web content filtering policy** &gt; **Review**, confirm your policy configuration.

    ![Screenshot of Security profiles, Edit Block on risk, Basics, Security profiles, Edit Baseline profile, Create a web content filtering policy.](media/deployment-scenario-internet-access/social-networking-policy-review.png)
11. Select **Create policy**.
12. To confirm policy creation, view it in **Manage web content filtering policies**.

### Create social networking security policy profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator)
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**. Select **Create profile**.

    [![Screenshot of Security profiles with a red box highlighting the Create profile control.](media/deployment-scenario-internet-access/security-profiles-inline.png)](media/deployment-scenario-internet-access/security-profiles-expanded.png#lightbox)
3. On **Create a profile** &gt; **Basics**, complete these fields:

    - **Profile name**: Allow Social Networking sites
    - **Description:** Add a description
    - **State**: Enabled
    - **Priority:** 1000
4. Select **Next**.
5. On **Create a profile** &gt; **Link policies**, select **Link a policy**.
6. Select **Existing policy**.
7. In **Link a policy**, complete these fields:

    - **Policy name**: Allow Social Networking
    - **Priority:** 1000
    - **State**: Enabled
8. Select **Add**.
9. On **Create a profile** &gt; **Link policies**, confirm **Allow Social Networking** is listed.
10. Select **Next**.
11. On **Create a profile** &gt; **Review**, confirm your profile configuration.

    ![Screenshot of Security profiles, Edit Block on risk, Basics, Security profiles, Edit Baseline profile, Create a profile.](media/deployment-scenario-internet-access/security-profile-review.png)
12. Select **Create a profile**.

### Create social networking Conditional Access policy

In this section, we create a Conditional Access policy that enforces the **Allow Social Networking** security profile for users that request access.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. In **New Conditional Access Policy**, complete these fields:
    - **Name**: Internet Access -- Allow Social Networking sites
    - **Users or workload identities:** Specific users included
    - **What does this policy apply to?** Users and groups
    - **Include** &gt; **Select users and groups** &gt; Users and groups
5. Select your test group (such as *Internet Access -- Allow Social Networking sites*). Select **Select**.
6. **Target resources**
    - **Select what this policy applies to** &gt; Global Secure Access
    - **Select the traffic profiles this policy applies to** &gt; Internet traffic
7. Leave **Grant** at its default settings to grant access so that your defined security profile defines block functionality.
8. In **Session**, select **Use Global Secure Access security profile**.
9. Select **Allow Social Networking sites**.
10. In **Conditional Access Overview** &gt; **Enable policy**, select **On**.
11. Select **Create**.

## Allow access to hacking sites

In this section, we create a new security profile that allows access to hacking sites for users that request it. Users receive access for eight hours after which access is automatically removed.

### Create hacking web filtering policy

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator)
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Web content filtering policies** &gt; **Create policy** &gt; [**Configure Global Secure Access content filtering**](../global-secure-access/how-to-configure-web-content-filtering).

    [![Screenshot of Security profiles with a red box highlighting the Create profile control.](media/deployment-scenario-internet-access/security-profiles-inline.png)](media/deployment-scenario-internet-access/security-profiles-expanded.png#lightbox)
3. On **Create a web content filtering policy** &gt; **Basics**, complete these fields:

    - **Name**: Allow Hacking sites
    - **Description:** Add a description
    - **Action**: Allow
4. Select **Next**.
5. On **Create a web content filtering policy** &gt; **Policy Rules**, select **Add Rule**.
6. In **Add Rule**, complete these fields:

    - **Name**: Hacking
    - **Destination type**: webCategory
    - **Search**: Hacking, select **Hacking**
7. Select **Add**.
8. On **Create a web content filtering policy** &gt; **Policy Rules**, select **Next**.
9. On **Create a web content filtering policy** &gt; **Review**, confirm your policy configuration.

    ![Screenshot of Add Rule with Hacking in Selected items.](media/deployment-scenario-internet-access/hacking-policy-rule-add.png)
10. Select **Create policy**.
11. To confirm policy creation, view it in **Manage web content filtering policies**.

    ![Screenshot of Security profiles, Web content filtering policies.](media/deployment-scenario-internet-access/hacking-policy-rule-confirm.png)

### Create hacking security policy profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**. Select **Create profile**.

    [![Screenshot of Security profiles with a red box highlighting the Create profile control.](media/deployment-scenario-internet-access/security-profiles-inline.png)](media/deployment-scenario-internet-access/security-profiles-expanded.png#lightbox)
3. On **Create a profile** &gt; **Basics**, complete these fields:

    - **Profile name**: Allow Hacking sites
    - **Description:** Add a description
    - **State**: Enabled
    - **Priority:** 2000
4. Select **Next**.
5. On **Create a profile** &gt; **Link policies**, select **Link a policy**.
6. Select **Existing policy**.
7. In the **Link a policy** dialog box, complete these fields:

    - **Policy name**: Allow Hacking
    - **Priority:** 2000
    - **State**: Enabled
8. Select **Add**.
9. On **Create a profile** &gt; **Link policies**, confirm **Allow Hacking** is listed.
10. Select **Next**.
11. On **Create a profile** &gt; **Review**, confirm your profile configuration.

    ![Screenshot of Security profiles, Edit Block on risk, Basics, Security profiles, Edit Baseline profile, Create a profile.](media/deployment-scenario-internet-access/security-profile-review.png)
12. Select **Create a profile**.

### Create hacking Conditional Access policy

In this section, we create a Conditional Access policy that enforces the **Allow Hacking sites** security profile for the users that request access.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. In the **New Conditional Access Policy**dialog box, complete these fields:
    - **Name**: Internet Access -- Allow Hacking sites
    - **Users or workload identities:** Specific users included
    - **What does this policy apply to?** Users and groups
5. **Include** &gt; **Select users and groups** &gt; Users and groups
6. Select your test group (such as *Internet Access -- Allow Hacking sites*) &gt; select **Select**.
7. **Target resources**
    - **Select what this policy applies to** &gt; Global Secure Access
    - **Select the traffic profiles this policy applies to** &gt; Internet traffic
8. Leave **Grant** at its default settings to grant access so that your defined security profile defines block functionality.
9. In the **Session** dialog box, select **Use Global Secure Access security profile**.
10. Select **Allow Hacking sites**.
11. In **Conditional Access Overview** &gt; **Enable policy**, select **On**.
12. Select **Create**.

## Configure access governance

Follow these steps to create an entitlement management catalog:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **Identity governance &gt; Entitlement management &gt; Catalogs**.
3. Select **New catalog**

    [![Screenshot of New access review, Enterprise applications, All applications, Identity Governance, New catalog.](media/deployment-scenario-internet-access/identity-governance-catalogs-inline.png)](media/deployment-scenario-internet-access/identity-governance-catalogs-expanded.png#lightbox)
4. Enter a unique name for the catalog and provide a description. Requestors see this information in an access package's details (for example, *Internet Access*).
5. For this scenario, we create access packages in the catalog for internal users. Set **Enabled for external users** to **No**.

    ![Screenshot of New catalog with No selected for the Enabled for external users control.](media/deployment-scenario-internet-access/identity-governance-new-catalog.png)
6. To add the resources, go to **Catalogs** and open the catalog to which you want to add resources. Select **Resources**. Select **Add resources**.
7. Add the two security groups that you previously created earlier (such as *Internet Access -- Allow Social Networking sites* and *Internet Access -- Allow Hacking sites*).

    ![Screenshot of Identity Governance, Internet Access, Resources.](media/deployment-scenario-internet-access/internet-access-resources.png)

## Create access packages

In this section, we create access packages that allow users to request access to the internet site categories that each security profile defines. Follow these steps to create an access package in Entitlement management:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Identity Governance Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#identity-governance-administrator).
2. Browse to **ID Governance** &gt; **Entitlement management** &gt; **Access package**.
3. Select **New access package**.
4. For **Basics**, give the access package a name (such as *Internet Access -- Allow Social Networking sites*). Specify the catalog that you previously created.
5. For **Resource roles**, select the security that you previously added (such as *Internet Access -- Allow Social Networking sites*).
6. In **Role**, select **Member**.
7. For **Requests**, select **For users in your directory**.
8. To scope the users that can request access to social networking sites, select **Specific users and groups** and add an appropriate group of users. Otherwise, select **All members**.
9. On **Requests**, select **Yes** for **Enable new requests**.
10. **Optional:** In **Approval**, specify whether approval is required when users request this access package.
11. For **Lifecycle**, specify when a user's assignment to the access package expires. Specify whether users can extend their assignments. For **Expiration,** set **Access package assignments** expiration to **On date**, **Number of days**, **Number of hours**, or **Never**.

    ![Screenshot of New access package, Requests.](media/deployment-scenario-internet-access/new-access-package-requests.png)
12. Repeat the steps to create a new access package that allows access to hacking sites. Configure these settings:

    - **Resource**: Internet Access -- Allow Hacking sites
    - **Who can request:** SOC team members
    - **Lifecycle:** Set **Number of hours** to 8 hours

## Test user access

In this section, we validate that the user can't access sites that the baseline profile blocks.

1. Sign in to the device where you installed the Global Secure Access client.
2. In a browser, go to sites that the baseline profile blocks and verify blocked access. For example:
    1. `hackthissite.org` is a free, safe, and legal training ground for security professionals to test and expand ethical hacking skills. This site is classified as Hacking.
    2. `YouTube.com` is a free video sharing platform. This site is classified as Social Networking.

        ![Screenshot of two browser windows showing blocked access to test sites.](media/deployment-scenario-internet-access/test-baseline-access.png)

### Request social networking access

In this section, we validate that a Marketing department user can request access to social networking sites.

1. Sign in to the device where you installed the Global Secure Access client with a user that is a member of the Marketing team (or a user that has authorization to request access to the example *Internet Access -- Allow Social Networking sites* access package).
2. In a browser, validate blocked access to a site in the Social Networking category that the baseline security profile blocks. For example, try accessing `youtube.com`.

    ![Screenshot of browser showing blocked access to a test site.](media/deployment-scenario-internet-access/validate-blocked-access.png)
3. Browse to `myaccess.microsoft.com`. Select **Access packages**. Select **Request** for the *Internet Access -- Allow Social Networking sites* access package.

    ![Screenshot of My Access, Access packages, Available.](media/deployment-scenario-internet-access/access-packages.png)
4. Select **Continue**. Select **Request**.
5. If you configured approval for the access package, sign in as an approver. Browse to `myaccess.microsoft.com`. Approve the request.
6. Sign in as a Marketing department user. Browse to `myaccess.microsoft.com`. Select **Request history**. Validate your request status to *Internet Access -- Allow Social Networking sites* is **Delivered**.
7. New settings might take a few minutes to apply. To speed up the process, right-click the Global Secure Access icon in the system tray. Select **Log in as a different user**. Sign in again.
8. Try accessing sites in the social networking category that the baseline security profile blocks. Validate that you can successfully browse them. For example, try browsing `youtube.com`.

    ![Screenshot of a browser showing access to a test site.](media/deployment-scenario-internet-access/validate-social-networking-access.png)

### Request hacking site access

In this section, we validate that a SOC team user can request access to hacking sites.

1. Sign in to the device where you installed the Global Secure Access client with a user that is a member of the SOC team (or a user that has authorization to request access to the example *Internet Access -- Allow Hacking sites* access package).
2. In a browser, validate blocked access to a site in the hacking category that the baseline security profile blocks. For example, `hackthissite.org`.

    ![Screenshot of browser showing blocked access to a test site.](media/deployment-scenario-internet-access/validate-blocked-access.png)
3. Browse to `myaccess.microsoft.com`. Select **Access packages**. Select **Request** for the *Internet Access -- Allow Hacking sites* access package.
4. Select **Continue**. Select **Request**.
5. If you configured approval for the access package, sign in as an approver. Browse to `myaccess.microsoft.com`. Approve the request.
6. Sign in as a SOC team user. Browse to `myaccess.microsoft.com`. Select **Request history**. Validate your request status to *Internet Access -- Allow Hacking sites* is **Delivered**.
7. New settings might take a few minutes to apply. To speed up the process, right-click the Global Secure Access icon in the system tray. Select **Log in as a different user**. Sign in again.
8. Try accessing sites in the hacking category that the baseline security profile blocks. Validate that you can successfully browse them. For example, try browsing `hackthissite.org`.

    ![Screenshot of browser window showing access to test site.](media/deployment-scenario-internet-access/test-hacking-access.png)
9. If you configured hacking site access with **Lifecycle** &gt; **Number of hours** set to 8 in previous steps, after eight hours elapses, verify blocked access to hacking sites.