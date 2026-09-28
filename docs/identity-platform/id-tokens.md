---
layout: Conceptual
title: ID tokens in the Microsoft identity platform - Microsoft identity platform | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity-platform/id-tokens
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: /entra/identity-platform/developer-support-help-options
author: cilwerner
ms.author: cwerner
ms.service: identity-platform
description: Learn about ID tokens used in the Microsoft identity platform.
manager: pmwongera
ms.custom: 
ms.date: 2025-05-14T00:00:00.0000000Z
ms.reviewer: ludwignick
ms.topic: concept-article
locale: en-us
document_id: 39e50f53-203a-35d3-794f-73b27be0fde0
document_version_independent_id: f2af0873-d2ef-6df2-d3c2-8c953d392097
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity-platform/id-tokens.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-platform/id-tokens
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity-platform/id-tokens.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 3db47168-99d6-738f-ac29-3ba675d5a425
---

# ID tokens in the Microsoft identity platform - Microsoft identity platform | Microsoft Learn

ID tokens are a security token that serves as proof of authentication, confirming that a user is successfully authenticated. Information in ID tokens enables the client to verify that a user is who they claim to be, similar to name tags at a conference. The authorization server issues ID tokens that contain claims that carry information about the user. They can be sent alongside or instead of an access token, and are always JWT (JSON Web Token) format.

ID tokens differ from [access tokens](access-tokens), which serve as proof of authorization. Confidential clients should validate ID tokens. You shouldn't use an ID token to call an API.

Third-party applications are intended to understand ID tokens. Do not use ID tokens for authorization purposes. Access tokens are used for authorization. The claims provided by ID tokens can be used for UX inside your application, as keys in a database, and providing access to the client application. For more information about the claims used in an ID token, see the [ID token claims reference](id-token-claims-reference). For more information about claims-based authorization, see [Secure applications and APIs by validating claims](claims-validation).

## Token formats

There are two versions of ID tokens available in the Microsoft identity platform: v1.0 and v2.0. These versions determine the claims that are in the token. The v1.0 and v2.0 ID tokens have differences in the information they carry. The version is based on the endpoint from where it was requested. New applications should use the v2.0.

