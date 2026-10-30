---
layout: Conceptual
title: What are custom security attributes in Microsoft Entra ID? - Microsoft Entra | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: kenwith
ms.author: kenwith
ms.service: entra
ms.subservice: fundamentals
manager: dougeby
description: Learn about custom security attributes in Microsoft Entra ID.
ms.topic: concept-article
ms.date: 2024-10-28T00:00:00.0000000Z
ms.collection: M365-identity-device-management
locale: en-us
document_id: 2896aa11-53c5-722b-aabf-e59dda55cf38
document_version_independent_id: 7291a3a0-24d6-0e88-9105-29001f7e3ed1
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/fundamentals/custom-security-attributes-overview.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: fundamentals/custom-security-attributes-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/fundamentals/custom-security-attributes-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: a723c886-1c44-d3b6-b55d-a98cc36bf02a
---

# What are custom security attributes in Microsoft Entra ID? - Microsoft Entra | Microsoft Learn

Custom security attributes in Microsoft Entra ID are business-specific attributes (key-value pairs) that you can define and assign to Microsoft Entra objects. These attributes can be used to store information, categorize objects, or enforce fine-grained access control over specific Azure resources. Custom security attributes can be used with [Azure attribute-based access control (ABAC)](/en-us/azure/role-based-access-control/conditions-overview).

## Why use custom security attributes?

Here are some scenarios where you could use custom security attributes:

- Extend user profiles, such as add Hourly Salary to all my employees.
- Ensure only administrators can see the Hourly Salary attribute in my employees' profiles.
- Categorize hundreds or thousands of applications to easily create a filterable inventory for auditing.
- Grant users access to the Azure Storage blobs belonging to a project.

## What can I do with custom security attributes?

Custom security attributes include these capabilities:

- Define business-specific information (attributes) for your tenant.
- Add a set of custom security attributes on users and applications.
- Manage Microsoft Entra objects using custom security attributes with queries and filters.
- Provide attribute governance so attributes determine who can get access.

Custom security attributes **aren't** supported in the following areas:

- [Microsoft Entra Domain Services](/en-us/entra/identity/domain-services/overview)
- [Security Assertion Markup Language (SAML) token claims](../identity-platform/saml-claims-customization)
- [JSON Web Token claims](/en-us/entra/identity-platform/security-tokens)

## Features of custom security attributes

Custom security attributes include these features:

- Available tenant-wide
- Include a description
- Support different data types: Boolean, integer, string
- Support single value or multiple values
- Support user-defined free-form values or predefined values
- Assign custom security attributes to directory synced users from an on-premises Active Directory

The following example shows several custom security attributes assigned to a user. The custom security attributes are different data types and have values that are single, multiple, free-form, or predefined.

