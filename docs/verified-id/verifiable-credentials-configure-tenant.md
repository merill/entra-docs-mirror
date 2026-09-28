---
layout: Conceptual
title: Tutorial - Advanced Microsoft Entra Verified ID setup - Microsoft Entra Verified ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-tenant
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra-verified-id
manager: dougeby
description: In this tutorial, you learn how to manually configure your tenant to support the Verified ID service.
ms.topic: tutorial
ms.date: 2025-04-30T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, sfi-image-nochange
locale: en-us
document_id: f84b158e-eebc-7d96-0992-8864316ddf5c
document_version_independent_id: 8909ba9b-bf26-fb5c-29f0-76244984e75a
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/verified-id/verifiable-credentials-configure-tenant.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: verified-id/verifiable-credentials-configure-tenant
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/verified-id/verifiable-credentials-configure-tenant.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f488294d-f483-456e-94e3-755f933b811b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/02662057-0b9b-40f4-a3c7-537125b6d283
platformId: 972d7054-857c-d384-e971-0532fc3fc005
---

# Tutorial - Advanced Microsoft Entra Verified ID setup - Microsoft Entra Verified ID | Microsoft Learn

## Overview

Advanced Verified ID setup is the classic way of setting up Verified ID where you, as an admin, manually configure various components. This includes setting up Azure Key Vault, registering your decentralized ID, and verifying your domain. The advanced setup gives you full control over the configuration process, ensuring that every detail meets your organization's specific requirements. It's ideal for enterprises that need a customized setup.

Advanced setup involves the following steps:

1. **Configure Azure Key Vault**: Securely store and manage the keys used for signing and verifying credentials.
2. **Register Decentralized ID**: Create and register your decentralized identifier (DID) to establish a trusted identity.
3. **Verify Domain**: Ensure your domain is correctly linked to your DID, providing a trusted source for your credentials.

In this tutorial, you learn how to:

- Create an Azure Key Vault instance.
- Configure the Verified ID service using the advanced setup.
- Register an application in Microsoft Entra ID.

The following diagram illustrates the Verified ID architecture and the component you configure.

![Diagram that illustrates the Microsoft Entra Verified ID architecture.](media/verifiable-credentials-configure-tenant/verifiable-credentials-architecture.png)

## Prerequisites

