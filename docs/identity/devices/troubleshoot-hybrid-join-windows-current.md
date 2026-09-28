---
layout: Conceptual
title: Troubleshoot Microsoft Entra hybrid joined devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/troubleshoot-hybrid-join-windows-current
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: This article helps you troubleshoot Microsoft Entra hybrid joined Windows 10 and Windows Server 2016 devices.
ms.topic: troubleshooting
ms.date: 2026-09-01T00:00:00.0000000Z
ms.reviewer: mozmaili
ms.custom: has-adal-ref, sfi-ropc-nochange, sfi-image-nochange
locale: en-us
document_id: b9f81d74-8dcb-e644-9647-0d1d0817f975
document_version_independent_id: e249cc9d-2120-8868-dbca-bc3b85f38b4b
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/troubleshoot-hybrid-join-windows-current.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/troubleshoot-hybrid-join-windows-current
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/troubleshoot-hybrid-join-windows-current.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: f7de82e9-38a0-2a07-3ea0-27fcaf6e3e5b
---

# Troubleshoot Microsoft Entra hybrid joined devices - Microsoft Entra ID | Microsoft Learn

This article provides troubleshooting guidance to help you resolve potential issues with devices that are running Windows 10 or newer and Windows Server 2016 or newer.

Microsoft Entra hybrid join supports the Windows 10 November 2015 update and later.

This article assumes that you have [Microsoft Entra hybrid joined devices](hybrid-join-plan) to support the following scenarios:

- Device-based Conditional Access
- [Enterprise state roaming](enterprise-state-roaming-enable)
- [Windows Hello for Business](/en-us/windows/security/identity-protection/hello-for-business/hello-identity-verification)

Note

To troubleshoot the common device registration issues, use [Device Registration Troubleshooter Tool](/en-us/samples/azure-samples/dsregtool/dsregtool/).

## Troubleshoot join failures

### Step 1: Retrieve the join status

1. Open a Command Prompt window as an administrator.
2. Type `dsregcmd /status`.

```
+----------------------------------------------------------------------+
| Device State                                                         |
+----------------------------------------------------------------------+

    AzureAdJoined: YES
 EnterpriseJoined: NO
         DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7
       Thumbprint: AA11BB22CC33DD44EE55FF66AA77BB88CC99DD00
   KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9
      KeyProvider: Microsoft Platform Crypto Provider
     TpmProtected: YES
     KeySignTest: : MUST Run elevated to test.
              Idp: login.windows.net
         TenantId: aaaabbbb-0000-cccc-1111-dddd2222eeee
       TenantName: Contoso
      AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize
   AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token
           MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc
        MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx
  dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance
      SettingsUrl: eyJVc{lots of characters}JdfQ==
   JoinSrvVersion: 1.0
       JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/
        JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net
    KeySrvVersion: 1.0
        KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/
         KeySrvId: urn:ms-drs:enterpriseregistration.windows.net
     DomainJoined: YES
       DomainName: CONTOSO

+----------------------------------------------------------------------+
| User State                                                           |
+----------------------------------------------------------------------+

             NgcSet: YES
           NgcKeyId: {aaaaaaaa-0b0b-1c1c-2d2d-333333333333}
    WorkplaceJoined: NO
      WamDefaultSet: YES
WamDefaultAuthority: organizations
       WamDefaultId: https://login.microsoft.com
     WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)
         AzureAdPrt: YES
```

### Step 2: Evaluate the join status

Review the fields in the following table, and make sure that they have the expected values:

| Field | Expected value | Description |
| --- | --- | --- |
| DomainJoined | YES | This field indicates whether the device is joined to an on-premises Active Directory. If the value is *NO*, the device can't do Microsoft Entra hybrid join. |
| WorkplaceJoined | NO | This field indicates whether the device is registered with Microsoft Entra ID as a personal device (marked as *Workplace Joined*). This value should be *NO* for a domain-joined computer that's also Microsoft Entra hybrid joined. If the value is *YES*, a work or school account was added before the completion of the Microsoft Entra hybrid join. In this case, the account is ignored when you're using Windows 10 version 1607 or later. |
| AzureAdJoined | YES | This field indicates whether the device is joined. The value is *YES* if the device is either a Microsoft Entra joined device or a Microsoft Entra hybrid joined device. If the value is *NO*, the join to Microsoft Entra ID hasn't finished yet. |

Continue to the next steps for further troubleshooting.

### Step 3: Find the phase in which the join failed, and the error code

**For Windows 10 version 1803 or later**

