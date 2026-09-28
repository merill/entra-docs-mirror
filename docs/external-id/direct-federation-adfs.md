---
layout: Conceptual
title: Set up AD FS federation - Microsoft Entra External ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/direct-federation-adfs
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to set up SAML/WS-Fed IdP federation with AD FS for B2B collaboration in Microsoft Entra External ID. Configure AD FS as a SAML 2.0 or WS-Fed IdP and manage attributes and claims.
ms.topic: how-to
ms.date: 2026-04-17T00:00:00.0000000Z
ms.custom: it-pro
ms.collection: M365-identity-device-management
ai-usage: ai-assisted
locale: en-us
document_id: 73f77b32-b5d1-9c2e-dfd4-7ad191dbd871
document_version_independent_id: ad120312-98ef-4db4-ffca-ca11f29e5c5e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/direct-federation-adfs.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/direct-federation-adfs
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/direct-federation-adfs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: a9245306-a156-dee9-77dd-a0ee9110612c
---

# Set up AD FS federation - Microsoft Entra External ID | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

Note

*Direct federation* in Microsoft Entra External ID is now referred to as *SAML/WS-Fed identity provider (IdP) federation*.

This article describes how to set up [SAML/WS-Fed IdP federation](direct-federation) using Active Directory Federation Services (AD FS) as either a SAML 2.0 or WS-Fed IdP. To support federation, certain attributes and claims must be configured at the IdP. To illustrate how to configure an IdP for federation, we use Active Directory Federation Services (AD FS) as an example. We show how to set up AD FS both as a SAML IdP and as a WS-Fed IdP.

Note

This article describes how to set up AD FS for both SAML and WS-Fed for illustration purposes. For federation integrations where the IdP is AD FS, we recommend using WS-Fed as the protocol.

## Configure AD FS for SAML 2.0 federation

Microsoft Entra B2B can be configured to federate with IdPs that use the SAML protocol with specific requirements listed below. To illustrate the SAML configuration steps, this section shows how to set up AD FS for SAML 2.0.

