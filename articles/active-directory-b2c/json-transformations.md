---
title: JSON claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: JSON claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: b6a00719fea78d5872dc00a874951c4760d9207f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857426"
---
# <a name="json-claims-transformations"></a><span data-ttu-id="1751b-103">JSON claims transformations</span><span class="sxs-lookup"><span data-stu-id="1751b-103">JSON claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="1751b-104">This article provides examples for using the JSON claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="1751b-104">This article provides examples for using the JSON claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="1751b-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="1751b-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="getclaimfromjson"></a><span data-ttu-id="1751b-106">GetClaimFromJson</span><span class="sxs-lookup"><span data-stu-id="1751b-106">GetClaimFromJson</span></span>

<span data-ttu-id="1751b-107">Get a specified element from a JSON data.</span><span class="sxs-lookup"><span data-stu-id="1751b-107">Get a specified element from a JSON data.</span></span>

| <span data-ttu-id="1751b-108">Item</span><span class="sxs-lookup"><span data-stu-id="1751b-108">Item</span></span> | <span data-ttu-id="1751b-109">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="1751b-109">TransformationClaimType</span></span> | <span data-ttu-id="1751b-110">Data Type</span><span class="sxs-lookup"><span data-stu-id="1751b-110">Data Type</span></span> | <span data-ttu-id="1751b-111">Notes</span><span class="sxs-lookup"><span data-stu-id="1751b-111">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="1751b-112">InputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-112">InputClaim</span></span> | <span data-ttu-id="1751b-113">inputJson</span><span class="sxs-lookup"><span data-stu-id="1751b-113">inputJson</span></span> | <span data-ttu-id="1751b-114">string</span><span class="sxs-lookup"><span data-stu-id="1751b-114">string</span></span> | <span data-ttu-id="1751b-115">The ClaimTypes that are used by the claims transformation to get the item.</span><span class="sxs-lookup"><span data-stu-id="1751b-115">The ClaimTypes that are used by the claims transformation to get the item.</span></span> |
| <span data-ttu-id="1751b-116">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1751b-116">InputParameter</span></span> | <span data-ttu-id="1751b-117">claimToExtract</span><span class="sxs-lookup"><span data-stu-id="1751b-117">claimToExtract</span></span> | <span data-ttu-id="1751b-118">string</span><span class="sxs-lookup"><span data-stu-id="1751b-118">string</span></span> | <span data-ttu-id="1751b-119">the name of the JSON element to be extracted.</span><span class="sxs-lookup"><span data-stu-id="1751b-119">the name of the JSON element to be extracted.</span></span> |
| <span data-ttu-id="1751b-120">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-120">OutputClaim</span></span> | <span data-ttu-id="1751b-121">extractedClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-121">extractedClaim</span></span> | <span data-ttu-id="1751b-122">string</span><span class="sxs-lookup"><span data-stu-id="1751b-122">string</span></span> | <span data-ttu-id="1751b-123">The ClaimType that is produced after this claims transformation has been invoked, the element value specified in the _claimToExtract_ input parameter.</span><span class="sxs-lookup"><span data-stu-id="1751b-123">The ClaimType that is produced after this claims transformation has been invoked, the element value specified in the _claimToExtract_ input parameter.</span></span> |

<span data-ttu-id="1751b-124">In the following example, the claims transformation extracted the `emailAddress` element from the JSON data: `{"emailAddress": "someone@example.com", "displayName": "Someone"}`</span><span class="sxs-lookup"><span data-stu-id="1751b-124">In the following example, the claims transformation extracted the `emailAddress` element from the JSON data: `{"emailAddress": "someone@example.com", "displayName": "Someone"}`</span></span>

