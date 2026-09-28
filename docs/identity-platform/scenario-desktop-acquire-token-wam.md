---
layout: Conceptual
title: Acquire a token to call a web API by using Web Account Manager (desktop app) - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/scenario-desktop-acquire-token-wam
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn how to build a desktop app that calls web APIs to acquire a token for the app by using Web Account Manager.
manager: dougeby
ms.custom: 
ms.date: 2024-01-15T00:00:00.0000000Z
ms.subservice: workforce
ms.topic: how-to
locale: en-us
document_id: 05e8b1a2-cfad-7192-7c04-c768965501e9
document_version_independent_id: 541253a0-818a-c681-ac65-2f29b8001420
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/scenario-desktop-acquire-token-wam.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/scenario-desktop-acquire-token-wam
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/scenario-desktop-acquire-token-wam.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
platformId: e3186141-8972-fa4b-6212-9b3dc5bd287d
---

# Acquire a token to call a web API by using Web Account Manager (desktop app) - Microsoft identity platform | Microsoft Learn

**Applies to**: ![Green circle with a white check mark symbol that indicates the following content applies to workforce tenants.](../external-id/media/common/applies-to-yes.png) Workforce tenants ([learn more](/en-us/entra/external-id/tenant-configurations))

The Microsoft Authentication Library (MSAL) calls Web Account Manager (WAM), a Windows 10+ component that acts as an authentication broker. The broker allows users of your app to benefit from integration with accounts known to Windows, such as the account you signed into your Windows session.

## WAM value proposition

Using an authentication broker such as WAM has numerous benefits:

- Enhanced security. See [Token protection](../identity/conditional-access/concept-token-protection).
- Support for Windows Hello, Conditional Access, and FIDO keys.
- Integration with the Windows **Email & accounts** view.
- Fast single sign-on.
- Ability to sign in silently with the current Windows account.
- Bug fixes and enhancements shipped with Windows.

## WAM limitations

- WAM is available on Windows 10 and later, and on Windows Server 2019 and later. On Mac, Linux, and earlier versions of Windows, MSAL automatically falls back to a browser.
- Azure Active Directory B2C (Azure AD B2C) and Active Directory Federation Services (AD FS) authorities aren't supported. MSAL falls back to a browser.

## WAM integration package

Most apps need to reference the `Microsoft.Identity.Client.Broker` package to use this integration. .NET MAUI apps don't have to do this, because the functionality is inside MSAL when the target is `net6-windows` and later.

## WAM calling pattern

You can use the following pattern for WAM:

```csharp
    // 1. Configuration - read below about redirect URI
    var pca = PublicClientApplicationBuilder.Create("client_id")
                    .WithBroker(new BrokerOptions(BrokerOptions.OperatingSystems.Windows))
                    .Build();

    // Add a token cache; see https://learn.microsoft.com/azure/active-directory/develop/msal-net-token-cache-serialization?tabs=desktop

    // 2. Find an account for silent login

    // Is there an account in the cache?
    IAccount accountToLogin = (await pca.GetAccountsAsync()).FirstOrDefault();
    if (accountToLogin == null)
    {
        // 3. No account in the cache; try to log in with the OS account
        accountToLogin = PublicClientApplication.OperatingSystemAccount;
    }

    try
    {
        // 4. Silent authentication 
        var authResult = await pca.AcquireTokenSilent(new[] { "User.Read" }, accountToLogin)
                                    .ExecuteAsync();
    }
    // Cannot log in silently - most likely Azure AD would show a consent dialog or the user needs to re-enter credentials
    catch (MsalUiRequiredException) 
    {
        // 5. Interactive authentication
        var authResult = await pca.AcquireTokenInteractive(new[] { "User.Read" })
                                    .WithAccount(accountToLogin)
                                    // This is mandatory so that WAM is correctly parented to your app; read on for more guidance
                                    .WithParentActivityOrWindow(myWindowHandle) 
                                    .ExecuteAsync();
                                    
        // Consider allowing the user to re-authenticate with a different account, by calling AcquireTokenInteractive again                                  
    }
```

If a broker isn't present (for example, Windows 8.1, Mac, or Linux), MSAL falls back to a browser, where redirect URI rules apply.

### Redirect URI

You don't need to configure WAM redirect URIs in MSAL, but you do need to configure them in the app registration:

```
ms-appx-web://Microsoft.AAD.BrokerPlugin/{client_id}

```

