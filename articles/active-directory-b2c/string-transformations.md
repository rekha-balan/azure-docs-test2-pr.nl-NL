---
title: String claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: String claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 54812ed8b53143d8fa156149bfb2c7adff7da98d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871560"
---
# <a name="string-claims-transformations"></a><span data-ttu-id="8473d-103">String claims transformations</span><span class="sxs-lookup"><span data-stu-id="8473d-103">String claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="8473d-104">This article provides examples for using the string claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="8473d-104">This article provides examples for using the string claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="8473d-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="8473d-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="assertstringclaimsareequal"></a><span data-ttu-id="8473d-106">AssertStringClaimsAreEqual</span><span class="sxs-lookup"><span data-stu-id="8473d-106">AssertStringClaimsAreEqual</span></span> 

<span data-ttu-id="8473d-107">Compare two claims, and throw an exception if they are not equal according to the specified comparison inputClaim1, inputClaim2 and stringComparison.</span><span class="sxs-lookup"><span data-stu-id="8473d-107">Compare two claims, and throw an exception if they are not equal according to the specified comparison inputClaim1, inputClaim2 and stringComparison.</span></span>

| <span data-ttu-id="8473d-108">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-108">Item</span></span> | <span data-ttu-id="8473d-109">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-109">TransformationClaimType</span></span> | <span data-ttu-id="8473d-110">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-110">Data Type</span></span> | <span data-ttu-id="8473d-111">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-111">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-112">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-112">inputClaim</span></span> | <span data-ttu-id="8473d-113">inputClaim1</span><span class="sxs-lookup"><span data-stu-id="8473d-113">inputClaim1</span></span> | <span data-ttu-id="8473d-114">string</span><span class="sxs-lookup"><span data-stu-id="8473d-114">string</span></span> | <span data-ttu-id="8473d-115">First claim's type, which is to be compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-115">First claim's type, which is to be compared.</span></span> |
| <span data-ttu-id="8473d-116">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-116">inputClaim</span></span> | <span data-ttu-id="8473d-117">inputClaim2</span><span class="sxs-lookup"><span data-stu-id="8473d-117">inputClaim2</span></span> | <span data-ttu-id="8473d-118">string</span><span class="sxs-lookup"><span data-stu-id="8473d-118">string</span></span> | <span data-ttu-id="8473d-119">Second claim's type, which is to be compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-119">Second claim's type, which is to be compared.</span></span> |
| <span data-ttu-id="8473d-120">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-120">InputParameter</span></span> | <span data-ttu-id="8473d-121">stringComparison</span><span class="sxs-lookup"><span data-stu-id="8473d-121">stringComparison</span></span> | <span data-ttu-id="8473d-122">string</span><span class="sxs-lookup"><span data-stu-id="8473d-122">string</span></span> | <span data-ttu-id="8473d-123">string comparison, one of the values: Ordinal, OrdinalIgnoreCase.</span><span class="sxs-lookup"><span data-stu-id="8473d-123">string comparison, one of the values: Ordinal, OrdinalIgnoreCase.</span></span> |

<span data-ttu-id="8473d-124">The **AssertStringClaimsAreEqual** claims transformation is always executed from a [validation technical profile](validation-technical-profile.md) that is called by a [self-asserted technical profile](self-asserted-technical-profile.md).</span><span class="sxs-lookup"><span data-stu-id="8473d-124">The **AssertStringClaimsAreEqual** claims transformation is always executed from a [validation technical profile](validation-technical-profile.md) that is called by a [self-asserted technical profile](self-asserted-technical-profile.md).</span></span> <span data-ttu-id="8473d-125">The **UserMessageIfClaimsTransformationStringsAreNotEqual** self-asserted technical profile metadata controls the error message that is presented to the user.</span><span class="sxs-lookup"><span data-stu-id="8473d-125">The **UserMessageIfClaimsTransformationStringsAreNotEqual** self-asserted technical profile metadata controls the error message that is presented to the user.</span></span>

![AssertStringClaimsAreEqual execution](./media/string-transformations/assert-execution.png)

<span data-ttu-id="8473d-127">You can use this claims transformation to make sure, two ClaimTypes have the same value.</span><span class="sxs-lookup"><span data-stu-id="8473d-127">You can use this claims transformation to make sure, two ClaimTypes have the same value.</span></span> <span data-ttu-id="8473d-128">If not, an error message is thrown.</span><span class="sxs-lookup"><span data-stu-id="8473d-128">If not, an error message is thrown.</span></span> <span data-ttu-id="8473d-129">The following example checks that the **strongAuthenticationEmailAddress** ClaimType is equal to **email** ClaimType.</span><span class="sxs-lookup"><span data-stu-id="8473d-129">The following example checks that the **strongAuthenticationEmailAddress** ClaimType is equal to **email** ClaimType.</span></span> <span data-ttu-id="8473d-130">Otherwise an error message is thrown.</span><span class="sxs-lookup"><span data-stu-id="8473d-130">Otherwise an error message is thrown.</span></span> 

```XML
<ClaimsTransformation Id="AssertEmailAndStrongAuthenticationEmailAddressAreEqual" TransformationMethod="AssertStringClaimsAreEqual">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="strongAuthenticationEmailAddress" TransformationClaimType="inputClaim1" />
    <InputClaim ClaimTypeReferenceId="email" TransformationClaimType="inputClaim2" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="stringComparison" DataType="string" Value="ordinalIgnoreCase" />
  </InputParameters>
</ClaimsTransformation>
```


<span data-ttu-id="8473d-131">The **login-NonInteractive** validation technical profile calls the **AssertEmailAndStrongAuthenticationEmailAddressAreEqual** claims transformation.</span><span class="sxs-lookup"><span data-stu-id="8473d-131">The **login-NonInteractive** validation technical profile calls the **AssertEmailAndStrongAuthenticationEmailAddressAreEqual** claims transformation.</span></span>
```XML
<TechnicalProfile Id="login-NonInteractive">
  ...
  <OutputClaimsTransformations>
    <OutputClaimsTransformation ReferenceId="AssertEmailAndStrongAuthenticationEmailAddressAreEqual" />
  </OutputClaimsTransformations>
</TechnicalProfile>
```

<span data-ttu-id="8473d-132">The self-asserted technical profile calls the validation **login-NonInteractive** technical profile.</span><span class="sxs-lookup"><span data-stu-id="8473d-132">The self-asserted technical profile calls the validation **login-NonInteractive** technical profile.</span></span>

```XML
<TechnicalProfile Id="SelfAsserted-LocalAccountSignin-Email">
  <Metadata>
    <Item Key="UserMessageIfClaimsTransformationStringsAreNotEqual">Custom error message the email addresses you provided are not the same.</Item>
  </Metadata>
  <ValidationTechnicalProfiles>
    <ValidationTechnicalProfile ReferenceId="login-NonInteractive" />
  </ValidationTechnicalProfiles>
</TechnicalProfile>
```

### <a name="example"></a><span data-ttu-id="8473d-133">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-133">Example</span></span>

- <span data-ttu-id="8473d-134">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-134">Input claims:</span></span>
    - <span data-ttu-id="8473d-135">**inputClaim1**: someone@contoso.com</span><span class="sxs-lookup"><span data-stu-id="8473d-135">**inputClaim1**: someone@contoso.com</span></span>
    - <span data-ttu-id="8473d-136">**inputClaim2**: someone@outlook.com</span><span class="sxs-lookup"><span data-stu-id="8473d-136">**inputClaim2**: someone@outlook.com</span></span>
 - <span data-ttu-id="8473d-137">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-137">Input parameters:</span></span>
    - <span data-ttu-id="8473d-138">**stringComparison**:  ordinalIgnoreCase</span><span class="sxs-lookup"><span data-stu-id="8473d-138">**stringComparison**:  ordinalIgnoreCase</span></span>
- <span data-ttu-id="8473d-139">Result: Error thrown</span><span class="sxs-lookup"><span data-stu-id="8473d-139">Result: Error thrown</span></span>

## <a name="changecase"></a><span data-ttu-id="8473d-140">ChangeCase</span><span class="sxs-lookup"><span data-stu-id="8473d-140">ChangeCase</span></span> 

<span data-ttu-id="8473d-141">Changes the case of the provided claim to lower or upper case depending on the operator.</span><span class="sxs-lookup"><span data-stu-id="8473d-141">Changes the case of the provided claim to lower or upper case depending on the operator.</span></span>

| <span data-ttu-id="8473d-142">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-142">Item</span></span> | <span data-ttu-id="8473d-143">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-143">TransformationClaimType</span></span> | <span data-ttu-id="8473d-144">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-144">Data Type</span></span> | <span data-ttu-id="8473d-145">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-145">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-146">InputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-146">InputClaim</span></span> | <span data-ttu-id="8473d-147">inputClaim1</span><span class="sxs-lookup"><span data-stu-id="8473d-147">inputClaim1</span></span> | <span data-ttu-id="8473d-148">string</span><span class="sxs-lookup"><span data-stu-id="8473d-148">string</span></span> | <span data-ttu-id="8473d-149">The ClaimType that be changed.</span><span class="sxs-lookup"><span data-stu-id="8473d-149">The ClaimType that be changed.</span></span> |
| <span data-ttu-id="8473d-150">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-150">InputParameter</span></span> | <span data-ttu-id="8473d-151">toCase</span><span class="sxs-lookup"><span data-stu-id="8473d-151">toCase</span></span> | <span data-ttu-id="8473d-152">string</span><span class="sxs-lookup"><span data-stu-id="8473d-152">string</span></span> | <span data-ttu-id="8473d-153">One of the following values: `LOWER` or `UPPER`.</span><span class="sxs-lookup"><span data-stu-id="8473d-153">One of the following values: `LOWER` or `UPPER`.</span></span> |
| <span data-ttu-id="8473d-154">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-154">OutputClaim</span></span> | <span data-ttu-id="8473d-155">outputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-155">outputClaim</span></span> | <span data-ttu-id="8473d-156">string</span><span class="sxs-lookup"><span data-stu-id="8473d-156">string</span></span> | <span data-ttu-id="8473d-157">The ClaimType that is produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="8473d-157">The ClaimType that is produced after this claims transformation has been invoked.</span></span> |

