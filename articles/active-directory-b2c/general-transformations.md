---
title: General claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: General claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: a13cb0360a33c301129f2975ce67580204602d9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870353"
---
# <a name="general-claims-transformations"></a><span data-ttu-id="62b3b-103">General claims transformations</span><span class="sxs-lookup"><span data-stu-id="62b3b-103">General claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="62b3b-104">This article provides examples for using general claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="62b3b-104">This article provides examples for using general claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="62b3b-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="62b3b-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="doesclaimexist"></a><span data-ttu-id="62b3b-106">DoesClaimExist</span><span class="sxs-lookup"><span data-stu-id="62b3b-106">DoesClaimExist</span></span>

<span data-ttu-id="62b3b-107">Checks if the **inputClaim** exists or not and sets **outputClaim** to true or false accordingly.</span><span class="sxs-lookup"><span data-stu-id="62b3b-107">Checks if the **inputClaim** exists or not and sets **outputClaim** to true or false accordingly.</span></span>

| <span data-ttu-id="62b3b-108">Item</span><span class="sxs-lookup"><span data-stu-id="62b3b-108">Item</span></span> | <span data-ttu-id="62b3b-109">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="62b3b-109">TransformationClaimType</span></span> | <span data-ttu-id="62b3b-110">Data Type</span><span class="sxs-lookup"><span data-stu-id="62b3b-110">Data Type</span></span> | <span data-ttu-id="62b3b-111">Notes</span><span class="sxs-lookup"><span data-stu-id="62b3b-111">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="62b3b-112">InputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-112">InputClaim</span></span> | <span data-ttu-id="62b3b-113">inputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-113">inputClaim</span></span> |<span data-ttu-id="62b3b-114">Any</span><span class="sxs-lookup"><span data-stu-id="62b3b-114">Any</span></span> | <span data-ttu-id="62b3b-115">The input claim whose existence needs to be verified.</span><span class="sxs-lookup"><span data-stu-id="62b3b-115">The input claim whose existence needs to be verified.</span></span> |
| <span data-ttu-id="62b3b-116">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-116">OutputClaim</span></span> | <span data-ttu-id="62b3b-117">outputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-117">outputClaim</span></span> | <span data-ttu-id="62b3b-118">boolean</span><span class="sxs-lookup"><span data-stu-id="62b3b-118">boolean</span></span> | <span data-ttu-id="62b3b-119">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="62b3b-119">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span></span> |

<span data-ttu-id="62b3b-120">Use this claims transformation to check if a claim exists or contains any value.</span><span class="sxs-lookup"><span data-stu-id="62b3b-120">Use this claims transformation to check if a claim exists or contains any value.</span></span> <span data-ttu-id="62b3b-121">The return value is a boolean that indicates whether the claim exists.</span><span class="sxs-lookup"><span data-stu-id="62b3b-121">The return value is a boolean that indicates whether the claim exists.</span></span> <span data-ttu-id="62b3b-122">Following example checks if the email address exists.</span><span class="sxs-lookup"><span data-stu-id="62b3b-122">Following example checks if the email address exists.</span></span>