Look for the "Previous Registration" subsection in the "Diagnostic Data" section of the join status output. This section is displayed only if the device is domain-joined and unable to Microsoft Entra hybrid join.

The "Error Phase" field denotes the phase of the join failure, and "Client ErrorCode" denotes the error code of the join operation.

```
+----------------------------------------------------------------------+
     Previous Registration : 2019-01-31 09:16:43.000 UTC
         Registration Type : sync
               Error Phase : join
          Client ErrorCode : 0x801c03f2
          Server ErrorCode : DirectoryError
            Server Message : The device object by the given id (e92325d0-xxxx-xxxx-xxxx-94ae875d5245) isn't found.
              Https Status : 400
                Request Id : 6bff0bd9-820b-484b-ab20-2a4f7b76c58e
+----------------------------------------------------------------------+
```

**For earlier Windows 10 versions**

Use Event Viewer logs to locate the phase and error code for the join failures.

1. In Event Viewer, open the **User Device Registration** event logs. They're stored under **Applications and Services Log** &gt; **Microsoft** &gt; **Windows** &gt; **User Device Registration**.
2. Look for events with the following event IDs: 304, 305, and 307.

![Screenshot of Event Viewer, with event ID 304 selected, its information displayed, and its error code and phase highlighted.](media/troubleshoot-hybrid-join-windows-current/1.png)

![Screenshot of Event Viewer, with event ID 305 selected, its information displayed, and its error code highlighted.](media/troubleshoot-hybrid-join-windows-current/2.png)

### Step 4: Check for possible causes and resolutions

#### Precheck phase

Possible reasons for failure:

- The device has no line of sight to the domain controller.
    - The device must be on the organization's internal network or on a virtual private network with a network line of sight to an on-premises Active Directory domain controller.

#### Discover phase

Possible reasons for failure:

- The service connection point object is misconfigured or can't be read from the domain controller.
    - A valid service connection point object is required in the AD forest, to which the device belongs, that points to a verified domain name in Microsoft Entra ID.
    - For more information, see the "Configure a service connection point" section of [Tutorial: Configure Microsoft Entra hybrid join for federated domains](how-to-hybrid-join).
- Failure to connect to and fetch the discovery metadata from the discovery endpoint.
    - The device should be able to access `https://enterpriseregistration.windows.net`, in the system context, to discover the registration and authorization endpoints.
    - If the on-premises environment requires an outbound proxy, the IT admin must ensure that the computer account of the device can discover and silently authenticate to the outbound proxy.
- Failure to connect to the user realm endpoint and do realm discovery (Windows 10 version 1809 and later only).
    - The device should be able to access `https://login.microsoftonline.com`, in the system context, to do realm discovery for the verified domain and determine the domain type (managed or federated).
    - If the on-premises environment requires an outbound proxy, the IT admin must ensure that the system context on the device can discover and silently authenticate to the outbound proxy.

**Common error codes:**

