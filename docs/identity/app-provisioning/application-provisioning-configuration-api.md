---
layout: Conceptual
title: Configure provisioning using Microsoft Graph APIs - Microsoft Entra ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/app-provisioning/application-provisioning-configuration-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: jenniferf-skc
ms.author: jfields
ms.service: entra-id
ms.subservice: app-provisioning
manager: dougeby
description: Learn how to save time by using the Microsoft Graph APIs to automate the configuration of automatic provisioning.
ms.topic: how-to
ms.date: 2025-03-04T00:00:00.0000000Z
ms.reviewer: arvinh
ai-usage: ai-assisted
locale: en-us
document_id: a675e37f-4cb0-81ef-995a-871ebd7b3ecb
document_version_independent_id: e3c547d9-f59b-5798-56d3-b8692e36c7d0
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/app-provisioning/application-provisioning-configuration-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
interactive_type: msgraph
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/app-provisioning/application-provisioning-configuration-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/app-provisioning/application-provisioning-configuration-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 00a59bbc-de5a-4b36-66bb-9951afdfa27d
---

# Configure provisioning using Microsoft Graph APIs - Microsoft Entra ID | Microsoft Learn

The Microsoft Entra admin center is a convenient way to configure provisioning for individual apps one at a time. But if you're creating several—or even hundreds—of instances of an application, or migrating application configuration from one environment to another, it can be easier to automate app creation and configuration with the Microsoft Graph APIs. This article outlines how to automate provisioning configuration through APIs. This method is commonly used for applications like [Amazon Web Services](../saas-apps/amazon-web-service-tutorial#configure-azure-ad-sso).

This article illustrates the process with APIs in the [Microsoft Graph beta endpoint](/en-us/graph/api/overview?view=graph-rest-beta&amp;preserve-view=true) and Microsoft Graph Explorer; similar APIs are also available in the [Microsoft Graph v1.0 endpoint](/en-us/graph/api/overview?view=graph-rest-1.0&amp;preserve-view=true). For an example of configuring provisioning with Graph v1.0 and PowerShell, see steps 6-13 of [Configure cross-tenant synchronization using PowerShell or Microsoft Graph API](../multi-tenant-organizations/cross-tenant-synchronization-configure-graph?tabs=ms-powershell).

**Overview of steps for using Microsoft Graph APIs to automate provisioning configuration**

| Step | Details |
| --- | --- |
| Step 1. Create the gallery application | Sign-in to the API client  Retrieve the gallery application template  Create the gallery application |
| Step 2. Create provisioning job based on template | Retrieve the template for the provisioning connector  Create the provisioning job |
| Step 3. Authorize access | Test the connection to the application  Save the credentials |
| Step 4. Start provisioning job | Start the job |
| Step 5. Monitor provisioning | Check the status of the provisioning job  Retrieve the provisioning logs |

If you are provisioning to an on-premises application, then you will also need to install and configure the provisioning agent, and assign the provisioning agent to the application.

## Step 1: Create the gallery application

### Sign in to Microsoft Graph Explorer (recommended), or any other API client you use

