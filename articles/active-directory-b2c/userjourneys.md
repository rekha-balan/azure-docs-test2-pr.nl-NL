---
title: UserJourneys | Microsoft Docs
description: Specify the UserJourneys element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: c49ebcf31df950920574af05a9411e463b908bad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856262"
---
# <a name="userjourneys"></a><span data-ttu-id="af818-103">UserJourneys</span><span class="sxs-lookup"><span data-stu-id="af818-103">UserJourneys</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="af818-104">User journeys specify explicit paths through which a policy allows a relying party application to obtain the desired claims for a user.</span><span class="sxs-lookup"><span data-stu-id="af818-104">User journeys specify explicit paths through which a policy allows a relying party application to obtain the desired claims for a user.</span></span> <span data-ttu-id="af818-105">The user is taken through these paths to retrieve the claims that are to be presented to the relying party.</span><span class="sxs-lookup"><span data-stu-id="af818-105">The user is taken through these paths to retrieve the claims that are to be presented to the relying party.</span></span> <span data-ttu-id="af818-106">In other words, user journeys define the business logic of what an end user goes through as the Azure AD B2C Identity Experience Framework processes the request.</span><span class="sxs-lookup"><span data-stu-id="af818-106">In other words, user journeys define the business logic of what an end user goes through as the Azure AD B2C Identity Experience Framework processes the request.</span></span>

<span data-ttu-id="af818-107">These user journeys can be considered as templates available to satisfy the core need of the various replying parties of the community of interest.</span><span class="sxs-lookup"><span data-stu-id="af818-107">These user journeys can be considered as templates available to satisfy the core need of the various replying parties of the community of interest.</span></span> <span data-ttu-id="af818-108">User journeys facilitate the definition the relying party part of a policy.</span><span class="sxs-lookup"><span data-stu-id="af818-108">User journeys facilitate the definition the relying party part of a policy.</span></span> <span data-ttu-id="af818-109">A policy can define multiple user journeys.</span><span class="sxs-lookup"><span data-stu-id="af818-109">A policy can define multiple user journeys.</span></span> <span data-ttu-id="af818-110">Each user journey is a sequence of orchestration steps.</span><span class="sxs-lookup"><span data-stu-id="af818-110">Each user journey is a sequence of orchestration steps.</span></span>

<span data-ttu-id="af818-111">To define the user journeys supported by the policy, a **UserJourneys** element is added under the top-level element of the policy file.</span><span class="sxs-lookup"><span data-stu-id="af818-111">To define the user journeys supported by the policy, a **UserJourneys** element is added under the top-level element of the policy file.</span></span> 

<span data-ttu-id="af818-112">The **UserJourneys** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="af818-112">The **UserJourneys** element contains the following element:</span></span>

| <span data-ttu-id="af818-113">Element</span><span class="sxs-lookup"><span data-stu-id="af818-113">Element</span></span> | <span data-ttu-id="af818-114">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-114">Occurrences</span></span> | <span data-ttu-id="af818-115">Description</span><span class="sxs-lookup"><span data-stu-id="af818-115">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="af818-116">UserJourney</span><span class="sxs-lookup"><span data-stu-id="af818-116">UserJourney</span></span> | <span data-ttu-id="af818-117">1:n</span><span class="sxs-lookup"><span data-stu-id="af818-117">1:n</span></span> | <span data-ttu-id="af818-118">A user journey that defines all of the constructs necessary for a complete user flow.</span><span class="sxs-lookup"><span data-stu-id="af818-118">A user journey that defines all of the constructs necessary for a complete user flow.</span></span> | 

<span data-ttu-id="af818-119">The **UserJourney** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="af818-119">The **UserJourney** element contains the following attribute:</span></span>

| <span data-ttu-id="af818-120">Attribute</span><span class="sxs-lookup"><span data-stu-id="af818-120">Attribute</span></span> | <span data-ttu-id="af818-121">Required</span><span class="sxs-lookup"><span data-stu-id="af818-121">Required</span></span> | <span data-ttu-id="af818-122">Description</span><span class="sxs-lookup"><span data-stu-id="af818-122">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="af818-123">Id</span><span class="sxs-lookup"><span data-stu-id="af818-123">Id</span></span> | <span data-ttu-id="af818-124">Yes</span><span class="sxs-lookup"><span data-stu-id="af818-124">Yes</span></span> | <span data-ttu-id="af818-125">An identifier of a user journey that can be used to reference it from other elements in the policy.</span><span class="sxs-lookup"><span data-stu-id="af818-125">An identifier of a user journey that can be used to reference it from other elements in the policy.</span></span> <span data-ttu-id="af818-126">The **DefaultUserJourney** element of the [relying party policy](relyingparty.md) points to this attribute.</span><span class="sxs-lookup"><span data-stu-id="af818-126">The **DefaultUserJourney** element of the [relying party policy](relyingparty.md) points to this attribute.</span></span> |

