---
layout: Conceptual
title: Govern the existing users of an application that does not support provisioning in Microsoft Entra ID with Microsoft PowerShell - Microsoft Entra ID Governance | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/id-governance/identity-governance-applications-not-provisioned-users
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: markwahl-msft
ms.author: mwahl
ms.service: entra-id-governance
manager: dougeby
description: Planning for a successful access reviews campaign for a particular application includes identifying if any users in that application have access that doesn't derive from Microsoft Entra ID.  If the application does not support provisioning, then you will need to create application role assignments for the application, and supply the list of changes when a review completes.
ms.topic: how-to
ms.date: 2026-04-13T00:00:00.0000000Z
ms.reviewer: mwahl
ms.custom: sfi-ga-nochange
locale: en-us
document_id: ea6fcbf2-4951-7b4d-f6f8-85588ea5ba4d
document_version_independent_id: 8ad1e0e0-2c69-8374-8cc3-19a0f0c9b20f
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/id-governance/identity-governance-applications-not-provisioned-users.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: id-governance/identity-governance-applications-not-provisioned-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/id-governance/identity-governance-applications-not-provisioned-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 245da890-c4cd-48ac-43ac-c1cd8c6df2ec
---

# Govern the existing users of an application that does not support provisioning in Microsoft Entra ID with Microsoft PowerShell - Microsoft Entra ID Governance | Microsoft Learn

There are four common scenarios in which it's necessary to populate Microsoft Entra ID with existing users and their access rights of an application before you use the application with a Microsoft Entra ID Governance feature such as [access reviews](access-reviews-application-preparation).

- Application migrated to Microsoft Entra ID after using its own identity provider
- Application that doesn't use Microsoft Entra ID as its only identity provider
- Application does not use Microsoft Entra ID as its identity provider nor does it support provisioning
- Application uses Microsoft Entra ID as its identity provider and has additional access rights for users

