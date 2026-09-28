---
layout: Conceptual
title: How to enable custom URL domains for External ID - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-custom-url-domain
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to set up custom URL domains to personalize the authentication sign-in endpoints for the external customers and consumers of your app.
ms.topic: how-to
ms.date: 2024-12-03T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 8cda1fb8-7f4a-2d26-0eab-e05f8d1662d8
document_version_independent_id: 8cda1fb8-7f4a-2d26-0eab-e05f8d1662d8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-custom-url-domain.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-custom-url-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-custom-url-domain.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b5e53e15-0a76-4936-b270-8b2badca62ac
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6908a4c7-0b59-4f8b-a00e-59c83ae0a04a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: ac644cc4-34d8-1e6f-9f32-cf6d4c58075b
---

# How to enable custom URL domains for External ID - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

This article describes how to enable [custom URL domains](concept-custom-url-domain) for Microsoft Entra External ID applications in external tenants. A custom URL domain allows you to brand your application’s sign-in endpoints with your own custom URL domain instead of Microsoft’s default domain name.

## Prerequisites

- [Learn how custom URL domains work](concept-custom-url-domain) in External ID.
- If you haven't already created an external tenant, [create one now](how-to-create-external-tenant-portal).
- [Create a user flow](how-to-user-flow-sign-up-sign-in-customers) so users can sign up and sign in to your application.
- [Register a web application](/en-us/entra/identity-platform/quickstart-register-app).

## Step 1: Add a custom domain name to your tenant

