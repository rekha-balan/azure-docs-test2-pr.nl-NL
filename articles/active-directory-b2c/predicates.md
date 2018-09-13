---
title: Predicates and PredicateValidations - Azure Active Directory B2C | Microsoft Docs
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
ms.openlocfilehash: 58ae0541b1b95f280cdd30327059d62ff26978ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869861"
---
# <a name="predicates-and-predicatevalidations"></a><span data-ttu-id="6e0b3-103">Predicates and PredicateValidations</span><span class="sxs-lookup"><span data-stu-id="6e0b3-103">Predicates and PredicateValidations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="6e0b3-104">The **Predicates** and **PredicateValidations** elements enable you to perform a validation process to ensure that only properly formed data is entered into your Azure Active Directory (Azure AD) B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-104">The **Predicates** and **PredicateValidations** elements enable you to perform a validation process to ensure that only properly formed data is entered into your Azure Active Directory (Azure AD) B2C tenant.</span></span>  

<span data-ttu-id="6e0b3-105">The following diagram shows the relationship between the elements:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-105">The following diagram shows the relationship between the elements:</span></span>  

![Predicates](./media/predicates/predicates.png)

## <a name="predicates"></a><span data-ttu-id="6e0b3-107">Predicates</span><span class="sxs-lookup"><span data-stu-id="6e0b3-107">Predicates</span></span>  

<span data-ttu-id="6e0b3-108">The **Predicate** element defines a basic validation to check the value of a claim type and returns `true` or `false`.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-108">The **Predicate** element defines a basic validation to check the value of a claim type and returns `true` or `false`.</span></span> <span data-ttu-id="6e0b3-109">The validation is done by using a specified **Method** element and a set of **Parameter** elements relevant to the method.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-109">The validation is done by using a specified **Method** element and a set of **Parameter** elements relevant to the method.</span></span> <span data-ttu-id="6e0b3-110">For example, a predicate can check whether the length of a string claim value is within the range of minimum and maximum parameters specified, or whether a string claim value contains a character set.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-110">For example, a predicate can check whether the length of a string claim value is within the range of minimum and maximum parameters specified, or whether a string claim value contains a character set.</span></span> <span data-ttu-id="6e0b3-111">The **UserHelpText** element provides an error message for users if the check fails.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-111">The **UserHelpText** element provides an error message for users if the check fails.</span></span> <span data-ttu-id="6e0b3-112">The value of **UserHelpText** element can be localized using [language customization](localization.md).</span><span class="sxs-lookup"><span data-stu-id="6e0b3-112">The value of **UserHelpText** element can be localized using [language customization](localization.md).</span></span>

<span data-ttu-id="6e0b3-113">The **Predicates** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-113">The **Predicates** element contains the following element:</span></span>

| <span data-ttu-id="6e0b3-114">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-114">Element</span></span> | <span data-ttu-id="6e0b3-115">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-115">Occurrences</span></span> | <span data-ttu-id="6e0b3-116">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-116">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-117">Predicate</span><span class="sxs-lookup"><span data-stu-id="6e0b3-117">Predicate</span></span> | <span data-ttu-id="6e0b3-118">1:n</span><span class="sxs-lookup"><span data-stu-id="6e0b3-118">1:n</span></span> | <span data-ttu-id="6e0b3-119">A list of predicates.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-119">A list of predicates.</span></span> | 

<span data-ttu-id="6e0b3-120">The **Predicate** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-120">The **Predicate** element contains the following attributes:</span></span>

