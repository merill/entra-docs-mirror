---
layout: FAQ
title: Microsoft Entra application proxy frequently asked questions - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-faq
summary: >
  <p>This page answers frequently asked questions about Microsoft Entra application proxy.</p>
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: app-proxy
manager: dougeby
description: Learn answers to frequently asked questions (FAQ) about using Microsoft Entra application proxy to publish internal, on-premises applications to remote users.
ms.topic: faq
ms.date: 2026-03-11T00:00:00.0000000Z
ms.reviewer: ashishj
ai-usage: ai-assisted
locale: en-us
document_id: 4d489cbc-59e1-82cc-0a39-256df8da29e2
document_version_independent_id: d81145b1-671e-cb50-7c4e-f577189e4e9e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-proxy/application-proxy-faq.yml
site_name: Docs
depot_name: MSDN.entra-docs
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-proxy/application-proxy-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-proxy/application-proxy-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: fe090621-d683-5b4a-9616-a559eb011a3e
---

# Microsoft Entra application proxy frequently asked questions - Microsoft Entra ID | Microsoft Learn

This page answers frequently asked questions about Microsoft Entra application proxy.

## General

### Can I modify an application proxy app from the \*\*App registrations\*\* page in the Microsoft Entra admin center?

No, the following configuration items are being used by app proxy and shouldn't be altered or deleted:

- Enable/Disable “Allow public clients flows”.
- Federated credentials.
- API Permissions. Modifying any of the above configuration items on the App registration page breaks preauthentication for Microsoft Entra application proxy.

### An application proxy app's client secret (CWAP\_AuthSecret) is nearing expiry or has already expired. What should I do?

Application Proxy apps no longer rely on CWAP secrets. For apps using Microsoft Entra ID preauthentication, Federated Identity Credentials (FIC) are now used instead. FIC is more secure, don't expire, and require significantly less maintenance. Applications configured with Passthrough pre-authentication or those using Access Tokens don't require Federated Identity Credentials — even if an FIC was previously created.

You can safely ignore any existing CWAP secrets in the app registration of your Application Proxy app or clean up old or expired secrets. For more information about Federated Identity Credentials, see [Overview of federated identity credentials in Microsoft Entra ID](/en-us/graph/api/resources/federatedidentitycredentials-overview).

### Can I delete an application proxy app from the App registrations page in the Microsoft Entra admin center?

No, you should delete an application proxy app from the **Enterprise applications** area of the Microsoft Entra admin center. If you delete the application proxy app from the **App registrations** area of the Microsoft Entra admin center, then you could experience issues.

### What license is required to use Microsoft Entra application proxy?

To use Microsoft Entra application proxy, you must have a Microsoft Entra ID P1 or P2 license. For more information about licensing, see [Microsoft Entra pricing](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing)

### What happens to Microsoft Entra application proxy in my tenant, if my license expires?

If your license expires, application proxy is automatically disabled. Your application information is saved for up to one year.

### Why is the Enable application proxy button grayed out?

Make sure you have at least a Microsoft Entra ID P1 or P2 license and a Microsoft Entra private network connector installed. After you successfully install your first connector, the Microsoft Entra application proxy service is enabled automatically.

## Connector configuration

### Does application proxy use the same connector as Microsoft Entra Private Access?

Yes, Microsoft Entra private network connector is used by both application proxy and Microsoft Entra Private Access. For more information about the connector, see [Microsoft Entra private network connector](../../global-secure-access/concept-connectors). To troubleshoot connector configuration, see [troubleshoot connectors](../../global-secure-access/troubleshoot-connectors).

### ConnectorTroubleshooter cannot start

The ConnectorTroubleshooterLauncher.exe is deprecated and no longer functional. Currently, there is no replacement available.

### Can I change the logon user of the Microsoft Entra Private Network Connector / Updater Services?

Changing the logon user of the connector or updater service is not supported.

Correct Configuration:

Microsoft Entra Private Network Connector: *Network Service* Microsoft Entra Private Network Connector Updater: *NT Authority\System*

## Application configuration

### Do I need to manage or rotate client secrets when deploying Application Proxy apps?

