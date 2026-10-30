---
layout: Conceptual
title: Troubleshoot the Global Secure Access mobile client with Health check utility - Global Secure Access | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-mobile-client-health-check-utility
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: HULKsmashGithub
ms.author: jayrusso
ms.service: global-secure-access
manager: dougeby
description: Learn if a device can communicate with the Global Secure Access service and tunnel traffic, by using the health check utility.
ms.topic: troubleshooting
ms.reviewer: gauthamca, matursca, jricketts
ms.date: 2026-03-20T00:00:00.0000000Z
locale: en-us
document_id: 9260ef36-4187-e2ea-3ac7-c0d11bd03088
document_version_independent_id: 9260ef36-4187-e2ea-3ac7-c0d11bd03088
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/global-secure-access/troubleshoot-global-secure-access-mobile-client-health-check-utility.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: global-secure-access/troubleshoot-global-secure-access-mobile-client-health-check-utility
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/global-secure-access/troubleshoot-global-secure-access-mobile-client-health-check-utility.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 23caf826-94e7-7e12-b8fa-e7dd06364b19
---

# Troubleshoot the Global Secure Access mobile client with Health check utility - Global Secure Access | Microsoft Learn

This article's troubleshooting guidance is for the [Global Secure Access](/en-us/entra/global-secure-access/overview-what-is-global-secure-access) mobile client, using the health check utility in [Microsoft Defender](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-defender-service-description).

The Global Secure Access mobile client health check utility helps you understand if a device can communicate with the Global Secure Access service and tunnel traffic. The health check has a single view for device compliance, local network configuration, and policy service readiness signals. When required conditions are met, the health check utility reports a healthy state and traffic forwarding functions as expected.

## Run the health check

Review the Global Secure Access client health check on a mobile client.

1. On the device, navigate to **Microsoft Defender**.
2. Select **Global Secure Access**.
3. Select **Troubleshooting**.
4. Select **Advanced Diagnostics**.
5. Select **Health check**.

In the healthy state in health check, green check marks appear under **Device Checks** and network-as-as-service **(Naas) Policy**.

![Screenshot of the health check utility.](media/troubleshoot-global-secure-access-mobile-client-health-check-utility/health-check.png)

When the **X** symbol appears, the state is unhealthy and troubleshooting is recommended. After you complete a fix for a failed result, refresh the health check utility to view updated results. To learn about specific remediation scenarios, use the information in the following sections.

Note

If attempts fail to fix the results, contact [Microsoft Support](/en-us/services-hub/unified/support/contact-support).

## Device compliant

Your organization might use [Microsoft Intune](/en-us/intune/intune-service/fundamentals/what-is-intune) to define device compliance policies, and [Microsoft Entra Conditional Access](/en-us/entra/identity/conditional-access/) policies to enforce the requirement to use Global Secure Access applications. Therefore, the device fails this test if it doesn't meet compliance criteria.

To remediate device compliant errors:

1. Go to **Settings**.
2. Select **General**.
3. Select **VPN & Device Management**.
4. Confirm the user is signed into the correct work account on the device.
5. Update the device operating system (OS) to the current version.
6. On the device, review failed compliance rules, for instance OS version, passcode, and jailbreak detection.

### Enrolled devices

