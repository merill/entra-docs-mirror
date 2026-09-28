---
layout: Conceptual
title: 'Quickstart: Microsoft Entra seamless single sign-on - Microsoft Entra ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sso-quick-start
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: Learn how to get started with Microsoft Entra seamless single sign-on by using Microsoft Entra Connect.
keywords: what is Azure AD Connect, install Active Directory, required components for Azure AD, SSO, Single Sign-on
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: a4b0e1f3-71c7-602c-0d1c-7f1ccea0558f
document_version_independent_id: b4216897-a2d9-67d4-5652-4f8ab77140ba
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-sso-quick-start.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-sso-quick-start
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-sso-quick-start.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 25341dad-6609-74c6-792e-248e18b89134
---

# Quickstart: Microsoft Entra seamless single sign-on - Microsoft Entra ID | Microsoft Learn

Microsoft Entra seamless single sign-on (Seamless SSO) automatically signs in users when they're using their corporate desktops that are connected to your corporate network. Seamless SSO provides your users with easy access to your cloud-based applications without using any other on-premises components.

To deploy Seamless SSO for Microsoft Entra ID by using Microsoft Entra Connect, complete the steps that are described in the following sections.

## Check the prerequisites

Ensure that the following prerequisites are in place:

- **Set up your Microsoft Entra Connect server**: If you use [pass-through authentication](how-to-connect-pta) as your sign-in method, no other prerequisite check is required. If you use [password hash synchronization](how-to-connect-password-hash-synchronization) as your sign-in method and there's a firewall between Microsoft Entra Connect and Microsoft Entra ID, ensure that:

    - You use Microsoft Entra Connect version 1.1.644.0 or later.
    - If your firewall or proxy allows, add the connections to your allowlist for `*.msappproxy.net` URLs over port 443. If you require a specific URL instead of a wildcard for proxy configuration, you can configure `tenantid.registration.msappproxy.net`, where `tenantid` is the GUID of the tenant for which you're configuring the feature. If URL-based proxy exceptions aren't possible in your organization, you can instead allow access to the [Azure datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated weekly. This prerequisite is applicable only when you enable the Seamless SSO feature. It isn't required for direct user sign-ins.

        Note

        - Microsoft Entra Connect versions 1.1.557.0, 1.1.558.0, 1.1.561.0, and 1.1.614.0 have a problem related to password hash sync. If you *don't* intend to use password hash sync in conjunction with pass-through authentication, review the [Microsoft Entra Connect release notes](reference-connect-version-history) to learn more.
- **Use a supported Microsoft Entra Connect topology**: Ensure that you're using one of the Microsoft Entra Connect [supported topologies](plan-connect-topologies).

    Note

    Seamless SSO supports multiple on-premises Windows Server Active Directory (Windows Server AD) forests, whether or not there are Windows Server AD trusts between them.
- **Set up domain administrator credentials**: You must have domain administrator credentials for each Windows Server AD forest that:

    - You sync to Microsoft Entra ID through Microsoft Entra Connect.
    - Contains users you want to enable Seamless SSO for.
- **Enable modern authentication**: To use this feature, you must enable [modern authentication](/en-us/microsoft-365/enterprise/modern-auth-for-office-2013-and-2016) on your tenant.
- **Use the latest versions of Microsoft 365 clients**: To get a silent sign-on experience with Microsoft 365 clients (for example, with Outlook, Word, or Excel), your users must use versions 16.0.8730.xxxx or later.

Note

If you have an outgoing HTTP proxy, make sure that the URL `autologon.microsoftazuread-sso.com` is on your allowlist. You should specify this URL explicitly because the wildcard might not be accepted.

## Enable the feature

Enable Seamless SSO through [Microsoft Entra Connect](../whatis-hybrid-identity).

Note

If Microsoft Entra Connect doesn't meet your requirements, you can [enable Seamless SSO by using PowerShell](tshoot-connect-sso#manual-reset-of-the-feature). Use this option if you have more than one domain per Windows Server AD forest, and you want to target the domain to enable Seamless SSO for.

If you're doing a *fresh installation of Microsoft Entra Connect*, choose the [custom installation path](how-to-connect-install-custom). On the **User sign-in** page, select the **Enable single sign on** option.

![Screenshot that shows the User sign-in page in Microsoft Entra Connect, with Enable single sign on selected.](media/how-to-connect-sso-quick-start/sso8.png)

Note

The option is available to select only if the sign-on method that's selected is **Password Hash Synchronization** or **Pass-through Authentication**.

If you *already have an installation of Microsoft Entra Connect*, in **Additional tasks**, select **Change user sign-in**, and then select **Next**. If you're using Microsoft Entra Connect versions 1.1.880.0 or later, the **Enable single sign on** option is selected by default. If you're using an earlier version of Microsoft Entra Connect, select the **Enable single sign on** option.

![Screenshot that shows the Additional tasks page with Change the user sign-in selected.](media/how-to-connect-pta-quick-start/changeusersignin.png)

Continue through the wizard to the **Enable single sign on** page. Provide Domain Administrator credentials for each Windows Server AD forest that:

- You sync to Microsoft Entra ID through Microsoft Entra Connect.
- Contains users you want to enable Seamless SSO for.

When you complete the wizard, Seamless SSO is enabled on your tenant.

Note

The Domain Administrator credentials are not stored in Microsoft Entra Connect or in Microsoft Entra ID. They're used only to enable the feature.

To verify that you have enabled Seamless SSO correctly:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Hybrid Identity Administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator).
2. Browse to **Entra ID** &gt; **Entra Connect** &gt; **Connect sync**.
3. Verify that **Seamless single sign-on** is set to **Enabled**.