To set up federation, the following attributes must be received in the SAML 2.0 response from the IdP. These attributes can be configured by linking to the online security token service XML file or by entering them manually. Step 12 in [Create a test AD FS instance](https://medium.com/in-the-weeds/create-a-test-active-directory-federation-services-3-0-instance-on-an-azure-virtual-machine-9071d978e8ed) describes how to find the AD FS endpoints or how to generate your metadata URL, for example `https://fs.iga.azure-test.net/federationmetadata/2007-06/federationmetadata.xml`.

| Attribute | Value |
| --- | --- |
| AssertionConsumerService | `https://login.microsoftonline.com/login.srf` |
| Audience | `urn:federation:MicrosoftOnline` |
| Issuer | The issuer URI of the partner IdP, for example `http://www.example.com/exk10l6w90DHM0yi...` |

The following claims need to be configured in the SAML 2.0 token issued by the IdP:

| Attribute | Value |
| --- | --- |
| NameID Format | `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent` |
| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` | The user's email address |

The next section illustrates how to configure the required attributes and claims using AD FS as an example of a SAML 2.0 IdP.

### Before you begin

An AD FS server must already be set up and functioning before you begin this procedure.

### Add the claim description

1. On your AD FS server, select **Tools** &gt; **AD FS management**.
2. In the navigation pane, select **Service** &gt; **Claim Descriptions**.
3. Under **Actions**, select **Add Claim Description**.
4. In the **Add a Claim Description** window, specify the following values:

    - **Display Name**: Persistent Identifier
    - **Claim identifier**: `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`
    - Select the check box for **Publish this claim description in federation metadata as a claim type that this federation service can accept**.
    - Select the check box for **Publish this claim description in federation metadata as a claim type that this federation service can send**.
5. Select **Ok**.

### Add the relying party trust

1. On the AD FS server, go to **Tools** &gt; **AD FS Management**.
2. In the navigation pane, select **Relying Party Trusts**.
3. Under **Actions**, select **Add Relying Party Trust**.
4. In the **Add Relying Party Trust** wizard, select **Claims aware**, and then select **Start**.
5. In the **Select Data Source** section, select the check box for **Import data about the relying party published online or on a local network**. Enter this federation metadata URL: `https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml`. Select **Next**.
6. Leave the other settings in their default options. Continue to select **Next**, and finally select **Close** to close the wizard.
7. In **AD FS Management**, under **Relying Party Trusts**, right click the relying party trust you just created and select **Properties**.
8. In the **Monitoring** tab, uncheck the box **Monitor relying party**.
9. In the **Identifiers** tab, enter `https://login.microsoftonline.com/<tenant ID>/` in the **Relying party identifier** text box using the tenant ID of the service partner’s Microsoft Entra tenant. Select **Add**.

    Note

    Be sure to include a slash (/) after the tenant ID, for example: `https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee/`.
10. Select **OK**.

### Create claims rules

1. Right-click the relying party trust you created, and then select **Edit Claim Issuance Policy**.
2. In the **Edit Claim Rules** wizard, select **Add Rule**.
3. In **Claim rule template**, select **Send LDAP Attributes as Claims**.
4. In **Configure Claim Rule**, specify the following values:

    - **Claim rule name**: Email claim rule
    - **Attribute store**: Active Directory
    - **LDAP Attribute**: E-Mail-Addresses
    - **Outgoing Claim Type**: E-Mail Address
5. Select **Finish**.
6. Select **Add Rule**.
7. In **Claim rule template**, select **Transform an Incoming Claim**, and then select **Next**.
8. In **Configure Claim Rule**, specify the following values:

    - **Claim rule name**: Email transform rule
    - **Incoming claim type**: E-mail Address
    - **Outgoing claim type**: Name ID
    - **Outgoing name ID format**: Persistent Identifier
    - Select **Pass through all claim values**.
9. Select **Finish**.
10. The **Edit Claim Rules** pane shows the new rules. Select **Apply**.
11. Select **OK**. The AD FS server is now configured for federation using the SAML 2.0 protocol.

## Configure AD FS for WS-Fed federation

Microsoft Entra B2B can be configured to federate with IdPs that use the WS-Fed protocol with the specific requirements listed below. Currently, the two WS-Fed providers tested for compatibility with Microsoft Entra External ID are AD FS and Shibboleth. Here, we use Active Directory Federation Services (AD FS) as an example of the WS-Fed IdP. For more information about establishing a relying party trust between a WS-Fed compliant provider and Microsoft Entra External ID, download the Microsoft Entra identity provider compatibility docs.

To set up federation, the following attributes must be received in the WS-Fed message from the IdP. These attributes can be configured by linking to the online security token service XML file or by entering them manually. Step 12 in [Create a test AD FS instance](https://medium.com/in-the-weeds/create-a-test-active-directory-federation-services-3-0-instance-on-an-azure-virtual-machine-9071d978e8ed) describes how to find the AD FS endpoints or how to generate your metadata URL, for example `https://fs.iga.azure-test.net/federationmetadata/2007-06/federationmetadata.xml`.

| Attribute | Value |
| --- | --- |
| PassiveRequestorEndpoint | `https://login.microsoftonline.com/login.srf` |
| Audience | `urn:federation:MicrosoftOnline` |
| Issuer | The issuer URI of the partner IdP, for example `http://www.example.com/exk10l6w90DHM0yi...` |

Required claims for the WS-Fed token issued by the IdP:

| Attribute | Value |
| --- | --- |
| ImmutableID | `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID` |
| emailaddress | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` |

The next section illustrates how to configure the required attributes and claims using AD FS as an example of a WS-Fed IdP.

### Before you begin

An AD FS server must already be set up and functioning before you begin this procedure.

### Add the relying party trust

1. On the AD FS server, go to **Tools** &gt; **AD FS management**.
2. In the navigation pane, select **Trust Relationships** &gt; **Relying Party Trusts**.
3. Under **Actions**, select **Add Relying Party Trust**.
4. In the Add Relying Party Trust wizard, select **Claims aware**, and then select Start.
5. In the **Select Data Source** section, select **Enter data about the relying party manually**, and then select **Next**.
6. In the **Specify Display Name** page, type a name in **Display name**. You may optionally enter a description for this relying party trust in the **Notes** section. Select **Next**.
7. Optionally, in the **Configure Certificate** page, if you have a token encryption certificate, select **Browse** to locate a certificate file. Select **Next**.
8. In the **Configure URL** page, select the **Enable support for the WS-Federation Passive protocol** check box. Under **Relying party WS-Federation Passive protocol URL**, enter the following URL: `https://login.microsoftonline.com/login.srf`
9. Select **Next**.
10. In the **Configure Identifiers** page, enter the following URLs and select **Add**. In the second URL, enter the tenant ID of service partner's Microsoft Entra tenant.

    - `urn:federation:MicrosoftOnline`
    - `https://login.microsoftonline.com/<tenant ID>/`

    Note

    Be sure to include a slash (/) after the tenant ID, for example: `https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee/`.
11. Select **Next**.
12. In the **Choose Access Control Policy** page, select a policy, and then select **Next**.
13. In the **Ready to Add Trust** page, review the settings, and then select **Next** to save your relying party trust information.
14. In the **Finish** page, select **Close**.
15. Select the relying party trust, and then select **Edit Claim Issuance Policy**.

### Create claims rules

1. Select the Relying Party Trust you just created, and then select **Edit Claim Issuance Policy**.
2. Select **Add rule**.
3. Select **Send LDAP Attributes as Claims**, and then select **Next**.
4. In **Configure Claim Rule**, specify the following values:

    - **Claim rule name**: Email claim rule
    - **Attribute store**: Active Directory
    - **LDAP Attribute**: E-Mail-Addresses
    - **Outgoing Claim Type**: E-Mail Address
5. Select **Finish**.
6. In the same **Edit Claim Rules** wizard, select **Add Rule**.
7. Select **Send Claims Using a Custom Rule**, and then select **Next**.
8. In **Configure Claim Rule**, specify the following values:

    - **Claim rule name**: Issue Immutable ID
    - **Custom rule**: `c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), query = "samAccountName={0};objectGUID;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);`
9. Select **Finish**.
10. Select **OK**. The AD FS server is now configured for federation using WS-Fed.