No. Application Proxy apps no longer rely on client secrets (CWAP\_AuthSecret). For apps using Microsoft Entra ID preauthentication, Federated Identity Credentials (FIC) are now used instead. FIC is more secure, doesn't expire, and requires no manual rotation or maintenance. Applications configured with passthrough preauthentication or those using access tokens don't require Federated Identity Credentials. You can safely ignore any existing CWAP secrets in the app registration and remove old or expired secrets. For more information, see [Overview of federated identity credentials in Microsoft Entra ID](/en-us/graph/api/resources/federatedidentitycredentials-overview).

### Can I use the domain suffixes `[tenant name].onmicrosoft.com` or `[tenant name].mail.onmicrosoft.com` in the external URL?

Although these suffixes appear in the suffix list, you shouldn't use them. These domain suffixes aren't meant to be used with Microsoft Entra application proxy. If you use these domain suffixes, the created Microsoft Entra application proxy application won't work. You can use either the standard domain suffix `msappproxy.net` or a [custom domain](how-to-configure-custom-domain).

### Does application proxy support sovereign and regional clouds?

Microsoft Entra ID has an application proxy service that enables users to access on-premises applications by signing in with their Microsoft Entra account. If you have installed connectors in different regions, you can optimize traffic by selecting the closest application proxy cloud service region to use with each connector group, see [Optimize traffic flow with Microsoft Entra application proxy](application-proxy-add-on-premises-application).

### I'm receiving an error about an invalid certificate or possible wrong password.

After you uploaded the SSL certificate, you receive the message "Invalid certificate, possible wrong password" on the portal.

Here are some tips for troubleshooting this error:

- Check for problems with the certificate. Install it on your local computer. If you don't experience any issues then the certificate is good.
- Ensure that the password doesn't contain any special characters. The password should only contain the characters 0-9, A-Z, and a-z.
- If the certificate was created with Microsoft Software Key Storage Provider, the RSA algorithm must be used.

### What is the length of the default and "long" backend timeout? Can the timeout be extended?

The default length is 85 seconds. The "long" setting is 180 seconds. The timeout limit can't be extended.

### Can a service principal manage application proxy using PowerShell or Microsoft Graph APIs?

No, this is currently not supported.

### I'm using or want to use Microsoft Entra application proxy. Can I replace the "onmicrosoft.com" fallback domain of my tenant in Microsoft 365 as suggested in the article "Add and replace your onmicrosoft.com fallback domain in Microsoft 365"?

No, you must use the original fallback domain.

Article mentioned in question: [Add and replace your onmicrosoft.com fallback domain in Microsoft 365](/en-us/microsoft-365/admin/setup/add-or-replace-your-onmicrosoftcom-domain?view=o365-worldwide)

### How do I change the landing page my application loads?

From the Application Registrations page, you can change the homepage URL to the desired external URL of the landing page. The specified page is loaded when the application is launched from My Apps or the Office 365 Portal. For configuration steps, see [Set a custom home page for published apps by using Microsoft Entra application proxy](application-proxy-configure-custom-home-page)

### Why do I get redirected to a truncated URL when I try to access my published application whenever the URL contains a "#" (hashtag) character?

If Microsoft Entra preauthentication is configured, and the application URL contains a “#” character when you try to access the application for the first time, you get redirected to Microsoft Entra ID (login.microsoftonline.com) for the authentication. After you complete the authentication, you get redirected to the URL part prior to the ”#” character and everything that comes after the “#“ seems to be ignored/ removed. For example if the URL is `https://www.contoso.com/#/home/index.html`, after Microsoft Entra authentication is done the user is redirected to `https://www.contoso.com/`. This behavior is by design due to how the “#” character is handled by the browser.

Possible solutions/alternatives:

- Set up a redirection from `https://www.contoso.com` to `https://contoso.com/#/home/index.html`. The user must first access `https://www.contoso.com`.
- The URL used for the first access attempt must include the “#” character in encoded form (%23). The published server might not accept this.
- Configure passthrough preauthentication type (not recommended).

### Can only IIS-based applications be published? What about web applications running on non-Windows web servers? Does the connector have to be installed on a server with IIS installed?

No, there's no IIS requirement for applications that are published. You can publish web applications running on servers other than Windows Server. However, you might not be able to use preauthentication with a non-Windows Server, depending on if the web server supports Negotiate (Kerberos authentication). IIS isn't required on the server where the connector is installed.

### Can I configure application proxy to add the HSTS header?