![Screenshot that shows the Microsoft Entra Connect pane in the admin portal.](media/how-to-connect-sso-quick-start/sso10.png)

Important

Seamless SSO creates a computer account named `AZUREADSSOACC` in each Windows Server AD forest in your on-premises Windows Server AD directory. The `AZUREADSSOACC` computer account must be strongly protected for security reasons. Only Domain Administrator accounts should be allowed to manage the computer account. Ensure that Kerberos delegation on the computer account is disabled, and that no other account in Windows Server AD has delegation permissions on the `AZUREADSSOACC` computer account. Store the computer accounts in an organization unit so that they're safe from accidental deletions and only Domain Administrators can access them.

Note

If you're using Pass-the-Hash and Credential Theft Mitigation architectures in your on-premises environment, make appropriate changes to ensure that the `AZUREADSSOACC` computer account doesn't end up in the Quarantine container.

## Roll out the feature

You can gradually roll out Seamless SSO to your users by using the instructions provided in the next sections. You start by adding the following Microsoft Entra URL to all or selected user intranet zone settings through Group Policy in Windows Server AD:

`https://autologon.microsoftazuread-sso.com`

You also must enable an intranet zone policy setting called **Allow updates to status bar via script** through Group Policy.

Note

The following instructions work only for Internet Explorer, Microsoft Edge, and Google Chrome on Windows (if Google Chrome shares a set of trusted site URLs with Internet Explorer). Learn how to set up Mozilla Firefox and Google Chrome on macOS.

### Why you need to modify user intranet zone settings

By default, a browser automatically calculates the correct zone, either internet or intranet, from a specific URL. For example, `http://contoso/` maps to the *intranet* zone, and `http://intranet.contoso.com/` maps to the *internet* zone (because the URL contains a period). Browsers don't send Kerberos tickets to a cloud endpoint, like to the Microsoft Entra URL, unless you explicitly add the URL to the browser's intranet zone.

There are two ways you can modify user intranet zone settings:

| Option | Admin consideration | User experience |
| --- | --- | --- |
| Group policy | Admin locks down editing of intranet zone settings | Users can't modify their own settings |
| Group policy preference | Admin allows editing of intranet zone settings | Users can modify their own settings |

### Group policy detailed steps

1. Open the Group Policy Management Editor tool.
2. Edit the group policy that's applied to some or all your users. This example uses **Default Domain Policy**.
3. Go to **User Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Internet Explorer** &gt; **Internet Control Panel** &gt; **Security Page**. Select **Site to Zone Assignment List**.

    ![Screenshot that shows the Security Page with Site to Zone Assignment List selected.](media/how-to-connect-sso-quick-start/sso6.png)
4. Enable the policy, and then enter the following values in the dialog:

    - **Value name**: The Microsoft Entra URL where the Kerberos tickets are forwarded.
    - **Value** (Data): **1** indicates the intranet zone.

        The result looks like this example:

        Value name: `https://autologon.microsoftazuread-sso.com`

        Value (Data): 1

    Note

    If you want to prevent some users from using Seamless SSO (for instance, if these users sign in on shared kiosks), set the preceding values to **4**. This action adds the Microsoft Entra URL to the restricted zone and Seamless SSO fails for the users all the time.
5. Select **OK**, and then select **OK** again.

    ![Screenshot that shows the Show Contents window with a zone assignment selected.](media/how-to-connect-sso-quick-start/sso7.png)
