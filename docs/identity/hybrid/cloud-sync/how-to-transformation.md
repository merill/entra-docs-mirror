---
layout: Conceptual
title: Microsoft Entra Cloud Sync transformations - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-transformation
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
manager: pmwongera
description: This article describes how to use transformations to alter the default attribute mappings.
ms.date: 2025-04-09T00:00:00.0000000Z
ms.topic: how-to
ms.subservice: hybrid-cloud-sync
locale: en-us
document_id: 941b31d2-4cbd-06a0-60b5-2ab373b4b215
document_version_independent_id: 010ae140-5553-b050-4ed9-1d93c6ccc276
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/hybrid/cloud-sync/how-to-transformation.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/hybrid/cloud-sync/how-to-transformation
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/hybrid/cloud-sync/how-to-transformation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 8365d162-92bf-5b59-94c8-ef160a1f74d4
---

# Microsoft Entra Cloud Sync transformations - Microsoft Entra ID | Microsoft Learn

With a transformation, you can change the default behavior of how an attribute is synchronized with Microsoft Entra ID by using cloud sync.

To do this task, you need to edit the schema and then resubmit it via a web request.

For more information on cloud sync attributes, see [Understanding the Microsoft Entra schema](concept-attributes).

## Retrieve the schema

To retrieve the schema, follow the steps in [View the synchronization schema](concept-attributes#view-the-synchronization-schema).

## Custom attribute mapping

To add a custom attribute mapping, follow these steps.

1. Copy the schema into a text or code editor such as [Visual Studio Code](https://code.visualstudio.com/).
2. Locate the object that you want to update in the schema.

    ![Screenshot of object in the schema.](media/how-to-transformation/transform-1.png)
3. Locate the code for `ExtensionAttribute3` under the user object.

    ```
                            {
                                "defaultValue": null,
                                "exportMissingReferences": false,
                                "flowBehavior": "FlowWhenChanged",
                                "flowType": "Always",
                                "matchingPriority": 0,
                                "targetAttributeName": "ExtensionAttribute3",
                                "source": {
                                    "expression": "Trim([extensionAttribute3])",
                                    "name": "Trim",
                                    "type": "Function",
                                    "parameters": [
                                        {
                                            "key": "source",
                                            "value": {
                                                "expression": "[extensionAttribute3]",
                                                "name": "extensionAttribute3",
                                                "type": "Attribute",
                                                "parameters": []
                                            }
                                        }
                                    ]
                                }
                            },
    ```
4. Edit the code so that the company attribute is mapped to `ExtensionAttribute3`.

    ```
                                     {
                                         "defaultValue": null,
                                         "exportMissingReferences": false,
                                         "flowBehavior": "FlowWhenChanged",
                                         "flowType": "Always",
                                         "matchingPriority": 0,
                                         "targetAttributeName": "ExtensionAttribute3",
                                         "source": {
                                             "expression": "Trim([company])",
                                             "name": "Trim",
                                             "type": "Function",
                                             "parameters": [
                                                 {
                                                     "key": "source",
                                                     "value": {
                                                         "expression": "[company]",
                                                         "name": "company",
                                                         "type": "Attribute",
                                                         "parameters": []
                                                     }
                                                 }
                                             ]
                                         }
                                     },
    ```
5. Copy the schema back into Graph Explorer, change the **Request Type** to **PUT**, and select **Run Query**.

    ![Run Query](media/how-to-transformation/transform-2.png)
6. Now, in the portal, go to the cloud sync configuration and select **Restart provisioning**.
7. After a little while, verify the attributes are being populated by running the following query in Graph Explorer: `https://graph.microsoft.com/beta/users/{Azure AD user UPN}`.
8. You should now see the value.

    ![The value appears](media/how-to-transformation/transform-4.png)

## Custom attribute mapping with function

For more advanced mapping, you can use functions that allow you to manipulate the data and create values for attributes to suit your organization's needs.

To do this task, follow the previous steps and then edit the function that's used to construct the final value.

For information on the syntax and examples of expressions, see [Writing expressions for attribute mappings in Microsoft Entra ID](reference-expressions).