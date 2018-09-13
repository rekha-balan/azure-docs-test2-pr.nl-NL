---
title: Define a OAuth1 technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a OAuth1 technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 10c90b060c184bb911ac149640e8a9570b59e2fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856294"
---
# <a name="define-a-oauth1-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a>Define a OAuth1 technical profile in an Azure Active Directory B2C custom policy

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Azure Active Directory (Azure AD) B2C provides support for the [OAuth 1.0 protocol](http://tools.ietf.org/html/rfc5849) identity provider. This article describes the specifics of a technical profile for interacting with a claims provider that supports this standardized protocol. With OAuth1 technical profile you can federate with an OAuth1 based identity provider, such as Twitter, allowing you users to sign-in with their existing social or enterprise identities.

## <a name="protocol"></a>Protocol

The **Name** attribute of the **Protocol** element needs to be set to `OAuth1`. For example, the protocol for the **Twitter-OAUTH1** technical profile is `OAuth1`.

```XML
<TechnicalProfile Id="Twitter-OAUTH1">
  <DisplayName>Twitter</DisplayName>
  <Protocol Name="OAuth1" />
  ...    
```

## <a name="input-claims"></a>Input claims

The **InputClaims** and **InputClaimsTransformations**  elements are empty or absent.

## <a name="output-claims"></a>Output claims

The **OutputClaims** element contains a list of claims returned by the OAuth1 identity provider. You may need to map the name of the claim defined in your policy to the name defined in the identity provider. You can also include claims that aren't returned by the identity provider as long as you set the **DefaultValue** attribute.

The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.

The following example shows the claims returned by the Twitter identity provider:

- The **user_id** claim that is mapped to the **socialIdpUserId** claim.
- The **screen_name** claim that is mapped to the **displayName** claim.
- The **email** claim without name mapping.

The technical profile also returns claims that aren't returned by the identity provider: 

- The **identityProvider** claim that contains the name of the identity provider.
- The **authenticationSource** claim with a default value of `socialIdpAuthentication`.

```xml
<OutputClaims>
  <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="user_id" />
  <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="screen_name" />
  <OutputClaim ClaimTypeReferenceId="email" />
  <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="twitter.com" />
  <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
</OutputClaims>
```

## <a name="metadata"></a>Metadata

| Attribute | Required | Description |
| --------- | -------- | ----------- |
| client_id | Yes | The application identifier of the identity provider. |
| ProviderName | No | The name of the identity provider. |
| request_token_endpoint | Yes | The URL of the request token endpoint as per RFC 5849. |
| authorization_endpoint | Yes | The URL of the authorization endpoint as per RFC 5849. |
| access_token_endpoint | Yes | The URL of the token endpoint as per RFC 5849. |
| ClaimsEndpoint | No | The URL of the user information endpoint. | 
| ClaimsResponseFormat | No | The claims response format.|

## <a name="cryptographic-keys"></a>Cryptographic keys

The **CryptographicKeys** element contains the following attribute:

| Attribute | Required | Description |
| --------- | -------- | ----------- |
| client_secret | Yes | The client secret of the identity provider application.   | 

## <a name="redirect-uri"></a>Redirect URI

When you configure the redirect URL of your identity provider, enter `https://login.microsoftonline.com/te/tenant/policyId/oauth1/authresp`. Make sure to replace **tenant** with your tenant name (for example, contosob2c.onmicrosoft.com) and **policyId** with the identifier of your policy (for example, b2c_1a_policy). The redirect URI needs to be in all lowercase. You should add a redirect UR for all policies that use the identity provider login. 

If you are using the **b2clogin.com** domain instead of **login.microsoftonline.com** Make sure to use b2clogin.com instead of login.microsoftonline.com.

Examples:

- [Add Twitter as an OAuth1 identity provider by using custom policies](active-directory-b2c-custom-setup-twitter-idp.md)













