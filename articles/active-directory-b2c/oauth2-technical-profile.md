---
title: Define a OAuth2 technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a OAuth2 technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 7f85de79b683ba7b10f5466c4a8042fc0ffdea90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867882"
---
# <a name="define-a-oauth2-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a>Define a OAuth2 technical profile in an Azure Active Directory B2C custom policy

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Azure Active Directory (Azure AD) B2C provides support for the OAuth2 protocol identity provider. This is the primary protocol for authorization and delegated authentication. For more information, see the [RFC 6749 The OAuth 2.0 Authorization Framework](http://tools.ietf.org/html/rfc6749). With OAuth2 technical profile you can federate with an OAuth2 based identity provider, such as Facebook and Live.com, allowing you users to sign-in with their existing social or enterprise identities.

## <a name="protocol"></a>Protocol

The **Name** attribute of the **Protocol** element needs to be set to `OAuth2`. For example, the protocol for the **Facebook-OAUTH** technical profile is `OAuth2`:

```XML
<TechnicalProfile Id="Facebook-OAUTH">
  <DisplayName>Facebook</DisplayName>
  <Protocol Name="OAuth2" />
  ...    
```

## <a name="input-claims"></a>Input claims

The **InputClaims** and **InputClaimsTransformations** elements are not required. But you may want to send additional parameters to your identity provider. The following example adds the **domain_hint** query string parameter with the value of `contoso.com` to the authorization request.

```XML
<InputClaims>
  <InputClaim ClaimTypeReferenceId="domain_hint" DefaultValue="contoso.com" />
</InputClaims>
```

## <a name="output-claims"></a>Output claims

The **OutputClaims** element contains a list of claims returned by the OAuth2 identity provider. You may need to map the name of the claim defined in your policy to the name defined in the identity provider. You can also include claims that aren't returned by the identity provider as long as the you set the `DefaultValue` attribute.

The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify the output claims or generate new ones.

The following example shows the claims returned by the Facebook identity provider:

- The **first_name** claim is mapped to the **givenName** claim.
- The **last_name** claim is mapped to the **surname** claim.
- The **displayName** claim without name mapping..
- The **email** claim without name mapping.

The technical profile also returns claims that aren't returned by the identity provider: 

- The **identityProvider** claim that contains the name of the identity provider.
- The **authenticationSource** claim with a default value of **socialIdpAuthentication**.

```xml
<OutputClaims>
  <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
  <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="first_name" />
  <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="last_name" />
  <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
  <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
  <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="facebook.com" />
  <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
</OutputClaims>
```

## <a name="metadata"></a>Metadata

| Attribute | Required | Description |
| --------- | -------- | ----------- |
| client_id | Yes | The application identifier of the identity provider. |
| IdTokenAudience | No | The audience of the id_token. If specified, Azure AD B2C checks whether the token is in a claim returned by the identity provider and is equal to the one specified. |
| authorization_endpoint | Yes | The URL of the authorization endpoint as per RFC 6749. |
| AccessTokenEndpoint | Yes | The URL of the token endpoint as per RFC 6749. |  
| ClaimsEndpoint | Yes | The URL of the user information endpoint as per RFC 6749. | 
| AccessTokenResponseFormat | No | The format of the access token endpoint call. For example, Facebook requires an HTTP GET method, but the access token response is in JSON format. |
| AdditionalRequestQueryParameters | No | Additional request query parameters. For example, you may want to send additional parameters to your identity provider. You can include multiple parameters using comma delimiter. | 
| ClaimsEndpointAccessTokenName | No | The name of the access token query string parameter. Some identity providers' claims endpoints support GET HTTP request. In this case, the bearer token is sent by using a query string parameter instead of the authorization header. |
| ClaimsEndpointFormatName | No | The name of the format query string parameter. For example, you can set the name as `format` in this LinkedIn claims endpoint `https://api.linkedin.com/v1/people/~?format=json`. | 
| ClaimsEndpointFormat | No | The value of the format query string parameter. For example, you can set the value as `json` in this LinkedIn claims endpoint `https://api.linkedin.com/v1/people/~?format=json`. | 
| ProviderName | No | The name of the identity provider. |
| response_mode | No | The method that the identity provider uses to send the result back to Azure AD B2C. Possible values: `query`, `form_post` (default), or `fragment`. |
| scope | No | The scope of the access request defined according to the OAuth2 identity provider specification. Such as `openid`, `profile`, and `email`. |
| HttpBinding | No | The expected HTTP binding to the access token and claims token endpoints. Possible values: `GET` or `POST`.  |
| ResponseErrorCodeParamName | No | The name of the parameter that contains the error message returned over HTTP 200 (Ok). |
| ExtraParamsInAccessTokenEndpointResponse | No | Contains the extra parameters that can be returned in the response from **AccessTokenEndpoint** by some identity providers. For example, the response from **AccessTokenEndpoint** contains an extra parameter such as `openid`, which is a mandatory parameter besides the access_token in a **ClaimsEndpoint** request query string. Multiple parameter names should be escaped and separated by the comma ',' delimiter. |
| ExtraParamsInClaimsEndpointRequest | No | Contains the extra parameters that can be returned in the **ClaimsEndpoint** request by some identity providers. Multiple parameter names should be escaped and separated by the comma ',' delimiter. |

## <a name="cryptographic-keys"></a>Cryptographic keys

The **CryptographicKeys** element contains the following attribute:

| Attribute | Required | Description |
| --------- | -------- | ----------- |
| client_secret | Yes | The client secret of the identity provider application. The cryptographic key is required only if the **response_types** metadata is set to `code`. In this case, Azure AD B2C makes another call to exchange the authorization code for an access token. If the metadata is set to `id_token` you can omit the cryptographic key.  |  

## <a name="redirect-uri"></a>Redirect URI

When you configure the redirect URL of your identity provider, enter `https://login.microsoftonline.com/te/tenant/policyId/oauth2/authresp`. Make sure to replace **tenant** with your tenant's name (for example, contosob2c.onmicrosoft.com) and **policyId** with the identifier of your policy (for example, b2c_1a_policy). The redirect URI needs to be in all lowercase.

If you are using the **b2clogin.com** domain instead of **login.microsoftonline.com** Make sure to use b2clogin.com instead of login.microsoftonline.com.

Examples:

- [Add Google+ as an OAuth2 identity provider using custom policies](active-directory-b2c-custom-setup-goog-idp.md)












