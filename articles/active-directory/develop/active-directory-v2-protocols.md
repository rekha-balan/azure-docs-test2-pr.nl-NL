---
title: Learn about the authorization protocols supported by Azure AD v2.0 | Microsoft Docs
description: A guide to protocols supported by the Azure AD v2.0 endpoint.
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2018
ms.author: celested
ms.reviewer: hirsin
ms.custom: aaddev
ms.openlocfilehash: 645ce394c09f5cdd9f45b085e8d86cdc07ee9158
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793681"
---
# <a name="v20-protocols---oauth-20--openid-connect"></a>v2.0 Protocols - OAuth 2.0 & OpenID Connect
The v2.0 endpoint can use Azure AD for identity-as-a-service with industry standard protocols, OpenID Connect and OAuth 2.0. While the service is standards-compliant, there can be subtle differences between any two implementations of these protocols. The information here will be useful if you choose to write your code by directly sending & handling HTTP requests or use a 3rd party open source library, rather than using one of our [open source libraries](reference-v2-libraries.md).

> [!NOTE]
> Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint. To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).
>
>

## <a name="the-basics"></a>The Basics
In nearly all OAuth & OpenID Connect flows, there are four parties involved in the exchange:

![OAuth 2.0 Roles](../../media/active-directory-v2-flows/protocols_roles.png)

* The **Authorization Server** is the v2.0 endpoint. It is responsible for ensuring the user's identity, granting and revoking access to resources, and issuing tokens. It is also known as the identity provider - it securely handles anything to do with the user's information, their access, and the trust relationships between parties in an flow.
* The **Resource Owner** is typically the end-user. It is the party that owns the data, and has the power to allow third parties to access that data, or resource.
* The **OAuth Client** is your app, identified by its Application Id. It is usually the party that the end-user interacts with, and it requests tokens from the authorization server. The client must be granted permission to access the resource by the resource owner.
* The **Resource Server** is where the resource or data resides. It trusts the Authorization Server to securely authenticate and authorize the OAuth Client, and uses Bearer access_tokens to ensure that access to a resource can be granted.

## <a name="app-registration"></a>App Registration
Every app that uses the v2.0 endpoint will need to be registered at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) before it can interact using OAuth or OpenID Connect. The app registration process will collect & assign a few values to your app:

* An **Application Id** that uniquely identifies your app
* A **Redirect URI** or **Package Identifier** that can be used to direct responses back to your app
* A few other scenario-specific values.

For more details, learn how to [register an app](quickstart-v2-register-an-app.md).

## <a name="endpoints"></a>Endpoints
Once registered, the app communicates with Azure AD by sending requests to the v2.0 endpoint:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Where the `{tenant}` can take one of four different values:

| Value | Description |
| --- | --- |
| `common` |Allows users with both personal Microsoft accounts and work/school accounts from Azure Active Directory to sign into the application. |
| `organizations` |Allows only users with work/school accounts from Azure Active Directory to sign into the application. |
| `consumers` |Allows only users with personal Microsoft accounts (MSA) to sign into the application. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` or `contoso.onmicrosoft.com` |Allows only users with work/school accounts from a particular Azure Active Directory tenant to sign into the application. Either the friendly domain name of the Azure AD tenant or the tenant's guid identifier can be used. |

For more information on how to interact with these endpoints, choose a particular app type below.

## <a name="tokens"></a>Tokens
The v2.0 implementation of OAuth 2.0 and OpenID Connect make extensive use of bearer tokens, including bearer tokens represented as JWTs. A bearer token is a lightweight security token that grants the “bearer” access to a protected resource. In this sense, the “bearer” is any party that can present the token. Though a party must first authenticate with Azure AD to receive the bearer token, if the required steps are not taken to secure the token in transmission and storage, it can be intercepted and used by an unintended party. While some security tokens have a built-in mechanism for preventing unauthorized parties from using them, bearer tokens do not have this mechanism and must be transported in a secure channel such as transport layer security (HTTPS). If a bearer token is transmitted in the clear, a man-in the middle attack can be used by a malicious party to acquire the token and use it for an unauthorized access to a protected resource. The same security principles apply when storing or caching bearer tokens for later use. Always ensure that your app transmits and stores bearer tokens in a secure manner. For more security considerations on bearer tokens, see [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).

Further details of different types of tokens used in the v2.0 endpoint is available in [the v2.0 endpoint token reference](v2-id-and-access-tokens.md).

## <a name="protocols"></a>Protocols
If you're ready to see some example requests, get started with one of the below tutorials. Each one corresponds to a particular authentication scenario. If you need help determining which is the right flow for you, check out [the types of apps you can build with the v2.0](v2-app-types.md).

* [Build Mobile and Native Application with OAuth 2.0](v2-oauth2-auth-code-flow.md)
* [Build Web Apps with Open ID Connect](v2-protocols-oidc.md)
* [Build Single Page Apps with the OAuth 2.0 Implicit Flow](v2-oauth2-implicit-grant-flow.md)
* [Build Daemons or Server Side Processes with the OAuth 2.0 Client Credentials Flow](v2-oauth2-client-creds-grant-flow.md)
* [Get tokens in a Web API with the OAuth 2.0 On Behalf Of Flow](v2-oauth2-on-behalf-of-flow.md)
