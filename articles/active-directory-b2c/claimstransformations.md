---
title: ClaimsTransformations - Azure Active Directory B2C | Microsoft Docs
description: Definition of the ClaimsTransformations element in the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 7e4f3d4cd66760fd2cca799e929d2035c0ba3fd0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870377"
---
# <a name="claimstransformations"></a><span data-ttu-id="1bb1c-103">ClaimsTransformations</span><span class="sxs-lookup"><span data-stu-id="1bb1c-103">ClaimsTransformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="1bb1c-104">The **ClaimsTransformations** element contains a list of claims transformation functions that can be used in user journeys as part of a [custom policy](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="1bb1c-104">The **ClaimsTransformations** element contains a list of claims transformation functions that can be used in user journeys as part of a [custom policy](active-directory-b2c-overview-custom.md).</span></span> <span data-ttu-id="1bb1c-105">A claims transformation converts a given claim into another one.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-105">A claims transformation converts a given claim into another one.</span></span> <span data-ttu-id="1bb1c-106">In the claims transformation, you specify the transform method, for example adding an item to a string collection or changing the case of a string.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-106">In the claims transformation, you specify the transform method, for example adding an item to a string collection or changing the case of a string.</span></span>

<span data-ttu-id="1bb1c-107">To include the list of claims transformation functions that can be used in the user journeys, a ClaimsTransformations XML element must be declared under the BuildingBlocks section of the policy.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-107">To include the list of claims transformation functions that can be used in the user journeys, a ClaimsTransformations XML element must be declared under the BuildingBlocks section of the policy.</span></span>

```xml
<ClaimsTransformations Id="<identifier>" TransformationMethod="<method>">
  ...
</ClaimsTransformation>
```

<span data-ttu-id="1bb1c-108">The **ClaimsTransformations** element conatains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-108">The **ClaimsTransformations** element conatains the following attributes:</span></span>

| <span data-ttu-id="1bb1c-109">Attribute</span><span class="sxs-lookup"><span data-stu-id="1bb1c-109">Attribute</span></span> |<span data-ttu-id="1bb1c-110">Required</span><span class="sxs-lookup"><span data-stu-id="1bb1c-110">Required</span></span> | <span data-ttu-id="1bb1c-111">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-111">Description</span></span> |
| --------- |-------- | ----------- |
| <span data-ttu-id="1bb1c-112">Id</span><span class="sxs-lookup"><span data-stu-id="1bb1c-112">Id</span></span> |<span data-ttu-id="1bb1c-113">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-113">Yes</span></span> | <span data-ttu-id="1bb1c-114">An identifier that is used to uniquely identify the claim transformation.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-114">An identifier that is used to uniquely identify the claim transformation.</span></span> <span data-ttu-id="1bb1c-115">The identifier is referenced from other XML elements in the policy.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-115">The identifier is referenced from other XML elements in the policy.</span></span> |
| <span data-ttu-id="1bb1c-116">TransformationMethod</span><span class="sxs-lookup"><span data-stu-id="1bb1c-116">TransformationMethod</span></span> | <span data-ttu-id="1bb1c-117">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-117">Yes</span></span> | <span data-ttu-id="1bb1c-118">The transform method to use in the claims transformation.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-118">The transform method to use in the claims transformation.</span></span> <span data-ttu-id="1bb1c-119">Each claim transformation has its own values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-119">Each claim transformation has its own values.</span></span> <span data-ttu-id="1bb1c-120">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-120">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span></span> |

## <a name="claimstransformation"></a><span data-ttu-id="1bb1c-121">ClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="1bb1c-121">ClaimsTransformation</span></span>

<span data-ttu-id="1bb1c-122">The **ClaimsTransformation** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-122">The **ClaimsTransformation** element contains the following elements:</span></span>

```xml
<ClaimsTransformation Id="<identifier>" TransformationMethod="<method>">
  <InputClaims>
    ...
  </InputClaims>
  <InputParameters>
    ...
  </InputParameters>                
  <OutputClaims>
    ...
  </OutputClaims>
</ClaimsTransformation>
```


