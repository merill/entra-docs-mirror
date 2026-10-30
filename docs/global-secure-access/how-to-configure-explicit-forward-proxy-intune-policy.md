---
layout: Conceptual
title: Configure a Microsoft Edge Application Management Policy for Explicit Forward Proxy - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-explicit-forward-proxy-intune-policy
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: alexpav
ms.service: global-secure-access
manager: dougeby
description: Learn how to configure a Microsoft Intune app management policy for Microsoft Edge to use the Explicit Forward Proxy feature of Global Secure Access.
ms.topic: how-to
ms.date: 2026-04-22T00:00:00.0000000Z
ms.subservice: entra-internet-access
locale: en-us
document_id: 595dc0e4-ee63-f059-3b56-678d9f0f005c
document_version_independent_id: 595dc0e4-ee63-f059-3b56-678d9f0f005c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/how-to-configure-explicit-forward-proxy-intune-policy.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/how-to-configure-explicit-forward-proxy-intune-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/how-to-configure-explicit-forward-proxy-intune-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: eed08a49-bb7a-12d0-4913-47b842f1d008
---

# Configure a Microsoft Edge Application Management Policy for Explicit Forward Proxy - Global Secure Access | Microsoft Learn

You can automatically deliver proxy settings and certificate authority trust settings in Microsoft Edge by using an Intune mobile application management (MAM) policy. The policy can take advantage of the Explicit Forward Proxy feature of Global Secure Access.

## Prerequisites

- A Microsoft Entra identity with at least the Global Secure Access Administrator Reader role and Intune Administrator role.
- Explicit Forward Proxy configured in the Microsoft Entra admin center.
- A security group in Microsoft Entra ID with users who should receive Explicit Forward Proxy configuration in Microsoft Edge.
- The plain-text public key of the Transport Layer Security (TLS) inspection root certificate that you used when you configured Microsoft Entra Internet Access TLS inspection.

## Limitations

- This method to apply a policy works only on Microsoft Edge for Windows.
- If mobile device management (MDM) is configured on the device, and the MDM policy has conflicting Microsoft Edge settings, the MAM policy isn't applied.

## Configuration

### 1. Get the URL of the PAC file

1. Open the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Go to **Global Secure Access** &gt; **Settings** &gt; **Session management** &gt; **Explicit Forward Proxy**.
3. Copy the URL of the proxy automatic configuration (PAC) file. Save it for the Intune app management policy that you configure next.

### 2. Select Microsoft Edge for the app

1. Open the [Intune admin center](https://intune.microsoft.com).
2. Under **Apps** &gt; **Manage apps**, select **Configuration**.
3. Select **+ Create** &gt; **Managed Apps**.
4. For **Name**, enter a name of your choice. For example, enter **GSA Explicit Forward Proxy Settings for Edge**.
5. For **Target policy to**, choose **Selected apps**.
6. Choose **+ Select public apps**. In the **Select apps to target** pane:

    1. Search for **Edge**.
    2. Select **Microsoft Edge** / **Windows**.
    3. Choose **Select**.

    ![Screenshot that shows Microsoft Edge and Windows selected for a public app.](media/how-to-configure-microsoft-edge-mam-policy/select-target-apps.png)
7. Select **Next** to advance to the **Settings catalog** tab.

### 3. Add proxy settings

1. Select **+ Add setting**. In the **Settings picker** pane:

    1. Enter **proxy** in the search box, and then select **Search**.
    2. In the results, select **Microsoft Edge/Proxy server**.
    3. Select the **Proxy settings** checkbox.

        ![Screenshot that shows the configuration of proxy settings.](media/how-to-configure-microsoft-edge-mam-policy/proxy-settings.png)
    4. Enter **TLS** in the search box, and then select **Search**.
    5. In the search results, select **Microsoft Edge Certificate management settings**.
    6. Select the **TLS server certificates that should be trusted by Microsoft Edge** checkbox.

        ![Screenshot that shows the configuration of TLS certificate settings.](media/how-to-configure-microsoft-edge-mam-policy/tls-certificate-settings.png)
    7. Close the **Settings picker** pane (**X** on the upper right).
2. In the **Proxy Server** section, configure proxy settings as follows:

    ```json
    {"ProxyMode":"pac_script","ProxyPacMandatory":false,"ProxyPacUrl":"URL_you_copied_from_the_Entra_portal"}
    ```

### 4. Convert the key into a string

Convert the TLS inspection root public key (certificate) to a contiguous plain-text string. You can use either PowerShell or a Linux/macOS terminal.

#### PowerShell

1. Change the directory to where the `.pem` or `.cer` plain-text key is stored.
2. Confirm that the key is plain text by running the following command:

    ```powershell
    if ((Get-Content cert.pem -First 1) -match '-----BEGIN') { 'PEM (plain text)' } else { 'DER (binary)' }
    ```

    If the output is `PEM (plain text)`, you can continue. Otherwise, convert the binary encoded file to PEM.
3. Convert the PEM certificate string to extract only the key, without the line breaks:

    ```powershell
    (Get-Content cert.pem | Where-Object { $_ -notmatch '-----' }) -join ''
    ```
4. Copy the resulting string from the console output and save it for the next step.

#### Linux/macOS terminal

1. Change the directory to where the `.pem` or `.cer` plain-text key is stored.
2. Confirm that the key is plain text by running the following command:

    ```bash
    head -c 15 cert.pem | grep -q 'BEGIN' && echo 'PEM (plain text)' || echo 'DER (binary)'
    ```

    If the output is `PEM (plain text)`, you can continue. Otherwise, convert the binary encoded file to PEM.
3. Extract the key from the file, without the line breaks:

    ```bash
    awk '!/-----/{printf "%s",$0}' cert.pem | tr -d '\r'
    ```
4. Copy the resulting string from the console output and save it for the next step. Don't copy the trailing `%` if it appears in the terminal output.

### 5. Paste the copied string

1. In the **Certificate management settings** section, paste the output of the converted, plain-text string (without line breaks) into the text box.

    Note

    Don't use the **Import** button in this section. Import is intended for bulk configuration settings, where you have multiple certificates that need to be trusted. The import function of the Intune portal expects a CSV file with a list of plain-text contiguous keys, not the PEM/CER file.
2. Your resulting configuration should look similar to the following screenshot. Select **Next**.

    ![Screenshot that shows a completed proxy and certificate configuration.](media/how-to-configure-microsoft-edge-mam-policy/completed-settings-configuration.png)

### 6. Assign the security group and create the policy

1. On the **Settings** tab, select **Next**.
2. On the **Assignments** tab:

    1. Select **Add Groups**.
    2. Select the security group in Microsoft Entra ID that contains users of Explicit Forward Proxy.
    3. Select **Next**.
3. Your **Review + create** tab should look similar to the following screenshot. Select **Create**.

    ![Screenshot that shows the tab for reviewing and creating a configured policy.](media/how-to-configure-microsoft-edge-mam-policy/review-create.png)

## Validation

1. Open Microsoft Edge on a Windows device. Sign in with a work or school account.
2. Go to `edge://policy`. Confirm that the policy settings that you configured for Explicit Forward Proxy appear.

    ![Screenshot that shows configured Microsoft Edge policy settings for Explicit Forward Proxy.](media/how-to-configure-microsoft-edge-mam-policy/edge-policy-validation.png)