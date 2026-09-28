---
layout: Conceptual
title: Admin takeover of an unmanaged directory - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/domains-admin-takeover
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: How to take over a DNS domain name in an unmanaged Microsoft Entra organization (shadow tenant).
ms.topic: how-to
ms.date: 2026-06-18T00:00:00.0000000Z
ms.reviewer: sumitp
ai-usage: ai-assisted
ms.custom: it-pro, no-azure-ad-ps-ref, sfi-ga-nochange
locale: en-us
document_id: cd934d58-08f8-a3ca-2686-0006b0b8f74a
document_version_independent_id: 84d9cab3-09b7-95ba-83ea-435ca0ccbb47
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/domains-admin-takeover.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/domains-admin-takeover
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/domains-admin-takeover.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: e67c5f1a-9852-156c-ce43-c8f89eb276d2
---

# Admin takeover of an unmanaged directory - Microsoft Entra ID | Microsoft Learn

## Overview

This article describes two ways to take over a DNS domain name in an unmanaged directory in Microsoft Entra ID. When a self-service user signs up for a cloud service that uses Microsoft Entra ID, they're added to an unmanaged Microsoft Entra directory based on their email domain. For more about self-service or "viral" sign-up for a service, see [What is self-service sign-up for Microsoft Entra ID?](directory-self-service-signup)

## Decide how you want to take over an unmanaged directory

During the process of admin takeover, you can prove ownership as described in [Add a custom domain name to Microsoft Entra ID](../../fundamentals/add-custom-domain). The next sections explain the admin experience in more detail, but here's a summary:

- When you perform an "internal" admin takeover of an unmanaged directory, you're assigned the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role of the unmanaged directory. No users, domains, or service plans are migrated to any other directory you administer.
- When you perform an "external" admin takeover of an unmanaged directory, you add the DNS domain name of the unmanaged directory to your managed Azure directory. When you add the domain name, a mapping of users to resources is created in your managed directory so that users can continue to access services without interruption.

Note

An "internal" admin takeover requires you to have some level of access to the unmanaged directory. If you're unable to access the directory that you're attempting to takeover, you need to perform an "external" admin takeover.

## Internal admin takeover

Some products that include SharePoint and OneDrive, such as Microsoft 365, don't support external takeover. If that's your scenario, or if you're an admin and want to take over an unmanaged or "shadow" Microsoft Entra organization created by users who used self-service sign-up, you can do this with an internal admin takeover.

