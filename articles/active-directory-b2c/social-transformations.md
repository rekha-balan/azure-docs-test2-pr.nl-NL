---
title: Social account claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: Social account claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: d9b592e7f61b87860e4f6fa2aa4d46e253b6257e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857354"
---
# <a name="social-accounts-claims-transformations"></a><span data-ttu-id="55c87-103">Social accounts claims transformations</span><span class="sxs-lookup"><span data-stu-id="55c87-103">Social accounts claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="55c87-104">In Azure Active Directory (Azure AD) B2C, social account identities are stored in a `userIdentities` attribute of a **alternativeSecurityIdCollection** claim type.</span><span class="sxs-lookup"><span data-stu-id="55c87-104">In Azure Active Directory (Azure AD) B2C, social account identities are stored in a `userIdentities` attribute of a **alternativeSecurityIdCollection** claim type.</span></span> <span data-ttu-id="55c87-105">Each item in the **alternativeSecurityIdCollection** specifies the issuer (identity provider name, such as facebook.com) and the `issuerUserId`, which is a unique user identifier for the issuer.</span><span class="sxs-lookup"><span data-stu-id="55c87-105">Each item in the **alternativeSecurityIdCollection** specifies the issuer (identity provider name, such as facebook.com) and the `issuerUserId`, which is a unique user identifier for the issuer.</span></span> 

```JSON
"userIdentities": [{
    "issuer": "google.com",
    "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw"
  },
  {
    "issuer": "facebook.com",
    "issuerUserId": "MTIzNDU="
  }]
```

This article provides examples for using the social account claims transformations of the Identity Experience Framework schema in Azure AD B2C. <span data-ttu-id="55c87-107">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="55c87-107">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="createalternativesecurityid"></a><span data-ttu-id="55c87-108">CreateAlternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="55c87-108">CreateAlternativeSecurityId</span></span>