In the [Microsoft Intune admin center](https://intune.microsoft.com/), confirm the following criteria:

1. Device enrollment: [Enroll the device in Intune](/en-us/intune/intune-service/fundamentals/deployment-guide-enrollment)
2. Device compliance: If not, open the **Company portal** app and [resolve compliance issues](/en-us/intune/intune-service/user-help/check-device-access-windows-cpapp).

    Note

    After changes are made, it can take up to 30 minutes for the status to update.
3. When health check tests indicate a healthy state, reattempt to connect to the resource.
4. After remediation, restart the Global Secure Access client: Toggle it **Off** and **On** in Microsoft Defender.
5. Restart the device.

    ![Screenshot of on and off options.](media/troubleshoot-global-secure-access-mobile-client-health-check-utility/on-off.png)

### Bring-your-own-device scenarios

Use the following checklist for bring-your-own-device (BYOD).

Ensure the Microsoft Authenticator, or Company Portal apps, are installed on the client device. Device enrollment isn't required.

In Microsoft Defender:

1. Confirm the user signed in to the corporate account.
2. Navigate to **Global Secure Access**.
3. Confirm that Global Secure Access is **Enabled**.
4. Navigate to **Global Secure Access**, then select **Services**.
5. Confirm required traffic profiles are connected.

    Note

    After remediation, restart the Global Secure Access client: Toggle it **Off** and **On** in Microsoft Defender.

You can learn to [monitor results of your Intune device-compliance policies](/en-us/intune/intune-service/protect/compliance-policy-monitor).

### Private DNS setting disabled

Private DNS isn't currently supported for Android.

1. Go to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Navigate to **Global Secure Access**.
3. Under **Applications**, select **Quick Access**.
4. In the **Private DNS** tab, ensure **Private DNS** is not selected.

### Manual proxy setting disabled

Manual proxy interferes with Global Secure Access traffic routing. For instance, The **Manual proxy setting disabled** label in the health check is red, or set to **No**. Or you might be unable to access resources. To clear this health check error, disable the manual proxy setting.

1. On the device, go to **Settings**, select **Wi-Fi**.
2. Next to the active network, select the **info** icon (**i**).
3. Scroll down to HTTP Proxy, and select **Configure Proxy**.
4. Select **Off**. Select **Automatic** if required by the environment for proxy autoconfiguration (PAC).

    ![Screenshot of Configure Proxy dialog.](media/troubleshoot-global-secure-access-mobile-client-health-check-utility/configure-proxy.png)

    Note

    Avoid static or manual proxy settings when using the Global Secure Access client. After making changes, disconnect the device from Wi-Fi and reconnect Wi-Fi. Restart the device.

On Apple Platform Deployment, you can learn more about [VPN Proxy device management settings for Apple devices](https://support.apple.com/guide/deployment/vpn-proxy-settings-depb78836926/web).

### NaaS policy: running policy service

If the Global Secure Access policy service isn't running or didn't initialize on the device, the health check fails. To troubleshoot this error:

1. On the client device, in Microsoft Defender, navigate to **Global Secure Access**.
2. Confirm the service is **Enabled**.
3. Confirm the user is signed in to the work or school account.

To ensure the VPN is disabled:

1. On the device, go to **Settings**.
2. Select **General**.
3. Select **VPN & Device Management**.
4. Confirm the VPN is set to **Not Connected**.
5. Navigate to Settings.
6. Select Battery.
7. Ensure **Lower Power Mode** is disabled.
8. To confirm no background app restrictions, go to **Settings**.
9. Select **General**.
10. Select **Background App Refresh**.
11. Confirm cellular data is turned on.

Note

After remediation, restart the Global Secure Access client: Toggle it **Off** and **On** in Microsoft Defender. Restart the device.

![Screenshot of on and off options.](media/troubleshoot-global-secure-access-mobile-client-health-check-utility/on-off.png)

## Diagnostic URLs in forwarding profile

The following test checks that the configuration contains a URL to probe service health, for channels activated in the forwarding profile.

### Break-glass mode disabled

Break-glass mode prevents the Global Secure Access client from tunneling network traffic to the Global Secure Access cloud service. In this mode, traffic profiles in the Global Secure Access portal are unchecked, and the Global Secure Access client isn't expected to tunnel any traffic.

Enable the client to acquire traffic and tunnel traffic to the Global Secure Access service.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as a [Global Secure Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference).
2. Browse to **Global Secure Access**
3. Select **Connect**.
4. Select **Traffic forwarding**.
5. Enable at least one traffic profile.
6. In about an hour, Global Secure Access receives the updated forwarding profile.

    ![Screenshot of profile options for traffic, private access, and internet access.](media/troubleshoot-global-secure-access-mobile-client-health-check-utility/profile-options.png)

    Note

    In addition to health check status indicators, a generic **Something went wrong** error can appear for device registration problems. To resolve, update the device to the latest OS version. Then, navigate to **Microsoft Defender**, then **Global Secure Access**. Toggle the Global Secure Access client **Off** then **On**.

    ![Screenshot of on and off options.](media/troubleshoot-global-secure-access-mobile-client-health-check-utility/on-off.png)