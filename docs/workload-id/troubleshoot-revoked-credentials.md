---
layout: Conceptual
title: Troubleshoot revoked application credentials - Microsoft Entra Workload ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/workload-id/troubleshoot-revoked-credentials
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-workload-id
manager: dougeby
description: Resolve revoked credential errors, inspect tokenRevocations, and determine whether Microsoft revoked an application credential.
ms.topic: troubleshooting
ms.date: 2026-10-22T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: f61c63f1-98af-3dac-973d-a9967e932f8f
document_version_independent_id: f61c63f1-98af-3dac-973d-a9967e932f8f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/workload-id/troubleshoot-revoked-credentials.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: workload-id/troubleshoot-revoked-credentials
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/workload-id/troubleshoot-revoked-credentials.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f233afb4-f511-4877-ab18-c53e36c47c54
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/aa758f63-7086-440d-afba-dcb5819f0b6f
platformId: a3951b7a-ba7d-e6e6-4f93-71dde13312a0
---

# Troubleshoot revoked application credentials - Microsoft Entra Workload ID | Microsoft Learn

If an application can't acquire a token because its credential was revoked, the Microsoft Entra security token service (STS) can return one of these errors.

| Error code | Error name | Error message |
| --- | --- | --- |
| AADSTS700027 | `InvalidClientAssertionRevokedKeysProvided` | The provided client assertion for {X} is using a key which is revoked. Please specify a valid client assertion. |
| AADSTS7005003 | `InvalidClientSecretRevokedKeysProvided` | The provided client secret keys for app '{X}' are revoked. Please specify a valid client secret. |
| AADSTS7005004 | `InvalidClientAssertionRevokedKeysProvided` | The provided client assertion for {X} is using a key which is revoked. Please specify a valid client assertion. |
| AADSTS7005005 | `FederatedIdentityCredentialRevoked` | The provided federated credential with id: '{Y}' for application '{X}' is revoked. |
| AADSTS7005006 | `TokenRevocationBlocksIssuance` | {X} has blocked token issuance for this request. |

In these messages, `{X}` is the application's application (client) ID, and `{Y}` is the federated identity credential ID. Match the message as well as the code: `AADSTS700027` can also indicate other client assertion validation failures.

Important

A revoked credential error doesn't, by itself, mean Microsoft revoked the credential. Application owners and administrators with sufficient permissions can also revoke credentials. A populated `tokenRevocations` collection doesn't identify who performed the revocation either. Follow the checks in this article to determine the source.

## Understand why a credential was revoked

Tenant administrators or Microsoft can revoke credentials. Microsoft can revoke a credential in your tenant after detecting that a threat actor compromised it. This can include a threat actor stealing an existing credential or adding a credential to a service principal or application object.

The `tokenRevocations` property records revocations on an application or service principal. Revoking a credential has the following effects:

- The revoked credential can no longer be used as a client credential to acquire new tokens.
- For some Microsoft resources, tokens already issued using the credential are invalidated before they expire.
- For other resources, tokens already issued using the credential continue to work until they expire, which can take up to 24 hours. The revoked credential can't acquire a replacement token.

Don't assume revocation immediately ends access to every resource. Investigate the compromise and the resources the application could access.

## Check both the application and service principal

Use Microsoft Graph to read `tokenRevocations` for both object types in the affected tenant. Your tenant might contain only the application object, only the service principal object, or both for the same application ID. A revocation can be recorded on either object. For background, see [Application and service principal objects](../identity-platform/app-objects-and-service-principals).

Use an account authorized to read the affected objects. The following requests use the Microsoft Graph `/beta` endpoint.

1. Record the application (client) ID from the error and confirm which tenant the failed token request targeted.
2. Replace `{appId}` with that application (client) ID, not an object ID. Query the application object's revocations:

    ```http
    GET https://graph.microsoft.com/beta/applications(appId='{appId}')/tokenRevocations
    ```
3. Query the service principal object's revocations with the same application ID:

    ```http
    GET https://graph.microsoft.com/beta/servicePrincipals(appId='{appId}')/tokenRevocations
    ```
4. Inspect both responses. Keep track of which object contains each revocation, even if you find a match in the first response.

Tip

You can run these requests in [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer). Sign in to the affected tenant with an authorized account; the unsigned-in sample tenant doesn't show your configuration. Select **GET** and **beta**, paste a request URL with `{appId}` replaced, and select **Run query**. The signed-in account needs appropriate access, and Graph Explorer needs consent for the required Microsoft Graph permissions. For help, see [Use Graph Explorer](/en-us/graph/graph-explorer/graph-explorer-overview).

### Interpret the response

A successful response contains a `value` array. A nonempty array means that the object has revocation entries. For example, this illustrative response shows a revoked client secret. Unrelated fields are omitted.

