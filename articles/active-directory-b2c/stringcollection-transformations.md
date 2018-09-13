---
title: StringCollection claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: StringCollection claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: cfc190d862c161783c2dd5fc7f03b7bb1ae6bed9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865396"
---
# <a name="stringcollection-claims-transformations"></a><span data-ttu-id="4c47a-103">StringCollection claims transformations</span><span class="sxs-lookup"><span data-stu-id="4c47a-103">StringCollection claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="4c47a-104">This article provides examples for using the string collection claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="4c47a-104">This article provides examples for using the string collection claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="4c47a-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="4c47a-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="additemtostringcollection"></a><span data-ttu-id="4c47a-106">AddItemToStringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-106">AddItemToStringCollection</span></span>

<span data-ttu-id="4c47a-107">Adds a string claim to a new stringCollection claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-107">Adds a string claim to a new stringCollection claim.</span></span> 

| <span data-ttu-id="4c47a-108">Item</span><span class="sxs-lookup"><span data-stu-id="4c47a-108">Item</span></span> | <span data-ttu-id="4c47a-109">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="4c47a-109">TransformationClaimType</span></span> | <span data-ttu-id="4c47a-110">Data Type</span><span class="sxs-lookup"><span data-stu-id="4c47a-110">Data Type</span></span> | <span data-ttu-id="4c47a-111">Notes</span><span class="sxs-lookup"><span data-stu-id="4c47a-111">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="4c47a-112">InputClaim</span><span class="sxs-lookup"><span data-stu-id="4c47a-112">InputClaim</span></span> | <span data-ttu-id="4c47a-113">item</span><span class="sxs-lookup"><span data-stu-id="4c47a-113">item</span></span> | <span data-ttu-id="4c47a-114">string</span><span class="sxs-lookup"><span data-stu-id="4c47a-114">string</span></span> | <span data-ttu-id="4c47a-115">The ClaimType to be added to the output claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-115">The ClaimType to be added to the output claim.</span></span> |
| <span data-ttu-id="4c47a-116">InputClaim</span><span class="sxs-lookup"><span data-stu-id="4c47a-116">InputClaim</span></span> | <span data-ttu-id="4c47a-117">collection</span><span class="sxs-lookup"><span data-stu-id="4c47a-117">collection</span></span> | <span data-ttu-id="4c47a-118">stringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-118">stringCollection</span></span> | <span data-ttu-id="4c47a-119">[Optional] If specified, the claims transformation copies the items from this collection, and adds the item to the end of the output collection claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-119">[Optional] If specified, the claims transformation copies the items from this collection, and adds the item to the end of the output collection claim.</span></span> |
| <span data-ttu-id="4c47a-120">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="4c47a-120">OutputClaim</span></span> | <span data-ttu-id="4c47a-121">collection</span><span class="sxs-lookup"><span data-stu-id="4c47a-121">collection</span></span> | <span data-ttu-id="4c47a-122">stringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-122">stringCollection</span></span> | <span data-ttu-id="4c47a-123">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="4c47a-123">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span></span> |

<span data-ttu-id="4c47a-124">Use this claims transformation to add a string to a new or existing stringCollection.</span><span class="sxs-lookup"><span data-stu-id="4c47a-124">Use this claims transformation to add a string to a new or existing stringCollection.</span></span> <span data-ttu-id="4c47a-125">It's commonly used in a **AAD-UserWriteUsingAlternativeSecurityId** technical profile.</span><span class="sxs-lookup"><span data-stu-id="4c47a-125">It's commonly used in a **AAD-UserWriteUsingAlternativeSecurityId** technical profile.</span></span> <span data-ttu-id="4c47a-126">Before a new social account is created, **CreateOtherMailsFromEmail** claims transformation reads the ClaimType and adds the value to the **otherMails** ClaimType.</span><span class="sxs-lookup"><span data-stu-id="4c47a-126">Before a new social account is created, **CreateOtherMailsFromEmail** claims transformation reads the ClaimType and adds the value to the **otherMails** ClaimType.</span></span> 

<span data-ttu-id="4c47a-127">The following claims transformation adds the **email** ClaimType to **otherMails** ClaimType.</span><span class="sxs-lookup"><span data-stu-id="4c47a-127">The following claims transformation adds the **email** ClaimType to **otherMails** ClaimType.</span></span>

