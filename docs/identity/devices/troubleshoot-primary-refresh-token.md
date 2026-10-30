---
layout: Conceptual
title: Troubleshoot primary refresh token issues on Windows devices - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/devices/troubleshoot-primary-refresh-token
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: OWinfreyATL
ms.author: owinfrey
ms.service: entra-id
ms.subservice: devices
manager: dougeby
description: Troubleshoot primary refresh token issues during authentication through Microsoft Entra credentials on Microsoft Entra joined Windows devices.
ms.topic: troubleshooting
ms.date: 2026-02-23T00:00:00.0000000Z
editor: v-jsitser
ms.reviewer: gudlapreethi, bemey, filuz, robgarcia, v-leedennis
locale: en-us
document_id: e808ed21-7cf4-ad31-5f14-89e970000e0c
document_version_independent_id: 054d28e5-e3e3-f099-54ff-77fb0dab006d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/devices/troubleshoot-primary-refresh-token.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/devices/troubleshoot-primary-refresh-token
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/devices/troubleshoot-primary-refresh-token.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 14af4725-92b8-95dc-ec4d-63bd9ce128bd
---

# Troubleshoot primary refresh token issues on Windows devices - Microsoft Entra ID | Microsoft Learn

This article discusses how to troubleshoot issues that involve the [primary refresh token (PRT)](concept-primary-refresh-token) when you authenticate on a Microsoft Entra joined Windows device by using your Microsoft Entra credentials.

On devices that are joined to Microsoft Entra ID or hybrid Microsoft Entra ID, the main component of authentication is the PRT. You obtain this token by signing in to Windows 10 by using Microsoft Entra credentials on a Microsoft Entra joined device for the first time. The PRT is cached on that device. For subsequent sign-ins, the cached token is used to let you use the desktop.

As part of the process of locking and unlocking the device or signing in again to Windows, a background network authentication attempt is made one time every four hours to refresh the PRT. If problems occur that prevent refreshing the token, the PRT eventually expires. Expiration affects single sign-on (SSO) to Microsoft Entra resources. It also causes sign-in prompts to be shown.

If you suspect that a PRT problem exists, we recommend that you first collect Microsoft Entra logs, and follow the steps that are outlined in the troubleshooting checklist. Do this for any Microsoft Entra client issue first, ideally within a repro session. Complete this process before you file a support request.

## Troubleshooting checklist

### Step 1: Get the status of the primary refresh token