<span data-ttu-id="8473d-158">Use this claim transformation to change any string ClaimType to lower or upper case.</span><span class="sxs-lookup"><span data-stu-id="8473d-158">Use this claim transformation to change any string ClaimType to lower or upper case.</span></span>  

```XML
<ClaimsTransformation Id="ChangeToLower" TransformationMethod="ChangeCase">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="email" TransformationClaimType="inputClaim1" />
  </InputClaims>
<InputParameters>
  <InputParameter Id="toCase" DataType="string" Value="LOWER" />
</InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="email" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-159">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-159">Example</span></span>

- <span data-ttu-id="8473d-160">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-160">Input claims:</span></span>
    - <span data-ttu-id="8473d-161">**email**: SomeOne@contoso.com</span><span class="sxs-lookup"><span data-stu-id="8473d-161">**email**: SomeOne@contoso.com</span></span>
- <span data-ttu-id="8473d-162">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-162">Input parameters:</span></span>
    - <span data-ttu-id="8473d-163">**toCase**: LOWER</span><span class="sxs-lookup"><span data-stu-id="8473d-163">**toCase**: LOWER</span></span>
- <span data-ttu-id="8473d-164">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-164">Output claims:</span></span>
    - <span data-ttu-id="8473d-165">**email**: someone@contoso.com</span><span class="sxs-lookup"><span data-stu-id="8473d-165">**email**: someone@contoso.com</span></span>

## <a name="createstringclaim"></a><span data-ttu-id="8473d-166">CreateStringClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-166">CreateStringClaim</span></span> 

<span data-ttu-id="8473d-167">Creates a string claim from the provided input parameter in the policy.</span><span class="sxs-lookup"><span data-stu-id="8473d-167">Creates a string claim from the provided input parameter in the policy.</span></span>

| <span data-ttu-id="8473d-168">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-168">Item</span></span> | <span data-ttu-id="8473d-169">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-169">TransformationClaimType</span></span> | <span data-ttu-id="8473d-170">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-170">Data Type</span></span> | <span data-ttu-id="8473d-171">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-171">Notes</span></span> |
|----- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-172">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-172">InputParameter</span></span> | <span data-ttu-id="8473d-173">value</span><span class="sxs-lookup"><span data-stu-id="8473d-173">value</span></span> | <span data-ttu-id="8473d-174">string</span><span class="sxs-lookup"><span data-stu-id="8473d-174">string</span></span> | <span data-ttu-id="8473d-175">The string to be set</span><span class="sxs-lookup"><span data-stu-id="8473d-175">The string to be set</span></span> |
| <span data-ttu-id="8473d-176">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-176">OutputClaim</span></span> | <span data-ttu-id="8473d-177">createdClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-177">createdClaim</span></span> | <span data-ttu-id="8473d-178">string</span><span class="sxs-lookup"><span data-stu-id="8473d-178">string</span></span> | <span data-ttu-id="8473d-179">The ClaimType that is produced after this claims transformation has been invoked, with the value specified in the input parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-179">The ClaimType that is produced after this claims transformation has been invoked, with the value specified in the input parameter.</span></span> |

<span data-ttu-id="8473d-180">Use this claims transformation to set a string ClaimType value.</span><span class="sxs-lookup"><span data-stu-id="8473d-180">Use this claims transformation to set a string ClaimType value.</span></span>

```XML
<ClaimsTransformation Id="CreateTermsOfService" TransformationMethod="CreateStringClaim">
  <InputParameters>
    <InputParameter Id="value" DataType="string" Value="Contoso terms of service..." />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="TOS" TransformationClaimType="createdClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-181">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-181">Example</span></span>

- <span data-ttu-id="8473d-182">Input parameter:</span><span class="sxs-lookup"><span data-stu-id="8473d-182">Input parameter:</span></span>
    - <span data-ttu-id="8473d-183">**value**: Contoso terms of service...</span><span class="sxs-lookup"><span data-stu-id="8473d-183">**value**: Contoso terms of service...</span></span>
- <span data-ttu-id="8473d-184">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-184">Output claims:</span></span>
    - <span data-ttu-id="8473d-185">**createdClaim**: The TOS ClaimType contains the "Contoso terms of service..." value.</span><span class="sxs-lookup"><span data-stu-id="8473d-185">**createdClaim**: The TOS ClaimType contains the "Contoso terms of service..." value.</span></span>

## <a name="compareclaims"></a><span data-ttu-id="8473d-186">CompareClaims</span><span class="sxs-lookup"><span data-stu-id="8473d-186">CompareClaims</span></span>

<span data-ttu-id="8473d-187">Determine whether one string claim is equal to another.</span><span class="sxs-lookup"><span data-stu-id="8473d-187">Determine whether one string claim is equal to another.</span></span> <span data-ttu-id="8473d-188">The result is a new boolean ClaimType boolean with a value of `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="8473d-188">The result is a new boolean ClaimType boolean with a value of `true` or `false`.</span></span>

| <span data-ttu-id="8473d-189">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-189">Item</span></span> | <span data-ttu-id="8473d-190">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-190">TransformationClaimType</span></span> | <span data-ttu-id="8473d-191">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-191">Data Type</span></span> | <span data-ttu-id="8473d-192">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-192">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-193">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-193">inputClaim</span></span> | <span data-ttu-id="8473d-194">inputClaim1</span><span class="sxs-lookup"><span data-stu-id="8473d-194">inputClaim1</span></span> | <span data-ttu-id="8473d-195">string</span><span class="sxs-lookup"><span data-stu-id="8473d-195">string</span></span> | <span data-ttu-id="8473d-196">First claim type, which is to be compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-196">First claim type, which is to be compared.</span></span> |
| <span data-ttu-id="8473d-197">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-197">inputClaim</span></span> | <span data-ttu-id="8473d-198">inputClaim2</span><span class="sxs-lookup"><span data-stu-id="8473d-198">inputClaim2</span></span> | <span data-ttu-id="8473d-199">string</span><span class="sxs-lookup"><span data-stu-id="8473d-199">string</span></span> | <span data-ttu-id="8473d-200">Second claim type, which is to be compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-200">Second claim type, which is to be compared.</span></span> |
| <span data-ttu-id="8473d-201">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-201">InputParameter</span></span> | <span data-ttu-id="8473d-202">operator</span><span class="sxs-lookup"><span data-stu-id="8473d-202">operator</span></span> | <span data-ttu-id="8473d-203">string</span><span class="sxs-lookup"><span data-stu-id="8473d-203">string</span></span> | <span data-ttu-id="8473d-204">Possible values: `Equal` or `Not Equal`.</span><span class="sxs-lookup"><span data-stu-id="8473d-204">Possible values: `Equal` or `Not Equal`.</span></span> |
| <span data-ttu-id="8473d-205">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-205">InputParameter</span></span> | <span data-ttu-id="8473d-206">ignoreCase</span><span class="sxs-lookup"><span data-stu-id="8473d-206">ignoreCase</span></span> | <span data-ttu-id="8473d-207">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-207">boolean</span></span> | <span data-ttu-id="8473d-208">Specifies whether this comparison should ignore the case of the strings being compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-208">Specifies whether this comparison should ignore the case of the strings being compared.</span></span> |
| <span data-ttu-id="8473d-209">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-209">OutputClaim</span></span> | <span data-ttu-id="8473d-210">outputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-210">outputClaim</span></span> | <span data-ttu-id="8473d-211">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-211">boolean</span></span> | <span data-ttu-id="8473d-212">The ClaimType that is produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="8473d-212">The ClaimType that is produced after this claims transformation has been invoked.</span></span> |

<span data-ttu-id="8473d-213">Use this claims transformation to check if a claim is equal to another claim.</span><span class="sxs-lookup"><span data-stu-id="8473d-213">Use this claims transformation to check if a claim is equal to another claim.</span></span> <span data-ttu-id="8473d-214">For example, the following claims transformation checks if the value of the **email** claim is equal to the **Verified.Email** claim.</span><span class="sxs-lookup"><span data-stu-id="8473d-214">For example, the following claims transformation checks if the value of the **email** claim is equal to the **Verified.Email** claim.</span></span>

```XML
<ClaimsTransformation Id="CheckEmail" TransformationMethod="CompareClaims">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="Email" TransformationClaimType="inputClaim1" />
    <InputClaim ClaimTypeReferenceId="Verified.Email" TransformationClaimType="inputClaim2" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="operator" DataType="string" Value="NOT EQUAL" />
    <InputParameter Id="ignoreCase" DataType="string" Value="true" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="SameEmailAddress" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-215">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-215">Example</span></span>

- <span data-ttu-id="8473d-216">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-216">Input claims:</span></span>
    - <span data-ttu-id="8473d-217">**inputClaim1**: someone@contoso.com</span><span class="sxs-lookup"><span data-stu-id="8473d-217">**inputClaim1**: someone@contoso.com</span></span>
    - <span data-ttu-id="8473d-218">**inputClaim2**: someone@outlook.com</span><span class="sxs-lookup"><span data-stu-id="8473d-218">**inputClaim2**: someone@outlook.com</span></span>