```json
{
  "value": [
    {
      "@odata.type": "#microsoft.graph.passwordCredentialRevocation",
      "id": "11111111-2222-3333-4444-555555555555",
      "auditDetails": {
        "reason": "Compromised credential",
        "fromDateTime": "2026-10-22T12:00:00Z",
        "issuedBy": "0e0fb671-b107-448b-a273-9d0ded7627a7"
      },
      "credential": {
        "id": "aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
      }
    }
  ]
}
```

Inspect these fields for the revocation that affects your credential:

| Field | What to look for |
| --- | --- |
| `id` | The revocation ID. Save this value if you need to delete the revocation. It isn't the application ID or credential ID. |
| `credential.id` | The affected credential's ID. For a federated identity credential error, compare it with `{Y}` in the error message. |
| `auditDetails.issuedBy` | The issuer's identifier. Use the check in the next section to determine whether Microsoft issued the revocation. |
| `auditDetails.reason` | Optional free-text context about the revocation. The text can vary and isn't proof of who issued it. |
| `auditDetails.fromDateTime` | The timestamp recorded in the revocation's audit details. Use it to help locate the corresponding audit event. |

Handle other responses as follows:

- An empty `"value": []` means that no revocations were returned for that object. Still check the other object type.
- An object-not-found response can mean that the object type doesn't exist in your tenant. Confirm the tenant and application ID, and check the other object type.
- An authorization error doesn't mean that no revocations exist. Resolve the access or consent issue before drawing a conclusion.
- If the response includes `@odata.nextLink`, follow it to inspect the remaining entries.

If neither object has a matching revocation, confirm the application ID, tenant, and credential used by the failing request. Don't attribute the failure to Microsoft without the evidence described next.

## Determine whether Microsoft revoked the credential

Either of the following checks confirms a Microsoft-initiated revocation. You don't need both to match.

### Check the revocation issuer

Inspect `auditDetails.issuedBy` on the matching revocation. If it equals the following value, Microsoft revoked the credential:

```text
0e0fb671-b107-448b-a273-9d0ded7627a7
```

The example response in the previous section contains this value. You can also use the audit logs to investigate the actor.

### Check tenant audit logs

Look for the update that recorded the revocation on the affected object:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) in the affected tenant as at least a [Reports Reader](../identity/role-based-access-control/permissions-reference#reports-reader).
2. Browse to **Entra ID** &gt; **Monitoring & health** &gt; **Audit logs**.
3. Set the date range to include the revocation. Look for an **Update application** or **Update service principal** activity for the affected object.
4. Open the event and review its target, changed properties, and initiator. A corresponding revocation update initiated by **Azure Active Directory Protection Services** means that Microsoft revoked the credential.

Check that the event relates to the affected object and revocation, rather than an unrelated update. If you can't find the event, check the time range and your tenant's [audit log retention](../identity/monitoring-health/reference-reports-data-retention). Missing audit history alone doesn't establish who revoked the credential.

## Restore application access

Investigate the credential and any unauthorized changes with your security team before restoring access. If Microsoft revoked it, treat the revocation as an indication that the credential was compromised.

The recommended recovery is to replace the compromised credential and update the workload to use the replacement. Leave the compromised credential revoked, and remove credentials or access that a threat actor added. For application credential setup, see [Add and manage application credentials](../identity-platform/how-to-add-credentials).

### Remove a revocation

If your investigation determines that the revocation was incorrect and the credential is safe to use, you can remove the revocation. You need permission to manage revocations on the affected object.

Warning

Deleting a revocation allows the credential to be used again if it's otherwise valid. It doesn't rotate the credential or remove a threat actor's copy of it. Don't remove a revocation from a compromised credential just to resolve the sign-in error.

1. Save the revocation details for your investigation. Identify the object that contains the entry and the entry's top-level `id`.
2. Replace `{appId}` with the application (client) ID and `{revocationId}` with that revocation ID. Use the request for the object that contains the entry.

    For a revocation on the application object:

    ```http
    DELETE https://graph.microsoft.com/beta/applications(appId='{appId}')/tokenRevocations/{revocationId}
    ```

    For a revocation on the service principal object:

    ```http
    DELETE https://graph.microsoft.com/beta/servicePrincipals(appId='{appId}')/tokenRevocations/{revocationId}
    ```

    These requests don't require a request body. Delete only the entry you intend to remove; don't clear unrelated revocations.
3. Repeat the earlier `GET` requests to confirm that the selected entry is gone and check for any remaining revocations affecting the credential. Deleting an entry from one object doesn't delete entries from the other.
4. Retry token acquisition with the intended credential. If it still fails, review the new error and any remaining revocations.