<span data-ttu-id="af818-127">The **UserJourney** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="af818-127">The **UserJourney** element contains the following elements:</span></span>

| <span data-ttu-id="af818-128">Element</span><span class="sxs-lookup"><span data-stu-id="af818-128">Element</span></span> | <span data-ttu-id="af818-129">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-129">Occurrences</span></span> | <span data-ttu-id="af818-130">Description</span><span class="sxs-lookup"><span data-stu-id="af818-130">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="af818-131">OrchestrationSteps</span><span class="sxs-lookup"><span data-stu-id="af818-131">OrchestrationSteps</span></span> | <span data-ttu-id="af818-132">1:n</span><span class="sxs-lookup"><span data-stu-id="af818-132">1:n</span></span> | <span data-ttu-id="af818-133">An orchestration sequence that must be followed through for a successful transaction.</span><span class="sxs-lookup"><span data-stu-id="af818-133">An orchestration sequence that must be followed through for a successful transaction.</span></span> <span data-ttu-id="af818-134">Every user journey consists of an ordered list of orchestration steps that are executed in sequence.</span><span class="sxs-lookup"><span data-stu-id="af818-134">Every user journey consists of an ordered list of orchestration steps that are executed in sequence.</span></span> <span data-ttu-id="af818-135">If any step fails, the transaction fails.</span><span class="sxs-lookup"><span data-stu-id="af818-135">If any step fails, the transaction fails.</span></span> |

## <a name="orchestrationsteps"></a><span data-ttu-id="af818-136">OrchestrationSteps</span><span class="sxs-lookup"><span data-stu-id="af818-136">OrchestrationSteps</span></span>

<span data-ttu-id="af818-137">A user journey is represented as an orchestration sequence that must be followed through for a successful transaction.</span><span class="sxs-lookup"><span data-stu-id="af818-137">A user journey is represented as an orchestration sequence that must be followed through for a successful transaction.</span></span> <span data-ttu-id="af818-138">If any step fails, the transaction fails.</span><span class="sxs-lookup"><span data-stu-id="af818-138">If any step fails, the transaction fails.</span></span> <span data-ttu-id="af818-139">These orchestration steps reference both the building blocks and the claims providers allowed in the policy file.</span><span class="sxs-lookup"><span data-stu-id="af818-139">These orchestration steps reference both the building blocks and the claims providers allowed in the policy file.</span></span> <span data-ttu-id="af818-140">Any orchestration step that is responsible to show or render a user experience also has a reference to the corresponding content definition identifier.</span><span class="sxs-lookup"><span data-stu-id="af818-140">Any orchestration step that is responsible to show or render a user experience also has a reference to the corresponding content definition identifier.</span></span>

<span data-ttu-id="af818-141">Orchestration steps can be conditionaly ecxetuted, based on preconditions defined in the orchestration step element.</span><span class="sxs-lookup"><span data-stu-id="af818-141">Orchestration steps can be conditionaly ecxetuted, based on preconditions defined in the orchestration step element.</span></span> <span data-ttu-id="af818-142">For examle you can check to perform an orchestration step only if a specific claims exists, or if a claim is equal or not to the specified value.</span><span class="sxs-lookup"><span data-stu-id="af818-142">For examle you can check to perform an orchestration step only if a specific claims exists, or if a claim is equal or not to the specified value.</span></span> 


<span data-ttu-id="af818-143">To specify the ordered list of orchestration steps, an **OrchestrationSteps** element is added as part of the policy.</span><span class="sxs-lookup"><span data-stu-id="af818-143">To specify the ordered list of orchestration steps, an **OrchestrationSteps** element is added as part of the policy.</span></span> <span data-ttu-id="af818-144">This element is required.</span><span class="sxs-lookup"><span data-stu-id="af818-144">This element is required.</span></span>

<span data-ttu-id="af818-145">The **OrchestrationSteps** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="af818-145">The **OrchestrationSteps** element contains the following element:</span></span>

| <span data-ttu-id="af818-146">Element</span><span class="sxs-lookup"><span data-stu-id="af818-146">Element</span></span> | <span data-ttu-id="af818-147">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-147">Occurrences</span></span> | <span data-ttu-id="af818-148">Description</span><span class="sxs-lookup"><span data-stu-id="af818-148">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="af818-149">OrchestrationStep</span><span class="sxs-lookup"><span data-stu-id="af818-149">OrchestrationStep</span></span> | <span data-ttu-id="af818-150">1:n</span><span class="sxs-lookup"><span data-stu-id="af818-150">1:n</span></span> | <span data-ttu-id="af818-151">An ordered orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-151">An ordered orchestration step.</span></span> | 

