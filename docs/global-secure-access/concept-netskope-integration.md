---
layout: Conceptual
title: 'Global Secure Access: Advanced Threat Protection - Global Secure Access | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/concept-netskope-integration
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn how to protect your organization with Global Secure Access Advanced Threat Protection (ATP) and Data Loss Prevention (DLP) policies powered by Netskope.
ms.topic: how-to
ms.date: 2025-11-07T00:00:00.0000000Z
ms.reviewer: abhijeetsinha
ai-usage: ai-assisted
locale: en-us
document_id: 9781f51c-6f76-54b0-f0ce-71316598c59e
document_version_independent_id: 9781f51c-6f76-54b0-f0ce-71316598c59e
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/concept-netskope-integration.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/concept-netskope-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/concept-netskope-integration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/00675be6-8413-445a-927c-01fdfb06925d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/3f4c9937-0bf4-403a-90e9-153dbfe1b4c3
platformId: 0f4a2ce2-d0cc-22c4-2176-332fbb9ee2f2
---

# Global Secure Access: Advanced Threat Protection - Global Secure Access | Microsoft Learn

In today's evolving threat landscape, organizations face challenges protecting sensitive data and systems from cyberattacks. Global Secure Access Advanced Threat Protection (ATP) combines Microsoft Security Service Edge (SSE) with Netskope's advanced threat detection and data loss prevention (DLP) capabilities to deliver a comprehensive security solution. This integration offers real-time protection against malware, zero-day vulnerabilities, and data leaks, and simplifies management through a unified platform.

This guide provides step-by-step instructions for configuring ATP and DLP policies to safeguard your organization. By following these steps, IT administrators can apply the power of Microsoft SSE and Netskope to enhance their organization's security posture and streamline threat management.

**High-level architecture**![Diagram that shows how data is routed and analyzed between Microsoft Entra, Global Secure Access, and Netskope.](media/concept-netskope-integration/high-level-architecture.png)

## Prerequisites

To complete these steps, make sure you have the following prerequisites:

- A Global Secure Access Administrator role in Microsoft Entra ID to configure Global Secure Access settings.
- A tenant configured with a Transport Layer Security (TLS) inspection policy as described in [Configure Transport Layer Security Inspection](how-to-transport-layer-security).
- Devices or virtual machines running Windows 10 or Windows 11 that are joined or hybrid joined to a Microsoft Entra ID.
- Devices with the Global Secure Access client installed. See [Global Secure Access client for Microsoft Windows](how-to-install-windows-client) for requirements and installation instructions.
- A Conditional Access Administrator role to configure Conditional Access policies.
- Trial Microsoft Entra Internet Access licenses. For licensing details, see the Global Secure Access [Licensing overview](overview-what-is-global-secure-access#licensing-overview). You can purchase licenses or get trial licenses. To activate an Internet Access trial, browse to https://aka.ms/InternetAccessTrial.

Important

Complete and verify the configuration steps marked **Important** before proceeding.

### Enable the Internet access traffic profile

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Browse to **Global Secure Access** &gt; **Connect** &gt; **Traffic forwarding** and enable the Internet access profile.
3. Under **Internet access profile** &gt; **User and Group assignments**, select **View** to choose the participating users.

    For more information, see [How to manage the Internet Access traffic forwarding profile](how-to-manage-internet-access-profile).

    Important

    Before continuing, check that your client's internet traffic is routed through the Global Secure Access service.
4. On your test device, right-click the Global Secure Access icon in the system tray and select **Advanced diagnostics**.
5. On the **Forwarding Profile** tab, verify **Internet Access rules** are present in the **Rules** section. This configuration can take up to 15 minutes to apply to clients after you enable the Internet access traffic profile.

![Screenshot of the Forwarding Profile tab with the Internet access rules highlighted.](media/concept-netskope-integration/internet-access-rules.png)

### Enable TLS inspection

A large percentage of internet traffic is encrypted. Terminating TLS at the edge lets Global Secure Access inspect and apply security policies to decrypted traffic. This process enables threat detection, content filtering, and granular access controls.

To enable TLS inspection, follow the steps in [Configure Transport Layer Security Inspection](how-to-transport-layer-security).

Caution

You must configure TLS inspection on your tenant before purchasing Netskope from the marketplace.

## Enable and test ATP and DLP policies

You can create ATP and DLP policies powered by Netskope engines directly from the Microsoft Entra admin center by completing the following high-level steps. Details for each step follow.

1. Activate the Netskope offer through the Global Secure Access marketplace
2. Create an ATP policy
3. Create a DLP policy
4. Link an ATP, DLP, or TLS inspection policy to the security profile
5. Create a conditional access policy to enforce ATP, DLP, and TLS inspection policies
6. Test ATP policies
7. Test DLP Policies

### Activate a Netskope offer through the Global Secure Access marketplace

You can activate a free trial or contact Netskope for a private offer. Select the tab to follow the steps for your preferred option.

# [Free trial](#tab/free-trial)
To activate a free trial of Netskope through the Global Secure Access marketplace:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Third Party Security Solutions** &gt; **Marketplace**.
3. Select the Netskope **Get it Now** button.
4. Select **Try free for 30 days**.[![Screenshot showing the Netskope One marketplace page with the Try free for 30 days button highlighted.](media/concept-netskope-integration/try-free-thirty.png)](media/concept-netskope-integration/try-free-thirty.png#lightbox)
5. Complete the form to request the trial.
6. Netskope reaches out within two business days to alert you if they accepted or rejected the trial.
7. If Netskope accepts your trial request, return to the Microsoft Entra admin center.
8. Browse to **Global Secure Access** &gt; **Third Party Security Solutions** &gt; **Marketplace**.
9. Select the Netskope **Get it Now** button.
10. Select **Validate Netskope license**. This step provisions Netskope for your tenant and begins the 30-day trial period.
11. After 30 days, the free trial expires.[![Screenshot showing that the Netskope trial is expired.](media/concept-netskope-integration/offer-expired.png)](media/concept-netskope-integration/offer-expired.png#lightbox)

# [Private offer](#tab/private-offer)
To contact Netskope to request a private offer for your tenant:

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](../identity/role-based-access-control/permissions-reference#global-secure-access-administrator).
2. Browse to **Global Secure Access** &gt; **Third Party Security Solutions** &gt; **Marketplace**.
3. Select the Netskope **Get it Now** button.
4. Select **Contact Netskope for private plan**.[![Screenshot showing the Netskope One marketplace page with the Contact Netskope for private plan button highlighted.](media/concept-netskope-integration/contact-private-plan.png)](media/concept-netskope-integration/contact-private-plan.png#lightbox)
5. Complete the form to request the private offer.
6. Netskope reaches out within two business days to discuss the private offer.
7. After agreeing to the private offer terms with Netskope, return to the Microsoft Entra admin center.
8. Browse to **Global Secure Access** &gt; **Third Party Security Solutions** &gt; **Marketplace**.
9. Select the Netskope **Get it Now** button.
10. Select **Validate Netskope license**. This step provisions Netskope for your tenant.
11. Once the offer is provisioned, the **Offers** page lists the Netskope status as **Active**.![Screenshot of the Offers page with the Netskope status of Active highlighted.](media/concept-netskope-integration/offers-active.png)

---

### Create an ATP policy

1. Browse to **Global Secure Access** &gt; **Secure** &gt; **Threat Protection policies**.
2. Select **+ Create policy**.
3. On the **Basics** tab:

    1. Set the **Security provider** to **Netskope**.
    2. Enter a **Policy name**.
    3. Select the policy **Position**.
        - The position sets the policy priority when Netskope processes multiple ATP and DLP policies.
        - Netskope's ATP and DLP policies share a common ordering list. The position you specify applies to both ATP and DLP policies in Netskope. For example, Netskope\_ATP\_Policy\_1 might have a position of 1, followed by Netskope\_DLP\_Policy\_1 with a position of 2, and Netskope\_ATP\_Policy\_2 with a position of 3.
        - If you assign a position that another Netskope ATP or DLP policy already uses, the positions of the lower policies automatically shift down by one.
    4. Set the **State** to **enabled**.
    5. Select **Next**.
4. On the **Policy** tab:

    1. Select the **Select destination** link.
    2. For **Destination type**, select **category** or **application**.
    3. Search for and select the desired categories or applications. To determine which Netskope web category to select, refer to the [Netskope URL categorization lookup](https://www.netskope.com/url-lookup).
    4. Select **Apply**.
    5. Select the type of **Activity** that triggers the policy: **upload** (data flowing from the user to the internet), **download** (data flowing from the internet to the user), or **upload download**.
    6. For **Action**, select the **Select action** link and set the action for **Low**-, **Medium**-, and **High**-level threat severities. These settings direct the threat engine on which action to take for each threat severity.
    7. Select **Apply**.
    8. The **Advanced settings** allow you to select the **Patient zero** option, which signals the threat engine to run more diagnostics on the threat and blocks the user from uploading or downloading until the threat engine reaches a verdict. These diagnostics can take up to 15 minutes.

        Note

        Don't check the **Patient zero** check box unless you explicitly understand and want to include the feature behavior. When Patient zero is enabled, the policy matches *only* binary and executable file types. The implications for Patient zero are:

        - If the file type is binary and executable, and the Netskope threat engine has a verdict, the threat engine takes the action that matches the policy.
        - If the file type is binary and executable, and the Netskope threat engine doesn't have a verdict, the threat engine blocks the activity.
        - If the file type isn't binary and executable, the file doesn't match the policy.

    For ATP policy recommendations from Netskope, refer to the FAQ section of this document.
5. Select **Next**.
6. Review the details and select **Submit**.

### Create a DLP policy

1. Browse to **Global Secure Access** &gt; **Secure** &gt; **Data Loss Prevention policies**.
2. Select **+ Create policy** &gt; **Netskope policies**.
3. On the **Basics**tab:
    1. Enter a **Name** and **Description** (optional) for the policy.
    2. Select the policy **Position**. The position sets the policy priority when Netskope processes multiple ATP and DLP policies.
    3. Set the **State** to **Enabled**.
    4. Select **Next**.
4. On the **Policy**tab:
    1. Select the **Select destinations** link.
    2. For **Destination type**, select **Categories** or **Applications**.
    3. Search for and select the desired categories or applications.
    4. Select **Apply**.
    5. Choose the type of **Activity** that should be subject to this policy. Select both **Upload** and **Download**. The activities available vary according to the categories and applications you select. In addition to **Upload** and **Download**, Netskope offers granular support for a wide range of activities for various applications and application categories. These categories allow you to apply comprehensive data loss prevention policies to secure data in your business-critical applications and application categories.
    6. To choose from and configure DLP profiles, select the **Select profiles** link. You can choose from DLP profiles that cover predefined data identifiers and personal identifiers such as financial data, medical data, biodata, inappropriate terms, and industry focused information.
    7. Select the DLP profiles that match your required information types and select the action to enforce for each. (For initial testing purposes, select **DLP-PCI** and **DLP-PII**.)
    8. Select **Apply**.
    9. Optionally, select the **Select advanced settings** link and select **Continue policy evaluation**. The Continue Policy evaluation option ensures DLP policy evaluation doesn't stop after a DLP policy match. Every DLP match raises an alert and policy evaluation continues for each of the remaining DLP policies. Alternatively, if you prefer to stop policy evaluation after the first DLP match and *not* continue with the rest of the DLP policies, don't select the **Continue policy evaluation** option.
    10. Select **Apply**.
    11. Select **Next**.
5. Review the details and select **Submit**.

For instructions on how to create custom DLP profiles, see [Create a custom DLP profile](how-to-full-data-loss-protection).

### Link an ATP, DLP, or TLS inspection policy to the security profile

Use **Security profiles** and **Conditional Access** to assign ATP and DLP policies to users.

1. Browse to **Global Secure Access** &gt; **Secure** &gt; **Security profiles**.
2. Select the security profile you want to modify.
3. Switch to the **Link policies** view.
4. Link an ATP policy:
    1. Select **+ Link a policy** &gt; **Existing Threat Protection policy**.
    2. From the **Policy name** menu, choose the Threat Protection policy you created.
    3. Leave **Position** and **State** set to the defaults.
    4. Select **Add**.
5. Link a DLP policy:
    1. Select **+ Link a policy** &gt; **Existing Netskope DLP policy**.
    2. From the **Policy name** menu, choose the DLP policy you created.
    3. Leave **Position** and **State** set to the defaults.
    4. Select **Add**.
6. Link a TLS inspection policy:
    1. Select **+ Link a policy** &gt; **Existing TLS inspection policy**.
    2. From the **Policy name** menu, choose the TLS inspection policy you created.
    3. Leave **Priority** and **State** set to the defaults.
    4. Select **Add**.
7. Close the Security Profile.

To prevent confusion between Microsoft and Netskope policies, Netskope policies include **NS** in their priority listing. The platform evaluates Microsoft security policies first. The traffic then goes to Netskope, which applies ATP and DLP policies before sending the traffic to its destination.

![Screenshot of the Link policies view showing the NS marker that identifies Netskope ATP and DLP policies.](media/concept-netskope-integration/link-policies.png)

Note

Don't use the baseline security profile to enforce ATP and DLP policies, as the baseline security profile isn't supported during this preview.

### Create a conditional access policy to enforce ATP, DLP, and TLS inspection policies

To enforce the Global Secure Access security profile and TLS inspection policy, create a conditional access policy with the following details. For more information, see [Create and link Conditional Access policy](how-to-configure-web-content-filtering#create-and-link-conditional-access-policy).

| **Policy detail** | **Description** |
| --- | --- |
| **Users** | Select your test users. |
| **Target resources** | All internet resources with Global Secure Access. |
| **Session** | Use the Global Secure Access security profile you created. |

### Validate your configuration

Because of token life validity on the Global Secure Access client, changes to the Security Profile policy or the ATP policy can take up to one hour to apply.

To ensure that TLS inspection works as expected, disable QUIC protocol support for your browsers. To disable QUIC, see [QUIC not supported for Internet Access](troubleshoot-global-secure-access-client-diagnostics-health-check#quic-not-supported-for-internet-access). For more detail, see the troubleshooting section TLS inspection only works on some sites.

Important

Before proceeding, validate your configuration settings.

To validate your configuration settings:

1. Validate that the client device has the Global Secure Access client installed.
2. Validate that the corresponding Security Profile using Conditional Access is enforced.
3. Browse to [netskope.com/url-lookup](https://www.netskope.com/url-lookup).

**Success**: If you see a search field and **Search** button, Netskope is analyzing your traffic and the policies are in effect. [![Screenshot of Netskope URL Lookup page showing a search field and Search button, indicating successful traffic analysis and active policies.](media/concept-netskope-integration/lookup-success.png)](media/concept-netskope-integration/lookup-success.png#lightbox)

**Failure**: If you see the message, "The URL Lookup is only available for Netskope customers. Use a Netskope steering method to access this service.", the test failed. Check the Troubleshooting section for guidance.[![Screenshot of Netskope URL Lookup failure message indicating that the service is restricted to Netskope customers.](media/concept-netskope-integration/lookup-fail.png)](media/concept-netskope-integration/lookup-fail.png#lightbox)

### Test ATP policies

To test your ATP policies, use the European Institute for Computer Antivirus Research (EICAR) anti-malware test file. For more advanced testing, engage your security or red teams. For the EICAR test:

1. Sign in to the test device by using a test user targeted by the Conditional Access policy you created.
2. Download the [EICAR test file](http://secure.eicar.org/eicar_com.zip). If Microsoft Defender SmartScreen blocks the download, select **More actions**, then select **Keep**.
3. Disable QUIC protocol support for your browsers. To disable QUIC, see [QUIC not supported for Internet Access](troubleshoot-global-secure-access-client-diagnostics-health-check#quic-not-supported-for-internet-access).

### Test DLP policies

To test the DLP policy:

1. Validate **DLP-PCI** and **DLP-PII** DLP profiles as suggested in the Create a DLP policy section.
2. Open a test file that contains PCI and PII data, such as https://dlptest.com/sample-data.pdf.
3. If the policy is configured properly, the action is blocked with the following message:

'**Non-compliant action**. The current operation is blocked by your IT administrator.'

## Monitoring and logging

Check alerts by going to **Global Secure Access** &gt; **Dashboard**.

### Threat alerts

To view threat alerts, go to **Global Secure Access** &gt; **Alerts**. [![Screenshot of the Alerts dashboard showing a list of detected alerts.](media/concept-netskope-integration/threat-alerts-dashboard.png)](media/concept-netskope-integration/threat-alerts-dashboard.png#lightbox)

More reporting might be available depending on the type of threat, such as **Malware detected** or **Data loss prevention**. Select the alert **Description** to inspect the alert type and view more details.

1. Expand the **Entities** section.
2. Switch to the **File hash** tab.
3. To download the Structured Threat Information eXpression threat report, select **Download malware STIX report**.
4. To download detonation images, if available, select **Download additional malware details**.[![Screenshot of the Entities section with malware download links highlighted.](media/concept-netskope-integration/file-hash-links.png)](media/concept-netskope-integration/file-hash-links.png#lightbox)
5. To view the threat URL, switch to the **URL** tab.

### Traffic logs

To view traffic logs, go to **Global Secure Access** &gt; **Monitor** &gt; **Traffic logs**.

To show all traffic subject to Netskope inspection:

1. Go to the **Transactions** tab.
2. Select **Add filter**.
3. Search for or scroll to find the **Vendor names** filter.
4. Enter `Netskope` in the field to show only Netskope traffic.
5. Select **Apply**.[![Screenshot of the Traffic logs with the Vendor names contains Netskope filter highlighted.](media/concept-netskope-integration/traffic-logs-filter.png)](media/concept-netskope-integration/traffic-logs-filter.png#lightbox)

This sample shows an event triggered by an ATP policy with blocked content. Check the **filteringProfileName** and **policyName** to identify the policies responsible for the applied action.

```json
{
    "action": "Block",
    "agentVersion": "1.7.669",
    "connectionId": "0000000000000000.0.0",
    "createdDateTime": "07/25/2024, 05:00 PM",
    "destinationFQDN": "secure.eicar.org",
    "destinationIp": "172.16.0.0",
    "destinationPort": "0000",
    "destinationWebCategory/displayName": "General,IllegalSoftware",
    "deviceCategory": "Client",
    "deviceId": "00001111-aaaa-2222-bbbb-3333cccc4444",
    "deviceOperatingSystem": "Windows 10 Pro",
    "deviceOperatingSystemVersion": "10.0.19045",
    "filteringProfileId": "11112222-bbbb-3333-cccc-4444dddd5555",
    "filteringProfileName": "ATP Profile",
    "headers/origin": "secure.eicar.org",
    "headers/referrer": "secure.eicar.org/text.html",
    "headers/xForwardedFor": "10.0.0.0",
    "initiatingProcessName": "chrome.exe",
    "networkProtocol": "IPv4",
    "policyId": "22223333-cccc-4444-dddd-5555eeee6666",
    "policyName": "Block Malware",
    "policyRuleId": "33334444-dddd-5555-eeee-6666ffff7777",
    "policyRuleName": "*",
    "receivedBytes": "14.78 KB",
    "resourceTenantId": "",
    "sentBytes": "0 bytes",
    "sessionId": "",
    "sourceIp": "clipped",
    "sourcePort": "00000",
    "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
    "trafficType": "Internet",
    "transactionId": "55556666-ffff-7777-aaaa-8888bbbb9999",
    "transportProtocol": "TCP",
    "userId": "ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0",
    "userPrincipalName": "user@contoso.com",
    "vendorNames": "Netskope"
}
```

## Troubleshooting

Try the following recommendations if you experience issues while configuring or using the Global Secure Access Advanced Threat Protection (ATP) and DLP integration with Netskope.

### I can't create a Netskope ATP or DLP policy

Check if you have an active Netskope offer.

### I can't purchase a Netskope offer, or the status shows as failed

Important

You must set up TLS inspection before purchasing a Netskope offer from the marketplace.

To enable TLS inspection, follow the steps in [Configure Transport Layer Security Inspection](how-to-transport-layer-security).

### I configured TLS inspection and now get errors browsing the internet

If you see errors like "Your connection isn't private" or other certificate errors, check that

- You imported the Certificate Authority certificate used to sign the TLS inspection certificate to the device.
- You placed the Certificate Authority certificate in the correct certificate store, **Trusted Root Certificate Authorities**.

### Check that TLS inspection is working correctly

To check if TLS inspection is working correctly, go to the website you'd like to check, select the **View site information** icon, and then select **Connection is secure**. Select the **Show certificate** icon and validate the issuer of the certificate is **Microsoft Global Secure Access Intermediate**. The presence of this certificate issuer indicates Microsoft intercepted the TLS session.[![Screenshot of the Certificate Viewer dialog showing the issuer of the certificate is Microsoft Global Secure Access Intermediate.](media/concept-netskope-integration/certificate-viewer.png)](media/concept-netskope-integration/certificate-viewer.png#lightbox)

If you configured TLS inspection correctly, waited at least 10 minutes after configuring it, and still don't see TLS sessions issued by Microsoft Global Secure Access Intermediate, check the configuration of your host file.

### TLS inspection only works on some sites

The Global Secure Access client doesn't currently intercept requests that use the QUIC protocol. The Global Secure Access client has a check for QUIC status within **Advanced diagnostics** &gt; **Health check**. To disable QUIC in your browser, see [QUIC not supported for Internet Access](troubleshoot-global-secure-access-client-diagnostics-health-check#quic-not-supported-for-internet-access).

### Check which Netskope web category a URL maps to

To ensure Netskope policies are set to the correct web or application categories, refer to the Netskope URL categorization lookup: https://www.netskope.com/url-lookup. To successfully access the lookup tool, the request must go through Netskope proxies, which requires at least one Netskope policy to be configured and linked to the security profile in use. **Note**: web categories Education, Government, Finance, and Health and Medicine aren't inspected by default.

### Check if Netskope ATP is analyzing your traffic

To test if Netskope's ATP engine is analyzing traffic, check the test machine's egress IP address by going to https://iplocation.net. Check the ISP field to confirm whether traffic is routed through Netskope's ATP engine.[![Screenshot of the IP Location website with the ISP field showing that the traffic is routed through Netskope.](media/concept-netskope-integration/ip-location.png)](media/concept-netskope-integration/ip-location.png#lightbox)

Note

If you can't access either of the lookup websites on the test machine with Netskope ATP policy active, and the policy has a **default** action set to block, the block might be due to policy rules.

## Known limitations

Known limitations for Advanced Threat Protection include:

- The baseline security profile doesn't support enforcing ATP or DLP policies in this preview. Use Security Profiles and Conditional Access to assign threat protection policies to users.
- Firefox isn't supported.

## Frequently asked questions (FAQ)

### What threat efficacy does Netskope ATP provide?

Netskope ATP provides Fast Scan and Deep Scan options.

- Fast Scan is the default option. It provides real-time (T+0) scans using Netskope's standard threat protection.
- Deep Scan provides more thorough T+1-hour scans using Netskope's advanced threat protection.

### Are there any recommended threat protection policies?

Yes, Netskope recommends creating these two category-based policies for threat protection:

| Policy | Destination categories | Activities | Severity-based action | Patient Zero |
| --- | --- | --- | --- | --- |
| Policy 1 (without Patient Zero) | All (Select all the categories in the destinations list) | Upload and Download | 'Block' for all | Not enabled |
| Policy 2 (with Patient Zero) | Newly registered domains, Newly observed domains, Parked Domains, Uncategorized, Web Proxies/Anonymizers | Upload and Download | 'Block' for all | Enabled |

Note

For the Netskope advanced threat protection policy, the patient zero setting only applies to binary and executable files (for more detail, see [Supported File Types for Detection](https://docs.netskope.com/en/supported-file-types-for-detection/)). When the patient zero setting is enabled, only binary and executable files are sent for threat scanning. The threat engine blocks new files until it reaches a verdict. Because of the default blocking nature, it's a good practice to enable the threat protection policies in the preceding table.

### What is the pricing of Microsoft products and Netskope functionality?

You can activate a free trial or contact Netskope for a private offer. For details, see Activate a Netskope offer through the Global Secure Access marketplace.

### What activities do Netskope threat engines support?

Netskope threat engines support three activities: **Upload**, **Download**, and **Browse**.

By default, Netskope scans traffic categorized as 'Browse,' so you don't need to configure a policy. You can configure 'Upload' and 'Download' via policies that match your requirements. For more information on Netskope web activities and policy usage, see Netskope's documentation on [Real-time Protection Policies](https://docs.netskope.com/en/inline-policies/).

### How can I customize or modify DLP profiles to suit organizational policies?

For instructions on how to create custom DLP profiles, see [Create a custom DLP profile](how-to-full-data-loss-protection).

Learn more about Netskope Threat Protection in these articles:

- [Netskope Threat Protection overview](https://www.netskope.com/netskope-one/threat-protection)
- [Netskope Threat Protection documentation](https://docs.netskope.com/en/threat-protection/)
- [Netskope Data Loss Prevention](https://www.netskope.com/products/data-loss-prevention)