6. Go to **User Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Internet Explorer** &gt; **Internet Control Panel** &gt; **Security Page** &gt; **Intranet Zone**. Select **Allow updates to status bar via script**.

    [![Screenshot that shows the Intranet Zone page with Allow updates to status bar via script selected.](media/how-to-connect-sso-quick-start/sso11.png)](media/how-to-connect-sso-quick-start/sso11.png#lightbox)
7. Enable the policy setting, and then select **OK**.

    ![Screenshot that shows the Allow updates to status bar via script window with the policy setting enabled.](media/how-to-connect-sso-quick-start/sso12.png)

### Group policy preference detailed steps

1. Open the Group Policy Management Editor tool.
2. Edit the group policy that's applied to some or all your users. This example uses **Default Domain Policy**.
3. Go to **User Configuration** &gt; **Preferences** &gt; **Windows Settings** &gt; **Registry** &gt; **New** &gt; **Registry item**.

    ![Screenshot that shows Registry selected and Registry Item selected.](media/how-to-connect-sso-quick-start/sso15.png)
4. Enter or select the following values as demonstrated, and then select **OK**.

    - **Key Path**: Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\microsoftazuread-sso.com\autologon
    - **Value name**: https
    - **Value type**: REG\_DWORD
    - **Value data**: 00000001

        ![Screenshot that shows the New Registry Properties window.](media/how-to-connect-sso-quick-start/sso16.png)

        ![Screenshot that shows the new values listed in Registry Editor.](media/how-to-connect-sso-quick-start/sso17.png)

### Browser considerations

The next sections have information about Seamless SSO that's specific to different types of browsers.

#### Mozilla Firefox (all platforms)

If you're using the [Authentication](https://github.com/mozilla/policy-templates/blob/master/README.md#authentication) policy settings in your environment, ensure that you add the Microsoft Entra URL (`https://autologon.microsoftazuread-sso.com`) to the **SPNEGO** section. You can also set the **PrivateBrowsing** option to **true** to allow Seamless SSO in private browsing mode.

#### Safari (macOS)

Ensure that the machine running the macOS is joined to Windows Server AD.

Instructions for joining your macOS device to Windows Server AD are outside the scope of this article.

#### Microsoft Edge based on Chromium (all platforms)

If you've overridden the [AuthNegotiateDelegateAllowlist](/en-us/DeployEdge/microsoft-edge-policies#authnegotiatedelegateallowlist) or [AuthServerAllowlist](/en-us/DeployEdge/microsoft-edge-policies#authserverallowlist) policy settings in your environment, ensure that you also add the Microsoft Entra URL (`https://autologon.microsoftazuread-sso.com`) to these policy settings.

#### Microsoft Edge based on Chromium (macOS and other non-Windows platforms)

For Microsoft Edge based on Chromium on macOS and other non-Windows platforms, see the [Microsoft Edge based on Chromium Policy List](/en-us/DeployEdge/microsoft-edge-policies#authserverallowlist) for information on how to add the Microsoft Entra URL for integrated authentication to your allowlist.

#### Google Chrome (all platforms)

If you've overridden the [AuthNegotiateDelegateAllowlist](https://chromeenterprise.google/policies/#AuthNegotiateDelegateAllowlist) or [AuthServerAllowlist](https://chromeenterprise.google/policies/#AuthServerAllowlist) policy settings in your environment, ensure that you also add the Microsoft Entra URL (`https://autologon.microsoftazuread-sso.com`) to these policy settings.

#### macOS

The use of third-party Active Directory Group Policy extensions to roll out the Microsoft Entra URL to Firefox and Google Chrome for macOS users is outside the scope of this article.

#### Known browser limitations

Seamless SSO doesn't work on Internet Explorer if the browser is running in Enhanced Protected mode. Seamless SSO supports the next version of Microsoft Edge based on Chromium, and it works in InPrivate and Guest mode by design. Microsoft Edge (legacy) is no longer supported.

You might need to configure `AmbientAuthenticationInPrivateModesEnabled` for InPrivate or guest users based on the corresponding documentation:

- [Microsoft Edge Chromium](/en-us/DeployEdge/microsoft-edge-policies#ambientauthenticationinprivatemodesenabled)
- [Google Chrome](https://chromeenterprise.google/policies/?policy=AmbientAuthenticationInPrivateModesEnabled)

## Test Seamless SSO

To test the feature for a specific user, ensure that all the following conditions are in place:

- The user signs in on a corporate device.
- The device is joined to your Windows Server AD domain. The device *doesn't* need to be [Microsoft Entra joined](../../devices/overview).
- The device has a direct connection to your domain controller, either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.
- You've rolled out the feature to this user through Group Policy.

To test a scenario in which the user enters a username, but not a password:

- Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com/). Be sure to either clear the browser cache or use a new private browser session with any of the supported browsers in private mode.

To test a scenario in which the user doesn't have to enter a username or password, use one of these steps:

- Sign in to `https://myapps.microsoft.com/contoso.onmicrosoft.com`. Be sure to either clear the browser cache or use a new private browser session with any of the supported browsers in private mode. Replace `contoso` with your tenant name.
- Sign in to `https://myapps.microsoft.com/contoso.com` in a new private browser session. Replace `contoso.com` with a verified domain (not a federated domain) on your tenant.

## Roll over keys

In Enable the feature, Microsoft Entra Connect creates computer accounts (representing Microsoft Entra ID) in all the Windows Server AD forests on which you enabled Seamless SSO. To learn more, see [Microsoft Entra seamless single sign-on: Technical deep dive](how-to-connect-sso-how-it-works).

Important

The Kerberos decryption key on a computer account, if leaked, can be used to generate Kerberos tickets for any synchronized user. Malicious actors can then impersonate Microsoft Entra sign-ins for compromised users. We highly recommend that you periodically roll over these Kerberos decryption keys, or at least once every 30 days.

For instructions on how to roll over keys, see [Microsoft Entra seamless single sign-on: Frequently asked questions](how-to-connect-sso-faq#how-can-i-roll-over-the-kerberos-decryption-key-of-the--azureadsso--computer-account-).

Important

You don't need to do this step *immediately* after you have enabled the feature. Roll over the Kerberos decryption keys at least once every 30 days.