- v1.0: `https://login.microsoftonline.com/common/oauth2/authorize`
- v2.0: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize`

### Sample v1.0 ID token

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjdfWnVmMXR2a3dMeFlhSFMzcTZsVWpVWUlHdyIsImtpZCI6IjdfWnVmMXR2a3dMeFlhSFMzcTZsVWpVWUlHdyJ9.eyJhdWQiOiJiMTRhNzUwNS05NmU5LTQ5MjctOTFlOC0wNjAxZDBmYzljYWEiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC9mYTE1ZDY5Mi1lOWM3LTQ0NjAtYTc0My0yOWYyOTU2ZmQ0MjkvIiwiaWF0IjoxNTM2Mjc1MTI0LCJuYmYiOjE1MzYyNzUxMjQsImV4cCI6MTUzNjI3OTAyNCwiYWlvIjoiQVhRQWkvOElBQUFBcXhzdUIrUjREMnJGUXFPRVRPNFlkWGJMRDlrWjh4ZlhhZGVBTTBRMk5rTlQ1aXpmZzN1d2JXU1hodVNTajZVVDVoeTJENldxQXBCNWpLQTZaZ1o5ay9TVTI3dVY5Y2V0WGZMT3RwTnR0Z2s1RGNCdGsrTExzdHovSmcrZ1lSbXY5YlVVNFhscGhUYzZDODZKbWoxRkN3PT0iLCJhbXIiOlsicnNhIl0sImVtYWlsIjoiYWJlbGlAbWljcm9zb2Z0LmNvbSIsImZhbWlseV9uYW1lIjoiTGluY29sbiIsImdpdmVuX25hbWUiOiJBYmUiLCJpZHAiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDcvIiwiaXBhZGRyIjoiMTMxLjEwNy4yMjIuMjIiLCJuYW1lIjoiYWJlbGkiLCJub25jZSI6IjEyMzUyMyIsIm9pZCI6IjA1ODMzYjZiLWFhMWQtNDJkNC05ZWMwLTFiMmJiOTE5NDQzOCIsInJoIjoiSSIsInN1YiI6IjVfSjlyU3NzOC1qdnRfSWN1NnVlUk5MOHhYYjhMRjRGc2dfS29vQzJSSlEiLCJ0aWQiOiJmYTE1ZDY5Mi1lOWM3LTQ0NjAtYTc0My0yOWYyOTU2ZmQ0MjkiLCJ1bmlxdWVfbmFtZSI6IkFiZUxpQG1pY3Jvc29mdC5jb20iLCJ1dGkiOiJMeGVfNDZHcVRrT3BHU2ZUbG40RUFBIiwidmVyIjoiMS4wIn0=.UJQrCA6qn2bXq57qzGX_-D3HcPHqBMOKDPx4su1yKRLNErVD8xkxJLNLVRdASHqEcpyDctbdHccu6DPpkq5f0ibcaQFhejQNcABidJCTz0Bb2AbdUCTqAzdt9pdgQvMBnVH1xk3SCM6d4BbT4BkLLj10ZLasX7vRknaSjE_C5DI7Fg4WrZPwOhII1dB0HEZ_qpNaYXEiy-o94UJ94zCr07GgrqMsfYQqFR7kn-mn68AjvLcgwSfZvyR_yIK75S_K37vC3QryQ7cNoafDe9upql_6pB2ybMVlgWPs_DmbJ8g0om-sPlwyn74Cc1tW3ze-Xptw_2uVdPgWyqfuWAfq6Q
```