| <span data-ttu-id="1bb1c-123">Element</span><span class="sxs-lookup"><span data-stu-id="1bb1c-123">Element</span></span> | <span data-ttu-id="1bb1c-124">Occurrences</span><span class="sxs-lookup"><span data-stu-id="1bb1c-124">Occurrences</span></span> | <span data-ttu-id="1bb1c-125">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-125">Description</span></span> |
| ------- | -------- | ----------- |
| <span data-ttu-id="1bb1c-126">InputClaims</span><span class="sxs-lookup"><span data-stu-id="1bb1c-126">InputClaims</span></span> | <span data-ttu-id="1bb1c-127">0:1</span><span class="sxs-lookup"><span data-stu-id="1bb1c-127">0:1</span></span> | <span data-ttu-id="1bb1c-128">A list of **InputClaim** elements that specify claim types that are taken as input to the claims transformation.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-128">A list of **InputClaim** elements that specify claim types that are taken as input to the claims transformation.</span></span> <span data-ttu-id="1bb1c-129">Each of these elements contains a reference to a ClaimType already defined in the ClaimsSchema section in the policy.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-129">Each of these elements contains a reference to a ClaimType already defined in the ClaimsSchema section in the policy.</span></span> |
| <span data-ttu-id="1bb1c-130">InputParameters</span><span class="sxs-lookup"><span data-stu-id="1bb1c-130">InputParameters</span></span> | <span data-ttu-id="1bb1c-131">0:1</span><span class="sxs-lookup"><span data-stu-id="1bb1c-131">0:1</span></span> | <span data-ttu-id="1bb1c-132">A list of **InputParameter** elements that are provided as input to the claims transformation.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-132">A list of **InputParameter** elements that are provided as input to the claims transformation.</span></span>  
| <span data-ttu-id="1bb1c-133">OutputClaims</span><span class="sxs-lookup"><span data-stu-id="1bb1c-133">OutputClaims</span></span> | <span data-ttu-id="1bb1c-134">0:1</span><span class="sxs-lookup"><span data-stu-id="1bb1c-134">0:1</span></span> | <span data-ttu-id="1bb1c-135">A list of **OutputClaim** elements that specify claim types that are produced after the ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-135">A list of **OutputClaim** elements that specify claim types that are produced after the ClaimsTransformation has been invoked.</span></span> <span data-ttu-id="1bb1c-136">Each of these elements contains reference to a ClaimType already defined in the ClaimsSchema section.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-136">Each of these elements contains reference to a ClaimType already defined in the ClaimsSchema section.</span></span> |

### <a name="inputclaims"></a><span data-ttu-id="1bb1c-137">InputClaims</span><span class="sxs-lookup"><span data-stu-id="1bb1c-137">InputClaims</span></span>

<span data-ttu-id="1bb1c-138">The **InputClaims** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-138">The **InputClaims** element contains the following element:</span></span>

| <span data-ttu-id="1bb1c-139">Element</span><span class="sxs-lookup"><span data-stu-id="1bb1c-139">Element</span></span> | <span data-ttu-id="1bb1c-140">Occurrences</span><span class="sxs-lookup"><span data-stu-id="1bb1c-140">Occurrences</span></span> | <span data-ttu-id="1bb1c-141">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-141">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="1bb1c-142">InputClaim</span><span class="sxs-lookup"><span data-stu-id="1bb1c-142">InputClaim</span></span> | <span data-ttu-id="1bb1c-143">1:n</span><span class="sxs-lookup"><span data-stu-id="1bb1c-143">1:n</span></span> | <span data-ttu-id="1bb1c-144">An expected input claim type.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-144">An expected input claim type.</span></span> |

#### <a name="inputclaim"></a><span data-ttu-id="1bb1c-145">InputClaim</span><span class="sxs-lookup"><span data-stu-id="1bb1c-145">InputClaim</span></span>

<span data-ttu-id="1bb1c-146">The **InputClaim** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-146">The **InputClaim** element contains the following attributes:</span></span>

