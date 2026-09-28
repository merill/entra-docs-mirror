---
layout: Conceptual
title: Register a Microsoft Entra app and create a service principal - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/howto-create-service-principal-portal
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Create a new Microsoft Entra app and service principal to manage access to resources with role-based access control in Azure Resource Manager.
manager: pmwongera
ms.date: 2025-05-26T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange
locale: en-us
document_id: 11aaa091-1108-52f6-0066-0f4e939aeef4
document_version_independent_id: dbc7e37e-87a7-c124-3e4c-47aa060e6cf3
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/howto-create-service-principal-portal.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/howto-create-service-principal-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/howto-create-service-principal-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 91d42b79-5ace-6758-700d-34d00a55c124
---

# Register a Microsoft Entra app and create a service principal - Microsoft identity platform | Microsoft Learn

In this article, you'll learn how to create a Microsoft Entra application and service principal that can be used with role-based access control (RBAC). When you register a new application in Microsoft Entra ID, a service principal is automatically created for the app registration. The service principal is the app's identity in the Microsoft Entra tenant. Access to resources is restricted by the roles assigned to the service principal, giving you control over which resources can be accessed and at which level. For security reasons, it's always recommended to use service principals with automated tools rather than allowing them to sign in with a user identity.

This example is applicable for line-of-business applications used within one organization. You can also [use Azure PowerShell](howto-authenticate-service-principal-powershell) or the [Azure CLI](/en-us/cli/azure/create-an-azure-service-principal-azure-cli) to create a service principal.

Important

Instead of creating a service principal, consider using managed identities for Azure resources for your application identity. If your code runs on a service that supports managed identities and accesses resources that support Microsoft Entra authentication, managed identities are a better option for you. To learn more about managed identities for Azure resources, including which services currently support it, see [What is managed identities for Azure resources?](../identity/managed-identities-azure-resources/overview).

For more information on the relationship between app registration, application objects, and service principals, read [Application and service principal objects in Microsoft Entra ID](app-objects-and-service-principals).

## Prerequisites

To register an application in your Microsoft Entra tenant, you need:

- A Microsoft Entra user account. If you don't already have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Sufficient permissions to register an application with your Microsoft Entra tenant, and assign to the application a role in your Azure subscription. To complete these tasks, you'll need the `Application.ReadWrite.All` permission.

## Register an application with Microsoft Entra ID and create a service principal

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **App registrations** then select **New registration**.
3. Give the application a name, such as *example-app*.
4. Under **Supported account types**, select *Accounts in this organizational directory only*.
5. Under **Redirect URI**, select **Web** for the type of application you want to create. Enter the URI where the access token is sent to.
6. Select **Register**.

    ![Screenshot showing the application registration page.](media/howto-create-service-principal-portal/create-app.png)

## Assign a role to the application

To access resources in your subscription, you must assign a role to the application. This needs to be done through the Azure portal. Decide which role offers the right permissions for the application. To learn about the available roles, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

You can set the scope at the level of the subscription, resource group, or resource. Permissions are inherited to lower levels of scope.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. In the search bar at the top of the screen, search for and select **Subscriptions**.
3. In the new window, select the subscription to want to modify. If you don't see the subscription you're looking for, select **global subscriptions filter**. Make sure the subscription you want is selected for the tenant.
4. In the left pane, select **Access control (IAM)**.
5. Select **Add**, then select **Add role assignment**.
6. In the **Role** tab, select the role you wish to assign to the application in the list, then select **Next**.
7. On the **Members** tab, for **Assign access to**, select **User, group, or service principal**.
8. Select **Select members**. By default, Microsoft Entra applications aren't displayed in the available options. To find your application, search for it by name.
9. Select the **Select** button, then select **Review + assign**.

    ![Screenshot showing role assignment, and highlighting how to add members.](media/howto-create-service-principal-portal/add-role-assignment.png)

Your service principal is set up. You can start using it to run your scripts or apps. To manage your service principal (permissions, user consented permissions, see which users have consented, review permissions, see sign in information, and more), go to **Enterprise applications**.

