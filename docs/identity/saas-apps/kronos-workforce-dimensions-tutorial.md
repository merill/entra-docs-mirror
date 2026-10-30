---
layout: Conceptual
title: Configure Kronos Workforce Dimensions for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/saas-apps/kronos-workforce-dimensions-tutorial
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jeevansd
ms.author: jeedes
ms.reviewer: jomondi
ms.service: entra-id
ms.subservice: saas-apps
manager: pmwongera
description: Learn how to configure single sign-on between Microsoft Entra ID and Kronos Workforce Dimensions.
ms.topic: how-to
ms.date: 2026-06-04T00:00:00.0000000Z
locale: en-us
document_id: 562ab326-ecac-34de-66e2-d021d0ce2684
document_version_independent_id: daa805e5-2a0e-b012-4524-20e025ed9861
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/saas-apps/kronos-workforce-dimensions-tutorial.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/saas-apps/kronos-workforce-dimensions-tutorial
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/saas-apps/kronos-workforce-dimensions-tutorial.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 66b32c1d-0973-c7d1-0090-e6e48a418b77
---

# Configure Kronos Workforce Dimensions for Single sign-on with Microsoft Entra ID - Microsoft Entra ID | Microsoft Learn

In this article, you learn how to integrate Kronos Workforce Dimensions with Microsoft Entra ID. When you integrate Kronos Workforce Dimensions with Microsoft Entra ID, you can:

- Control in Microsoft Entra ID who has access to Kronos Workforce Dimensions.
- Enable your users to be automatically signed-in to Kronos Workforce Dimensions with their Microsoft Entra accounts.
- Manage your accounts in one central location.

Kronos Workforce Dimensions is available in the following [national cloud deployments](/en-us/graph/deployments).

| Global service | US Government | China operated by 21Vianet |
| --- | --- | --- |
| ✅ | ✅ |  |

## Prerequisites

The scenario outlined in this article assumes that you already have the following prerequisites:

- A Microsoft Entra user account with an active subscription. If you don't already have one, you can [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- One of the following roles:
    - [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator)
    - [Cloud Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#cloud-application-administrator)
    - [Application Owner](/en-us/entra/fundamentals/users-default-permissions#owned-enterprise-applications).

- Kronos Workforce Dimensions single sign-on (SSO) enabled subscription.

## Scenario description

In this article, you configure and test Microsoft Entra SSO in a test environment.

- Kronos Workforce Dimensions supports **SP** initiated SSO.

## Add Kronos Workforce Dimensions from the gallery

To configure the integration of Kronos Workforce Dimensions into Microsoft Entra ID, you need to add Kronos Workforce Dimensions from the gallery to your list of managed SaaS apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **New application**.
3. In the **Add from the gallery** section, type **Kronos Workforce Dimensions** in the search box.
4. Select **Kronos Workforce Dimensions** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, and walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/en-us/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Microsoft Entra SSO for Kronos Workforce Dimensions

Configure and test Microsoft Entra SSO with Kronos Workforce Dimensions using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between a Microsoft Entra user and the related user in Kronos Workforce Dimensions.

To configure and test Microsoft Entra SSO with Kronos Workforce Dimensions, perform the following steps:

1. **Configure Microsoft Entra SSO**- to enable your users to use this feature.
    1. **Create a Microsoft Entra test user** - to test Microsoft Entra single sign-on with B.Simon.
    2. **Assign the Microsoft Entra test user** - to enable B.Simon to use Microsoft Entra single sign-on.
2. **Configure Kronos Workforce Dimensions SSO**- to configure the single sign-on settings on application side.
    1. **Create Kronos Workforce Dimensions test user** - to have a counterpart of B.Simon in Kronos Workforce Dimensions that's linked to the Microsoft Entra representation of user.
3. **Test SSO** - to verify whether the configuration works.

## Configure Microsoft Entra SSO

Follow these steps to enable Microsoft Entra SSO.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Cloud Application Administrator](../role-based-access-control/permissions-reference#cloud-application-administrator).
2. Browse to **Entra ID** &gt; **Enterprise apps** &gt; **Kronos Workforce Dimensions** &gt; **Single sign-on**.
3. On the **Select a single sign-on method** page, select **SAML**.
4. On the **Set up single sign-on with SAML** page, select the pencil icon for **Basic SAML Configuration** to edit the settings.

    ![Screenshot shows how to edit Basic SAML Configuration.](common/edit-urls.png)
5. On the **Basic SAML Configuration** section, perform the following steps:

    a. In the **Identifier (Entity ID)** text box, type a URL using the following pattern: `https://<SUBDOMAIN>.<ENVIRONMENT>.mykronos.com/authn/<TENANT_ID/hsp/<TENANT_NUMBER>`

    b. In the **Sign on URL** text box, type a URL using one of the following patterns:

    | **Sign on URL** |
    | --- |
    | `https://<CUSTOMER>-<ENVIRONMENT>-sso.<ENVIRONMENT>.mykronos.com/` |
    | `https://<CUSTOMER>-sso.<ENVIRONMENT>.mykronos.com/` |

    Note

    These values aren't real. Update these values with the actual Identifier and Sign on URL. Contact [Kronos Workforce Dimensions Client support team](mailto:support@kronos.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section.
6. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, select copy button to copy **App Federation Metadata Url** and save it on your computer.

    ![Screenshot shows the Certificate download link.](common/copy-metadataurl.png)

### Create and assign Microsoft Entra test user

Follow the guidelines in the [create and assign a user account](../enterprise-apps/add-application-portal-assign-users) quickstart to create a test user account called B.Simon.

## Configure Kronos Workforce Dimensions SSO

To configure single sign-on on **Kronos Workforce Dimensions** side, you need to send the **App Federation Metadata Url** to [Kronos Workforce Dimensions support team](mailto:support@kronos.com). They set this setting to have the SAML SSO connection set properly on both sides.

## Create Kronos Workforce Dimensions test user

In this section, you create a user called Britta Simon in Kronos Workforce Dimensions. Work with [Kronos Workforce Dimensions support team](mailto:support@kronos.com) to add the users in the Kronos Workforce Dimensions platform. Users must be created and activated before you use single sign-on.

Note

Original Microsoft documentation advises to contact UKG Support via email to create your Microsoft Entra users. While this option is available please consider the following self-service options.

### Manual Process

There are two ways to manually create your Microsoft Entra users in WFD. You can either select an existing user, duplicate them and then update the necessary fields to make that user unique. This process can be time consuming and requires knowledge of the WFD User Interface. The alternative is to create the user via the WFD API which is much quicker. This option requires knowledge of using API Tools such as Postman to send the request to the API instead. The following instructions will assist with importing a prebuilt example into the Postman API Tool.

#### Setup

1. Open Postman tool and import the following files:

    a. Workforce Dimensions - Create User.postman\_collection.json

    b. Microsoft Entra ID to WFD Env Variables.json
2. In the left-pane, select the **Environments** button.
3. Select **AAD\_to\_WFD\_Env\_Variables** and add the values provided by UKG Support pertaining to your WFD instance.

    Note

    access\_token and refresh\_token should be empty as these will automatically populate as a result of the Obtain Access Token HTTP Request.
4. Open the **Create Microsoft Entra user in WFD** HTTP Request and update highlighted properties within the JSON payload:

    ```
    { 
    
    "personInformation": { 
    
       "accessAssignment": { 
    
          "accessProfileName": "accessProfileName", 
    
          "notificationProfileName": "All" 
    
        }, 
    
        "emailAddresses": [ 
    
          { 
    
            "address": "address” 
    
            "contactTypeName": "Work" 
    
          } 
    
        ], 
    
        "employmentStatusList": [ 
    
          { 
    
            "effectiveDate": "2019-08-15", 
    
            "employmentStatusName": "Active", 
    
            "expirationDate": "3000-01-01" 
    
          } 
    
        ], 
    
        "person": { 
    
          "personNumber": "personNumber", 
    
          "firstName": "firstName", 
    
          "lastName": "lastName", 
    
          "fullName": "fullName", 
    
          "hireDate": "2019-08-15", 
    
          "shortName": "shortName" 
    
        }, 
    
        "personAuthenticationTypes": [ 
    
          { 
    
            "activeFlag": true, 
    
            "authenticationTypeName": "Federated" 
    
          } 
    
        ], 
    
        "personLicenseTypes": [ 
    
          { 
    
            "activeFlag": true, 
    
            "licenseTypeName": "Employee" 
    
          }, 
    
          { 
    
            "activeFlag": true, 
    
            "licenseTypeName": "Absence" 
    
          }, 
    
          { 
    
            "activeFlag": true, 
    
            "licenseTypeName": "Hourly Timekeeping" 
    
          }, 
    
          { 
    
            "activeFlag": true, 
    
            "licenseTypeName": "Scheduling" 
    
          } 
    
        ], 
    
        "userAccountStatusList": [ 
    
          { 
    
            "effectiveDate": "2019-08-15", 
    
            "expirationDate": "3000-01-01", 
    
            "userAccountStatusName": "Active" 
    
          } 
    
        ] 
    
      }, 
    
      "jobAssignment": { 
    
        "baseWageRates": [ 
    
          { 
    
            "effectiveDate": "2019-01-01", 
    
            "expirationDate": "3000-01-01", 
    
            "hourlyRate": 20.15 
    
          } 
    
        ], 
    
        "jobAssignmentDetails": { 
    
          "payRuleName": "payRuleName", 
    
          "timeZoneName": "timeZoneName" 
    
        }, 
    
        "primaryLaborAccounts": [ 
    
          { 
    
            "effectiveDate": "2019-08-15", 
    
            "expirationDate": "3000-01-01", 
    
            "organizationPath": "organizationPath" 
    
          } 
    
        ] 
    
      }, 
    
      "user": { 
    
        "userAccount": { 
    
          "logonProfileName": "Default", 
    
          "userName": "userName" 
    
        } 
    
      } 
    
    }
    ```

    Note

    The personInformation.emailAddress.address and the user.userAccount.userName must both match the targeted Microsoft Entra user you're trying to create in WFD.
5. In the upper-righthand corner, select the **Environments** drop-down-box and select **AAD\_to\_WFD\_Env\_Variables**.
6. Once the JSON payload has been updated and the correct environment variables selected, select the **Obtain Access Token** HTTP Request and select the **Send** button. This will leverage the updated environment variables to authenticate to your WFD instance and then cache your access token in the environment variables to use when calling the create user method.
7. If the authentication call was successful, you should see a 200 response with an access token returned. This access token will also now show in the **CURRENT VALUE** column in the environment variables for the **access\_token** entry.

    Note

    If an access\_token isn't received, confirm that all variables in the environment variables are correct. User credentials should be a super user account.
8. Once an **access\_token** is obtained, select the **AAD\_to\_WFD\_Env\_Variables** HTTP Request and select the **Send** button. If the request is successful you receive a 200 HTTP status back.
9. Login to WFD with the **Super User** account and confirm the new Microsoft Entra user was created within the WFD instance.

### Automated Process

The automated process consists of a flat-file in CSV format which allows the user to prespecify the highlighted values in the payload from the manual API process above. The flat-file is consumed by the accompanying PowerShell script which creates the new WFD users in bulk. The script processes new user creations in batches of 70 (default) which is configurable for optimal performance. The following instructions will walk through the setup and execution of the script.

1. Save both the **AAD\_To\_WFD.csv** and **AAD\_To\_WFD.ps1** files locally to your computer.
2. Open the **AAD\_To\_WFD.csv** file and fill in the columns.

    - **personInformation.accessAssignment.accessProfileName**: Specific Access Profile Name from WFD instance.
    - **personInformation.emailAddresses.address**: Must match the User Principle Name in Microsoft Entra ID.
    - **personInformation.personNumber**: Must be unique across the WFD instance.
    - **personInformation.firstName**: User’s first name.
    - **personInformation.lastName**: User’s last name.
    - **jobAssignment.jobAssignmentDetails.payRuleName**: Specific Pay Rule Name from WFD.
    - **jobAssignment.jobAssignmentDetails.timeZoneName**: Timezone format must match WFD instance (that is, `(GMT -08:00) Pacific Time`).
    - **jobAssignment.primaryLaborAccounts.organizationPath**: Organization Path of a specific Business structure in the WFD instance.
3. Save the .csv file.
4. Right-Select the **AAD\_To\_WFD.ps1** script and select **Edit** to modify it.
5. Confirm the path specified in Line 15 is the correct name/path to the **AAD\_To\_WFD.csv** file.
6. Update the following lines with the values provided by UKG Support pertaining to your WFD instance.

    - Line 33: vanityUrl
    - Line 43: appKey
    - Line 48: client\_id
    - Line 49: client\_secret
7. Save and execute the script.
8. Provide WFD **Super User** credentials when prompted.
9. Once completed, the script will return a list of any users that failed to create.

Note

Be sure to check the values provided in the AAD\_To\_WFD.csv file if it's returned as the result of typos or mismatched fields in the WFD instance. The error could also be returned by the WFD API instance if all users in the batch already exist in the instance.

## Test SSO

In this section, you test your Microsoft Entra single sign-on configuration with following options.

- Select **Test this application**, this option redirects to Kronos Workforce Dimensions Sign-on URL where you can initiate the login flow.
- Go to Kronos Workforce Dimensions Sign-on URL directly and initiate the login flow from there.
- You can use Microsoft My Apps. When you select the Kronos Workforce Dimensions tile in the My Apps, this option redirects to Kronos Workforce Dimensions Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).