- <span data-ttu-id="8473d-219">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-219">Input parameters:</span></span>
    - <span data-ttu-id="8473d-220">**operator**:  NOT EQUAL</span><span class="sxs-lookup"><span data-stu-id="8473d-220">**operator**:  NOT EQUAL</span></span>
    - <span data-ttu-id="8473d-221">**ignoreCase**: true</span><span class="sxs-lookup"><span data-stu-id="8473d-221">**ignoreCase**: true</span></span>
- <span data-ttu-id="8473d-222">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-222">Output claims:</span></span>
    - <span data-ttu-id="8473d-223">**outputClaim**: true</span><span class="sxs-lookup"><span data-stu-id="8473d-223">**outputClaim**: true</span></span>

## <a name="compareclaimtovalue"></a><span data-ttu-id="8473d-224">CompareClaimToValue</span><span class="sxs-lookup"><span data-stu-id="8473d-224">CompareClaimToValue</span></span>

<span data-ttu-id="8473d-225">Determines whether a claim value is equal to the input parameter value.</span><span class="sxs-lookup"><span data-stu-id="8473d-225">Determines whether a claim value is equal to the input parameter value.</span></span>

| <span data-ttu-id="8473d-226">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-226">Item</span></span> | <span data-ttu-id="8473d-227">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-227">TransformationClaimType</span></span> | <span data-ttu-id="8473d-228">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-228">Data Type</span></span> | <span data-ttu-id="8473d-229">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-229">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-230">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-230">inputClaim</span></span> | <span data-ttu-id="8473d-231">inputClaim1</span><span class="sxs-lookup"><span data-stu-id="8473d-231">inputClaim1</span></span> | <span data-ttu-id="8473d-232">string</span><span class="sxs-lookup"><span data-stu-id="8473d-232">string</span></span> | <span data-ttu-id="8473d-233">The claim's type, which is to be compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-233">The claim's type, which is to be compared.</span></span> |
| <span data-ttu-id="8473d-234">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-234">InputParameter</span></span> | <span data-ttu-id="8473d-235">operator</span><span class="sxs-lookup"><span data-stu-id="8473d-235">operator</span></span> | <span data-ttu-id="8473d-236">string</span><span class="sxs-lookup"><span data-stu-id="8473d-236">string</span></span> | <span data-ttu-id="8473d-237">Possible values: `Equal` or `Not Equal`.</span><span class="sxs-lookup"><span data-stu-id="8473d-237">Possible values: `Equal` or `Not Equal`.</span></span> |
| <span data-ttu-id="8473d-238">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-238">InputParameter</span></span> | <span data-ttu-id="8473d-239">compareTo</span><span class="sxs-lookup"><span data-stu-id="8473d-239">compareTo</span></span> | <span data-ttu-id="8473d-240">string</span><span class="sxs-lookup"><span data-stu-id="8473d-240">string</span></span> | <span data-ttu-id="8473d-241">string comparison, one of the values: Ordinal, OrdinalIgnoreCase.</span><span class="sxs-lookup"><span data-stu-id="8473d-241">string comparison, one of the values: Ordinal, OrdinalIgnoreCase.</span></span> |
| <span data-ttu-id="8473d-242">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-242">InputParameter</span></span> | <span data-ttu-id="8473d-243">ignoreCase</span><span class="sxs-lookup"><span data-stu-id="8473d-243">ignoreCase</span></span> | <span data-ttu-id="8473d-244">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-244">boolean</span></span> | <span data-ttu-id="8473d-245">Specifies whether this comparison should ignore the case of the strings being compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-245">Specifies whether this comparison should ignore the case of the strings being compared.</span></span> |
| <span data-ttu-id="8473d-246">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-246">OutputClaim</span></span> | <span data-ttu-id="8473d-247">outputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-247">outputClaim</span></span> | <span data-ttu-id="8473d-248">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-248">boolean</span></span> | <span data-ttu-id="8473d-249">The ClaimType that is produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="8473d-249">The ClaimType that is produced after this claims transformation has been invoked.</span></span> |

<span data-ttu-id="8473d-250">You can use this claims transformation to check if a claim is equal to a value you specified.</span><span class="sxs-lookup"><span data-stu-id="8473d-250">You can use this claims transformation to check if a claim is equal to a value you specified.</span></span> <span data-ttu-id="8473d-251">For example, the following claims transformation checks if the value of the **termsOfUseConsentVersion** claim is equal to `v1`.</span><span class="sxs-lookup"><span data-stu-id="8473d-251">For example, the following claims transformation checks if the value of the **termsOfUseConsentVersion** claim is equal to `v1`.</span></span>

```XML
<ClaimsTransformation Id="IsTermsOfUseConsentRequiredForVersion" TransformationMethod="CompareClaimToValue">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="termsOfUseConsentVersion" TransformationClaimType="inputClaim1" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="compareTo" DataType="string" Value="V1" />
    <InputParameter Id="operator" DataType="string" Value="not equal" />
    <InputParameter Id="ignoreCase" DataType="string" Value="true" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="termsOfUseConsentRequired" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-252">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-252">Example</span></span>
- <span data-ttu-id="8473d-253">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-253">Input claims:</span></span>
    - <span data-ttu-id="8473d-254">**inputClaim1**: v1</span><span class="sxs-lookup"><span data-stu-id="8473d-254">**inputClaim1**: v1</span></span>
- <span data-ttu-id="8473d-255">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-255">Input parameters:</span></span>
    - <span data-ttu-id="8473d-256">**compareTo**: V1</span><span class="sxs-lookup"><span data-stu-id="8473d-256">**compareTo**: V1</span></span>
    - <span data-ttu-id="8473d-257">**operator**: equal</span><span class="sxs-lookup"><span data-stu-id="8473d-257">**operator**: equal</span></span> 
    - <span data-ttu-id="8473d-258">**ignoreCase**:  true</span><span class="sxs-lookup"><span data-stu-id="8473d-258">**ignoreCase**:  true</span></span>
- <span data-ttu-id="8473d-259">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-259">Output claims:</span></span>
    - <span data-ttu-id="8473d-260">**outputClaim**: true</span><span class="sxs-lookup"><span data-stu-id="8473d-260">**outputClaim**: true</span></span>

## <a name="createrandomstring"></a><span data-ttu-id="8473d-261">CreateRandomString</span><span class="sxs-lookup"><span data-stu-id="8473d-261">CreateRandomString</span></span>

<span data-ttu-id="8473d-262">Creates a random string using the random number generator.</span><span class="sxs-lookup"><span data-stu-id="8473d-262">Creates a random string using the random number generator.</span></span> <span data-ttu-id="8473d-263">If the random number generator is of type `integer`, optionally a seed parameter and a maximum number may be provided.</span><span class="sxs-lookup"><span data-stu-id="8473d-263">If the random number generator is of type `integer`, optionally a seed parameter and a maximum number may be provided.</span></span> <span data-ttu-id="8473d-264">An optional string format parameter allows the output to be formatted using it, and an optional base64 parameter specifies whether the output is base64 encoded randomGeneratorType [guid, integer] outputClaim (String).</span><span class="sxs-lookup"><span data-stu-id="8473d-264">An optional string format parameter allows the output to be formatted using it, and an optional base64 parameter specifies whether the output is base64 encoded randomGeneratorType [guid, integer] outputClaim (String).</span></span>

| <span data-ttu-id="8473d-265">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-265">Item</span></span> | <span data-ttu-id="8473d-266">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-266">TransformationClaimType</span></span> | <span data-ttu-id="8473d-267">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-267">Data Type</span></span> | <span data-ttu-id="8473d-268">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-268">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-269">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-269">InputParameter</span></span> | <span data-ttu-id="8473d-270">randomGeneratorType</span><span class="sxs-lookup"><span data-stu-id="8473d-270">randomGeneratorType</span></span> | <span data-ttu-id="8473d-271">string</span><span class="sxs-lookup"><span data-stu-id="8473d-271">string</span></span> | <span data-ttu-id="8473d-272">Specifies the random value to be generated, `GUID` (global unique ID) or `integer` (a number).</span><span class="sxs-lookup"><span data-stu-id="8473d-272">Specifies the random value to be generated, `GUID` (global unique ID) or `integer` (a number).</span></span> |
| <span data-ttu-id="8473d-273">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-273">InputParameter</span></span> | <span data-ttu-id="8473d-274">stringFormat</span><span class="sxs-lookup"><span data-stu-id="8473d-274">stringFormat</span></span> | <span data-ttu-id="8473d-275">string</span><span class="sxs-lookup"><span data-stu-id="8473d-275">string</span></span> | <span data-ttu-id="8473d-276">[Optional] Format the random value.</span><span class="sxs-lookup"><span data-stu-id="8473d-276">[Optional] Format the random value.</span></span> |
| <span data-ttu-id="8473d-277">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-277">InputParameter</span></span> | <span data-ttu-id="8473d-278">base64</span><span class="sxs-lookup"><span data-stu-id="8473d-278">base64</span></span> | <span data-ttu-id="8473d-279">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-279">boolean</span></span> | <span data-ttu-id="8473d-280">[Optional] Convert the random value to base64.</span><span class="sxs-lookup"><span data-stu-id="8473d-280">[Optional] Convert the random value to base64.</span></span> <span data-ttu-id="8473d-281">If string format is applied, the value after string format is encoded to base64.</span><span class="sxs-lookup"><span data-stu-id="8473d-281">If string format is applied, the value after string format is encoded to base64.</span></span> |
| <span data-ttu-id="8473d-282">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-282">InputParameter</span></span> | <span data-ttu-id="8473d-283">maximumNumber</span><span class="sxs-lookup"><span data-stu-id="8473d-283">maximumNumber</span></span> | <span data-ttu-id="8473d-284">int</span><span class="sxs-lookup"><span data-stu-id="8473d-284">int</span></span> | <span data-ttu-id="8473d-285">[Optional] For `Integer` randomGeneratorType only.</span><span class="sxs-lookup"><span data-stu-id="8473d-285">[Optional] For `Integer` randomGeneratorType only.</span></span> <span data-ttu-id="8473d-286">Specify the maximute number.</span><span class="sxs-lookup"><span data-stu-id="8473d-286">Specify the maximute number.</span></span> |
| <span data-ttu-id="8473d-287">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-287">InputParameter</span></span> | <span data-ttu-id="8473d-288">seed</span><span class="sxs-lookup"><span data-stu-id="8473d-288">seed</span></span>  | <span data-ttu-id="8473d-289">int</span><span class="sxs-lookup"><span data-stu-id="8473d-289">int</span></span> | <span data-ttu-id="8473d-290">[Optional] For `Integer` randomGeneratorType only.</span><span class="sxs-lookup"><span data-stu-id="8473d-290">[Optional] For `Integer` randomGeneratorType only.</span></span> <span data-ttu-id="8473d-291">Specify the seed for the random value.</span><span class="sxs-lookup"><span data-stu-id="8473d-291">Specify the seed for the random value.</span></span> <span data-ttu-id="8473d-292">Note: same seed yields same sequence of random numbers.</span><span class="sxs-lookup"><span data-stu-id="8473d-292">Note: same seed yields same sequence of random numbers.</span></span> |
| <span data-ttu-id="8473d-293">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-293">OutputClaim</span></span> | <span data-ttu-id="8473d-294">outputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-294">outputClaim</span></span> | <span data-ttu-id="8473d-295">string</span><span class="sxs-lookup"><span data-stu-id="8473d-295">string</span></span> | <span data-ttu-id="8473d-296">The ClaimTypes that will be produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="8473d-296">The ClaimTypes that will be produced after this claims transformation has been invoked.</span></span> <span data-ttu-id="8473d-297">The random value.</span><span class="sxs-lookup"><span data-stu-id="8473d-297">The random value.</span></span> |

<span data-ttu-id="8473d-298">Following example generates a global unique ID.</span><span class="sxs-lookup"><span data-stu-id="8473d-298">Following example generates a global unique ID.</span></span> <span data-ttu-id="8473d-299">This claims transformation is used to create the random UPN (user principle name).</span><span class="sxs-lookup"><span data-stu-id="8473d-299">This claims transformation is used to create the random UPN (user principle name).</span></span>

```XML
<ClaimsTransformation Id="CreateRandomUPNUserName" TransformationMethod="CreateRandomString">
  <InputParameters>
    <InputParameter Id="randomGeneratorType" DataType="string" Value="GUID" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="upnUserName" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```
### <a name="example"></a><span data-ttu-id="8473d-300">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-300">Example</span></span>

- <span data-ttu-id="8473d-301">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-301">Input parameters:</span></span>
    - <span data-ttu-id="8473d-302">**randomGeneratorType**: GUID</span><span class="sxs-lookup"><span data-stu-id="8473d-302">**randomGeneratorType**: GUID</span></span>
- <span data-ttu-id="8473d-303">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-303">Output claims:</span></span> 
    - <span data-ttu-id="8473d-304">**outputClaim**: bc8bedd2-aaa3-411e-bdee-2f1810b73dfc</span><span class="sxs-lookup"><span data-stu-id="8473d-304">**outputClaim**: bc8bedd2-aaa3-411e-bdee-2f1810b73dfc</span></span>

<span data-ttu-id="8473d-305">Following example generates an integer random value between 0 and 1000.</span><span class="sxs-lookup"><span data-stu-id="8473d-305">Following example generates an integer random value between 0 and 1000.</span></span> <span data-ttu-id="8473d-306">The value is formatted to OTP_{random value}.</span><span class="sxs-lookup"><span data-stu-id="8473d-306">The value is formatted to OTP_{random value}.</span></span>

```XML
<ClaimsTransformation Id="SetRandomNumber" TransformationMethod="CreateRandomString">
  <InputParameters>
    <InputParameter Id="randomGeneratorType" DataType="string" Value="integer" />
    <InputParameter Id="maximumNumber" DataType="int" Value="1000" />
    <InputParameter Id="stringFormat" DataType="string" Value="OTP_{0}" />
    <InputParameter Id="base64" DataType="boolean" Value="false" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="randomNumber" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-307">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-307">Example</span></span>

