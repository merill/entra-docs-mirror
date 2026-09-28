---
layout: Conceptual
title: 'Quickstart: Add sign in to a Python Flask web app - Microsoft Entra External ID | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/entra/external-id/customers/web-app-quickstart-portal-python-flask-ciam
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://aka.ms/microsoftentraexternalid
author: csmulligan
ms.author: cmulligan
ms.service: entra-external-id
ms.subservice: external
manager: dougeby
description: Learn how to run a sample Python Flask web app to sign in users
ms.custom: devx-track-python
ROBOTS: NOINDEX
ms.topic: concept-article
ms.date: 2024-04-24T00:00:00.0000000Z
locale: en-us
document_id: a61a20d5-4f94-7ef7-4d6a-05ff8bc1fd4c
document_version_independent_id: a61a20d5-4f94-7ef7-4d6a-05ff8bc1fd4c
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/external-id/customers/web-app-quickstart-portal-python-flask-ciam.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-id/customers/web-app-quickstart-portal-python-flask-ciam
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/external-id/customers/web-app-quickstart-portal-python-flask-ciam.md
platformId: 90c2bba3-fafa-aa9b-6595-f973dce08c40
---

# Quickstart: Add sign in to a Python Flask web app - Microsoft Entra External ID | Microsoft Learn

> 
> In this quickstart, you download and run a code sample that demonstrates how a Python Flask web app can sign in users with Microsoft Entra External ID.

1. Make sure you've installed [Python 3+](https://www.python.org/).
2. Unzip the sample app.
3. In your terminal, navigate to the root directory of the app then run the following command to install dependencies:

    ```console
    pip install -r requirements.txt
    ```
4. In your terminal, run the following command to start the app:

    ```console
    flask run -h localhost -p 5000
    ```
5. Open your browser, visit `http://localhost:5000`, select **Sign-in**, then follow the prompts.