<span data-ttu-id="af818-152">The **OrchestrationStep** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="af818-152">The **OrchestrationStep** element contains the following attributes:</span></span>

| <span data-ttu-id="af818-153">Attribute</span><span class="sxs-lookup"><span data-stu-id="af818-153">Attribute</span></span> | <span data-ttu-id="af818-154">Required</span><span class="sxs-lookup"><span data-stu-id="af818-154">Required</span></span> | <span data-ttu-id="af818-155">Description</span><span class="sxs-lookup"><span data-stu-id="af818-155">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="af818-156">Order</span><span class="sxs-lookup"><span data-stu-id="af818-156">Order</span></span> | <span data-ttu-id="af818-157">Yes</span><span class="sxs-lookup"><span data-stu-id="af818-157">Yes</span></span> | <span data-ttu-id="af818-158">The order of the orchestration steps.</span><span class="sxs-lookup"><span data-stu-id="af818-158">The order of the orchestration steps.</span></span> | 
| <span data-ttu-id="af818-159">Type</span><span class="sxs-lookup"><span data-stu-id="af818-159">Type</span></span> | <span data-ttu-id="af818-160">Yes</span><span class="sxs-lookup"><span data-stu-id="af818-160">Yes</span></span> | <span data-ttu-id="af818-161">The type of the orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-161">The type of the orchestration step.</span></span> <span data-ttu-id="af818-162">Possible values:</span><span class="sxs-lookup"><span data-stu-id="af818-162">Possible values:</span></span> <ul><li><span data-ttu-id="af818-163">**ClaimsProviderSelection** - Indicates that the orchestration step presents various claims providers to the user to select one.</span><span class="sxs-lookup"><span data-stu-id="af818-163">**ClaimsProviderSelection** - Indicates that the orchestration step presents various claims providers to the user to select one.</span></span></li><li><span data-ttu-id="af818-164">**CombinedSignInAndSignUp** - Indicates that the orchestration step presents a combined social provider sign-in and local account sign-up page.</span><span class="sxs-lookup"><span data-stu-id="af818-164">**CombinedSignInAndSignUp** - Indicates that the orchestration step presents a combined social provider sign-in and local account sign-up page.</span></span></li><li><span data-ttu-id="af818-165">**ClaimsExchange** - Indicates that the orchestration step exchanges claims with a claims provider.</span><span class="sxs-lookup"><span data-stu-id="af818-165">**ClaimsExchange** - Indicates that the orchestration step exchanges claims with a claims provider.</span></span></li><li><span data-ttu-id="af818-166">**SendClaims** - Indicates that the orchestration step sends the claims to the relying party with a token issued by a claims issuer.</span><span class="sxs-lookup"><span data-stu-id="af818-166">**SendClaims** - Indicates that the orchestration step sends the claims to the relying party with a token issued by a claims issuer.</span></span></li></ul> | 
| <span data-ttu-id="af818-167">ContentDefinitionReferenceId</span><span class="sxs-lookup"><span data-stu-id="af818-167">ContentDefinitionReferenceId</span></span> | <span data-ttu-id="af818-168">No</span><span class="sxs-lookup"><span data-stu-id="af818-168">No</span></span> | <span data-ttu-id="af818-169">The identifier of the [content definition](contentdefinitions.md) associated with this orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-169">The identifier of the [content definition](contentdefinitions.md) associated with this orchestration step.</span></span> <span data-ttu-id="af818-170">Usually the content definition reference identifier is defined in the self-asserted technical profile.</span><span class="sxs-lookup"><span data-stu-id="af818-170">Usually the content definition reference identifier is defined in the self-asserted technical profile.</span></span> <span data-ttu-id="af818-171">But, there are some cases when Azure AD B2C needs to display something without a technical profile.</span><span class="sxs-lookup"><span data-stu-id="af818-171">But, there are some cases when Azure AD B2C needs to display something without a technical profile.</span></span> <span data-ttu-id="af818-172">There are two examples, if the type of the orchestration step is one of follwing: `ClaimsProviderSelection` or  `CombinedSignInAndSignUp`.</span><span class="sxs-lookup"><span data-stu-id="af818-172">There are two examples, if the type of the orchestration step is one of follwing: `ClaimsProviderSelection` or  `CombinedSignInAndSignUp`.</span></span> <span data-ttu-id="af818-173">Azure AD B2C needs to display the identity provider selection without having a technical profile.</span><span class="sxs-lookup"><span data-stu-id="af818-173">Azure AD B2C needs to display the identity provider selection without having a technical profile.</span></span> | 
| <span data-ttu-id="af818-174">CpimIssuerTechnicalProfileReferenceId</span><span class="sxs-lookup"><span data-stu-id="af818-174">CpimIssuerTechnicalProfileReferenceId</span></span> | <span data-ttu-id="af818-175">No</span><span class="sxs-lookup"><span data-stu-id="af818-175">No</span></span> | <span data-ttu-id="af818-176">The type of the orchestration step is `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="af818-176">The type of the orchestration step is `SendClaims`.</span></span> <span data-ttu-id="af818-177">This property defines the technical profile identifier of the claims provider that issues the token for the relying party.</span><span class="sxs-lookup"><span data-stu-id="af818-177">This property defines the technical profile identifier of the claims provider that issues the token for the relying party.</span></span>  <span data-ttu-id="af818-178">If absent, no relying party token is created.</span><span class="sxs-lookup"><span data-stu-id="af818-178">If absent, no relying party token is created.</span></span> |


<span data-ttu-id="af818-179">The **OrchestrationStep** element can contain the following elements:</span><span class="sxs-lookup"><span data-stu-id="af818-179">The **OrchestrationStep** element can contain the following elements:</span></span>

| <span data-ttu-id="af818-180">Element</span><span class="sxs-lookup"><span data-stu-id="af818-180">Element</span></span> | <span data-ttu-id="af818-181">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-181">Occurrences</span></span> | <span data-ttu-id="af818-182">Description</span><span class="sxs-lookup"><span data-stu-id="af818-182">Description</span></span> |
| ------- | ----------- | ----------- | 
| <span data-ttu-id="af818-183">Preconditions</span><span class="sxs-lookup"><span data-stu-id="af818-183">Preconditions</span></span> | <span data-ttu-id="af818-184">0:n</span><span class="sxs-lookup"><span data-stu-id="af818-184">0:n</span></span> | <span data-ttu-id="af818-185">A list of preconditions that must be satisfied for the orchestration step to execute.</span><span class="sxs-lookup"><span data-stu-id="af818-185">A list of preconditions that must be satisfied for the orchestration step to execute.</span></span> | 
| <span data-ttu-id="af818-186">ClaimsProviderSelections</span><span class="sxs-lookup"><span data-stu-id="af818-186">ClaimsProviderSelections</span></span> | <span data-ttu-id="af818-187">0:n</span><span class="sxs-lookup"><span data-stu-id="af818-187">0:n</span></span> | <span data-ttu-id="af818-188">A list of claims provider selections for the orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-188">A list of claims provider selections for the orchestration step.</span></span> | 
| <span data-ttu-id="af818-189">ClaimsExchanges</span><span class="sxs-lookup"><span data-stu-id="af818-189">ClaimsExchanges</span></span> | <span data-ttu-id="af818-190">0:n</span><span class="sxs-lookup"><span data-stu-id="af818-190">0:n</span></span> | <span data-ttu-id="af818-191">A list of claims exchanges for the orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-191">A list of claims exchanges for the orchestration step.</span></span> | 

#### <a name="preconditions"></a><span data-ttu-id="af818-192">Preconditions</span><span class="sxs-lookup"><span data-stu-id="af818-192">Preconditions</span></span>

<span data-ttu-id="af818-193">The **Preconditions** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="af818-193">The **Preconditions** element contains the following element:</span></span>

| <span data-ttu-id="af818-194">Element</span><span class="sxs-lookup"><span data-stu-id="af818-194">Element</span></span> | <span data-ttu-id="af818-195">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-195">Occurrences</span></span> | <span data-ttu-id="af818-196">Description</span><span class="sxs-lookup"><span data-stu-id="af818-196">Description</span></span> |
| ------- | ----------- | ----------- | 
| <span data-ttu-id="af818-197">Precondition</span><span class="sxs-lookup"><span data-stu-id="af818-197">Precondition</span></span> | <span data-ttu-id="af818-198">0:n</span><span class="sxs-lookup"><span data-stu-id="af818-198">0:n</span></span> | <span data-ttu-id="af818-199">Depending on the technical profile being used, either redirects the client according to the claims provider selection or makes a server call to exchange claims.</span><span class="sxs-lookup"><span data-stu-id="af818-199">Depending on the technical profile being used, either redirects the client according to the claims provider selection or makes a server call to exchange claims.</span></span> | 


##### <a name="precondition"></a><span data-ttu-id="af818-200">Precondition</span><span class="sxs-lookup"><span data-stu-id="af818-200">Precondition</span></span>

<span data-ttu-id="af818-201">The **Precondition** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="af818-201">The **Precondition** element contains the following attribute:</span></span>

| <span data-ttu-id="af818-202">Attribute</span><span class="sxs-lookup"><span data-stu-id="af818-202">Attribute</span></span> | <span data-ttu-id="af818-203">Required</span><span class="sxs-lookup"><span data-stu-id="af818-203">Required</span></span> | <span data-ttu-id="af818-204">Description</span><span class="sxs-lookup"><span data-stu-id="af818-204">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="af818-205">Type</span><span class="sxs-lookup"><span data-stu-id="af818-205">Type</span></span> | <span data-ttu-id="af818-206">Yes</span><span class="sxs-lookup"><span data-stu-id="af818-206">Yes</span></span> | <span data-ttu-id="af818-207">The type of check or query to perform for this precondition.</span><span class="sxs-lookup"><span data-stu-id="af818-207">The type of check or query to perform for this precondition.</span></span> <span data-ttu-id="af818-208">The value can be **ClaimsExist**, which specifies that the actions should be performed if the specified claims exist in the user's current claim set, or **ClaimEquals**, which specifies that the actions should be performed if the specified claim exists and its value is equal to the specified value.</span><span class="sxs-lookup"><span data-stu-id="af818-208">The value can be **ClaimsExist**, which specifies that the actions should be performed if the specified claims exist in the user's current claim set, or **ClaimEquals**, which specifies that the actions should be performed if the specified claim exists and its value is equal to the specified value.</span></span> |
| <span data-ttu-id="af818-209">ExecuteActionsIf</span><span class="sxs-lookup"><span data-stu-id="af818-209">ExecuteActionsIf</span></span> | <span data-ttu-id="af818-210">Yes</span><span class="sxs-lookup"><span data-stu-id="af818-210">Yes</span></span> | <span data-ttu-id="af818-211">Use a true or false test to decide if the actions in the precondition should be performed.</span><span class="sxs-lookup"><span data-stu-id="af818-211">Use a true or false test to decide if the actions in the precondition should be performed.</span></span> | 

<span data-ttu-id="af818-212">The **Precondition** elements contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="af818-212">The **Precondition** elements contains the following elements:</span></span>

| <span data-ttu-id="af818-213">Element</span><span class="sxs-lookup"><span data-stu-id="af818-213">Element</span></span> | <span data-ttu-id="af818-214">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-214">Occurrences</span></span> | <span data-ttu-id="af818-215">Description</span><span class="sxs-lookup"><span data-stu-id="af818-215">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="af818-216">Value</span><span class="sxs-lookup"><span data-stu-id="af818-216">Value</span></span> | <span data-ttu-id="af818-217">1:n</span><span class="sxs-lookup"><span data-stu-id="af818-217">1:n</span></span> | <span data-ttu-id="af818-218">A ClaimTypeReferenceId to be queried for.</span><span class="sxs-lookup"><span data-stu-id="af818-218">A ClaimTypeReferenceId to be queried for.</span></span> <span data-ttu-id="af818-219">Another value element contains the value to be checked.</span><span class="sxs-lookup"><span data-stu-id="af818-219">Another value element contains the value to be checked.</span></span></li></ul>|
| <span data-ttu-id="af818-220">Action</span><span class="sxs-lookup"><span data-stu-id="af818-220">Action</span></span> | <span data-ttu-id="af818-221">1:1</span><span class="sxs-lookup"><span data-stu-id="af818-221">1:1</span></span> | <span data-ttu-id="af818-222">The action that should be performed if the precondition check within an orchestration step is true.</span><span class="sxs-lookup"><span data-stu-id="af818-222">The action that should be performed if the precondition check within an orchestration step is true.</span></span> <span data-ttu-id="af818-223">If the value of the `Action` is set to `SkipThisOrchestrationStep`, the associated `OrchestrationStep` should not be executed.</span><span class="sxs-lookup"><span data-stu-id="af818-223">If the value of the `Action` is set to `SkipThisOrchestrationStep`, the associated `OrchestrationStep` should not be executed.</span></span> | 

### <a name="preconditions-examples"></a><span data-ttu-id="af818-224">Preconditions examples</span><span class="sxs-lookup"><span data-stu-id="af818-224">Preconditions examples</span></span>

<span data-ttu-id="af818-225">The following preconditions checks whether the user's objectId exists.</span><span class="sxs-lookup"><span data-stu-id="af818-225">The following preconditions checks whether the user's objectId exists.</span></span> <span data-ttu-id="af818-226">In the user journey, the user has selected to sign in using local account.</span><span class="sxs-lookup"><span data-stu-id="af818-226">In the user journey, the user has selected to sign in using local account.</span></span> <span data-ttu-id="af818-227">If the objectId exists, skip this orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-227">If the objectId exists, skip this orchestration step.</span></span>

```XML
<OrchestrationStep Order="2" Type="ClaimsExchange">
  <Preconditions>
    <Precondition Type="ClaimsExist" ExecuteActionsIf="true">
      <Value>objectId</Value>
      <Action>SkipThisOrchestrationStep</Action>
    </Precondition>
  </Preconditions>
  <ClaimsExchanges>
    <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
    <ClaimsExchange Id="SignUpWithLogonEmailExchange" TechnicalProfileReferenceId="LocalAccountSignUpWithLogonEmail" />
  </ClaimsExchanges>