- <span data-ttu-id="8473d-308">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-308">Input parameters:</span></span>
    - <span data-ttu-id="8473d-309">**randomGeneratorType**: integer</span><span class="sxs-lookup"><span data-stu-id="8473d-309">**randomGeneratorType**: integer</span></span>
    - <span data-ttu-id="8473d-310">**maximumNumber**: 1000</span><span class="sxs-lookup"><span data-stu-id="8473d-310">**maximumNumber**: 1000</span></span>
    - <span data-ttu-id="8473d-311">**stringFormat**: OTP_{0}</span><span class="sxs-lookup"><span data-stu-id="8473d-311">**stringFormat**: OTP_{0}</span></span>
    - <span data-ttu-id="8473d-312">**base64**: false</span><span class="sxs-lookup"><span data-stu-id="8473d-312">**base64**: false</span></span>
- <span data-ttu-id="8473d-313">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-313">Output claims:</span></span> 
    - <span data-ttu-id="8473d-314">**outputClaim**: OTP_853</span><span class="sxs-lookup"><span data-stu-id="8473d-314">**outputClaim**: OTP_853</span></span>


## <a name="formatstringclaim"></a><span data-ttu-id="8473d-315">FormatStringClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-315">FormatStringClaim</span></span>

<span data-ttu-id="8473d-316">Format a claim according to the provided format string.</span><span class="sxs-lookup"><span data-stu-id="8473d-316">Format a claim according to the provided format string.</span></span> <span data-ttu-id="8473d-317">This transformation uses the C# `String.Format` method.</span><span class="sxs-lookup"><span data-stu-id="8473d-317">This transformation uses the C# `String.Format` method.</span></span>

| <span data-ttu-id="8473d-318">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-318">Item</span></span> | <span data-ttu-id="8473d-319">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-319">TransformationClaimType</span></span> | <span data-ttu-id="8473d-320">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-320">Data Type</span></span> | <span data-ttu-id="8473d-321">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-321">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-322">InputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-322">InputClaim</span></span> | <span data-ttu-id="8473d-323">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-323">inputClaim</span></span> |<span data-ttu-id="8473d-324">string</span><span class="sxs-lookup"><span data-stu-id="8473d-324">string</span></span> |<span data-ttu-id="8473d-325">The ClaimType that acts as string format {0} parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-325">The ClaimType that acts as string format {0} parameter.</span></span> |
| <span data-ttu-id="8473d-326">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-326">InputParameter</span></span> | <span data-ttu-id="8473d-327">stringFormat</span><span class="sxs-lookup"><span data-stu-id="8473d-327">stringFormat</span></span> | <span data-ttu-id="8473d-328">string</span><span class="sxs-lookup"><span data-stu-id="8473d-328">string</span></span> | <span data-ttu-id="8473d-329">The string format, including the {0}  parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-329">The string format, including the {0}  parameter.</span></span> |
| <span data-ttu-id="8473d-330">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-330">OutputClaim</span></span> | <span data-ttu-id="8473d-331">outputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-331">outputClaim</span></span> | <span data-ttu-id="8473d-332">string</span><span class="sxs-lookup"><span data-stu-id="8473d-332">string</span></span> | <span data-ttu-id="8473d-333">The ClaimType that is produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="8473d-333">The ClaimType that is produced after this claims transformation has been invoked.</span></span> |

<span data-ttu-id="8473d-334">Use this claims transformation to format any string with one parameter {0}.</span><span class="sxs-lookup"><span data-stu-id="8473d-334">Use this claims transformation to format any string with one parameter {0}.</span></span> <span data-ttu-id="8473d-335">The following example creates a **userPrincipalName**.</span><span class="sxs-lookup"><span data-stu-id="8473d-335">The following example creates a **userPrincipalName**.</span></span> <span data-ttu-id="8473d-336">All social identity provider technical profiles, such as `Facebook-OAUTH` calls the **CreateUserPrincipalName** to generate a **userPrincipalName**.</span><span class="sxs-lookup"><span data-stu-id="8473d-336">All social identity provider technical profiles, such as `Facebook-OAUTH` calls the **CreateUserPrincipalName** to generate a **userPrincipalName**.</span></span>   

