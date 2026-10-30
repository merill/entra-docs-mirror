---
layout: Conceptual
title: Learn about Microsoft Authentication Extensions for Node - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/msal-node-extensions
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: The Microsoft Authentication Extensions for Node enables application developers to perform cross-platform token cache serialization and persistence. It gives extra support to the Microsoft Authentication Library for Node (MSAL Node).
manager: pmwongera
ms.date: 2022-02-04T00:00:00.0000000Z
ms.reviewer: emilylauber
ms.topic: concept-article
locale: en-us
document_id: 5e67722f-114a-354f-22c0-f42c74a4e5ac
document_version_independent_id: 896c1bb9-deac-3217-c04b-195f381ec7a8
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/msal-node-extensions.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/msal-node-extensions
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/msal-node-extensions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5f286262-a4cb-47f4-92d3-dc24f172492b
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e31b9be-b6e9-4221-a20b-d1460dbd5dfa
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90571f66-8410-4272-8117-79ce87fc2dcc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8d63a4c4-4889-43b4-a98e-8e50dbfdb083
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 5aa3e374-a376-5bc0-46f7-0438251a0f9d
---

# Learn about Microsoft Authentication Extensions for Node - Microsoft identity platform | Microsoft Learn

The Microsoft Authentication Extensions for Node enables developers to perform cross-platform token cache serialization and persistence to disk. It gives extra support to the Microsoft Authentication Library (MSAL) for Node.

The [MSAL for Node](tutorial-v2-nodejs-webapp-msal) supports an in-memory cache by default and provides the ICachePlugin interface to perform cache serialization, but doesn't provide a default way of storing the token cache to disk. The Microsoft Authentication Extensions for Node is the default implementation for persisting cache to disk across different platforms.

The Microsoft Authentication Extensions for Node support the following platforms:

- Windows - Data protection API (DPAPI) is used for protection.
- Mac - The Mac Keychain is used.
- Linux - LibSecret is used for storing to "Secret Service".

## Installation

The `msal-node-extensions` package is available on Node Package Manager (NPM).

```bash
npm i @azure/msal-node-extensions --save
```

## Configure the token cache

Here's an example of code that uses Microsoft Authentication Extensions for Node to configure the token cache.

```javascript
const {
  DataProtectionScope,
  Environment,
  PersistenceCreator,
  PersistenceCachePlugin,
} = require("@azure/msal-node-extensions");

// You can use the helper functions provided through the Environment class to construct your cache path
// The helper functions provide consistent implementations across Windows, Mac and Linux.
const cachePath = path.join(Environment.getUserRootDirectory(), "./cache.json");

const persistenceConfiguration = {
  cachePath,
  dataProtectionScope: DataProtectionScope.CurrentUser,
  serviceName: "<SERVICE-NAME>",
  accountName: "<ACCOUNT-NAME>",
  usePlaintextFileOnLinux: false,
};

// The PersistenceCreator obfuscates a lot of the complexity by doing the following actions for you :-
// 1. Detects the environment the application is running on and initializes the right persistence instance for the environment.
// 2. Performs persistence validation for you.
// 3. Performs any fallbacks if necessary.
PersistenceCreator.createPersistence(persistenceConfiguration).then(
  async (persistence) => {
    const publicClientConfig = {
      auth: {
        clientId: "<CLIENT-ID>",
        authority: "<AUTHORITY>",
      },

      // This hooks up the cross-platform cache into MSAL
      cache: {
        cachePlugin: new PersistenceCachePlugin(persistence),
      },
    };

    const pca = new msal.PublicClientApplication(publicClientConfig);

    // Use the public client application as required...
  }
);
```

The following table provides an explanation for all the arguments for the persistence configuration.

| Field Name | Description | Required For |
| --- | --- | --- |
| cachePath | The path to the lock file the library uses to synchronize the reads and the writes | Windows, Mac, and Linux |
| dataProtectionScope | Specifies the scope of the data protection on Windows either the current user or the local machine. | Windows |
| serviceName | Specifies the service name to be used on Mac and/or Linux | Mac and Linux |
| accountName | Specifies the account name to be used on Mac and/or Linux | Mac and Linux |
| usePlaintextFileOnLinux | The flag to default to plain text on linux if LibSecret fails. Defaults to `false` | Linux |