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
# <a name="boolean-claims-transformations"></a><span data-ttu-id="ba076-103">Boolean claims transformations</span><span class="sxs-lookup"><span data-stu-id="ba076-103">Boolean claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ba076-104">This article provides examples for using the boolean claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="ba076-104">This article provides examples for using the boolean claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="ba076-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="ba076-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="andclaims"></a><span data-ttu-id="ba076-106">AndClaims</span><span class="sxs-lookup"><span data-stu-id="ba076-106">AndClaims</span></span>

<span data-ttu-id="ba076-107">Performs an And operation of two boolean inputClaims and sets the outputClaim with result of the operation.</span><span class="sxs-lookup"><span data-stu-id="ba076-107">Performs an And operation of two boolean inputClaims and sets the outputClaim with result of the operation.</span></span>

| <span data-ttu-id="ba076-108">Item</span><span class="sxs-lookup"><span data-stu-id="ba076-108">Item</span></span>  | <span data-ttu-id="ba076-109">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="ba076-109">TransformationClaimType</span></span>  | <span data-ttu-id="ba076-110">Data Type</span><span class="sxs-lookup"><span data-stu-id="ba076-110">Data Type</span></span>  | <span data-ttu-id="ba076-111">Notes</span><span class="sxs-lookup"><span data-stu-id="ba076-111">Notes</span></span> |
|-------| ------------------------ | ---------- | ----- |
| <span data-ttu-id="ba076-112">InputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-112">InputClaim</span></span> | <span data-ttu-id="ba076-113">inputClaim1</span><span class="sxs-lookup"><span data-stu-id="ba076-113">inputClaim1</span></span> | <span data-ttu-id="ba076-114">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-114">boolean</span></span> | <span data-ttu-id="ba076-115">The first ClaimType to evaluate.</span><span class="sxs-lookup"><span data-stu-id="ba076-115">The first ClaimType to evaluate.</span></span> |
| <span data-ttu-id="ba076-116">InputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-116">InputClaim</span></span> | <span data-ttu-id="ba076-117">inputClaim2</span><span class="sxs-lookup"><span data-stu-id="ba076-117">inputClaim2</span></span>  | <span data-ttu-id="ba076-118">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-118">boolean</span></span> | <span data-ttu-id="ba076-119">The second ClaimType to evaluate.</span><span class="sxs-lookup"><span data-stu-id="ba076-119">The second ClaimType to evaluate.</span></span> |
|<span data-ttu-id="ba076-120">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-120">OutputClaim</span></span> | <span data-ttu-id="ba076-121">outputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-121">outputClaim</span></span> | <span data-ttu-id="ba076-122">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-122">boolean</span></span> | <span data-ttu-id="ba076-123">The ClaimTypes that will be produced after this claims transformation has been invoked (true or false).</span><span class="sxs-lookup"><span data-stu-id="ba076-123">The ClaimTypes that will be produced after this claims transformation has been invoked (true or false).</span></span> |

<span data-ttu-id="ba076-124">The following claims transformation demonstrates how to And two boolean ClaimTypes: `isEmailNotExist`, and `isSocialAccount`.</span><span class="sxs-lookup"><span data-stu-id="ba076-124">The following claims transformation demonstrates how to And two boolean ClaimTypes: `isEmailNotExist`, and `isSocialAccount`.</span></span> <span data-ttu-id="ba076-125">The output claim `presentEmailSelfAsserted` is set to `true` if the value of both input claims are `true`.</span><span class="sxs-lookup"><span data-stu-id="ba076-125">The output claim `presentEmailSelfAsserted` is set to `true` if the value of both input claims are `true`.</span></span> <span data-ttu-id="ba076-126">In an orchestration step, you can use a precondition to preset a self-asserted page, only if a social account email is empty.</span><span class="sxs-lookup"><span data-stu-id="ba076-126">In an orchestration step, you can use a precondition to preset a self-asserted page, only if a social account email is empty.</span></span>

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

### <a name="example"></a><span data-ttu-id="ba076-127">Example</span><span class="sxs-lookup"><span data-stu-id="ba076-127">Example</span></span>

- <span data-ttu-id="ba076-128">Input claims:</span><span class="sxs-lookup"><span data-stu-id="ba076-128">Input claims:</span></span>
    - <span data-ttu-id="ba076-129">**inputClaim1**: true</span><span class="sxs-lookup"><span data-stu-id="ba076-129">**inputClaim1**: true</span></span>
    - <span data-ttu-id="ba076-130">**inputClaim2**: false</span><span class="sxs-lookup"><span data-stu-id="ba076-130">**inputClaim2**: false</span></span>