```XML
<ClaimsTransformation Id="CreateUserPrincipalName" TransformationMethod="FormatStringClaim">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="upnUserName" TransformationClaimType="inputClaim" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="stringFormat" DataType="string" Value="cpim_{0}@{RelyingPartyTenantId}" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="userPrincipalName" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-337">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-337">Example</span></span>

- <span data-ttu-id="8473d-338">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-338">Input claims:</span></span>
    - <span data-ttu-id="8473d-339">**inputClaim**: 5164db16-3eee-4629-bfda-dcc3326790e9</span><span class="sxs-lookup"><span data-stu-id="8473d-339">**inputClaim**: 5164db16-3eee-4629-bfda-dcc3326790e9</span></span>
- <span data-ttu-id="8473d-340">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-340">Input parameters:</span></span>
    - <span data-ttu-id="8473d-341">**stringFormat**:  cpim_{0}@{RelyingPartyTenantId}</span><span class="sxs-lookup"><span data-stu-id="8473d-341">**stringFormat**:  cpim_{0}@{RelyingPartyTenantId}</span></span>
- <span data-ttu-id="8473d-342">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-342">Output claims:</span></span>
    - <span data-ttu-id="8473d-343">**outputClaim**: cpim_5164db16-3eee-4629-bfda-dcc3326790e9@b2cdemo.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="8473d-343">**outputClaim**: cpim_5164db16-3eee-4629-bfda-dcc3326790e9@b2cdemo.onmicrosoft.com</span></span>

## <a name="formatstringmultipleclaims"></a><span data-ttu-id="8473d-344">FormatStringMultipleClaims</span><span class="sxs-lookup"><span data-stu-id="8473d-344">FormatStringMultipleClaims</span></span>

<span data-ttu-id="8473d-345">Format two claims according to the provided format string.</span><span class="sxs-lookup"><span data-stu-id="8473d-345">Format two claims according to the provided format string.</span></span> <span data-ttu-id="8473d-346">This transformation uses the C# **String.Format** method.</span><span class="sxs-lookup"><span data-stu-id="8473d-346">This transformation uses the C# **String.Format** method.</span></span>

| <span data-ttu-id="8473d-347">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-347">Item</span></span> | <span data-ttu-id="8473d-348">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-348">TransformationClaimType</span></span> | <span data-ttu-id="8473d-349">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-349">Data Type</span></span> | <span data-ttu-id="8473d-350">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-350">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-351">InputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-351">InputClaim</span></span> | <span data-ttu-id="8473d-352">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-352">inputClaim</span></span> |<span data-ttu-id="8473d-353">string</span><span class="sxs-lookup"><span data-stu-id="8473d-353">string</span></span> | <span data-ttu-id="8473d-354">The ClaimType that acts as string format {0} parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-354">The ClaimType that acts as string format {0} parameter.</span></span> |
| <span data-ttu-id="8473d-355">InputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-355">InputClaim</span></span> | <span data-ttu-id="8473d-356">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-356">inputClaim</span></span> | <span data-ttu-id="8473d-357">string</span><span class="sxs-lookup"><span data-stu-id="8473d-357">string</span></span> | <span data-ttu-id="8473d-358">The ClaimType that acts as string format {1} parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-358">The ClaimType that acts as string format {1} parameter.</span></span> |
| <span data-ttu-id="8473d-359">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-359">InputParameter</span></span> | <span data-ttu-id="8473d-360">stringFormat</span><span class="sxs-lookup"><span data-stu-id="8473d-360">stringFormat</span></span> | <span data-ttu-id="8473d-361">string</span><span class="sxs-lookup"><span data-stu-id="8473d-361">string</span></span> | <span data-ttu-id="8473d-362">The string format, including the {0} and {1} parameters.</span><span class="sxs-lookup"><span data-stu-id="8473d-362">The string format, including the {0} and {1} parameters.</span></span> |
| <span data-ttu-id="8473d-363">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-363">OutputClaim</span></span> | <span data-ttu-id="8473d-364">outputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-364">outputClaim</span></span> | <span data-ttu-id="8473d-365">string</span><span class="sxs-lookup"><span data-stu-id="8473d-365">string</span></span> | <span data-ttu-id="8473d-366">The ClaimType that is produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="8473d-366">The ClaimType that is produced after this claims transformation has been invoked.</span></span> |

<span data-ttu-id="8473d-367">Use this claims transformation to format any string with two parameters, {0} and {1}.</span><span class="sxs-lookup"><span data-stu-id="8473d-367">Use this claims transformation to format any string with two parameters, {0} and {1}.</span></span> <span data-ttu-id="8473d-368">The following example creates a **displayName** with the specified format:</span><span class="sxs-lookup"><span data-stu-id="8473d-368">The following example creates a **displayName** with the specified format:</span></span>

```XML
<ClaimsTransformation Id="CreateDisplayNameFromFirstNameAndLastName" TransformationMethod="FormatStringMultipleClaims">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="givenName" TransformationClaimType="inputClaim1" />
    <InputClaim ClaimTypeReferenceId="surName" TransformationClaimType="inputClaim2" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="stringFormat" DataType="string" Value="{0} {1}" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="displayName" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-369">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-369">Example</span></span>

- <span data-ttu-id="8473d-370">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-370">Input claims:</span></span>
    - <span data-ttu-id="8473d-371">**inputClaim1**: Joe</span><span class="sxs-lookup"><span data-stu-id="8473d-371">**inputClaim1**: Joe</span></span>
    - <span data-ttu-id="8473d-372">**inputClaim2**: Fernando</span><span class="sxs-lookup"><span data-stu-id="8473d-372">**inputClaim2**: Fernando</span></span>
- <span data-ttu-id="8473d-373">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-373">Input parameters:</span></span>
    - <span data-ttu-id="8473d-374">**stringFormat**: {0} {1}</span><span class="sxs-lookup"><span data-stu-id="8473d-374">**stringFormat**: {0} {1}</span></span>
- <span data-ttu-id="8473d-375">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-375">Output claims:</span></span>
    - <span data-ttu-id="8473d-376">**outputClaim**: Joe Fernando</span><span class="sxs-lookup"><span data-stu-id="8473d-376">**outputClaim**: Joe Fernando</span></span>

## <a name="getmappedvaluefromlocalizedcollection"></a><span data-ttu-id="8473d-377">GetMappedValueFromLocalizedCollection</span><span class="sxs-lookup"><span data-stu-id="8473d-377">GetMappedValueFromLocalizedCollection</span></span>

<span data-ttu-id="8473d-378">Looking up an item from a claim **Restriction** collection.</span><span class="sxs-lookup"><span data-stu-id="8473d-378">Looking up an item from a claim **Restriction** collection.</span></span>

| <span data-ttu-id="8473d-379">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-379">Item</span></span> | <span data-ttu-id="8473d-380">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-380">TransformationClaimType</span></span> | <span data-ttu-id="8473d-381">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-381">Data Type</span></span> | <span data-ttu-id="8473d-382">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-382">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-383">InputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-383">InputClaim</span></span> | <span data-ttu-id="8473d-384">mapFromClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-384">mapFromClaim</span></span> | <span data-ttu-id="8473d-385">string</span><span class="sxs-lookup"><span data-stu-id="8473d-385">string</span></span> | <span data-ttu-id="8473d-386">The claim that contains the text to be looked up in the **restrictionValueClaim** claims with the **Restriction** collection.</span><span class="sxs-lookup"><span data-stu-id="8473d-386">The claim that contains the text to be looked up in the **restrictionValueClaim** claims with the **Restriction** collection.</span></span>  |
| <span data-ttu-id="8473d-387">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-387">OutputClaim</span></span> | <span data-ttu-id="8473d-388">restrictionValueClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-388">restrictionValueClaim</span></span> | <span data-ttu-id="8473d-389">string</span><span class="sxs-lookup"><span data-stu-id="8473d-389">string</span></span> | <span data-ttu-id="8473d-390">The claim that contains the **Restriction** collection.</span><span class="sxs-lookup"><span data-stu-id="8473d-390">The claim that contains the **Restriction** collection.</span></span> <span data-ttu-id="8473d-391">After the claims transformation has been invoked, the value of this claim contains the value of the selected item.</span><span class="sxs-lookup"><span data-stu-id="8473d-391">After the claims transformation has been invoked, the value of this claim contains the value of the selected item.</span></span> |

<span data-ttu-id="8473d-392">The following example looks up the error message description based on the error key.</span><span class="sxs-lookup"><span data-stu-id="8473d-392">The following example looks up the error message description based on the error key.</span></span> <span data-ttu-id="8473d-393">The **responseMsg** claim contains a collection of error messages to present to the end user or to be sent to the relying party.</span><span class="sxs-lookup"><span data-stu-id="8473d-393">The **responseMsg** claim contains a collection of error messages to present to the end user or to be sent to the relying party.</span></span>

```XML
<ClaimType Id="responseMsg">
  <DisplayName>Error message: </DisplayName>
  <DataType>string</DataType>
  <UserInputType>Paragraph</UserInputType>
  <Restriction>
    <Enumeration Text="B2C_V1_90001" Value="You cant sign in because you are a minor" />
    <Enumeration Text="B2C_V1_90002" Value="This action can only be performed by gold members" />
    <Enumeration Text="B2C_V1_90003" Value="You have not been enabled for this operation" />
  </Restriction>
</ClaimType>
```
<span data-ttu-id="8473d-394">The claims transformation looks up the text of the item and returns its value.</span><span class="sxs-lookup"><span data-stu-id="8473d-394">The claims transformation looks up the text of the item and returns its value.</span></span> <span data-ttu-id="8473d-395">If the restriction is localized using `<LocalizedCollection>`, the claims transformation returns the localized value.</span><span class="sxs-lookup"><span data-stu-id="8473d-395">If the restriction is localized using `<LocalizedCollection>`, the claims transformation returns the localized value.</span></span>

