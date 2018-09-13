---
title: Boolean claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: Boolean claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: b1e56e9126b1dd93ed790da1526b64c49524149d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868688"
---
# <a name="boolean-claims-transformations"></a>Boolean claims transformations

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

This article provides examples for using the boolean claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C. For more information, see [ClaimsTransformations](claimstransformations.md).

## <a name="andclaims"></a>AndClaims

Performs an And operation of two boolean inputClaims and sets the outputClaim with result of the operation.

| Item  | TransformationClaimType  | Data Type  | Notes |
|-------| ------------------------ | ---------- | ----- |
| InputClaim | inputClaim1 | boolean | The first ClaimType to evaluate. |
| InputClaim | inputClaim2  | boolean | The second ClaimType to evaluate. |
|OutputClaim | outputClaim | boolean | The ClaimTypes that will be produced after this claims transformation has been invoked (true or false). |

The following claims transformation demonstrates how to And two boolean ClaimTypes: `isEmailNotExist`, and `isSocialAccount`. The output claim `presentEmailSelfAsserted` is set to `true` if the value of both input claims are `true`. In an orchestration step, you can use a precondition to preset a self-asserted page, only if a social account email is empty.

```XML
<ClaimsTransformation Id="CheckWhetherEmailBePresented" TransformationMethod="AndClaims">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="isEmailNotExist" TransformationClaimType="inputClaim1" />
    <InputClaim ClaimTypeReferenceId="isSocialAccount" TransformationClaimType="inputClaim2" />
  </InputClaims>                    
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="presentEmailSelfAsserted" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a>Example

- Input claims:
    - **inputClaim1**: true
    - **inputClaim2**: false
- Output claims:
    - **outputClaim**: false


## <a name="assertbooleanclaimisequaltovalue"></a>AssertBooleanClaimIsEqualToValue

Checks that boolean values of two claims are equal, and throws an exception if they are not.

| Item | TransformationClaimType  | Data Type  | Notes |
| ---- | ------------------------ | ---------- | ----- |
| inputClaim | inputClaim | boolean | The ClaimType to be asserted. |
| InputParameter |valueToCompareTo | boolean | The value to compare (true or false). |

The **AssertBooleanClaimIsEqualToValue** claims transformation is always executed from a [validation technical profile](validation-technical-profile.md) that is called by a [self-asserted technical profile](self-asserted-technical-profile.md). The **UserMessageIfClaimsTransformationBooleanValueIsNotEqual** self-asserted technical profile metadata controls the error message that the technical profile presents to the user.

![AssertStringClaimsAreEqual execution](./media/boolean-transformations/assert-execution.png)

The following claims transformation demonstrates how to check the value of a boolean ClaimType with a `true` value. If the value of the `accountEnabled` ClaimType is false, an error message is thrown.

```XML
<ClaimsTransformation Id="AssertAccountEnabledIsTrue" TransformationMethod="AssertBooleanClaimIsEqualToValue">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="accountEnabled" TransformationClaimType="inputClaim" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="valueToCompareTo" DataType="boolean" Value="true" />
  </InputParameters>
</ClaimsTransformation>
```


The `login-NonInteractive` validation technical profile calls the `AssertAccountEnabledIsTrue` claims transformation.
```XML
<TechnicalProfile Id="login-NonInteractive">
  ...
  <OutputClaimsTransformations>
    <OutputClaimsTransformation ReferenceId="AssertAccountEnabledIsTrue" />
  </OutputClaimsTransformations>
</TechnicalProfile>
```

The self-asserted technical profile calls the validation **login-NonInteractive** technical profile.

```XML
<TechnicalProfile Id="SelfAsserted-LocalAccountSignin-Email">
  <Metadata>
    <Item Key="UserMessageIfClaimsTransformationBooleanValueIsNotEqual">Custom error message if account is disabled.</Item>
  </Metadata>
  <ValidationTechnicalProfiles>
    <ValidationTechnicalProfile ReferenceId="login-NonInteractive" />
  </ValidationTechnicalProfiles>
</TechnicalProfile>
```

### <a name="example"></a>Example

- Input claims:
    - **inputClaim**: false
    - **valueToCompareTo**: true
- Result: Error thrown

## <a name="notclaims"></a>NotClaims

Performs a Not operation of the boolean inputClaim and sets the outputClaim with result of the operation.

| Item | TransformationClaimType | Data Type | Notes |
| ---- | ----------------------- | --------- | ----- |
| InputClaim | inputClaim | boolean | The claim to be operated. |
| OutputClaim | outputClaim | boolean | The ClaimTypes that are produced after this ClaimsTransformation has been invoked (true or false). |

Use this claim transformation to perform logical negation on a claim.

```XML
<ClaimsTransformation Id="CheckWhetherEmailBePresented" TransformationMethod="AndClaims">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="userExists" TransformationClaimType="inputClaim" />
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="userExists" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a>Example

- Input claims:
    - **inputClaim**: false
- Output claims:
    - **outputClaim**: true

## <a name="orclaims"></a>OrClaims 

Computes an Or of two boolean inputClaims and sets the outputClaim with result of the operation.

| Item | TransformationClaimType | Data Type | Notes |
| ---- | ----------------------- | --------- | ----- |
| InputClaim | inputClaim1 | boolean | The first ClaimType to evaluate. |
| InputClaim | inputClaim2 | boolean | The second ClaimType to evaluate. |
| OutputClaim | outputClaim | boolean | The ClaimTypes that will be produced after this ClaimsTransformation has been invoked (true or false). |

The following claims transformation demonstrates how to `Or` two boolean ClaimTypes. In the orchestration step, you can use a precondition to preset a self-asserted page, if the value of one of the claims is `true`.

```XML
<ClaimsTransformation Id="CheckWhetherEmailBePresented" TransformationMethod="OrClaims">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="isLastTOSAcceptedNotExists" TransformationClaimType="inputClaim1" />
    <InputClaim ClaimTypeReferenceId="isLastTOSAcceptedGreaterThanNow" TransformationClaimType="inputClaim2" />
  </InputClaims>                    
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="presentTOSSelfAsserted" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
</ClaimsTransformation>
```

### <a name="example"></a>Example

- Input claims:
    - **inputClaim1**: true
    - **inputClaim2**: false
- Output claims:
    - **outputClaim**: true