</OrchestrationStep>
```

<span data-ttu-id="af818-228">The following preconditions checks whether the user signed in with a social account.</span><span class="sxs-lookup"><span data-stu-id="af818-228">The following preconditions checks whether the user signed in with a social account.</span></span> <span data-ttu-id="af818-229">An attempt is made to find the user account in the directory.</span><span class="sxs-lookup"><span data-stu-id="af818-229">An attempt is made to find the user account in the directory.</span></span> <span data-ttu-id="af818-230">If the user signs in or signs up with a local account skip, this orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-230">If the user signs in or signs up with a local account skip, this orchestration step.</span></span>

```XML
<OrchestrationStep Order="3" Type="ClaimsExchange">
  <Preconditions>
    <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
      <Value>authenticationSource</Value>
      <Value>localAccountAuthentication</Value>
      <Action>SkipThisOrchestrationStep</Action>
    </Precondition>
  </Preconditions>
  <ClaimsExchanges>
    <ClaimsExchange Id="AADUserReadUsingAlternativeSecurityId" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId-NoError" />
  </ClaimsExchanges>
</OrchestrationStep>
```

<span data-ttu-id="af818-231">Preconditions can check multiple preconditions.</span><span class="sxs-lookup"><span data-stu-id="af818-231">Preconditions can check multiple preconditions.</span></span> <span data-ttu-id="af818-232">The following example checks whether 'objectId' or 'email' exists.</span><span class="sxs-lookup"><span data-stu-id="af818-232">The following example checks whether 'objectId' or 'email' exists.</span></span> <span data-ttu-id="af818-233">If the first condition is true, The journey skips to the next orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-233">If the first condition is true, The journey skips to the next orchestration step.</span></span>

```XML
<OrchestrationStep Order="4" Type="ClaimsExchange">
  <Preconditions>
  <Precondition Type="ClaimsExist" ExecuteActionsIf="true">
      <Value>objectId</Value>
      <Action>SkipThisOrchestrationStep</Action>
    </Precondition>
    <Precondition Type="ClaimsExist" ExecuteActionsIf="true">
      <Value>email</Value>
      <Action>SkipThisOrchestrationStep</Action>
    </Precondition>
  </Preconditions>      
  <ClaimsExchanges>
    <ClaimsExchange Id="SelfAsserted-SocialEmail" TechnicalProfileReferenceId="SelfAsserted-SocialEmail" />
  </ClaimsExchanges>
