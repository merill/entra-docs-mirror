---
layout: Conceptual
title: Govern agent access to data in Azure Database for PostgreSQL flexible server | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/govern-agent-access-azure-postgresql
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: markwahl-msft
ms.author: mwahl
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to use Microsoft Entra agent ID identity governance and conditional access for an agent accessing an Azure Database for PostgreSQL database.
ms.topic: tutorial
ms.date: 2026-10-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6475e233-4cb0-b8f3-db52-933d15cea1b4
document_version_independent_id: 6475e233-4cb0-b8f3-db52-933d15cea1b4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/govern-agent-access-azure-postgresql.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/govern-agent-access-azure-postgresql
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/govern-agent-access-azure-postgresql.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9527be-7cdf-4bdd-8574-272df09987d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://authoring-docs-microsoft.poolparty.biz/devrel/e87f9e59-cf8f-4272-9365-9d20f2c3efe5
platformId: fdb91b8a-bd57-6400-671f-550078b6711b
---

# Govern agent access to data in Azure Database for PostgreSQL flexible server | Microsoft Learn

Microsoft Entra Agent ID provides a centralized set of tools for managing agent identities and their access to applications across your organization. This guide illustrates how to govern an agent with a Microsoft Entra Agent ID needing access to data in an example application, [Azure Database for PostgreSQL](https://azure.microsoft.com/products/postgresql/). Azure Database for PostgreSQL integrates with Microsoft Entra for authentication and authorization for service principals and agent identities. For more information, see [Use Microsoft Entra ID authentication in Azure Database for PostgreSQL flexible server](/en-us/azure/postgresql/security/security-entra-configure).

In this tutorial, you configure Microsoft Entra and Azure Database for PostgreSQL so that an AI agent authenticates using its own Entra agent identity, and is authorized to interact with the database. You configure Microsoft Entra **Entitlement Management** access packages to set up the security group membership that grants the agent access to a table in the database. This enables additional agents to be able to obtain the same access as this agent, while maintaining their own identities and without needing to make changes to the database security principals.

## Prerequisites

Microsoft Entra Agent ID is a product within Microsoft Entra that provides the platform for creating and managing agent identities and agent identity blueprints. Agent ID is available for all Microsoft Entra customers.

[Microsoft Agent 365](/en-us/microsoft-agent-365/overview) enables agents to operate across Microsoft 365 services and enterprise workflows, which requires a **Microsoft Agent 365** license for each user. For pricing details, see [Microsoft Agent 365 plans and pricing](https://www.microsoft.com/microsoft-agent-365#plans-and-pricing).

Extending Microsoft Entra security features to agents requires Microsoft Agent 365. Agent 365 is included with Microsoft 365 E7 and is available as an add-on to Microsoft E5/A5/Business Premium (or Microsoft Defender Suite + Microsoft Purview Suite). See our latest [Agent 365 product terms for more details](https://www.microsoft.com/licensing/terms/productoffering/Agent365/EAEAS#clause-2755-h3-1).

You'll need to have an Azure Database for PostgreSQL server in an Azure subscription, with a database where you are an administrator. If you don't have one already, see [Quickstart: Create an Azure Database for PostgreSQL flexible server](/en-us/azure/postgresql/configure-maintain/quickstart-create-server).

You'll also need an agent which has a Microsoft Entra agent ID.

## Architecture

![Diagram showing the relationship of the agent, Microsoft Entra components, and the Azure Database for PostgreSQL.](media/govern-agent-access-azure-postgresql/database-authorization-components.png)

### Authentication interactions

The agent uses a two-step token exchange flow to obtain a short-lived access token for the Azure Database for PostgreSQL derived from its Microsoft Entra Agent ID. When the agent needs to use the database,

1. The agent authenticates to Microsoft Entra as an agent blueprint, providing blueprint credentials and an agent ID.
2. The agent exchanges at a Microsoft Entra authentication endpoint for an access token with the Azure Database scope.
3. The agent sends the security group name and that access token to the Azure Database for PostgreSQL server as the credential to authenticate.
4. Azure Database for PostgreSQL validates that the agent identity in the token is a member of the group, and therefore is authorized to act as the principal named by that group in the server's databases.

## Enable Microsoft Entra authentication and authorization for Azure Database for PostgreSQL

In this section, you'll enable agents to authenticate using Microsoft Entra agent ID to your database, and create a security group that you'll authorize to read a table named `employees` in a database.

### Create a security group for authorization to read from a PostgreSQL data set

1. In the Microsoft Entra Admin Center, go to **Microsoft Entra ID**, select **Groups**, and select **New group**.
2. Set **Group type** to **Security**.
3. Enter a **Group name** such as `pg-employees-readers`. Keep the name short; you will use it verbatim inside PostgreSQL.
4. Leave membership type as **Assigned**, as Entitlement Management will be used to assign membership. Do not add any members yet.
5. Select **Create**.
6. After creation, open the group and note the name and Object ID, which you'll use when creating the principal and role assignment in the PostgreSQL database.

### Enable Microsoft Entra authentication in Azure Database for PostgreSQL

If you have not enabled Microsoft Entra authentication in the database, then do so to allow the agent to use a Microsoft Entra agent ID. If you have already configured Microsoft Entra authentication, then continue at the next section.

1. In the [Azure portal](https://portal.azure.com), open your **Azure Database for PostgreSQL** resource.
2. In the left menu, go to **Security** &gt; **Authentication**.
3. Under **Microsoft Entra authentication**, toggle **Enable** to on.
4. Select **Add Microsoft Entra Admins**.
5. Search for and select your own account (or a group of database administrators). This account will have the ability to perform operations inside PostgreSQL as a superuser-equivalent Entra identity.
6. Select **Save**.

Important

Enabling Entra authentication does not disable password authentication. If you want to enforce Entra-only connections, additionally set the server parameter `azure.enable_passwordless_auth=on` (preview) or remove the local `postgres` superuser password and rely solely on Entra identities.

### Create a table in the database

Connect to your Azure Database for PostgreQL server using the Entra admin account you just configured.

Once connected, confirm you have an `employees` table. If you don't have a table with that name in your PostgreSQL database, connect to PostgreSQL and create that table.

### Create the database role for the security group to read from that database

Create a PostgreSQL principal for the security group created earlier, and grant it SELECT access on the `employees` table:

```sql
-- Create a role whose name matches the Entra security group name exactly (case-sensitive)
SELECT pgaadauth_create_principal('pg-employees-readers', false, false);

-- Grant the group role read access to the employees table
GRANT SELECT ON TABLE employees TO "pg-employees-readers";
```

Note

`pgaadauth_create_principal` is a helper function provided by the `pgaadauth` extension that Azure Database for PostgreSQL loads automatically when Entra authentication is enabled. The second parameter controls whether the role is a superuser; always set it to `false` for agent identities. The third parameter controls whether login is enabled on the role itself; set it to `false` because individual Microsoft Entra ID principals (not the group role) will log in.

Then, verify the role and grant are present.

```sql
-- List Entra-authenticated roles
SELECT * FROM pgaadauth_list_principals(false);

-- Confirm the table grant
\dp employees
```

You should see `pg-employees-readers` listed with `r` (SELECT) privileges on the `employees` table.

## Create an access package to assign agent identites to the security group

Entitlement Management lets you define an *access package* that bundles the security group membership and attach a policy describing how identities, including agent identities, can request access.

### Create a catalog to contain the access package

1. In the Entra Admin Center, go to **Identity Governance** &gt; **Entitlement management** &gt; **Catalogs**.
2. Select to create a **New catalog**.
3. Name it `AI Agents` and provide a description. Set **Enabled** to **Yes**. Select **Create**.
4. Open the new catalog and choose **Resources** &gt; **Add resources**.
5. Select **Groups and teams**, find and select `pg-employees-readers`, then choose **Add**.

### Create the access package

1. In the catalog, change to **Access packages**.
2. Select **New access package**.
3. On the **Basics**tab:
    - **Name**: `Employee Database Readers`
    - **Catalog**: `AI Agents`
    - Select **Next: Resource roles**.
4. On the **Resource roles**tab:
    - Select **Groups and teams**, choose `pg-employees-readers`.
    - Set the role to **Member**.
    - Select **Next: Requests**.
5. On the **Requests**tab:
    - Under **Who can request access**, select **None (administrator direct assignments only)**. In this first policy, a human administrator controls which agent identities get access; the agent never self-requests.
    - Select **Next: Requestor information**, skip optional questions, **Next: Lifecycle**.
6. On the **Lifecycle**tab:
    - Set **Access package assignment expires** to an appropriate duration (for example, 180 days).
    - Select **Next: Rules**, then **Next: Review + create**.
7. Select **Create**.

## Register an agent blueprint and agent identity in Microsoft Entra

In this section, you'll create the representation of the agent in Microsoft Entra.

1. Ensure you are signed into the Entra Admin Center as a user in the **Agent ID Developer** or **Agent ID Administrator** roles.
2. Navigate to **Agents**, **Agent Blueprints**, and select **New agent blueprint (Preview)**.
3. Give the agent a name such as `EmployeeAgentIdentity`, and confirm the sponsor.
4. One the blueprint is created, navigate to the blueprint, select **Credentials (Preview)**, select **Client secrets**, and select **New client secret**.
5. Record the displayed client secret value.
6. Change to the **Overview (Preview)** tab, and record the blueprint app ID and blueprint principal object ID.
7. Change to the **Linked agent identities (Preview)** tab, select the agent identity. Record the object ID.

For more information on other options for how agent identities are created in Microsoft Entra, see [How are agent identities created?](agent-id-creation-channels).

## Authorize the agent identity using Microsoft Entra entitlement management

You can authorize the agent by directly assigning the agent identity to the access package.

1. In the Entra Admin Center, go to **Identity Governance** &gt; **Entitlement management** &gt; **Access packages**.
2. Open the **Employee Database Readers** access package created earlier.
3. Choose **Assignments** &gt; **New assignment**.
4. Under **Select policy**, choose **Initial policy** (or the administrator assignment policy you created).
5. Under **Select user or service principal**, search for and select `EmployeeAgentIdentity`.
6. Set the assignment end date consistent with the lifecycle policy.
7. Select **Add**.

After the assignment request is processed, usually within a few minutes, `EmployeeAgentIdentity` becomes a member of the `pg-employees-readers` security group.

Note

You can verify group membership in the Microsoft Entra Admin Center, by changing to **Microsoft Entra ID** &gt; **Groups**, Selecting **pg-employees-readers** and viewing the **Members**.

## Agent connects to the database

Now that the agent's identity is a member of the security group, when it connects to the Azure Database for PostgreSQL server, the server can validate its identity and check its authorization for subsequent SQL calls. In order to connect to the database, the agent first obtains a token for the database as a resource.

![Diagram showing the token sequence of autonomous app token acquisition flow for agents.](media/agent-autonomous-app-oauth-flow/autonomous-app-flow-token-sequence.png)

1. The agent authenticates to Microsoft Entra as the blueprint, and indicates the agent identity.

    In this step, the agent supplies the blueprint credentials and the identity of the agent ID, and receives an intermediate token. For more information on other authentication options, see [Agent autonomous app OAuth flow - App-only protocol](agent-autonomous-app-oauth-flow).

    ```
    POST https://login.microsoftonline.com/<tenant-id>/oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    grant_type=client_credentials
    &scope=api%3A%2F%2FAzureADTokenExchange%2F.default
    &client_id=<blueprint-client-id>
    &client_secret=<blueprint-client-secret>
    &Fmi_Path=<agent-id>
    ```

    In this step, Microsoft Entra ID checks:

    - The blueprint credentials are valid.
    - Conditional Access policies assigned to the blueprint principal are satisfied.
    - The `Fmi_Path` value resolves to a known agent identity within the tenant.
2. If the checks were successful, Microsoft Entra ID provides a response to the agent with the intermediate token.

    This token consists of a short-lived JWT, the intermediate token, issued for the `api://AzureADTokenExchange` audience.
3. The agent obtains from Microsoft Entra ID a PostgreSQL access token.

    In this step, the agent exchanges the intermediate token for an access token it can supply to the Azure Database for PostgreSQL.

    ```
    POST https://login.microsoftonline.com/<tenant-id>/oauth2/v2.0/token
    Content-Type: application/x-www-form-urlencoded
    
    grant_type=client_credentials
    &client_id=<agent-id>
    &scope=https%3A%2F%2Fossrdbms-aad.database.windows.net%2F.default
    &client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
    &client_assertion=<intermediate-token>
    ```

    In this step, Microsoft Entra ID checks:

    - The intermediate token signature and audience are valid.
    - The `client_id` matches the agent identity registration.
    - Any Conditional Access policies assigned to the `EmployeeAgentIdentity` service principal are evaluated here. If the request violates the network or risk policy, Entra returns `conditional_access_failed` and the agent cannot connect.
    - The agent identity is not blocked or disabled.
4. If the checks are successful, Microsoft Entra ID provides a response with a token for the resource.

    The response includes a short-lived JWT access token issued for the `https://ossrdbms-aad.database.windows.net` audience.
5. The agent connects to the database.

    When connecting, the agent uses the group name as the username, and the access token as the PostgreSQL user password. PostgreSQL then:

    1. Validates the token signature using Entra's public keys.
    2. Confirms the token audience is `https://ossrdbms-aad.database.windows.net`.
6. The agent sends a request to the database.

    Because the session included in the `groups` claim included `pg-employees-readers`, the session has the privileges associated with that role — including `SELECT` on the `employees` table.