View this v1.0 sample token in [jwt.ms](https://jwt.ms/#id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjdfWnVmMXR2a3dMeFlhSFMzcTZsVWpVWUlHdyIsImtpZCI6IjdfWnVmMXR2a3dMeFlhSFMzcTZsVWpVWUlHdyJ9.eyJhdWQiOiJiMTRhNzUwNS05NmU5LTQ5MjctOTFlOC0wNjAxZDBmYzljYWEiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC9mYTE1ZDY5Mi1lOWM3LTQ0NjAtYTc0My0yOWYyOTU2ZmQ0MjkvIiwiaWF0IjoxNTM2Mjc1MTI0LCJuYmYiOjE1MzYyNzUxMjQsImV4cCI6MTUzNjI3OTAyNCwiYWlvIjoiQVhRQWkvOElBQUFBcXhzdUIrUjREMnJGUXFPRVRPNFlkWGJMRDlrWjh4ZlhhZGVBTTBRMk5rTlQ1aXpmZzN1d2JXU1hodVNTajZVVDVoeTJENldxQXBCNWpLQTZaZ1o5ay9TVTI3dVY5Y2V0WGZMT3RwTnR0Z2s1RGNCdGsrTExzdHovSmcrZ1lSbXY5YlVVNFhscGhUYzZDODZKbWoxRkN3PT0iLCJhbXIiOlsicnNhIl0sImVtYWlsIjoiYWJlbGlAbWljcm9zb2Z0LmNvbSIsImZhbWlseV9uYW1lIjoiTGluY29sbiIsImdpdmVuX25hbWUiOiJBYmUiLCJpZHAiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDcvIiwiaXBhZGRyIjoiMTMxLjEwNy4yMjIuMjIiLCJuYW1lIjoiYWJlbGkiLCJub25jZSI6IjEyMzUyMyIsIm9pZCI6IjA1ODMzYjZiLWFhMWQtNDJkNC05ZWMwLTFiMmJiOTE5NDQzOCIsInJoIjoiSSIsInN1YiI6IjVfSjlyU3NzOC1qdnRfSWN1NnVlUk5MOHhYYjhMRjRGc2dfS29vQzJSSlEiLCJ0aWQiOiJmYTE1ZDY5Mi1lOWM3LTQ0NjAtYTc0My0yOWYyOTU2ZmQ0MjkiLCJ1bmlxdWVfbmFtZSI6IkFiZUxpQG1pY3Jvc29mdC5jb20iLCJ1dGkiOiJMeGVfNDZHcVRrT3BHU2ZUbG40RUFBIiwidmVyIjoiMS4wIn0=.UJQrCA6qn2bXq57qzGX_-D3HcPHqBMOKDPx4su1yKRLNErVD8xkxJLNLVRdASHqEcpyDctbdHccu6DPpkq5f0ibcaQFhejQNcABidJCTz0Bb2AbdUCTqAzdt9pdgQvMBnVH1xk3SCM6d4BbT4BkLLj10ZLasX7vRknaSjE_C5DI7Fg4WrZPwOhII1dB0HEZ_qpNaYXEiy-o94UJ94zCr07GgrqMsfYQqFR7kn-mn68AjvLcgwSfZvyR_yIK75S_K37vC3QryQ7cNoafDe9upql_6pB2ybMVlgWPs_DmbJ8g0om-sPlwyn74Cc1tW3ze-Xptw_2uVdPgWyqfuWAfq6Q).

### Sample v2.0 ID token

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IjFMVE16YWtpaGlSbGFfOHoyQkVKVlhlV01xbyJ9.eyJ2ZXIiOiIyLjAiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vOTEyMjA0MGQtNmM2Ny00YzViLWIxMTItMzZhMzA0YjY2ZGFkL3YyLjAiLCJzdWIiOiJBQUFBQUFBQUFBQUFBQUFBQUFBQUFJa3pxRlZyU2FTYUZIeTc4MmJidGFRIiwiYXVkIjoiNmNiMDQwMTgtYTNmNS00NmE3LWI5OTUtOTQwYzc4ZjVhZWYzIiwiZXhwIjoxNTM2MzYxNDExLCJpYXQiOjE1MzYyNzQ3MTEsIm5iZiI6MTUzNjI3NDcxMSwibmFtZSI6IkFiZSBMaW5jb2xuIiwicHJlZmVycmVkX3VzZXJuYW1lIjoiQWJlTGlAbWljcm9zb2Z0LmNvbSIsIm9pZCI6IjAwMDAwMDAwLTAwMDAtMDAwMC02NmYzLTMzMzJlY2E3ZWE4MSIsInRpZCI6IjkxMjIwNDBkLTZjNjctNGM1Yi1iMTEyLTM2YTMwNGI2NmRhZCIsIm5vbmNlIjoiMTIzNTIzIiwiYWlvIjoiRGYyVVZYTDFpeCFsTUNXTVNPSkJjRmF0emNHZnZGR2hqS3Y4cTVnMHg3MzJkUjVNQjVCaXN2R1FPN1lXQnlqZDhpUURMcSFlR2JJRGFreXA1bW5PcmNkcUhlWVNubHRlcFFtUnA2QUlaOGpZIn0.1AFWW-Ck5nROwSlltm7GzZvDwUkqvhSQpm55TQsmVo9Y59cLhRXpvB8n-55HCr9Z6G_31_UbeUkoz612I2j_Sm9FFShSDDjoaLQr54CreGIJvjtmS3EkK9a7SJBbcpL1MpUtlfygow39tFjY7EVNW9plWUvRrTgVk7lYLprvfzw-CIqw3gHC-T7IK_m_xkr08INERBtaecwhTeN4chPC4W3jdmw_lIxzC48YoQ0dB1L9-ImX98Egypfrlbm0IBL5spFzL6JDZIRRJOu8vecJvj1mq-IUhGt0MacxX8jdxYLP-KUu2d9MbNKpCKJuZ7p8gwTL5B7NlUdh_dmSviPWrw
```

View this v2.0 sample token in [jwt.ms](https://jwt.ms/#id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IjFMVE16YWtpaGlSbGFfOHoyQkVKVlhlV01xbyJ9.eyJ2ZXIiOiIyLjAiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vOTEyMjA0MGQtNmM2Ny00YzViLWIxMTItMzZhMzA0YjY2ZGFkL3YyLjAiLCJzdWIiOiJBQUFBQUFBQUFBQUFBQUFBQUFBQUFJa3pxRlZyU2FTYUZIeTc4MmJidGFRIiwiYXVkIjoiNmNiMDQwMTgtYTNmNS00NmE3LWI5OTUtOTQwYzc4ZjVhZWYzIiwiZXhwIjoxNTM2MzYxNDExLCJpYXQiOjE1MzYyNzQ3MTEsIm5iZiI6MTUzNjI3NDcxMSwibmFtZSI6IkFiZSBMaW5jb2xuIiwicHJlZmVycmVkX3VzZXJuYW1lIjoiQWJlTGlAbWljcm9zb2Z0LmNvbSIsIm9pZCI6IjAwMDAwMDAwLTAwMDAtMDAwMC02NmYzLTMzMzJlY2E3ZWE4MSIsInRpZCI6IjkxMjIwNDBkLTZjNjctNGM1Yi1iMTEyLTM2YTMwNGI2NmRhZCIsIm5vbmNlIjoiMTIzNTIzIiwiYWlvIjoiRGYyVVZYTDFpeCFsTUNXTVNPSkJjRmF0emNHZnZGR2hqS3Y4cTVnMHg3MzJkUjVNQjVCaXN2R1FPN1lXQnlqZDhpUURMcSFlR2JJRGFreXA1bW5PcmNkcUhlWVNubHRlcFFtUnA2QUlaOGpZIn0.1AFWW-Ck5nROwSlltm7GzZvDwUkqvhSQpm55TQsmVo9Y59cLhRXpvB8n-55HCr9Z6G_31_UbeUkoz612I2j_Sm9FFShSDDjoaLQr54CreGIJvjtmS3EkK9a7SJBbcpL1MpUtlfygow39tFjY7EVNW9plWUvRrTgVk7lYLprvfzw-CIqw3gHC-T7IK_m_xkr08INERBtaecwhTeN4chPC4W3jdmw_lIxzC48YoQ0dB1L9-ImX98Egypfrlbm0IBL5spFzL6JDZIRRJOu8vecJvj1mq-IUhGt0MacxX8jdxYLP-KUu2d9MbNKpCKJuZ7p8gwTL5B7NlUdh_dmSviPWrw).

## Token lifetime

By default, an ID token is valid for one hour - after one hour, the client must acquire a new ID token.

You can adjust the lifetime of an ID token to control how often the client application expires the application session, and how often it requires the user to authenticate again either silently or interactively. For more information, read [Configurable token lifetimes](configurable-token-lifetimes).

## Validate tokens

To validate an ID token, your client can check whether the token has been tampered with. It can also validate the issuer to ensure that the correct issuer has sent back the token. Because ID tokens are always a JWT token, many libraries exist to validate these tokens - you should use one of these libraries rather than doing it yourself. Only confidential clients should validate ID tokens. For more information, see [Secure applications and APIs by validating claims](claims-validation).

Public applications (code running entirely on a device or network you don't control such as a user's browser or their home network) don't benefit from validating the ID token. In this instance, a malicious user can intercept and edit the keys used for validation of the token.

The following JWT claims should be validated in the ID token after validating the signature on the token. Your token validation library may also validate the following claims:

- Timestamps: the `iat`, `nbf`, and `exp` timestamps should all fall before or after the current time, as appropriate.
- Audience: the `aud` claim should match the app ID for your application.
- Nonce: the `nonce` claim in the payload must match the nonce parameter passed into the `/authorize` endpoint during the initial request.