| <span data-ttu-id="1bb1c-147">Attribute</span><span class="sxs-lookup"><span data-stu-id="1bb1c-147">Attribute</span></span> |<span data-ttu-id="1bb1c-148">Required</span><span class="sxs-lookup"><span data-stu-id="1bb1c-148">Required</span></span> | <span data-ttu-id="1bb1c-149">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-149">Description</span></span> |
| --------- | ----------- | ----------- |
| <span data-ttu-id="1bb1c-150">ClaimTypeReferenceId</span><span class="sxs-lookup"><span data-stu-id="1bb1c-150">ClaimTypeReferenceId</span></span> |<span data-ttu-id="1bb1c-151">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-151">Yes</span></span> | <span data-ttu-id="1bb1c-152">A reference to a ClaimType already defined in the ClaimsSchema section in the policy.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-152">A reference to a ClaimType already defined in the ClaimsSchema section in the policy.</span></span> |
| <span data-ttu-id="1bb1c-153">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="1bb1c-153">TransformationClaimType</span></span> |<span data-ttu-id="1bb1c-154">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-154">Yes</span></span> | <span data-ttu-id="1bb1c-155">An identifier to reference a transformation claim type.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-155">An identifier to reference a transformation claim type.</span></span> <span data-ttu-id="1bb1c-156">Each claim transformation has its own values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-156">Each claim transformation has its own values.</span></span> <span data-ttu-id="1bb1c-157">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-157">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span></span> |

### <a name="inputparameters"></a><span data-ttu-id="1bb1c-158">InputParameters</span><span class="sxs-lookup"><span data-stu-id="1bb1c-158">InputParameters</span></span>

<span data-ttu-id="1bb1c-159">The **InputParameters** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-159">The **InputParameters** element contains the following element:</span></span>

| <span data-ttu-id="1bb1c-160">Element</span><span class="sxs-lookup"><span data-stu-id="1bb1c-160">Element</span></span> | <span data-ttu-id="1bb1c-161">Occurrences</span><span class="sxs-lookup"><span data-stu-id="1bb1c-161">Occurrences</span></span> | <span data-ttu-id="1bb1c-162">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-162">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="1bb1c-163">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1bb1c-163">InputParameter</span></span> | <span data-ttu-id="1bb1c-164">1:n</span><span class="sxs-lookup"><span data-stu-id="1bb1c-164">1:n</span></span> | <span data-ttu-id="1bb1c-165">An expected input parameter.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-165">An expected input parameter.</span></span> |

#### <a name="inputparameter"></a><span data-ttu-id="1bb1c-166">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1bb1c-166">InputParameter</span></span>

| <span data-ttu-id="1bb1c-167">Attribute</span><span class="sxs-lookup"><span data-stu-id="1bb1c-167">Attribute</span></span> | <span data-ttu-id="1bb1c-168">Required</span><span class="sxs-lookup"><span data-stu-id="1bb1c-168">Required</span></span> |<span data-ttu-id="1bb1c-169">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-169">Description</span></span> |
| --------- | ----------- |----------- |
| <span data-ttu-id="1bb1c-170">Id</span><span class="sxs-lookup"><span data-stu-id="1bb1c-170">Id</span></span> | <span data-ttu-id="1bb1c-171">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-171">Yes</span></span> | <span data-ttu-id="1bb1c-172">An identifier that is a reference to a parameter of the claims transformation method.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-172">An identifier that is a reference to a parameter of the claims transformation method.</span></span> <span data-ttu-id="1bb1c-173">Each claims transformation method has its own values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-173">Each claims transformation method has its own values.</span></span> <span data-ttu-id="1bb1c-174">See the claims transformation table for a complete list of the available values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-174">See the claims transformation table for a complete list of the available values.</span></span> |
| <span data-ttu-id="1bb1c-175">DataType</span><span class="sxs-lookup"><span data-stu-id="1bb1c-175">DataType</span></span> | <span data-ttu-id="1bb1c-176">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-176">Yes</span></span> | <span data-ttu-id="1bb1c-177">The type of data of the parameter, such as String, Boolean, Int, or DateTime as per the DataType enumeration in the custom policy XML schema.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-177">The type of data of the parameter, such as String, Boolean, Int, or DateTime as per the DataType enumeration in the custom policy XML schema.</span></span> <span data-ttu-id="1bb1c-178">This type is used to perform arithmetic operations correctly.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-178">This type is used to perform arithmetic operations correctly.</span></span> <span data-ttu-id="1bb1c-179">Each claim transformation has its own values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-179">Each claim transformation has its own values.</span></span> <span data-ttu-id="1bb1c-180">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-180">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span></span> |
| <span data-ttu-id="1bb1c-181">Value</span><span class="sxs-lookup"><span data-stu-id="1bb1c-181">Value</span></span> | <span data-ttu-id="1bb1c-182">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-182">Yes</span></span> | <span data-ttu-id="1bb1c-183">A value that is passed verbatim to the transformation.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-183">A value that is passed verbatim to the transformation.</span></span> <span data-ttu-id="1bb1c-184">Some of the values are arbitrary, some of them you select from the claims transformation method.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-184">Some of the values are arbitrary, some of them you select from the claims transformation method.</span></span> |