```XML
<ClaimsTransformation Id="CreateOtherMailsFromEmail" TransformationMethod="AddItemToStringCollection">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="email" TransformationClaimType="item" />
    <InputClaim ClaimTypeReferenceId="otherMails" TransformationClaimType="collection" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="otherMails" TransformationClaimType="collection" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="4c47a-128">Example</span><span class="sxs-lookup"><span data-stu-id="4c47a-128">Example</span></span>

- <span data-ttu-id="4c47a-129">Input claims:</span><span class="sxs-lookup"><span data-stu-id="4c47a-129">Input claims:</span></span>
    - <span data-ttu-id="4c47a-130">**collection**: ["someone@outlook.com"]</span><span class="sxs-lookup"><span data-stu-id="4c47a-130">**collection**: ["someone@outlook.com"]</span></span>
    - <span data-ttu-id="4c47a-131">**item**: "admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="4c47a-131">**item**: "admin@contoso.com"</span></span>
- <span data-ttu-id="4c47a-132">Output claims: admin@contoso.com</span><span class="sxs-lookup"><span data-stu-id="4c47a-132">Output claims: admin@contoso.com</span></span>
    - <span data-ttu-id="4c47a-133">**collection**: ["someone@outlook.com", "admin@contoso.com"]</span><span class="sxs-lookup"><span data-stu-id="4c47a-133">**collection**: ["someone@outlook.com", "admin@contoso.com"]</span></span>

## <a name="addparametertostringcollection"></a><span data-ttu-id="4c47a-134">AddParameterToStringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-134">AddParameterToStringCollection</span></span>

<span data-ttu-id="4c47a-135">Adds a string parameter to a new stringCollection claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-135">Adds a string parameter to a new stringCollection claim.</span></span> 

| <span data-ttu-id="4c47a-136">Item</span><span class="sxs-lookup"><span data-stu-id="4c47a-136">Item</span></span> | <span data-ttu-id="4c47a-137">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="4c47a-137">TransformationClaimType</span></span> | <span data-ttu-id="4c47a-138">Data Type</span><span class="sxs-lookup"><span data-stu-id="4c47a-138">Data Type</span></span> | <span data-ttu-id="4c47a-139">Notes</span><span class="sxs-lookup"><span data-stu-id="4c47a-139">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="4c47a-140">InputClaim</span><span class="sxs-lookup"><span data-stu-id="4c47a-140">InputClaim</span></span> | <span data-ttu-id="4c47a-141">collection</span><span class="sxs-lookup"><span data-stu-id="4c47a-141">collection</span></span> | <span data-ttu-id="4c47a-142">stringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-142">stringCollection</span></span> | <span data-ttu-id="4c47a-143">[Optional] If specified, the claims transformation copies the items from this collection, and adds the item to the end of the output collection claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-143">[Optional] If specified, the claims transformation copies the items from this collection, and adds the item to the end of the output collection claim.</span></span> |
| <span data-ttu-id="4c47a-144">InputParameter</span><span class="sxs-lookup"><span data-stu-id="4c47a-144">InputParameter</span></span> | <span data-ttu-id="4c47a-145">item</span><span class="sxs-lookup"><span data-stu-id="4c47a-145">item</span></span> | <span data-ttu-id="4c47a-146">string</span><span class="sxs-lookup"><span data-stu-id="4c47a-146">string</span></span> | <span data-ttu-id="4c47a-147">The value to be added to the output claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-147">The value to be added to the output claim.</span></span> |
| <span data-ttu-id="4c47a-148">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="4c47a-148">OutputClaim</span></span> | <span data-ttu-id="4c47a-149">collection</span><span class="sxs-lookup"><span data-stu-id="4c47a-149">collection</span></span> | <span data-ttu-id="4c47a-150">stringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-150">stringCollection</span></span> | <span data-ttu-id="4c47a-151">The ClaimTypes that will be produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="4c47a-151">The ClaimTypes that will be produced after this ClaimsTransformation has been invoked.</span></span> |

<span data-ttu-id="4c47a-152">Use this claims transformation to add a string value to a new or existing stringCollection.</span><span class="sxs-lookup"><span data-stu-id="4c47a-152">Use this claims transformation to add a string value to a new or existing stringCollection.</span></span> <span data-ttu-id="4c47a-153">The following example adds a constant email address (admin@contoso.com) to the **otherMails** claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-153">The following example adds a constant email address (admin@contoso.com) to the **otherMails** claim.</span></span> 

```XML
<ClaimsTransformation Id="SetCompanyEmail" TransformationMethod="AddParameterToStringCollection">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="otherMails" TransformationClaimType="collection" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="item" DataType="string" Value="admin@contoso.com" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="otherMails" TransformationClaimType="collection" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="4c47a-154">Example</span><span class="sxs-lookup"><span data-stu-id="4c47a-154">Example</span></span>