```XML
<ClaimsTransformation Id="GetEmailClaimFromJson" TransformationMethod="GetClaimFromJson">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="customUserData" TransformationClaimType="inputJson" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="claimToExtract" DataType="string" Value="emailAddress" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="extractedEmail" TransformationClaimType="extractedClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="1751b-125">Example</span><span class="sxs-lookup"><span data-stu-id="1751b-125">Example</span></span>

- <span data-ttu-id="1751b-126">Input claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-126">Input claims:</span></span>
    - <span data-ttu-id="1751b-127">**inputJson**: {"emailAddress": "someone@example.com", "displayName": "Someone"}</span><span class="sxs-lookup"><span data-stu-id="1751b-127">**inputJson**: {"emailAddress": "someone@example.com", "displayName": "Someone"}</span></span>
- <span data-ttu-id="1751b-128">Input parameter:</span><span class="sxs-lookup"><span data-stu-id="1751b-128">Input parameter:</span></span>
    - <span data-ttu-id="1751b-129">**claimToExtract**: emailAddress</span><span class="sxs-lookup"><span data-stu-id="1751b-129">**claimToExtract**: emailAddress</span></span>
- <span data-ttu-id="1751b-130">Output claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-130">Output claims:</span></span> 
    - <span data-ttu-id="1751b-131">**extractedClaim**: someone@example.com</span><span class="sxs-lookup"><span data-stu-id="1751b-131">**extractedClaim**: someone@example.com</span></span>


## <a name="getclaimsfromjsonarray"></a><span data-ttu-id="1751b-132">GetClaimsFromJsonArray</span><span class="sxs-lookup"><span data-stu-id="1751b-132">GetClaimsFromJsonArray</span></span>

<span data-ttu-id="1751b-133">Get a list of specified elements from Json data.</span><span class="sxs-lookup"><span data-stu-id="1751b-133">Get a list of specified elements from Json data.</span></span>

| <span data-ttu-id="1751b-134">Item</span><span class="sxs-lookup"><span data-stu-id="1751b-134">Item</span></span> | <span data-ttu-id="1751b-135">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="1751b-135">TransformationClaimType</span></span> | <span data-ttu-id="1751b-136">Data Type</span><span class="sxs-lookup"><span data-stu-id="1751b-136">Data Type</span></span> | <span data-ttu-id="1751b-137">Notes</span><span class="sxs-lookup"><span data-stu-id="1751b-137">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="1751b-138">InputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-138">InputClaim</span></span> | <span data-ttu-id="1751b-139">jsonSourceClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-139">jsonSourceClaim</span></span> | <span data-ttu-id="1751b-140">string</span><span class="sxs-lookup"><span data-stu-id="1751b-140">string</span></span> | <span data-ttu-id="1751b-141">The ClaimTypes that are used by the claims transformation to get the claims.</span><span class="sxs-lookup"><span data-stu-id="1751b-141">The ClaimTypes that are used by the claims transformation to get the claims.</span></span> |
| <span data-ttu-id="1751b-142">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1751b-142">InputParameter</span></span> | <span data-ttu-id="1751b-143">errorOnMissingClaims</span><span class="sxs-lookup"><span data-stu-id="1751b-143">errorOnMissingClaims</span></span> | <span data-ttu-id="1751b-144">boolean</span><span class="sxs-lookup"><span data-stu-id="1751b-144">boolean</span></span> | <span data-ttu-id="1751b-145">Specifies whether to throw an error if one of the claims is missing.</span><span class="sxs-lookup"><span data-stu-id="1751b-145">Specifies whether to throw an error if one of the claims is missing.</span></span> |
| <span data-ttu-id="1751b-146">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1751b-146">InputParameter</span></span> | <span data-ttu-id="1751b-147">includeEmptyClaims</span><span class="sxs-lookup"><span data-stu-id="1751b-147">includeEmptyClaims</span></span> | <span data-ttu-id="1751b-148">string</span><span class="sxs-lookup"><span data-stu-id="1751b-148">string</span></span> | <span data-ttu-id="1751b-149">Specify whether to include empty claims.</span><span class="sxs-lookup"><span data-stu-id="1751b-149">Specify whether to include empty claims.</span></span> |
| <span data-ttu-id="1751b-150">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1751b-150">InputParameter</span></span> | <span data-ttu-id="1751b-151">jsonSourceKeyName</span><span class="sxs-lookup"><span data-stu-id="1751b-151">jsonSourceKeyName</span></span> | <span data-ttu-id="1751b-152">string</span><span class="sxs-lookup"><span data-stu-id="1751b-152">string</span></span> | <span data-ttu-id="1751b-153">Element key name</span><span class="sxs-lookup"><span data-stu-id="1751b-153">Element key name</span></span> |
| <span data-ttu-id="1751b-154">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1751b-154">InputParameter</span></span> | <span data-ttu-id="1751b-155">jsonSourceValueName</span><span class="sxs-lookup"><span data-stu-id="1751b-155">jsonSourceValueName</span></span> | <span data-ttu-id="1751b-156">string</span><span class="sxs-lookup"><span data-stu-id="1751b-156">string</span></span> | <span data-ttu-id="1751b-157">Element value name</span><span class="sxs-lookup"><span data-stu-id="1751b-157">Element value name</span></span> |
| <span data-ttu-id="1751b-158">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-158">OutputClaim</span></span> | <span data-ttu-id="1751b-159">Collection</span><span class="sxs-lookup"><span data-stu-id="1751b-159">Collection</span></span> | <span data-ttu-id="1751b-160">string, int, boolean, and datetime</span><span class="sxs-lookup"><span data-stu-id="1751b-160">string, int, boolean, and datetime</span></span> |<span data-ttu-id="1751b-161">List of claims to extract.</span><span class="sxs-lookup"><span data-stu-id="1751b-161">List of claims to extract.</span></span> <span data-ttu-id="1751b-162">The name of the claim should be equal to the one specified in _jsonSourceClaim_ input claim.</span><span class="sxs-lookup"><span data-stu-id="1751b-162">The name of the claim should be equal to the one specified in _jsonSourceClaim_ input claim.</span></span> |

<span data-ttu-id="1751b-163">In the following example, the claims transformation extracts the following claims: email (string), displayName (string), membershipNum (int), active (boolean) and  birthdate (datetime) from the JSON data.</span><span class="sxs-lookup"><span data-stu-id="1751b-163">In the following example, the claims transformation extracts the following claims: email (string), displayName (string), membershipNum (int), active (boolean) and  birthdate (datetime) from the JSON data.</span></span>

```JSON
[{"key":"email","value":"someone@example.com"}, "key":"displayName","value":"Someone"}, {"key":"membershipNum","value":6353399}, {"key":"active","value":true}, {"key":"birthdate","value":"1980-09-23T00:00:00Z"}]
```

```XML
<ClaimsTransformation Id="GetClaimsFromJson" TransformationMethod="GetClaimsFromJsonArray">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="jsonSourceClaim" TransformationClaimType="jsonSource" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="errorOnMissingClaims" DataType="boolean" Value="false" />
    <InputParameter Id="includeEmptyClaims" DataType="boolean" Value="false" />
    <InputParameter Id="jsonSourceKeyName" DataType="string" Value="type" />
    <InputParameter Id="jsonSourceValueName" DataType="string" Value="value" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="email" />
    <OutputClaim ClaimTypeReferenceId="displayName" />
    <OutputClaim ClaimTypeReferenceId="membershipNum" />
    <OutputClaim ClaimTypeReferenceId="active" />
    <OutputClaim ClaimTypeReferenceId="birthdate" />
  </OutputClaims>