```XML
<ClaimsTransformation Id="GetResponseMsgMappedToResponseCode" TransformationMethod="GetMappedValueFromLocalizedCollection">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="responseCode" TransformationClaimType="mapFromClaim" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="responseMsg" TransformationClaimType="restrictionValueClaim" />         
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-396">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-396">Example</span></span>

- <span data-ttu-id="8473d-397">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-397">Input claims:</span></span>
    - <span data-ttu-id="8473d-398">**mapFromClaim**: B2C_V1_90001</span><span class="sxs-lookup"><span data-stu-id="8473d-398">**mapFromClaim**: B2C_V1_90001</span></span>
- <span data-ttu-id="8473d-399">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-399">Output claims:</span></span>
    - <span data-ttu-id="8473d-400">**restrictionValueClaim**: You cant sign in because you are a minor.</span><span class="sxs-lookup"><span data-stu-id="8473d-400">**restrictionValueClaim**: You cant sign in because you are a minor.</span></span>

## <a name="lookupvalue"></a><span data-ttu-id="8473d-401">LookupValue</span><span class="sxs-lookup"><span data-stu-id="8473d-401">LookupValue</span></span>

<span data-ttu-id="8473d-402">Look up a claim value from a list of values based on the value of another claim.</span><span class="sxs-lookup"><span data-stu-id="8473d-402">Look up a claim value from a list of values based on the value of another claim.</span></span>

| <span data-ttu-id="8473d-403">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-403">Item</span></span> | <span data-ttu-id="8473d-404">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-404">TransformationClaimType</span></span> | <span data-ttu-id="8473d-405">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-405">Data Type</span></span> | <span data-ttu-id="8473d-406">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-406">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-407">InputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-407">InputClaim</span></span> | <span data-ttu-id="8473d-408">inputParameterId</span><span class="sxs-lookup"><span data-stu-id="8473d-408">inputParameterId</span></span> | <span data-ttu-id="8473d-409">string</span><span class="sxs-lookup"><span data-stu-id="8473d-409">string</span></span> | <span data-ttu-id="8473d-410">The claim that contains the lookup value</span><span class="sxs-lookup"><span data-stu-id="8473d-410">The claim that contains the lookup value</span></span> |
| <span data-ttu-id="8473d-411">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-411">InputParameter</span></span> | |<span data-ttu-id="8473d-412">string</span><span class="sxs-lookup"><span data-stu-id="8473d-412">string</span></span> | <span data-ttu-id="8473d-413">Collection of inputParameters.</span><span class="sxs-lookup"><span data-stu-id="8473d-413">Collection of inputParameters.</span></span> |
| <span data-ttu-id="8473d-414">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-414">InputParameter</span></span> | <span data-ttu-id="8473d-415">errorOnFailedLookup</span><span class="sxs-lookup"><span data-stu-id="8473d-415">errorOnFailedLookup</span></span> | <span data-ttu-id="8473d-416">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-416">boolean</span></span> | <span data-ttu-id="8473d-417">Controlling whether an error is returned when no matching lookup.</span><span class="sxs-lookup"><span data-stu-id="8473d-417">Controlling whether an error is returned when no matching lookup.</span></span> |
| <span data-ttu-id="8473d-418">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-418">OutputClaim</span></span> | <span data-ttu-id="8473d-419">inputParameterId</span><span class="sxs-lookup"><span data-stu-id="8473d-419">inputParameterId</span></span> | <span data-ttu-id="8473d-420">string</span><span class="sxs-lookup"><span data-stu-id="8473d-420">string</span></span> | <span data-ttu-id="8473d-421">The ClaimTypes that will be produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="8473d-421">The ClaimTypes that will be produced after this claims transformation has been invoked.</span></span> <span data-ttu-id="8473d-422">The value of the matching Id.</span><span class="sxs-lookup"><span data-stu-id="8473d-422">The value of the matching Id.</span></span> |

<span data-ttu-id="8473d-423">The following example looks up the domain name in one of the inpuParameters collections.</span><span class="sxs-lookup"><span data-stu-id="8473d-423">The following example looks up the domain name in one of the inpuParameters collections.</span></span> <span data-ttu-id="8473d-424">The claims transformation looks up the domain name in the identifier and returns its value (an application ID).</span><span class="sxs-lookup"><span data-stu-id="8473d-424">The claims transformation looks up the domain name in the identifier and returns its value (an application ID).</span></span>

```XML
 <ClaimsTransformation Id="DomainToClientId" TransformationMethod="LookupValue">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="domainName" TransformationClaimType="inputParameterId" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="contoso.com" DataType="string" Value="13c15f79-8fb1-4e29-a6c9-be0d36ff19f1" />
    <InputParameter Id="microsoft.com" DataType="string" Value="0213308f-17cb-4398-b97e-01da7bd4804e" />
    <InputParameter Id="test.com" DataType="string" Value="c7026f88-4299-4cdb-965d-3f166464b8a9" />
    <InputParameter Id="errorOnFailedLookup" DataType="boolean" Value="false" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="domainAppId" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation> 
```

### <a name="example"></a><span data-ttu-id="8473d-425">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-425">Example</span></span>

- <span data-ttu-id="8473d-426">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-426">Input claims:</span></span>
    - <span data-ttu-id="8473d-427">**inputParameterId**: test.com</span><span class="sxs-lookup"><span data-stu-id="8473d-427">**inputParameterId**: test.com</span></span>
- <span data-ttu-id="8473d-428">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-428">Input parameters:</span></span>
    - <span data-ttu-id="8473d-429">**contoso.com**: 13c15f79-8fb1-4e29-a6c9-be0d36ff19f1</span><span class="sxs-lookup"><span data-stu-id="8473d-429">**contoso.com**: 13c15f79-8fb1-4e29-a6c9-be0d36ff19f1</span></span>
    - <span data-ttu-id="8473d-430">**microsoft.com**: 0213308f-17cb-4398-b97e-01da7bd4804e</span><span class="sxs-lookup"><span data-stu-id="8473d-430">**microsoft.com**: 0213308f-17cb-4398-b97e-01da7bd4804e</span></span>
    - <span data-ttu-id="8473d-431">**test.com**: c7026f88-4299-4cdb-965d-3f166464b8a9</span><span class="sxs-lookup"><span data-stu-id="8473d-431">**test.com**: c7026f88-4299-4cdb-965d-3f166464b8a9</span></span>
    - <span data-ttu-id="8473d-432">**errorOnFailedLookup**: false</span><span class="sxs-lookup"><span data-stu-id="8473d-432">**errorOnFailedLookup**: false</span></span>
- <span data-ttu-id="8473d-433">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-433">Output claims:</span></span>
    - <span data-ttu-id="8473d-434">**outputClaim**:  c7026f88-4299-4cdb-965d-3f166464b8a9</span><span class="sxs-lookup"><span data-stu-id="8473d-434">**outputClaim**:  c7026f88-4299-4cdb-965d-3f166464b8a9</span></span>

## <a name="nullclaim"></a><span data-ttu-id="8473d-435">NullClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-435">NullClaim</span></span>

<span data-ttu-id="8473d-436">Clean the value of a given claim.</span><span class="sxs-lookup"><span data-stu-id="8473d-436">Clean the value of a given claim.</span></span>

| <span data-ttu-id="8473d-437">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-437">Item</span></span> | <span data-ttu-id="8473d-438">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-438">TransformationClaimType</span></span> | <span data-ttu-id="8473d-439">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-439">Data Type</span></span> | <span data-ttu-id="8473d-440">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-440">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-441">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-441">OutputClaim</span></span> | <span data-ttu-id="8473d-442">claim_to_null</span><span class="sxs-lookup"><span data-stu-id="8473d-442">claim_to_null</span></span> | <span data-ttu-id="8473d-443">string</span><span class="sxs-lookup"><span data-stu-id="8473d-443">string</span></span> | <span data-ttu-id="8473d-444">The claim its value to be NULL.</span><span class="sxs-lookup"><span data-stu-id="8473d-444">The claim its value to be NULL.</span></span> |

<span data-ttu-id="8473d-445">Use this claim transformation to remove unnecessary data from the claims property bag.</span><span class="sxs-lookup"><span data-stu-id="8473d-445">Use this claim transformation to remove unnecessary data from the claims property bag.</span></span> <span data-ttu-id="8473d-446">So, the session cookie will be smaller.</span><span class="sxs-lookup"><span data-stu-id="8473d-446">So, the session cookie will be smaller.</span></span> <span data-ttu-id="8473d-447">The following example removes the value of the `TermsOfService` claim type.</span><span class="sxs-lookup"><span data-stu-id="8473d-447">The following example removes the value of the `TermsOfService` claim type.</span></span>

```XML
<ClaimsTransformation Id="SetTOSToNull" TransformationMethod="NullClaim">
  <OutputClaims>
  <OutputClaim ClaimTypeReferenceId="TermsOfService" TransformationClaimType="claim_to_null" />
  </OutputClaims>
</ClaimsTransformation>
```

- <span data-ttu-id="8473d-448">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-448">Input claims:</span></span>
    - <span data-ttu-id="8473d-449">**outputClaim**: Welcome to Contoso App.</span><span class="sxs-lookup"><span data-stu-id="8473d-449">**outputClaim**: Welcome to Contoso App.</span></span> <span data-ttu-id="8473d-450">If you continue to browse and use this website, you are agreeing to comply with and be bound by the following terms and conditions...</span><span class="sxs-lookup"><span data-stu-id="8473d-450">If you continue to browse and use this website, you are agreeing to comply with and be bound by the following terms and conditions...</span></span>
- <span data-ttu-id="8473d-451">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-451">Output claims:</span></span>
    - <span data-ttu-id="8473d-452">**outputClaim**: NULL</span><span class="sxs-lookup"><span data-stu-id="8473d-452">**outputClaim**: NULL</span></span>

## <a name="parsedomain"></a><span data-ttu-id="8473d-453">ParseDomain</span><span class="sxs-lookup"><span data-stu-id="8473d-453">ParseDomain</span></span>

<span data-ttu-id="8473d-454">Gets the domain portion of an email address.</span><span class="sxs-lookup"><span data-stu-id="8473d-454">Gets the domain portion of an email address.</span></span>

| <span data-ttu-id="8473d-455">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-455">Item</span></span> | <span data-ttu-id="8473d-456">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-456">TransformationClaimType</span></span> | <span data-ttu-id="8473d-457">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-457">Data Type</span></span> | <span data-ttu-id="8473d-458">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-458">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-459">InputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-459">InputClaim</span></span> | <span data-ttu-id="8473d-460">emailAddress</span><span class="sxs-lookup"><span data-stu-id="8473d-460">emailAddress</span></span> | <span data-ttu-id="8473d-461">string</span><span class="sxs-lookup"><span data-stu-id="8473d-461">string</span></span> | <span data-ttu-id="8473d-462">The ClaimType that contains the email address.</span><span class="sxs-lookup"><span data-stu-id="8473d-462">The ClaimType that contains the email address.</span></span> |
| <span data-ttu-id="8473d-463">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-463">OutputClaim</span></span> | <span data-ttu-id="8473d-464">domain</span><span class="sxs-lookup"><span data-stu-id="8473d-464">domain</span></span> | <span data-ttu-id="8473d-465">string</span><span class="sxs-lookup"><span data-stu-id="8473d-465">string</span></span> | <span data-ttu-id="8473d-466">The ClaimType that is produced after this claims transformation has been invoked - the domain.</span><span class="sxs-lookup"><span data-stu-id="8473d-466">The ClaimType that is produced after this claims transformation has been invoked - the domain.</span></span> |

<span data-ttu-id="8473d-467">Use this claims transformation to parse the domain name after the @ symbol of the user.</span><span class="sxs-lookup"><span data-stu-id="8473d-467">Use this claims transformation to parse the domain name after the @ symbol of the user.</span></span> <span data-ttu-id="8473d-468">This can be helpful in removing Personally identifiable information (PII) from audit data.</span><span class="sxs-lookup"><span data-stu-id="8473d-468">This can be helpful in removing Personally identifiable information (PII) from audit data.</span></span> <span data-ttu-id="8473d-469">The following claims transformation demonstrates how to parse the domain name from an **email** claim.</span><span class="sxs-lookup"><span data-stu-id="8473d-469">The following claims transformation demonstrates how to parse the domain name from an **email** claim.</span></span>

```XML
<ClaimsTransformation Id="SetDomainName" TransformationMethod="ParseDomain">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="email" TransformationClaimType="emailAddress" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="domainName" TransformationClaimType="domain" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-470">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-470">Example</span></span>

