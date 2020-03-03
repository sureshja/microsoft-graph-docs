---
title: "application: removeKey"
description: "Remove a key credential from an application"
localization_priority: Normal
author: "davidmu1"
ms.prod: "microsoft-identity-platform"
doc_type: "apiPageType"
---

# application: removeKey

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Removes a key credential from an [application](../resources/application.md). This method along with [addKey](application-addkey.md) can be used by an application to automate rolling its expiring keys.

> [!Note]
> [Create servicePrincipal](../api/serviceprincipal-post-serviceprincipals.md) and
[Update servicePrincipal](../api/serviceprincipal-update.md) operations can continue to be used to add and update key credentials for any application with application or a user's context.

As part of the request validation for this method, a proof of possession of an existing key is verified before the action can be performed.

## Permissions

None. An application does not need any specific permission to roll it's own keys.

## HTTP request

<!-- { "blockType": "ignored" } -->

```http
POST /applications/{id}/removeKey
```

## Request headers

| Name           | Description                |
|:---------------|:---------------------------|
| Authorization  | Bearer {token}. Required.  |
| Content-Type   | application/json. Required.|

## Request body

In the request body, provide the following required properties.

| Property	| Type | Description|
|:----------|:-----|:-----------|
| keyId     | GUID | The unique identifier for the password.|
| proof | String | A self-signed JWT token used as a proof of possession of the existing keys. This JWT token must be signed using the private key of one of the application's existing valid certificates. The token should contain the following claims:<ul><li>`aud` - Audience needs to be `00000002-0000-0000-c000-000000000000`.</li><li>`iss` - Issuer needs to be the __id__  of the application that is making the call.</li><li>`nbf` - Not before time.</li><li>`exp` - Expiration time should be "nbf" + 10 mins.</li></ul><br>A code [sample](#sample-to-generate-proof-token) to generate this proof of possession token is provided at the end of this topic.|

## Response

If successful, this method returns a `204 No content` response code.

## Examples

The following is example shows how to call this API.

### Request

The following is an example of the request.

<!-- {
  "blockType": "request",
  "name": "application_removekey"
}-->

```http
POST https://graph.microsoft.com/beta/applications/{id}/removeKey
Content-Type: application/json

{
    "keyId": "f0b0b335-1d71-4883-8f98-567911bfdca6",
    "proof":"eyJ0eXAiOiJ..."
}
```

### Response

The following is an example of the response.

<!-- {
  "blockType": "response",
  "truncated": true
} -->

```http
HTTP/1.1 204 No Content
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "application: removeKey",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->

## Sample to generate proof token

The following sample could be used to generate the proof token:

```csharp
using System;
using System.Collections.Generic;
using System.Security.Cryptography.X509Certificates;
using Microsoft.IdentityModel.Tokens;
using Microsoft.IdentityModel.JsonWebTokens;

namespace MicrosoftIdentityPlatformProofTokenGenerator
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the following
            string pfxFilePath = "<Path to your certificate file";
            string password = "<Certificate password>";
            string objectId = "<id of the application object>";

            // Get signing certificate
            X509Certificate2 signingCert = new X509Certificate2(pfxFilePath, password);

            // audience
            string aud = $"00000002-0000-0000-c000-000000000000";

            // aud and iss are the only required claims.
            var claims = new Dictionary<string, object>()
            {
                { "aud", aud },
                { "iss", objectId }
            };

            // token validity should not be more than 10 minutes
            var now = DateTime.UtcNow;
            var securityTokenDescriptor = new SecurityTokenDescriptor
            {
                Claims = claims,
                NotBefore = now,
                Expires = now.AddMinutes(10),
                SigningCredentials = new X509SigningCredentials(signingCert)
            };

            var handler = new JsonWebTokenHandler();
            var x = handler.CreateToken(securityTokenDescriptor);
            Console.WriteLine(x);
        }
    }
}
```