- Ensure that you have the [Authentication Policy Administrator](../identity/role-based-access-control/permissions-reference#authentication-policy-administrator) permission for the directory you want to configure. If you need to perform app registration tasks, you'll also need the [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator) permission. The [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator) role also has these permissions but should only be used if no other role combination meets your needs.
- Ensure that you have the [contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor) role for the Azure subscription or the resource group where you are deploying Azure Key Vault.
- Ensure that you provide access permissions for Key Vault. For more information, see [Provide access to Key Vault keys, certificates, and secrets with an Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide).

## Create a key vault

Note

The Azure Key Vault that you use to set up the Verified ID service must have [Key Vault Access Policy](/en-us/azure/key-vault/general/assign-access-policy) for its Permission model. There's currently a limitation if the Key Vault has Azure role-based access control.

[Azure Key Vault](/en-us/azure/key-vault/general/basic-concepts) is a cloud service that enables the secure storage and access management of secrets and keys. The Verified ID service stores public and private keys in Azure Key Vault. These keys are used to sign and verify credentials.

If you don't have an Azure Key Vault instance available, follow [these steps](/en-us/azure/key-vault/general/quick-create-portal) to create a key vault using the Azure portal. The Azure Key Vault that you use to set up the Verified ID service must have [Key Vault Access Policy](/en-us/azure/key-vault/general/assign-access-policy) for its Permission model instead of Azure role-based access control.

Note

By default, the vault's creator account is the only one with access. The Verified ID service needs access to the key vault. You must [authenticate your key vault](/en-us/azure/key-vault/general/basic-concepts), allowing the account used during configuration to create and delete keys. The account used during configuration also requires permissions to sign so that it can create the domain binding for Verified ID. If you use the same account while testing, modify the default policy to grant the account sign permission, in addition to the default permissions granted to vault creators.

### Manage access to the key vault

Before you can set up Verified ID, you need Key Vault [access](/en-us/azure/key-vault/general/rbac-guide). Provide access permissions to your key vault for both the Verified ID administrator account, and for the Request Service API principal that you created.

After you create your key vault, Verifiable Credentials generates a set of keys used to provide message security. These keys are stored in Key Vault. You use a key set for signing verifiable credentials.

## Set up Verified ID

![Screenshot that shows how to set up Verifiable Credentials.](media/verifiable-credentials-configure-tenant/verifiable-credentials-setup-advanced-1-2-3.png)

To set up Verified ID, follow these steps:

1. Sign in to the **Microsoft Entra admin center** with the **Authentication Policy Administrator** role.
2. From the left menu, select **Overview** under **Verified ID**.
3. From the middle menu, select **Setup** tab and then select **Advanced Setup**.
4. Select **Configure organization settings**.
5. Set up your organization by providing the following information:

    1. **Organization name**: Enter a name to reference your business within Verified IDs. Your customers don't see this name.
    2. **Trusted domain**: Enter a domain name. The name you specify is added to a service endpoint in your decentralized identity (DID) document. The domain is what binds your DID to something tangible that the user might know about your business. Microsoft Authenticator and other digital wallets use this information to validate that your DID is linked to your domain. If the wallet can verify the DID, it displays a verified symbol. If the wallet can't verify the DID, it informs the user that the credential issuer is an organization it couldn't validate.

        Important

        The domain can't be a redirect. Otherwise, the DID and domain can't be linked. Make sure to use HTTPS for the domain. For example: `https://did.woodgrove.com`. Also ensure that the Key Vault's Permission Model is set to Vault Access Policy.
    3. **Key vault**: Select the key vault that you created earlier.
6. Select **Save**.

    ![Screenshot that shows how to set up Verifiable Credentials first step.](media/verifiable-credentials-configure-tenant/verifiable-credentials-advanced-setup-save.png)

## Register an application in Microsoft Entra ID

Your application needs to get access tokens when it wants to call into Microsoft Entra Verified ID so it can issue or verify credentials. To get access tokens, you have to register an application and grant API permission for the Verified ID Request Service. For example, use the following steps for a web application:

1. Sign in to the **Microsoft Entra admin center** with appropriate administrator permissions.
2. Select **Microsoft Entra ID**.
3. Under **Applications**, select **App registrations** &gt; **New registration**.

    ![Screenshot that shows how to select a new application registration.](media/verifiable-credentials-configure-tenant/register-app.png)
4. Enter a display name for your application. For example: *verifiable-credentials-app*.
5. For **Supported account types**, select **Accounts in this organizational directory only (Default Directory only - Single tenant)**.
6. Select **Register** to create the application.

    ![Screenshot that shows how to register the verifiable credentials app.](media/verifiable-credentials-configure-tenant/register-app-properties.png)

### Grant permissions to get access tokens

In this step, you grant permissions to the **Verifiable Credentials Service Request** Service principal.

To add the required permissions, follow these steps:

1. Stay in the **verifiable-credentials-app** application details page. Select **API permissions** &gt; **Add a permission**.

    ![Screenshot that shows how to add permissions to the verifiable credentials app.](media/verifiable-credentials-configure-tenant/add-app-api-permissions.png)
2. Select **APIs my organization uses**.
3. Search for the **Verifiable Credentials Service Request** service principal and select it.

    ![Screenshot that shows how to select the service principal.](media/verifiable-credentials-configure-tenant/add-app-api-permissions-select-service-principal.png)
4. Choose **Application Permission**, and expand **VerifiableCredential.Create.All**.

    ![Screenshot that shows how to select the required permissions.](media/verifiable-credentials-configure-tenant/add-app-api-permissions-verifiable-credentials.png)
5. Select **Add permissions**.
6. Select **Grant admin consent for &lt;your tenant name&gt;**.

You can choose to grant issuance and presentation permissions separately if you prefer to segregate the scopes to different applications.

![Screenshot that shows how to select granular permissions for issuance or presentation.](media/verifiable-credentials-configure-tenant/granular-app-permissions.png)

## Register decentralized ID and verify domain ownership

After Azure Key Vault is set up, and the service has a signing key, you must complete steps 2 and 3 in the setup.

![Screenshot that shows how to set up Verifiable Credentials step 2 and 3.](media/verifiable-credentials-configure-tenant/verifiable-credentials-getting-started-step-2-3.png)

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) with the [Authentication Policy Administrator](../identity/role-based-access-control/permissions-reference#authentication-policy-administrator) role.
2. Select **Verified ID**.
3. From the left menu, select **Overview**.
4. From the middle menu, select **Register decentralized ID** to register your DID document, as per instructions in article [How to register your decentralized ID for did:web](how-to-register-didwebsite). You must complete this step before you can continue to verify your domain.
5. From the middle menu, select **Verify domain ownership** to verify your domain, as per instructions in article [Verify domain ownership to your Decentralized Identifier (DID)](how-to-dnsbind).

After you've successfully completed the verification steps, and have green checkmarks on all three steps, you're ready to continue to the next tutorial.