- <span data-ttu-id="8473d-471">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-471">Input claims:</span></span>
    - <span data-ttu-id="8473d-472">**emailAddress**: joe@outlook.com</span><span class="sxs-lookup"><span data-stu-id="8473d-472">**emailAddress**: joe@outlook.com</span></span>
- <span data-ttu-id="8473d-473">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-473">Output claims:</span></span>
    - <span data-ttu-id="8473d-474">**domain**: outlook.com</span><span class="sxs-lookup"><span data-stu-id="8473d-474">**domain**: outlook.com</span></span>

## <a name="setclaimsifstringsareequal"></a><span data-ttu-id="8473d-475">SetClaimsIfStringsAreEqual</span><span class="sxs-lookup"><span data-stu-id="8473d-475">SetClaimsIfStringsAreEqual</span></span>

<span data-ttu-id="8473d-476">Checks that a string claim and `matchTo` input parameter are equal, and sets the output claims with the value present in `stringMatchMsg` and `stringMatchMsgCode` input parameters, along with  compare result output claim, which is to be set as `true` or `false` based on the result of comparison.</span><span class="sxs-lookup"><span data-stu-id="8473d-476">Checks that a string claim and `matchTo` input parameter are equal, and sets the output claims with the value present in `stringMatchMsg` and `stringMatchMsgCode` input parameters, along with  compare result output claim, which is to be set as `true` or `false` based on the result of comparison.</span></span>

| <span data-ttu-id="8473d-477">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-477">Item</span></span> | <span data-ttu-id="8473d-478">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-478">TransformationClaimType</span></span> | <span data-ttu-id="8473d-479">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-479">Data Type</span></span> | <span data-ttu-id="8473d-480">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-480">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-481">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-481">inputClaim</span></span> | <span data-ttu-id="8473d-482">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-482">inputClaim</span></span> | <span data-ttu-id="8473d-483">string</span><span class="sxs-lookup"><span data-stu-id="8473d-483">string</span></span> | <span data-ttu-id="8473d-484">The claim type, which is to be compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-484">The claim type, which is to be compared.</span></span> |
| <span data-ttu-id="8473d-485">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-485">InputParameter</span></span> | <span data-ttu-id="8473d-486">matchTo</span><span class="sxs-lookup"><span data-stu-id="8473d-486">matchTo</span></span> | <span data-ttu-id="8473d-487">string</span><span class="sxs-lookup"><span data-stu-id="8473d-487">string</span></span> | <span data-ttu-id="8473d-488">The string to be compared with `inputClaim`.</span><span class="sxs-lookup"><span data-stu-id="8473d-488">The string to be compared with `inputClaim`.</span></span> |
| <span data-ttu-id="8473d-489">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-489">InputParameter</span></span> | <span data-ttu-id="8473d-490">stringComparison</span><span class="sxs-lookup"><span data-stu-id="8473d-490">stringComparison</span></span> | <span data-ttu-id="8473d-491">string</span><span class="sxs-lookup"><span data-stu-id="8473d-491">string</span></span> | <span data-ttu-id="8473d-492">Possible values: `Ordinal` or `OrdinalIgnoreCase`.</span><span class="sxs-lookup"><span data-stu-id="8473d-492">Possible values: `Ordinal` or `OrdinalIgnoreCase`.</span></span> |
| <span data-ttu-id="8473d-493">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-493">InputParameter</span></span> | <span data-ttu-id="8473d-494">stringMatchMsg</span><span class="sxs-lookup"><span data-stu-id="8473d-494">stringMatchMsg</span></span> | <span data-ttu-id="8473d-495">string</span><span class="sxs-lookup"><span data-stu-id="8473d-495">string</span></span> | <span data-ttu-id="8473d-496">First value to be set if strings are equal.</span><span class="sxs-lookup"><span data-stu-id="8473d-496">First value to be set if strings are equal.</span></span> |
| <span data-ttu-id="8473d-497">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-497">InputParameter</span></span> | <span data-ttu-id="8473d-498">stringMatchMsgCode</span><span class="sxs-lookup"><span data-stu-id="8473d-498">stringMatchMsgCode</span></span> | <span data-ttu-id="8473d-499">string</span><span class="sxs-lookup"><span data-stu-id="8473d-499">string</span></span> | <span data-ttu-id="8473d-500">Second value to be set if strings are equal.</span><span class="sxs-lookup"><span data-stu-id="8473d-500">Second value to be set if strings are equal.</span></span> |
| <span data-ttu-id="8473d-501">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-501">OutputClaim</span></span> | <span data-ttu-id="8473d-502">outputClaim1</span><span class="sxs-lookup"><span data-stu-id="8473d-502">outputClaim1</span></span> | <span data-ttu-id="8473d-503">string</span><span class="sxs-lookup"><span data-stu-id="8473d-503">string</span></span> | <span data-ttu-id="8473d-504">If strings are equals, this output claim contains the value of `stringMatchMsg` input parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-504">If strings are equals, this output claim contains the value of `stringMatchMsg` input parameter.</span></span> |
| <span data-ttu-id="8473d-505">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-505">OutputClaim</span></span> | <span data-ttu-id="8473d-506">outputClaim2</span><span class="sxs-lookup"><span data-stu-id="8473d-506">outputClaim2</span></span> | <span data-ttu-id="8473d-507">string</span><span class="sxs-lookup"><span data-stu-id="8473d-507">string</span></span> | <span data-ttu-id="8473d-508">If strings are equals, this output claim contains the value of `stringMatchMsgCode` input parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-508">If strings are equals, this output claim contains the value of `stringMatchMsgCode` input parameter.</span></span> |
| <span data-ttu-id="8473d-509">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-509">OutputClaim</span></span> | <span data-ttu-id="8473d-510">stringCompareResultClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-510">stringCompareResultClaim</span></span> | <span data-ttu-id="8473d-511">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-511">boolean</span></span> | <span data-ttu-id="8473d-512">The compare result output claim type, which is to be set as `true` or `false` based on the result of comparison.</span><span class="sxs-lookup"><span data-stu-id="8473d-512">The compare result output claim type, which is to be set as `true` or `false` based on the result of comparison.</span></span> |

<span data-ttu-id="8473d-513">You can use this claims transformation to check if a claim is equal to value you specified.</span><span class="sxs-lookup"><span data-stu-id="8473d-513">You can use this claims transformation to check if a claim is equal to value you specified.</span></span> <span data-ttu-id="8473d-514">For example, the following claims transformation checks if the value of the **termsOfUseConsentVersion** claim is equal to `v1`.</span><span class="sxs-lookup"><span data-stu-id="8473d-514">For example, the following claims transformation checks if the value of the **termsOfUseConsentVersion** claim is equal to `v1`.</span></span> <span data-ttu-id="8473d-515">If yes, change the value to `v2`.</span><span class="sxs-lookup"><span data-stu-id="8473d-515">If yes, change the value to `v2`.</span></span> 

```XML
<ClaimsTransformation Id="CheckTheTOS" TransformationMethod="SetClaimsIfStringsAreEqual">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="termsOfUseConsentVersion" TransformationClaimType="inputClaim" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="matchTo" DataType="string" Value="v1" />
    <InputParameter Id="stringComparison" DataType="string" Value="ordinalIgnoreCase" />
    <InputParameter Id="stringMatchMsg" DataType="string" Value="B2C_V1_90005" />
    <InputParameter Id="stringMatchMsgCode" DataType="string" Value="The TOS is upgraded to v2" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="termsOfUseConsentVersion" TransformationClaimType="outputClaim1" />
    <OutputClaim ClaimTypeReferenceId="termsOfUseConsentVersionUpgradeCode" TransformationClaimType="outputClaim2" />
    <OutputClaim ClaimTypeReferenceId="termsOfUseConsentVersionUpgradeResult" TransformationClaimType="stringCompareResultClaim" />
  </OutputClaims>
</ClaimsTransformation>
```
### <a name="example"></a><span data-ttu-id="8473d-516">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-516">Example</span></span>

- <span data-ttu-id="8473d-517">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-517">Input claims:</span></span>
    - <span data-ttu-id="8473d-518">**inputClaim**: v1</span><span class="sxs-lookup"><span data-stu-id="8473d-518">**inputClaim**: v1</span></span>