<span data-ttu-id="55c87-109">Creates a JSON representation of the user’s alternativeSecurityId property that can be used in the calls to Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="55c87-109">Creates a JSON representation of the user’s alternativeSecurityId property that can be used in the calls to Azure Active Directory.</span></span> <span data-ttu-id="55c87-110">For more information, see [AlternativeSecurityId's schema](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#AlternativeSecurityIdType).</span><span class="sxs-lookup"><span data-stu-id="55c87-110">For more information, see [AlternativeSecurityId's schema](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#AlternativeSecurityIdType).</span></span>

| <span data-ttu-id="55c87-111">Item</span><span class="sxs-lookup"><span data-stu-id="55c87-111">Item</span></span> | <span data-ttu-id="55c87-112">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="55c87-112">TransformationClaimType</span></span> | <span data-ttu-id="55c87-113">Data Type</span><span class="sxs-lookup"><span data-stu-id="55c87-113">Data Type</span></span> | <span data-ttu-id="55c87-114">Notes</span><span class="sxs-lookup"><span data-stu-id="55c87-114">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="55c87-115">InputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-115">InputClaim</span></span> | <span data-ttu-id="55c87-116">key</span><span class="sxs-lookup"><span data-stu-id="55c87-116">key</span></span> | <span data-ttu-id="55c87-117">string</span><span class="sxs-lookup"><span data-stu-id="55c87-117">string</span></span> | <span data-ttu-id="55c87-118">The ClaimType that specifies the unique user identifier used by the social identity provider.</span><span class="sxs-lookup"><span data-stu-id="55c87-118">The ClaimType that specifies the unique user identifier used by the social identity provider.</span></span> |
| <span data-ttu-id="55c87-119">InputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-119">InputClaim</span></span> | <span data-ttu-id="55c87-120">identityProvider</span><span class="sxs-lookup"><span data-stu-id="55c87-120">identityProvider</span></span> | <span data-ttu-id="55c87-121">string</span><span class="sxs-lookup"><span data-stu-id="55c87-121">string</span></span> | <span data-ttu-id="55c87-122">The ClaimType that specifies the social account identity provider name, such as facebook.com.</span><span class="sxs-lookup"><span data-stu-id="55c87-122">The ClaimType that specifies the social account identity provider name, such as facebook.com.</span></span> |
| <span data-ttu-id="55c87-123">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-123">OutputClaim</span></span> | <span data-ttu-id="55c87-124">alternativeSecurityId</span><span class="sxs-lookup"><span data-stu-id="55c87-124">alternativeSecurityId</span></span> | <span data-ttu-id="55c87-125">string</span><span class="sxs-lookup"><span data-stu-id="55c87-125">string</span></span> | <span data-ttu-id="55c87-126">The ClaimType that is produced after the ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="55c87-126">The ClaimType that is produced after the ClaimsTransformation has been invoked.</span></span> <span data-ttu-id="55c87-127">Contains information about the identity of a social account user.</span><span class="sxs-lookup"><span data-stu-id="55c87-127">Contains information about the identity of a social account user.</span></span> <span data-ttu-id="55c87-128">The **issuer** is the value of the `identityProvider` claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-128">The **issuer** is the value of the `identityProvider` claim.</span></span> <span data-ttu-id="55c87-129">The **issuerUserId** is the value of the `key` claim in base64 format.</span><span class="sxs-lookup"><span data-stu-id="55c87-129">The **issuerUserId** is the value of the `key` claim in base64 format.</span></span> |

<span data-ttu-id="55c87-130">Use this claims transformation to generate a `alternativeSecurityId` ClaimType.</span><span class="sxs-lookup"><span data-stu-id="55c87-130">Use this claims transformation to generate a `alternativeSecurityId` ClaimType.</span></span> <span data-ttu-id="55c87-131">It's used by all social identity provider technical profiles, such as `Facebook-OAUTH`.</span><span class="sxs-lookup"><span data-stu-id="55c87-131">It's used by all social identity provider technical profiles, such as `Facebook-OAUTH`.</span></span> <span data-ttu-id="55c87-132">The following claims transformation receives the user social account ID and the identity provider name.</span><span class="sxs-lookup"><span data-stu-id="55c87-132">The following claims transformation receives the user social account ID and the identity provider name.</span></span> <span data-ttu-id="55c87-133">The output of this technical profile is a JSON string format that can be used in Azure AD directory services.</span><span class="sxs-lookup"><span data-stu-id="55c87-133">The output of this technical profile is a JSON string format that can be used in Azure AD directory services.</span></span>  

```XML
<ClaimsTransformation Id="CreateAlternativeSecurityId" TransformationMethod="CreateAlternativeSecurityId">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="socialIdpUserId" TransformationClaimType="key" />
    <InputClaim ClaimTypeReferenceId="identityProvider" TransformationClaimType="identityProvider" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="alternativeSecurityId" TransformationClaimType="alternativeSecurityId" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="55c87-134">Example</span><span class="sxs-lookup"><span data-stu-id="55c87-134">Example</span></span>

- <span data-ttu-id="55c87-135">Input claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-135">Input claims:</span></span>
    - <span data-ttu-id="55c87-136">**key**: 12334</span><span class="sxs-lookup"><span data-stu-id="55c87-136">**key**: 12334</span></span>
    - <span data-ttu-id="55c87-137">**identityProvider**: Facebook.com</span><span class="sxs-lookup"><span data-stu-id="55c87-137">**identityProvider**: Facebook.com</span></span>
- <span data-ttu-id="55c87-138">Output claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-138">Output claims:</span></span>
    - <span data-ttu-id="55c87-139">**alternativeSecurityId**: { "issuer": "facebook.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw"}</span><span class="sxs-lookup"><span data-stu-id="55c87-139">**alternativeSecurityId**: { "issuer": "facebook.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw"}</span></span>

## <a name="additemtoalternativesecurityidcollection"></a><span data-ttu-id="55c87-140">AddItemToAlternativeSecurityIdCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-140">AddItemToAlternativeSecurityIdCollection</span></span>

<span data-ttu-id="55c87-141">Adds an `AlternativeSecurityId` to an `alternativeSecurityIdCollection` claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-141">Adds an `AlternativeSecurityId` to an `alternativeSecurityIdCollection` claim.</span></span> 

| <span data-ttu-id="55c87-142">Item</span><span class="sxs-lookup"><span data-stu-id="55c87-142">Item</span></span> | <span data-ttu-id="55c87-143">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="55c87-143">TransformationClaimType</span></span> | <span data-ttu-id="55c87-144">Data Type</span><span class="sxs-lookup"><span data-stu-id="55c87-144">Data Type</span></span> | <span data-ttu-id="55c87-145">Notes</span><span class="sxs-lookup"><span data-stu-id="55c87-145">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="55c87-146">InputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-146">InputClaim</span></span> | <span data-ttu-id="55c87-147">item</span><span class="sxs-lookup"><span data-stu-id="55c87-147">item</span></span> | <span data-ttu-id="55c87-148">string</span><span class="sxs-lookup"><span data-stu-id="55c87-148">string</span></span> | <span data-ttu-id="55c87-149">The ClaimType to be added to the output claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-149">The ClaimType to be added to the output claim.</span></span> |
| <span data-ttu-id="55c87-150">InputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-150">InputClaim</span></span> | <span data-ttu-id="55c87-151">collection</span><span class="sxs-lookup"><span data-stu-id="55c87-151">collection</span></span> | <span data-ttu-id="55c87-152">alternativeSecurityIdCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-152">alternativeSecurityIdCollection</span></span> | <span data-ttu-id="55c87-153">The ClaimTypes that are used by the claims transformation if available in the policy.</span><span class="sxs-lookup"><span data-stu-id="55c87-153">The ClaimTypes that are used by the claims transformation if available in the policy.</span></span> <span data-ttu-id="55c87-154">If provided, the claims transformation adds the `item` at the end of the collection.</span><span class="sxs-lookup"><span data-stu-id="55c87-154">If provided, the claims transformation adds the `item` at the end of the collection.</span></span> |
| <span data-ttu-id="55c87-155">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-155">OutputClaim</span></span> | <span data-ttu-id="55c87-156">collection</span><span class="sxs-lookup"><span data-stu-id="55c87-156">collection</span></span> | <span data-ttu-id="55c87-157">alternativeSecurityIdCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-157">alternativeSecurityIdCollection</span></span> | <span data-ttu-id="55c87-158">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="55c87-158">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span></span> <span data-ttu-id="55c87-159">The new collection that contains both the items from input `collection` and `item`.</span><span class="sxs-lookup"><span data-stu-id="55c87-159">The new collection that contains both the items from input `collection` and `item`.</span></span> |

<span data-ttu-id="55c87-160">The following example links a new social identity with an existing account.</span><span class="sxs-lookup"><span data-stu-id="55c87-160">The following example links a new social identity with an existing account.</span></span> <span data-ttu-id="55c87-161">To link a new social identity:</span><span class="sxs-lookup"><span data-stu-id="55c87-161">To link a new social identity:</span></span> 
1. <span data-ttu-id="55c87-162">In the **AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserReadUsingObjectId** technical profiles, output the user's **alternativeSecurityIds** claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-162">In the **AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserReadUsingObjectId** technical profiles, output the user's **alternativeSecurityIds** claim.</span></span>
1. <span data-ttu-id="55c87-163">Ask the user to sign in with one of the identity providers that are not associated with this user.</span><span class="sxs-lookup"><span data-stu-id="55c87-163">Ask the user to sign in with one of the identity providers that are not associated with this user.</span></span> 
1. <span data-ttu-id="55c87-164">Using the **CreateAlternativeSecurityId** claims transformation, create a new **alternativeSecurityId** claim type with a name of `AlternativeSecurityId2`</span><span class="sxs-lookup"><span data-stu-id="55c87-164">Using the **CreateAlternativeSecurityId** claims transformation, create a new **alternativeSecurityId** claim type with a name of `AlternativeSecurityId2`</span></span> 
1. <span data-ttu-id="55c87-165">Call the **AddItemToAlternativeSecurityIdCollection** claims transformation to add the **AlternativeSecurityId2** claim to the existing **AlternativeSecurityIds** claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-165">Call the **AddItemToAlternativeSecurityIdCollection** claims transformation to add the **AlternativeSecurityId2** claim to the existing **AlternativeSecurityIds** claim.</span></span> 
1. <span data-ttu-id="55c87-166">Persist the **alternativeSecurityIds** claim to the user account</span><span class="sxs-lookup"><span data-stu-id="55c87-166">Persist the **alternativeSecurityIds** claim to the user account</span></span>

```XML
<ClaimsTransformation Id="AddAnotherAlternativeSecurityId" TransformationMethod="AddItemToAlternativeSecurityIdCollection">
  <InputClaims>
      <InputClaim ClaimTypeReferenceId="AlternativeSecurityId2" TransformationClaimType="item" />
      <InputClaim ClaimTypeReferenceId="AlternativeSecurityIds" TransformationClaimType="collection" />
  </InputClaims>
  <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="AlternativeSecurityIds" TransformationClaimType="collection" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="55c87-167">Example</span><span class="sxs-lookup"><span data-stu-id="55c87-167">Example</span></span>

- <span data-ttu-id="55c87-168">Input claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-168">Input claims:</span></span>
    - <span data-ttu-id="55c87-169">**item**: { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" }</span><span class="sxs-lookup"><span data-stu-id="55c87-169">**item**: { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" }</span></span>
    - <span data-ttu-id="55c87-170">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" } ]</span><span class="sxs-lookup"><span data-stu-id="55c87-170">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" } ]</span></span>