</ClaimsTransformation>
```    

- <span data-ttu-id="1751b-164">Input claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-164">Input claims:</span></span>
    - <span data-ttu-id="1751b-165">**jsonSourceClaim**: [{"key":"email","value":"someone@example.com"}, "key":"displayName","value":"Someone"}, {"key":"membershipNum","value":6353399}, {"key":"active","value": true}, {"key":"birthdate","value":"1980-09-23T00:00:00Z"}]</span><span class="sxs-lookup"><span data-stu-id="1751b-165">**jsonSourceClaim**: [{"key":"email","value":"someone@example.com"}, "key":"displayName","value":"Someone"}, {"key":"membershipNum","value":6353399}, {"key":"active","value": true}, {"key":"birthdate","value":"1980-09-23T00:00:00Z"}]</span></span>
- <span data-ttu-id="1751b-166">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="1751b-166">Input parameters:</span></span>
    - <span data-ttu-id="1751b-167">**errorOnMissingClaims**: false</span><span class="sxs-lookup"><span data-stu-id="1751b-167">**errorOnMissingClaims**: false</span></span>
    - <span data-ttu-id="1751b-168">**includeEmptyClaims**: false</span><span class="sxs-lookup"><span data-stu-id="1751b-168">**includeEmptyClaims**: false</span></span>
    - <span data-ttu-id="1751b-169">**jsonSourceKeyName**: key</span><span class="sxs-lookup"><span data-stu-id="1751b-169">**jsonSourceKeyName**: key</span></span>
    - <span data-ttu-id="1751b-170">**jsonSourceValueName**: value</span><span class="sxs-lookup"><span data-stu-id="1751b-170">**jsonSourceValueName**: value</span></span>
- <span data-ttu-id="1751b-171">Output claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-171">Output claims:</span></span>
    - <span data-ttu-id="1751b-172">**email**: "someone@example.com"</span><span class="sxs-lookup"><span data-stu-id="1751b-172">**email**: "someone@example.com"</span></span>
    - <span data-ttu-id="1751b-173">**displayName**: "Someone"</span><span class="sxs-lookup"><span data-stu-id="1751b-173">**displayName**: "Someone"</span></span>
    - <span data-ttu-id="1751b-174">**membershipNum**: 6353399</span><span class="sxs-lookup"><span data-stu-id="1751b-174">**membershipNum**: 6353399</span></span>
    - <span data-ttu-id="1751b-175">**active**: true</span><span class="sxs-lookup"><span data-stu-id="1751b-175">**active**: true</span></span>
    - <span data-ttu-id="1751b-176">**birthdate**: 1980-09-23T00:00:00Z</span><span class="sxs-lookup"><span data-stu-id="1751b-176">**birthdate**: 1980-09-23T00:00:00Z</span></span>

## <a name="getnumericclaimfromjson"></a><span data-ttu-id="1751b-177">GetNumericClaimFromJson</span><span class="sxs-lookup"><span data-stu-id="1751b-177">GetNumericClaimFromJson</span></span>

<span data-ttu-id="1751b-178">Gets a specified numeric (long) element from a JSON data.</span><span class="sxs-lookup"><span data-stu-id="1751b-178">Gets a specified numeric (long) element from a JSON data.</span></span>

| <span data-ttu-id="1751b-179">Item</span><span class="sxs-lookup"><span data-stu-id="1751b-179">Item</span></span> | <span data-ttu-id="1751b-180">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="1751b-180">TransformationClaimType</span></span> | <span data-ttu-id="1751b-181">Data Type</span><span class="sxs-lookup"><span data-stu-id="1751b-181">Data Type</span></span> | <span data-ttu-id="1751b-182">Notes</span><span class="sxs-lookup"><span data-stu-id="1751b-182">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="1751b-183">InputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-183">InputClaim</span></span> | <span data-ttu-id="1751b-184">inputJson</span><span class="sxs-lookup"><span data-stu-id="1751b-184">inputJson</span></span> | <span data-ttu-id="1751b-185">string</span><span class="sxs-lookup"><span data-stu-id="1751b-185">string</span></span> | <span data-ttu-id="1751b-186">The ClaimTypes that are used by the claims transformation to get the claim.</span><span class="sxs-lookup"><span data-stu-id="1751b-186">The ClaimTypes that are used by the claims transformation to get the claim.</span></span> |
| <span data-ttu-id="1751b-187">InputParameter</span><span class="sxs-lookup"><span data-stu-id="1751b-187">InputParameter</span></span> | <span data-ttu-id="1751b-188">claimToExtract</span><span class="sxs-lookup"><span data-stu-id="1751b-188">claimToExtract</span></span> | <span data-ttu-id="1751b-189">string</span><span class="sxs-lookup"><span data-stu-id="1751b-189">string</span></span> | <span data-ttu-id="1751b-190">The name of the JSON element to extract.</span><span class="sxs-lookup"><span data-stu-id="1751b-190">The name of the JSON element to extract.</span></span> |
| <span data-ttu-id="1751b-191">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-191">OutputClaim</span></span> | <span data-ttu-id="1751b-192">extractedClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-192">extractedClaim</span></span> | <span data-ttu-id="1751b-193">long</span><span class="sxs-lookup"><span data-stu-id="1751b-193">long</span></span> | <span data-ttu-id="1751b-194">The ClaimType that is produced after this ClaimsTransformation has been invoked, the element's value specified in the _claimToExtract_ input parameters.</span><span class="sxs-lookup"><span data-stu-id="1751b-194">The ClaimType that is produced after this ClaimsTransformation has been invoked, the element's value specified in the _claimToExtract_ input parameters.</span></span> |

<span data-ttu-id="1751b-195">In the following example, the claims transformation extracts the `id` element from the JSON data.</span><span class="sxs-lookup"><span data-stu-id="1751b-195">In the following example, the claims transformation extracts the `id` element from the JSON data.</span></span>

```JSON
{
    "emailAddress": "someone@example.com", 
    "displayName": "Someone", 
    "id" : 6353399
}
```

```XML
<ClaimsTransformation Id="GetIdFromResponse" TransformationMethod="GetNumericClaimFromJson">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="exampleInputClaim" TransformationClaimType="inputJson" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="claimToExtract" DataType="string" Value="id" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="membershipId" TransformationClaimType="extractedClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="1751b-196">Example</span><span class="sxs-lookup"><span data-stu-id="1751b-196">Example</span></span>