1. Create a user context in the unmanaged organization through signing up for Power BI. For convenience of example, these steps assume that path.
2. Open the [Power BI site](https://powerbi.microsoft.com) and select **Start Free**. Enter a user account that uses the domain name for the organization; for example, `admin@fourthcoffee.xyz`. After you enter in the verification code, check your email for the confirmation code.
3. In the confirmation email from Power BI, select **Yes, that's me**.
4. Sign in to the [Microsoft 365 admin center](https://portal.office.com/admintakeover) with the Power BI user account.

    ![Screenshot of the Microsoft 365 Welcome page.](media/domains-admin-takeover/m365-welcome-screen.png)
5. You receive a message that instructs you to **Become the Admin** of the domain name that was already verified in the unmanaged organization. select **Yes, I want to be the admin**.

    ![Screenshot for Become the Admin.](media/domains-admin-takeover/become-admin-first.png)
6. Add the TXT record to prove that you own the domain name **fourthcoffee.xyz** at your domain name registrar. In this example, it's GoDaddy.com.

    ![Screenshot of Add a TXT record for the domain name.](media/domains-admin-takeover/become-admin-txt-record.png)

When the DNS TXT records are verified at your domain name registrar, you can manage the Microsoft Entra organization.

When you complete the preceding steps, you're now the Global Administrator of the Fourth Coffee organization in Microsoft 365. To integrate the domain name with your other Azure services, you can remove it from Microsoft 365 and add it to a different managed organization in Azure.

### Add the domain name to a managed organization in Microsoft Entra ID

1. Open the [Microsoft 365 admin center](https://admin.microsoft.com).
2. Select the **Users** tab, and create a new user account with a name like *user@fourthcoffeexyz.onmicrosoft.com* that doesn't use the custom domain name.
3. Ensure that the new user account has Global Administrator privileges for the Microsoft Entra organization.
4. Open the **Domains** tab in the Microsoft 365 admin center, select the domain name and select **Remove**.

    ![Screenshot showing the option to remove the domain name from Microsoft 365.](media/domains-admin-takeover/remove-domain-from-o365.png)
5. If you have any users or groups in Microsoft 365 that reference the removed domain name, they must be renamed to the .onmicrosoft.com domain. If you force delete the domain name, all users are automatically renamed, in this example to *user@fourthcoffeexyz.onmicrosoft.com*.
6. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Administrator](../role-based-access-control/permissions-reference#global-administrator).
7. In the search box at the top of the page, search for **Domain Names**.
8. Select **+ Add custom domain names**, then add the domain name. You have to enter the DNS TXT records to verify ownership of the domain name.

    ![Screenshot showing the domain verified as added to Microsoft Entra ID.](media/domains-admin-takeover/add-domain.png)

Note

Any users of Power BI or Azure Rights Management service who have licenses assigned in the Microsoft 365 organization must save their dashboards if the domain name is removed. They must sign in with a user name like *user@fourthcoffeexyz.onmicrosoft.com* rather than *user@fourthcoffee.xyz*.

## External admin takeover

If you already manage an organization with Azure services or Microsoft 365, you can't add a custom domain name if it's already verified in another Microsoft Entra organization. However, from your managed organization in Microsoft Entra ID you can take over an unmanaged organization as an external admin takeover. The general procedure follows the article [Add a custom domain to Microsoft Entra ID](../../fundamentals/add-custom-domain).

When you verify ownership of the domain name, Microsoft Entra ID removes the domain name from the unmanaged organization and moves it to your existing organization. External admin takeover of an unmanaged directory requires the same DNS TXT validation process as internal admin takeover. The difference is that the following are also moved over with the domain name:

- Users
- Subscriptions
- License assignments

### Support for external admin takeover

External admin takeover is supported by the following online services:

- Azure Rights Management
- Exchange Online

The supported service plans include:

- Power Apps Free
- Power Automate Free
- RMS for individuals
- Microsoft Stream
- Dynamics 365 free trial

External admin takeover isn't supported for any service that has service plans that include SharePoint, OneDrive, or Skype For Business; for example, through an Office free subscription.

Note

External admin takeover isn't supported cross cloud boundaries (ex. Azure Commercial to Azure Government). In these scenarios, it's recommended to perform External admin takeover into another Azure Commercial tenant, and then delete the domain from this tenant so you can verify successfully into the destination Azure Government tenant.

#### More information about RMS for individuals

For [RMS for individuals](/en-us/azure/information-protection/rms-for-individuals), when the unmanaged organization is in the same region as the organization that you own, the automatically created [Azure Information Protection organization key](/en-us/azure/information-protection/plan-implement-tenant-key) and [default protection templates](/en-us/azure/information-protection/configure-usage-rights#rights-included-in-the-default-templates) are additionally moved over with the domain name.

The key and templates aren't moved over when the unmanaged organization is in a different region. For example, if the unmanaged organization is in Europe and the organization that you own is in North America.

Although RMS for individuals is designed to support Microsoft Entra authentication to open protected content, it doesn't prevent users from also protecting content. If users did protect content with the RMS for individuals subscription, and the key and templates weren't moved over, that content isn't accessible after the domain takeover.

### PowerShell and Microsoft Graph API steps for external admin takeover

You can see these commands and API calls used in PowerShell example.

| Command or API call | Usage |
| --- | --- |
| `Connect-MgGraph` | When prompted, sign in to your managed organization with the `Domain.ReadWrite.All` scope. For delegated access, the signed-in user must have a supported Microsoft Entra role. [Domain Name Administrator](../role-based-access-control/permissions-reference#domain-name-administrator) is the least privileged role supported for domain verification. |
| `Get-MgDomain` | Shows your domain names associated with the current organization. |
| `New-MgDomain -BodyParameter @{Id="<your domain name>"; IsDefault="False"}` | Adds the domain name to organization as Unverified (no DNS verification has been performed yet). |
| `Get-MgDomain` | The domain name is now included in the list of domain names associated with your managed organization, but is listed as **Unverified**. |
| `Get-MgDomainVerificationDnsRecord` | Provides the information to put into a new DNS TXT record for the domain (MS=xxxxx). Verification might not happen immediately because it takes some time for the TXT record to propagate. |
| `Confirm-MgDomain -DomainId <domain name>` | Verifies ownership for standard domain verification scenarios. The current `Confirm-MgDomain` cmdlet doesn't expose a `-ForceTakeover` parameter. |
| `Invoke-MgGraphRequest` | Calls the Microsoft Graph [domain: verify](/en-us/graph/api/domain-verify?view=graph-rest-1.0&amp;preserve-view=true) API directly. For external admin takeover of an unmanaged domain, set the API's `forceTakeover` request body parameter to `true` after you add the required TXT record. |
| `Get-MgDomain` | The domain list now shows the domain name as **Verified**. |

Note

The unmanaged Microsoft Entra organization is deleted 10 days after a successful external admin takeover with the `forceTakeover` option.

### PowerShell example

1. Connect to Microsoft Graph using the credentials that were used to respond to the self-service offering:

    ```powershell
    Install-Module -Name Microsoft.Graph
    
    Connect-MgGraph -Scopes "Domain.ReadWrite.All"
    ```
2. Get a list of domains:

    ```powershell
    Get-MgDomain
    ```
3. Run the New-MgDomain cmdlet to add a new domain:

    ```powershell
    New-MgDomain -BodyParameter @{Id="<your domain name>"; IsDefault="False"}
    ```
4. Run the Get-MgDomainVerificationDnsRecord cmdlet to view the DNS challenge:

    ```powershell
    (Get-MgDomainVerificationDnsRecord -DomainId "<your domain name>" | ?{$_.recordtype -eq "Txt"}).AdditionalProperties.text
    ```

    For example:

    ```powershell
    (Get-MgDomainVerificationDnsRecord -DomainId "contoso.com" | ?{$_.recordtype -eq "Txt"}).AdditionalProperties.text
    ```
5. Copy the value (the challenge) that is returned from this command. For example:

    ```powershell
    MS=ms18939161
    ```
6. In your public DNS namespace, create a DNS txt record that contains the value that you copied in the previous step. The name for this record is the name of the parent domain, so if you create this resource record by using the DNS role from Windows Server, leave the Record name blank and just paste the value into the Text box.
7. Choose how to verify the challenge.

    For standard domain verification, run the [Confirm-MgDomain](/en-us/powershell/module/microsoft.graph.identity.directorymanagement/confirm-mgdomain?view=graph-powershell-1.0&amp;preserve-view=true) cmdlet:

    ```powershell
    Confirm-MgDomain -DomainId "<your domain name>"
    ```

    For example:

    ```powershell
    Confirm-MgDomain -DomainId "contoso.com"
    ```

    For external admin takeover of an unmanaged domain, use [Invoke-MgGraphRequest](/en-us/powershell/module/microsoft.graph.authentication/invoke-mggraphrequest?view=graph-powershell-1.0&amp;preserve-view=true) to call the Microsoft Graph [domain: verify](/en-us/graph/api/domain-verify?view=graph-rest-1.0&amp;preserve-view=true) API with `forceTakeover` set to `true`:

    ```powershell
    $body = @{
        forceTakeover = $true
    } | ConvertTo-Json
    
    Invoke-MgGraphRequest -Method POST `
        -Uri "https://graph.microsoft.com/v1.0/domains/<your domain name>/verify" `
        -Body $body `
        -ContentType "application/json"
    ```

    For example:

    ```powershell
    $body = @{
        forceTakeover = $true
    } | ConvertTo-Json
    
    Invoke-MgGraphRequest -Method POST `
        -Uri "https://graph.microsoft.com/v1.0/domains/contoso.com/verify" `
        -Body $body `
        -ContentType "application/json"
    ```

Note

The current `Confirm-MgDomain` cmdlet doesn't expose the `forceTakeover` request body parameter. Use `Invoke-MgGraphRequest` for external admin takeover scenarios that require `forceTakeover`.

A successful verification returns without an error. The `domain: verify` API returns a domain object in the response body.