- <span data-ttu-id="55c87-171">Output claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-171">Output claims:</span></span>
    - <span data-ttu-id="55c87-172">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" }, { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" } ]</span><span class="sxs-lookup"><span data-stu-id="55c87-172">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" }, { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" } ]</span></span>

## <a name="getidentityprovidersfromalternativesecurityidcollectiontransformation"></a><span data-ttu-id="55c87-173">GetIdentityProvidersFromAlternativeSecurityIdCollectionTransformation</span><span class="sxs-lookup"><span data-stu-id="55c87-173">GetIdentityProvidersFromAlternativeSecurityIdCollectionTransformation</span></span>

<span data-ttu-id="55c87-174">Returns list of issuers from the **alternativeSecurityIdCollection** claim into a new **stringCollection** claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-174">Returns list of issuers from the **alternativeSecurityIdCollection** claim into a new **stringCollection** claim.</span></span>

| <span data-ttu-id="55c87-175">Item</span><span class="sxs-lookup"><span data-stu-id="55c87-175">Item</span></span> | <span data-ttu-id="55c87-176">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="55c87-176">TransformationClaimType</span></span> | <span data-ttu-id="55c87-177">Data Type</span><span class="sxs-lookup"><span data-stu-id="55c87-177">Data Type</span></span> | <span data-ttu-id="55c87-178">Notes</span><span class="sxs-lookup"><span data-stu-id="55c87-178">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="55c87-179">InputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-179">InputClaim</span></span> | <span data-ttu-id="55c87-180">alternativeSecurityIdCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-180">alternativeSecurityIdCollection</span></span> | <span data-ttu-id="55c87-181">alternativeSecurityIdCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-181">alternativeSecurityIdCollection</span></span> | <span data-ttu-id="55c87-182">The ClaimType to be used to get the list of identity providers (issuer).</span><span class="sxs-lookup"><span data-stu-id="55c87-182">The ClaimType to be used to get the list of identity providers (issuer).</span></span> |
| <span data-ttu-id="55c87-183">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-183">OutputClaim</span></span> | <span data-ttu-id="55c87-184">identityProvidersCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-184">identityProvidersCollection</span></span> | <span data-ttu-id="55c87-185">stringCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-185">stringCollection</span></span> | <span data-ttu-id="55c87-186">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="55c87-186">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span></span> <span data-ttu-id="55c87-187">List of identity providers associate with the alternativeSecurityIdCollection input claim</span><span class="sxs-lookup"><span data-stu-id="55c87-187">List of identity providers associate with the alternativeSecurityIdCollection input claim</span></span> |