- <span data-ttu-id="ba076-131">Output claims:</span><span class="sxs-lookup"><span data-stu-id="ba076-131">Output claims:</span></span>
    - <span data-ttu-id="ba076-132">**outputClaim**: false</span><span class="sxs-lookup"><span data-stu-id="ba076-132">**outputClaim**: false</span></span>


## <a name="assertbooleanclaimisequaltovalue"></a><span data-ttu-id="ba076-133">AssertBooleanClaimIsEqualToValue</span><span class="sxs-lookup"><span data-stu-id="ba076-133">AssertBooleanClaimIsEqualToValue</span></span>

<span data-ttu-id="ba076-134">Checks that boolean values of two claims are equal, and throws an exception if they are not.</span><span class="sxs-lookup"><span data-stu-id="ba076-134">Checks that boolean values of two claims are equal, and throws an exception if they are not.</span></span>

| <span data-ttu-id="ba076-135">Item</span><span class="sxs-lookup"><span data-stu-id="ba076-135">Item</span></span> | <span data-ttu-id="ba076-136">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="ba076-136">TransformationClaimType</span></span>  | <span data-ttu-id="ba076-137">Data Type</span><span class="sxs-lookup"><span data-stu-id="ba076-137">Data Type</span></span>  | <span data-ttu-id="ba076-138">Notes</span><span class="sxs-lookup"><span data-stu-id="ba076-138">Notes</span></span> |
| ---- | ------------------------ | ---------- | ----- |
| <span data-ttu-id="ba076-139">inputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-139">inputClaim</span></span> | <span data-ttu-id="ba076-140">inputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-140">inputClaim</span></span> | <span data-ttu-id="ba076-141">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-141">boolean</span></span> | <span data-ttu-id="ba076-142">The ClaimType to be asserted.</span><span class="sxs-lookup"><span data-stu-id="ba076-142">The ClaimType to be asserted.</span></span> |
| <span data-ttu-id="ba076-143">InputParameter</span><span class="sxs-lookup"><span data-stu-id="ba076-143">InputParameter</span></span> |<span data-ttu-id="ba076-144">valueToCompareTo</span><span class="sxs-lookup"><span data-stu-id="ba076-144">valueToCompareTo</span></span> | <span data-ttu-id="ba076-145">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-145">boolean</span></span> | <span data-ttu-id="ba076-146">The value to compare (true or false).</span><span class="sxs-lookup"><span data-stu-id="ba076-146">The value to compare (true or false).</span></span> |

<span data-ttu-id="ba076-147">The **AssertBooleanClaimIsEqualToValue** claims transformation is always executed from a [validation technical profile](validation-technical-profile.md) that is called by a [self-asserted technical profile](self-asserted-technical-profile.md).</span><span class="sxs-lookup"><span data-stu-id="ba076-147">The **AssertBooleanClaimIsEqualToValue** claims transformation is always executed from a [validation technical profile](validation-technical-profile.md) that is called by a [self-asserted technical profile](self-asserted-technical-profile.md).</span></span> <span data-ttu-id="ba076-148">The **UserMessageIfClaimsTransformationBooleanValueIsNotEqual** self-asserted technical profile metadata controls the error message that the technical profile presents to the user.</span><span class="sxs-lookup"><span data-stu-id="ba076-148">The **UserMessageIfClaimsTransformationBooleanValueIsNotEqual** self-asserted technical profile metadata controls the error message that the technical profile presents to the user.</span></span>

![AssertStringClaimsAreEqual execution](./media/boolean-transformations/assert-execution.png)

<span data-ttu-id="ba076-150">The following claims transformation demonstrates how to check the value of a boolean ClaimType with a `true` value.</span><span class="sxs-lookup"><span data-stu-id="ba076-150">The following claims transformation demonstrates how to check the value of a boolean ClaimType with a `true` value.</span></span> <span data-ttu-id="ba076-151">If the value of the `accountEnabled` ClaimType is false, an error message is thrown.</span><span class="sxs-lookup"><span data-stu-id="ba076-151">If the value of the `accountEnabled` ClaimType is false, an error message is thrown.</span></span>

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


