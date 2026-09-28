---
layout: Conceptual
title: Add an identity provider to a user flow - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-add-identity-provider-to-user-flow-customers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to add a configured external identity provider (OIDC, SAML/WS-Fed, or social) to a user flow in Microsoft Entra External ID so it appears on the sign-in page for self-service sign-up.
ms.topic: how-to
ms.date: 2026-05-29T00:00:00.0000000Z
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: f5844060-c9a3-d212-5247-4a91f8c10382
document_version_independent_id: f5844060-c9a3-d212-5247-4a91f8c10382
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/how-to-add-identity-provider-to-user-flow-customers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/how-to-add-identity-provider-to-user-flow-customers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/how-to-add-identity-provider-to-user-flow-customers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c77bc83e-f0b0-4b63-836e-6630e606bf7c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b98eda1f-6af8-444f-bbfb-7f2366948cbc
platformId: fc4adae6-c2e6-0f9a-502c-28e7995e8b67
---

# Add an identity provider to a user flow - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to external tenants.](../media/common/applies-to-yes.png) External tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

After you configure an external identity provider in your external tenant, you need to add it to a user flow to make it available on the sign-in page.

For steps on configuring identity providers, see:

- [Configure a custom OIDC identity provider](how-to-custom-oidc-federation-customers)
- [Add a Microsoft Entra ID tenant as an OIDC identity provider](how-to-entra-id-federation-customers)
- [Configure SAML/WS-Fed IdP federation](../direct-federation)
- [Add Google as an identity provider](how-to-google-federation-customers)
- [Add Facebook as an identity provider](how-to-facebook-federation-customers)
- [Add Apple as an identity provider](how-to-apple-federation-customers)
- [Add Microsoft account as an identity provider](how-to-microsoft-accounts-federation-customers)

## Prerequisites

- An [external tenant](how-to-create-external-tenant-portal).
- A registered application in the tenant.
- A configured identity provider (see links above).
- A [sign-up and sign-in user flow](how-to-user-flow-sign-up-sign-in-customers).

## Add the identity provider to a user flow

To add a configured identity provider to a user flow, follow these steps:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [External ID User Flow Administrator](../../identity/role-based-access-control/permissions-reference#external-id-user-flow-administrator).
2. Switch to your external tenant by selecting the **Settings** icon in the top menu and choosing the external tenant.
3. Browse to **Entra ID** &gt; **External Identities** &gt; **User flows**.
4. Select the user flow where you want to add the identity provider.

    ![Screenshot of the External Identities User flows page showing the user flow list.](media/how-to-add-identity-provider-to-user-flow-customers/select-user-flow.png)
5. Under **Settings**, select **Identity providers**.
6. Under **Other Identity Providers**, select the identity provider you want to add.

    ![Screenshot of the Identity providers page showing the Other Identity Providers section.](media/how-to-add-identity-provider-to-user-flow-customers/select-identity-provider.png)
7. Select **Save**.