### <a name="outputclaims"></a><span data-ttu-id="1bb1c-185">OutputClaims</span><span class="sxs-lookup"><span data-stu-id="1bb1c-185">OutputClaims</span></span>

<span data-ttu-id="1bb1c-186">The **OutputClaims** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-186">The **OutputClaims** element contains the following element:</span></span>

| <span data-ttu-id="1bb1c-187">Element</span><span class="sxs-lookup"><span data-stu-id="1bb1c-187">Element</span></span> | <span data-ttu-id="1bb1c-188">Occurrences</span><span class="sxs-lookup"><span data-stu-id="1bb1c-188">Occurrences</span></span> | <span data-ttu-id="1bb1c-189">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-189">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="1bb1c-190">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="1bb1c-190">OutputClaim</span></span> | <span data-ttu-id="1bb1c-191">0:n</span><span class="sxs-lookup"><span data-stu-id="1bb1c-191">0:n</span></span> | <span data-ttu-id="1bb1c-192">An expected output claim type.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-192">An expected output claim type.</span></span> |

#### <a name="outputclaim"></a><span data-ttu-id="1bb1c-193">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="1bb1c-193">OutputClaim</span></span> 

<span data-ttu-id="1bb1c-194">The **OutputClaim** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-194">The **OutputClaim** element contains the following attributes:</span></span>

| <span data-ttu-id="1bb1c-195">Attribute</span><span class="sxs-lookup"><span data-stu-id="1bb1c-195">Attribute</span></span> |<span data-ttu-id="1bb1c-196">Required</span><span class="sxs-lookup"><span data-stu-id="1bb1c-196">Required</span></span> | <span data-ttu-id="1bb1c-197">Description</span><span class="sxs-lookup"><span data-stu-id="1bb1c-197">Description</span></span> |
| --------- | ----------- |----------- |
| <span data-ttu-id="1bb1c-198">ClaimTypeReferenceId</span><span class="sxs-lookup"><span data-stu-id="1bb1c-198">ClaimTypeReferenceId</span></span> | <span data-ttu-id="1bb1c-199">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-199">Yes</span></span> | <span data-ttu-id="1bb1c-200">A reference to a ClaimType already defined in the ClaimsSchema section in the policy.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-200">A reference to a ClaimType already defined in the ClaimsSchema section in the policy.</span></span>
| <span data-ttu-id="1bb1c-201">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="1bb1c-201">TransformationClaimType</span></span> | <span data-ttu-id="1bb1c-202">Yes</span><span class="sxs-lookup"><span data-stu-id="1bb1c-202">Yes</span></span> | <span data-ttu-id="1bb1c-203">An identifier to reference a transformation claim type.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-203">An identifier to reference a transformation claim type.</span></span> <span data-ttu-id="1bb1c-204">Each claim transformation has its own values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-204">Each claim transformation has its own values.</span></span> <span data-ttu-id="1bb1c-205">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-205">See the [claims transformation reference](#Claims-transformations-reference) for a complete list of the available values.</span></span> |
 
<span data-ttu-id="1bb1c-206">If input claim and the output claim are the same type (string, or boolean), you can use the same input claim as the output claim.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-206">If input claim and the output claim are the same type (string, or boolean), you can use the same input claim as the output claim.</span></span> <span data-ttu-id="1bb1c-207">In this case, the claims transformation changes the input claim with the output value.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-207">In this case, the claims transformation changes the input claim with the output value.</span></span>

## <a name="example"></a><span data-ttu-id="1bb1c-208">Example</span><span class="sxs-lookup"><span data-stu-id="1bb1c-208">Example</span></span>