- <span data-ttu-id="1751b-197">Input claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-197">Input claims:</span></span>
    - <span data-ttu-id="1751b-198">**inputJson**: {"emailAddress": "someone@example.com", "displayName": "Someone", "id" : 6353399}</span><span class="sxs-lookup"><span data-stu-id="1751b-198">**inputJson**: {"emailAddress": "someone@example.com", "displayName": "Someone", "id" : 6353399}</span></span>
- <span data-ttu-id="1751b-199">Input parameters</span><span class="sxs-lookup"><span data-stu-id="1751b-199">Input parameters</span></span>
    - <span data-ttu-id="1751b-200">**claimToExtract**:  id</span><span class="sxs-lookup"><span data-stu-id="1751b-200">**claimToExtract**:  id</span></span>
- <span data-ttu-id="1751b-201">Output claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-201">Output claims:</span></span> 
    - <span data-ttu-id="1751b-202">**extractedClaim**: 6353399</span><span class="sxs-lookup"><span data-stu-id="1751b-202">**extractedClaim**: 6353399</span></span>

## <a name="getsinglevaluefromjsonarray"></a><span data-ttu-id="1751b-203">GetSingleValueFromJsonArray</span><span class="sxs-lookup"><span data-stu-id="1751b-203">GetSingleValueFromJsonArray</span></span>