For more information on those first two scenarios, where the application supports provisioning, or uses an LDAP directory, SQL database, has a SOAP or REST API or relies upon Microsoft Entra ID as its identity provider, see the article [govern an application's existing users](identity-governance-applications-existing-users). That article covers how to use identity governance features for existing users of those categories of applications.

This article covers the third scenario. For some legacy applications, it might not be feasible to remove other identity providers or local credential authentication from the application, or enable support for provisioning protocols for those applications. For those applications, if you want to use Microsoft Entra ID to review who has access to that application, or remove someone's access from that application, you'll need to create assignments in Microsoft Entra ID that represent application users. This article covers that scenario of an application that does not use Microsoft Entra ID as its identity provider and does not support provisioning.

For more information on the fourth scenario, see [include custom data provided resource in the catalog for catalog user Access Reviews (Preview)](custom-data-resource-access-reviews).

## License requirements

Using this feature requires Microsoft Entra ID Governance or Microsoft Entra Suite licenses. To find the right license for your requirements, see [Microsoft Entra ID Governance licensing fundamentals](licensing-fundamentals).

## Terminology

This article illustrates the process for managing application role assignments by using the [Microsoft Graph PowerShell cmdlets](https://www.powershellgallery.com/packages/Microsoft.Graph). It uses the following Microsoft Graph terminology.

![Diagram that illustrates Microsoft Graph terminology.](media/identity-governance-applications-existing-users/data-model-terminology.png)

In Microsoft Entra ID, a service principal (`ServicePrincipal`) represents an application in a particular organization's directory. `ServicePrincipal` has a property called `AppRoles` that lists the roles that an application supports, such as `Marketing specialist`. `AppRoleAssignment` links a user to a service principal and specifies which role that user has in that application.

You might also be using [Microsoft Entra entitlement management](entitlement-management-overview) access packages to give users time-limited access to the application. In entitlement management, `AccessPackage` contains one or more resource roles, potentially from multiple service principals. `AccessPackage` also has assignments (`Assignment`) for users to the access package.

When you create an assignment for a user to an access package, Microsoft Entra entitlement management automatically creates the necessary `AppRoleAssignment` instances for the user to each application. For more information, see the [Manage access to resources in Microsoft Entra entitlement management](/en-us/powershell/microsoftgraph/tutorial-entitlement-management) tutorial on how to create access packages through PowerShell.

## Before you begin

- You must have one of the following licenses in your tenant:

    - Microsoft Entra ID P2 or Microsoft Entra ID Governance
    - Enterprise Mobility + Security E5 license
- You need to have an appropriate administrative role. If this is the first time you're performing these steps, you need the Global Administrator role to authorize the use of Microsoft Graph PowerShell in your tenant.
- Your application needs a service principal in your tenant. If a service principal does not already exist, then you can register an application to represent it in Microsoft Entra ID.

## Collect existing users from an application

The first step toward ensuring that all users are recorded in Microsoft Entra ID is to collect the list of existing users who have access to the application.

Some applications might have a built-in command to export a list of current users from the data store. In other cases, the application might rely on an external directory or database.

In some environments, the application might be located on a network segment or system that isn't appropriate for managing access to Microsoft Entra ID. If this system doesn't have the Microsoft Graph PowerShell cmdlets installed or doesn't have connectivity to Microsoft Entra ID, transfer the CSV file that contains the list of users to a system that has the [Microsoft Graph PowerShell cmdlets](https://www.powershellgallery.com/packages/Microsoft.Graph) installed.

This section explains four approaches for how to get a list of users in a comma-separated values (CSV) file:

- From an LDAP directory
- From a SQL Server database
- From another SQL-based database
- From SAP Cloud Identity Services

### Collect existing users from an application that uses an LDAP directory

This section applies to applications that use an LDAP directory as the underlying data store for users who don't authenticate to Microsoft Entra ID. Many LDAP directories, such as Active Directory, include a command that outputs a list of users.

1. Identify which of the users in that directory are in scope for being users of the application. This choice will depend on your application's configuration. For some applications, any user who exists in an LDAP directory is a valid user. Other applications might require the user to have a particular attribute or be a member of a group in that directory.
2. Run the command that retrieves that subset of users from your directory. Ensure that the output includes the attributes of users that will be used for matching with Microsoft Entra ID. Examples of these attributes are employee ID, account name, and email address.

    For example, this command would produce a CSV file in the current file system directory with the `userPrincipalName` attribute of every person in the LDAP directory:

    ```powershell
    $out_filename = ".\users.csv"
    csvde -f $out_filename -l userPrincipalName,cn -r "(objectclass=person)"
    ```
3. If needed, transfer the CSV file that contains the list of users to a system with the [Microsoft Graph PowerShell cmdlets](https://www.powershellgallery.com/packages/Microsoft.Graph) installed.
4. Continue reading at the Confirm Microsoft Entra ID has users that match users from the application section later in this article.

### Collect existing users from an application's database table by using a SQL Server wizard

This section applies to applications that use SQL Server as the underlying data store.

First, get a list of the users from the tables. Most databases provide a way to export the contents of tables to a standard file format, such as to a CSV file. If the application uses a SQL Server database, you can use the SQL Server Import and Export Wizard to export portions of a database. If you don't have a utility for your database, you can use the ODBC driver with PowerShell, as described in the next section.

1. Log in to the system where SQL Server is installed.
2. Open **SQL Server 2019 Import and Export (64 bit)** or the equivalent for your database.
3. Select the existing database as the source.
4. Select **Flat File Destination** as the destination. Provide a file name, and change the **Code page** value to **65001 (UTF-8)**.
5. Complete the wizard, and select the option to run immediately.
6. Wait for the execution to finish.
7. If needed, transfer the CSV file that contains the list of users to a system with the [Microsoft Graph PowerShell cmdlets](https://www.powershellgallery.com/packages/Microsoft.Graph) installed.
8. Continue reading at the Confirm Microsoft Entra ID has users that match users from the application section later in this article.

### Collect existing users from an application's database table by using PowerShell

This section applies to applications that use another SQL database as the underlying data store, where you're using the [ECMA Connector Host](../identity/app-provisioning/on-premises-sql-connector-configure) to provision users into that application. If you haven't yet configured the provisioning agent, use that guide to create the DSN connection file you'll use in this section.

1. Log in to the system where the provisioning agent is or will be installed.
2. Open PowerShell.
3. Construct a connection string for connecting to your database system.

    The components of a connection string depend on the requirements of your database. If you're using SQL Server, see the [list of DSN and connection string keywords and attributes](/en-us/sql/connect/odbc/dsn-connection-string-attribute).

    If you're using a different database, you need to include the mandatory keywords for connecting to that database. For example, if your database uses the fully qualified path name of the DSN file, a user ID, and a password, construct the connection string by using the following commands:

    ```powershell
    $filedsn = "c:\users\administrator\documents\db.dsn"
    $db_cs = "filedsn=" + $filedsn + ";uid=p;pwd=secret"
    ```
4. Open a connection to your database and provide the connection string, by using the following commands:

    ```powershell
    $db_conn = New-Object data.odbc.OdbcConnection
    $db_conn.ConnectionString = $db_cs
    $db_conn.Open()
    ```
5. Construct a SQL query to retrieve the users from the database table. Be sure to include the columns that will be used to match users in the application's database with those users in Microsoft Entra ID. Columns might include employee ID, account name, or email address.

    For example, if your users are held in a database table named `USERS` that has columns `name` and `email`, enter the following command:

    ```powershell
    $db_query = "SELECT name,email from USERS"
    
    ```
6. Send the query to the database via the connection:

    ```powershell
    $result = (new-object data.odbc.OdbcCommand($db_query,$db_conn)).ExecuteReader()
    $table = new-object System.Data.DataTable
    $table.Load($result)
    ```

    The result is the list of rows that represents users that were retrieved from the query.
7. Write the result to a CSV file:

    ```powershell
    $out_filename = ".\users.csv"
    $table.Rows | Export-Csv -Path $out_filename -NoTypeInformation -Encoding UTF8
    ```
8. If this system doesn't have the Microsoft Graph PowerShell cmdlets installed or doesn't have connectivity to Microsoft Entra ID, transfer the CSV file that contains the list of users to a system that has the [Microsoft Graph PowerShell cmdlets](https://www.powershellgallery.com/packages/Microsoft.Graph) installed.

### Collect existing users from SAP Cloud Identity Services

This section applies to SAP applications that use SAP Cloud Identity Services as the underlying service for user provisioning.

1. Sign in to your SAP Cloud Identity Services Admin Console, `https://<tenantID>.accounts.ondemand.com/admin`, or `https://<tenantID>.trial-accounts.ondemand.com/admin` if a trial.
2. Navigate to **Users & Authorizations &gt; Export Users**.
3. Select all attributes required for matching Microsoft Entra users with those in SAP. This includes the `SCIM ID`, `userName`, `emails`, and other attributes you may be using in your SAP Systems.
4. Select **Export** and wait for the browser to download the CSV file.
5. If this system doesn't have the Microsoft Graph PowerShell cmdlets installed or doesn't have connectivity to Microsoft Entra ID, transfer the CSV file that contains the list of users to a system that has the [Microsoft Graph PowerShell cmdlets](https://www.powershellgallery.com/packages/Microsoft.Graph) installed.

## Confirm Microsoft Entra ID has users that match users from the application

Now that you have a list of all the users obtained from the application, you'll match those users from the application's data store with users in Microsoft Entra ID.

### Retrieve the IDs of the users in Microsoft Entra ID

This section shows how to interact with Microsoft Entra ID by using [Microsoft Graph PowerShell](https://www.powershellgallery.com/packages/Microsoft.Graph) cmdlets.

The first time your organization uses these cmdlets for this scenario, you need to be in a Global Administrator role to allow Microsoft Graph PowerShell to be used in your tenant. Subsequent interactions can use a lower-privileged role, such as:

- User Administrator, if you anticipate creating new users.
- Application Administrator or [Identity Governance Administrator](../identity/role-based-access-control/permissions-reference#identity-governance-administrator), if you're just managing application role assignments.

1. Open PowerShell.
2. If you don't have the [Microsoft Graph PowerShell modules](https://www.powershellgallery.com/packages/Microsoft.Graph) already installed, install the `Microsoft.Graph.Users` module and others by using this command:

    ```powershell
    Install-Module Microsoft.Graph
    ```

    If you already have the modules installed, ensure that you're using a recent version:

    ```powershell
    Update-Module microsoft.graph.users,microsoft.graph.identity.governance,microsoft.graph.applications
    ```
3. Connect to Microsoft Entra ID:

    ```powershell
    $msg = Connect-MgGraph -ContextScope Process -Scopes "User.ReadWrite.All,Application.ReadWrite.All,AppRoleAssignment.ReadWrite.All,EntitlementManagement.ReadWrite.All"
    ```
4. If this is the first time you have used this command, you may need to consent to allow the Microsoft Graph Command Line tools to have these permissions.
5. Read the list of users obtained from the application's data store into the PowerShell session. If the list of users was in a CSV file, you can use the PowerShell cmdlet `Import-Csv` and provide the name of the file from the previous section as an argument.

    For example, if the file obtained from SAP Cloud Identity Services is named *Users-exported-from-sap.csv* and is located in the current directory, enter this command.

    ```powershell
    $filename = ".\Users-exported-from-sap.csv"
    $dbusers = Import-Csv -Path $filename -Encoding UTF8
    ```

    For another example if you are using a database or directory, if the file is named *users.csv* and located in the current directory, enter this command:

    ```powershell
    $filename = ".\users.csv"
    $dbusers = Import-Csv -Path $filename -Encoding UTF8
    ```
6. Choose the column of the *users.csv* file that will match with an attribute of a user in Microsoft Entra ID.

    If you are using SAP Cloud Identity Services, then the default mapping is the SAP SCIM attribute `userName` with the Microsoft Entra ID attribute `userPrincipalName`:

    ```powershell
    $db_match_column_name = "userName"
    $azuread_match_attr_name = "userPrincipalName"
    ```

    For another example if you are using a database or directory, you might have users in a database where the value in the column named `EMail` is the same value as in the Microsoft Entra attribute `userPrincipalName`:

    ```powershell
    $db_match_column_name = "EMail"
    $azuread_match_attr_name = "userPrincipalName"
    ```
7. Retrieve the IDs of those users in Microsoft Entra ID.

    The following PowerShell script uses the `$dbusers`, `$db_match_column_name`, and `$azuread_match_attr_name` values specified earlier. It will query Microsoft Entra ID to locate a user that has an attribute with a matching value for each record in the source file. If there are many users in the file obtained from the source SAP Cloud Identity Services, database, or directory, this script might take several minutes to finish. If you don't have an attribute in Microsoft Entra ID that has the value, and need to use a `contains` or other filter expression, then you will need to customize this script and that in step 11 below to use a different filter expression.

    ```powershell
    $dbu_not_queried_list = @()
    $dbu_not_matched_list = @()
    $dbu_match_ambiguous_list = @()
    $dbu_query_failed_list = @()
    $azuread_match_id_list = @()
    $azuread_not_enabled_list = @()
    $dbu_values = @()
    $dbu_duplicate_list = @()
    
    foreach ($dbu in $dbusers) { 
       if ($null -ne $dbu.$db_match_column_name -and $dbu.$db_match_column_name.Length -gt 0) { 
          $val = $dbu.$db_match_column_name
          $escval = $val -replace "'","''"
          if ($dbu_values -contains $escval) { $dbu_duplicate_list += $dbu; continue } else { $dbu_values += $escval }
          $filter = $azuread_match_attr_name + " eq '" + $escval + "'"
          try {
             $ul = @(Get-MgUser -Filter $filter -All -Property Id,accountEnabled -ErrorAction Stop)
             if ($ul.length -eq 0) { $dbu_not_matched_list += $dbu; } elseif ($ul.length -gt 1) {$dbu_match_ambiguous_list += $dbu } else {
                $id = $ul[0].id; 
                $azuread_match_id_list += $id;
                if ($ul[0].accountEnabled -eq $false) {$azuread_not_enabled_list += $id }
             } 
          } catch { $dbu_query_failed_list += $dbu } 
        } else { $dbu_not_queried_list += $dbu }
    }
    
    ```
8. View the results of the previous queries. See if any of the users in SAP Cloud Identity Services, the database, or directory couldn't be located in Microsoft Entra ID, because of errors or missing matches.

    The following PowerShell script will display the counts of records that weren't located:

    ```powershell
    $dbu_not_queried_count = $dbu_not_queried_list.Count
    if ($dbu_not_queried_count -ne 0) {
      Write-Error "Unable to query for $dbu_not_queried_count records as rows lacked values for $db_match_column_name."
    }
    $dbu_duplicate_count = $dbu_duplicate_list.Count
    if ($dbu_duplicate_count -ne 0) {
      Write-Error "Unable to locate Microsoft Entra ID users for $dbu_duplicate_count rows as multiple rows have the same value"
    }
    $dbu_not_matched_count = $dbu_not_matched_list.Count
    if ($dbu_not_matched_count -ne 0) {
      Write-Error "Unable to locate $dbu_not_matched_count records in Microsoft Entra ID by querying for $db_match_column_name values in $azuread_match_attr_name."
    }
    $dbu_match_ambiguous_count = $dbu_match_ambiguous_list.Count
    if ($dbu_match_ambiguous_count -ne 0) {
      Write-Error "Unable to locate $dbu_match_ambiguous_count records in Microsoft Entra ID as attribute match ambiguous."
    }
    $dbu_query_failed_count = $dbu_query_failed_list.Count
    if ($dbu_query_failed_count -ne 0) {
      Write-Error "Unable to locate $dbu_query_failed_count records in Microsoft Entra ID as queries returned errors."
    }
    $azuread_not_enabled_count = $azuread_not_enabled_list.Count
    if ($azuread_not_enabled_count -ne 0) {
     Write-Error "$azuread_not_enabled_count users in Microsoft Entra ID are blocked from sign-in."
    }
    if ($dbu_not_queried_count -ne 0 -or $dbu_duplicate_count -ne 0 -or $dbu_not_matched_count -ne 0 -or $dbu_match_ambiguous_count -ne 0 -or $dbu_query_failed_count -ne 0 -or $azuread_not_enabled_count) {
     Write-Output "You will need to resolve those issues before access of all existing users can be reviewed."
    }
    $azuread_match_count = $azuread_match_id_list.Count
    Write-Output "Users corresponding to $azuread_match_count records were located in Microsoft Entra ID." 
    ```
9. When the script finishes, it will indicate an error if any records from the data source weren't located in Microsoft Entra ID. If not all the records for users from the application's data store could be located as users in Microsoft Entra ID, you'll need to investigate which records didn't match and why.

    For example, someone's email address and userPrincipalName might have been changed in Microsoft Entra ID without their corresponding `mail` property being updated in the application's data source. Or, the user might have already left the organization but is still in the application's data source. Or there might be a vendor or super-admin account in the application's data source that does not correspond to any specific person in Microsoft Entra ID.
10. If there were users who couldn't be located in Microsoft Entra ID, or weren't active and able to sign in, but you want to have their access reviewed or their attributes updated in SAP Cloud Identity Services, the database, or directory, you'll need to update the application, the matching rule, or update or create Microsoft Entra users for them. For more information on which change to make, see [manage mappings and user accounts in applications that did not match to users in Microsoft Entra ID](../identity/app-provisioning/application-provisioning-application-unmatched-users).

    If you choose the option of creating users in Microsoft Entra ID, you can create users in bulk by using either:

    - A CSV file, as described in [Bulk create users in the Microsoft Entra admin center](../identity/users/users-bulk-add)
    - The [New-MgUser](/en-us/powershell/module/microsoft.graph.users/new-mguser?view=graph-powershell-1.0#examples&amp;preserve-view=true) cmdlet

    Ensure that these new users are populated with the attributes required for Microsoft Entra ID to later match them to the existing users in the application, and the attributes required by Microsoft Entra ID, including `userPrincipalName`, `mailNickname` and `displayName`. The `userPrincipalName` must be unique among all the users in the directory.

    For example, you might have users in a database where the value in the column named `EMail` is the value you want to use as the Microsoft Entra user principal Name, the value in the column `Alias` contains the Microsoft Entra ID mail nickname, and the value in the column `Full name` contains the user's display name:

    ```powershell
    $db_display_name_column_name = "Full name"
    $db_user_principal_name_column_name = "Email"
    $db_mail_nickname_column_name = "Alias"
    ```

    Then you can use this script to create Microsoft Entra users for those in SAP Cloud Identity Services, the database, or directory that didn't match with users in Microsoft Entra ID. Note that you may need to modify this script to add additional Microsoft Entra attributes needed in your organization, or if the `$azuread_match_attr_name` is neither `mailNickname` nor `userPrincipalName`, in order to supply that Microsoft Entra attribute.

    ```powershell
    $dbu_missing_columns_list = @()
    $dbu_creation_failed_list = @()
    foreach ($dbu in $dbu_not_matched_list) {
       if (($null -ne $dbu.$db_display_name_column_name -and $dbu.$db_display_name_column_name.Length -gt 0) -and
           ($null -ne $dbu.$db_user_principal_name_column_name -and $dbu.$db_user_principal_name_column_name.Length -gt 0) -and
           ($null -ne $dbu.$db_mail_nickname_column_name -and $dbu.$db_mail_nickname_column_name.Length -gt 0)) {
          $params = @{
             accountEnabled = $false
             displayName = $dbu.$db_display_name_column_name
             mailNickname = $dbu.$db_mail_nickname_column_name
             userPrincipalName = $dbu.$db_user_principal_name_column_name
             passwordProfile = @{
               Password = -join (((48..90) + (96..122)) * 16 | Get-Random -Count 16 | % {[char]$_})
             }
          }
          try {
            New-MgUser -BodyParameter $params
          } catch { $dbu_creation_failed_list += $dbu; throw }
       } else {
          $dbu_missing_columns_list += $dbu
       }
    }
    ```
11. After you add any missing users to Microsoft Entra ID, run the script from step 7 again. Then run the script from step 8. Check that no errors are reported.

    ```powershell
    $dbu_not_queried_list = @()
    $dbu_not_matched_list = @()
    $dbu_match_ambiguous_list = @()
    $dbu_query_failed_list = @()
    $azuread_match_id_list = @()
    $azuread_not_enabled_list = @()
    $dbu_values = @()
    $dbu_duplicate_list = @()
    
    foreach ($dbu in $dbusers) { 
       if ($null -ne $dbu.$db_match_column_name -and $dbu.$db_match_column_name.Length -gt 0) { 
          $val = $dbu.$db_match_column_name
          $escval = $val -replace "'","''"
          if ($dbu_values -contains $escval) { $dbu_duplicate_list += $dbu; continue } else { $dbu_values += $escval }
          $filter = $azuread_match_attr_name + " eq '" + $escval + "'"
          try {
             $ul = @(Get-MgUser -Filter $filter -All -Property Id,accountEnabled -ErrorAction Stop)
             if ($ul.length -eq 0) { $dbu_not_matched_list += $dbu; } elseif ($ul.length -gt 1) {$dbu_match_ambiguous_list += $dbu } else {
                $id = $ul[0].id; 
                $azuread_match_id_list += $id;
                if ($ul[0].accountEnabled -eq $false) {$azuread_not_enabled_list += $id }
             } 
          } catch { $dbu_query_failed_list += $dbu } 
        } else { $dbu_not_queried_list += $dbu }
    }
    
    $dbu_not_queried_count = $dbu_not_queried_list.Count
    if ($dbu_not_queried_count -ne 0) {
      Write-Error "Unable to query for $dbu_not_queried_count records as rows lacked values for $db_match_column_name."
    }
    $dbu_duplicate_count = $dbu_duplicate_list.Count
    if ($dbu_duplicate_count -ne 0) {
      Write-Error "Unable to locate Microsoft Entra ID users for $dbu_duplicate_count rows as multiple rows have the same value"
    }
    $dbu_not_matched_count = $dbu_not_matched_list.Count
    if ($dbu_not_matched_count -ne 0) {
      Write-Error "Unable to locate $dbu_not_matched_count records in Microsoft Entra ID by querying for $db_match_column_name values in $azuread_match_attr_name."
    }
    $dbu_match_ambiguous_count = $dbu_match_ambiguous_list.Count
    if ($dbu_match_ambiguous_count -ne 0) {
      Write-Error "Unable to locate $dbu_match_ambiguous_count records in Microsoft Entra ID as attribute match ambiguous."
    }
    $dbu_query_failed_count = $dbu_query_failed_list.Count
    if ($dbu_query_failed_count -ne 0) {
      Write-Error "Unable to locate $dbu_query_failed_count records in Microsoft Entra ID as queries returned errors."
    }
    $azuread_not_enabled_count = $azuread_not_enabled_list.Count
    if ($azuread_not_enabled_count -ne 0) {
     Write-Warning "$azuread_not_enabled_count users in Microsoft Entra ID are blocked from sign-in."
    }
    if ($dbu_not_queried_count -ne 0 -or $dbu_duplicate_count -ne 0 -or $dbu_not_matched_count -ne 0 -or $dbu_match_ambiguous_count -ne 0 -or $dbu_query_failed_count -ne 0 -or $azuread_not_enabled_count -ne 0) {
     Write-Output "You will need to resolve those issues before access of all existing users can be reviewed."
    }
    $azuread_match_count = $azuread_match_id_list.Count
    Write-Output "Users corresponding to $azuread_match_count records were located in Microsoft Entra ID." 
    ```

## Register the application

If the application is already registered in Microsoft Entra ID, then continue to the next step.

The account you're using must have permission to manage applications in Microsoft Entra ID. Any of the following Microsoft Entra roles include the required permissions:

- [Application Administrator](../identity/role-based-access-control/permissions-reference#application-administrator)
- [Application Developer](../identity/role-based-access-control/permissions-reference#application-developer)
- [Cloud Application Administrator](../identity/role-based-access-control/permissions-reference#cloud-application-administrator)

1. Create the application and service principal.

    For example, if the enterprise application is named `CORPDB1`, enter the following commands:

    ```powershell
    $azuread_app_name = "CORPDB1"
    $azuread_app = New-MgApplication -DisplayName $azuread_app_name
    $azuread_sp = New-MgServicePrincipal -DisplayName $azuread_app_name -AppId $azuread_app.AppId
    ```
2. Add a role to the application, and tag the application as integrated with Microsoft Entra ID so that its assignments can be reviewed. For example, if the role name is `General`, provide that value in the following PowerShell commands:

    ```powershell
    $ar0 = New-Object Microsoft.Graph.PowerShell.Models.MicrosoftGraphAppRole
    $ar0.AllowedMemberTypes += "User"
    $ar0.Description = "General role"
    $ar0.DisplayName = "General"
    $ar0.id = New-Guid
    $ar0.IsEnabled = $true
    $ar0.Value = "General"
    $ara = @()
    $ara += $ar0
    
    $azuread_app_tags = @()
    $azuread_app_tags += "WindowsAzureActiveDirectoryIntegratedApp"
    
    $azuread_app_update = Update-MgApplication -ApplicationId $azuread_app.Id -AppRoles $ara -Tags $azuread_app_tags
    ```

## Check for users who are not already assigned to the application

The previous steps have confirmed that all the users in the application's data store exist as users in Microsoft Entra ID. However, they might not all currently be assigned to the application's roles in Microsoft Entra ID. So the next steps are to see which users don't have assignments to application roles.

1. Look up the service principal ID for the application's service principal.

    For example, if the enterprise application is named `CORPDB1`, enter the following commands:

    ```powershell
    $azuread_app_name = "CORPDB1"
    $azuread_sp_filter = "displayName eq '" + ($azuread_app_name -replace "'","''") + "'"
    $azuread_sp = Get-MgServicePrincipal -Filter $azuread_sp_filter -All
    ```
2. Retrieve the users who currently have assignments to the application in Microsoft Entra ID.

    This builds upon the `$azuread_sp` variable set in the previous command.

    ```powershell
    $azuread_existing_assignments = @(Get-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $azuread_sp.Id -All)
    ```
3. Compare the list of user IDs from the previous section to those users currently assigned to the application:

    ```powershell
    $azuread_not_in_role_list = @()
    foreach ($id in $azuread_match_id_list) {
       $found = $false
       foreach ($existing in $azuread_existing_assignments) {
          if ($existing.principalId -eq $id) {
             $found = $true; break;
          }
       }
       if ($found -eq $false) { $azuread_not_in_role_list += $id }
    }
    $azuread_not_in_role_count = $azuread_not_in_role_list.Count
    Write-Output "$azuread_not_in_role_count users in the application's data store are not assigned to the application roles."
    ```

    If zero users are *not* assigned to application roles, indicating that all users *are* assigned to application roles, you don't need to make any further changes before performing an access review.

    However, if one or more users aren't currently assigned to the application roles, you'll need to continue the procedure and add them to one of the application's roles.
4. Select the role of the application to assign the remaining users to.

    An application might have more than one role. Use this command to list the available roles:

    ```powershell
    $azuread_sp.AppRoles | where-object {$_.AllowedMemberTypes -contains "User"} | ft DisplayName,Id
    ```

    Select the appropriate role from the list, and obtain its role ID. For example, if the role name is `General`, provide that value in the following PowerShell commands:

    ```powershell
    $azuread_app_role_name = "General"
    $azuread_app_role_id = ($azuread_sp.AppRoles | where-object {$_.AllowedMemberTypes -contains "User" -and $_.DisplayName -eq $azuread_app_role_name}).Id
    if ($null -eq $azuread_app_role_id) { write-error "role $azuread_app_role_name not located in application manifest"}
    ```

## Create app role assignments in Microsoft Entra ID

For Microsoft Entra ID to match the users in the application with the users in Microsoft Entra ID, you need to create application role assignments in Microsoft Entra ID.

When an application role assignment is created in Microsoft Entra ID for a user to an application, and the application does not support provisioning, then

- The user will remain in the application indefinitely unless they're updated outside Microsoft Entra ID, or until the assignment in Microsoft Entra ID is removed.
- On the next review of that application's role assignments, the user will be included in the review.
- If the user is denied in an access review, their application role assignment will be removed.

1. Create application role assignments for users who don't currently have role assignments:

    ```powershell
    foreach ($u in $azuread_not_in_role_list) {
       $res = New-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $azuread_sp.Id -AppRoleId $azuread_app_role_id -PrincipalId $u -ResourceId $azuread_sp.Id 
    }
    ```
2. Wait one minute for changes to propagate within Microsoft Entra ID.
3. Query Microsoft Entra ID to obtain the updated list of role assignments:

    ```powershell
    $azuread_existing_assignments = @(Get-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $azuread_sp.Id -All)
    ```
4. Compare the list of user IDs from the previous section to those users now assigned to the application:

    ```powershell
    $azuread_still_not_in_role_list = @()
    foreach ($id in $azuread_match_id_list) {
       $found = $false
       foreach ($existing in $azuread_existing_assignments) {
          if ($existing.principalId -eq $id) {
             $found = $true; break;
          }
       }
       if ($found -eq $false) { $azuread_still_not_in_role_list += $id }
    }
    $azuread_still_not_in_role_count = $azuread_still_not_in_role_list.Count
    if ($azuread_still_not_in_role_count -gt 0) {
       Write-Output "$azuread_still_not_in_role_count users in the application's data store are not assigned to the application roles."
    }
    ```

    If any users aren't assigned to application roles, check the Microsoft Entra audit log for an error from a previous step.

## Select appropriate reviewers

When you create each access review, administrators can choose one or more reviewers. The reviewers can carry out a review by choosing users for continued access to a resource or removing them.

Typically a resource owner is responsible for performing a review. If you're creating a review of a group, as part of reviewing access for an application integrated in pattern B, then you can select the group owners as reviewers. As applications in Microsoft Entra ID don't necessarily have an owner, the option for selecting the application owner as a reviewer isn't possible. Instead, when creating the review, you can supply the names of the application owners to be the reviewers.

You can also choose, when creating a review of a group or application, to have a [multi-stage review](create-access-review#create-a-multi-stage-access-review). For example, you could select to have the manager of each assigned user perform the first stage of the review, and the resource owner the second stage. That way the resource owner can focus on the users who have already been approved by their manager.

Before creating the reviews, check that you have sufficient Microsoft Entra ID P2 or Microsoft Entra ID Governance SKU seats in your tenant. Also, check that all reviewers are active users with email addresses. When the access reviews start, they each review an email from Microsoft Entra ID. If the reviewer doesn't have a mailbox, they will not receive the email when the review starts or an email reminder. And, if they are blocked from being able to sign in to Microsoft Entra ID, they will not be able to perform the review.

## Create the review of the application role assignments

Once the users are in the application roles, and you have the reviewers identified, then you can configure Microsoft Entra ID to [start a review](access-reviews-application-preparation#create-the-reviews).

Follow the instructions in the [guide for creating an access review of groups or applications](create-access-review), to create the review of the application's role assignments. Configure the review to apply results when it completes.

## Retrieve the assignments that are updated when the reviews are complete

1. When the review completes, you can retrieve the updated list of users with application role assignments.

    ```powershell
    $res = (Get-MgServicePrincipalAppRoleAssignedTo -ServicePrincipalId $azuread_sp.Id -All)
    ```
2. The columns `PrincipalDisplayName` and `PrincipalId` contain the display names and Microsoft Entra user IDs of each user who retains an application role assignment.

## Configure entitlement management integration with ServiceNow for ticketing (optional)

If you have ServiceNow, then you can optionally configure automated ServiceNow ticket creation, using the [entitlement management integration](entitlement-management-ticketed-provisioning) via Logic Apps. In that scenario, entitlement management can automatically create ServiceNow tickets for manual provisioning of users who have received access package assignments.