| <span data-ttu-id="6e0b3-121">Attribute</span><span class="sxs-lookup"><span data-stu-id="6e0b3-121">Attribute</span></span> | <span data-ttu-id="6e0b3-122">Required</span><span class="sxs-lookup"><span data-stu-id="6e0b3-122">Required</span></span> | <span data-ttu-id="6e0b3-123">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-123">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="6e0b3-124">Id</span><span class="sxs-lookup"><span data-stu-id="6e0b3-124">Id</span></span> | <span data-ttu-id="6e0b3-125">Yes</span><span class="sxs-lookup"><span data-stu-id="6e0b3-125">Yes</span></span> | <span data-ttu-id="6e0b3-126">An identifier that's used for the predicate.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-126">An identifier that's used for the predicate.</span></span> <span data-ttu-id="6e0b3-127">Other elements can use this identifier in the policy.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-127">Other elements can use this identifier in the policy.</span></span> |
| <span data-ttu-id="6e0b3-128">Method</span><span class="sxs-lookup"><span data-stu-id="6e0b3-128">Method</span></span> | <span data-ttu-id="6e0b3-129">Yes</span><span class="sxs-lookup"><span data-stu-id="6e0b3-129">Yes</span></span> | <span data-ttu-id="6e0b3-130">The method type to use for validation.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-130">The method type to use for validation.</span></span> <span data-ttu-id="6e0b3-131">Possible values: **IsLengthRange**, **MatchesRegex**, **IncludesCharacters**, or **IsDateRange**.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-131">Possible values: **IsLengthRange**, **MatchesRegex**, **IncludesCharacters**, or **IsDateRange**.</span></span> <span data-ttu-id="6e0b3-132">The **IsLengthRange** value checks whether the length of a string claim value is within the range of minimum and maximum parameters specified.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-132">The **IsLengthRange** value checks whether the length of a string claim value is within the range of minimum and maximum parameters specified.</span></span> <span data-ttu-id="6e0b3-133">The **MatchesRegex** value checks whether a string claim value matches a regular expression.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-133">The **MatchesRegex** value checks whether a string claim value matches a regular expression.</span></span> <span data-ttu-id="6e0b3-134">The **IncludesCharacters** value checks whether a string claim value contains a character set.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-134">The **IncludesCharacters** value checks whether a string claim value contains a character set.</span></span> <span data-ttu-id="6e0b3-135">The **IsDateRange** value checks whether a date claim value is between a range of minimum and maximum parameters specified.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-135">The **IsDateRange** value checks whether a date claim value is between a range of minimum and maximum parameters specified.</span></span> |

<span data-ttu-id="6e0b3-136">The **Predicate** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-136">The **Predicate** element contains the following elements:</span></span>

| <span data-ttu-id="6e0b3-137">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-137">Element</span></span> | <span data-ttu-id="6e0b3-138">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-138">Occurrences</span></span> | <span data-ttu-id="6e0b3-139">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-139">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-140">UserHelpText</span><span class="sxs-lookup"><span data-stu-id="6e0b3-140">UserHelpText</span></span> | <span data-ttu-id="6e0b3-141">1:1</span><span class="sxs-lookup"><span data-stu-id="6e0b3-141">1:1</span></span> | <span data-ttu-id="6e0b3-142">An error message for users if the check fails.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-142">An error message for users if the check fails.</span></span> <span data-ttu-id="6e0b3-143">This string can be localized using the [language customization](localization.md)</span><span class="sxs-lookup"><span data-stu-id="6e0b3-143">This string can be localized using the [language customization](localization.md)</span></span> |
| <span data-ttu-id="6e0b3-144">Parameters</span><span class="sxs-lookup"><span data-stu-id="6e0b3-144">Parameters</span></span> | <span data-ttu-id="6e0b3-145">1:1</span><span class="sxs-lookup"><span data-stu-id="6e0b3-145">1:1</span></span> | <span data-ttu-id="6e0b3-146">The parameters for the method type of the string validation.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-146">The parameters for the method type of the string validation.</span></span> | 

<span data-ttu-id="6e0b3-147">The **Parameters** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-147">The **Parameters** element contains the following elements:</span></span>

| <span data-ttu-id="6e0b3-148">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-148">Element</span></span> | <span data-ttu-id="6e0b3-149">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-149">Occurrences</span></span> | <span data-ttu-id="6e0b3-150">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-150">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="6e0b3-151">Parameter</span></span> | <span data-ttu-id="6e0b3-152">1:n</span><span class="sxs-lookup"><span data-stu-id="6e0b3-152">1:n</span></span> | <span data-ttu-id="6e0b3-153">The parameters for the method type of the string validation.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-153">The parameters for the method type of the string validation.</span></span> | 

<span data-ttu-id="6e0b3-154">The **Parameter** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-154">The **Parameter** element contains the following attributes:</span></span>

| <span data-ttu-id="6e0b3-155">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-155">Element</span></span> | <span data-ttu-id="6e0b3-156">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-156">Occurrences</span></span> | <span data-ttu-id="6e0b3-157">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-157">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-158">Id</span><span class="sxs-lookup"><span data-stu-id="6e0b3-158">Id</span></span> | <span data-ttu-id="6e0b3-159">1:1</span><span class="sxs-lookup"><span data-stu-id="6e0b3-159">1:1</span></span> | <span data-ttu-id="6e0b3-160">The identifier of the parameter.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-160">The identifier of the parameter.</span></span> |

