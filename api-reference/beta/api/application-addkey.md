---
title: "application: addKey"
description: "Adds a strong password to an application."
localization_priority: Normal
author: "sureshja"
ms.prod: ""
doc_type: "apiPageType"
---

# application: addPasswordKey

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Adds a key to an application.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged) |
|:---------------------------------------|:--------------------------------------------|
| Delegated (work or school account)     | Directory.AccessAsUser.All |
| Delegated (personal Microsoft account) | Not supported. |
| Application                            | Application.ReadWrite.OwnedBy, Application.ReadWrite.All |

## HTTP request

<!-- { "blockType": "ignored" } -->

```http
POST /applications/{id}/addKey
```

## Request headers

| Name           | Type   | Description                |
|:---------------|:-------|:---------------------------|
| Authorization  | string | Bearer {token}. Required.  |

## Request body

In the request body, provide an optional `keyCredential` property as a JSON object with the following parameters.

| Property	   | Type	|Description|
|:---------------|:--------|:----------|
| `displayName` | String | Optional; Friendly name for passwords |
| `endDateTime` | DateTimeOffset | Optional; The date and time at which the password expires.The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 would look like this: `'2014-01-01T00:00:00Z'` |
| `startDateTime` | DateTimeOffset | Optional; The date and time at which the password becomes valid.The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 would look like this: `'2014-01-01T00:00:00Z'` |

## Response

If successful, this method returns `200, OK` response code and a new [keyCredential](../resources/keycredential.md) object in the response body.

## Examples

The following is an example of how to call this API.

### Request

The following is an example of the request.
<!-- {
  "blockType": "request",
  "name": "application_addkey"
}-->

```http
POST https://graph.microsoft.com/beta/applications/{id}/addKey
Content-type: application/json

{
  "keyCredential": {
    "customKeyIdentifier": "6uv7gh",
    "endDate": "endDate=2017-10-11T07:00:00Z",
    "keyId": "633b1614-b669-47c5-961e-f4a45978ffff",
    "type": "AsymmetricX509Cert",
    "usage": "Verify",
    "value": null
  }
}
```

### Response

The following is an example of the response.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.keyCredential"
} -->

```http
HTTP/1.1 200 OK
Content-type: application/json
{
  "keyCredential": {
    "customKeyIdentifier": "6uv7gh",
    "type": "AsymmetricX509Cert",
    "usage": "Verify",
    "value": "MIZB9jVCACfEw="
  }
}
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "application: addKey",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->