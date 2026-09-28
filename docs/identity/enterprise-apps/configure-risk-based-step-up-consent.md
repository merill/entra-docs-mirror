---
layout: Conceptual
title: Configure risk-based step-up consent - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/enterprise-apps/configure-risk-based-step-up-consent
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: omondiatieno
ms.author: jomondi
ms.service: entra-id
ms.subservice: enterprise-apps
manager: dougeby
description: Learn how to disable and enable risk-based step-up consent to reduce user exposure to malicious apps that make illicit consent requests.
ms.topic: how-to
ms.date: 2025-05-21T00:00:00.0000000Z
ms.reviewer: phsignor
ms.custom: enterprise-apps, no-azure-ad-ps-ref,
locale: en-us
document_id: db3269f0-cea2-f300-3bca-a1d5979bf8c2
document_version_independent_id: 0a924307-45b5-ab5c-d444-860cae8f5557
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/enterprise-apps/configure-risk-based-step-up-consent.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/enterprise-apps/configure-risk-based-step-up-consent
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/enterprise-apps/configure-risk-based-step-up-consent.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 8c42af7a-eecc-4ae8-c1b1-136e8eea7614
---

# Configure risk-based step-up consent - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to configure risk-based step-up consent in Microsoft Entra ID. Risk-based step-up consent helps reduce user exposure to malicious apps that make [illicit consent requests](/en-us/microsoft-365/security/office-365-security/detect-and-remediate-illicit-consent-grants).

For example, consent requests for newly registered multitenant apps that aren't [publisher verified](../../identity-platform/publisher-verification-overview) and require nonbasic permissions are considered risky. If a risky user consent request is detected, the request requires a "step-up" to admin consent instead. This step-up capability is enabled by default, but it results in a behavior change only when user consent is enabled.

When a risky consent request is detected, the consent prompt displays a message that indicates that admin approval is needed. If the [admin consent request workflow](configure-admin-consent-workflow) is enabled, the user can send the request to an admin for further review directly from the consent prompt. If the admin consent request workflow isn't enabled, the following message is displayed:

**AADSTS90094**: &lt;clientAppDisplayName&gt; needs permission to access resources in your organization that only an admin can grant. Request an admin to grant permission to this app before you can use it.

In this case, an audit event is also logged with a category of "ApplicationManagement," an activity type of "Consent to application," and a status reason of "Risky application detected."

## Prerequisites

To configure risk-based step-up consent, you need:

- A user account. If you don't already have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- A [Privileged Role Administrator](../role-based-access-control/permissions-reference#privileged-role-administrator).

## Disable or re-enable risk-based step-up consent

Use the [Microsoft Graph PowerShell beta module](/en-us/powershell/microsoftgraph/installation) to disable or enable the admin step-up when a risk is detected.

Important

Make sure you're using the Microsoft Graph PowerShell Beta cmdlets module.

1. Run the following command:

    ```powershell
    Install-Module Microsoft.Graph.Beta
    ```
2. Connect to Microsoft Graph PowerShell:

    ```powershell
    Connect-MgGraph -Scopes "Directory.ReadWrite.All"
    ```
3. Retrieve the current value for the **Consent Policy Settings** directory settings in your tenant. Doing so requires checking to see whether the directory settings for this feature are created. If they aren't created, use the values from the corresponding directory settings template.

    ```powershell
    $consentSettingsTemplateId = "dffd5d46-495d-40a9-8e21-954ff55e198a" # Consent Policy Settings
    $settings = Get-MgBetaDirectorySetting -All | Where-Object { $_.TemplateId -eq $consentSettingsTemplateId }
    if (-not $settings) {
        $params = @{
            TemplateId = $consentSettingsTemplateId
            Values = @(
                @{ 
                    Name = "BlockUserConsentForRiskyApps"
                    Value = "True"
                }
                @{ 
                    Name = "ConstrainGroupSpecificConsentToMembersOfGroupId"
                    Value = "<groupId>"
                }
                @{ 
                    Name = "EnableAdminConsentRequests"
                    Value = "True"
                }
                @{ 
                    Name = "EnableGroupSpecificConsent"
                    Value = "True"
                }
            )
        }
        $settings = New-MgBetaDirectorySetting -BodyParameter $params
    }
    $riskBasedConsentEnabledValue = $settings.Values | ? { $_.Name -eq "BlockUserConsentForRiskyApps" }
    ```
4. Check the value:

    ```powershell
    $riskBasedConsentEnabledValue
    ```

    Understand the settings value:

    | Setting | Type | Description |
    | --- | --- | --- |
    | BlockUserConsentForRiskyApps | Boolean | A flag indicating whether user consent is blocked when a risky request is detected. |
5. To change the value of `BlockUserConsentForRiskyApps`, use the [Update-MgBetaDirectorySetting](/en-us/powershell/module/microsoft.graph.beta.identity.directorymanagement/update-mgbetadirectorysetting) cmdlet.

    ```powershell
    $params = @{
        TemplateId = $consentSettingsTemplateId
        Values = @(
            @{ 
                Name = "BlockUserConsentForRiskyApps"
                Value = "False"
            }
            @{ 
                Name = "ConstrainGroupSpecificConsentToMembersOfGroupId"
                Value = "<groupId>"
            }
            @{ 
                Name = "EnableAdminConsentRequests"
                Value = "True"
            }
            @{ 
                Name = "EnableGroupSpecificConsent"
                Value = "True"
            }
        )
    }
    Update-MgBetaDirectorySetting -DirectorySettingId $settings.Id -BodyParameter $params
    ```