<span data-ttu-id="6e0b3-161">The following example shows a `IsLengthRange` method with the parameters `Minimum` and `Maximum` that specify the length range of the string:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-161">The following example shows a `IsLengthRange` method with the parameters `Minimum` and `Maximum` that specify the length range of the string:</span></span>

```XML
<Predicate Id="IsLengthBetween8And64" Method="IsLengthRange">
  <UserHelpText>The password must be between 8 and 64 characters.</UserHelpText>
    <Parameters>
      <Parameter Id="Minimum">8</Parameter>
      <Parameter Id="Maximum">64</Parameter>
  </Parameters>
</Predicate>
```

<span data-ttu-id="6e0b3-162">The following example shows a `MatchesRegex` method with the parameter `RegularExpression` that specifies a regular expression:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-162">The following example shows a `MatchesRegex` method with the parameter `RegularExpression` that specifies a regular expression:</span></span>

```XML
<Predicate Id="PIN" Method="MatchesRegex">
  <UserHelpText>The password must be numbers only.</UserHelpText>
  <Parameters>
    <Parameter Id="RegularExpression">^[0-9]+$</Parameter>
  </Parameters>
</Predicate>
```

<span data-ttu-id="6e0b3-163">The following example shows a `IncludesCharacters` method with the parameter `CharacterSet` that specifies the set of characters:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-163">The following example shows a `IncludesCharacters` method with the parameter `CharacterSet` that specifies the set of characters:</span></span>

```XML
<Predicate Id="Lowercase" Method="IncludesCharacters">
  <UserHelpText>a lowercase letter</UserHelpText>
  <Parameters>
    <Parameter Id="CharacterSet">a-z</Parameter>
  </Parameters>
</Predicate>
```

<span data-ttu-id="6e0b3-164">The following example shows a `IsDateRange` method with the parameters `Minimum` and `Maximum` that specify the date range with a format of `yyyy-MM-dd` and `Today`.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-164">The following example shows a `IsDateRange` method with the parameters `Minimum` and `Maximum` that specify the date range with a format of `yyyy-MM-dd` and `Today`.</span></span>

```XML
<Predicate Id="DateRange" Method="IsDateRange" HelpText="The date must be between 1970-01-01 and today.">
  <Parameters>
    <Parameter Id="Minimum">1970-01-01</Parameter>
    <Parameter Id="Maximum">Today</Parameter>
  </Parameters>
</Predicate>
```

## <a name="predicatevalidations"></a><span data-ttu-id="6e0b3-165">PredicateValidations</span><span class="sxs-lookup"><span data-stu-id="6e0b3-165">PredicateValidations</span></span> 

<span data-ttu-id="6e0b3-166">While the predicates define the validation to check against a claim type, the **PredicateValidations** group a set of predicates to form a user input validation that can be applied to a claim type.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-166">While the predicates define the validation to check against a claim type, the **PredicateValidations** group a set of predicates to form a user input validation that can be applied to a claim type.</span></span> <span data-ttu-id="6e0b3-167">Each **PredicateValidation** element contains a set of **PredicateGroup** elements that contain a set of **PredicateReference** elements that points to a **Predicate**.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-167">Each **PredicateValidation** element contains a set of **PredicateGroup** elements that contain a set of **PredicateReference** elements that points to a **Predicate**.</span></span> <span data-ttu-id="6e0b3-168">To pass the validation, the value of the claim should pass all of the tests of any predicate under all of the **PredicateGroup** with their set of **PredicateReference** elements.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-168">To pass the validation, the value of the claim should pass all of the tests of any predicate under all of the **PredicateGroup** with their set of **PredicateReference** elements.</span></span>

```XML
<PredicateValidations>
  <PredicateValidation Id="">
    <PredicateGroups>
      <PredicateGroup Id="">
        <UserHelpText></UserHelpText>
        <PredicateReferences MatchAtLeast="">
          <PredicateReference Id="" />
          ...
        </PredicateReferences>
      </PredicateGroup>
      ...
    </PredicateGroups>
  </PredicateValidation>
...
</PredicateValidations>
```

<span data-ttu-id="6e0b3-169">The **PredicateValidations** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-169">The **PredicateValidations** element contains the following element:</span></span>

