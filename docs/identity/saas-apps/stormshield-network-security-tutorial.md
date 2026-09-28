---
layout: Conceptual
title: Configure Stormshield Network Security (OIDC) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/stormshield-network-security-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: mwongerapk
description: Learn how to configure single sign-on between Microsoft Entra ID and Stormshield Network Security (OIDC).
ms.workload: identity
ms.topic: how-to
ms.date: 2025-10-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: f7ed52e9-5d94-e813-ff45-0d94c4ebf09c
document_version_independent_id: f7ed52e9-5d94-e813-ff45-0d94c4ebf09c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/stormshield-network-security-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/stormshield-network-security-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/stormshield-network-security-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: acda68c0-d282-5c8f-d314-7df3dfbe335a
---

# Configure Stormshield Network Security (OIDC) for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Stormshield Network Security (OIDC) with Microsoft Entra ID. When you integrate Stormshield Network Security (OIDC) with Microsoft Entra ID, you can:

- Use Microsoft Entra ID to control who can access Stormshield Network Security (OIDC).
- Enable your users to be automatically signed in to Stormshield Network Security (OIDC) with their Microsoft Entra accounts.
- Manage your accounts in one central location: the Microsoft Entra admin center.

## Prerequisites

To get started, you need the following items:

- A Microsoft Entra subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Stormshield Network Security (OIDC) single sign-on (SSO) enabled subscription.

## Add Stormshield Network Security (OIDC) from the gallery

To configure the integration of Stormshield Network Security (OIDC) into Microsoft Entra ID, you need to add Stormshield Network Security (OIDC) from the gallery to your list of managed SaaS apps.

## Collect and generate OIDC provider credentials (Client ID, Secret, Domain, Tenant ID)

