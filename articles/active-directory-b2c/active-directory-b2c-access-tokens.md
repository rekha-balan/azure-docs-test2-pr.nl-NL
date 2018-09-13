---
title: 'Azure Active Directory B2C: Requesting access tokens | Microsoft Docs'
description: This article will show you how to setup a client application and acquire an access token.
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: ''
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.translationtype: HT
ms.date: 03/16/2017
ms.author: parakhj
ms.openlocfilehash: dbe4c24a75eb2f58d22cefb64bb482caa3886542
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548824"
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: Requesting Access Tokens


An access token (denoted as **access\_token**) is a form of security token that a client can use to access resources that are secured by an [authorization server](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), such as a web API. Access tokens are represented as [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) and contain information about the intended resource server and the granted permissions to the server. When calling the resource server, the access token must be present in the HTTP request.

This article discusses how to configure a client application and have it make a request to acquire an **access\_token** from the `authorize` and `token` endpoints.

## <a name="prerequisite"></a>Prerequisite

Before requesting an access token, you first need to register a web API and publish permissions that can be granted to the client application. Get started by following the steps under the [Register a web API](active-directory-b2c-app-registration.md) section.

## <a name="granting-permissions-to-a-web-api"></a>Granting permissions to a web API

In order for a client application to get specific permissions to an API, the client application needs to be granted those permissions via the Azure portal. To grant permissions to a client application:

1. Navigate to the **Applications** menu in the B2C features blade.
2. Click on your client application ([Register an application](active-directory-b2c-app-registration.md) if you don’t have one).
3. Select **Api access**.
4. Click on **Add**.
5. Select your web API and the scopes (permissions) you would like to grant.
6. Click **OK**.

> [!NOTE]
> Azure AD B2C does not ask your client application users for their consent. Instead, all consent is provided by the admin, based on the permissions configured between the applications described above. If a permission grant for an application is revoked, all users who were previously able to acquire that permission will no longer be able to do so.

## <a name="requesting-a-token"></a>Requesting a token

To get an access token for a resource application, the client application needs to specify the permissions wanted in the **scope** parameter of the request. For example, to acquire the “read” permission for the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/notes`, the scope would be `https://contoso.onmicrosoft.com/notes/read`. Below is an example of an authorization code request to the `authorize` endpoint.

```
https://login.microsoftonline.com/<yourTenantId>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

To acquire multiple permissions in the same request, you can add multiple entries in the single **scope** parameter, separated by spaces. For example:

URL decoded:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

URL encoded:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

You may request more scopes/permissions for a resource than what is granted for your client application. When this is the case, the call will succeed if at least one permission is granted. The resulting **access\_token** will have its “scp” claim populated with only the permissions that were successfully granted.

> [!NOTE] 
> We do not support requesting permissions against two different web resources in the same request. This kind of request will fail.

### <a name="special-cases"></a>Special cases

The OpenID Connect standard specifies several special “scope” values. The following special scopes represent the permission to “access the user’s profile”:

* **openid**: This requests an ID token
* **offline\_access**: This requests a refresh token (using Auth Code flows).

If the “response\_type” parameter in a `authorize` request includes “token”, the “scope” parameter must include at least one resource permission (other than “openid” and “offline\_access”) that will be granted. Otherwise, the `authorize` request will terminate with a failure.

## <a name="the-returned-token"></a>The returned token

In a successfully minted **access\_token** (from either the `authorize` or `token` endpoint), the following claims will be present:

| Name | Claim | Description |
| --- | --- | --- |
|Audience |`aud` |The \*application ID\* of the single resource that the token grants access to. |
|Scope |`scp` |The permissions granted to the resource. Multiple granted permissions will be separated by space. |
|Authorized Party |`azp` |The \*application ID\* of the client application that initiated the request. |

When your API receives the **access\_token**, it must [validate the token](active-directory-b2c-reference-tokens.md) to prove that the token is authentic and has the correct claims.

We are always open to feedback and suggestions! If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page. For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