[![Screenshot of custom security attribute examples assigned to a user.](media/custom-security-attributes-overview/attribute-values-examples.png)](media/custom-security-attributes-overview/attribute-values-examples.png#lightbox)

## Objects that support custom security attributes

You can add custom security attributes for the following Microsoft Entra objects:

- Microsoft Entra users
- Microsoft Entra enterprise applications (service principals)

## How do custom security attributes compare with extensions?

While both extensions and custom security attributes can be used to extend objects in Microsoft Entra ID and Microsoft 365, they are suitable for fundamentally different custom data scenarios. Here are some ways that custom security attributes compare with [extensions](/en-us/graph/extensibility-overview):

| Capability | Extensions | Custom security attributes |
| --- | --- | --- |
| Extend Microsoft Entra ID and Microsoft 365 objects | Yes | Yes |
| Supported objects | Depends on the extension type | Users and service principals |
| Restricted access | No. Anyone with permissions to read the object can read the extension data. | Yes. Read and write access is restricted through a separate set of permissions and role-based access control (RBAC). |
| When to use | Store data to be used by an application  Store non-sensitive data | Store sensitive data  Use for authorization scenarios |
| License requirements | Available in all editions of Microsoft Entra ID | Available in all editions of Microsoft Entra ID |

For more information about working with extensions, see [Add custom data to resources using extensions](/en-us/graph/extensibility-overview).

## Steps to use custom security attributes

1. **Check permissions**

    Check that you are assigned the [Attribute Definition Administrator](../identity/role-based-access-control/permissions-reference#attribute-definition-administrator) or [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) roles. If necessary, someone with at least the [Privileged Role Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#privileged-role-administrator) role can assign these roles.

    ![Diagram showing checking permissions to add custom security attributes in Microsoft Entra ID.](media/custom-security-attributes-overview/attributes-permissions.png)
2. **Add attribute sets**

    Add attribute sets to group and manage related custom security attributes. [Learn more](custom-security-attributes-add)

    ![Diagram showing adding multiple attribute sets.](media/custom-security-attributes-overview/attribute-sets.png)
3. **Manage attribute sets**

    Specify who can read, define, or assign custom security attributes in an attribute set. [Learn more](custom-security-attributes-manage)

    ![Diagram showing assigning attribute definition administrators and attribute assignment administrators to attribute sets.](media/custom-security-attributes-overview/delegate-attribute-sets-manage.png)
4. **Define attributes**

    Add your custom security attributes to your directory. You can specify the date type (Boolean, integer, or string) and whether values are predefined, free-form, single, or multiple. [Learn more](custom-security-attributes-add)

    ![Diagram showing delegated administrators defining custom security attributes.](media/custom-security-attributes-overview/delegate-attributes-define.png)
5. **Assign attributes**

    Assign custom security attributes to Microsoft Entra objects for your business scenarios. [Learn more](../identity/users/users-custom-security-attributes)

    ![Diagram showing delegated administrators assigning custom security attributes to Microsoft Entra objects.](media/custom-security-attributes-overview/delegate-attributes-assign.png)
6. **Use attributes**

    Filter users and applications that use custom security attributes. [Learn more](../identity/users/users-custom-security-attributes)

    Add conditions that use custom security attributes to Azure role assignments for fine-grained access control. [Learn more](/en-us/azure/role-based-access-control/conditions-custom-security-attributes)

## Terminology

To better understand custom security attributes, you can refer back to the following list of terms.

| Term | Definition |
| --- | --- |
| attribute definition | The schema of a custom security attribute or key-value pair. For example, the custom security attribute name, description, data type, and predefined values. |
| attribute set | A collection of related custom security attributes. Attribute sets can be delegated to other users for defining and assigning custom security attributes. |
| attribute name | A unique name of a custom security attribute within an attribute set. The combination of attribute set and attribute name forms a unique attribute for your tenant. |
| attribute assignment | The assignment of a custom security attribute to a Microsoft Entra object, such as users and enterprise applications (service principals). |
| predefined value | A value that is allowed for a custom security attribute. |

## Custom security attribute properties

The following table lists the properties you can specify for attribute sets and custom security attributes. Some properties are immutable and cannot be changed later.

| Property | Required | Can be changed later | Description |
| --- | --- | --- | --- |
| Attribute set name | ✅ |  | Name of the attribute set. Must be unique within a tenant. Cannot include spaces or special characters. |
| Attribute set description |  | ✅ | Description of the attribute set. |
| Maximum number of attributes |  | ✅ | Maximum number of custom security attributes that can be defined in an attribute set. Default value is `null`. If not specified, the administrator can add up to the maximum of 500 active attributes per tenant. |
| Attribute set | ✅ |  | A collection of related custom security attributes. Every custom security attribute must be part of an attribute set. |
| Attribute name | ✅ |  | Name of the custom security attribute. Must be unique within an attribute set. Cannot include spaces or special characters. |
| Attribute description |  | ✅ | Description of the custom security attribute. |
| Data type | ✅ |  | Data type for the custom security attribute values. Supported types are `Boolean`, `Integer`, and `String`. |
| Allow multiple values to be assigned | ✅ |  | Indicates whether multiple values can be assigned to the custom security attribute. If data type is set to `Boolean`, cannot be set to Yes. |
| Only allow predefined values to be assigned | ✅ |  | Indicates whether only predefined values can be assigned to the custom security attribute. If set to No, free-form values are allowed. Can later be changed from Yes to No, but cannot be changed from No to Yes. If data type is set to `Boolean`, cannot be set to Yes. |
| Predefined values |  |  | Predefined values for the custom security attribute of the selected data type. More predefined values can be added later. Values can include spaces, but some special characters are not allowed. |
| Predefined value is active |  | ✅ | Specifies whether the predefined value is active or deactivated. If set to false, the predefined value cannot be assigned to any additional supported directory objects. |
| Attribute is active |  | ✅ | Specifies whether the custom security attribute is active or deactivated. |

## Limits and constraints

Here are some of the limits and constraints for custom security attributes.

| Resource | Limit | Notes |
| --- | --- | --- |
| Attribute definitions per tenant | 500 | Applies only to active attributes in the tenant |
| Attribute sets per tenant | 500 |  |
| Attribute set name length | 32 | Unicode characters and case sensitive |
| Attribute set description length | 128 | Unicode characters |
| Attribute name length | 32 | Unicode characters and case sensitive |
| Attribute description length | 128 | Unicode characters |
| Predefined values |  | Unicode characters and case sensitive |
| Predefined values per attribute definition | 100 |  |
| Attribute value length | 64 | Unicode characters |
| Attribute values assigned per object | 50 | Values can be distributed across single and multivalued attributes.Example: 5 attributes with 10 values each or 50 attributes with 1 value each |
| Special characters **not** allowed for:Attribute set nameAttribute name | `<space> ` ~ ! @ # $ % ^ & * ( ) _ - + = { [ } ] \| \ : ; " ' < , > . ? /` | Attribute set name and attribute name cannot start with a number |
| Special characters allowed for attribute values | All special characters |  |
| Special characters allowed for attribute values when used with blob index tags | `<space> + - . : = _ /` | If you plan to use [attribute values with blob index tags](/en-us/azure/role-based-access-control/conditions-custom-security-attributes), these are the only special characters allowed for blob index tags. For more information, see [Setting blob index tags](/en-us/azure/storage/blobs/storage-manage-find-blobs#setting-blob-index-tags). |

## Custom security attribute roles

Microsoft Entra ID provides built-in roles to work with custom security attributes. The Attribute Definition Administrator role is the minimum role you need to manage custom security attributes. The Attribute Assignment Administrator role is the minimum role you need to assign custom security attribute values for Microsoft Entra objects like users and applications. You can assign these roles at tenant scope or at attribute set scope.

| Role | Permissions |
| --- | --- |
| [Attribute Definition Reader](../identity/role-based-access-control/permissions-reference#attribute-definition-reader) | Read attribute setsRead custom security attribute definitions |
| [Attribute Definition Administrator](../identity/role-based-access-control/permissions-reference#attribute-definition-administrator) | Manage all aspects of attribute setsManage all aspects of custom security attribute definitions |
| [Attribute Assignment Reader](../identity/role-based-access-control/permissions-reference#attribute-assignment-reader) | Read attribute setsRead custom security attribute definitionsRead custom security attribute keys and values for users and service principals |
| [Attribute Assignment Administrator](../identity/role-based-access-control/permissions-reference#attribute-assignment-administrator) | Read attribute setsRead custom security attribute definitionsRead and update custom security attribute keys and values for users and service principals |
| [Attribute Log Reader](../identity/role-based-access-control/permissions-reference#attribute-log-reader) | Read audit logs for custom security attributes |
| [Attribute Log Administrator](../identity/role-based-access-control/permissions-reference#attribute-log-administrator) | Read audit logs for custom security attributesConfigure diagnostic settings for custom security attributes |

Important

By default, [Global Administrator](../identity/role-based-access-control/permissions-reference#global-administrator) and other administrator roles do not have permissions to read, define, or assign custom security attributes.

## Microsoft Graph API

You can manage custom security attributes programmatically using Microsoft Graph API. For more information, see [Overview of custom security attributes using the Microsoft Graph API](/en-us/graph/api/resources/custom-security-attributes-overview).

You can use an API client such as [Graph Explorer](/en-us/graph/graph-explorer/graph-explorer-overview) to more easily try the Microsoft Graph API for custom security attributes.

![Screenshot that shows a Microsoft Graph API call for custom security attributes.](media/custom-security-attributes-overview/graph-explorer-success.png)

## License requirements

Using this feature is free and included in your Azure subscription.