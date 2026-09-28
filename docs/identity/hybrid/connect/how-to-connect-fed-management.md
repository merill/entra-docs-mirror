---
layout: Conceptual
title: Microsoft Entra Connect - AD FS management and customization - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-fed-management
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: boscoMW
ms.author: bmutunga
ms.service: entra-id
manager: pmwongera
description: This article discusses how to manage AD FS with Microsoft Entra Connect and customize the AD FS user sign-in experience with Microsoft Entra Connect and PowerShell.
keywords: AD FS, ADFS, AD FS management, AAD Connect, Connect, sign-in, AD FS customization, repair trust, M365, federation, relying party
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.tgt_pltfrm: na
ms.topic: how-to
ms.date: 2025-04-09T00:00:00.0000000Z
ms.subservice: hybrid-connect
ms.custom: sfi-image-nochange
locale: en-us
document_id: c6678472-1676-1396-63a8-f16bdf507f7a
document_version_independent_id: c63479c3-6fc2-c70a-a3ef-e9f577462e77
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/connect/how-to-connect-fed-management.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: azurepowershell
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/connect/how-to-connect-fed-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/connect/how-to-connect-fed-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: cc6a1c67-03b4-6808-7807-7fed55b0cdba
---

# Microsoft Entra Connect - AD FS management and customization - Microsoft Entra ID | Microsoft Learn

This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Microsoft Entra Connect.

You'll also learn about other common AD FS tasks that you might need to perform to completely configure an AD FS farm. These tasks are listed in the following table:

| Task | Description |
| --- | --- |
| **Manage AD FS** |  |
| Repair the trust | Learn how to repair the federation trust with Microsoft 365. |
| Federate with Microsoft Entra ID by using an alternative sign-in ID | Learn how to configure federation by using an alternative sign-in ID. |
| Add an AD FS server | Learn how to expand an AD FS farm with an extra AD FS server. |
| Add an AD FS Web Application Proxy (WAP) server | Learn how to expand an AD FS farm with an additional WAP server. |
| Add a federated domain | Learn how to add a federated domain. |
| [Update the TLS/SSL certificate](how-to-connect-fed-ssl-update) | Learn how to update the TLS/SSL certificate for an AD FS farm. |
| **Customize AD FS** |  |
| Add a custom company logo or illustration | Learn how to customize an AD FS sign-in page with a company logo and illustration. |
| Add a sign-in description | Learn how to add a sign-in page description. |
| Modify AD FS claim rules | Learn how to modify AD FS claims for various federation scenarios. |

## Manage AD FS

You can perform various AD FS-related tasks in Microsoft Entra Connect with minimal user intervention by using the Microsoft Entra Connect wizard. After you've finished installing Microsoft Entra Connect by running the wizard, you can run it again to perform other tasks.

Important