| <span data-ttu-id="6e0b3-170">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-170">Element</span></span> | <span data-ttu-id="6e0b3-171">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-171">Occurrences</span></span> | <span data-ttu-id="6e0b3-172">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-172">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-173">PredicateValidation</span><span class="sxs-lookup"><span data-stu-id="6e0b3-173">PredicateValidation</span></span> | <span data-ttu-id="6e0b3-174">1:n</span><span class="sxs-lookup"><span data-stu-id="6e0b3-174">1:n</span></span> | <span data-ttu-id="6e0b3-175">A list of predicate validation.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-175">A list of predicate validation.</span></span> | 

<span data-ttu-id="6e0b3-176">The **PredicateValidation** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-176">The **PredicateValidation** element contains the following attribute:</span></span>

| <span data-ttu-id="6e0b3-177">Attribute</span><span class="sxs-lookup"><span data-stu-id="6e0b3-177">Attribute</span></span> | <span data-ttu-id="6e0b3-178">Required</span><span class="sxs-lookup"><span data-stu-id="6e0b3-178">Required</span></span> | <span data-ttu-id="6e0b3-179">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-179">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="6e0b3-180">Id</span><span class="sxs-lookup"><span data-stu-id="6e0b3-180">Id</span></span> | <span data-ttu-id="6e0b3-181">Yes</span><span class="sxs-lookup"><span data-stu-id="6e0b3-181">Yes</span></span> | <span data-ttu-id="6e0b3-182">An identifier that's used for the predicate validation.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-182">An identifier that's used for the predicate validation.</span></span> <span data-ttu-id="6e0b3-183">The **ClaimType** element can use this identifier in the policy.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-183">The **ClaimType** element can use this identifier in the policy.</span></span> |

<span data-ttu-id="6e0b3-184">The **PredicateValidation** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-184">The **PredicateValidation** element contains the following element:</span></span>

| <span data-ttu-id="6e0b3-185">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-185">Element</span></span> | <span data-ttu-id="6e0b3-186">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-186">Occurrences</span></span> | <span data-ttu-id="6e0b3-187">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-187">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-188">PredicateGroups</span><span class="sxs-lookup"><span data-stu-id="6e0b3-188">PredicateGroups</span></span> | <span data-ttu-id="6e0b3-189">1:n</span><span class="sxs-lookup"><span data-stu-id="6e0b3-189">1:n</span></span> | <span data-ttu-id="6e0b3-190">A list of predicate groups.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-190">A list of predicate groups.</span></span> | 

<span data-ttu-id="6e0b3-191">The **PredicateGroups** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-191">The **PredicateGroups** element contains the following element:</span></span>

| <span data-ttu-id="6e0b3-192">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-192">Element</span></span> | <span data-ttu-id="6e0b3-193">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-193">Occurrences</span></span> | <span data-ttu-id="6e0b3-194">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-194">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-195">PredicateGroup</span><span class="sxs-lookup"><span data-stu-id="6e0b3-195">PredicateGroup</span></span> | <span data-ttu-id="6e0b3-196">1:n</span><span class="sxs-lookup"><span data-stu-id="6e0b3-196">1:n</span></span> | <span data-ttu-id="6e0b3-197">A list of predicates.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-197">A list of predicates.</span></span> | 

<span data-ttu-id="6e0b3-198">The **PredicateGroup** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-198">The **PredicateGroup** element contains the following attribute:</span></span>

| <span data-ttu-id="6e0b3-199">Attribute</span><span class="sxs-lookup"><span data-stu-id="6e0b3-199">Attribute</span></span> | <span data-ttu-id="6e0b3-200">Required</span><span class="sxs-lookup"><span data-stu-id="6e0b3-200">Required</span></span> | <span data-ttu-id="6e0b3-201">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-201">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="6e0b3-202">Id</span><span class="sxs-lookup"><span data-stu-id="6e0b3-202">Id</span></span> | <span data-ttu-id="6e0b3-203">Yes</span><span class="sxs-lookup"><span data-stu-id="6e0b3-203">Yes</span></span> | <span data-ttu-id="6e0b3-204">An identifier that's used for the predicate group.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-204">An identifier that's used for the predicate group.</span></span>  |

<span data-ttu-id="6e0b3-205">The **PredicateGroup** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-205">The **PredicateGroup** element contains the following elements:</span></span>