- <span data-ttu-id="8473d-519">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-519">Input parameters:</span></span>
    - <span data-ttu-id="8473d-520">**matchTo**: V1</span><span class="sxs-lookup"><span data-stu-id="8473d-520">**matchTo**: V1</span></span>
    - <span data-ttu-id="8473d-521">**stringComparison**: ordinalIgnoreCase</span><span class="sxs-lookup"><span data-stu-id="8473d-521">**stringComparison**: ordinalIgnoreCase</span></span> 
    - <span data-ttu-id="8473d-522">**stringMatchMsg**:  B2C_V1_90005</span><span class="sxs-lookup"><span data-stu-id="8473d-522">**stringMatchMsg**:  B2C_V1_90005</span></span>
    - <span data-ttu-id="8473d-523">**stringMatchMsgCode**:  The TOS is upgraded to v2</span><span class="sxs-lookup"><span data-stu-id="8473d-523">**stringMatchMsgCode**:  The TOS is upgraded to v2</span></span>
- <span data-ttu-id="8473d-524">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-524">Output claims:</span></span>
    - <span data-ttu-id="8473d-525">**outputClaim1**: B2C_V1_90005</span><span class="sxs-lookup"><span data-stu-id="8473d-525">**outputClaim1**: B2C_V1_90005</span></span>
    - <span data-ttu-id="8473d-526">**outputClaim2**: The TOS is upgraded to v2</span><span class="sxs-lookup"><span data-stu-id="8473d-526">**outputClaim2**: The TOS is upgraded to v2</span></span>
    - <span data-ttu-id="8473d-527">**stringCompareResultClaim**: true</span><span class="sxs-lookup"><span data-stu-id="8473d-527">**stringCompareResultClaim**: true</span></span>

## <a name="setclaimsifstringsmatch"></a><span data-ttu-id="8473d-528">SetClaimsIfStringsMatch</span><span class="sxs-lookup"><span data-stu-id="8473d-528">SetClaimsIfStringsMatch</span></span>

<span data-ttu-id="8473d-529">Checks that a string claim and `matchTo` input parameter are equal, and sets the output claims with the value present in `outputClaimIfMatched` input parameter, along with  compare result output claim, which is to be set as `true` or `false` based on the result of comparison.</span><span class="sxs-lookup"><span data-stu-id="8473d-529">Checks that a string claim and `matchTo` input parameter are equal, and sets the output claims with the value present in `outputClaimIfMatched` input parameter, along with  compare result output claim, which is to be set as `true` or `false` based on the result of comparison.</span></span>

| <span data-ttu-id="8473d-530">Item</span><span class="sxs-lookup"><span data-stu-id="8473d-530">Item</span></span> | <span data-ttu-id="8473d-531">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="8473d-531">TransformationClaimType</span></span> | <span data-ttu-id="8473d-532">Data Type</span><span class="sxs-lookup"><span data-stu-id="8473d-532">Data Type</span></span> | <span data-ttu-id="8473d-533">Notes</span><span class="sxs-lookup"><span data-stu-id="8473d-533">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="8473d-534">inputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-534">inputClaim</span></span> | <span data-ttu-id="8473d-535">claimToMatch</span><span class="sxs-lookup"><span data-stu-id="8473d-535">claimToMatch</span></span> | <span data-ttu-id="8473d-536">string</span><span class="sxs-lookup"><span data-stu-id="8473d-536">string</span></span> | <span data-ttu-id="8473d-537">The claim type, which is to be compared.</span><span class="sxs-lookup"><span data-stu-id="8473d-537">The claim type, which is to be compared.</span></span> |
| <span data-ttu-id="8473d-538">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-538">InputParameter</span></span> | <span data-ttu-id="8473d-539">matchTo</span><span class="sxs-lookup"><span data-stu-id="8473d-539">matchTo</span></span> | <span data-ttu-id="8473d-540">string</span><span class="sxs-lookup"><span data-stu-id="8473d-540">string</span></span> | <span data-ttu-id="8473d-541">The string to be compared with inputClaim.</span><span class="sxs-lookup"><span data-stu-id="8473d-541">The string to be compared with inputClaim.</span></span> |
| <span data-ttu-id="8473d-542">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-542">InputParameter</span></span> | <span data-ttu-id="8473d-543">stringComparison</span><span class="sxs-lookup"><span data-stu-id="8473d-543">stringComparison</span></span> | <span data-ttu-id="8473d-544">string</span><span class="sxs-lookup"><span data-stu-id="8473d-544">string</span></span> | <span data-ttu-id="8473d-545">Possible values: `Ordinal` or `OrdinalIgnoreCase`.</span><span class="sxs-lookup"><span data-stu-id="8473d-545">Possible values: `Ordinal` or `OrdinalIgnoreCase`.</span></span> |
| <span data-ttu-id="8473d-546">InputParameter</span><span class="sxs-lookup"><span data-stu-id="8473d-546">InputParameter</span></span> | <span data-ttu-id="8473d-547">outputClaimIfMatched</span><span class="sxs-lookup"><span data-stu-id="8473d-547">outputClaimIfMatched</span></span> | <span data-ttu-id="8473d-548">string</span><span class="sxs-lookup"><span data-stu-id="8473d-548">string</span></span> | <span data-ttu-id="8473d-549">The value to be set if strings are equal.</span><span class="sxs-lookup"><span data-stu-id="8473d-549">The value to be set if strings are equal.</span></span> |
| <span data-ttu-id="8473d-550">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-550">OutputClaim</span></span> | <span data-ttu-id="8473d-551">outputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-551">outputClaim</span></span> | <span data-ttu-id="8473d-552">string</span><span class="sxs-lookup"><span data-stu-id="8473d-552">string</span></span> | <span data-ttu-id="8473d-553">If strings are equals, this output claim contains the value of `outputClaimIfMatched` input parameter.</span><span class="sxs-lookup"><span data-stu-id="8473d-553">If strings are equals, this output claim contains the value of `outputClaimIfMatched` input parameter.</span></span> <span data-ttu-id="8473d-554">Or null, if the strings aren't match.</span><span class="sxs-lookup"><span data-stu-id="8473d-554">Or null, if the strings aren't match.</span></span> |
| <span data-ttu-id="8473d-555">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-555">OutputClaim</span></span> | <span data-ttu-id="8473d-556">stringCompareResultClaim</span><span class="sxs-lookup"><span data-stu-id="8473d-556">stringCompareResultClaim</span></span> | <span data-ttu-id="8473d-557">boolean</span><span class="sxs-lookup"><span data-stu-id="8473d-557">boolean</span></span> | <span data-ttu-id="8473d-558">The compare result output claim type, which is to be set as `true` or `false` based on the result of comparison.</span><span class="sxs-lookup"><span data-stu-id="8473d-558">The compare result output claim type, which is to be set as `true` or `false` based on the result of comparison.</span></span> |

<span data-ttu-id="8473d-559">For example, the following claims transformation checks if the value of **ageGroup** claim is equal to `Minor`.</span><span class="sxs-lookup"><span data-stu-id="8473d-559">For example, the following claims transformation checks if the value of **ageGroup** claim is equal to `Minor`.</span></span> <span data-ttu-id="8473d-560">If yes, return the value to `B2C_V1_90001`.</span><span class="sxs-lookup"><span data-stu-id="8473d-560">If yes, return the value to `B2C_V1_90001`.</span></span> 

```XML
<ClaimsTransformation Id="SetIsMinor" TransformationMethod="SetClaimsIfStringsMatch">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="ageGroup" TransformationClaimType="claimToMatch" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="matchTo" DataType="string" Value="Minor" />
    <InputParameter Id="stringComparison" DataType="string" Value="ordinalIgnoreCase" />
    <InputParameter Id="outputClaimIfMatched" DataType="string" Value="B2C_V1_90001" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="isMinor" TransformationClaimType="outputClaim" />
    <OutputClaim ClaimTypeReferenceId="isMinorResponseCode" TransformationClaimType="stringCompareResultClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="8473d-561">Example</span><span class="sxs-lookup"><span data-stu-id="8473d-561">Example</span></span>

- <span data-ttu-id="8473d-562">Input claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-562">Input claims:</span></span>
    - <span data-ttu-id="8473d-563">**claimToMatch**: Minor</span><span class="sxs-lookup"><span data-stu-id="8473d-563">**claimToMatch**: Minor</span></span>
- <span data-ttu-id="8473d-564">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="8473d-564">Input parameters:</span></span>
    - <span data-ttu-id="8473d-565">**matchTo**: Minor</span><span class="sxs-lookup"><span data-stu-id="8473d-565">**matchTo**: Minor</span></span>
    - <span data-ttu-id="8473d-566">**stringComparison**: ordinalIgnoreCase</span><span class="sxs-lookup"><span data-stu-id="8473d-566">**stringComparison**: ordinalIgnoreCase</span></span> 
    - <span data-ttu-id="8473d-567">**outputClaimIfMatched**:  B2C_V1_90001</span><span class="sxs-lookup"><span data-stu-id="8473d-567">**outputClaimIfMatched**:  B2C_V1_90001</span></span>
- <span data-ttu-id="8473d-568">Output claims:</span><span class="sxs-lookup"><span data-stu-id="8473d-568">Output claims:</span></span>
    - <span data-ttu-id="8473d-569">**isMinorResponseCode**: B2C_V1_90001</span><span class="sxs-lookup"><span data-stu-id="8473d-569">**isMinorResponseCode**: B2C_V1_90001</span></span>
    - <span data-ttu-id="8473d-570">**isMinor**: true</span><span class="sxs-lookup"><span data-stu-id="8473d-570">**isMinor**: true</span></span>