<span data-ttu-id="ba076-152">The `login-NonInteractive` validation technical profile calls the `AssertAccountEnabledIsTrue` claims transformation.</span><span class="sxs-lookup"><span data-stu-id="ba076-152">The `login-NonInteractive` validation technical profile calls the `AssertAccountEnabledIsTrue` claims transformation.</span></span>
```XML
<TechnicalProfile Id="login-NonInteractive">
  ...
  <OutputClaimsTransformations>
    <OutputClaimsTransformation ReferenceId="AssertAccountEnabledIsTrue" />
  </OutputClaimsTransformations>
</TechnicalProfile>
```

<span data-ttu-id="ba076-153">The self-asserted technical profile calls the validation **login-NonInteractive** technical profile.</span><span class="sxs-lookup"><span data-stu-id="ba076-153">The self-asserted technical profile calls the validation **login-NonInteractive** technical profile.</span></span>

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

### <a name="example"></a><span data-ttu-id="ba076-154">Example</span><span class="sxs-lookup"><span data-stu-id="ba076-154">Example</span></span>

- <span data-ttu-id="ba076-155">Input claims:</span><span class="sxs-lookup"><span data-stu-id="ba076-155">Input claims:</span></span>
    - <span data-ttu-id="ba076-156">**inputClaim**: false</span><span class="sxs-lookup"><span data-stu-id="ba076-156">**inputClaim**: false</span></span>
    - <span data-ttu-id="ba076-157">**valueToCompareTo**: true</span><span class="sxs-lookup"><span data-stu-id="ba076-157">**valueToCompareTo**: true</span></span>
- <span data-ttu-id="ba076-158">Result: Error thrown</span><span class="sxs-lookup"><span data-stu-id="ba076-158">Result: Error thrown</span></span>

## <a name="notclaims"></a><span data-ttu-id="ba076-159">NotClaims</span><span class="sxs-lookup"><span data-stu-id="ba076-159">NotClaims</span></span>

<span data-ttu-id="ba076-160">Performs a Not operation of the boolean inputClaim and sets the outputClaim with result of the operation.</span><span class="sxs-lookup"><span data-stu-id="ba076-160">Performs a Not operation of the boolean inputClaim and sets the outputClaim with result of the operation.</span></span>

| <span data-ttu-id="ba076-161">Item</span><span class="sxs-lookup"><span data-stu-id="ba076-161">Item</span></span> | <span data-ttu-id="ba076-162">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="ba076-162">TransformationClaimType</span></span> | <span data-ttu-id="ba076-163">Data Type</span><span class="sxs-lookup"><span data-stu-id="ba076-163">Data Type</span></span> | <span data-ttu-id="ba076-164">Notes</span><span class="sxs-lookup"><span data-stu-id="ba076-164">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="ba076-165">InputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-165">InputClaim</span></span> | <span data-ttu-id="ba076-166">inputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-166">inputClaim</span></span> | <span data-ttu-id="ba076-167">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-167">boolean</span></span> | <span data-ttu-id="ba076-168">The claim to be operated.</span><span class="sxs-lookup"><span data-stu-id="ba076-168">The claim to be operated.</span></span> |
| <span data-ttu-id="ba076-169">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-169">OutputClaim</span></span> | <span data-ttu-id="ba076-170">outputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-170">outputClaim</span></span> | <span data-ttu-id="ba076-171">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-171">boolean</span></span> | <span data-ttu-id="ba076-172">The ClaimTypes that are produced after this ClaimsTransformation has been invoked (true or false).</span><span class="sxs-lookup"><span data-stu-id="ba076-172">The ClaimTypes that are produced after this ClaimsTransformation has been invoked (true or false).</span></span> |

<span data-ttu-id="ba076-173">Use this claim transformation to perform logical negation on a claim.</span><span class="sxs-lookup"><span data-stu-id="ba076-173">Use this claim transformation to perform logical negation on a claim.</span></span>