<span data-ttu-id="1751b-204">Gets the first element from a JSON data array.</span><span class="sxs-lookup"><span data-stu-id="1751b-204">Gets the first element from a JSON data array.</span></span>

| <span data-ttu-id="1751b-205">Item</span><span class="sxs-lookup"><span data-stu-id="1751b-205">Item</span></span> | <span data-ttu-id="1751b-206">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="1751b-206">TransformationClaimType</span></span> | <span data-ttu-id="1751b-207">Data Type</span><span class="sxs-lookup"><span data-stu-id="1751b-207">Data Type</span></span> | <span data-ttu-id="1751b-208">Notes</span><span class="sxs-lookup"><span data-stu-id="1751b-208">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="1751b-209">InputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-209">InputClaim</span></span> | <span data-ttu-id="1751b-210">inputJsonClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-210">inputJsonClaim</span></span> | <span data-ttu-id="1751b-211">string</span><span class="sxs-lookup"><span data-stu-id="1751b-211">string</span></span> | <span data-ttu-id="1751b-212">The ClaimTypes that are used by the claims transformation to get the item from the JSON array.</span><span class="sxs-lookup"><span data-stu-id="1751b-212">The ClaimTypes that are used by the claims transformation to get the item from the JSON array.</span></span> |
| <span data-ttu-id="1751b-213">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-213">OutputClaim</span></span> | <span data-ttu-id="1751b-214">extractedClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-214">extractedClaim</span></span> | <span data-ttu-id="1751b-215">string</span><span class="sxs-lookup"><span data-stu-id="1751b-215">string</span></span> | <span data-ttu-id="1751b-216">The ClaimType that is produced after this ClaimsTransformation has been invoked, the first element in the JSON array.</span><span class="sxs-lookup"><span data-stu-id="1751b-216">The ClaimType that is produced after this ClaimsTransformation has been invoked, the first element in the JSON array.</span></span> |

<span data-ttu-id="1751b-217">In the following example, the claims transformation extracts the first element (email address) from the JSON array  `["someone@example.com", "Someone", 6353399]`.</span><span class="sxs-lookup"><span data-stu-id="1751b-217">In the following example, the claims transformation extracts the first element (email address) from the JSON array  `["someone@example.com", "Someone", 6353399]`.</span></span>