<span data-ttu-id="1bb1c-209">For example, you may store the last version of your terms of services that the user accepted.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-209">For example, you may store the last version of your terms of services that the user accepted.</span></span> <span data-ttu-id="1bb1c-210">When you update the terms of services, you can ask the user to accept the new version.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-210">When you update the terms of services, you can ask the user to accept the new version.</span></span> <span data-ttu-id="1bb1c-211">In the following example, the **HasTOSVersionChanged** claims transformation compares the value of the **TOSVersion** claim with the value of the **LastTOSAcceptedVersion** claim and then returns the boolean **TOSVersionChanged** claim.</span><span class="sxs-lookup"><span data-stu-id="1bb1c-211">In the following example, the **HasTOSVersionChanged** claims transformation compares the value of the **TOSVersion** claim with the value of the **LastTOSAcceptedVersion** claim and then returns the boolean **TOSVersionChanged** claim.</span></span>

```XML
<BuildingBlocks>
  <ClaimsSchema>
    <ClaimType Id="TOSVersionChanged">
      <DisplayName>Indicates if the TOS version accepted by the end user is equal to the current version</DisplayName>
      <DataType>boolean</DataType>
    </ClaimType>
    <ClaimType Id="TOSVersion">
      <DisplayName>TOS version</DisplayName>
      <DataType>string</DataType>
    </ClaimType>
    <ClaimType Id="LastTOSAcceptedVersion">
      <DisplayName>TOS version accepted by the end user</DisplayName>
      <DataType>string</DataType>
    </ClaimType>
  </ClaimsSchema>

  <ClaimsTransformations>
    <ClaimsTransformation Id="HasTOSVersionChanged" TransformationMethod="CompareClaims">
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="TOSVersion" TransformationClaimType="inputClaim1" />
        <InputClaim ClaimTypeReferenceId="LastTOSAcceptedVersion" TransformationClaimType="inputClaim2" />
      </InputClaims>
      <InputParameters>
        <InputParameter Id="operator" DataType="string" Value="NOT EQUAL" />
      </InputParameters>
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="TOSVersionChanged" TransformationClaimType="outputClaim" />
      </OutputClaims>
    </ClaimsTransformation>
  </ClaimsTransformations>
</BuildingBlocks>
```

## <a name="claims-transformations-reference"></a><span data-ttu-id="1bb1c-212">Claims transformations reference</span><span class="sxs-lookup"><span data-stu-id="1bb1c-212">Claims transformations reference</span></span>

<span data-ttu-id="1bb1c-213">For examples of claims transformations, see the following reference pages:</span><span class="sxs-lookup"><span data-stu-id="1bb1c-213">For examples of claims transformations, see the following reference pages:</span></span>

- [<span data-ttu-id="1bb1c-214">Boolean</span><span class="sxs-lookup"><span data-stu-id="1bb1c-214">Boolean</span></span>](boolean-transformations.md)
- [<span data-ttu-id="1bb1c-215">Date</span><span class="sxs-lookup"><span data-stu-id="1bb1c-215">Date</span></span>](date-transformations.md)
- [<span data-ttu-id="1bb1c-216">Integer</span><span class="sxs-lookup"><span data-stu-id="1bb1c-216">Integer</span></span>](integer-transformations.md)
- [<span data-ttu-id="1bb1c-217">JSON</span><span class="sxs-lookup"><span data-stu-id="1bb1c-217">JSON</span></span>](json-transformations.md)
- [<span data-ttu-id="1bb1c-218">General</span><span class="sxs-lookup"><span data-stu-id="1bb1c-218">General</span></span>](general-transformations.md)
- [<span data-ttu-id="1bb1c-219">Social account</span><span class="sxs-lookup"><span data-stu-id="1bb1c-219">Social account</span></span>](social-transformations.md)
- [<span data-ttu-id="1bb1c-220">String</span><span class="sxs-lookup"><span data-stu-id="1bb1c-220">String</span></span>](string-transformations.md)
- [<span data-ttu-id="1bb1c-221">StringCollection</span><span class="sxs-lookup"><span data-stu-id="1bb1c-221">StringCollection</span></span>](stringcollection-transformations.md)