| Error code | Reason | Resolution |
| --- | --- | --- |
| **DSREG\_AUTOJOIN\_ADCONFIG\_READ\_FAILED** (0x801c001d/-2145648611) | Unable to read the service connection point (SCP) object and get the Microsoft Entra tenant information. | Refer to the [Configure a service connection point](hybrid-join-manual#configure-a-service-connection-point) section. |
| **DSREG\_AUTOJOIN\_DISC\_FAILED** (0x801c0021/-2145648607) | Generic discovery failure. Failed to get the discovery metadata from the data replication service (DRS). | To investigate further, find the suberror in the next sections. |
| **DSREG\_AUTOJOIN\_DISC\_WAIT\_TIMEOUT** (0x801c001f/-2145648609) | Operation timed out while performing discovery. | Ensure that `https://enterpriseregistration.windows.net` is accessible in the system context. For more information, see the [Network connectivity requirements](how-to-hybrid-join#prerequisites) section. |
| **DSREG\_AUTOJOIN\_USERREALM\_DISCOVERY\_FAILED** (0x801c003d/-2145648579) | Generic realm discovery failure. Failed to determine domain type (managed/federated) from STS. | To investigate further, find the suberror in the next sections. |

**Common sub-error codes:**

To find the suberror code for the discovery error code, use one of the following methods.

##### Windows 10 version 1803 or later

Look for "DRS Discovery Test" in the "Diagnostic Data" section of the join status output. This section is displayed only if the device is domain-joined and unable to Microsoft Entra hybrid join.

```
+----------------------------------------------------------------------+
| Diagnostic Data                                                      |
+----------------------------------------------------------------------+

     Diagnostics Reference : www.microsoft.com/aadjerrors
              User Context : UN-ELEVATED User
               Client Time : 2019-06-05 08:25:29.000 UTC
      AD Connectivity Test : PASS
     AD Configuration Test : PASS
        DRS Discovery Test : FAIL [0x801c0021/0x80072ee2]
     DRS Connectivity Test : SKIPPED
    Token acquisition Test : SKIPPED
     Fallback to Sync-Join : ENABLED

+----------------------------------------------------------------------+
```

##### Earlier Windows 10 versions

Use Event Viewer logs to look for the phase and error code for the join failures.

1. In Event Viewer, open the **User Device Registration** event logs. They're stored under **Applications and Services Log** &gt; **Microsoft** &gt; **Windows** &gt; **User Device Registration**.
2. Look for event ID 201.

![Screenshot of Event Viewer, with event ID 201 selected, its information displayed, and its error code highlighted.](media/troubleshoot-hybrid-join-windows-current/5.png)

**Network errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **WININET\_E\_CANNOT\_CONNECT** (0x80072efd/-2147012867) | Connection with the server couldn't be established. | Ensure network connectivity to the required Microsoft resources. For more information, see [Network connectivity requirements](how-to-hybrid-join#prerequisites). |
| **WININET\_E\_TIMEOUT** (0x80072ee2/-2147012894) | General network timeout. | Ensure network connectivity to the required Microsoft resources. For more information, see [Network connectivity requirements](how-to-hybrid-join#prerequisites). |
| **WININET\_E\_DECODING\_FAILED** (0x80072f8f/-2147012721) | Network stack was unable to decode the response from the server. | Ensure that the network proxy isn't interfering and modifying the server response. |

**HTTP errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **DSREG\_DISCOVERY\_TENANT\_NOT\_FOUND** (0x801c003a/-2145648582) | The service connection point object is configured with the wrong tenant ID, or no active subscriptions were found in the tenant. | Ensure that the service connection point object is configured with the correct Microsoft Entra tenant ID and active subscriptions or that the service is present in the tenant. |
| **DSREG\_SERVER\_BUSY** (0x801c0025/-2145648603) | HTTP 503 from DRS server. | The server is currently unavailable. Future join attempts will likely succeed after the server is back online. |

**Other errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **E\_INVALIDDATA** (0x8007000d/-2147024883) | The server response JSON couldn't be parsed, likely because the proxy is returning an HTTP 200 with an HTML authorization page. | If the on-premises environment requires an outbound proxy, the IT admin must ensure that the system context on the device can discover and silently authenticate to the outbound proxy. |

#### Authentication phase

This content applies only to federated domain accounts.

Reasons for failure:

- Unable to get an access token silently for the DRS resource.
    - Windows 10 and Windows 11 devices acquire the authentication token from the Federation Service by using integrated Windows authentication to an active WS-Trust endpoint. For more information, see [Federation Service configuration](hybrid-join-manual#set-up-issuance-of-claims).

**Common error codes**:

Use Event Viewer logs to locate the error code, suberror code, server error code, and server error message.

1. In Event Viewer, open the **User Device Registration** event logs. They're stored under **Applications and Services Log** &gt; **Microsoft** &gt; **Windows** &gt; **User Device Registration**.
2. Look for event ID 305.

![Screenshot of Event Viewer, with event ID 305 selected, its information displayed, and the ADAL error codes and status highlighted.](media/troubleshoot-hybrid-join-windows-current/3.png)

**Configuration errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **ERROR\_ADAL\_PROTOCOL\_NOT\_SUPPORTED** (0xcaa90017/-894894057) | The Azure AD Authentication Library (ADAL) authentication protocol isn't WS-Trust. | The on-premises identity provider must support WS-Trust. |
| **ERROR\_ADAL\_FAILED\_TO\_PARSE\_XML** (0xcaa9002c/-894894036) | The on-premises Federation Service didn't return an XML response. | Ensure that the Metadata Exchange (MEX) endpoint is returning a valid XML. Ensure that the proxy isn't interfering and returning nonxml responses. |
| **ERROR\_ADAL\_COULDNOT\_DISCOVER\_USERNAME\_PASSWORD\_ENDPOINT** (0xcaa90023/-894894045) | Couldn't discover an endpoint for username/password authentication. | Check the on-premises identity provider settings. Ensure that the WS-Trust endpoints are enabled and that the MEX response contains these correct endpoints. |

**Network errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **ERROR\_ADAL\_INTERNET\_TIMEOUT** (0xcaa82ee2/-894947614) | General network timeout. | Ensure that `https://login.microsoftonline.com` is accessible in the system context. Ensure that the on-premises identity provider is accessible in the system context. For more information, see [Network connectivity requirements](how-to-hybrid-join#prerequisites). |
| **ERROR\_ADAL\_INTERNET\_CONNECTION\_ABORTED** (0xcaa82efe/-894947586) | Connection with the authorization endpoint was aborted. | Retry the join after a while, or try joining from another stable network location. |
| **ERROR\_ADAL\_INTERNET\_SECURE\_FAILURE** (0xcaa82f8f/-894947441) | The Transport Layer Security (TLS) certificate (previously known as the Secure Sockets Layer [SSL] certificate) sent by the server couldn't be validated. | Check the client time skew. Retry the join after a while, or try joining from another stable network location. |
| **ERROR\_ADAL\_INTERNET\_CANNOT\_CONNECT** (0xcaa82efd/-894947587) | The attempt to connect to `https://login.microsoftonline.com` failed. | Check the network connection to `https://login.microsoftonline.com`. |

**Other errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **ERROR\_ADAL\_SERVER\_ERROR\_INVALID\_GRANT** (0xcaa20003/-895352829) | The SAML token from the on-premises identity provider wasn't accepted by Microsoft Entra ID. | Check the Federation Server settings. Look for the server error code in the authentication logs. |
| **ERROR\_ADAL\_WSTRUST\_REQUEST\_SECURITYTOKEN\_FAILED** (0xcaa90014/-894894060) | The Server WS-Trust response reported a fault exception, and it failed to get assertion. | Check the Federation Server settings. Look for the server error code in the authentication logs. |
| **ERROR\_ADAL\_WSTRUST\_TOKEN\_REQUEST\_FAIL** (0xcaa90006/-894894074) | Received an error when trying to get access token from the token endpoint. | Look for the underlying error in the ADAL log. |
| **ERROR\_ADAL\_OPERATION\_PENDING** (0xcaa1002d/-895418323) | General ADAL failure. | Look for the suberror code or server error code from the authentication logs. |

#### Join phase

Reasons for failure:

Look for the registration type and error code from the following tables, depending on the Windows 10 version you're using.

#### Windows 10 version 1803 or later

Look for the "Previous Registration" subsection in the "Diagnostic Data" section of the join status output. This section is displayed only if the device is domain-joined and is unable to Microsoft Entra hybrid join.

The "Registration Type" field denotes the type of join.

```
+----------------------------------------------------------------------+
     Previous Registration : 2019-01-31 09:16:43.000 UTC
         Registration Type : sync
               Error Phase : join
          Client ErrorCode : 0x801c03f2
          Server ErrorCode : DirectoryError
            Server Message : The device object by the given id (aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb) is not found.
              Https Status : 400
                Request Id : 6bff0bd9-820b-484b-ab20-2a4f7b76c58e
+----------------------------------------------------------------------+
```

#### Earlier Windows 10 versions

Use Event Viewer logs to locate the phase and error code for the join failures.

1. In Event Viewer, open the **User Device Registration** event logs. They're stored under **Applications and Services Log** &gt; **Microsoft** &gt; **Windows** &gt; **User Device Registration**.
2. Look for event ID 204.

![Screenshot of Event Viewer, with event ID 204 selected and its error code, H T T P status, and message highlighted.](media/troubleshoot-hybrid-join-windows-current/4.png)

**HTTP errors returned from DRS server**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **DSREG\_E\_DIRECTORY\_FAILURE** (0x801c03f2/-2145647630) | Received an error response from DRS with ErrorCode: "DirectoryError". | Refer to the server error code for possible reasons and resolutions. |
| **DSREG\_E\_DEVICE\_AUTHENTICATION\_ERROR** (0x801c0002/-2145648638) | Received an error response from DRS with ErrorCode: "AuthenticationError" and ErrorSubCode is *not* "DeviceNotFound". | Refer to the server error code for possible reasons and resolutions. |
| **DSREG\_E\_DEVICE\_INTERNALSERVICE\_ERROR** (0x801c0006/-2145648634) | Received an error response from DRS with ErrorCode: "DirectoryError". | Refer to the server error code for possible reasons and resolutions. |

**TPM errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **NTE\_BAD\_KEYSET** (0x80090016/-2146893802) | The Trusted Platform Module (TPM) operation failed or was invalid. | This error indicates that the keyset doesn't exist. This error happens when the TPM is cleared on the systems, or when there's a bad sysprep image.  Avoid clearing the TPM in BIOS or Windows settings. If the TPM is cleared, users might need to recover by removing and readding accounts to fix the problem, especially when they have multiple WAM accounts. Ensure that the machine from which the sysprep image was created isn't Microsoft Entra joined, Microsoft Entra hybrid joined, or Microsoft Entra registered. |
| **TPM\_E\_PCP\_INTERNAL\_ERROR** (0x80290407/-2144795641) | Generic TPM error. | Disable TPM on devices with this error. Windows 10 versions 1809 and later automatically detect TPM failures and complete Microsoft Entra hybrid join without using the TPM. |
| **TPM\_E\_NOTFIPS** (0x80280036/-2144862154) | TPM in FIPS mode isn't currently supported. | Disable TPM on devices with this error. Windows 10 version 1809 automatically detects TPM failures and completes the Microsoft Entra hybrid join without using the TPM. |
| **NTE\_AUTHENTICATION\_IGNORED** (0x80090031/-2146893775) | TPM is locked out. | Transient error. Wait for the cool-down period. The join attempt should succeed after a while. For more information, see [TPM fundamentals](/en-us/windows/security/hardware-security/tpm/tpm-fundamentals#anti-hammering). |

**Network errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **WININET\_E\_TIMEOUT** (0x80072ee2/-2147012894) | General network time out trying to register the device at DRS. | Check network connectivity to `https://enterpriseregistration.windows.net`. |
| **WININET\_E\_NAME\_NOT\_RESOLVED** (0x80072ee7/-2147012889) | The server name or address couldn't be resolved. | Check network connectivity to `https://enterpriseregistration.windows.net`. |
| **WININET\_E\_CONNECTION\_ABORTED** (0x80072efe/-2147012866) | The connection with the server was terminated abnormally. | Retry the join after a while, or try joining from another stable network location. |

**Other errors**:

| Error code | Reason | Resolution |
| --- | --- | --- |
| **DSREG\_AUTOJOIN\_ADCONFIG\_READ\_FAILED** (0x801c001d/-2145648611) | Event ID 220 is present in User Device Registration event logs. Windows can't access the computer object in Active Directory. A Windows error code might be included in the event. Error codes ERROR\_NO\_SUCH\_LOGON\_SESSION (1312) and ERROR\_NO\_SUCH\_USER (1317) are related to replication issues in on-premises Active Directory. | Troubleshoot replication issues in Active Directory. These replication issues might be transient, and they might go away after a while. |

**Federated join server errors**:

| Server error code | Server error message | Possible reasons | Resolution |
| --- | --- | --- | --- |
| DirectoryError | Your request is throttled temporarily. Please try after 300 seconds. | This error is expected, possibly because multiple registration requests were made in quick succession. | Retry the join after the cool-down period |

**Sync-join server errors**:

| Server error code | Server error message | Possible reasons | Resolution |
| --- | --- | --- | --- |
| DirectoryError | AADSTS90002: Tenant `UUID` not found. This error might happen if there are no active subscriptions for the tenant. Check with your subscription administrator. | The tenant ID in the service connection point object is incorrect. | Ensure that the service connection point object is configured with the correct Microsoft Entra tenant ID and active subscriptions or that the service is present in the tenant. |
| DirectoryError | The device object by the given ID isn't found. | This error is expected for sync-join. The device object hasn't synced from AD to Microsoft Entra ID | Wait for the Microsoft Entra Connect Sync to finish, and the next join attempt after sync completion will resolve the issue. |
| AuthenticationError | The verification of the target computer's SID | The certificate on the Microsoft Entra device doesn't match the certificate used to sign in to the blob during the sync-join. This error ordinarily means that sync hasn't finished yet. | Wait for the Microsoft Entra Connect Sync to finish, and the next join attempt after the sync completion will resolve the issue. |

### Step 5: Collect logs and contact Microsoft Support

1. [Download the *Auth.zip* file](https://aka.ms/authscripts).
2. Extract the files to a folder, such as *c:\temp*, and then go to the folder.
3. From an elevated Azure PowerShell session, run `.\start-auth.ps1 -vAuth -accepteula`.
4. Select **Switch Account** to toggle to another session with the problem user.
5. Reproduce the issue.
6. Select **Switch Account** to toggle back to the admin session that's running the tracing.
7. From the elevated PowerShell session, run `.\stop-auth.ps1`.
8. Zip (compress) and send the folder *Authlogs* from the folder where the scripts were executed.

## Troubleshoot post-join authentication issues

### Step 1: Retrieve the PRT status by using `dsregcmd /status`

1. Open a Command Prompt window.

    Note

    To get the Primary Refresh Token (PRT) status, open the Command Prompt window in the context of the logged-in user.
2. Run `dsregcmd /status`.

    The "SSO state" section provides the current PRT status.

    If the AzureAdPrt field is set to *NO*, there was an error acquiring the PRT status from Microsoft Entra ID.
3. If the AzureAdPrtUpdateTime is more than four hours, there's likely an issue with refreshing the PRT. Lock and unlock the device to force the PRT refresh, and then check to see whether the time updates.

```
+----------------------------------------------------------------------+
| SSO State                                                            |
+----------------------------------------------------------------------+

                AzureAdPrt : YES
      AzureAdPrtUpdateTime : 2020-07-12 22:57:53.000 UTC
      AzureAdPrtExpiryTime : 2019-07-26 22:58:35.000 UTC
       AzureAdPrtAuthority : https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee
             EnterprisePrt : YES
   EnterprisePrtUpdateTime : 2020-07-12 22:57:54.000 UTC
   EnterprisePrtExpiryTime : 2020-07-26 22:57:54.000 UTC
    EnterprisePrtAuthority : https://corp.hybridadfs.contoso.com:443/adfs

+----------------------------------------------------------------------+
```

### Step 2: Find the error code

**From the `dsregcmd` output**

Note

The output is available from the Windows 10 May 2021 update (version 21H1).

The "Attempt Status" field under the "AzureAdPrt" field provides the status of the previous PRT attempt, along with other required debug information. For earlier Windows versions, extract the information from the [Microsoft Entra analytics and operational logs](/en-us/troubleshoot/windows-server/networking/diagnostic-logging-troubleshoot-workplace-join-issues#enable-workplace-join-debug-logging-by-using-event-viewer).

```
+----------------------------------------------------------------------+
| SSO State                                                            |
+----------------------------------------------------------------------+

                AzureAdPrt : NO
       AzureAdPrtAuthority : https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee
     AcquirePrtDiagnostics : PRESENT
      Previous Prt Attempt : 2020-07-18 20:10:33.789 UTC
            Attempt Status : 0xc000006d
             User Identity : john@contoso.com
           Credential Type : Password
            Correlation ID : aaaa0000-bb11-2222-33cc-444444dddddd
              Endpoint URI : https://login.microsoftonline.com/aaaabbbb-0000-cccc-1111-dddd2222eeee/oauth2/token/
               HTTP Method : POST
                HTTP Error : 0x0
               HTTP status : 400
         Server Error Code : invalid_grant
  Server Error Description : AADSTS50126: Error validating credentials due to invalid username or password.
```

**From the Microsoft Entra analytics and operational logs**

Use Event Viewer to look for the log entries logged by the Microsoft Entra CloudAP plug-in during PRT acquisition.

1. In Event Viewer, open the Microsoft Entra Operational event logs. They're stored under **Applications and Services Log** &gt; **Microsoft** &gt; **Windows** &gt; **AAD**.

Note

The CloudAP plug-in logs error events in the operational logs, and it logs the info events in the analytics logs. The analytics and operational log events are both required to troubleshoot issues.

1. Event 1006 in the analytics logs denotes the start of the PRT acquisition flow, and event 1007 in the analytics logs denotes the end of the PRT acquisition flow. All events in the Microsoft Entra logs (analytics and operational) that are logged between events 1006 and 1007 were logged as part of the PRT acquisition flow.
2. Event 1007 logs the final error code.

![Screenshot of Event Viewer, with event IDs 1006 and 1007 selected and the final error code highlighted.](media/troubleshoot-hybrid-join-windows-current/event-viewer-prt-acquire.png)

### Step 3: Troubleshoot further, based on the found error code

| Error code | Reason | Resolution |
| --- | --- | --- |
| **STATUS\_LOGON\_FAILURE** (-1073741715/ 0xc000006d)**STATUS\_WRONG\_PASSWORD** (-1073741718/ 0xc000006a) | - The device is unable to connect to the Microsoft Entra authentication service.<br>- Received an error response (HTTP 400) from the Microsoft Entra authentication service or WS-Trust endpoint.**Note**: WS-Trust is required for federated authentication. | - If the on-premises environment requires an outbound proxy, the IT admin must ensure that the computer account of the device can discover and silently authenticate to the outbound proxy.<br>- Events 1081 and 1088 (Microsoft Entra operational logs) would contain the server error code for errors originating from the Microsoft Entra authentication service and error description for errors originating from the WS-Trust endpoint. Common server error codes and their resolutions are listed in the next section. The first instance of event 1022 (Microsoft Entra analytics logs), preceding events 1081 or 1088, contain the URL that's being accessed. |
| **STATUS\_REQUEST\_NOT\_ACCEPTED** (-1073741616/ 0xc00000d0) | Received an error response (HTTP 400) from the Microsoft Entra authentication service or WS-Trust endpoint.**Note**: WS-Trust is required for federated authentication. | Events 1081 and 1088 (Microsoft Entra operational logs) would contain the server error code and error description for errors originating from Microsoft Entra authentication service and WS-Trust endpoint, respectively. Common server error codes and their resolutions are listed in the next section. The first instance of event 1022 (Microsoft Entra analytics logs), preceding events 1081 or 1088, contain the URL that's being accessed. |
| **STATUS\_NETWORK\_UNREACHABLE** (-1073741252/ 0xc000023c)**STATUS\_BAD\_NETWORK\_PATH** (-1073741634/ 0xc00000be)**STATUS\_UNEXPECTED\_NETWORK\_ERROR** (-1073741628/ 0xc00000c4) | - Received an error response (HTTP &gt; 400) from the Microsoft Entra authentication service or WS-Trust endpoint.**Note**: WS-Trust is required for federated authentication.<br>- Network connectivity issue to a required endpoint. | - For server errors, events 1081 and 1088 (Microsoft Entra operational logs) would contain the error code from the Microsoft Entra authentication service and the error description from the WS-Trust endpoint. Common server error codes and their resolutions are listed in the next section.<br>- For connectivity issues, event 1022 (Microsoft Entra analytics logs) contains the URL that's being accessed, and event 1084 (Microsoft Entra operational logs) contains the suberror code from the network stack. |
| **STATUS\_NO\_SUCH\_LOGON\_SESSION** (-1073741729/ 0xc000005f) | User realm discovery failed because the Microsoft Entra authentication service was unable to find the user's domain. | - The domain of the user's UPN must be added as a custom domain in Microsoft Entra ID. Event 1144 (Microsoft Entra analytics logs) will contain the UPN provided.<br>- If the on-premises domain name is nonroutable (jdoe@contoso.local), configure an Alternate Login ID (AltID). References: [Prerequisites](hybrid-join-plan); [Configure Alternate Login ID](/en-us/windows-server/identity/ad-fs/operations/configuring-alternate-login-id). |
| **AAD\_CLOUDAP\_E\_OAUTH\_USERNAME\_IS\_MALFORMED** (-1073445812/ 0xc004844c) | The user's UPN isn't in the expected format.**Notes**:- For Microsoft Entra joined devices, the UPN is the text that's entered by the user in the LoginUI.<br>- For Microsoft Entra hybrid joined devices, the UPN is returned from the domain controller during the login process. | - User's UPN should be in the internet-style login name, based on the internet standard RFC 822. Event 1144 (Microsoft Entra analytics logs) contains the UPN provided.<br>- For hybrid-joined devices, ensure that the domain controller is configured to return the UPN in the correct format. In the domain controller, `whoami /upn` should display the configured UPN.<br>- If the on-premises domain name is nonroutable (jdoe@contoso.local), configure Alternate Login ID (AltID). References: [Prerequisites](hybrid-join-plan); [Configure Alternate Login ID](/en-us/windows-server/identity/ad-fs/operations/configuring-alternate-login-id). |
| **AAD\_CLOUDAP\_E\_OAUTH\_USER\_SID\_IS\_EMPTY** (-1073445822/ 0xc0048442) | The user SID is missing in the ID token that's returned by the Microsoft Entra authentication service. | Ensure that the network proxy isn't interfering with and modifying the server response. |
| **AAD\_CLOUDAP\_E\_WSTRUST\_SAML\_TOKENS\_ARE\_EMPTY** (--1073445695/ 0xc00484c1) | Received an error from the WS-Trust endpoint.**Note**: WS-Trust is required for federated authentication. | - Ensure that the network proxy isn't interfering with and modifying the WS-Trust response.<br>- Event 1088 (Microsoft Entra operational logs) would contain the server error code and error description from the WS-Trust endpoint. Common server error codes and their resolutions are listed in the next section. |
| **AAD\_CLOUDAP\_E\_HTTP\_PASSWORD\_URI\_IS\_EMPTY** (-1073445749/ 0xc004848b) | The MEX endpoint is incorrectly configured. The MEX response doesn't contain any password URLs. | - Ensure that the network proxy isn't interfering with and modifying the server response.<br>- Fix the MEX configuration to return valid URLs in response. |
| **AAD\_CLOUDAP\_E\_HTTP\_CERTIFICATE\_URI\_IS\_EMPTY** (-1073445748/ 0xc004848C) | The MEX endpoint is incorrectly configured. The MEX response doesn't contain any certificate endpoint URLs. | - Ensure that the network proxy isn't interfering with and modifying the server response.<br>- Fix the MEX configuration in the identity provider to return valid certificate URLs in response. |
| **WC\_E\_DTDPROHIBITED** (-1072894385/ 0xc00cee4f) | The XML response, from the WS-Trust endpoint, included a Document Type Definition (DTD). A DTD isn't expected in XML responses, and parsing the response fails if a DTD is included.**Note**: WS-Trust is required for federated authentication. | - Fix the configuration in the identity provider to avoid sending a DTD in the XML response.<br>- Event 1022 (Microsoft Entra analytics logs) contains the URL that's being accessed that's returning an XML response with a DTD. |

#### Common server error codes

| Error code | Reason | Resolution |
| --- | --- | --- |
| **AADSTS50155: Device authentication failed** | - Microsoft Entra ID is unable to authenticate the device to issue a PRT.<br>- Confirm that the device isn't deleted or disabled. For more information about this issue, see [Microsoft Entra device management FAQ](faq#why-do-my-users-see-an-error-message-saying--your-organization-has-deleted-the-device--or--your-organization-has-disabled-the-device--on-their-windows-10-11-devices). | Follow the instructions for this issue in [Microsoft Entra device management FAQ](faq#i-disabled-or-deleted-my-device--but-the-local-state-on-the-device-says-it-s-registered--what-should-i-do) to re-register the device based on the device join type. |
| **AADSTS50034: The user account `Account` does not exist in the `tenant id` directory** | Microsoft Entra ID is unable to find the user account in the tenant. | - Ensure that the user is typing the correct UPN.<br>- Ensure that the on-premises user account is being synced with Microsoft Entra ID.<br>- Event 1144 (Microsoft Entra analytics logs) contains the UPN provided. This error can sometimes be mapped to STATUS\_ACCOUNT\_DISABLED on a Windows client. However, the account is not actually disabled. This usually happens when the Windows client sends a SAM account name to Entra STS instead of a properly formatted UPN. This issue is usually accompanied by a lack of communication with an on-prem Active Directory domain controller in Hybrid deployments. Entra-native deployments do not encounter this issue. |
| **AADSTS50126: Error validating credentials due to invalid username or password.** | - The username and password entered by the user in the Windows LoginUI are incorrect.<br>- If the tenant has password hash sync enabled, the device is hybrid-joined, and the user just changed the password, it's likely that the new password hasn't synced with Microsoft Entra ID. | To acquire a fresh PRT with the new credentials, wait for the Microsoft Entra password sync to finish. |

#### Common network error codes

| Error code | Reason | Resolution |
| --- | --- | --- |
| **ERROR\_WINHTTP\_TIMEOUT** (12002)**ERROR\_WINHTTP\_NAME\_NOT\_RESOLVED** (12007)**ERROR\_WINHTTP\_CANNOT\_CONNECT** (12029)**ERROR\_WINHTTP\_CONNECTION\_ERROR** (12030) | Common general network-related issues. | - Events 1022 (Microsoft Entra analytics logs) and 1084 (Microsoft Entra operational logs) contain the URL that's being accessed.<br>- If the on-premises environment requires an outbound proxy, the IT admin must ensure that the computer account of the device can discover and silently authenticate to the outbound proxy.Get more [network error codes](/en-us/windows/win32/winhttp/error-messages). |

### Step 4: Collect logs

#### Regular logs

1. Go to https://aka.ms/icesdptool to automatically download a *.cab* file containing the Diagnostic tool.
2. Run the tool and repro your scenario.
3. For Fiddler traces, accept the certificate requests that pop up.
4. The wizard prompts you for a password to safeguard your trace files. Provide a password.
5. Finally, open the folder where all the collected logs are stored, such as *%LOCALAPPDATA%\ElevatedDiagnostics\numbers*.
6. Contact Support with contents of the latest *.cab* file.

#### Network traces

Note

When you're collecting network traces, it's important to *not* use Fiddler during repro.

1. Run `netsh trace start scenario=internetClient_dbg capture=yes persistent=yes`.
2. Lock and unlock the device. For hybrid-joined devices, wait a minute or more to allow the PRT acquisition task to finish.
3. Run `netsh trace stop`.
4. Share the *nettrace.cab* file with Support.

## Known issues

If you're connected to a mobile hotspot or an external Wi-Fi network and you go to **Settings** &gt; **Accounts** &gt; **Access Work or School**, Microsoft Entra hybrid joined devices might show two different accounts, one for Microsoft Entra ID and one for on-premises AD. This UI issue doesn't affect functionality.