When you create an external tenant, it comes with an initial domain name, &lt;domainname&gt;.onmicrosoft.com. You can't change or delete the initial domain name, but you can add your own custom domain name. For these steps, be sure to sign in to your *external* tenant configuration in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Domain Name Administrator](../../identity/role-based-access-control/permissions-reference#domain-name-administrator).
2. Choose your *external* tenant: Select the **Settings** icon in the top menu, and then switch to your external tenant.
3. Navigate to **Identity** &gt; **Settings** &gt; **Domain names** &gt; **Custom domain names**.
4. [Add your custom domain name](../../fundamentals/add-custom-domain#add-your-custom-domain-name) to Microsoft Entra ID.
5. [Add your DNS information to the domain registrar](../../fundamentals/add-custom-domain#add-your-dns-information-to-the-domain-registrar). After you add your custom domain name to your tenant, create a DNS `TXT` or `MX` record for your domain. Creating this DNS record for your domain verifies ownership of your domain name.

    The following are examples of TXT records for *login.contoso.com* and *account.contoso.com*:

    | Name (hostname) | Type | Data |
    | --- | --- | --- |
    | login | TXT | MS=ms12345678 |
    | account | TXT | MS=ms87654321 |

    The TXT record must be associated with the subdomain or hostname of the domain (for example, the *login* part of the *contoso.com* domain). If the hostname is empty or `@`, Microsoft Entra ID can't verify the custom domain name you added.

    Tip

    You can manage your custom domain name with any publicly available DNS service, such as GoDaddy. If you don't have a DNS server, you can use [Azure DNS zone](/en-us/azure/dns/dns-getstarted-portal), or [App Service domains](/en-us/azure/app-service/manage-custom-dns-buy-domain).
6. [Verify your custom domain name](../../fundamentals/add-custom-domain#verify-your-custom-domain-name). Verify each subdomain or hostname you plan to use. For example, to be able to sign in with *login.contoso.com* and *account.contoso.com*, you need to verify both subdomains and not just the top-level domain *contoso.com*.

    Important

    After the domain is verified, delete the DNS TXT record you created.

## Step 2: Associate the custom domain name with a custom URL domain

After you add and verify the custom domain name in your external tenant, associate the custom domain name with a custom URL domain.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Choose your *external* tenant: Select the **Settings** icon in the top menu, and then switch to your external tenant.
3. Navigate to **Entra ID** &gt; **Domain names** &gt; **Custom URL domains**.
4. Select **Add custom url domain**.
5. In the **Add custom url domain** pane, select the custom domain name you entered in Step 1.

    [![Screenshot showing the Add custom URL domain pane.](media/how-to-custom-url-domain/add-custom-url-domain.png)](media/how-to-custom-url-domain/add-custom-url-domain.png#lightbox)
6. Select **Add**.

## Step 3: Create a new Azure Front Door instance

Follow these steps to create an Azure Front Door:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Choose the tenant containing your Azure Front Door subscription: Select the **Settings** icon in the top menu, and then switch to the tenant that contains your Azure Front Door subscription.
3. Follow the steps in [Create Front Door profile - Quick Create](/en-us/azure/frontdoor/create-front-door-portal#create-front-door-profile---quick-create) to create a Front Door for your tenant using the following settings. Leave the **Caching** and **WAF policy** settings empty.

    | Key | Value |
    | --- | --- |
    | Subscription | Select your Azure subscription. |
    | Resource group | Select an existing resource group, or create a new one. |
    | Name | Give your profile a name such as `ciamazurefrontdoor`. |
    | Tier | Select either Standard or Premium tier. Standard tier is content delivery optimized. Premium tier builds on Standard tier and is focused on security. See [Tier Comparison](/en-us/azure/frontdoor/standard-premium/tier-comparison). |
    | Endpoint name | Enter a globally unique name for your endpoint, such as `ciamazurefrontdoor`. The **Endpoint hostname** is generated automatically. |
    | Origin type | Select `Custom`. |
    | Origin host name | Enter `<tenant-name>.ciamlogin.com`. Replace `<tenant-name>` with the name of your tenant, for example `contoso.ciamlogin.com`. |
4. Once the Azure Front Door resource is created, select **Overview**, and copy the **Endpoint hostname** for use in a later step. It looks something like `ciamazurefrontdoor-ab123e.z01.azurefd.net`.
5. Make sure the **Host name** and **Origin host header** of your origin have the same value:

    1. Under **Settings**, select **Origin groups**.
    2. Select your origin group from the list, such as **default-origin-group**.
    3. On the right pane, select your **Origin host name** such as `contoso.ciamlogin.com`.
    4. On the **Update origin** pane, update the **Host name** and **Origin host header** to have the same value.

    ![Screenshot showing the host name and origin host header fields.](media/how-to-custom-url-domain/front-door-update-origin-page.png)

## Step 4: Set up your custom URL domain on Azure Front Door

In this step, you add the custom URL domain you registered in Step 1 to your Azure Front Door.

### 4.1. Create a CNAME DNS record

To add the custom URL domain, create a canonical name (CNAME) record with your domain provider. A CNAME record is a type of DNS record that maps a source domain name to a destination domain name (alias). For Azure Front Door, the source domain name is your custom URL domain name, and the destination domain name is your Front Door default hostname that you configured in Step 2, for example, `ciamazurefrontdoor-ab123e.z01.azurefd.net`.

After Front Door verifies the CNAME record that you created, traffic addressed to the source custom URL domain (such as `login.contoso.com`) is routed to the specified destination Front Door default frontend host, such as `contoso-frontend.azurefd.net`. For more information, see [add a custom domain to your Front Door](/en-us/azure/frontdoor/front-door-custom-domain).

To create a CNAME record for your custom domain:

1. Sign in to the web site of the domain provider for your custom domain.
2. Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the web site labeled **Domain Name**, **DNS**, or **Name Server Management**.
3. Create a CNAME record entry for your custom URL domain and complete the fields as shown in the following table.

    | Source | Type | Destination |
    | --- | --- | --- |
    | `<login.contoso.com>` | CNAME | `contoso-frontend.azurefd.net` |

    - Source: Enter your custom URL domain (for example, login.contoso.com).
    - Type: Enter *CNAME*.
    - Destination: Enter the default Front Door frontend host you create in Step 2. It must be in the following format: *&lt;hostname&gt;*.azurefd.net, for example, `contoso-frontend.azurefd.net`.
4. Save your changes.

### 4.2. Associate the custom URL domain with your Front Door

1. In the Azure portal home, search for and select the `ciamazurefrontdoor` Azure Front Door resource to open it.
2. In the left menu, under **Settings**, select **Domains**.
3. Select **Add a domain**.
4. For **DNS management**, select **All other DNS services**.
5. For **Custom domain**, enter your custom domain, such as `login.contoso.com`.
6. Keep the other values as defaults, and then select **Add**. Your custom domain is added to the list.
7. Under **Validation state** of the domain that you just added, select **Pending**. A pane with a TXT record info opens.

    1. Sign in to the web site of the domain provider for your custom domain.
    2. Find the page for managing DNS records by consulting the provider's documentation or searching for areas of the web site labeled **Domain Name**, **DNS**, or **Name Server Management**.
    3. Create a new TXT DNS record and complete the following fields:

        - **Name**: Enter just subdomain portion of `_dnsauth.contoso.com`, for example `_dnsauth`
        - **Type**: `TXT`
        - **Value**: For example, `75abc123t48y2qrtsz2bvk......`

        After you add the TXT DNS record, the **Validation state** in the Front Door resource will eventually change from **Pending** to **Approved**. You might need to refresh the page to see the change.
8. In the Azure portal. Under **Endpoint association** of the domain that you just added, select **Unassociated**.
9. For **Select endpoint**, select the hostname endpoint from the dropdown.
10. For **Select routes** list, select **default-route**, and then select **Associate**.

### 4.3. Enable the route

The **default-route** routes the traffic from the client to Azure Front Door. Then, Azure Front Door uses your configuration to send the traffic to the external tenant. To enable the default-route, follow these steps.

1. Select **Front Door manager**.
2. To enable the **default-route**, first expand an endpoint from the list of endpoints in the Front Door manager. Then, select the **default-route**.
3. Select the **Enabled route** checkbox.
4. Select **Update** to save the changes.

## Test your custom URL domains

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Choose your *external* tenant: Select the **Settings** icon in the top menu, and then switch to your external tenant.
3. Under **External Identities**, select **User flows**.
4. Select a user flow, and then select **Run user flow**.
5. For **Application**, select the web application named *webapp1* that you previously registered. The **Reply URL** should show `https://jwt.ms`.
6. Copy the URL under **Run user flow endpoint**.

    ![Screenshot showing the run user flow option.](media/how-to-custom-url-domain/run-user-flow.png)
7. To simulate a sign in with your custom domain, open a web browser and use the URL you copied. Replace the domain (*&lt;tenant-name&gt;*.ciamlogin.com) with your custom domain.

    For example, instead of:

    ```http
    https://contoso.ciamlogin.com/contoso.onmicrosoft.com/oauth2/v2.0/authorize?p=B2C_1_susi&client_id=00001111-aaaa-2222-bbbb-3333cccc4444&nonce=defaultNonce&redirect_uri=https%3A%2F%2Fjwt.ms&scope=openid&response_type=id_token&prompt=login
    ```

    use:

    ```http
    https://login.contoso.com/contoso.onmicrosoft.com/oauth2/v2.0/authorize?p=B2C_1_susi&client_id=00001111-aaaa-2222-bbbb-3333cccc4444&nonce=defaultNonce&redirect_uri=https%3A%2F%2Fjwt.ms&scope=openid&response_type=id_token&prompt=login
    ```
8. Verify that the sign-in page is loaded correctly. Then, sign in with a local account.

## Configure your applications

After you configure and test the custom URL domain, update your applications to load a URL with your custom URL domain as the hostname instead of the default domain.

The custom URL domain integration applies to authentication endpoints that use External ID user flows to authenticate users. These endpoints have the following format:

- `https://<custom-url-domain>/<tenant-name>/v2.0/.well-known/openid-configuration`
- `https://<custom-url-domain>/<tenant-name>/oauth2/v2.0/authorize`
- `https://<custom-url-domain>/<tenant-name>/oauth2/v2.0/token`

Replace:

- **custom-url-domain** with your custom URL domain
- **tenant-name** with your tenant name or tenant ID

The SAML service provider metadata might look like the following sample:

```html
https://custom-url-domain-name/tenant-name/Samlp/metadata
```

### (Optional) Use the tenant ID

You can replace your external tenant name in the URL with your tenant ID GUID to remove all references to “onmicrosoft.com” in the URL. You can find your tenant ID GUID in the **Overview** page in the Azure portal or the Microsoft Entra admin center. For example, change `https://account.contosobank.co.uk/contosobank.onmicrosoft.com/` to `https://account.contosobank.co.uk/<tenant-ID-GUID>/`.

If you choose to use tenant ID instead of tenant name, be sure to update the identity provider **OAuth redirect URIs** accordingly. When you use your tenant ID instead of tenant name, a valid OAuth redirect URI looks similar to the following sample:

```html
https://login.contoso.com/00001111-aaaa-2222-bbbb-3333cccc4444/oauth2/authresp 
```

## (Optional) Azure Front Door advanced configuration

You can use Azure Front Door advanced configuration, such as Azure Web Application Firewall (WAF). Azure WAF provides centralized protection of your web applications from common exploits and vulnerabilities.

When using custom domains, consider the following points:

- The WAF policy must be the same tier as the Azure Front Door profile. For more information about how to create a WAF policy to use with Azure Front Door, see [Configure WAF policy](/en-us/azure/frontdoor/how-to-configure-endpoints).
- The WAF managed rules feature isn't officially supported as it can cause false positives and prevent legitimate requests from passing through, so only use WAF custom rules if they meet your needs.

## (Optional) Block the default domain

After you configure custom URL domains, users will still be able to access the default domain name *&lt;tenant-name&gt;.ciamlogin.com*. You need to block access to the default domain so that attackers can't use it to access your apps or run distributed denial-of-service (DDoS) attacks. Submit a support ticket to request the blocking of access to the default domain.

Caution

Make sure your custom domain works properly before you request that the default domain be blocked. After the default domain is blocked, certain features will no longer work. See [Blocking the default domain](concept-custom-url-domain#blocking-the-default-domain).

## Troubleshooting

- **Page not found message.** When you try to sign in with the custom URL domain, you get an HTTP 404 error message. This issue could be related to the DNS configuration or the Azure Front Door backend configuration. Try the following steps:

    - Make sure the custom URL domain is registered and successfully verified in your tenant.
    - Make sure the [custom domain](/en-us/azure/frontdoor/front-door-custom-domain) is configured properly. The `CNAME` record for your custom domain must point to your Azure Front Door default frontend host (for example, contoso-frontend.azurefd.net).
- **Our services aren't available right now message.** When you try to sign in with the custom URL domain, you get the error message: *Our services aren't available right now. We're working to restore all services as soon as possible. Please check back soon.* This issue could be related to the Azure Front Door route configuration. Check the status of the **default-route**. If it's disabled, enable the route.
- **Resource was removed, changed names, or is temporarily unavailable.** When you try to sign in with the custom URL domain, you get the error message *the resource you are looking for has been removed, had its name changed, or is temporarily unavailable*. This issue could be related to the Microsoft Entra custom domain verification. Make sure the custom domain is registered and **successfully verified** in your tenant.
- **Error code 399265: RoutingFromInvalidHost.** This error code appears when a tenant is making a request from a domain that isn't verified. Make sure to add TXT record details in your DNS records. Then [verify your custom domain name](../../fundamentals/add-custom-domain#verify-your-custom-domain-name) again.
- **Error code 399280: InvalidCustomUrlDomain.** This error code appears when a tenant is making request from a verified domain that is not a custom URL domain. Make sure to associate the custom domain name with a custom URL domain.