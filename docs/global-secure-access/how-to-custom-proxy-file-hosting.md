---
layout: Conceptual
title: Host custom Proxy Automatic Configuration files for Explicit Forward Proxy in Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-custom-proxy-file-hosting
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: idMdev
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Learn how to upload and host your own Proxy Auto-Configuration (PAC) files
ms.topic: how-to
ms.date: 2026-06-19T00:00:00.0000000Z
locale: en-us
document_id: f168fc48-ef2d-3060-43ad-36d40cb2edbc
document_version_independent_id: f168fc48-ef2d-3060-43ad-36d40cb2edbc
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-custom-proxy-file-hosting.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-custom-proxy-file-hosting
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-custom-proxy-file-hosting.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/05a837ba-792f-460a-9e68-3842c0ffd1c0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6640a16a-1cc5-458f-8945-86702f70af60
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: c133f110-96c7-7032-df45-6cc4c449b46f
---

# Host custom Proxy Automatic Configuration files for Explicit Forward Proxy in Microsoft Entra Internet Access - Global Secure Access | Microsoft Learn

Important

The Explicit Forward Proxy feature is currently in preview. This information relates to a prerelease product that might be substantially modified before release. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Global Secure Access (GSA) Explicit Forward Proxy (EFP) automatically generates a Proxy Automatic Configuration (PAC) file that routes traffic through the service with recommended settings. If you need more control over proxy routing decisions, you can host your own custom PAC files.

Custom PAC files allow you to:

- Exclude specific hosts or IP ranges from Explicit Forward Proxy traffic acquisition.
- Route traffic to different proxies based on URL patterns or destination hosts for coexistence with your existing proxy solutions.
- Implement proxy logic relevant to your organization.

## Prerequisites

- A Global Secure Access license. For more information about licensing, see [Global Secure Access licensing](/en-us/entra/global-secure-access/overview-what-is-global-secure-access#licensing).
- An administrator account with the [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator) role.
- Explicit Forward Proxy [enabled and configured](/en-us/entra/global-secure-access/how-to-configure-explicit-forward-proxy) in your tenant.

## Create a custom PAC file

Note

While custom PAC file hosting validates basic JavaScript, it does not validate your intent for traffic routing and JavaScript logic that was implemented. We recommend that you approach PAC files as any other custom code artifact and review the code before relying on it in production. One way to achieve this is to use AI tools to review proposed PAC file contents and check it for validity, syntax, and intended logic. Example prompt: "Analyze this custom proxy automatic configuration file for explicit forward proxy. Check for syntax and routing decisions logic. Produce a report that includes details on what conditions influence routing decisions."

1. Sign in to the [Microsoft Entra Admin Center](https://entra.microsoft.com) as at least a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Session Management**.
3. Select the **Explicit Forward Proxy** tab.
4. In the **Internet Access** section, select the link to download the default PAC file for your tenant. [![Screenshot of the Explicit Forward Proxy configuration page.](media/how-to-custom-proxy-autoconfiguration-files/download-template.png)](media/how-to-custom-proxy-autoconfiguration-files/download-template.png#lightbox)

Important

PAC files use JavaScript syntax, which is a case-sensitive language. When you use variables in the PAC file script, ensure that the casing of the variables is consistent. This means that the variable named **efpURL** is different than the variable named **efpUrl**. Always validate JavaScript syntax when working with custom PAC files.

1. Open the downloaded PAC file in a text editor.
2. Delete lines that start with "var tenantId" and "var efpEndpoint".
3. Update the line that starts with "var efpUrl" to the following code:

    ```javascript
    var efpUrl = "HTTPS ${GSAEFP}";
    ```
4. Make your modifications to implement your custom PAC file logic. Always use the **${GSAEFP}** variable when you reference the EFP proxy endpoint.
5. Save the PAC file with a \*.pac extension.
6. Next to **Custom PAC files**, select **Manage**.
7. Select **+ Add PAC file**.
8. Enter a unique **Name** for the PAC file. The `.pac` extension is appended automatically.
9. Select **Load from file**. In the file picker dialog box, find the custom PAC file you modified and select it. [![Screenshot of the Explicit Forward Proxy upload file page.](media/how-to-custom-proxy-autoconfiguration-files/upload-file.png)](media/how-to-custom-proxy-autoconfiguration-files/upload-file.png#lightbox)
10. Set the **Enabled** toggle to **On** when you're ready to make the file available to devices.
11. Select **Save**. [![Screenshot of the Explicit Forward Proxy save configuration page.](media/how-to-custom-proxy-autoconfiguration-files/save-configuration.png)](media/how-to-custom-proxy-autoconfiguration-files/save-configuration.png#lightbox)

## Edit a custom PAC file

1. In the **Custom PAC files** panel, select the PAC file you want to edit.
2. Make your changes in the editor.
3. Select **Save**.

Important

Connected devices cache PAC files. Edits to an enabled file can take some time to roll out to all devices using the file.

## Enable or disable a custom PAC file

You can enable or disable a custom PAC file without deleting it:

1. In the **Custom PAC files** panel, select the PAC file.
2. Toggle the **Enabled** switch on or off.
3. Select **Save**.

When a PAC file is disabled, users with browsers that are configured with the URL of that PAC could experience issues with accessing resources. Ensure that browser PAC file settings are reconfigured before you disable existing PAC files.

## PAC file placeholder variables

Global Secure Access provides placeholder variables that are substituted with the correct values when the PAC file is served to devices. Variable values are replaced contextually at the time when the browser requests the PAC file.

| Variable | Description |
| --- | --- |
| `${GSAEFP}` | The Explicit Forward Proxy hostname for your tenant. To route traffic through GSA EFP, use this variable in `PROXY` or `HTTPS` return statements. |

## Considerations and limitations

- **Caching**: Connected devices cache PAC files. When you edit an enabled PAC file, changes might take time to propagate to all devices.
- **Maximum PAC file size**: you can upload files that are up to 950 KB in size. Larger PAC files take longer to load and we recommend that you avoid exceeding 250 KB for each PAC file.
- **Maximum number of PAC files**: you can have up to 20 PAC files hosted in your tenant.