The first step is to collect the necessary information from Microsoft Entra ID and generate the application secret to configure the Stormshield Network Security firewall.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, enter **Stormshield Network Security (OIDC)** in the search box.
4. Select **Stormshield Network Security (OIDC)** in the results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO in the Microsoft Entra admin center.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Stormshield Network Security (OIDC)** &gt; **Single sign-on**.
3. Perform the following steps:

    1. Select **Go to application**.

        [![Screenshot shows the identity configuration.](common/go-to-application.png)](common/go-to-application.png#lightbox)
    2. Copy **Application (client) ID** and use it later in the Stormshield Network Security (OIDC) side configuration.

        [![Screenshot of application client values.](common/application-id.png)](common/application-id.png#lightbox)
    3. Under **Endpoints** tab, copy **OpenID Connect metadata document** link and use it later in the Stormshield Network Security (OIDC) side configuration.

        ![Screenshot shows the endpoints on tab.](common/endpoints.png)

## Configure the redirect URI(s)

Important

This step ensures that Microsoft Entra ID sends the user back to the correct firewall URL after successful authentication.

1. Navigate to the **Authentication** tab on the left menu and perform the following steps:

    1. In the **Redirect URIs** textbox, paste the **Relying Party Redirect URI** value that you copied from the Stormshield Network Security (OIDC) side. These URIs must use HTTPS.

        [![Screenshot shows the redirect values.](common/redirect.png)](common/redirect.png#lightbox)
    2. Select **Configure** button.
2. Navigate to **Certificates & secrets** on the left menu and perform the following steps:

    1. Go to the **Client secrets** tab and select **+New client secret**.
    2. Enter a valid **Description** in the textbox, select an expiration period from the **Expires** drop-down as per your requirement, and select **Add**.

        [![Screenshot shows the client secrets value.](common/client-secret.png)](common/client-secret.png#lightbox)
    3. Once you add a client secret, **Value** is generated. Copy the value and use it later in the Stormshield Network Security (OIDC) side configuration.

        [![Screenshot shows how to add a client secret.](common/client.png)](common/client.png#lightbox)

### Create a Microsoft Entra test user

In this section, you create a test user called B.Simon.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [User Administrator](../role-based-access-control/permissions-reference#user-administrator).
2. Browse to **Entra ID** &gt; **Users**.
3. Select **New user** &gt; **Create new user**, at the top of the screen.
4. In the **User**properties, follow these steps:
    1. In the **Display name** field, enter `B.Simon`.
    2. In the **User principal name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
    3. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
    4. Select **Review + create**.
5. Select **Create**.

### Assign roles to users or groups in the application (Optional)

In this section, you configure which users in Microsoft Entra ID are authorized to use the application and manage their access rights. You enable B.Simon to use single sign-on by granting access to Stormshield Network Security (OIDC).

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Stormshield Network Security (OIDC)**.
3. In the app's overview page, select **Users and groups**.
4. Select **Add user/group**, then select **Users and groups** in the **Add Assignment**dialog.
    1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then select the **Select** button at the bottom of the screen.
    2. If you're expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
    3. In the **Add Assignment** dialog, select the **Assign** button.

## Configure Stormshield Network Security (OIDC) SSO

To configure single sign-on on **Stormshield Network Security** side, you need to download user groups to import them into the SNS firewall. To simplify the creation of local group objects on the SNS firewall, you can retrieve the unique identifiers (GUIDs) of your Microsoft Entra ID groups.

## Download user groups to import them into the SNS firewall (Optional)

To simplify the creation of local group objects on the SNS firewall, you can retrieve the unique identifiers (GUIDs) of your Microsoft Entra ID groups.

1. Browse to **Entra ID** &gt; **Groups** &gt; **All groups**.
2. Select the desired group (e.g., **SNS Authentication**).
3. Copy the **Object ID** (GUID) of the group.

Note

The SNS firewall uses the Object ID (GUID) to identify groups from Microsoft Entra ID. The next section will show you the method for **importing** the complete list of groups in CSV format, which is the most efficient method for a large number of groups.

### Configure the Stormshield Network Security Firewall for Microsoft Entra ID authentication

This section guides you through the necessary configurations on the **Stormshield Network Security (SNS) firewall** to enable **OIDC authentication** via **Microsoft Entra ID**.

**Sign in** to the web administration interface of the firewall.

### Set the firewall FQDN for access to the captive portal

Note

The FQDN configured here must be resolvable by browsers on client workstations for captive portal access to function correctly. This is a network prerequisite.

In **System** &gt; **Configuration** &gt; **General configuration** tab &gt; **Captive portal** section:

1. In the **Redirect to the captive portal** field, select the value **Specify a domain name (FQDN)**.
2. In the **Domain name (FQDN)** field, enter the full name of the firewall (example: `documentation-firewall.stormshield.eu`).

Important

This FQDN must be identical to the one used when declaring URIs in the Stormshield application defined in the **Microsoft Entra ID** tenant.

### Configure the server identity based on this FQDN

The certificate of this server identity is meant to be used by the firewall's captive portal.

Note

In **SSL** VPN access, it is preferable for the captive portal identity to come from a public CA, as it is already integrated into browsers.

### Import a public server identity (Recommended)

If you have obtained a server certificate from a public CA that matches the FQDN defined in the previous step, you must import it into the firewall.

1. Go to **Objects** &gt; **Certificates and PKI**.
2. Select **Import a File** (or **Import an Identity**).
3. Follow the wizard steps to import the certificate and its private key.

Note

You can choose to generate a server identity from the firewall's internal CA, but this is **not recommended** for production environments.

### Configure the captive portal to use the identity

Once the server identity is available on the firewall:

1. Go to **Configuration** &gt; **Users** &gt; **Authentication** tab.
2. In the **SSL server** fieldset, use the drop-down menu in the **Certificate (private key)** field to select the server identity you just imported/created.
3. Select **Apply** to save the changes to the configuration.

### Enable the OIDC authentication method

In **Users** &gt; **Authentication &gt; Available methods** tab:

1. Select **Enable a method**.
2. Select **OIDC/Microsoft Entra ID**. A configuration wizard will automatically launch:
3. **Domain name**: indicate the main domain name retrieved from your Microsoft Entra ID administration center (e.g., `snsdoc.onmicrosoft.com`).
4. **Tenant ID**: enter the ID retrieved from your Microsoft Entra ID administration center in this field.
5. **Application ID (client)**: enter the value retrieved from your Microsoft Entra ID administration center in this field.
6. **Client secret**: enter the value retrieved and saved when Creating a secret for the application during the creation of the SNS application on your **Microsoft Entra ID** tenant. If you did not save this value, you need to delete the **Client secret** that was created earlier for your application, and generate a new one, by following the procedure described in this step.
7. Select **Next**. The wizard suggests URLs that correspond to the captive portal service, the **SSL** VPN service, and access to the firewall’s web administration interface. These URLs can be copied directly from this wizard to be entered as redirect URLs in your **Microsoft Entra ID** administration center if necessary. They are also available in the OIDC/**Microsoft Entra ID** method editing panel.
8. Select **Next**.
9. Select the CSV file containing the groups in your **Microsoft Entra ID** tenant, which was downloaded when Download user groups to import them into the SNS firewall, then select **Next**. A summary of the group import operation then appears.
10. Select **Next**.
11. Confirm your configuration by selecting on **Finish**. You will be redirected to the OIDC/**Microsoft Entra ID** authentication method editing panel.
12. Select **Apply** to save the configuration of the **Microsoft Entra ID** authentication method on the firewall.

In this example, the configuration of the OIDC/**Microsoft Entra ID** method on the firewall will therefore resemble the following:

![Screenshot shows the SNS OIDC-Entra Configuration.](media/stormshield-network-security-tutorial/entra-configuration.png)

### Create the authentication rule

Go to **Configuration** &gt; **Users** &gt; **Authentication** &gt; **Authentication policy** tab:

1. Select **New rule** and select **Standard rule**.
2. Select **All** users in the **Users** menu. Permissions to connect to the captive portal, web administration interface or **SSL** VPN by authenticating through **Microsoft Entra ID** will be granted according to the privileges set in the tenant.
3. In the **Sources** menu: add the network interfaces through which users authenticated by **Microsoft Entra ID**will be presenting on the firewall. In this example, the following interfaces are used:
    - **in**: interface to access the internal captive portal to authenticate administrators via the web administration interface,
    - **out**: interface to access the external captive portal that **SSL** VPN clients use for retrieving their configuration files and setting up tunnels,
    - **sslvpn**: interface used by **SSL** VPN clients to access the firewall's **SSL** VPN service when the tunnel is set up.
4. In the **Authentication methods** menu: select **Enable a method** and select the **OIDC** method.
5. Likewise, add the other authentication methods for your users (e.g., **LDAP**).
6. Confirm this authentication rule by selecting **OK**. The rule will be added to the authentication policy but will not be enabled by default.
7. In the authentication rule grid, select on the status of the rule to enable it.

The authentication rule will look like this:

![Screenshot shows the Authentication Policy.](media/stormshield-network-security-tutorial/authentication-policy.png)

Note

During an authentication, rules are scanned in order of their appearance in the list. As such, ensure that you organize them using the **Up** and **Down** buttons when necessary, as well as the associated actions (**Allow**/**Block**).

The firewall's captive portal will now offer **Microsoft Entra ID** authentication:

![Screenshot shows the Captif Portal login page](media/stormshield-network-security-tutorial/connection-portal-captive.png)

### Configure the captive portal

In **Configuration** &gt; **Users** &gt; **Authentication** &gt; **Captive portal** tab:

1. Add the **in** and **out** interfaces to respectively associate them with the **Internal** and **External** profiles of the captive portal.
2. Select the server identity certificate based on the firewall’s FQDN.

The captive portal configuration will look like this:

![Screenshot shows the Captive Portal Configuration page.](media/stormshield-network-security-tutorial/captive-portal-configuration.png)

### Import Microsoft Entra security groups

Go to **Configuration** &gt; **Users** &gt; **Users and Groups &gt; Microsoft Entra ID** tab. The list of imported **Microsoft Entra ID** groups and their group IDs are displayed in the grid.

When you add or edit groups in your **Microsoft Entra ID** administration center, you can import these groups into this module by using the **Import groups** button, and selecting the CSV file that was exported from your **Microsoft Entra ID** tenant when Downloading user groups to import them into the SNS firewall.

Note

If custom groups were added through this module, they will not be overwritten when a CSV file is imported. If an imported group has the same name as a custom group, they will be differentiated by their unique identifiers (UIDs), and can coexist in the configuration.

### Create application roles on the firewall (optional)

To use application roles to manage user permissions, these roles must have identical configurations on the firewall and in the **Microsoft Entra ID** tenant application.

Note

The Stormshield Network Security firewall is provided with the default application roles that mirror those available in the **Microsoft Entra ID** tenant application. You only need to create or edit roles in this section if you wish to use **custom roles**.

Go to **Users &gt; Users** &gt; **Microsoft Entra ID** tab.

1. Select **Add,** then on **Application role**.
2. Fill in the following fields:
    - The **Application role name** (any text).
    - The **Application role UID**, which has to use syntax in `Actions.Permissions` format (e.g., `SNS.Config.All.Write`, `SNS.Config.All.Read`).
    - The optional **Description** (any text).

Important

The role UID must be unique on the firewall, and identical to the UID of the corresponding application role that was created in your **Microsoft Entra ID** tenant.

1. Select **Apply** to confirm the creation of the role.
2. Select **Apply** to save changes to the configuration.

### Allow SSL VPN for users authenticated through Microsoft Entra ID

In **Configuration** &gt; **Users** &gt; **Access privileges** &gt; **Detailed access** tab:

1. Select **Add**.
2. Enable **Microsoft Entra ID** and select a group that has been imported from **Microsoft Entra ID**, a custom group or an application role.
3. Select **Apply**. A rule is added to the grid.
4. Select in the **SSL VPN** column of this rule and select **Allow**.
5. Select in the **Status** column of this rule to enable it.
6. Select **Apply**, then **Save** to confirm changes to the configuration.

![Screenshot shows the SSL VPN Rule.](media/stormshield-network-security-tutorial/users-access-privileges.png)

### Allow administrators to access the web administration interface

In **System** &gt; **Administrators**:

1. Select **Add an administrator**.
2. Select the type of permissions to be granted to the administrator group.
3. Select **Microsoft Entra ID**, then select a security group that was imported from **Microsoft Entra ID**, a custom security group or an application role.
4. Confirm your selection by selecting on **Apply**.
5. Select **Apply** to confirm changes to the configuration.

![Screenshot shows the admin access.](media/stormshield-network-security-tutorial/admin-access.png)