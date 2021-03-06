---
title: Define a technical profile for a JWT token issuer in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a technical profile for a JWT token issuer in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: cb004745cfbc6af185a06c4787fb34326eccc69a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870039"
---
# <a name="define-a-technical-profile-for-a-jwt-token-issuer-in-an-azure-active-directory-b2c-custom-policy"></a>Define a technical profile for a JWT token issuer in an Azure Active Directory B2C custom policy

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Azure Active Directory (Azure AD) B2C emits several types of security tokens as it processes each authentication flow. A technical profile for a JWT token issuer emits a JWT token that is returned back to the relying party application. Usually this technical profile is the last orchestration step in the user journey.

## <a name="protocol"></a>Protocol

The **Name** attribute of the **Protocol** element needs to be set to `None`. Set the **OutputTokenFormat** element to `JWT`.

The following example shows a technical profile for `JwtIssuer`:

```XML
<TechnicalProfile Id="JwtIssuer">
  <DisplayName>JWT Issuer</DisplayName>
  <Protocol Name="None" />
  <OutputTokenFormat>JWT</OutputTokenFormat>
  ...
</TechnicalProfile>
```
 
## <a name="input-output-and-persist-claims"></a>Input, output, and persist claims

The **InputClaims**, **OutputClaims**, and **PersistClaims** elements are empty or absent. The **InutputClaimsTransformations** and **OutputClaimsTransformations** elements are also absent.

## <a name="metadata"></a>Metadata

| Attribute | Required | Description |
| --------- | -------- | ----------- |
| issuer_refresh_token_user_identity_claim_type | Yes | The claim that should be used as the user identity claim within the OAuth2 authorization codes and refresh tokens. By default, you should set it to `objectId`, unless you specify a different SubjectNamingInfo claim type. | 
| SendTokenResponseBodyWithJsonNumbers | No | Always set to `true`. For legacy format where numeric values are given as strings instead of JSON numbers, set to `false`. This attribute is needed for clients that have taken a dependency on an earlier implementation that returned such properties as strings. | 
| token_lifetime_secs | No | Access token lifetimes. The lifetime of the OAuth 2.0 bearer token used to gain access to a protected resource. The default is 3,600 seconds (1 hour). The minimum (inclusive) is 300 seconds (5 minutes). The maximum (inclusive) is 86,400 seconds (24 hours). | 
| id_token_lifetime_secs | No | ID token lifetimes. The default is 3,600 seconds (1 hour). The minimum (inclusive) is 300 seconds (5 minutes). The maximum (inclusive) is seconds 86,400 (24 hours). | 
| refresh_token_lifetime_secs | No | Refresh token lifetimes. The maximum time period before which a refresh token can be used to acquire a new access token, if your application had been granted the offline_access scope. The default is 120,9600 seconds (14 days). The minimum (inclusive) is 86,400 seconds (24 hours). The maximum (inclusive) is 7,776,000 seconds (90 days). | 
| rolling_refresh_token_lifetime_secs | No | Refresh token sliding window lifetime. After this time period elapses the user is forced to reauthenticate, irrespective of the validity period of the most recent refresh token acquired by the application. If you don't want to enforce a sliding window lifetime, set the value of allow_infinite_rolling_refresh_token to `true`. The default is 7,776,000 seconds (90 days). The minimum (inclusive) is 86,400 seconds (24 hours). The maximum (inclusive) is 31,536,000 seconds (365 days). | 
| rolling_refresh_token_lifetime_secs | No | If set to `true`, the refresh token sliding window lifetime never expires. |
| IssuanceClaimPattern | Yes | Controls the Issuer (iss) claim. One of the values:<ul><li>AuthorityAndTenantGuid - The iss claim includes your domain name, such as `login.microsoftonline` or `tenant-name.b2clogin.com`, and your tenant identifier https://login.microsoftonline.com/00000000-0000-0000-0000-000000000000/v2.0/</li><li>AuthorityWithTfp - The iss claim includes your domain name, such as `login.microsoftonline` or `tenant-name.b2clogin.com`, your tenant identifier and your relying party policy name. https://login.microsoftonline.com/tfp/00000000-0000-0000-0000-000000000000/b2c_1a_tp_sign-up-or-sign-in/v2.0/</li></ul> | 
| AuthenticationContextReferenceClaimPattern | No | Controls the `acr` claim value.<ul><li>None - Azure AD B2C doesn't issue the acr claim</li><li>PolicyId - the `acr` claim contains the policy name</li></ul>The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference). It is recommended setting this value to TFP, to set the value, ensure the `<Item>` with the `Key="AuthenticationContextReferenceClaimPattern"` exists and the value is `None`. In your relying party policy, add <OutputClaims> item, add this element `<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />`. Also make sure your policy contains the claim type `<ClaimType Id="trustFrameworkPolicy"> <DisplayName>trustFrameworkPolicy</DisplayName>     <DataType>string</DataType> </ClaimType>` | 

## <a name="cryptographic-keys"></a>Cryptographic keys

The CryptographicKeys element contains the following attributes:

| Attribute | Required | Description |
| --------- | -------- | ----------- |
| issuer_secret | Yes | The X509 certificate (RSA key set) to use to sign the JWT token. This is the `B2C_1A_TokenSigningKeyContainer` key you cofigured in [Get started with custom policies](active-directory-b2c-get-started-custom.md). | 
| issuer_refresh_token_key | Yes | The X509 certificate (RSA key set) to use to encrypt the refresh token. You configured the `B2C_1A_TokenEncryptionKeyContainer` key in [Get started with custom policies](active-directory-b2c-get-started-custom.md) |