| <span data-ttu-id="6e0b3-206">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-206">Element</span></span> | <span data-ttu-id="6e0b3-207">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-207">Occurrences</span></span> | <span data-ttu-id="6e0b3-208">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-208">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-209">UserHelpText</span><span class="sxs-lookup"><span data-stu-id="6e0b3-209">UserHelpText</span></span> | <span data-ttu-id="6e0b3-210">1:1</span><span class="sxs-lookup"><span data-stu-id="6e0b3-210">1:1</span></span> |  <span data-ttu-id="6e0b3-211">A description of the predicate that can be helpful for users to know what value they should type.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-211">A description of the predicate that can be helpful for users to know what value they should type.</span></span> | 
| <span data-ttu-id="6e0b3-212">PredicateReferences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-212">PredicateReferences</span></span> | <span data-ttu-id="6e0b3-213">1:n</span><span class="sxs-lookup"><span data-stu-id="6e0b3-213">1:n</span></span> | <span data-ttu-id="6e0b3-214">A list of  predicate references.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-214">A list of  predicate references.</span></span> | 

<span data-ttu-id="6e0b3-215">The **PredicateReferences** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-215">The **PredicateReferences** element contains the following attributes:</span></span>

| <span data-ttu-id="6e0b3-216">Attribute</span><span class="sxs-lookup"><span data-stu-id="6e0b3-216">Attribute</span></span> | <span data-ttu-id="6e0b3-217">Required</span><span class="sxs-lookup"><span data-stu-id="6e0b3-217">Required</span></span> | <span data-ttu-id="6e0b3-218">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-218">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="6e0b3-219">MatchAtLeast</span><span class="sxs-lookup"><span data-stu-id="6e0b3-219">MatchAtLeast</span></span> | <span data-ttu-id="6e0b3-220">No</span><span class="sxs-lookup"><span data-stu-id="6e0b3-220">No</span></span> | <span data-ttu-id="6e0b3-221">Specifies that the value must match at least that many predicate definitions for the input to be accepted.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-221">Specifies that the value must match at least that many predicate definitions for the input to be accepted.</span></span> |

<span data-ttu-id="6e0b3-222">The **PredicateReferences** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-222">The **PredicateReferences** element contains the following elements:</span></span>

| <span data-ttu-id="6e0b3-223">Element</span><span class="sxs-lookup"><span data-stu-id="6e0b3-223">Element</span></span> | <span data-ttu-id="6e0b3-224">Occurrences</span><span class="sxs-lookup"><span data-stu-id="6e0b3-224">Occurrences</span></span> | <span data-ttu-id="6e0b3-225">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-225">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="6e0b3-226">PredicateReference</span><span class="sxs-lookup"><span data-stu-id="6e0b3-226">PredicateReference</span></span> | <span data-ttu-id="6e0b3-227">1:n</span><span class="sxs-lookup"><span data-stu-id="6e0b3-227">1:n</span></span> | <span data-ttu-id="6e0b3-228">A reference to a predicate.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-228">A reference to a predicate.</span></span> | 

<span data-ttu-id="6e0b3-229">The **PredicateReference** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-229">The **PredicateReference** element contains the following attributes:</span></span>

| <span data-ttu-id="6e0b3-230">Attribute</span><span class="sxs-lookup"><span data-stu-id="6e0b3-230">Attribute</span></span> | <span data-ttu-id="6e0b3-231">Required</span><span class="sxs-lookup"><span data-stu-id="6e0b3-231">Required</span></span> | <span data-ttu-id="6e0b3-232">Description</span><span class="sxs-lookup"><span data-stu-id="6e0b3-232">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="6e0b3-233">Id</span><span class="sxs-lookup"><span data-stu-id="6e0b3-233">Id</span></span> | <span data-ttu-id="6e0b3-234">Yes</span><span class="sxs-lookup"><span data-stu-id="6e0b3-234">Yes</span></span> | <span data-ttu-id="6e0b3-235">An identifier that's used for the predicate validation.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-235">An identifier that's used for the predicate validation.</span></span>  |


## <a name="configure-password-complexity"></a><span data-ttu-id="6e0b3-236">Configure password complexity</span><span class="sxs-lookup"><span data-stu-id="6e0b3-236">Configure password complexity</span></span>