Application proxy doesn't automatically add the HTTP Strict-Transport-Security header to HTTPS responses, but it maintains the header if it is in the original response sent by the published application. Providing a setting to enable this functionality is on the roadmap.

### Can I use a custom port number in the external URL?

No, if the protocol `http` is configured in the external URL then the Microsoft Entra application proxy endpoint accepts incoming request on the port TCP 80, if the protocol `https` then on the port TCP 443.

### Can I use a custom port number in the internal URL?

Yes, some examples for internal URLs including ports: `http://app.contoso.local:8888/`, `https://app.contoso.local:8080/`, `https://app.contoso.local:8081/test/`.

### What are the challenges, if the external and the internal URLs are different?

Some responses sent by the published web applications might contain hard-coded URLs. In this case it must be ensured by using a link translation solution that the client always uses the correct URL. Link translation solutions might be complex and might not work in all the scenarios. For more information, see [Redirect hardcoded links for apps published with Microsoft Entra application proxy](application-proxy-configure-hard-coded-link-translation).

As best practice it's advised to use identical external and internal URLs. External and internal URLs are considered to be identical, if the `protocol://hostname:port/path/` in both URLs are identical.

This can be achieved by using the [Custom Domains](how-to-configure-custom-domain) feature.

Examples:

Identical:

```
External URL: https://app1.contoso.com/test/
Internal URL: https://app1.contoso.com/test/
```

Not identical:

```
External URL: https://app1.contoso.com/test/
Internal URL: http://app1.contoso.com/test/

External URL: https://app1.contoso.com/test/
Internal URL: https://app1.contoso.com:8080/test/

External URL: https://app1.msappproxy.net/test/
Internal URL: https://app1.contoso.com:/test/
```

Making the external and internal URLs identical isn't possible at all, if the internal URL contains a nonstandard port (other than TCP 80 / 443).

In some scenarios changes must be done in the configuration of the web app.

## Integrated Windows authentication

### When should I use the PrincipalsAllowedToDelegateToAccount method when setting up Kerberos Constrained Delegation (KCD)?

The PrincipalsAllowedToDelegateToAccount method is used when connector servers are in a different domain from the web application service account. It requires the use of Resource-based Constrained Delegation. If the connector servers and the web application service account are in the same domain, you can use Active Directory Users and Computers to configure the delegation settings on each of the connector machine accounts, allowing them to delegate to the target SPN.

If the connector servers and the web application service account are in different domains, Resource-based delegation is used. The delegation permissions are configured on the target web server and web application service account. This method of Constrained Delegation is relatively new. The method was introduced in Windows Server 2012, which supports cross-domain delegation by allowing the resource (web service) owner to control which machine and service accounts can delegate to it. There's no UI to assist with this configuration, so you need to use PowerShell. For more information, see the whitepaper [Understanding Kerberos Constrained Delegation with application proxy](https://aka.ms/kcdpaper).

### Does NTLM authentication work with Microsoft Entra application proxy?

NTLM authentication can’t be used as a preauthentication or single sign-on method. NTLM authentication can be used only when it can be negotiated directly between the client and the published web application. Using NTLM authentication usually causes a sign-in prompt to appear in the browser.

### Can I use the sign in identity “On-premises user principal name” or “On-premises SAM account name” in a B2B IWA single sign-on scenario?

No, this won’t work, because a guest user in Microsoft Entra ID doesn't have the attribute that is required by any of the sign in identities mentioned above.

In this case there's a fallback to “User principal name”. For more details on the B2B scenario, see [Grant B2B users in Microsoft Entra ID access to your on-premises applications](../../external-id/hybrid-cloud-to-on-premises).

## Passthrough preauthentication

### Can I use Conditional Access Policies for applications published with passthrough preauthentication?

Conditional Access Policies are only enforced for successfully authenticated users in Microsoft Entra ID. Passthrough preauthentication doesn’t trigger Microsoft Entra authentication, so Conditional Access Policies can't be enforced. With passthrough preauthentication, MFA policies must be implemented on the on-premises server, if possible, or by enabling Microsoft Entra ID preauthentication with Microsoft Entra application proxy.

### Can I publish a web application with client certificate authentication requirement?

No, this scenario isn't supported because application proxy terminates TLS traffic.

## Remote Desktop Gateway publishing

### How can I publish Remote Desktop Gateway over Microsoft Entra application proxy?

