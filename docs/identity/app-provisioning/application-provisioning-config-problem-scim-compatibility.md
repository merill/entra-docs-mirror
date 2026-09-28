---
layout: Conceptual
title: Known issues with System for Cross-Domain Identity Management (SCIM) 2.0 protocol compliance - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/application-provisioning-config-problem-scim-compatibility
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: How to solve common protocol compatibility issues faced when adding a non-gallery application that supports SCIM 2.0 to Microsoft Entra ID
ms.topic: reference
ms.date: 2025-08-25T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 09b8c472-3a4e-dd2c-11df-f05b05e5a642
document_version_independent_id: 834bcfe7-2e5c-97ed-eeb8-d5eed616188b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/application-provisioning-config-problem-scim-compatibility.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/application-provisioning-config-problem-scim-compatibility
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/application-provisioning-config-problem-scim-compatibility.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 7d762339-f2ca-8d26-7e14-7b1291fb9116
---

# Known issues with System for Cross-Domain Identity Management (SCIM) 2.0 protocol compliance - Microsoft Entra ID | Microsoft Learn

Microsoft Entra ID can automatically provision users and groups to any application or system fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).

Microsoft Entra support for the SCIM 2.0 protocol is described in [Using System for Cross-Domain Identity Management (SCIM) to automatically provision users and groups from Microsoft Entra ID to applications](use-scim-to-provision-users-and-groups), which lists the specific parts of the protocol that it implements in order to automatically provision users and groups from Microsoft Entra ID to applications that support SCIM 2.0.

This article describes current and past issues with the Microsoft Entra user provisioning service's adherence to the SCIM 2.0 protocol, and how to work around these issues.

## Understanding the provisioning job