1. Sign in to Windows under the user account in which you experience PRT issues.
2. Select **Start**, and then search for and select **Command Prompt**.
3. To run the device registration command ([dsregcmd](troubleshoot-device-dsregcmd)), enter `dsregcmd /status`.
4. Locate the [SSO state](troubleshoot-device-dsregcmd#sso-state) section of the device registration command's output. The following text shows an example of this section:

    ```output
    +----------------------------------------------------------------------+
    | SSO State                                                            |
    +----------------------------------------------------------------------+
    
                    AzureAdPrt : YES
          AzureAdPrtUpdateTime : 2020-07-12 22:57:53.000 UTC
          AzureAdPrtExpiryTime : 2020-07-26 22:58:35.000 UTC
           AzureAdPrtAuthority : https://login.microsoftonline.com/00001111-aaaa-2222-bbbb-3333cccc4444
                 EnterprisePrt : YES
       EnterprisePrtUpdateTime : 2020-07-12 22:57:54.000 UTC
       EnterprisePrtExpiryTime : 2020-07-26 22:57:54.000 UTC
        EnterprisePrtAuthority : https://msft.sts.microsoft.com:443/adfs
    
    +----------------------------------------------------------------------+
    ```
5. Check the value of the `AzureAdPrt` field. If it's set to `NO`, an error occurred when you tried to acquire the PRT status from Microsoft Entra ID.
6. Check the value of the `AzureAdPrtUpdateTime` field. If the value of the `AzureAdPrtUpdateTime` field is more than four hours, a problem is likely preventing the PRT from refreshing. Lock and unlock the device to force a PRT refresh, and then check whether the time is updated.

### Step 2: Get the error code

The next step is to get the error code that causes the PRT error. The quickest way to get the PRT error code is to examine the device registration command output. However, this method requires the Windows 10 May 2021 update (version 21H1) or a later version. The other method is to find the error code in Microsoft Entra analytic and operational logs.

#### Method 1: Examine the device registration command output

Note

This method is available only if you're using the Windows 10 May 2021 update (version 21H1) or a later version of Windows.

To get the PRT error code, run the `dsregcmd` command, and then locate the `SSO State` section. In the `AzureAdPrt` field, the `Attempt Status` field contains the error code. In the following example, the error code is `0xc000006d`.

```output
                AzureAdPrt : NO
       AzureAdPrtAuthority : https://login.microsoftonline.com/aaaa0000-bb11-2222-33cc-444444dddddd
     AcquirePrtDiagnostics : PRESENT
      Previous Prt Attempt : 2020-09-18 20:20:09.760 UTC
            Attempt Status : 0xc000006d
             User Identity : user@contoso.com
           Credential Type : Password
            Correlation ID : aaaa0000-bb11-2222-33cc-444444dddddd
              Endpoint URI : https://login.microsoftonline.com/aaaa0000-bb11-2222-33cc-444444dddddd/oauth2/token
               HTTP Method : POST
                HTTP Error : 0x0
               HTTP status : 400
         Server Error Code : invalid_grant
  Server Error Description : AADSTS50126: Error validating credentials due to invalid username or password.
```

#### Method 2: Use Event Viewer to examine AAD analytic and operational logs

1. Select **Start**, and then search for and select **Event Viewer**.
2. If the console tree doesn't appear in the **Event Viewer** window, select the **Show/Hide Console Tree** icon to make the console tree visible.
3. In the console tree, select **Event Viewer (Local)**. If child nodes don't appear underneath this item, double-click your selection to show them.
4. Select the **View** menu. If a check mark isn't displayed next to **Show Analytic and Debug Logs**, select that menu item to enable that feature.
5. In the console tree, expand **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **AAD**. The **Operational** and **Analytic** child nodes appear.

    Note

    In the Microsoft Entra Cloud Authentication Provider (CloudAP) plug-in, **Error** events are written to the **Operational** event logs, and information events are written to the **Analytic** event logs. You have to examine both the **Operational** and **Analytic** event logs to troubleshoot PRT issues.
6. In the console tree, select the **Analytic** node to view AAD-related analytic events.
7. In the list of analytic events, search for Event IDs 1006 and 1007. Event ID 1006 denotes the beginning of the PRT acquisition flow, and Event ID 1007 denotes the end of the PRT acquisition flow. All events in the **AAD** logs (both **Analytic** and **Operational**) that occurred between Event ID 1006 and Event ID 1007 are logged as part of the PRT acquisition flow. The following table shows an example event listing.

    | Level | Date and Time | Source | Event ID | Task Category |
    | --- | --- | --- | --- | --- |
    | **Information** | **6/24/2020 3:35:35 AM** | **AAD** | **1006** | **AadCloudAPPlugin Operation** |
    | Information | 6/24/2020 3:35:35 AM | AAD | 1018 | AadCloudAPPlugin Operation |
    | Information | 6/24/2020 3:35:35 AM | AAD | 1144 | AadCloudAPPlugin Operation |
    | Information | 6/24/2020 3:35:35 AM | AAD | 1022 | AadCloudAPPlugin Operation |
    | Error | 6/24/2020 3:35:35 AM | AAD | 1084 | AadCloudAPPlugin Operation |
    | Error | 6/24/2020 3:35:35 AM | AAD | 1086 | AadCloudAPPlugin Operation |
    | Error | 6/24/2020 3:35:35 AM | AAD | 1160 | AadCloudAPPlugin Operation |
    | **Information** | **6/24/2020 3:35:35 AM** | **AAD** | **1007** | **AadCloudAPPlugin Operation** |
    | Information | 6/24/2020 3:35:35 AM | AAD | 1157 | AadCloudAPPlugin Operation |
    | Information | 6/24/2020 3:35:35 AM | AAD | 1158 | AadCloudAPPlugin Operation |
8. Double-click the row that contains Event ID 1007. The **Event Properties** dialog box for this event appears.
9. In the description box on the **General** tab, copy the error code. The error code is a 10-character string that begins with `0x`, followed by an 8-digit hexadecimal number.

### Step 3: Get troubleshooting instructions for certain error codes

#### Status codes ("STATUS\_" prefix, codes that begin with "0xc000")

STATUS\_LOGON\_FAILURE (-1073741715 / 0xc000006d), STATUS\_WRONG\_PASSWORD (-1073741718 / 0xc000006a)

##### Cause

- The device can't connect to the Microsoft Entra authentication service.
- The device received a `400 Bad Request` HTTP error response from one of the following sources:

    - The Microsoft Entra authentication service
    - An endpoint for the [WS-Trust protocol](http://docs.oasis-open.org/ws-sx/ws-trust/v1.4/ws-trust.html) (required for federated authentication)

##### Solution

- If the on-premises environment requires an outbound proxy, make sure that the computer account of the device can discover and silently authenticate to the outbound proxy.
- Get the server error code and error description, and then go to the Common server error codes ("AADSTS" prefix) section to find the cause of that server error code and the solution details.

    In the Microsoft Entra operational logs, Event ID 1081 contains the server error code and error description if the error occurs in the Microsoft Entra authentication service. If the error occurs in a WS-Trust endpoint, the server error code and error description are found in Event ID 1088. In the Microsoft Entra analytic logs, the first instance of Event ID 1022 (that precedes operational Event IDs 1081 and 1088) contains the URL that's being accessed.

    To view Event IDs in the Microsoft Entra operational and analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.

STATUS\_REQUEST\_NOT\_ACCEPTED (-1073741616 / 0xc00000d0)

##### Cause

The device received a `400 Bad Request` HTTP error response from one of the following sources:

- The Microsoft Entra authentication service
- An endpoint for the [WS-Trust protocol](http://docs.oasis-open.org/ws-sx/ws-trust/v1.4/ws-trust.html) (required for federated authentication)

##### Solution

Get the server error code and error description, and then go to the Common server error codes ("AADSTS" prefix) section to find the cause of that server error code and the solution details.

In the Microsoft Entra operational logs, Event ID 1081 contains the server error code and error description if the error occurs in the Microsoft Entra authentication service. If the error occurs in a WS-Trust endpoint, the server error code and error description are found in Event ID 1088. In the Microsoft Entra analytic logs, the first instance of Event ID 1022 (that precedes operational Event IDs 1081 and 1088) contains the URL that's being accessed.

To view Event IDs in the Microsoft Entra operational and analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.

STATUS\_NETWORK\_UNREACHABLE (-1073741252 / 0xc000023c), STATUS\_BAD\_NETWORK\_PATH (-1073741634 / 0xc00000be), STATUS\_UNEXPECTED\_NETWORK\_ERROR (-1073741628 / 0xc00000c4)

##### Cause

- The device received a `4xx` HTTP error response from one of the following sources:

    - The Microsoft Entra authentication service
    - An endpoint for the [WS-Trust protocol](http://docs.oasis-open.org/ws-sx/ws-trust/v1.4/ws-trust.html) (required for federated authentication)
- A network connectivity issue to a required endpoint exists.

##### Solution

- Get the server error code and error description, and then go to the Common server error codes ("AADSTS" prefix) section to find the cause of that server error code and the solution details.

    In the Microsoft Entra operational logs, Event ID 1081 contains the server error code and error description if the error occurs in the Microsoft Entra authentication service. If the error occurs in a WS-Trust endpoint, the server error code and error description are found in Event ID 1088.
- For a network connectivity issue, get the URL that's being accessed and the suberror code from the network stack. Event ID 1022 in the Microsoft Entra analytic logs contains the URL that's being accessed. Event ID 1084 in the Microsoft Entra operational logs contains the suberror code from the network stack.

To view Event IDs in the Microsoft Entra operational and analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.

STATUS\_NO\_SUCH\_LOGON\_SESSION (-1073741729 / 0xc000005f)

##### Cause

The user realm discovery failed because the Microsoft Entra authentication service can't find the user's domain.

##### Solution

- Add the domain of the user principal name (UPN) of the user as a custom domain in Microsoft Entra ID. To find the provided UPN, look for Event ID 1144 in the Microsoft Entra analytic logs.

    To view Event IDs in the Microsoft Entra analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.
- If the on-premises domain name can't be routed (for example, if the UPN is something such as `jdoe@contoso.local`), [configure the Alternate Login ID](/en-us/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) (AltID). (To view the prerequisites, see [Plan your Microsoft Entra hybrid join implementation](hybrid-join-plan).)

#### Common CloudAP plug-in error codes ("AAD\_CLOUDAP\_E\_" prefix, codes that begin with "0xc004")

AAD\_CLOUDAP\_E\_OAUTH\_USERNAME\_IS\_MALFORMED (-1073445812 / 0xc004844c)

##### Cause

The UPN for the user isn't in the expected format. The UPN value varies according to the device type, as shown in the following table.

| Device join type | UPN value |
| --- | --- |
| Microsoft Entra joined devices | The text that's entered when the user signs in |
| Microsoft Entra hybrid joined devices | The UPN that the domain controller returns during the sign-in process |

##### Solution

- Set the UPN of the user to an internet-style sign-in name, based on internet standard RFC 822. To find the current UPN, look for event ID 1144 in the Microsoft Entra analytic logs.

    To view Event IDs in the Microsoft Entra analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.
- For Microsoft Entra hybrid joined devices, make sure that you configured the domain controller to return the UPN in the correct format. To display the configured UPN in the domain controller, run the following [whoami](/en-us/windows-server/administration/windows-commands/whoami) command:

    ```cmd
    whoami /upn
    ```

    If Active Directory is configured with the correct UPN, collect time travel traces for the Local Security Authority Subsystem Service (LSASS or *lsass.exe*).
- If the on-premises domain name can't be routed (for example, if the UPN is something such as `jdoe@contoso.local`), [configure the Alternate Login ID](/en-us/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) (AltID). (To view the prerequisites, see [Plan your Microsoft Entra hybrid join implementation](hybrid-join-plan).)

AAD\_CLOUDAP\_E\_OAUTH\_USER\_SID\_IS\_EMPTY (-1073445822 / 0xc0048442)

##### Cause

The user security identifier (SID) is missing in the ID token that the Microsoft Entra authentication service returns.

##### Solution

Make sure that the network proxy doesn't interfere with or modify the server response.

AAD\_CLOUDAP\_E\_WSTRUST\_SAML\_TOKENS\_ARE\_EMPTY (-1073445695 / 0xc00484c1 / 0x800484c1)

##### Cause

You received an error from the [WS-Trust protocol](http://docs.oasis-open.org/ws-sx/ws-trust/v1.4/ws-trust.html) endpoint (required for federated authentication).

##### Solution

- Make sure that the network proxy doesn't interfere with or modify the server response.
- Get the server error code and error description from Event ID 1088 in the Microsoft Entra operational logs. Then, go to the Common server error codes ("AADSTS" prefix) section to find the cause of that server error code and the solution details.

    To view Event IDs in the Microsoft Entra operational logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.

AAD\_CLOUDAP\_E\_HTTP\_PASSWORD\_URI\_IS\_EMPTY (-1073445749 / 0xc004848b)

##### Cause

The Metadata Exchange (MEX) endpoint is configured incorrectly. The MEX response doesn't contain any password URLs.

##### Solution

- Make sure that the network proxy doesn't interfere with or modify the server response.
- Fix the MEX configuration to return valid URLs in the response.

AAD\_CLOUDAP\_E\_HTTP\_CERTIFICATE\_URI\_IS\_EMPTY (-1073445748 / 0xc004848c)

##### Cause

The Metadata Exchange (MEX) endpoint is configured incorrectly. The MEX response doesn't contain any certificate endpoint URLs.

##### Solution

- Make sure that the network proxy doesn't interfere with or modify the server response.
- Fix the MEX configuration in the identity provider to return valid certificate URLs in the response.

#### Common XML error codes (codes that begin with "0xc00c")

WC\_E\_DTDPROHIBITED (-1072894385 / 0xc00cee4f)

##### Cause

The XML response from the [WS-Trust protocol](http://docs.oasis-open.org/ws-sx/ws-trust/v1.4/ws-trust.html) endpoint (required for federated authentication) included a document type definition (DTD). The DTD isn't expected in the XML response, and response parsing fails if the DTD is included.

##### Solution

- Fix the configuration in the identity provider to avoid sending the DTD in the XML response.
- Get the URL that's being accessed from Event ID 1022 in the Microsoft Entra analytic logs.

    To view Event IDs in the Microsoft Entra analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.

#### Common server error codes ("AADSTS" prefix)

You can find a full list and description of server error codes in [Microsoft Entra authentication and authorization error codes](../../identity-platform/reference-error-codes).

AADSTS50155: Device authentication failed

##### Cause

- Microsoft Entra ID can't authenticate the device to issue a PRT.
- The device might have been deleted or disabled. (For more information, see [Why do my users see an error message saying "Your organization has deleted the device" or "Your organization has disabled the device" on their Windows 10/11 devices?](faq#why-do-my-users-see-an-error-message-saying--your-organization-has-deleted-the-device--or--your-organization-has-disabled-the-device--on-their-windows-10-11-devices))

##### Solution

Re-register the device based on the device join type. For instructions, see [I disabled or deleted my device. But the local state on the device says it's still registered. What should I do?](faq#i-disabled-or-deleted-my-device--but-the-local-state-on-the-device-says-it-s-registered--what-should-i-do).

AADSTS50034: The user account &lt;Account&gt; does not exist in the &lt;tenant-id&gt; directory

##### Cause

Microsoft Entra ID can't find the user account in the tenant.

##### Solution

- Make sure that the user is entering the correct UPN.
- Make sure that the on-premises user account is being synchronized to Microsoft Entra ID.
- Get the provided UPN by looking for Event ID 1144 in the Microsoft Entra analytic logs.

    To view Event IDs in the Microsoft Entra analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.

AADSTS50126: Error validating credentials due to invalid username or password

##### Cause

- The user entered an incorrect username or password in the sign-in UI.
- The password hasn't been synchronized to Microsoft Entra ID because of the following scenario:

    - The tenant has enabled [password hash synchronization](../hybrid/connect/whatis-phs).
    - The device is a Microsoft Entra hybrid joined device.
    - The user recently changed the password.

##### Solution

To acquire a fresh PRT that has the new credentials, wait for the Microsoft Entra synchronization to finish.

#### Common network error codes ("ERROR\_WINHTTP\_" prefix)

You can find a full list and description of network error codes in [Error messages (Winhttp.h)](/en-us/windows/win32/winhttp/error-messages).

ERROR\_WINHTTP\_TIMEOUT (12002), ERROR\_WINHTTP\_NAME\_NOT\_RESOLVED (12007), ERROR\_WINHTTP\_CANNOT\_CONNECT (12029), ERROR\_WINHTTP\_CONNECTION\_ERROR (12030)

##### Cause

Common general network-related issues.

##### Solution

- Get the URL that's being accessed. You can find the URL in Event ID 1084 of the Microsoft Entra operational log or Event ID 1022 of the Microsoft Entra analytic log.

    To view Event IDs in the Microsoft Entra operational and analytic logs, refer to the Method 2: Use Event Viewer to examine Microsoft Entra analytic and operational logs section.
- If the on-premises environment requires an outbound proxy, make sure that the computer account of the device can discover and silently authenticate to the outbound proxy.
- Collect network traces by following these steps:

    Important

    Don't use Fiddler during this procedure.

    1. Run the following [netsh trace start](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj129382%28v=ws.11%29#start) command:

        ```cmd
        netsh trace start scenario=InternetClient_dbg capture=yes persistent=yes
        ```
    2. Lock the device.
    3. If the device is a Microsoft Entra hybrid joined device, wait at least 60 seconds to let the PRT acquisition task finish.
    4. Unlock the device.
    5. Run the following [netsh trace stop](/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj129382%28v=ws.11%29#stop) command:

        ```cmd
        netsh trace stop
        ```

### Step 4: Collect the logs and traces

#### Regular logs

1. Download the [Auth script archive](https://aka.ms/authscripts), and extract the scripts into a local directory.
2. Open an administrative PowerShell session, and change the current directory to the directory in which you saved the Auth scripts.
3. To begin the error tracing session, enter the following command:

    ```powershell
    .\Start-auth.ps1 -vAuth -acceptEULA
    ```
4. Switch the Windows user account to go to your problem user's session.
5. Lock the device.
6. If the device is a Microsoft Entra hybrid joined device, wait at least 60 seconds to let the PRT acquisition task finish.
7. Unlock the device.
8. Switch the Windows user account back to your administrative session that's running the tracing session.
9. After you reproduce the issue, run the following command to end the tracing session:

    ```powershell
    .\stop-auth.ps1
    ```
10. Wait for all tracing to stop completely.

#### Time travel traces

The following procedure describes how to capture traces by using the [Time Travel Debugging (TTD)](/en-us/windows-hardware/drivers/debugger/time-travel-debugging-overview) feature.

Warning

Time travel traces contain personal data. In addition, Local Security Authority Subsystem Service (LSASS or *lsass.exe*) traces contain extremely sensitive information. When you handle these traces, make sure that you use best practices for the storage and sharing of this type of information.

1. Select **Start**, enter *cmd*, locate and right-click **Command Prompt** in the search results, and then select **Run as administrator**.
2. At the command prompt, create a temporary directory:

    ```cmd
    mkdir c:\temp
    ```
3. Run the following [tasklist](/en-us/windows-server/administration/windows-commands/tasklist) command:

    ```cmd
    tasklist /m lsasrv.dll
    ```
4. In the `tasklist` command output, find the process identifier (`PID`) of *lsass.exe*.
5. To begin a tracing session of the *lsass.exe* process, run the following time travel debugging command (*[TTD.exe](/en-us/windows-hardware/drivers/debugger/time-travel-debugging-ttd-exe-command-line-util)*):

    ```cmd
    TTD.exe -attach <lsass-pid> -out c:\temp
    ```
6. Lock the device that's signed in under the domain account.
7. Unlock the device.
8. To end the time travel tracing session, run the following TTD command:

    ```cmd
    TTD.exe -stop all
    ```
9. Get the latest *lsass##.run* file.