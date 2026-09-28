---
layout: Conceptual
title: Configuring macOS Platform SSO (PSSO) to meet NIST SP 800-63 and EO 14028 Requirements - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/macos-psso-deployment-eocustomers
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: How to deploy macOS Platform Single Sign On (PSSO) to meet NIST SP 800-63 and EO 14028 Requirements.
ms.topic: how-to
ms.date: 2025-05-01T00:00:00.0000000Z
ms.reviewer: jploegert
locale: en-us
document_id: ccfbf937-8bf9-916a-c391-5d8a48878ad4
document_version_independent_id: ccfbf937-8bf9-916a-c391-5d8a48878ad4
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/macos-psso-deployment-eocustomers.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/macos-psso-deployment-eocustomers
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/macos-psso-deployment-eocustomers.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://authoring-docs-microsoft.poolparty.biz/devrel/9d7be3ef-f27c-4c7f-9eba-67c3cd429995
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://authoring-docs-microsoft.poolparty.biz/devrel/feeb50f3-b677-44f9-b3a6-5f2f58182b0d
platformId: 989e5745-a595-e466-5b07-cebee2dafc3d
---

# Configuring macOS Platform SSO (PSSO) to meet NIST SP 800-63 and EO 14028 Requirements - Microsoft Entra ID | Microsoft Learn

This document provides a comprehensive guidance for deploying macOS Platform Single Sign-On (PSSO) by US government agencies to meet the National Institute of Standards and Technology (NIST) Special Publication (SP) 800-63 Revision 4 and Executive Order (EO) 14028 requirements. By following the instructions and best practices outlined in this document, organizations can ensure a seamless and secure SSO experience for their macOS users.

## Prerequisites

- Minimum version of macOS 13 Ventura (macOS 14 Sonoma or later recommended)
- Users must be able to perform a multifactor authentication during registration using one of the supported MFA methods in Entra ID.
    - [Microsoft Entra MFA](../authentication/concept-mfa-howitworks)
    - [Federated MFA](/en-us/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)
    - [External Auth Methods](../authentication/how-to-authentication-external-method-manage)
- [Microsoft Intune Company Portal app version 5.2408.0](/en-us/mem/intune/apps/apps-company-portal-macos) or later installed. This version is required before users are targeted for PSSO.
- (Highly recommended) Users are advised to [register a passkey on their mobile devices.](../authentication/how-to-register-passkey)

## Authentication Method Selection

US government agencies must use a phishing-resistant authentication method in the Platform SSO configuration deployed to their devices.

macOS 14 Sonoma and later offer two phishing-resistant methods in the Apple Platform SSO framework:

1. [Secure Enclave](/en-us/mem/intune/configuration/platform-sso-macos#secure-enclave) (Recommended).
2. [Smart card](/en-us/mem/intune/configuration/platform-sso-macos#smart-card).

For more information and a comparison of available authentication methods with Platform SSO, please see [Decide the authentication method](/en-us/mem/intune/configuration/platform-sso-macos#step-1---decide-the-authentication-method).

## Microsoft Intune Configuration

See [Configure Platform SSO for macOS devices in Microsoft Intune](/en-us/mem/intune/configuration/platform-sso-macos).

## Configuration for other MDMs

Please refer to your MDM provider’s documentation for information on support and provisioning Platform SSO for macOS.

## Enable SSO for Applications that don’t use Microsoft Authentication Library (MSAL)

See [Enable SSO for apps that don’t use MSAL](../../identity-platform/apple-sso-plugin).

## Configure Kerberos SSO Integration

See [Enable Kerberos SSO to on-premises Active Directory and Microsoft Entra ID Kerberos resources in Platform SSO](device-join-macos-platform-single-sign-on-kerberos-configuration).

## Account Management

### Create and Provision Accounts

To use Platform SSO, the devices must be MDM-enrolled. If using Intune, use one of the following methods:

- For organization-owned devices, you can:

    - Create an [Automated device enrollment](/en-us/mem/intune/enrollment/device-enrollment-program-enroll-macos) policy using Apple Business Manager.
    - Create a [Direct enrollment](/en-us/mem/intune/enrollment/device-enrollment-direct-enroll-macos) policy using Apple Configurator.
- For personally owned devices, create a [Device enrollment](/en-us/mem/intune/fundamentals/deployment-guide-enrollment-macos#byod-device-enrollment) policy. With this enrollment method, end users open the Company Portal app and sign in with their Microsoft Entra ID user account. When the successfully signed in, the enrollment policy applies.

For new devices, we recommend you pre-create and configure all the necessary policies, including the enrollment policy. Then, when the devices enroll in Intune, the policies automatically apply.

For existing devices already enrolled in Intune, assign the Platform SSO policy to your users or user groups. The next time the devices sync or check-in with Intune, they receive the Platform SSO policy settings you create.

### Create Device Compliance Policies

Device Compliance Policies in Microsoft Intune allow administrators to ensure that enrolled devices meet organizational security standards and are configured properly. These policies help safeguard corporate data by enforcing requirements such as encryption, operating system versions, and security measures like password strength. For more information on configuring Device Compliance Policies, please see [Device Compliance Settings for macOS Settings in Intune](/en-us/mem/intune/protect/compliance-policy-create-mac-os).

### Deprovision or Offboard Accounts

#### Deleting users from a tenant

See [How to create, invite, and delete users](../../fundamentals/how-to-create-delete-users).

#### Revoke a user's access

See [Revoke user access in Microsoft Entra ID](../users/users-revoke-access).

#### Remotely lock devices with Intune

See [Remotely lock devices with Intune](/en-us/mem/intune/remote-actions/device-remote-lock).

### MDM Unenrollment

#### Step 1 - Remove PSSO targeted users from the Configuration Profile assignment

1. In the Microsoft Intune admin center click on **Home**.
2. Go to **Devices** and then **Configuration profiles**.
3. Select the configuration profile you want to edit from the list.
4. Next to **Assignments**, select **Edit**.
5. To remove the assignment select **Remove**.
6. Select **Review + Save** to complete the changes.

#### Step 2 - Perform a Bulk Device Action to synchronize the policy removal

1. In Microsoft Endpoint Management center select **Devices**.
2. Choose **All devices** and select **Bulk device actions**.
3. On the **Bulk Device Action** page, select *macOS* as the OS, and *Sync* as the device action.
4. Select **Next** and choose the maximum number of devices that the action supports and select **Next**.
5. On the **Review + Create** page, select **Create** and run the action.

Tip

If you would like to synchronize a specific device, please refer to [Sync devices to get the latest policies and actions with Intune](/en-us/mem/intune/remote-actions/device-sync#sync-a-device).

#### Detect and Remove Stale Devices in Microsoft Entra ID and Intune

See [How To: Manage stale devices in Microsoft Entra ID](manage-stale-devices) and [Delete devices from the Intune Admin Center](/en-us/mem/intune/remote-actions/devices-wipe#delete-devices-from-the-intune-admin-center).

## Integrate Applications with the SSO Broker

[MSAL for Apple devices](https://github.com/AzureAD/microsoft-authentication-library-for-objc) versions 1.1.0 and later support the Microsoft Enterprise SSO plug-in for Apple devices natively for work and school accounts.

You don’t need any special configuration if you followed [Quickstart: Sign in users and call Microsoft Graph from an iOS or macOS app](../../identity-platform/quickstart-mobile-app-ios-sign-in) and used the [default redirect URI format](/en-us/mem/intune/remote-actions/devices-wipe#delete-devices-from-the-intune-admin-center).

On devices that have the SSO plug-in, MSAL automatically invokes it for all interactive and silent token requests. It also invokes it for account enumeration and account removal operations. Because MSAL implements a native SSO plug-in protocol that relies on customer operations, this setup provides the smoothest native experience to the end user.

## Best Practices

### Smart Card Certificate Pinning

When using smart card-based authentication, it is highly recommended that you specify which Certificate Issuing Authorities are used for the trust evaluation of smart card certificates. This trust, which works in conjunction with Certificate Trust settings, is known as certificate pinning. For more information, see [Advanced Smart card Options on Mac](https://support.apple.com/guide/deployment/advanced-smart-card-options-dep7b2ede1e3/web#:%7E:text=Certificate%20pinning,%3C/plist%3E).

#### Example configuration

```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" http://www.apple.com/DTDs/PropertyList-1.0.dtd>
    <plist version="1.0">
    <dict>
        <key>AttributeMapping</key>
        <dict>
            <key>dsAttributeString</key
            <string>dsAttrTypeStandard:AltSecurityIdentities</string>
            <key>fields</key>
            <array>
                <string>NT Principal Name</string>
            </array>
            <key>formatString</key>
            <string>PlatformSSO:$1</string>
        </dict>
        <key>TrustedAuthorities</key>
        <array>
    <string>SHA256_HASH_OF_CERTDOMAIN_1,SHA256_HASH_OF_CERTDOMAIN_2</string>
        </array>
    </dict>
    </plist>
```

## Troubleshooting

If you experience issues when deploying macOS Platform SSO, refer to our documentation on [macOS Platform Single Sign-on known issues and troubleshooting](troubleshoot-macos-platform-single-sign-on-extension).