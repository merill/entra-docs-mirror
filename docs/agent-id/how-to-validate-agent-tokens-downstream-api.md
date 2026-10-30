---
layout: Conceptual
title: Validate agent identity tokens in a downstream API - Microsoft Entra Agent ID | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/agent-id/how-to-validate-agent-tokens-downstream-api
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
author: Dickson-Mwendia
ms.author: dmwendia
ms.service: entra-id
ms.subservice: agent-id
manager: pmwongera
description: Learn how to validate Microsoft Entra Agent ID tokens in a downstream API by checking the signature, issuer, audience, and agent identity marker claim.
ms.topic: how-to
ms.date: 2026-04-28T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: 079c1e26-95fd-ebda-f4d9-a7c2ba0d9858
document_version_independent_id: 079c1e26-95fd-ebda-f4d9-a7c2ba0d9858
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/agent-id/how-to-validate-agent-tokens-downstream-api.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: agent-id/how-to-validate-agent-tokens-downstream-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/agent-id/how-to-validate-agent-tokens-downstream-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 85c48139-649b-f3b2-5910-89c47000e685
---

# Validate agent identity tokens in a downstream API - Microsoft Entra Agent ID | Microsoft Learn

When an AI agent calls your API through the Microsoft Entra ID Auth SDK (sidecar), the request includes a `Bearer` token. Your API validates this token to confirm the request comes from an authenticated agent with the correct permissions. If validation fails, your API returns HTTP 401 with a reason.

This article explains the validation checks and shows how to configure and run a sample weather API that validates agent identity tokens end-to-end.

## Prerequisites

- **Docker Desktop** (macOS / Windows) or **Docker Engine** (Linux).
- A **Microsoft Entra tenant** with an agent identity blueprint and an agent identity. For setup steps, see [Create an agent blueprint](create-blueprint) and [Create and delete agent identities](create-delete-agent-identities).
- An agent identity token for testing. You can get one from the [sidecar local development sample](sidecar-local-development) or from the scripts in the [Microsoft Entra Agent ID samples repository](https://github.com/microsoft/entra-agentid-samples).

## Token validation checks

Your downstream API should perform four checks on every incoming agent identity token:

| Check | What it verifies | Details |
| --- | --- | --- |
| **Signature** | The token isn't tampered with. | Verify the RS256 signature against the JSON Web Key Set (JWKS) at `https://login.microsoftonline.com/<tenant>/discovery/v2.0/keys`. |
| **Issuer** | Microsoft Entra ID issued the token. | The `iss` claim matches `https://sts.windows.net/<tenant>/` or `https://login.microsoftonline.com/<tenant>/v2.0`. |
| **Audience** | The token is intended for your API. | The `aud` claim matches your API's expected audience value. |
| **Agent identity marker** | The token was issued to an agent, not a regular app. | The `xms_par_app_azp` claim is present in agent identity tokens and absent in standard app-only tokens. This claim identifies the blueprint that created the agent. |

When all four checks pass, your API can trust and process the request.

## How the sample weather API works

The [Microsoft Entra Agent ID samples repository](https://github.com/microsoft/entra-agentid-samples) includes a sample weather API that demonstrates these validation checks. The sample API is a minimal Flask app that acts as the downstream API your agent calls. It validates incoming agent identity tokens and returns real weather data from [Open-Meteo](https://open-meteo.com).

Both the [local development (Ollama)](sidecar-local-development) and AWS (Bedrock) sidecar samples call the same weather API container. The sample consists of three files:

- **`app.py`:** Flask app with route handlers, token validation logic, and Open-Meteo client.
- **`Dockerfile`:** Uses `python:3.13-slim` as the base image. Runs `gunicorn app:app` on port 8080.
- **`requirements.txt`:** Dependencies: `flask`, `pyjwt[crypto]`, `cryptography`, `requests`, `gunicorn`.

The API exposes two endpoints:

- **`GET /weather?city=<name>`:** Validates the `Authorization: Bearer <token>` header and returns weather data for the specified city.
- **`GET /healthz`:** Returns a health status without requiring token validation.

The following diagram shows how tokens flow from the agent through the sidecar to the weather API. The agent never contacts Microsoft Entra ID directly. Instead, the sidecar acquires a token (TR) on behalf of the agent identity, and the agent passes that token to the weather API in the `Authorization: Bearer` header.

[![Diagram showing the agent caller sending a Bearer token to the weather API, which verifies the token and calls Open-Meteo.](media/how-to-validate-agent-tokens-downstream-api/agent-token-flow-to-downstream-api.png)](media/how-to-validate-agent-tokens-downstream-api/agent-token-flow-to-downstream-api.png#lightbox)

The agent identity token, TR, is issued by Microsoft Entra ID through the sidecar. It contains the claims your API validates, including the `xms_par_app_azp` agent identity marker. For a detailed breakdown of all tokens in the flow, see [Run the sidecar for local development](sidecar-local-development#understand-the-token-flow).

Token validation libraries differ across ecosystems (Python, Node.js, .NET). This sample uses PyJWT with the `cryptography` backend for RS256 signature verification. When you build your own downstream API, choose the equivalent JWT validation library for your technology stack.

## Configure the sample weather API

The sample weather API accepts the following environment variables:

| Variable | Required | Default | Purpose |
| --- | --- | --- | --- |
| `TENANT_ID` | Yes | — | Your Microsoft Entra tenant ID, used to build the JWKS URL and verify the issuer claim. |
| `EXPECTED_AUDIENCE` | No | `https://graph.microsoft.com` | The expected `aud` claim value. Defaults to Microsoft Graph so that the same agent tokens work for local testing. |
| `PORT` | No | `8080` | The HTTP port the API listens on. |

## Run the sample weather API

To run the weather API as a standalone container and test token validation:

1. Clone the repository and navigate to the weather API directory:

    ```bash
    git clone https://github.com/microsoft/entra-agentid-samples.git
    cd entra-agentid-samples/sidecar/weather-api
    ```
2. Build and run the container:

    ```bash
    docker build -t weather-api:local .
    docker run --rm -p 8080:8080 \
      -e TENANT_ID=<your-tenant-id> \
      -e EXPECTED_AUDIENCE=https://graph.microsoft.com \
      weather-api:local
    ```
3. Send a request with an agent identity token:

    ```bash
    curl -H "Authorization: Bearer $TOKEN" \
         "http://localhost:8080/weather?city=Dallas"
    ```

The API returns a JSON response that includes both the weather data and the token validation results:

```json
{
  "city": "Dallas",
  "temperature": 61,
  "temperature_unit": "F",
  "condition": "Overcast",
  "humidity": 93,
  "wind_speed": 8,
  "is_agent_identity": true,
  "agent_app_id": "<agent-app-id from xms_par_app_azp>",
  "validated_by": "Agent Identity Token",
  "data_source": "Open-Meteo API (Real-time)"
}
```

The `is_agent_identity`, `agent_app_id`, and `validated_by` fields confirm token validation:

- **`is_agent_identity`:** Set to `true` when the `xms_par_app_azp` claim is present, which confirms the token was issued to an agent identity rather than a standard app registration.
- **`agent_app_id`:** The value of the `xms_par_app_azp` claim, which identifies the blueprint application that created the agent identity.
- **`validated_by`:** The validation method applied to the token. Displays `Agent Identity Token` when the agent marker claim is present.