</OrchestrationStep>
```

## <a name="claimsproviderselection"></a><span data-ttu-id="af818-234">ClaimsProviderSelection</span><span class="sxs-lookup"><span data-stu-id="af818-234">ClaimsProviderSelection</span></span>

<span data-ttu-id="af818-235">An orchestration step of type `ClaimsProviderSelection` or `CombinedSignInAndSignUp` may contain a list of claims providers that a user can sign in with.</span><span class="sxs-lookup"><span data-stu-id="af818-235">An orchestration step of type `ClaimsProviderSelection` or `CombinedSignInAndSignUp` may contain a list of claims providers that a user can sign in with.</span></span> <span data-ttu-id="af818-236">The order of the elements inside the `ClaimsProviderSelections` elements controls the order of the identity providers presented to the user.</span><span class="sxs-lookup"><span data-stu-id="af818-236">The order of the elements inside the `ClaimsProviderSelections` elements controls the order of the identity providers presented to the user.</span></span>

<span data-ttu-id="af818-237">The **ClaimsProviderSelection** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="af818-237">The **ClaimsProviderSelection** element contains the following element:</span></span>

| <span data-ttu-id="af818-238">Element</span><span class="sxs-lookup"><span data-stu-id="af818-238">Element</span></span> | <span data-ttu-id="af818-239">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-239">Occurrences</span></span> | <span data-ttu-id="af818-240">Description</span><span class="sxs-lookup"><span data-stu-id="af818-240">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="af818-241">ClaimsProviderSelection</span><span class="sxs-lookup"><span data-stu-id="af818-241">ClaimsProviderSelection</span></span> | <span data-ttu-id="af818-242">0:n</span><span class="sxs-lookup"><span data-stu-id="af818-242">0:n</span></span> | <span data-ttu-id="af818-243">Provides the list of claims providers that can be selected.</span><span class="sxs-lookup"><span data-stu-id="af818-243">Provides the list of claims providers that can be selected.</span></span>|

<span data-ttu-id="af818-244">The **ClaimsProviderSelection** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="af818-244">The **ClaimsProviderSelection** element contains the following attributes:</span></span> 

| <span data-ttu-id="af818-245">Attribute</span><span class="sxs-lookup"><span data-stu-id="af818-245">Attribute</span></span> | <span data-ttu-id="af818-246">Required</span><span class="sxs-lookup"><span data-stu-id="af818-246">Required</span></span> | <span data-ttu-id="af818-247">Description</span><span class="sxs-lookup"><span data-stu-id="af818-247">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="af818-248">TargetClaimsExchangeId</span><span class="sxs-lookup"><span data-stu-id="af818-248">TargetClaimsExchangeId</span></span> | <span data-ttu-id="af818-249">No</span><span class="sxs-lookup"><span data-stu-id="af818-249">No</span></span> | <span data-ttu-id="af818-250">The identifier of the claims exchange, which is executed in the next orchestration step of the claims provider selection.</span><span class="sxs-lookup"><span data-stu-id="af818-250">The identifier of the claims exchange, which is executed in the next orchestration step of the claims provider selection.</span></span> <span data-ttu-id="af818-251">This attribute of the ValidationClaimsExchangeId attribute must be specified.</span><span class="sxs-lookup"><span data-stu-id="af818-251">This attribute of the ValidationClaimsExchangeId attribute must be specified.</span></span> | 
| <span data-ttu-id="af818-252">ValidationClaimsExchangeId</span><span class="sxs-lookup"><span data-stu-id="af818-252">ValidationClaimsExchangeId</span></span> | <span data-ttu-id="af818-253">No</span><span class="sxs-lookup"><span data-stu-id="af818-253">No</span></span> | <span data-ttu-id="af818-254">The identifier of the claims exchange, which is executed in the current orchestration step to validate the claims provider selection.</span><span class="sxs-lookup"><span data-stu-id="af818-254">The identifier of the claims exchange, which is executed in the current orchestration step to validate the claims provider selection.</span></span> <span data-ttu-id="af818-255">This attribute of the TargetClaimsExchangeId attribute must be specified.</span><span class="sxs-lookup"><span data-stu-id="af818-255">This attribute of the TargetClaimsExchangeId attribute must be specified.</span></span> |

### <a name="claimsproviderselection-example"></a><span data-ttu-id="af818-256">ClaimsProviderSelection example</span><span class="sxs-lookup"><span data-stu-id="af818-256">ClaimsProviderSelection example</span></span>

<span data-ttu-id="af818-257">In the following orchestration step, the user can choose to sign in with, Facebook, LinkIn, Twitter, Google, or a local account.</span><span class="sxs-lookup"><span data-stu-id="af818-257">In the following orchestration step, the user can choose to sign in with, Facebook, LinkIn, Twitter, Google, or a local account.</span></span> <span data-ttu-id="af818-258">If the user selects one of the social identity providers, the second orchestration step executes with the selected claim exchange specified in the `TargetClaimsExchangeId` attribute.</span><span class="sxs-lookup"><span data-stu-id="af818-258">If the user selects one of the social identity providers, the second orchestration step executes with the selected claim exchange specified in the `TargetClaimsExchangeId` attribute.</span></span> <span data-ttu-id="af818-259">The second orchestration step redirects the user to the social identity provider to complete the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="af818-259">The second orchestration step redirects the user to the social identity provider to complete the sign-in process.</span></span> <span data-ttu-id="af818-260">If the user chooses to sign in with the local account, Azure AD B2C stays on the same orchestration step (the same sign-up page or sign-in page) and skips the second orchestration step.</span><span class="sxs-lookup"><span data-stu-id="af818-260">If the user chooses to sign in with the local account, Azure AD B2C stays on the same orchestration step (the same sign-up page or sign-in page) and skips the second orchestration step.</span></span>

```XML
<OrchestrationStep Order="1" Type="CombinedSignInAndSignUp" ContentDefinitionReferenceId="api.signuporsignin">
    <ClaimsProviderSelections>
    <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
    <ClaimsProviderSelection TargetClaimsExchangeId="LinkedInExchange" />
    <ClaimsProviderSelection TargetClaimsExchangeId="TwitterExchange" />
    <ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
    <ClaimsProviderSelection ValidationClaimsExchangeId="LocalAccountSigninEmailExchange" />
    </ClaimsProviderSelections>
    <ClaimsExchanges>
    <ClaimsExchange Id="LocalAccountSigninEmailExchange" 
                    TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
    </ClaimsExchanges>