The next section shows how to get values that are needed when signing in programmatically.

## Sign in to the application

When programmatically signing in, you pass the directory (tenant) ID and the application (client) ID in your authentication request. You also need a certificate or an authentication key. To obtain the directory ID and application ID:

1. Open the [Microsoft Entra admin center](https://entra.microsoft.com)**Home** page.
2. Browse to **Entra ID** &gt; **App registrations**, then select your application.
3. On the app's overview page, copy the Directory (tenant) ID value and store it in your application code.
4. Copy the Application (client) ID value and store it in your application code.

## Set up authentication

There are two types of authentication available for service principals: password-based authentication (application secret) and certificate-based authentication. *We recommend using a trusted certificate issued by a certificate authority*, but you can also create an application secret or create a self-signed certificate for testing.

### Option 1 (recommended): Upload a trusted certificate issued by a certificate authority

To upload the certificate file:

1. Browse to **Entra ID** &gt; **App registrations**, then select your application.
2. Select **Certificates & secrets**.
3. Select **Certificates**, then select **Upload certificate** and then select the certificate file to upload.
4. Select **Add**. Once the certificate is uploaded, the thumbprint, start date, and expiration values are displayed.

After registering the certificate with your application in the application registration portal, enable the [confidential client application](authentication-flows-app-scenarios#single-page-public-client-and-confidential-client-applications) code to use the certificate.

### Option 2: Testing only: Create and upload a self-signed certificate

Optionally, you can create a self-signed certificate for *testing purposes only*. To create a self-signed certificate, open Windows PowerShell and run [New-SelfSignedCertificate](/en-us/powershell/module/pki/new-selfsignedcertificate) with the following parameters to create the certificate in the user certificate store on your computer:

```powershell
$cert=New-SelfSignedCertificate -Subject "CN=DaemonConsoleCert" -CertStoreLocation "Cert:\CurrentUser\My"  -KeyExportPolicy Exportable -KeySpec Signature
```

Export this certificate to a file using the [Manage User Certificate](/en-us/dotnet/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in) MMC snap-in accessible from the Windows Control Panel.

1. Select **Run** from the **Start** menu, and then enter **certmgr.msc**. The Certificate Manager tool for the current user appears.
2. To view your certificates, under **Certificates - Current User** in the left pane, expand the **Personal** directory.
3. Right-click on the certificate you created, select **All tasks-&gt;Export**.
4. Follow the Certificate Export wizard.

To upload the certificate:

1. Browse to **Entra ID** &gt; **App registrations**, then select your application.
2. Select **Certificates & secrets**.
3. Select **Certificates**, then select **Upload certificate** and then select the certificate (an existing certificate or the self-signed certificate you exported).
4. Select **Add**.

After registering the certificate with your application in the application registration portal, enable the [confidential client application](authentication-flows-app-scenarios#single-page-public-client-and-confidential-client-applications) code to use the certificate.

### Option 3: Create a new client secret

If you choose not to use a certificate, you can create a new client secret.

1. Browse to **Entra ID** &gt; **App registrations**, then select your application.
2. Select **Certificates & secrets**.
3. Select **Client secrets**, and then select **New client secret**.
4. Provide a description of the secret, and a duration.
5. Select **Add**.

Once you've saved the client secret, the value of the client secret is displayed. This is only displayed once, so copy this value and store it where your application can retrieve it, usually where your application keeps values like `clientId`, or `authority` in the source code. You'll provide the secret value along with the application's client ID to sign in as the application.

## Configure access policies on resources

You might need to configure extra permissions on resources that your application needs to access. For example, you must also [update a key vault's access policies](/en-us/azure/key-vault/general/security-features#privileged-access) to give your application access to keys, secrets, or certificates.

To configure access policies:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select your key vault and select **Access policies**.
3. Select **Add access policy**, then select the key, secret, and certificate permissions you want to grant your application. Select the service principal you created previously.
4. Select **Add** to add the access policy, then select **Save**.

    ![Add access policy](media/howto-create-service-principal-portal/add-access-policy.png)