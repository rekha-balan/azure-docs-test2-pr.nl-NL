---
title: Azure AD v2.0 OAuth Authorization Code Flow | Microsoft Docs
description: Building web applications using Azure AD's implementation of the OAuth 2.0 authentication protocol.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2018
ms.author: celested
ms.reviewer: hirsin
ms.custom: aaddev
ms.openlocfilehash: 3fb6cad6243bd6cd0b6a09827d590f7097550e31
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856706"
---
# <a name="v20-protocols---oauth-20-authorization-code-flow"></a>v2.0 Protocols - OAuth 2.0 Authorization Code Flow
The OAuth 2.0 authorization code grant can be used in apps that are installed on a device to gain access to protected resources, such as web APIs. Using the app model v2.0 's implementation of OAuth 2.0, you can add sign in and API access to your mobile and desktop apps. This guide is language-independent, and describes how to send and receive HTTP messages without using any of the [Azure open-source authentication libraries](active-directory-authentication-libraries.md).

> [!NOTE]
> Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint. To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

The OAuth 2.0 authorization code flow is described in [section 4.1 of the OAuth 2.0 specification](http://tools.ietf.org/html/rfc6749). It is used to perform authentication and authorization in the majority of app types, including [web apps](v2-app-types.md#web-apps) and [natively installed  apps](v2-app-types.md#mobile-and-native-apps). The flow enables apps to securely acquire access_tokens that can be used to access resources secured by the v2.0 endpoint. 

## <a name="protocol-diagram"></a>Protocol diagram
At a high level, the entire authentication flow for a native/mobile application looks a bit like this:

![OAuth Auth Code Flow](./media/v2-oauth2-auth-code-flow/convergence_scenarios_native.png)

## <a name="request-an-authorization-code"></a>Request an authorization code
The authorization code flow begins with the client directing the user to the `/authorize` endpoint. In this request, the client indicates the permissions it needs to acquire from the user:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Click the link below to execute this request! After signing in, your browser should be redirected to `https://localhost/myapp/` with a `code` in the address bar.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Parameter             |             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-----------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| tenant                | required    | The `{tenant}` value in the path of the request can be used to control who can sign into the application. The allowed values are `common`, `organizations`, `consumers`, and tenant identifiers. For more detail, see [protocol basics](active-directory-v2-protocols.md#endpoints).                                                                                                                                                                                                                                                                                                                    |
| client_id             | required    | The Application ID that the registration portal ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assigned your app.  |
| response_type         | required    | Must include `code` for the authorization code flow.       |
| redirect_uri          | recommended | The redirect_uri of your app, where authentication responses can be sent and received by your app. It must exactly match one of the redirect_uris you registered in the portal, except it must be url encoded. For native & mobile apps, you should use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.   |
| scope                 | required    | A space-separated list of [scopes](v2-permissions-and-consent.md) that you want the user to consent to.           |
| response_mode         | recommended | Specifies the method that should be used to send the resulting token back to your app. Can be `query`, `fragment`, or `form_post`. `query` provides the code as a query string parameter on your redirect URI. If you're requesting an ID token using the implicit flow, you cannot use `query` as specified in the [OpenID spec](https://openid.net/specs/oauth-v2-multiple-response-types-1_0.html#Combinations). If you're requesting just the code, you can use `query`, `fragment`, or `form_post`. `form_post` executes a POST containing the code to your redirect URI. For more info, see [OpenID Connect protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code).  |
| state                 | recommended | A value included in the request that will also be returned in the token response. It can be a string of any content that you wish. A randomly generated unique value is typically used for [preventing cross-site request forgery attacks](http://tools.ietf.org/html/rfc6749#section-10.12). The value can also encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on. |
| prompt                | optional    | Indicates the type of user interaction that is required. The only valid values at this time are 'login', 'none', and 'consent'. `prompt=login` will force the user to enter their credentials on that request, negating single-sign on. `prompt=none` is the opposite - it will ensure that the user is not presented with any interactive prompt whatsoever. If the request cannot be completed silently via single-sign on, the v2.0 endpoint will return an `interaction_required` error. `prompt=consent` will trigger the OAuth consent dialog after the user signs in, asking the user to grant permissions to the app. |
| login_hint            | optional    | Can be used to pre-fill the username/email address field of the sign-in page for the user, if you know their username ahead of time. Often apps will use this parameter during re-authentication, having already extracted the username from a previous sign-in using the `preferred_username` claim.                                                                                                                                                                                                                                                                                                    |
| domain_hint           | optional    | Can be one of `consumers` or `organizations`. If included, it will skip the email-based discovery process that user goes through on the v2.0 sign-in page, leading to a slightly more streamlined user experience. Often apps will use this parameter during re-authentication, by extracting the `tid` from a previous sign-in. If the `tid` claim value is `9188040d-6c67-4c5b-b112-36a304b66dad`, you should use `domain_hint=consumers`. Otherwise, use `domain_hint=organizations`.                                                                                                              |
| code_challenge_method | optional    | The method used to encode the `code_verifier` for the `code_challenge` parameter. Can be one of `plain` or `S256`. If excluded, `code_challenge` is assumed to be plaintext if `code_challenge` is included. Azure AAD v2.0 supports both `plain` and `S256`. For more information, see the [PKCE RFC](https://tools.ietf.org/html/rfc7636). |
| code_challenge        | optional    | Used to secure authorization code grants via Proof Key for Code Exchange (PKCE) from a native client. Required if `code_challenge_method` is included. For more information, see the [PKCE RFC](https://tools.ietf.org/html/rfc7636).                                                                                                                                                                                                                                                                                                                                                                    |

At this point, the user will be asked to enter their credentials and complete the authentication. The v2.0 endpoint will also ensure that the user has consented to the permissions indicated in the `scope` query parameter. If the user has not consented to any of those permissions, it will ask the user to consent to the required permissions. Details of [permissions, consent, and multi-tenant apps are provided here](v2-permissions-and-consent.md).

Once the user authenticates and grants consent, the v2.0 endpoint will return a response to your app at the indicated `redirect_uri`, using the method specified in the `response_mode` parameter.

#### <a name="successful-response"></a>Successful response
A successful response using `response_mode=query` looks like:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Parameter | Description                                                                                                                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| code      | The authorization_code that the app requested. The app can use the authorization code to request an access token for the target resource. Authorization_codes are very short lived, typically they expire after about 10 minutes. |
| state     | If a state parameter is included in the request, the same value should appear in the response. The app should verify that the state values in the request and response are identical.                                            |

#### <a name="error-response"></a>Error response
Error responses may also be sent to the `redirect_uri` so the app can handle them appropriately:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parameter         | Description                                                                                                       |
|-------------------|-------------------------------------------------------------------------------------------------------------------|
| error             | An error code string that can be used to classify types of errors that occur, and can be used to react to errors. |
| error_description | A specific error message that can help a developer identify the root cause of an authentication error.          |

#### <a name="error-codes-for-authorization-endpoint-errors"></a>Error codes for authorization endpoint errors
The following table describes the various error codes that can be returned in the `error` parameter of the error response.

| Error Code                | Description                                                                                                           | Client Action                                                                                                                                                                                                                               |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| invalid_request           | Protocol error, such as a missing required parameter.                                                               | Fix and resubmit the request. This is a development error typically caught during initial testing.                                                                                                                                     |
| unauthorized_client       | The client application is not permitted to request an authorization code.                                           | This error usually occurs when the client application is not registered in Azure AD or is not added to the user's Azure AD tenant. The application can prompt the user with instruction for installing the application and adding it to Azure AD. |
| access_denied             | Resource owner denied consent                                                                                         | The client application can notify the user that it cannot proceed unless the user consents.                                                                                                                                               |
| unsupported_response_type | The authorization server does not support the response type in the request.                                         | Fix and resubmit the request. This is a development error is typically caught during initial testing.                                                                                                                                     |
| server_error              | The server encountered an unexpected error.                                                                         | Retry the request. These errors can result from temporary conditions. The client application might explain to the user that its response is delayed  to a temporary error.                                                                |
| temporarily_unavailable   | The server is temporarily too busy to handle the request.                                                           | Retry the request. The client application might explain to the user that its response is delayed due to a temporary condition.                                                                                                               |
| invalid_resource          | The target resource is invalid because it does not exist, Azure AD cannot find it, or it is not correctly configured. | This error indicates the resource, if it exists, has not been configured in the tenant. The application can prompt the user with instruction for installing the application and adding it to Azure AD.                                          |
|login_required             | Too many or no users found | The client requested silent authentication (`prompt=none`), but a single user could not found. This may mean there are multiple users active in the session, or no users. This takes into account the tenant chosen (for example, if there are 2 AAD accounts active and one MSA, and `consumers` is chosen, silent authentication will work). |
|interaction_required       | The request requires user interaction. | An additional authentication step or consent is required. Retry the request without `prompt=none`. |

## <a name="request-an-access-token"></a>Request an access token
Now that you've acquired an authorization_code and have been granted permission by the user, you can redeem the `code` for an `access_token` to the desired resource. Do this by sending a `POST` request to the `/token` endpoint:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Try executing this request in Postman! (Don't forget to replace the `code`) [![Run in Postman](./media/v2-oauth2-auth-code-flow/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parameter     |                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                |
|---------------|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| tenant        | required              | The `{tenant}` value in the path of the request can be used to control who can sign into the application. The allowed values are `common`, `organizations`, `consumers`, and tenant identifiers. For more detail, see [protocol basics](active-directory-v2-protocols.md#endpoints).                                                                                                                                                   |
| client_id     | required              | The Application ID that the registration portal ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assigned your app.                                                                                                                                                                                                                             |
| grant_type    | required              | Must be `authorization_code` for the authorization code flow.                                                                                                                                                                                                                                                                                                                                                                            |
| scope         | required              | A space-separated list of scopes. The scopes requested in this leg must be equivalent to or a subset of the scopes requested in the first leg. If the scopes specified in this request span multiple resource server, then the v2.0 endpoint will return a token for the resource specified in the first scope. For a more detailed explanation of scopes, refer to [permissions, consent, and scopes](v2-permissions-and-consent.md). |
| code          | required              | The authorization_code that you acquired in the first leg of the flow.                                                                                                                                                                                                                                                                                                                                                                   |
| redirect_uri  | required              | The same redirect_uri value that was used to acquire the authorization_code.                                                                                                                                                                                                                                                                                                                                                             |
| client_secret | required for web apps | The application secret that you created in the app registration portal for your app. It should not be used in a native app, because client_secrets cannot be reliably stored on devices. It is required for web apps and web APIs, which have the ability to store the client_secret securely on the server side.  The client secret must be URL-encoded before being sent.                                                                                                                    |
| code_verifier | optional              | The same code_verifier that was used to obtain the authorization_code. Required if PKCE was used in the authorization code grant request. For more information, see the [PKCE RFC](https://tools.ietf.org/html/rfc7636)                                                                                                                                                                                                                                                                                             |
#### <a name="successful-response"></a>Successful response
A successful token response will look like:

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parameter     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| access_token  | The requested access token. The  app can use this token to authenticate to the secured resource, such as a web API.                                                                                                                                                                                                                                                                                                                                    |
| token_type    | Indicates the token type value. The only type that Azure AD supports is Bearer                                                                                                                                                                                                                                                                                                                                                                           |
| expires_in    | How long the access token is valid (in seconds).                                                                                                                                                                                                                                                                                                                                                                                                       |
| scope         | The scopes that the access_token is valid for.                                                                                                                                                                                                                                                                                                                                                                                                         |
| refresh_token | An OAuth 2.0 refresh token. The  app can use this token acquire additional access tokens after the current access token expires. Refresh_tokens are long-lived, and can be used to retain access to resources for extended periods of time. For more detail, refer to the [v2.0 token reference](v2-id-and-access-tokens.md). <br> **Note:** Only provided if `offline_access` scope was requested.                                               |
| id_token      | An unsigned JSON Web Token (JWT). The  app can base64Url decode the segments of this token to request information about the user who signed in. The  app can cache the values and display them, but it should not rely on them for any authorization or security boundaries. For more information about id_tokens, see the [v2.0 endpoint token reference](v2-id-and-access-tokens.md). <br> **Note:** Only provided if `openid` scope was requested. |
#### <a name="error-response"></a>Error response
Error responses will look like:

```json
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: The provided value for the input parameter 'scope' is not valid. The scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parameter         | Description                                                                                                       |
|-------------------|-------------------------------------------------------------------------------------------------------------------|
| error             | An error code string that can be used to classify types of errors that occur, and can be used to react to errors. |
| error_description | A specific error message that can help a developer identify the root cause of an authentication error.          |
| error_codes       | A list of STS-specific error codes that can help in diagnostics.                                                |
| timestamp         | The time at which the error occurred.                                                                           |
| trace_id          | A unique identifier for the request that can help in diagnostics.                                               |
| correlation_id    | A unique identifier for the request that can help in diagnostics across components.                             |

#### <a name="error-codes-for-token-endpoint-errors"></a>Error codes for token endpoint errors
| Error Code              | Description                                                                                                           | Client Action                                                                                                                                                                                                                               |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| invalid_request         | Protocol error, such as a missing required parameter.                                                               | Fix and resubmit the request                                                                                                                                                                                                                |
| invalid_grant           | The authorization code or PKCE code verifier is invalid or has expired.                                             | Try a new request to the `/authorize` endpoint and verify that the code_verifier parameter was correct.                                                                                                                                   |
| unauthorized_client     | The authenticated client is not authorized to use this authorization grant type.                                     | This usually occurs when the client application is not registered in Azure AD or is not added to the user's Azure AD tenant. The application can prompt the user with instruction for installing the application and adding it to Azure AD. |
| invalid_client          | Client authentication failed.                                                                                        | The client credentials are not valid. To fix, the application administrator updates the credentials.                                                                                                                                       |
| unsupported_grant_type  | The authorization server does not support the authorization grant type.                                              | Change the grant type in the request. This type of error should occur only during development and be detected during initial testing.                                                                                                      |
| invalid_resource        | The target resource is invalid because it does not exist, Azure AD cannot find it, or it is not correctly configured. | This indicates the resource, if it exists, has not been configured in the tenant. The application can prompt the user with instruction for installing the application and adding it to Azure AD.                                           |
| interaction_required    | The request requires user interaction. For example, an additional authentication step is required.                   | Retry the request with the same resource.                                                                                                                                                                                                  |
| temporarily_unavailable | The server is temporarily too busy to handle the request.                                                            | Retry the request. The client application might explain to the user that its response is delayed due to a temporary condition.                                                                                                                |

## <a name="use-the-access-token"></a>Use the access token
Now that you've successfully acquired an `access_token`, you can use the token in requests to Web APIs by including it in the `Authorization` header:

> [!TIP]
> Execute this request in Postman! (Replace the `Authorization` header first) [![Run in Postman](./media/v2-oauth2-auth-code-flow/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-the-access-token"></a>Refresh the access token
Access_tokens are short lived, and you must refresh them after they expire to continue accessing resources. You can do so by submitting another `POST` request to the `/token` endpoint, this time providing the `refresh_token` instead of the `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Try executing this request in Postman! (Don't forget to replace the `refresh_token`) [![Run in Postman](./media/v2-oauth2-auth-code-flow/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parameter     |                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|---------------|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| tenant        | required              | The `{tenant}` value in the path of the request can be used to control who can sign into the application. The allowed values are `common`, `organizations`, `consumers`, and tenant identifiers. For more detail, see [protocol basics](active-directory-v2-protocols.md#endpoints).                                                                                                                                                                                  |
| client_id     | required              | The Application ID that the registration portal ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) assigned your app.                                                                                                                                                                                                                                                            |
| grant_type    | required              | Must be `refresh_token` for this leg of the authorization code flow.                                                                                                                                                                                                                                                                                                                                                                                                    |
| scope         | required              | A space-separated list of scopes. The scopes requested in this leg must be equivalent to or a subset of the scopes requested in the original authorization_code request leg. If the scopes specified in this request span multiple resource server, then the v2.0 endpoint will return a token for the resource specified in the first scope. For a more detailed explanation of scopes, refer to [permissions, consent, and scopes](v2-permissions-and-consent.md). |
| refresh_token | required              | The refresh_token that you acquired in the second leg of the flow.                                                                                                                                                                                                                                                                                                                                                                                                      |
| redirect_uri  | required              | The same redirect_uri value that was used to acquire the authorization_code.                                                                                                                                                                                                                                                                                                                                                                                            |
| client_secret | required for web apps | The application secret that you created in the app registration portal for your app. It should not be used in a native  app, because client_secrets cannot be reliably stored on devices. It is required for web apps and web APIs, which have the ability to store the client_secret securely on the server side.                                                                                                                                                    |

#### <a name="successful-response"></a>Successful response
A successful token response will look like:

```json
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parameter     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| access_token  | The requested access token. The  app can use this token to authenticate to the secured resource, such as a web API.                                                                                                                                                                                                                                                                                                                                     |
| token_type    | Indicates the token type value. The only type that Azure AD supports is Bearer                                                                                                                                                                                                                                                                                                                                                                           |
| expires_in    | How long the access token is valid (in seconds).                                                                                                                                                                                                                                                                                                                                                                                                        |
| scope         | The scopes that the access_token is valid for.                                                                                                                                                                                                                                                                                                                                                                                                          |
| refresh_token | A new OAuth 2.0 refresh token. You should replace the old refresh token with this newly acquired refresh token to ensure your refresh tokens remain valid for as long as possible. <br> **Note:** Only provided if `offline_access` scope was requested.                                                                                                                                                                                                |
| id_token      | An unsigned JSON Web Token (JWT). The  app can base64Url decode the segments of this token to request information about the user who signed in. The  app can cache the values and display them, but it should not rely on them for any authorization or security boundaries. For more information about id_tokens, see the [v2.0 endpoint token reference](v2-id-and-access-tokens.md). <br> **Note:** Only provided if `openid` scope was requested. |

#### <a name="error-response"></a>Error response

```json
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: The provided value for the input parameter 'scope' is not valid. The scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parameter         | Description                                                                                                       |
|-------------------|-------------------------------------------------------------------------------------------------------------------|
| error             | An error code string that can be used to classify types of errors that occur, and can be used to react to errors. |
| error_description | A specific error message that can help a developer identify the root cause of an authentication error.           |
| error_codes |A list of STS-specific error codes that can help in diagnostics. |
| timestamp |The time at which the error occurred. |
| trace_id |A unique identifier for the request that can help in diagnostics. |
| correlation_id |A unique identifier for the request that can help in diagnostics across components. |

For a description of the error codes and the recommended client action, see [Error codes for token endpoint errors](#error-codes-for-token-endpoint-errors).