<span data-ttu-id="6e0b3-237">With **Predicates** and **PredicateValidationsInput** you can control the complexity requirements for passwords provided by a user when creating an account.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-237">With **Predicates** and **PredicateValidationsInput** you can control the complexity requirements for passwords provided by a user when creating an account.</span></span> <span data-ttu-id="6e0b3-238">By default, Azure AD B2C uses strong passwords.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-238">By default, Azure AD B2C uses strong passwords.</span></span> <span data-ttu-id="6e0b3-239">Azure AD B2C also supports configuration options to control the complexity of passwords that customers can use.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-239">Azure AD B2C also supports configuration options to control the complexity of passwords that customers can use.</span></span> <span data-ttu-id="6e0b3-240">You can define password complexity by using these predicate elements:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-240">You can define password complexity by using these predicate elements:</span></span> 

- <span data-ttu-id="6e0b3-241">**IsLengthBetween8And64** using the `IsLengthRange` method, validates that the password must be between 8 and 64 characters.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-241">**IsLengthBetween8And64** using the `IsLengthRange` method, validates that the password must be between 8 and 64 characters.</span></span>
- <span data-ttu-id="6e0b3-242">**Lowercase** using the `IncludesCharacters` method, validates that the password contains a lowercase letter.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-242">**Lowercase** using the `IncludesCharacters` method, validates that the password contains a lowercase letter.</span></span>
- <span data-ttu-id="6e0b3-243">**Uppercase** using the `IncludesCharacters` method, validates that the password contains an uppercase letter.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-243">**Uppercase** using the `IncludesCharacters` method, validates that the password contains an uppercase letter.</span></span>
- <span data-ttu-id="6e0b3-244">**Number** using the `IncludesCharacters` method, validates that the password contains a digit.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-244">**Number** using the `IncludesCharacters` method, validates that the password contains a digit.</span></span>
- <span data-ttu-id="6e0b3-245">**Symbol** using the `IncludesCharacters` method, validates that the password contains one of following symbols `@#$%^&*\-_+=[]{}|\:',?/~"();!`</span><span class="sxs-lookup"><span data-stu-id="6e0b3-245">**Symbol** using the `IncludesCharacters` method, validates that the password contains one of following symbols `@#$%^&*\-_+=[]{}|\:',?/~"();!`</span></span>
- <span data-ttu-id="6e0b3-246">**PIN** using the `MatchesRegex` method, validates that the password contains numbers only.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-246">**PIN** using the `MatchesRegex` method, validates that the password contains numbers only.</span></span>
- <span data-ttu-id="6e0b3-247">**AllowedAADCharacters** using the `MatchesRegex` method, validates that the password only invalid character was provided.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-247">**AllowedAADCharacters** using the `MatchesRegex` method, validates that the password only invalid character was provided.</span></span>
- <span data-ttu-id="6e0b3-248">**DisallowedWhitespace** using the `MatchesRegex` method, validates that the password doesn't begin or end with a whitespace character.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-248">**DisallowedWhitespace** using the `MatchesRegex` method, validates that the password doesn't begin or end with a whitespace character.</span></span>