```XML
<ClaimsTransformation Id="GetEmailFromJson" TransformationMethod="GetSingleValueFromJsonArray">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="userData" TransformationClaimType="inputJsonClaim" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="email" TransformationClaimType="extractedClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="1751b-218">Example</span><span class="sxs-lookup"><span data-stu-id="1751b-218">Example</span></span>

- <span data-ttu-id="1751b-219">Input claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-219">Input claims:</span></span>
    - <span data-ttu-id="1751b-220">**inputJsonClaim**: ["someone@example.com", "Someone", 6353399]</span><span class="sxs-lookup"><span data-stu-id="1751b-220">**inputJsonClaim**: ["someone@example.com", "Someone", 6353399]</span></span>
- <span data-ttu-id="1751b-221">Output claims:</span><span class="sxs-lookup"><span data-stu-id="1751b-221">Output claims:</span></span> 
    - <span data-ttu-id="1751b-222">**extractedClaim**: someone@example.com</span><span class="sxs-lookup"><span data-stu-id="1751b-222">**extractedClaim**: someone@example.com</span></span>

## <a name="xmlstringtojsonstring"></a><span data-ttu-id="1751b-223">XmlStringToJsonString</span><span class="sxs-lookup"><span data-stu-id="1751b-223">XmlStringToJsonString</span></span>

<span data-ttu-id="1751b-224">Converts XML data to JSON format.</span><span class="sxs-lookup"><span data-stu-id="1751b-224">Converts XML data to JSON format.</span></span>

| <span data-ttu-id="1751b-225">Item</span><span class="sxs-lookup"><span data-stu-id="1751b-225">Item</span></span> | <span data-ttu-id="1751b-226">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="1751b-226">TransformationClaimType</span></span> | <span data-ttu-id="1751b-227">Data Type</span><span class="sxs-lookup"><span data-stu-id="1751b-227">Data Type</span></span> | <span data-ttu-id="1751b-228">Notes</span><span class="sxs-lookup"><span data-stu-id="1751b-228">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="1751b-229">InputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-229">InputClaim</span></span> | <span data-ttu-id="1751b-230">xml</span><span class="sxs-lookup"><span data-stu-id="1751b-230">xml</span></span> | <span data-ttu-id="1751b-231">string</span><span class="sxs-lookup"><span data-stu-id="1751b-231">string</span></span> | <span data-ttu-id="1751b-232">The ClaimTypes that are used by the claims transformation to convert the data from XML to JSON format.</span><span class="sxs-lookup"><span data-stu-id="1751b-232">The ClaimTypes that are used by the claims transformation to convert the data from XML to JSON format.</span></span> |
| <span data-ttu-id="1751b-233">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="1751b-233">OutputClaim</span></span> | <span data-ttu-id="1751b-234">json</span><span class="sxs-lookup"><span data-stu-id="1751b-234">json</span></span> | <span data-ttu-id="1751b-235">string</span><span class="sxs-lookup"><span data-stu-id="1751b-235">string</span></span> | <span data-ttu-id="1751b-236">The ClaimType that is produced after this ClaimsTransformation has been invoked, the data in JSON format.</span><span class="sxs-lookup"><span data-stu-id="1751b-236">The ClaimType that is produced after this ClaimsTransformation has been invoked, the data in JSON format.</span></span> |

```XML
<ClaimsTransformation Id="ConvertXmlToJson" TransformationMethod="XmlStringToJsonString">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="intpuXML" TransformationClaimType="xml" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="outputJson" TransformationClaimType="json" />
  </OutputClaims>
</ClaimsTransformation>
```

<span data-ttu-id="1751b-237">In the following example, the claims transformation converts the following XML data to JSON format.</span><span class="sxs-lookup"><span data-stu-id="1751b-237">In the following example, the claims transformation converts the following XML data to JSON format.</span></span>

#### <a name="example"></a><span data-ttu-id="1751b-238">Example</span><span class="sxs-lookup"><span data-stu-id="1751b-238">Example</span></span>
<span data-ttu-id="1751b-239">Input claim:</span><span class="sxs-lookup"><span data-stu-id="1751b-239">Input claim:</span></span>

```XML
<user>
  <name>Someone</name>
  <email>someone@example.com</email>
</user>
```

<span data-ttu-id="1751b-240">Output claim:</span><span class="sxs-lookup"><span data-stu-id="1751b-240">Output claim:</span></span>

```JSON
{
  {
    "user": {
      "name":"Someone",
      "email":"someone@example.com"
    }
  }
}
```

