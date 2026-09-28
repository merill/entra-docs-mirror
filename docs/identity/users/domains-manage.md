---
layout: Conceptual
title: Add and verify custom domain names - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/users/domains-manage
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kenwith
ms.author: kenwith
ms.service: entra-id
ms.subservice: users
manager: dougeby
description: Management concepts and how-tos for managing a domain name in Microsoft Entra ID
ms.topic: how-to
ms.date: 2026-04-07T00:00:00.0000000Z
ms.reviewer: sumitp
ms.custom: it-pro
ai-usage: ai-assisted
locale: en-us
document_id: 67566e6a-ffb4-4adf-73b5-3d6c0c58cd05
document_version_independent_id: 9c9a6f63-ec87-0e45-9d0e-f5030041ab06
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/users/domains-manage.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/users/domains-manage
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/users/domains-manage.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 77e52d51-74bb-bf83-e46c-806353b5734f
---

# Add and verify custom domain names - Microsoft Entra ID | Microsoft Learn

## Overview

A domain name is an important part of the identifier for resources in many Microsoft Entra deployments. It's part of a user name or email address for a user, part of the address for a group, and is sometimes part of the app ID URI for an application. A resource in Microsoft Entra ID can include a domain name that's owned by the Microsoft Entra organization (sometimes called a tenant) that contains the resource. The [Domain Name Administrator](../role-based-access-control/permissions-reference#domain-name-administrator) role is the least privileged role required to manage domains in Microsoft Entra ID.

## Set the primary domain name for your Microsoft Entra organization

When your organization is created, the initial domain name, such as "contoso.onmicrosoft.com," is also the primary domain name. The primary domain is the default domain name for a new user when you create a new user. Setting a primary domain name streamlines the process for an administrator to create new users in the portal. To change the primary domain name:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Domain Name Administrator](../role-based-access-control/permissions-reference#domain-name-administrator).
2. Browse to **Entra ID** &gt; **Domain names**
3. Select **Custom domain names**.

    ![Screenshot of opening the user management page.](media/domains-manage/add-custom-domain.png)
4. Select the name of the domain that you want to be the primary domain.
5. Select the **Make primary** command. Confirm your choice when prompted.

    ![Screenshot of making a domain name the primary.](media/domains-manage/make-primary-domain.png)

You can change the primary domain name for your organization to be any verified custom domain that isn't federated. Changing the primary domain for your organization doesn't change the user name for any existing users.

## Add custom domain names to your Microsoft Entra organization

You can add up to 5000 managed domain names. If you're configuring all your domains for federation with on-premises Active Directory, you can add up to 2,500 domain names in each organization.

## Add subdomains of a custom domain

If you want to add a subdomain name such as ‘europe.contoso.com’ to your organization, you should first add and verify the root domain, such as contoso.com. Microsoft Entra ID automatically verifies the subdomain. To see that the subdomain you added is verified, refresh the domain list in the browser.

If you have already added a contoso.com domain to one Microsoft Entra organization, you can also verify the subdomain europe.contoso.com in a different Microsoft Entra organization. When adding the subdomain, you're prompted to add a TXT record in the Domain Name Server (DNS) hosting provider.

## What to do if you change the DNS registrar for your custom domain name

If you change the DNS registrars, there are no other configuration tasks in Microsoft Entra ID. You can continue using the domain name with Microsoft Entra ID without interruption. If you use your custom domain name with Microsoft 365, Intune, or other services that rely on custom domain names in Microsoft Entra ID, see the documentation for those services.

## Delete a custom domain name

You can delete a custom domain name from your Microsoft Entra ID if your organization no longer uses that domain name, or if you need to use that domain name with another Microsoft Entra organization.

To delete a custom domain name, you must first ensure that no resources in your organization rely on the domain name. You can't delete a domain name from your organization if:

- Any user has a user name, email address, or proxy address that includes the domain name.
- Any group has an email address or proxy address that includes the domain name.
- Any application in your Microsoft Entra ID has an app ID URI that includes the domain name.

You must change or delete any such resource in your Microsoft Entra organization before you can delete the custom domain name.

Note

To delete the custom domain, use an account with at least the [Domain Name Administrator](../role-based-access-control/permissions-reference#domain-name-administrator) role that is based on either the default domain (onmicrosoft.com) or a different custom domain (mydomainname.com).

## ForceDelete option

You can `ForceDelete` a domain name in the [Azure portal](https://portal.azure.com) or using [Microsoft Graph API](/en-us/graph/api/domain-forcedelete). These options use an asynchronous operation and update all references from the custom domain name like “user@contoso.com” to the initial default domain name such as "user@contoso.onmicrosoft.com."

To call **ForceDelete** in the Azure portal, you must ensure that there are fewer than 1,000 references to the domain name, and any references where Exchange is the provisioning service must be updated or removed in the [Exchange Admin Center (EAC)](/en-us/exchange/exchange-admin-center). This includes Exchange Mail-Enabled Security Groups and distributed lists. For more information, see [Removing mail-enabled security groups](/en-us/Exchange/recipients/mail-enabled-security-groups#Remove%20mail-enabled%20security%20groups). Also, the **ForceDelete** operation doesn't succeed if either of the following is true:

- You purchased a domain via Microsoft 365 domain subscription services
- You're a partner administering on behalf of another customer organization

The following actions are performed as part of the **ForceDelete** operation:

- Renames the UPN, EmailAddress, and ProxyAddress of users with references to the custom domain name to the initial default domain name.
- Renames the EmailAddress of groups with references to the custom domain name to the initial default domain name.
- Renames the identifierUris of applications with references to the custom domain name to the initial default domain name.
- Disables user accounts impacted by the ForceDelete option in the Microsoft Entra admin center and optionally when using the Graph API.

An error is returned when:

- The number of objects to be renamed is greater than 1000
- One of the applications to be renamed is a multitenant app

## Best practices for domain hygiene

Use a reputable registrar that provides ample notifications for domain name changes, registration expiry, a grace period for expired domains, and maintains high security standards for controlling who has access to your domain name configuration and TXT records. Keep your domain names current with your registrar, and verify TXT records for accuracy.

- If you purposefully are expiring your domain name or turning over ownership to someone else (separately from your Microsoft Entra tenant), you should delete it from your Microsoft Entra tenant before expiring or transferring.
- If you do allow your domain name to expire, if you're able to reactivate it/regain control of it, carefully review all TXT records with the registrar to ensure no tampering of your domain name took place.
- If you can't reactivate or regain control of your domain name immediately, you should delete it from your Microsoft Entra tenant. Don't read/re-verify until you're able to resolve ownership of the domain name and verify the full TXT record for correctness.

Note

Microsoft won't allow a domain name to be verified with more than one Microsoft Entra tenant. Once you delete a domain name from your tenant, you won't be able to re-add/re-verify it with your Microsoft Entra tenant if it is subsequently added and verified with another Microsoft Entra tenant.

## Frequently asked questions

**Q: Why is the domain deletion failing with an error that states that I have Exchange mastered groups on this domain name?** **A:** Today, certain groups like Mail-Enabled Security groups and distributed lists are provisioned by Exchange and need to be manually cleaned up in [Exchange Admin Center](/en-us/exchange/exchange-admin-center). There might be lingering ProxyAddresses, which rely on the custom domain name and will need to be updated manually to another domain name.

**Q: I am logged in as admin@contoso.com but I cannot delete the domain name “contoso.com”?** **A:** You can't reference the custom domain name you're trying to delete in your user account name. Ensure that your account with at least the [Domain Name Administrator](../role-based-access-control/permissions-reference#domain-name-administrator) role is using the initial default domain name (.onmicrosoft.com) such as admin@contoso.onmicrosoft.com. Sign in with a different account that has at least the [Domain Name Administrator](../role-based-access-control/permissions-reference#domain-name-administrator) role, such as admin@contoso.onmicrosoft.com or another custom domain name like “fabrikam.com” where the account is admin@fabrikam.com.

**Q: I clicked the Delete domain button and see `In Progress` status for the Delete operation. How long does it take? What happens if it fails?** **A:** The delete domain operation is an asynchronous background task that renames all references to the domain name. It might take up to 24 hours to complete. If domain deletion fails, ensure that you don’t have:

- Apps configured on the domain name with the appIdentifierURI
- Any mail-enabled group referencing the custom domain name
- More than 1000 references to the domain name
- The domain to be removed is set as the primary domain of your organization

Also note that the ForceDelete option won't work if the domain uses Federated authentication type. In that case the users/groups on the domain must be renamed or removed using the on-premises Active Directory before reattempting the domain removal. If you find that any of the conditions haven’t been met, manually clean up the references, and try to delete the domain again.

## Use PowerShell or the Microsoft Graph API to manage domain names

Most management tasks for domain names in Microsoft Entra ID can also be completed using Microsoft PowerShell, or programmatically using the Microsoft Graph API.

- [Using PowerShell to manage domain names in Microsoft Entra ID](/en-us/powershell/module/azuread/?preserve-view=true#domains)
- [`Domain` resource type](/en-us/graph/api/resources/domain)