1. Start [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Select the "Sign-In with Microsoft" button and sign in with a user with the [Application Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#application-administrator) role.
3. Upon successful sign-in, you'll see the user account details in the left-hand pane.

### Retrieve the gallery application template identifier

Applications in the Microsoft Entra application gallery each have an [application template](/en-us/graph/api/applicationtemplate-list?tabs=http&amp;view=graph-rest-beta&amp;preserve-view=true) that describes the metadata for that application. Using this template, you can create an instance of the application and service principal in your tenant for management. Retrieve the identifier of the application template for **AWS Single-Account Access** and from the response, record the value of the **id** property to use later in this tutorial.

#### Request

```msgraph
GET https://graph.microsoft.com/beta/applicationTemplates?$filter=displayName eq 'AWS Single-Account Access'
```

#### Response

```http
HTTP/1.1 200 OK
Content-type: application/json

{
  "value": [
  {
    "id": "8b1025e4-1dd2-430b-a150-2ef79cd700f5",
        "displayName": "AWS Single-Account Access",
        "homePageUrl": "http://aws.amazon.com/",
        "supportedSingleSignOnModes": [
             "password",
             "saml",
             "external"
         ],
         "supportedProvisioningTypes": [
             "sync"
         ],
         "logoUrl": "https://az495088.vo.msecnd.net/app-logo/aws_215.png",
         "categories": [
             "developerServices"
         ],
         "publisher": "Amazon",
         "description": "Federate to a single AWS account and use SAML claims to authorize access to AWS IAM roles. If you have many AWS accounts, consider using the AWS Single Sign-On gallery application instead."    

}
```

### Create the gallery application

Use the template ID retrieved for your application in the last step to [create an instance](/en-us/graph/api/applicationtemplate-instantiate?tabs=http&amp;view=graph-rest-beta&amp;preserve-view=true) of the application and service principal in your tenant.

#### Request

```msgraph
POST https://graph.microsoft.com/beta/applicationTemplates/{applicationTemplateId}/instantiate
Content-type: application/json

{
  "displayName": "AWS Contoso"
}
```

#### Response

```http
HTTP/1.1 201 OK
Content-type: application/json

{
    "application": {
        "objectId": "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
        "appId": "00001111-aaaa-2222-bbbb-3333cccc4444",
        "applicationTemplateId": "8b1025e4-1dd2-430b-a150-2ef79cd700f5",
        "displayName": "AWS Contoso",
        "homepage": "https://signin.aws.amazon.com/saml?metadata=aws|ISV9.1|primary|z",
        "replyUrls": [
            "https://signin.aws.amazon.com/saml"
        ],
        "logoutUrl": null,
        "samlMetadataUrl": null,
    },
    "servicePrincipal": {
        "objectId": "bbbbbbbb-1111-2222-3333-cccccccccccc",
        "appDisplayName": "AWS Contoso",
        "applicationTemplateId": "8b1025e4-1dd2-430b-a150-2ef79cd700f5",
        "appRoleAssignmentRequired": true,
        "displayName": "My custom name",
        "homepage": "https://signin.aws.amazon.com/saml?metadata=aws|ISV9.1|primary|z",
        "replyUrls": [
            "https://signin.aws.amazon.com/saml"
        ],
        "servicePrincipalNames": [
            "93653dd4-aa3a-4323-80cf-e8cfefcc8d7d"
        ],
        "tags": [
            "WindowsAzureActiveDirectoryIntegratedApp"
        ],
    }
}
```

## Step 2: Create the provisioning job based on the template

### Retrieve the template for the provisioning connector

Applications in the gallery that are enabled for provisioning have templates to streamline configuration. Use the request below to [retrieve the template for the provisioning configuration](/en-us/graph/api/synchronization-synchronization-list-templates?preserve-view=true&amp;tabs=http&amp;view=graph-rest-beta). Note that you will need to provide the ID. The ID is that of the servicePrincipal resource, created in the preceding step.

#### Request

```msgraph
GET https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/templates
```

#### Response

```http
HTTP/1.1 200 OK

{
    "value": [
        {
            "id": "aws",
            "factoryTag": "aws",
            "schema": {
                    "directories": [],
                    "synchronizationRules": []
                    }
        }
    ]
}
```

### Create the provisioning job

To enable provisioning, you'll first need to [create a job](/en-us/graph/api/synchronization-synchronization-post-jobs?preserve-view=true&amp;tabs=http&amp;view=graph-rest-beta). Use the following request to create a provisioning job. Use the templateId from the previous step when specifying the template to be used for the job.

#### Request

```msgraph
POST https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs
Content-type: application/json

{ 
    "templateId": "aws"
}
```

#### Response

```http
HTTP/1.1 201 OK
Content-type: application/json

{
    "id": "{jobId}",
    "templateId": "aws",
    "schedule": {
        "expiration": null,
        "interval": "P10675199DT2H48M5.4775807S",
        "state": "Disabled"
    },
    "status": {
        "countSuccessiveCompleteFailures": 0,
        "escrowsPruned": false,
        "synchronizedEntryCountByType": [],
        "code": "NotConfigured",
        "lastExecution": null,
        "lastSuccessfulExecution": null,
        "lastSuccessfulExecutionWithExports": null,
        "steadyStateFirstAchievedTime": "0001-01-01T00:00:00Z",
        "steadyStateLastAchievedTime": "0001-01-01T00:00:00Z",
        "quarantine": null,
        "troubleshootingUrl": null
    }
}
```

## Step 3: Authorize access

### Test the connection to the application

Test the connection with the third-party application. The following example is for an application that requires a client secret and secret token. Each application has its own requirements. Applications often use a base address in place of a client secret. To determine what credentials your app requires, go to the provisioning configuration page for your application, and in developer mode, click **test connection**. The network traffic will show the parameters used for credentials. For a full list of credentials, see [synchronizationJob: validateCredentials](/en-us/graph/api/synchronization-synchronizationjob-validatecredentials?tabs=http&amp;view=graph-rest-beta&amp;preserve-view=true). Most applications, such as Azure Databricks, rely on a BaseAddress and SecretToken. The BaseAddress is referred to as a tenant URL in the Microsoft Entra admin center.

#### Request

```msgraph
POST https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs/{jobId}/validateCredentials

{ 
    "credentials": [ 
        { 
            "key": "ClientSecret", "value": "xxxxxxxxxxxxxxxxxxxxx" 
        },
        {
            "key": "SecretToken", "value": "xxxxxxxxxxxxxxxxxxxxx"
        }
    ]
}
```

#### Response

```http
HTTP/1.1 204 No Content
```

### Save your credentials

Configuring provisioning requires establishing a trust between Microsoft Entra ID and the application to authorize Microsoft Entra to have the ability to call the third-party application. The following example is specific to an application that requires a client secret and a secret token. Each application has its own requirements. Review the [API documentation](/en-us/graph/api/synchronization-synchronizationjob-validatecredentials?tabs=http&amp;view=graph-rest-beta&amp;preserve-view=true) to see the available options.

#### Request

```msgraph
PUT https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/secrets 

{ 
    "value": [ 
        { 
            "key": "ClientSecret", "value": "xxxxxxxxxxxxxxxxxxxxx"
        },
        {
            "key": "SecretToken", "value": "xxxxxxxxxxxxxxxxxxxxx"
        }
    ]
}
```

#### Response

```http
HTTP/1.1 204 No Content
```

## Step 4: Start the provisioning job

Now that the provisioning job is configured, use the following command to [start the job](/en-us/graph/api/synchronization-synchronizationjob-start?tabs=http&amp;view=graph-rest-beta&amp;preserve-view=true).

#### Request

```http
POST https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs/{jobId}/start
```

#### Response

```http
HTTP/1.1 204 No Content
```

## Step 5: Monitor provisioning

### Monitor the provisioning job status

Now that the provisioning job is running, use the following command to track the progress. Each [synchronization job](/en-us/graph/api/resources/synchronization-synchronizationjob) in the response includes the [status](/en-us/graph/api/resources/synchronization-synchronizationstatus) of the current provisioning cycle as well as statistics to date such as the number of users and groups that have been created in the target system.

#### Request

```msgraph
GET https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs
```

#### Response

```http
HTTP/1.1 200 OK
Content-type: application/json

{ "value": [
{
    "id": "{jobId}",
    "templateId": "aws",
    "schedule": {
        "expiration": null,
        "interval": "P10675199DT2H48M5.4775807S",
        "state": "Disabled"
    },
    "status": {
        "countSuccessiveCompleteFailures": 0,
        "escrowsPruned": false,
        "synchronizedEntryCountByType": [],
        "code": "Paused",
        "lastExecution": null,
        "lastSuccessfulExecution": null,
        "progress": [],
        "lastSuccessfulExecutionWithExports": null,
        "steadyStateFirstAchievedTime": "0001-01-01T00:00:00Z",
        "steadyStateLastAchievedTime": "0001-01-01T00:00:00Z",
        "quarantine": null,
        "troubleshootingUrl": null
    },
    "synchronizationJobSettings": [
      {
          "name": "QuarantineTooManyDeletesThreshold",
          "value": "500"
      }
    ]
}
]
}
```

### Monitor provisioning events using the provisioning logs

In addition to monitoring the status of the provisioning job, you can use the [provisioning logs](/en-us/graph/api/provisioningobjectsummary-list?tabs=http&amp;view=graph-rest-beta&amp;preserve-view=true) to query for all the events that are occurring. For example, query for a particular user and determine if they were successfully provisioned.

#### Request

```msgraph
GET https://graph.microsoft.com/beta/auditLogs/provisioning
```

#### Response

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#auditLogs/provisioning",
    "value": [
        {
            "id": "gc532ff9-r265-ec76-861e-42e2970a8218",
            "activityDateTime": "2019-06-24T20:53:08Z",
            "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee",
            "cycleId": "44576n58-v14b-70fj-8404-3d22tt46ed93",
            "changeId": "eaad2f8b-e6e3-409b-83bd-e4e2e57177d5",
            "action": "Create",
            "durationInMilliseconds": 2785,
            "sourceSystem": {
                "id": "0404601d-a9c0-4ec7-bbcd-02660120d8c9",
                "displayName": "Azure Active Directory",
                "details": {}
            },
            "targetSystem": {
                "id": "cd22f60b-5f2d-1adg-adb4-76ef31db996b",
                "displayName": "AWS Contoso",
                "details": {
                    "ApplicationId": "00001111-aaaa-2222-bbbb-3333cccc4444",
                    "ServicePrincipalId": "aaaaaaaa-bbbb-cccc-1111-222222222222",
                    "ServicePrincipalDisplayName": "AWS Contoso"
                }
            },
            "initiatedBy": {
                "id": "",
                "displayName": "Azure AD Provisioning Service",
                "initiatorType": "system"
            }
            ]
       }
    ]
}
```