```XML
<ClaimsTransformation Id="CheckWhetherEmailBePresented" TransformationMethod="AndClaims">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="userExists" TransformationClaimType="inputClaim" />
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="userExists" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="ba076-174">Example</span><span class="sxs-lookup"><span data-stu-id="ba076-174">Example</span></span>

- <span data-ttu-id="ba076-175">Input claims:</span><span class="sxs-lookup"><span data-stu-id="ba076-175">Input claims:</span></span>
    - <span data-ttu-id="ba076-176">**inputClaim**: false</span><span class="sxs-lookup"><span data-stu-id="ba076-176">**inputClaim**: false</span></span>
- <span data-ttu-id="ba076-177">Output claims:</span><span class="sxs-lookup"><span data-stu-id="ba076-177">Output claims:</span></span>
    - <span data-ttu-id="ba076-178">**outputClaim**: true</span><span class="sxs-lookup"><span data-stu-id="ba076-178">**outputClaim**: true</span></span>

## <a name="orclaims"></a><span data-ttu-id="ba076-179">OrClaims</span><span class="sxs-lookup"><span data-stu-id="ba076-179">OrClaims</span></span> 

<span data-ttu-id="ba076-180">Computes an Or of two boolean inputClaims and sets the outputClaim with result of the operation.</span><span class="sxs-lookup"><span data-stu-id="ba076-180">Computes an Or of two boolean inputClaims and sets the outputClaim with result of the operation.</span></span>

| <span data-ttu-id="ba076-181">Item</span><span class="sxs-lookup"><span data-stu-id="ba076-181">Item</span></span> | <span data-ttu-id="ba076-182">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="ba076-182">TransformationClaimType</span></span> | <span data-ttu-id="ba076-183">Data Type</span><span class="sxs-lookup"><span data-stu-id="ba076-183">Data Type</span></span> | <span data-ttu-id="ba076-184">Notes</span><span class="sxs-lookup"><span data-stu-id="ba076-184">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="ba076-185">InputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-185">InputClaim</span></span> | <span data-ttu-id="ba076-186">inputClaim1</span><span class="sxs-lookup"><span data-stu-id="ba076-186">inputClaim1</span></span> | <span data-ttu-id="ba076-187">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-187">boolean</span></span> | <span data-ttu-id="ba076-188">The first ClaimType to evaluate.</span><span class="sxs-lookup"><span data-stu-id="ba076-188">The first ClaimType to evaluate.</span></span> |
| <span data-ttu-id="ba076-189">InputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-189">InputClaim</span></span> | <span data-ttu-id="ba076-190">inputClaim2</span><span class="sxs-lookup"><span data-stu-id="ba076-190">inputClaim2</span></span> | <span data-ttu-id="ba076-191">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-191">boolean</span></span> | <span data-ttu-id="ba076-192">The second ClaimType to evaluate.</span><span class="sxs-lookup"><span data-stu-id="ba076-192">The second ClaimType to evaluate.</span></span> |
| <span data-ttu-id="ba076-193">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-193">OutputClaim</span></span> | <span data-ttu-id="ba076-194">outputClaim</span><span class="sxs-lookup"><span data-stu-id="ba076-194">outputClaim</span></span> | <span data-ttu-id="ba076-195">boolean</span><span class="sxs-lookup"><span data-stu-id="ba076-195">boolean</span></span> | <span data-ttu-id="ba076-196">The ClaimTypes that will be produced after this ClaimsTransformation has been invoked (true or false).</span><span class="sxs-lookup"><span data-stu-id="ba076-196">The ClaimTypes that will be produced after this ClaimsTransformation has been invoked (true or false).</span></span> |

<span data-ttu-id="ba076-197">The following claims transformation demonstrates how to `Or` two boolean ClaimTypes.</span><span class="sxs-lookup"><span data-stu-id="ba076-197">The following claims transformation demonstrates how to `Or` two boolean ClaimTypes.</span></span> <span data-ttu-id="ba076-198">In the orchestration step, you can use a precondition to preset a self-asserted page, if the value of one of the claims is `true`.</span><span class="sxs-lookup"><span data-stu-id="ba076-198">In the orchestration step, you can use a precondition to preset a self-asserted page, if the value of one of the claims is `true`.</span></span>

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

### <a name="example"></a><span data-ttu-id="ba076-199">Example</span><span class="sxs-lookup"><span data-stu-id="ba076-199">Example</span></span>

- <span data-ttu-id="ba076-200">Input claims:</span><span class="sxs-lookup"><span data-stu-id="ba076-200">Input claims:</span></span>
    - <span data-ttu-id="ba076-201">**inputClaim1**: true</span><span class="sxs-lookup"><span data-stu-id="ba076-201">**inputClaim1**: true</span></span>
    - <span data-ttu-id="ba076-202">**inputClaim2**: false</span><span class="sxs-lookup"><span data-stu-id="ba076-202">**inputClaim2**: false</span></span>
- <span data-ttu-id="ba076-203">Output claims:</span><span class="sxs-lookup"><span data-stu-id="ba076-203">Output claims:</span></span>
    - <span data-ttu-id="ba076-204">**outputClaim**: true</span><span class="sxs-lookup"><span data-stu-id="ba076-204">**outputClaim**: true</span></span>

