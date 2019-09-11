---
title: "keyCredential resource type"
description: "Contains a key credential associated with an application or a service principal. The **keyCredentials** property of the application and servicePrincipal entities is a collection of **keyCredential**."
localization_priority: Normal
doc_type: resourcePageType
ms.prod: ""
author: ""
---

# keyCredential resource type

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Contains a key credential associated with an application or a service principal. The **keyCredentials** property of the [application](application.md) and [servicePrincipal](serviceprincipal.md) entities is a collection of **keyCredential**.


## Properties
| Property	   | Type	|Description|
|:---------------|:--------|:----------|
| customKeyIdentifier | Binary | Certificate thumbprint |
| displayName | String | Subject name of the certificate |
| endDateTime | DateTimeOffset | The date and time at which the credential expires.The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 would look like this: `'2014-01-01T00:00:00Z'` |
| key| Binary | |
| keyId| Guid | The unique identifier (GUID) for the key. |
| startDateTime | DateTimeOffset|The date and time at which the credential becomes valid.The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 would look like this: `'2014-01-01T00:00:00Z'` |
| type | String | The type of key credential; for example, “Symmetric”. |
| usage | String | A string that describes the purpose for which the key can be used; for example, “Verify”. |

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!--
{
  "type": "#page.annotation",
  "description": "keyCredential resource",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": []
}
-->

## JSON representation

The following is a JSON representation of the resource.

<!-- {
  "blockType": "resource",
  "optionalProperties": [

  ],
  "@odata.type": "microsoft.graph.keyCredential",
  "baseType": null
}-->

```json
{
  "customKeyIdentifier": "Binary",
  "displayName": "String",
  "endDateTime": "String (timestamp)",
  "key": "Binary",
  "keyId": "Guid",
  "startDateTime": "String (timestamp)",
  "type": "String",
  "usage": "String"
}
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "keyCredential resource",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->