```XML
<ClaimsTransformation Id="CheckIfEmailPresent" TransformationMethod="DoesClaimExist">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="email" TransformationClaimType="inputClaim" />
  </InputClaims>                    
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="isEmailPresent" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="62b3b-123">Example</span><span class="sxs-lookup"><span data-stu-id="62b3b-123">Example</span></span>

- <span data-ttu-id="62b3b-124">Input claims:</span><span class="sxs-lookup"><span data-stu-id="62b3b-124">Input claims:</span></span>
    - <span data-ttu-id="62b3b-125">**inputClaim**: someone@contoso.com</span><span class="sxs-lookup"><span data-stu-id="62b3b-125">**inputClaim**: someone@contoso.com</span></span>
- <span data-ttu-id="62b3b-126">Output claims:</span><span class="sxs-lookup"><span data-stu-id="62b3b-126">Output claims:</span></span> 
    - <span data-ttu-id="62b3b-127">**outputClaim**: true</span><span class="sxs-lookup"><span data-stu-id="62b3b-127">**outputClaim**: true</span></span>

## <a name="hash"></a><span data-ttu-id="62b3b-128">Hash</span><span class="sxs-lookup"><span data-stu-id="62b3b-128">Hash</span></span>

<span data-ttu-id="62b3b-129">Hash the provided plain text using the salt and a secret.</span><span class="sxs-lookup"><span data-stu-id="62b3b-129">Hash the provided plain text using the salt and a secret.</span></span>

| <span data-ttu-id="62b3b-130">Item</span><span class="sxs-lookup"><span data-stu-id="62b3b-130">Item</span></span> | <span data-ttu-id="62b3b-131">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="62b3b-131">TransformationClaimType</span></span> | <span data-ttu-id="62b3b-132">Data Type</span><span class="sxs-lookup"><span data-stu-id="62b3b-132">Data Type</span></span> | <span data-ttu-id="62b3b-133">Notes</span><span class="sxs-lookup"><span data-stu-id="62b3b-133">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="62b3b-134">InputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-134">InputClaim</span></span> | <span data-ttu-id="62b3b-135">plaintext</span><span class="sxs-lookup"><span data-stu-id="62b3b-135">plaintext</span></span> | <span data-ttu-id="62b3b-136">string</span><span class="sxs-lookup"><span data-stu-id="62b3b-136">string</span></span> | <span data-ttu-id="62b3b-137">The input claim to be encrypted</span><span class="sxs-lookup"><span data-stu-id="62b3b-137">The input claim to be encrypted</span></span> |
| <span data-ttu-id="62b3b-138">InputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-138">InputClaim</span></span> | <span data-ttu-id="62b3b-139">salt</span><span class="sxs-lookup"><span data-stu-id="62b3b-139">salt</span></span> | <span data-ttu-id="62b3b-140">string</span><span class="sxs-lookup"><span data-stu-id="62b3b-140">string</span></span> | <span data-ttu-id="62b3b-141">The salt parameter.</span><span class="sxs-lookup"><span data-stu-id="62b3b-141">The salt parameter.</span></span> <span data-ttu-id="62b3b-142">You can create a random value, using `CreateRandomString` claims transformation.</span><span class="sxs-lookup"><span data-stu-id="62b3b-142">You can create a random value, using `CreateRandomString` claims transformation.</span></span> |
| <span data-ttu-id="62b3b-143">InputParameter</span><span class="sxs-lookup"><span data-stu-id="62b3b-143">InputParameter</span></span> | <span data-ttu-id="62b3b-144">randomizerSecret</span><span class="sxs-lookup"><span data-stu-id="62b3b-144">randomizerSecret</span></span> | <span data-ttu-id="62b3b-145">string</span><span class="sxs-lookup"><span data-stu-id="62b3b-145">string</span></span> | <span data-ttu-id="62b3b-146">Points to an existing Azure AD B2C **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="62b3b-146">Points to an existing Azure AD B2C **Policy Keys**.</span></span> <span data-ttu-id="62b3b-147">To create a new one: In your Azure AD B2C tenant, select **B2C Settings > Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="62b3b-147">To create a new one: In your Azure AD B2C tenant, select **B2C Settings > Identity Experience Framework**.</span></span> <span data-ttu-id="62b3b-148">Select **Policy Keys** to view the keys that are available in your tenant.</span><span class="sxs-lookup"><span data-stu-id="62b3b-148">Select **Policy Keys** to view the keys that are available in your tenant.</span></span> <span data-ttu-id="62b3b-149">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="62b3b-149">Select **Add**.</span></span> <span data-ttu-id="62b3b-150">For **Options**, select **Manual**.</span><span class="sxs-lookup"><span data-stu-id="62b3b-150">For **Options**, select **Manual**.</span></span> <span data-ttu-id="62b3b-151">Provide a name (the prefix B2C_1A_ might be added automatically.).</span><span class="sxs-lookup"><span data-stu-id="62b3b-151">Provide a name (the prefix B2C_1A_ might be added automatically.).</span></span> <span data-ttu-id="62b3b-152">In the Secret box, enter any secret you want to use, such as 1234567890.</span><span class="sxs-lookup"><span data-stu-id="62b3b-152">In the Secret box, enter any secret you want to use, such as 1234567890.</span></span> <span data-ttu-id="62b3b-153">For Key usage, select **Secret**.</span><span class="sxs-lookup"><span data-stu-id="62b3b-153">For Key usage, select **Secret**.</span></span> <span data-ttu-id="62b3b-154">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="62b3b-154">Select **Create**.</span></span> |
| <span data-ttu-id="62b3b-155">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-155">OutputClaim</span></span> | <span data-ttu-id="62b3b-156">outputClaim</span><span class="sxs-lookup"><span data-stu-id="62b3b-156">outputClaim</span></span> | <span data-ttu-id="62b3b-157">boolean</span><span class="sxs-lookup"><span data-stu-id="62b3b-157">boolean</span></span> | <span data-ttu-id="62b3b-158">The ClaimType that is produced after this claims transformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="62b3b-158">The ClaimType that is produced after this claims transformation has been invoked.</span></span> <span data-ttu-id="62b3b-159">The claim configured in the `plaintext` inputClaim.</span><span class="sxs-lookup"><span data-stu-id="62b3b-159">The claim configured in the `plaintext` inputClaim.</span></span> |

```XML
<ClaimsTransformation Id="HashPasswordWithEmail" TransformationMethod="Hash">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="password" TransformationClaimType="plaintext" />
    <InputClaim ClaimTypeReferenceId="email" TransformationClaimType="salt" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="randomizerSecret" DataType="string" Value="B2C_1A_AccountTransformSecret" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="hashedPassword" TransformationClaimType="hash" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="62b3b-160">Example</span><span class="sxs-lookup"><span data-stu-id="62b3b-160">Example</span></span>

- <span data-ttu-id="62b3b-161">Input claims:</span><span class="sxs-lookup"><span data-stu-id="62b3b-161">Input claims:</span></span>
    - <span data-ttu-id="62b3b-162">**plaintext**: MyPass@word1</span><span class="sxs-lookup"><span data-stu-id="62b3b-162">**plaintext**: MyPass@word1</span></span>
    - <span data-ttu-id="62b3b-163">**salt**: 487624568</span><span class="sxs-lookup"><span data-stu-id="62b3b-163">**salt**: 487624568</span></span>
    - <span data-ttu-id="62b3b-164">**randomizerSecret**: B2C_1A_AccountTransformSecret</span><span class="sxs-lookup"><span data-stu-id="62b3b-164">**randomizerSecret**: B2C_1A_AccountTransformSecret</span></span>
- <span data-ttu-id="62b3b-165">Output claims:</span><span class="sxs-lookup"><span data-stu-id="62b3b-165">Output claims:</span></span> 
    - <span data-ttu-id="62b3b-166">**outputClaim**: CdMNb/KTEfsWzh9MR1kQGRZCKjuxGMWhA5YQNihzV6U=</span><span class="sxs-lookup"><span data-stu-id="62b3b-166">**outputClaim**: CdMNb/KTEfsWzh9MR1kQGRZCKjuxGMWhA5YQNihzV6U=</span></span>



