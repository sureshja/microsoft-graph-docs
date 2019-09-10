---
title: "application: addPassword"
description: "Adds a strong password to an application."
localization_priority: Normal
author: "sureshja"
ms.prod: ""
doc_type: "apiPageType"
---

# application: addPassword

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Adds a strong password to an application.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged) |
|:---------------------------------------|:--------------------------------------------|
| Delegated (work or school account)     | Directory.Read.All, Directory.ReadWrite.All, Directory.AccessAsUser.All |
| Delegated (personal Microsoft account) | Not supported. |
| Application                            | Application.ReadWrite.OwnedBy, Application.ReadWrite.All, Directory.Read.All |

## HTTP request

<!-- { "blockType": "ignored" } -->

```http
POST /applications/{id}/addPassword
```

## Request headers

| Name           | Type   | Description                |
|:---------------|:-------|:---------------------------|
| Authorization  | string | Bearer {token}. Required.  |

## Request body

In the request body, provide a JSON representation of [passwordCredential](../resources/passwordcredential.md) object.


## Response

If successful, this method returns `200, OK` response code and a new [passwordCredential](../resources/passwordcredential.md) object in the response body. Azure AD generates a strong password which is returned via the `secretText` property. There is no way to retrieve this password in the future.

## Examples

The following is an example of how to call this API.

### Request

The following is an example of the request.
<!-- {
  "blockType": "request",
  "name": "application_addpassword"
}-->

```http
POST https://graph.microsoft.com/beta/applications/{id}/addPassword
Content-type: application/json

{
  "passwordCredential": {
    "displayName": "Password friendly name"
  }
}
```

### Response

The following is an example of the response.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.passwordCredential"
} -->

```http
HTTP/1.1 200 OK
Content-type: application/json
{
    "customKeyIdentifier": null,
    "endDateTime": "2021-09-09T19:50:29.3086381Z",
    "keyId": "f0b0b335-1d71-4883-8f98-567911bfdca6",
    "startDateTime": "2019-09-09T19:50:29.3086381Z",
    "secretText": "[6gyXA5S20@MN+WRXAJ]I-TO7g1:h2P8",
    "hint": "[6g",
    "displayName": "Password friendly name"
}
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "application: addPassword",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->