<span data-ttu-id="55c87-188">The following claims transformation reads the user **alternativeSecurityIds** claim and extracts the list of identity provider names associated with that account.</span><span class="sxs-lookup"><span data-stu-id="55c87-188">The following claims transformation reads the user **alternativeSecurityIds** claim and extracts the list of identity provider names associated with that account.</span></span> <span data-ttu-id="55c87-189">Use output **identityProvidersCollection** to show the user the list of identity providers associated with the account.</span><span class="sxs-lookup"><span data-stu-id="55c87-189">Use output **identityProvidersCollection** to show the user the list of identity providers associated with the account.</span></span> <span data-ttu-id="55c87-190">Or, on the identity provider selection page, filter the list of identity providers based on output **identityProvidersCollection** claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-190">Or, on the identity provider selection page, filter the list of identity providers based on output **identityProvidersCollection** claim.</span></span> <span data-ttu-id="55c87-191">So, user can select to link new social identity that is not already associated with the account.</span><span class="sxs-lookup"><span data-stu-id="55c87-191">So, user can select to link new social identity that is not already associated with the account.</span></span> 

```XML
<ClaimsTransformation Id="ExtractIdentityProviders" TransformationMethod="GetIdentityProvidersFromAlternativeSecurityIdCollectionTransformation">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="alternativeSecurityIds" TransformationClaimType="alternativeSecurityIdCollection" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="identityProviders" TransformationClaimType="identityProvidersCollection" />
  </OutputClaims>
</ClaimsTransformation>
```