```XML
<Predicates>
  <Predicate Id="IsLengthBetween8And64" Method="IsLengthRange">
    <UserHelpText>The password must be between 8 and 64 characters.</UserHelpText>
    <Parameters>
      <Parameter Id="Minimum">8</Parameter>
      <Parameter Id="Maximum">64</Parameter>
    </Parameters>
  </Predicate>

  <Predicate Id="Lowercase" Method="IncludesCharacters">
    <UserHelpText>a lowercase letter</UserHelpText>
    <Parameters>
      <Parameter Id="CharacterSet">a-z</Parameter>
    </Parameters>
  </Predicate>

  <Predicate Id="Uppercase" Method="IncludesCharacters">
    <UserHelpText>an uppercase letter</UserHelpText>
    <Parameters>
      <Parameter Id="CharacterSet">A-Z</Parameter>
    </Parameters>
  </Predicate>

  <Predicate Id="Number" Method="IncludesCharacters">
    <UserHelpText>a digit</UserHelpText>
    <Parameters>
      <Parameter Id="CharacterSet">0-9</Parameter>
    </Parameters>
  </Predicate>

  <Predicate Id="Symbol" Method="IncludesCharacters">
    <UserHelpText>a symbol</UserHelpText>
    <Parameters>
      <Parameter Id="CharacterSet">@#$%^&amp;*\-_+=[]{}|\:',?/`~"();!</Parameter>
    </Parameters>
  </Predicate>

  <Predicate Id="PIN" Method="MatchesRegex">
    <UserHelpText>The password must be numbers only.</UserHelpText>
    <Parameters>
      <Parameter Id="RegularExpression">^[0-9]+$</Parameter>
    </Parameters>
  </Predicate>

  <Predicate Id="AllowedAADCharacters" Method="MatchesRegex">
    <UserHelpText>An invalid character was provided.</UserHelpText>
    <Parameters>
      <Parameter Id="RegularExpression">(^([0-9A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~"();! ]|(\.(?!@)))+$)|(^$)</Parameter>
    </Parameters>
  </Predicate>

  <Predicate Id="DisallowedWhitespace" Method="MatchesRegex">
    <UserHelpText>The password must not begin or end with a whitespace character.</UserHelpText>
    <Parameters>
      <Parameter Id="RegularExpression">(^\S.*\S$)|(^\S+$)|(^$)</Parameter>
    </Parameters>
  </Predicate>
```

<span data-ttu-id="6e0b3-249">After you define the basic validations, you can combine them together and create a set of password policies that you can use in your policy:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-249">After you define the basic validations, you can combine them together and create a set of password policies that you can use in your policy:</span></span>

- <span data-ttu-id="6e0b3-250">**SimplePassword** validates the DisallowedWhitespace, AllowedAADCharacters, and IsLengthBetween8And64</span><span class="sxs-lookup"><span data-stu-id="6e0b3-250">**SimplePassword** validates the DisallowedWhitespace, AllowedAADCharacters, and IsLengthBetween8And64</span></span>
- <span data-ttu-id="6e0b3-251">**StrongPassword** validates the DisallowedWhitespace, AllowedAADCharacters, IsLengthBetween8And64.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-251">**StrongPassword** validates the DisallowedWhitespace, AllowedAADCharacters, IsLengthBetween8And64.</span></span> <span data-ttu-id="6e0b3-252">The last group `CharacterClasses` runs an additional set of predicates with `MatchAtLeast` set to 3.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-252">The last group `CharacterClasses` runs an additional set of predicates with `MatchAtLeast` set to 3.</span></span> <span data-ttu-id="6e0b3-253">The user password must be between 8 and 16 characters, and three of the following characters: Lowercase, Uppercase, Number, or Symbol.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-253">The user password must be between 8 and 16 characters, and three of the following characters: Lowercase, Uppercase, Number, or Symbol.</span></span>
- <span data-ttu-id="6e0b3-254">**CustomPassword** validates only DisallowedWhitespace, AllowedAADCharacters.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-254">**CustomPassword** validates only DisallowedWhitespace, AllowedAADCharacters.</span></span> <span data-ttu-id="6e0b3-255">So, user can provide any password with any length, as long as the characters are valid.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-255">So, user can provide any password with any length, as long as the characters are valid.</span></span>

```XML
<PredicateValidations>
  <PredicateValidation Id="SimplePassword">
    <PredicateGroups>
      <PredicateGroup Id="DisallowedWhitespaceGroup">
        <PredicateReferences>
          <PredicateReference Id="DisallowedWhitespace" />
        </PredicateReferences>
      </PredicateGroup>
      <PredicateGroup Id="AllowedAADCharactersGroup">
        <PredicateReferences>
          <PredicateReference Id="AllowedAADCharacters" />
        </PredicateReferences>
      </PredicateGroup>
      <PredicateGroup Id="LengthGroup">
        <PredicateReferences>
          <PredicateReference Id="IsLengthBetween8And64" />
        </PredicateReferences>
      </PredicateGroup>
    </PredicateGroups>
  </PredicateValidation>

  <PredicateValidation Id="StrongPassword">
    <PredicateGroups>
      <PredicateGroup Id="DisallowedWhitespaceGroup">
        <PredicateReferences>
          <PredicateReference Id="DisallowedWhitespace" />
       </PredicateReferences>
      </PredicateGroup>
      <PredicateGroup Id="AllowedAADCharactersGroup">
        <PredicateReferences>
          <PredicateReference Id="AllowedAADCharacters" />
        </PredicateReferences>
      </PredicateGroup>
      <PredicateGroup Id="LengthGroup">
        <PredicateReferences>
          <PredicateReference Id="IsLengthBetween8And64" />
        </PredicateReferences>
      </PredicateGroup>
      <PredicateGroup Id="CharacterClasses">
        <UserHelpText>The password must have at least 3 of the following:</UserHelpText>
        <PredicateReferences MatchAtLeast="3">
          <PredicateReference Id="Lowercase" />
          <PredicateReference Id="Uppercase" />
          <PredicateReference Id="Number" />
          <PredicateReference Id="Symbol" />
        </PredicateReferences>
      </PredicateGroup>
    </PredicateGroups>
  </PredicateValidation>

  <PredicateValidation Id="CustomPassword">
    <PredicateGroups>
      <PredicateGroup Id="DisallowedWhitespaceGroup">
        <PredicateReferences>
          <PredicateReference Id="DisallowedWhitespace" />
        </PredicateReferences>
      </PredicateGroup>
      <PredicateGroup Id="AllowedAADCharactersGroup">
        <PredicateReferences>
          <PredicateReference Id="AllowedAADCharacters" />
        </PredicateReferences>
      </PredicateGroup>
    </PredicateGroups>
  </PredicateValidation>
</PredicateValidations>
```

<span data-ttu-id="6e0b3-256">In your claim type, add the **PredicateValidationReference** element and specify the identifier as one of the predicate validations, such as SimplePassword, StrongPassword, or CustomPassword.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-256">In your claim type, add the **PredicateValidationReference** element and specify the identifier as one of the predicate validations, such as SimplePassword, StrongPassword, or CustomPassword.</span></span>

```XML
<ClaimType Id="password">
  <DisplayName>Password</DisplayName>
  <DataType>string</DataType>
  <AdminHelpText>Enter password</AdminHelpText>
  <UserHelpText>Enter password</UserHelpText>
  <UserInputType>Password</UserInputType>
  <PredicateValidationReference Id="StrongPassword" />
</ClaimType>
```

<span data-ttu-id="6e0b3-257">The following shows how the elements are organized when Azure AD B2C displays the error message:</span><span class="sxs-lookup"><span data-stu-id="6e0b3-257">The following shows how the elements are organized when Azure AD B2C displays the error message:</span></span>

![Predicate process](./media/predicates/predicates-pass.png)

 ## <a name="configure-a-date-range"></a><span data-ttu-id="6e0b3-259">Configure a date range</span><span class="sxs-lookup"><span data-stu-id="6e0b3-259">Configure a date range</span></span>

<span data-ttu-id="6e0b3-260">With the **Predicates** and **PredicateValidations** elements you can control the minimum and maximum date values of the **UserInputType** by using a `DateTimeDropdown`.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-260">With the **Predicates** and **PredicateValidations** elements you can control the minimum and maximum date values of the **UserInputType** by using a `DateTimeDropdown`.</span></span> <span data-ttu-id="6e0b3-261">To do this, create a **Predicate** with the `IsDateRange` method and provide the minimum and maximum parameters.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-261">To do this, create a **Predicate** with the `IsDateRange` method and provide the minimum and maximum parameters.</span></span>

```XML
<Predicates>
  <Predicate Id="DateRange" Method="IsDateRange" HelpText="The date must be between 01-01-1905 and today.">
    <Parameters>
      <Parameter Id="Minimum">1980-01-01</Parameter>
      <Parameter Id="Maximum">Today</Parameter>
    </Parameters>
  </Predicate>
</Predicates>
```

<span data-ttu-id="6e0b3-262">Add a **PredicateValidation** with a reference to the `DateRange` predicate.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-262">Add a **PredicateValidation** with a reference to the `DateRange` predicate.</span></span>

```XML
<PredicateValidations>
  <PredicateValidation Id="CustomDateRange">
    <PredicateGroups>
      <PredicateGroup Id="DateRangeGroup">
        <PredicateReferences>
          <PredicateReference Id="DateRange" />
        </PredicateReferences>
      </PredicateGroup>
    </PredicateGroups>
  </PredicateValidation>
</PredicateValidations>
```

<span data-ttu-id="6e0b3-263">In your claim type, add **PredicateValidationReference** element and specify the identifier as `CustomDateRange`.</span><span class="sxs-lookup"><span data-stu-id="6e0b3-263">In your claim type, add **PredicateValidationReference** element and specify the identifier as `CustomDateRange`.</span></span> 
    
```XML
<ClaimType Id="dateOfBirth">
  <DisplayName>Date of Birth</DisplayName>
  <DataType>date</DataType>
  <AdminHelpText>The user's date of birth.</AdminHelpText>
  <UserHelpText>Your date of birth.</UserHelpText>
  <UserInputType>DateTimeDropdown</UserInputType>
  <PredicateValidationReference Id="CustomDateRange" />
</ClaimType>
 ```