The provisioning service uses the concept of a job to operate against an application. The jobID can be found in the [progress bar](application-provisioning-when-will-provisioning-finish-specific-user#view-the-provisioning-progress-bar). All new provisioning applications are created with a jobID starting with `scim`. The scim job represents the current state of the service. Older jobs have the ID `customappsso`. This job represents the state of the service in 2018.

If you're using an application in the gallery, the job generally contains the name of the app (such as zoom snowFlake or dataBricks). You can skip this documentation when using a gallery application. This primarily applies for non-gallery applications with jobID SCIM or customAppSSO.

## SCIM 2.0 compliance issues and status

In the, any item marked as fixed means that the proper behavior can be found on the SCIM job. We have worked to ensure backwards compatibility for the changes we have made. We recommend using the new behavior for any new implementations and updating existing implementations. The customappSSO behavior that was the default prior to December 2018 isn't supported anymore.

Note

For the changes made in 2018, it's possible to revert back to the customappsso behavior. For the changes made since 2018, you can use the URLs to revert back to the older behavior. We have worked to ensure backwards compatibility for the changes we have made by allowing you to revert back to the old jobID or by using a flag. However, as previously mentioned, we don't recommend implementing old behavior as it isn't supported anymore. We recommend using the new behavior for any new implementations and updating existing implementations.

| **SCIM 2.0 compliance issue** | **Fixed?** | **Fix date** | **Backwards compatibility** |
| --- | --- | --- | --- |
| Microsoft Entra ID requires "/scim" to be in the root of the application's SCIM endpoint URL | Yes | December 18, 2018 | downgrade to customappSSO |
| Extension attributes use dot `.` notation before attribute names instead of colon ":" notation | Yes | December 18, 2018 | downgrade to customappSSO |
| Patch requests for multi-value attributes contain invalid path filter syntax | Yes | December 18, 2018 | downgrade to customappSSO |
| Group creation requests contain an invalid schema URI | Yes | December 18, 2018 | downgrade to customappSSO |
| Update PATCH behavior to ensure compliance (such as active as boolean and proper group membership removals) | No | TBD | use feature flag |

## Flags to alter the SCIM behavior

Use the flags in the tenant URL of your application in order to change the default SCIM client behavior.

![SCIM flags to later behavior.](media/application-provisioning-config-problem-scim-compatibility/scim-flags.png)

Use the following URL to update PATCH behavior and ensure SCIM compliance. The flag alters the following behaviors:

- Requests made to disable users
- Requests to add a single-value string attribute
- Requests to replace multiple attributes
- Requests to remove a group member

This behavior is currently only available when using the flag, but will become the default behavior over the next few months. Note this feature flag currently doesn't work with on-demand provisioning.

- **URL (SCIM Compliant):** aadOptscim062020
- **SCIM RFC references:**
    - https://tools.ietf.org/html/rfc7644#section-3.5.2

Sample requests to help outline what the sync engine currently sends versus the requests that are sent once the feature flag is enabled.

**Requests made to disable users:**

**Without feature flag**

```json
{
  "schemas": [
      "urn:ietf:params:scim:api:messages:2.0:PatchOp"
  ],
  "Operations": [
      {
          "op": "Replace",
          "path": "active",
          "value": "False"
      }
  ]
}
```

**With feature flag**

```json
{
  "schemas": [
      "urn:ietf:params:scim:api:messages:2.0:PatchOp"
  ],
  "Operations": [
      {
          "op": "replace",
          "path": "active",
          "value": false
      }
  ]
}
```

**Requests made to add a single-value string attribute:**

**Without feature flag**

```json
{
  "schemas": [
      "urn:ietf:params:scim:api:messages:2.0:PatchOp"
  ],
  "Operations": [
    {
      "op": "Add",
      "path": "nickName",
      "value": "Babs"
    }
  ]
}
```

**With feature flag**

```json
{
  "schemas": ["urn:ietf:params:scim:api:messages:2.0:PatchOp"],
  "Operations": [
    {
      "op": "add",
      "path": "nickName",
      "value": "Babs"
    }
  ]
}
```

**Requests to replace multiple attributes:**

**Without feature flag**

```json
{
  "schemas": [
      "urn:ietf:params:scim:api:messages:2.0:PatchOp"
  ],
  "Operations": [
      {
          "op": "Replace",
          "path": "displayName",
          "value": "Pvlo"
      },
      {
          "op": "Replace",
          "path": "emails[type eq \"work\"].value",
          "value": "TestBcwqnm@test.microsoft.com"
      },
      {
          "op": "Replace",
          "path": "name.givenName",
          "value": "Gtfd"
      },
      {
          "op": "Replace",
          "path": "name.familyName",
          "value": "Pkqf"
      },
      {
          "op": "Replace",
          "path": "externalId",
          "value": "Eqpj"
      },
      {
          "op": "Replace",
          "path": "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber",
          "value": "Eqpj"
      }
  ]
}
```

**With feature flag**

```json
{
  "schemas": [
      "urn:ietf:params:scim:api:messages:2.0:PatchOp"
  ],
  "Operations": [
      {
          "op": "replace",
          "path": "emails[type eq \"work\"].value",
          "value": "TestMhvaes@test.microsoft.com"
      },
      {
          "op": "replace",
          "value": {
              "displayName": "Bjfe",
              "name.givenName": "Kkom",
              "name.familyName": "Unua",
              "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber": "Aklq"
          }
      }
  ]
}
```

**Requests made to remove a group member:**

**Without feature flag**

```json
{
  "schemas": [
      "urn:ietf:params:scim:api:messages:2.0:PatchOp"
  ],
  "Operations": [
      {
          "op": "Remove",
          "path": "members",
          "value": [
              {
                  "value": "u1091"
              }
          ]
      }
  ]
}
```

**With feature flag**

```json
{
  "schemas": [
      "urn:ietf:params:scim:api:messages:2.0:PatchOp"
  ],
  "Operations": [
      {
          "op": "remove",
          "path": "members[value eq \"7f4bc1a3-285e-48ae-8202-5accb43efb0e\"]"
      }
  ]
}
```

- **Downgrade URL:** Once the new SCIM compliant behavior becomes the default on the non-gallery application, you can use the following URL to roll back to the old, non SCIM compliant behavior: AzureAdScimPatch2017

## Upgrading from the older customappsso job to the SCIM job

Delete your existing `customappsso` job and create a new SCIM job.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. Locate and select your existing SCIM application.
4. In the **Properties** section of your existing SCIM app, copy the **Object ID**.
5. In a new web browser window, go to https://developer.microsoft.com/graph/graph-explorer and sign in as the administrator for the Microsoft Entra tenant where your app is added.
6. In the Graph Explorer, run the command below to locate the ID of your provisioning job. Replace "[object-id]" with the service principal ID (object ID) copied from the third step.

    `GET https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs`

    ![Get Jobs](media/application-provisioning-config-problem-scim-compatibility/get-jobs.png)
7. In the results, copy the full "ID" string that begins with either "customappsso" or "scim".
8. Run the command below to retrieve the attribute-mapping configuration, so you can make a backup. Use the same [object-id] as before, and replace [job-id] with the provisioning job ID copied from the last step.

    `GET https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/[job-id]/schema`
9. Copy the JSON output from the last step, and save it to a text file. The JSON contains any custom attribute-mappings that you added to your old app, and should be approximately a few thousand lines of JSON.
10. Run the command below to delete the provisioning job:

    `DELETE https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/[job-id]`
11. Run the command below to create a new provisioning job that has the latest service fixes.

`POST https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs``{   "templateId": "scim"   }`

1. In the results of the last step, copy the full "ID" string that begins with "scim". Optionally, reapply your old attribute-mappings by running the command below, replacing [new-job-id] with the new job ID you copied, and entering the JSON output from step #7 as the request body.

`PUT https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/[new-job-id]/schema``{   <your-schema-json-here>   }`

1. Return to the first web browser window, and select the **Provisioning** tab for your application.
2. Verify your configuration, and then start the provisioning job.

## Downgrading from the SCIM job to the customappsso job (not recommended)

We allow you to downgrade back to the old behavior but don't recommend it as the customappsso doesn't benefit from some of the updates we make, and may not be supported forever.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least an [Application Administrator](../role-based-access-control/permissions-reference#application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps**.
3. In the **Create application** section, create a new **Non-gallery** application.
4. In the **Properties** section of your new custom app, copy the **Object ID**.
5. In a new web browser window, go to https://developer.microsoft.com/graph/graph-explorer and sign in as the administrator for the Microsoft Entra tenant where your app is added.
6. In the Graph Explorer, run the command below to initialize the provisioning configuration for your app. Replace "[object-id]" with the service principal ID (object ID) copied from the third step.

    `POST https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs``{   templateId: "customappsso"   }`
7. Return to the first web browser window, and select the **Provisioning** tab for your application.
8. Complete the user provisioning configuration as you normally would.