---
layout: Conceptual
title: Overview of custom URL domains for External ID - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/concept-custom-url-domain
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn about setting up custom URL domains to personalize the authentication sign-in endpoints for the external customers and consumers of your app.
ms.topic: concept-article
ms.date: 2025-09-16T00:00:00.0000000Z
ms.custom: it-pro, sfi-image-nochange
locale: en-us
document_id: 921b028e-1c03-2051-0847-ffff04ceaba6
document_version_independent_id: 921b028e-1c03-2051-0847-ffff04ceaba6
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/concept-custom-url-domain.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/concept-custom-url-domain
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/concept-custom-url-domain.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b5e53e15-0a76-4936-b270-8b2badca62ac
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6908a4c7-0b59-4f8b-a00e-59c83ae0a04a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: cf65403e-942e-010c-bc63-617448950715
---

# Overview of custom URL domains for External ID - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

A custom URL domain allows you to brand your application’s sign-in endpoints with your own custom URL domain instead of Microsoft’s default domain name.

[![Screenshot demonstrates an External ID custom URL domain user experience.](media/concept-custom-url-domain/custom-domain-user-experience-small.png)](media/concept-custom-url-domain/custom-domain-user-experience.png#lightbox)

Using a verified custom URL domain has several benefits:

- It provides a more consistent user experience. From the user's perspective, they remain in your domain during the sign in process rather than redirecting to the default domain *&lt;tenant-name&gt;.ciamlogin.com*.
- You mitigate the effect of [third-party cookie blocking](../../identity-platform/reference-third-party-cookies-spas) by staying in the same domain for your application during sign-in.

## How a custom URL domain works

A custom URL domain lets you use your verified custom URL domain names as your applications' sign-in authentication endpoints. When you add a new custom URL domain name, you can associate it with a custom URL domain. Then a reverse proxy service, such as [Azure Front Door](https://azure.microsoft.com/services/frontdoor/), can use the custom URL domain to direct sign-ins to your application.

The following diagram illustrates Azure Front Door integration:

![Diagram showing Azure Front Door integration with External ID.](media/concept-custom-url-domain/custom-domain-network-flow.png)

1. From an application, a user selects the sign in button, which takes them to the sign in page. This page specifies a custom URL domain.
2. The web browser resolves the custom URL domain to the Azure Front Door IP address. During Domain Name System (DNS) resolution, a canonical name (CNAME) record with a custom URL domain points to your Front Door default front-end host (for example, `contoso-frontend.azurefd.net`).
3. The traffic addressed to the custom URL domain (for example, `login.contoso.com`) is routed to the specified Front Door default front-end host (`contoso-frontend.azurefd.net`).
4. Azure Front Door invokes content using the `<tenant-name>.ciamlogin.com` default domain. The request to the endpoint includes the original custom URL domain.
5. External ID responds to the custom URL domain request by displaying the relevant content and the original custom URL domain.

Azure Front Door passes the user's original IP address, which is the IP address you see in the audit reporting.

Important

If the client sends an `x-forwarded-for` header to Azure Front Door, External ID will use the originator's `x-forwarded-for` as the user's IP address for Conditional Access evaluation and the `{Context:IPAddress}` claims resolver.

## Considerations and limitations

When using custom URL domains:

- You can set up multiple custom URL domains. For the maximum number of supported custom URL domains, see [Microsoft Entra service limits and restrictions](../../identity/users/directory-service-limits-restrictions) for Microsoft Entra, and [Azure subscription and service limits, quotas, and constraints](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-front-door-classic-limits) for Azure Front Door.
- You can use Azure Front Door, which is a separate Azure service that incurs extra charges. For more information, see [Front Door pricing](https://azure.microsoft.com/pricing/details/frontdoor). Your Azure Front Door instance can be hosted in a different subscription than your external tenant.
- If you have multiple applications, migrate them all to the custom URL domain because the browser stores the session under the domain name currently being used.

Important

- Azure Front Door: The connection from the browser to Azure Front Door should always use IPv4 instead of IPv6.
- Social identity providers: Custom URL domains now support Google and Facebook in addition to Apple.

## Blocking the default domain

For added security, we recommend blocking the default domain. After you configure custom URL domains, users will still be able to access the default domain name *&lt;tenant-name&gt;.ciamlogin.com*. You need to block access to the default domain so that attackers can't use it to access your apps or run distributed denial-of-service (DDoS) attacks. To block access to the default domain, [open a support ticket](../../fundamentals/how-to-get-support) and submit a request.

Caution

Make sure your custom URL domain works properly before you submit a request to block the default domain.

### Feature impact and workarounds

Blocking the default domain will disable certain features that depend on it. However, you can maintain functionality for the features outlined in the following table by configuring them with your custom URL domain.

| Feature | Workaround |
| --- | --- |
| Run now | In the Microsoft Entra admin center, update the URL used by the "Run now" feature in the get started guide and the user flow pane with your custom URL domain. In the browser URL, replace `{your_domain}.ciamlogin.com` with your custom URL domain `{your_custom_URL_domain}/{your_tenant_ID}`. |
| Get started samples | Configure the samples in the get started guide with your custom URL domain. For detailed instructions, refer to the documentation for each sample. For example, see the “Use custom URL domain” section in the [Vanilla JavaScript single-page app tutorial](../../identity-platform/tutorial-single-page-app-javascript-configure-authentication). |
| Power Pages with External ID | When using [External ID with your Power Pages site](/en-us/power-pages/security/authentication/entra-external-id), update the site settings with your custom URL domain. In the Power Pages identity provider configuration page, replace the Authority URL field, which contains `{your_domain}.ciamlogin.com`, with your custom URL domain `{your_custom_URL_domain}/{your_tenant_ID}`. |
| Azure App Service with External ID | When using [External ID with Azure App Service](/en-us/azure/app-service/scenario-secure-app-authentication-app-service), edit the identity provider and change the Issuer URL field from `{your_domain}.ciamlogin.com` to your custom URL domain `{your_custom_URL_domain}/{your_tenant_ID}`. |
| Visual Studio Code Extension | In the [Visual Studio Code extension](visual-studio-code-extension), add your custom URL domain to the application's MSAL configuration so the application and the “Run it now” feature work properly. Change the authority in the authconfig file from `{your_domain}.ciamlogin.com` to `{your_custom_URL_domain}/{your_tenant_ID}`, and add the known authorities with your custom URL domain. |
| Visual Studio with External ID | In the appsettings.json file, add your custom URL domain followed by the tenant ID, and add the known authorities with your custom URL domain. |
| GitHub samples | Certain samples, such as [OpenAI Chat Application with Microsoft Entra Authentication (Python)](https://github.com/Azure-Samples/openai-chat-app-entra-auth-builtin/blob/main/README.md), need your custom URL domain. When setting up the sample, set the AZURE\_AUTH\_LOGIN\_ENDPOINT to your custom URL domain. |