- <span data-ttu-id="4c47a-155">Input claims:</span><span class="sxs-lookup"><span data-stu-id="4c47a-155">Input claims:</span></span>
    - <span data-ttu-id="4c47a-156">**collection**: ["someone@outlook.com"]</span><span class="sxs-lookup"><span data-stu-id="4c47a-156">**collection**: ["someone@outlook.com"]</span></span>
- <span data-ttu-id="4c47a-157">Input parameters</span><span class="sxs-lookup"><span data-stu-id="4c47a-157">Input parameters</span></span> 
    - <span data-ttu-id="4c47a-158">**item**: "admin@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="4c47a-158">**item**: "admin@contoso.com"</span></span>
- <span data-ttu-id="4c47a-159">Output claims: admin@contoso.com</span><span class="sxs-lookup"><span data-stu-id="4c47a-159">Output claims: admin@contoso.com</span></span>
    - <span data-ttu-id="4c47a-160">**collection**: ["someone@outlook.com", "admin@contoso.com"]</span><span class="sxs-lookup"><span data-stu-id="4c47a-160">**collection**: ["someone@outlook.com", "admin@contoso.com"]</span></span>

## <a name="getsingleitemfromstringcollection"></a><span data-ttu-id="4c47a-161">GetSingleItemFromStringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-161">GetSingleItemFromStringCollection</span></span>

<span data-ttu-id="4c47a-162">Gets the first item from the provided string collection.</span><span class="sxs-lookup"><span data-stu-id="4c47a-162">Gets the first item from the provided string collection.</span></span> 

| <span data-ttu-id="4c47a-163">Item</span><span class="sxs-lookup"><span data-stu-id="4c47a-163">Item</span></span> | <span data-ttu-id="4c47a-164">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="4c47a-164">TransformationClaimType</span></span> | <span data-ttu-id="4c47a-165">Data Type</span><span class="sxs-lookup"><span data-stu-id="4c47a-165">Data Type</span></span> | <span data-ttu-id="4c47a-166">Notes</span><span class="sxs-lookup"><span data-stu-id="4c47a-166">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="4c47a-167">InputClaim</span><span class="sxs-lookup"><span data-stu-id="4c47a-167">InputClaim</span></span> | <span data-ttu-id="4c47a-168">collection</span><span class="sxs-lookup"><span data-stu-id="4c47a-168">collection</span></span> | <span data-ttu-id="4c47a-169">stringCollection</span><span class="sxs-lookup"><span data-stu-id="4c47a-169">stringCollection</span></span> | <span data-ttu-id="4c47a-170">The ClaimTypes that are used by the claims transformation to get the item.</span><span class="sxs-lookup"><span data-stu-id="4c47a-170">The ClaimTypes that are used by the claims transformation to get the item.</span></span> |
| <span data-ttu-id="4c47a-171">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="4c47a-171">OutputClaim</span></span> | <span data-ttu-id="4c47a-172">extractedItem</span><span class="sxs-lookup"><span data-stu-id="4c47a-172">extractedItem</span></span> | <span data-ttu-id="4c47a-173">string</span><span class="sxs-lookup"><span data-stu-id="4c47a-173">string</span></span> | <span data-ttu-id="4c47a-174">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="4c47a-174">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span></span> <span data-ttu-id="4c47a-175">The first item in the collection.</span><span class="sxs-lookup"><span data-stu-id="4c47a-175">The first item in the collection.</span></span> |

<span data-ttu-id="4c47a-176">The following example reads the **otherMails** claim and return the first item into the **email** claim.</span><span class="sxs-lookup"><span data-stu-id="4c47a-176">The following example reads the **otherMails** claim and return the first item into the **email** claim.</span></span> 

```XML
<ClaimsTransformation Id="CreateEmailFromOtherMails" TransformationMethod="GetSingleItemFromStringCollection">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="otherMails" TransformationClaimType="collection" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="email" TransformationClaimType="extractedItem" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="4c47a-177">Example</span><span class="sxs-lookup"><span data-stu-id="4c47a-177">Example</span></span>

- <span data-ttu-id="4c47a-178">Input claims:</span><span class="sxs-lookup"><span data-stu-id="4c47a-178">Input claims:</span></span>
    - <span data-ttu-id="4c47a-179">**collection**: ["someone@outlook.com", "someone@contoso.com"]</span><span class="sxs-lookup"><span data-stu-id="4c47a-179">**collection**: ["someone@outlook.com", "someone@contoso.com"]</span></span>
- <span data-ttu-id="4c47a-180">Output claims:</span><span class="sxs-lookup"><span data-stu-id="4c47a-180">Output claims:</span></span> 
    - <span data-ttu-id="4c47a-181">**extractedItem**: "someone@outlook.com"</span><span class="sxs-lookup"><span data-stu-id="4c47a-181">**extractedItem**: "someone@outlook.com"</span></span>