- <span data-ttu-id="55c87-192">Input claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-192">Input claims:</span></span>
    - <span data-ttu-id="55c87-193">**alternativeSecurityIdCollection**: [ { "issuer": "google.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" }, { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" } ]</span><span class="sxs-lookup"><span data-stu-id="55c87-193">**alternativeSecurityIdCollection**: [ { "issuer": "google.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" }, { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" } ]</span></span>
- <span data-ttu-id="55c87-194">Output claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-194">Output claims:</span></span>
    - <span data-ttu-id="55c87-195">**identityProvidersCollection**: [ "facebook.com", "google.com" ]</span><span class="sxs-lookup"><span data-stu-id="55c87-195">**identityProvidersCollection**: [ "facebook.com", "google.com" ]</span></span>

## <a name="removealternativesecurityidbyidentityprovider"></a><span data-ttu-id="55c87-196">RemoveAlternativeSecurityIdByIdentityProvider</span><span class="sxs-lookup"><span data-stu-id="55c87-196">RemoveAlternativeSecurityIdByIdentityProvider</span></span>

<span data-ttu-id="55c87-197">Removes an **AlternativeSecurityId** from an **alternativeSecurityIdCollection** claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-197">Removes an **AlternativeSecurityId** from an **alternativeSecurityIdCollection** claim.</span></span> 

| <span data-ttu-id="55c87-198">Item</span><span class="sxs-lookup"><span data-stu-id="55c87-198">Item</span></span> | <span data-ttu-id="55c87-199">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="55c87-199">TransformationClaimType</span></span> | <span data-ttu-id="55c87-200">Data Type</span><span class="sxs-lookup"><span data-stu-id="55c87-200">Data Type</span></span> | <span data-ttu-id="55c87-201">Notes</span><span class="sxs-lookup"><span data-stu-id="55c87-201">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="55c87-202">InputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-202">InputClaim</span></span> | <span data-ttu-id="55c87-203">identityProvider</span><span class="sxs-lookup"><span data-stu-id="55c87-203">identityProvider</span></span> | <span data-ttu-id="55c87-204">string</span><span class="sxs-lookup"><span data-stu-id="55c87-204">string</span></span> | <span data-ttu-id="55c87-205">The ClaimType that contains the identity provider name to be removed from the collection.</span><span class="sxs-lookup"><span data-stu-id="55c87-205">The ClaimType that contains the identity provider name to be removed from the collection.</span></span> |
| <span data-ttu-id="55c87-206">InputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-206">InputClaim</span></span> | <span data-ttu-id="55c87-207">collection</span><span class="sxs-lookup"><span data-stu-id="55c87-207">collection</span></span> | <span data-ttu-id="55c87-208">alternativeSecurityIdCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-208">alternativeSecurityIdCollection</span></span> | <span data-ttu-id="55c87-209">The ClaimTypes that are used by the claims transformation.</span><span class="sxs-lookup"><span data-stu-id="55c87-209">The ClaimTypes that are used by the claims transformation.</span></span> <span data-ttu-id="55c87-210">The claims transformation removes the identityProvider from the collection.</span><span class="sxs-lookup"><span data-stu-id="55c87-210">The claims transformation removes the identityProvider from the collection.</span></span> |
| <span data-ttu-id="55c87-211">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="55c87-211">OutputClaim</span></span> | <span data-ttu-id="55c87-212">collection</span><span class="sxs-lookup"><span data-stu-id="55c87-212">collection</span></span> | <span data-ttu-id="55c87-213">alternativeSecurityIdCollection</span><span class="sxs-lookup"><span data-stu-id="55c87-213">alternativeSecurityIdCollection</span></span> | <span data-ttu-id="55c87-214">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="55c87-214">The ClaimTypes that are produced after this ClaimsTransformation has been invoked.</span></span> <span data-ttu-id="55c87-215">The new collection, after the identityProvider removed from the collection.</span><span class="sxs-lookup"><span data-stu-id="55c87-215">The new collection, after the identityProvider removed from the collection.</span></span> |