Refer to [Publish Remote Desktop with Microsoft Entra application proxy](application-proxy-integrate-with-remote-desktop-services).

### Can I use Kerberos Constrained Delegation (single sign-on - Windows Integrated Authentication) in the Remote Desktop Gateway publishing scenario?

No, this scenario isn't supported.

### My users don't use Internet Explorer 11 and the preauthentication scenario doesn’t work for them. Is this expected?

Yes, it’s expected. The preauthentication scenario requires an ActiveX control, which isn't supported in third-party browsers.

### Is the Remote Desktop Web Client (HTML5) supported?

Yes, this scenario is currently in preview. Refer to [Publish Remote Desktop with Microsoft Entra application proxy](application-proxy-integrate-with-remote-desktop-services).

### After I configured the preauthentication scenario, I realized that the user has to authenticate twice: first on the Microsoft Entra sign-in form, and then on the RDWeb sign-in form. Is this expected? How can I reduce this to one sign-in?

Yes, it's expected. If the user’s computer is Microsoft Entra joined, the user signs in to Microsoft Entra ID automatically. The user needs to provide their credentials only on the RDWeb sign-in form.

### Can I use the Resources Launch Method option "Download the rdp file" under Settings on the Remote Desktop Web Client Portal in Microsoft Entra preauthentication scenario?

This option enables the user to download the rdp file and use it by another RDP client (outside of the Remote Desktop Web Client). Typically, another RDP clients (like the Microsoft Remote Desktop Client) can't handle the preauthentication natively. That's why the scenario doesn't work.

## SharePoint publishing

### How can I publish SharePoint over Microsoft Entra application proxy?

Refer to [Enable remote access to SharePoint with Microsoft Entra application proxy](application-proxy-integrate-with-sharepoint-server).

### Can I use the SharePoint mobile app (iOS/ Android) to access a published SharePoint Server?

The [SharePoint mobile app](/en-us/sharepoint/administration/supporting-the-sharepoint-mobile-apps-online-and-on-premises) doesn't support Microsoft Entra preauthentication currently.

## Active Directory Federation Services (AD FS) publishing

### Can I use Microsoft Entra application proxy as AD FS proxy (like Web application proxy)?

No, Microsoft Entra application proxy is designed to work with Microsoft Entra ID and doesn’t fulfill the requirements to act as an AD FS proxy.

### Can I use Microsoft Entra application proxy to publish any AD FS endpoint (like /adfs/portal/updatepassword/)?

No, this isn't supported.

## WebSocket

### Does Microsoft Entra application proxy support the WebSocket protocol?

Applications that use the WebSocket protocol, for example QlikSense and Remote Desktop Web Client (HTML5), are now supported. The following are known limitations:

- Application proxy discards the cookie that is set on the server response while opening the WebSocket connection.
- There's no SSO applied to the WebSocket request.
- Features (Eventlogs, PowerShell, and Remote Desktop Services) in the Windows Admin Center (WAC) don't work through Microsoft Entra application proxy.

The WebSocket application doesn't have any unique publishing requirements, and can be [published](application-proxy-add-on-premises-application) the same way as all your other application proxy applications.

## Link translation

### Does using Link translation affect performance?

Yes. Link translation affects performance. The application proxy service scans the application for hardcoded links and replaces them with their respective, published external URLs before presenting them to the user.

For best performance, we recommend using identical internal and external URLs by configuring [custom domains](how-to-configure-custom-domain). If using custom domains isn't possible, you can improve link translation performance by using the My Apps Secure Sign in Extension or Microsoft Edge Browser on mobile. See [Redirect hardcoded links for apps published with Microsoft Entra application proxy](application-proxy-configure-hard-coded-link-translation).

## Wildcards

### How do I use wildcards to publish two applications with the same custom domain name but with different protocols, one for HTTP and one for HTTPS?

This scenario isn't supported directly. Your options for this scenario are:

1. Publish both the HTTP and HTTPS URLs as separate applications with a wildcard, but give each of them a different custom domain. This configuration works since they have different external URLS.
2. Publish the HTTPS URL through a wildcard application. Publish the HTTP applications separately using these application proxy PowerShell cmdlets:

    - [Application proxy application management](/en-us/powershell/module/azuread/?preserve-view=true#application_proxy_application_management)
    - [private network connector management](/en-us/powershell/module/azuread/?preserve-view=true#application_proxy_connector_management)