</OrchestrationStep>


<OrchestrationStep Order="2" Type="ClaimsExchange">
  <Preconditions>
    <Precondition Type="ClaimsExist" ExecuteActionsIf="true">
      <Value>objectId</Value>
      <Action>SkipThisOrchestrationStep</Action>
    </Precondition>
  </Preconditions>
  <ClaimsExchanges>
    <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
    <ClaimsExchange Id="SignUpWithLogonEmailExchange" TechnicalProfileReferenceId="LocalAccountSignUpWithLogonEmail" />
    <ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
    <ClaimsExchange Id="LinkedInExchange" TechnicalProfileReferenceId="LinkedIn-OAUTH" />
    <ClaimsExchange Id="TwitterExchange" TechnicalProfileReferenceId="Twitter-OAUTH1" />
  </ClaimsExchanges>
</OrchestrationStep>
```

## <a name="claimsexchanges"></a><span data-ttu-id="af818-261">ClaimsExchanges</span><span class="sxs-lookup"><span data-stu-id="af818-261">ClaimsExchanges</span></span>

<span data-ttu-id="af818-262">The **ClaimsExchanges** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="af818-262">The **ClaimsExchanges** element contains the following element:</span></span>

| <span data-ttu-id="af818-263">Element</span><span class="sxs-lookup"><span data-stu-id="af818-263">Element</span></span> | <span data-ttu-id="af818-264">Occurrences</span><span class="sxs-lookup"><span data-stu-id="af818-264">Occurrences</span></span> | <span data-ttu-id="af818-265">Description</span><span class="sxs-lookup"><span data-stu-id="af818-265">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="af818-266">ClaimsExchange</span><span class="sxs-lookup"><span data-stu-id="af818-266">ClaimsExchange</span></span> | <span data-ttu-id="af818-267">0:n</span><span class="sxs-lookup"><span data-stu-id="af818-267">0:n</span></span> | <span data-ttu-id="af818-268">Depending on the technical profile being used, either redirects the client according to the ClaimsProviderSelection that was selected, or makes a server call to exchange claims.</span><span class="sxs-lookup"><span data-stu-id="af818-268">Depending on the technical profile being used, either redirects the client according to the ClaimsProviderSelection that was selected, or makes a server call to exchange claims.</span></span> | 

<span data-ttu-id="af818-269">The **ClaimsExchange** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="af818-269">The **ClaimsExchange** element contains the following attributes:</span></span>

| <span data-ttu-id="af818-270">Attribute</span><span class="sxs-lookup"><span data-stu-id="af818-270">Attribute</span></span> | <span data-ttu-id="af818-271">Required</span><span class="sxs-lookup"><span data-stu-id="af818-271">Required</span></span> | <span data-ttu-id="af818-272">Description</span><span class="sxs-lookup"><span data-stu-id="af818-272">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="af818-273">Id</span><span class="sxs-lookup"><span data-stu-id="af818-273">Id</span></span> | <span data-ttu-id="af818-274">Yes</span><span class="sxs-lookup"><span data-stu-id="af818-274">Yes</span></span> | <span data-ttu-id="af818-275">An identifier of the claims exchange step.</span><span class="sxs-lookup"><span data-stu-id="af818-275">An identifier of the claims exchange step.</span></span> <span data-ttu-id="af818-276">The identifier is used to reference the claims exchange from a claims provider selection step in the policy.</span><span class="sxs-lookup"><span data-stu-id="af818-276">The identifier is used to reference the claims exchange from a claims provider selection step in the policy.</span></span> | 
| <span data-ttu-id="af818-277">TechnicalProfileReferenceId</span><span class="sxs-lookup"><span data-stu-id="af818-277">TechnicalProfileReferenceId</span></span> | <span data-ttu-id="af818-278">Yes</span><span class="sxs-lookup"><span data-stu-id="af818-278">Yes</span></span> | <span data-ttu-id="af818-279">The identifier of the technical profile that is to be executed.</span><span class="sxs-lookup"><span data-stu-id="af818-279">The identifier of the technical profile that is to be executed.</span></span> |
 
