<span data-ttu-id="55c87-216">The following example unlinks one of the social identity with an existing account.</span><span class="sxs-lookup"><span data-stu-id="55c87-216">The following example unlinks one of the social identity with an existing account.</span></span> <span data-ttu-id="55c87-217">To unlink a social identity:</span><span class="sxs-lookup"><span data-stu-id="55c87-217">To unlink a social identity:</span></span> 
1. <span data-ttu-id="55c87-218">In the **AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserReadUsingObjectId** technical profiles, output the user's **alternativeSecurityIds** claim.</span><span class="sxs-lookup"><span data-stu-id="55c87-218">In the **AAD-UserReadUsingAlternativeSecurityId** and **AAD-UserReadUsingObjectId** technical profiles, output the user's **alternativeSecurityIds** claim.</span></span>
2. <span data-ttu-id="55c87-219">Ask the user to select which social account to remove from the list identity providers that are associated with this user.</span><span class="sxs-lookup"><span data-stu-id="55c87-219">Ask the user to select which social account to remove from the list identity providers that are associated with this user.</span></span> 
3. <span data-ttu-id="55c87-220">Call a claims transformation technical profile that calls the **RemoveAlternativeSecurityIdByIdentityProvider** claims transformation, that removed the selected social identity, using identity provider name.</span><span class="sxs-lookup"><span data-stu-id="55c87-220">Call a claims transformation technical profile that calls the **RemoveAlternativeSecurityIdByIdentityProvider** claims transformation, that removed the selected social identity, using identity provider name.</span></span>
4. <span data-ttu-id="55c87-221">Persist the **alternativeSecurityIds** claim to the user account.</span><span class="sxs-lookup"><span data-stu-id="55c87-221">Persist the **alternativeSecurityIds** claim to the user account.</span></span>

```XML
<ClaimsTransformation Id="RemoveAlternativeSecurityIdByIdentityProvider" TransformationMethod="RemoveAlternativeSecurityIdByIdentityProvider">
    <InputClaims>
        <InputClaim ClaimTypeReferenceId="secondIdentityProvider" TransformationClaimType="identityProvider" />
        <InputClaim ClaimTypeReferenceId="AlternativeSecurityIds" TransformationClaimType="collection" />
    </InputClaims>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="AlternativeSecurityIds" TransformationClaimType="collection" />
    </OutputClaims>
</ClaimsTransformation>               
</ClaimsTransformations>
```

### <a name="example"></a><span data-ttu-id="55c87-222">Example</span><span class="sxs-lookup"><span data-stu-id="55c87-222">Example</span></span>

- <span data-ttu-id="55c87-223">Input claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-223">Input claims:</span></span>
    - <span data-ttu-id="55c87-224">**identityProvider**: facebook.com</span><span class="sxs-lookup"><span data-stu-id="55c87-224">**identityProvider**: facebook.com</span></span>
    - <span data-ttu-id="55c87-225">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" }, { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" } ]</span><span class="sxs-lookup"><span data-stu-id="55c87-225">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" }, { "issuer": "facebook.com", "issuerUserId": "MTIzNDU=" } ]</span></span>
- <span data-ttu-id="55c87-226">Output claims:</span><span class="sxs-lookup"><span data-stu-id="55c87-226">Output claims:</span></span>
    - <span data-ttu-id="55c87-227">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" } ]</span><span class="sxs-lookup"><span data-stu-id="55c87-227">**collection**: [ { "issuer": "live.com", "issuerUserId": "MTA4MTQ2MDgyOTI3MDUyNTYzMjcw" } ]</span></span>