### Token cache persistence

It's important to persist the MSAL token cache because MSAL continues to store ID tokens and account metadata there. For more information, see [Token cache serialization in MSAL.NET](/en-us/entra/msal/dotnet/how-to/token-cache-serialization?tabs=desktop).

### Account for silent login

To find an account for silent login, we recommend this pattern:

- If the user previously logged in, use that account. If not, use `PublicClientApplication.OperatingSystemAccount` for the current Windows account.
- Allow the user to change to a different account by logging in interactively.

## Parent window handles

You must configure MSAL with the window that the interactive experience should be parented to, by using `WithParentActivityOrWindow` APIs.

### UI applications

For UI apps like Windows Forms (WinForms), Windows Presentation Foundation (WPF), or Windows UI Library version 3 (WinUI3), see [Retrieve a window handle](/en-us/windows/apps/develop/ui-input/retrieve-hwnd).

### Console applications

For console applications, the configuration is more involved because of the terminal window and its tabs. Use the following code:

```csharp
enum GetAncestorFlags
{   
    GetParent = 1,
    GetRoot = 2,
    /// <summary>
    /// Retrieves the owned root window by walking the chain of parent and owner windows returned by GetParent.
    /// </summary>
    GetRootOwner = 3
}

/// <summary>
/// Retrieves the handle to the ancestor of the specified window.
/// </summary>
/// <param name="hwnd">A handle to the window whose ancestor will be retrieved.
/// If this parameter is the desktop window, the function returns NULL. </param>
/// <param name="flags">The ancestor to be retrieved.</param>
/// <returns>The return value is the handle to the ancestor window.</returns>
[DllImport("user32.dll", ExactSpelling = true)]
static extern IntPtr GetAncestor(IntPtr hwnd, GetAncestorFlags flags);

[DllImport("kernel32.dll")]
static extern IntPtr GetConsoleWindow();

// This is your window handle!
public IntPtr GetConsoleOrTerminalWindow()
{
   IntPtr consoleHandle = GetConsoleWindow();
   IntPtr handle = GetAncestor(consoleHandle, GetAncestorFlags.GetRootOwner );
  
   return handle;
}
```

## Troubleshooting

### "WAM Account Picker did not return an account" error message

The "WAM Account Picker did not return an account" message indicates that either the application user closed the dialog that displays accounts, or the dialog itself crashed. A crash might occur if `AccountsControl`, a Windows control, is registered incorrectly in Windows. To resolve this problem:

1. On the taskbar, right-click **Start**, and then select **Windows PowerShell (Admin)**.
2. If you're prompted by a User Account Control dialog, select **Yes** to start PowerShell.
3. Copy and then run the following script:

    ```powershell
    if (-not (Get-AppxPackage Microsoft.AccountsControl)) { Add-AppxPackage -Register "$env:windir\SystemApps\Microsoft.AccountsControl_cw5n1h2txyewy\AppxManifest.xml" -DisableDevelopmentMode -ForceApplicationShutdown } Get-AppxPackage Microsoft.AccountsControl
    ```

### "MsalClientException: ErrorCode: wam\_runtime\_init\_failed" error message during a single file deployment

You might see the following error when packaging your application into a [single file bundle](/en-us/dotnet/core/deploying/single-file/overview):

```
MsalClientException: wam_runtime_init_failed: The type initializer for 'Microsoft.Identity.Client.NativeInterop.API' threw an exception. See https://aka.ms/msal-net-wam#troubleshooting
```

This error indicates that the native binaries from [Microsoft.Identity.Client.NativeInterop](https://www.nuget.org/packages/Microsoft.Identity.Client.NativeInterop/) were not packaged into the single file bundle. To embed those files for extraction and get one output file, set the property `IncludeNativeLibrariesForSelfExtract` to `true`. [Read more about how to package native binaries into a single file](/en-us/dotnet/core/deploying/single-file/overview?tabs=cli#native-libraries).

### Connection problems

If the application user regularly sees an error message that's similar to "Please check your connection and try again," see the [troubleshooting guide for Office](/en-us/microsoft-365/troubleshoot/authentication/connection-issue-when-sign-in-office-2016). That troubleshooting guide also uses the broker.

## Sample

You can find a WPF sample that uses WAM [on GitHub](https://github.com/azure-samples/active-directory-dotnet-desktop-msgraph-v2).