Please note that if you are configuring federation with AD FS or PingFederate you will need either an account with the global administrator role or an account that has the [hybrid identity administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) and [domain name administrator](../../role-based-access-control/permissions-reference#domain-name-administrator) roles. The configurations related to federation require permissions that the [hybrid identity administrator](../../role-based-access-control/permissions-reference#hybrid-identity-administrator) currently doesn't have but the [domain name administrator](../../role-based-access-control/permissions-reference#domain-name-administrator) role does.

## Repair the trust

You can use Microsoft Entra Connect to check the current health of the AD FS and Microsoft Entra ID trust and then take appropriate actions to repair the trust. To repair your Microsoft Entra ID and AD FS trust, do the following:

1. Select **Repair Microsoft Entra ID and ADFS Trust** from the list of tasks.

    ![Screenshot of the &quot;Additional tasks&quot; page for repairing the Microsoft Entra ID and AD FS trust.](media/how-to-connect-fed-management/repairadtrust1.png)
2. On the **Connect to Microsoft Entra ID** page, provide your Hybrid Identity Administrator credentials for Microsoft Entra ID, and then select **Next**.

    ![Screenshot that shows the &quot;Connect to Microsoft Entra ID&quot; page with example credentials entered.](media/how-to-connect-fed-management/repairadtrust2.png)
3. On the **Remote access credentials** page, enter the credentials for the domain administrator.

    ![Screenshot that shows the &quot;Remote access credentials&quot; page with example domain administrator credentials entered.](media/how-to-connect-fed-management/repairadtrust3.png)
4. Select **Next**.

    Microsoft Entra Connect checks for certificate health and shows any issues.

    ![Screenshot of the &quot;Certificates&quot; page displaying the state of the current certificates.](media/how-to-connect-fed-management/repairadtrust4.png)

    The **Ready to configure** page shows the list of actions that will be performed to repair the trust.

    ![Screenshot that shows the &quot;Ready to configure&quot; page with a list of actions to be performed.](media/how-to-connect-fed-management/repairadtrust5.png)
5. Select **Install** to repair the trust.

Note

Microsoft Entra Connect can repair or act on only certificates that are self-signed. Microsoft Entra Connect can't repair third-party certificates.

## Federate with Microsoft Entra ID by using alternateID

We recommend that you keep the *on-premises* User Principal Name (UPN) and the *cloud* User Principal Name the same. If the on-premises UPN uses a non-routable domain (for example, Contoso.local) or can't be changed because of local application dependencies, we recommend setting up an alternative sign-in ID. By using an alternative sign-in ID, you can configure a sign-in experience where users can sign in with an attribute other than their UPN, such as an email address.

The choice of UPN in Microsoft Entra Connect defaults to the userPrincipalName attribute in Active Directory. If you choose any other attribute for the UPN and are federating by using AD FS, Microsoft Entra Connect configures AD FS for an alternative sign-in ID.

An example of choosing a different attribute for the UPN is shown in the following image:

![Screenshot that shows the &quot;Microsoft Entra sign-in configuration&quot; page for choosing a different attribute for the UPN.](media/how-to-connect-fed-management/attributeselection.png)

Configuring an alternative sign-in ID for AD FS consists of two main steps:

1. **Configure the right set of issuance claims**: The issuance claim rules in the Microsoft Entra ID relying party trust are modified to use the selected UserPrincipalName attribute as the alternative ID of the user.
2. **Enable an alternative sign-in ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests by using the alternative ID. This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later. If the AD FS servers are 2012 R2, Microsoft Entra Connect checks for the presence of the required KB. If the KB isn't detected, a warning is displayed after the configuration is completed, as shown in the following image:

    ![Screenshot of the &quot;Configuration complete&quot; page displaying a warning for a missing KB on Windows Server 2012 R2.](media/how-to-connect-fed-management/kbwarning.png)

    If there's a missing KB, you can remedy the configuration by installing the required [KB2919355](https://go.microsoft.com/fwlink/?LinkID=396590). You can then follow the instructions in repair the trust.

Note

For more information about alternateID and steps to manually configure it, see [Configure an alternative sign-in ID](/en-us/windows-server/identity/ad-fs/operations/configuring-alternate-login-id).

## Add an AD FS server

Note

To add an AD FS server, Microsoft Entra Connect requires a PFX certificate. Therefore, you can perform this operation only if you configured the AD FS farm by using Microsoft Entra Connect.

1. Select **Deploy an additional Federation Server**, and then select **Next**.

    ![Screenshot of the &quot;Additional tasks&quot; pane for deploying an additional federation server.](media/how-to-connect-fed-management/addnewadfsserver1.png)
2. On the **Connect to Microsoft Entra ID** page, enter your Hybrid Identity Administrator credentials for Microsoft Entra ID, and then select **Next**.

    ![Screenshot that shows the &quot;Connect to Microsoft Entra ID&quot; page with sample credentials entered.](media/how-to-connect-fed-management/addnewadfsserver2.png)
3. Provide the domain administrator credentials.

    ![Screenshot that shows the &quot;Connect to Microsoft Entra ID&quot; page, with sample credentials entered.](media/how-to-connect-fed-management/addnewadfsserver3.png)
4. Microsoft Entra Connect asks for the password of the PFX file that you provided when you configured your new AD FS farm with Microsoft Entra Connect. Select **Enter Password** to provide the password for the PFX file.

    ![Screenshot of the &quot;Domain Administrator credentials&quot; page, with example credentials entered.](media/how-to-connect-fed-management/addnewadfsserver4.png)

    ![Screenshot that shows the &quot;Specify SSL certificate&quot; page after a password for the PFX file is entered.](media/how-to-connect-fed-management/addnewadfsserver5.png)
5. On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.

    ![Screenshot that shows the &quot;AD FS Servers&quot; page.](media/how-to-connect-fed-management/addnewadfsserver6.png)
6. Select **Next**, and then continue completing the final **Configure** page.

    After Microsoft Entra Connect has finished adding the servers to the AD FS farm, you'll be given the option to verify the connectivity.

    ![Screenshot that shows the &quot;Ready to configure&quot; page with a list of actions to be completed after you select &quot;Install&quot;.](media/how-to-connect-fed-management/addnewadfsserver7.png)

    ![Screenshot that shows the &quot;Installation complete&quot; page.](media/how-to-connect-fed-management/addnewadfsserver8.png)

## Add an AD FS WAP server

Note

To add a Web Application Proxy server, Microsoft Entra Connect requires the PFX certificate. Therefore, you can perform this operation only after you've configured the AD FS farm by using Microsoft Entra Connect.

1. Select **Deploy Web Application Proxy** from the list of available tasks.

    ![Deploy Web Application Proxy](media/how-to-connect-fed-management/wapserver1.png)
2. Provide the Azure Hybrid Identity Administrator credentials.

    ![Screenshot that shows the &quot;Connect to Microsoft Entra ID&quot; page with an example username and password entered.](media/how-to-connect-fed-management/wapserver2.png)
3. On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Microsoft Entra Connect. ![Certificate password](media/how-to-connect-fed-management/wapserver3.png)

    ![Specify TLS/SSL certificate](media/how-to-connect-fed-management/wapserver4.png)
4. Add the server to be added as a WAP server. Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.

    ![Administrative server credentials](media/how-to-connect-fed-management/wapserver5.png)
5. On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.

    ![Proxy trust credentials](media/how-to-connect-fed-management/wapserver6.png)
6. On the **Ready to configure** page, the wizard shows the list of actions that will be performed.

    ![Screenshot that shows the &quot;Ready to configure&quot; page, with a list of actions to be performed.](media/how-to-connect-fed-management/wapserver7.png)
7. Select **Install** to finish the configuration. After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers. Select **Verify** to check connectivity.

    ![Installation complete](media/how-to-connect-fed-management/wapserver8.png)

## Add a federated domain

It's easy to add a domain to be federated with Microsoft Entra ID by using Microsoft Entra Connect. Microsoft Entra Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Microsoft Entra ID.

1. To add a federated domain, select **Add an additional Microsoft Entra domain**.

    ![Screenshot of the &quot;Additional tasks&quot; pane for selecting &quot;Add an additional Microsoft Entra domain&quot;.](media/how-to-connect-fed-management/additionaldomain1.png)
2. On the next page of the wizard, provide the Hybrid Administrator credentials for Microsoft Entra ID.

    ![Screenshot that shows the &quot;Additional tasks&quot; pane for selecting &quot;Add an additional Microsoft Entra domain&quot;.](media/how-to-connect-fed-management/additionaldomain2.png)
3. On the **Remote access credentials** page, provide the domain administrator credentials.

    ![Screenshot showing the &quot;Additional tasks&quot; pane for selecting &quot;Add an additional Microsoft Entra domain&quot;.](media/how-to-connect-fed-management/additionaldomain3.png)
4. On the next page, the wizard provides a list of Microsoft Entra domains that you can federate your on-premises directory with. Choose the domain from the list.

    ![Screenshot of the &quot;Additional tasks&quot; pane, showing how to add an additional Microsoft Entra domain.](media/how-to-connect-fed-management/additionaldomain4.png)

    After you choose the domain, the wizard informs you about further actions that it will take and the impact of the configuration. In some cases, if you select a domain that isn't yet verified in Microsoft Entra ID, the wizard helps you verify the domain. For more information, see [Add your custom domain name to Microsoft Entra ID](../../../fundamentals/add-custom-domain).
5. Select **Next**.

    The **Ready to configure** page lists the actions that Microsoft Entra Connect will perform.

    ![Screenshot of the &quot;Additional tasks&quot; pane that shows how to add an additional Microsoft Entra domain.](media/how-to-connect-fed-management/additionaldomain5.png)
6. Select **Install** to finish the configuration.

Note

Users in the added federated domain must be synchronized before they can sign in to Microsoft Entra ID.

## Customize AD FS

The following sections provide details about some of the common tasks that you might have to perform to customize your AD FS sign-in page.

## Add a custom company logo or illustration

To change the logo of the company that's displayed on the **Sign-in** page, use the following PowerShell cmdlet and syntax.

Note

The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.

```azurepowershell
Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}
```

Note

The *TargetName* parameter is required. The default theme that's released with AD FS is named Default.

## Add a sign-in description

To add a sign-in page description to the **Sign-in page**, use the following PowerShell cmdlet and syntax.

```azurepowershell
Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Select <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"
```

## Modify AD FS claim rules

AD FS supports a rich claim language that you can use to create custom claim rules. For more information, see [The Role of the Claim Rule Language](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807118%28v=ws.11%29).

The following sections describe how you can write custom rules for some scenarios that relate to Microsoft Entra ID and AD FS federation.

### Immutable ID conditional on a value being present in the attribute

Microsoft Entra Connect lets you specify an attribute to be used as a source anchor when objects are synced to Microsoft Entra ID. If the value in the custom attribute isn't empty, you might want to issue an immutable ID claim.

For example, you might select `ms-ds-consistencyguid` as the attribute for the source anchor and issue **ImmutableID** as `ms-ds-consistencyguid` in case the attribute has a value against it. If there's no value against the attribute, issue `objectGuid` as the immutable ID. You can construct the set of custom claim rules as described in the following section.

**Rule 1: Query attributes**

```claim
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
=> add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);
```

In this rule, you're querying the values of `ms-ds-consistencyguid` and `objectGuid` for the user from Active Directory. Change the store name to an appropriate store name in your AD FS deployment. Also change the claims type to a proper claims type for your federation, as defined for `objectGuid` and `ms-ds-consistencyguid`.

Also, by using `add` and not `issue`, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values. you'll issue the claim in a later rule after you establish which value to use as the immutable ID.

**Rule 2: Check to see whether ms-ds-consistencyguid exists for the user**

```claim
NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
=> add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");
```

This rule defines a temporary flag called `idflag` that's set to `useguid` if there's no `ms-ds-consistencyguid` populated for the user. The logic behind this is that AD FS doesn't allow empty claims. When you add claims `http://contoso.com/ws/2016/02/identity/claims/objectguid` and `http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid` in Rule 1, you end up with an *msdsconsistencyguid* claim only if the value is populated for the user. If it isn't populated, AD FS sees that it will have an empty value and drops it immediately. All objects will have `objectGuid`, so that claim will always be there after Rule 1 is executed.

**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**

```claim
c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
=> issue(Type = "http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID", Value = c.Value);
```

This is an implicit `Exist` check. If the value for the claim exists, issue it as the immutable ID. The previous example uses the `nameidentifier` claim. You'll have to change this to the appropriate claim type for the immutable ID in your environment.

**Rule 4: Issue objectGuid as an immutable ID if ms-ds-consistencyGuid isn't present**

```claim
c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
&& c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
=> issue(Type = "http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID", Value = c2.Value);
```

With this rule, you're simply checking the temporary flag `idflag`. You decide whether to issue the claim based on its value.

Note

The sequence of these rules is important.

### SSO with a subdomain UPN

You can add more than one domain to be federated by using Microsoft Entra Connect, as described in Add a new federated domain. Microsoft Entra Connect versions 1.1.553.0 and later create the correct claim rule for `issuerID` automatically.