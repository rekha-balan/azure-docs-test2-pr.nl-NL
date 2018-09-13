---
title: Define a validation technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a Azure Active Directory technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 07a5c378ddf73f245104f64e1dae945525a1e01a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855762"
---
# <a name="define-a-validation-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a><span data-ttu-id="f3920-103">Define a validation technical profile in an Azure Active Directory B2C custom policy</span><span class="sxs-lookup"><span data-stu-id="f3920-103">Define a validation technical profile in an Azure Active Directory B2C custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]
 
<span data-ttu-id="f3920-104">A validation technical profile is an ordinary technical profile from any protocol, such as [Azure Active Directory](active-directory-technical-profile.md) or a [REST API](restful-technical-profile.md).</span><span class="sxs-lookup"><span data-stu-id="f3920-104">A validation technical profile is an ordinary technical profile from any protocol, such as [Azure Active Directory](active-directory-technical-profile.md) or a [REST API](restful-technical-profile.md).</span></span> <span data-ttu-id="f3920-105">The validation technical profile returns output claims or returns an HTTP 409 error message (Conflict response status code), with the following data:</span><span class="sxs-lookup"><span data-stu-id="f3920-105">The validation technical profile returns output claims or returns an HTTP 409 error message (Conflict response status code), with the following data:</span></span>

```JSON
{
    "version": "1.0.0",
    "status": 409,
    "userMessage": "Your error message"
}
```

<span data-ttu-id="f3920-106">Claims that are retuned from a validation technical profile are added back to the claims bag.</span><span class="sxs-lookup"><span data-stu-id="f3920-106">Claims that are retuned from a validation technical profile are added back to the claims bag.</span></span> <span data-ttu-id="f3920-107">You can use those claims in the next validation technical profiles.</span><span class="sxs-lookup"><span data-stu-id="f3920-107">You can use those claims in the next validation technical profiles.</span></span>

<span data-ttu-id="f3920-108">Validation technical profiles are executed in the sequence that they appear in the **ValidationTechnicalProfiles** element.</span><span class="sxs-lookup"><span data-stu-id="f3920-108">Validation technical profiles are executed in the sequence that they appear in the **ValidationTechnicalProfiles** element.</span></span> <span data-ttu-id="f3920-109">You can configure in a validation technical profile whether the execution of any subsequent validation technical profiles should continue if the validation technical profile raises an error or is successful.</span><span class="sxs-lookup"><span data-stu-id="f3920-109">You can configure in a validation technical profile whether the execution of any subsequent validation technical profiles should continue if the validation technical profile raises an error or is successful.</span></span>  

<span data-ttu-id="f3920-110">A validation technical profile can be conditionally executed based on preconditions defined in the **ValidationTechnicalProfile** element.</span><span class="sxs-lookup"><span data-stu-id="f3920-110">A validation technical profile can be conditionally executed based on preconditions defined in the **ValidationTechnicalProfile** element.</span></span> <span data-ttu-id="f3920-111">For example, you can check whether a specific claims exists, or if a claim is equal or not to the specified value.</span><span class="sxs-lookup"><span data-stu-id="f3920-111">For example, you can check whether a specific claims exists, or if a claim is equal or not to the specified value.</span></span>

<span data-ttu-id="f3920-112">A self-asserted technical profile may define a validation technical profile to be used for validating some or all of its output claims.</span><span class="sxs-lookup"><span data-stu-id="f3920-112">A self-asserted technical profile may define a validation technical profile to be used for validating some or all of its output claims.</span></span> <span data-ttu-id="f3920-113">All of the input claims of the referenced technical profile must appear in the output claims of the referencing validation technical profile.</span><span class="sxs-lookup"><span data-stu-id="f3920-113">All of the input claims of the referenced technical profile must appear in the output claims of the referencing validation technical profile.</span></span>


## <a name="validationtechnicalprofiles"></a><span data-ttu-id="f3920-114">ValidationTechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="f3920-114">ValidationTechnicalProfiles</span></span>

<span data-ttu-id="f3920-115">The **ValidationTechnicalProfiles** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="f3920-115">The **ValidationTechnicalProfiles** element contains the following elements:</span></span>

| <span data-ttu-id="f3920-116">Element</span><span class="sxs-lookup"><span data-stu-id="f3920-116">Element</span></span> | <span data-ttu-id="f3920-117">Occurrences</span><span class="sxs-lookup"><span data-stu-id="f3920-117">Occurrences</span></span> | <span data-ttu-id="f3920-118">Description</span><span class="sxs-lookup"><span data-stu-id="f3920-118">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="f3920-119">ValidationTechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="f3920-119">ValidationTechnicalProfile</span></span> | <span data-ttu-id="f3920-120">1:n</span><span class="sxs-lookup"><span data-stu-id="f3920-120">1:n</span></span> | <span data-ttu-id="f3920-121">A technical profile to be used for validating some or all of the output claims of the referencing technical profile.</span><span class="sxs-lookup"><span data-stu-id="f3920-121">A technical profile to be used for validating some or all of the output claims of the referencing technical profile.</span></span> |

<span data-ttu-id="f3920-122">The **ValidationTechnicalProfile** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="f3920-122">The **ValidationTechnicalProfile** element contains the following attribute:</span></span>

| <span data-ttu-id="f3920-123">Attribute</span><span class="sxs-lookup"><span data-stu-id="f3920-123">Attribute</span></span> | <span data-ttu-id="f3920-124">Required</span><span class="sxs-lookup"><span data-stu-id="f3920-124">Required</span></span> | <span data-ttu-id="f3920-125">Description</span><span class="sxs-lookup"><span data-stu-id="f3920-125">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="f3920-126">ReferenceId</span><span class="sxs-lookup"><span data-stu-id="f3920-126">ReferenceId</span></span> | <span data-ttu-id="f3920-127">Yes</span><span class="sxs-lookup"><span data-stu-id="f3920-127">Yes</span></span> | <span data-ttu-id="f3920-128">An identifier of a technical profile already defined in the policy or parent policy.</span><span class="sxs-lookup"><span data-stu-id="f3920-128">An identifier of a technical profile already defined in the policy or parent policy.</span></span> |
|<span data-ttu-id="f3920-129">ContinueOnError</span><span class="sxs-lookup"><span data-stu-id="f3920-129">ContinueOnError</span></span>|<span data-ttu-id="f3920-130">No</span><span class="sxs-lookup"><span data-stu-id="f3920-130">No</span></span>| <span data-ttu-id="f3920-131">Indicating whether validation of any subsequent validation technical profiles should continue if this validaiton technical profile raises an error.</span><span class="sxs-lookup"><span data-stu-id="f3920-131">Indicating whether validation of any subsequent validation technical profiles should continue if this validaiton technical profile raises an error.</span></span> <span data-ttu-id="f3920-132">Posible values: `ture` or `false` (default,  processing of further validation profiles will stop and an error returned).</span><span class="sxs-lookup"><span data-stu-id="f3920-132">Posible values: `ture` or `false` (default,  processing of further validation profiles will stop and an error returned).</span></span> 
|<span data-ttu-id="f3920-133">ContinueOnSuccess</span><span class="sxs-lookup"><span data-stu-id="f3920-133">ContinueOnSuccess</span></span> | <span data-ttu-id="f3920-134">No</span><span class="sxs-lookup"><span data-stu-id="f3920-134">No</span></span> | <span data-ttu-id="f3920-135">Indicating whether validation of any subsequent validation profiles should continue if this validation technical profile succeeds.</span><span class="sxs-lookup"><span data-stu-id="f3920-135">Indicating whether validation of any subsequent validation profiles should continue if this validation technical profile succeeds.</span></span> <span data-ttu-id="f3920-136">Posible values: `ture` or `false`.</span><span class="sxs-lookup"><span data-stu-id="f3920-136">Posible values: `ture` or `false`.</span></span> <span data-ttu-id="f3920-137">The default is `true`, meaning that the processing of further validation profiles will continue.</span><span class="sxs-lookup"><span data-stu-id="f3920-137">The default is `true`, meaning that the processing of further validation profiles will continue.</span></span> |

<span data-ttu-id="f3920-138">The **ValidationTechnicalProfile** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="f3920-138">The **ValidationTechnicalProfile** element contains the following element:</span></span>

| <span data-ttu-id="f3920-139">Element</span><span class="sxs-lookup"><span data-stu-id="f3920-139">Element</span></span> | <span data-ttu-id="f3920-140">Occurrences</span><span class="sxs-lookup"><span data-stu-id="f3920-140">Occurrences</span></span> | <span data-ttu-id="f3920-141">Description</span><span class="sxs-lookup"><span data-stu-id="f3920-141">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="f3920-142">Preconditions</span><span class="sxs-lookup"><span data-stu-id="f3920-142">Preconditions</span></span> | <span data-ttu-id="f3920-143">0:1</span><span class="sxs-lookup"><span data-stu-id="f3920-143">0:1</span></span> | <span data-ttu-id="f3920-144">A list of preconditions that must be satisfied for the validation technical profile to execute.</span><span class="sxs-lookup"><span data-stu-id="f3920-144">A list of preconditions that must be satisfied for the validation technical profile to execute.</span></span> |

<span data-ttu-id="f3920-145">The **Precondition** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="f3920-145">The **Precondition** element contains the following attribute:</span></span>

| <span data-ttu-id="f3920-146">Attribute</span><span class="sxs-lookup"><span data-stu-id="f3920-146">Attribute</span></span> | <span data-ttu-id="f3920-147">Required</span><span class="sxs-lookup"><span data-stu-id="f3920-147">Required</span></span> | <span data-ttu-id="f3920-148">Description</span><span class="sxs-lookup"><span data-stu-id="f3920-148">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="f3920-149">Type</span><span class="sxs-lookup"><span data-stu-id="f3920-149">Type</span></span> | <span data-ttu-id="f3920-150">Yes</span><span class="sxs-lookup"><span data-stu-id="f3920-150">Yes</span></span> | <span data-ttu-id="f3920-151">The type of check or query to perform for the precondition.</span><span class="sxs-lookup"><span data-stu-id="f3920-151">The type of check or query to perform for the precondition.</span></span> <span data-ttu-id="f3920-152">Either `ClaimsExist` is specified to ensure that actions should be performed if the specified claims exist in the user's current claim set, or `ClaimEquals` is specified that the actions should be performed if the specified claim exists and its value is equal to the specified value.</span><span class="sxs-lookup"><span data-stu-id="f3920-152">Either `ClaimsExist` is specified to ensure that actions should be performed if the specified claims exist in the user's current claim set, or `ClaimEquals` is specified that the actions should be performed if the specified claim exists and its value is equal to the specified value.</span></span> |
| <span data-ttu-id="f3920-153">ExecuteActionsIf</span><span class="sxs-lookup"><span data-stu-id="f3920-153">ExecuteActionsIf</span></span> | <span data-ttu-id="f3920-154">Yes</span><span class="sxs-lookup"><span data-stu-id="f3920-154">Yes</span></span> | <span data-ttu-id="f3920-155">Indicates whether the actions in the precondition should be performed if the test is true or false.</span><span class="sxs-lookup"><span data-stu-id="f3920-155">Indicates whether the actions in the precondition should be performed if the test is true or false.</span></span> | 

<span data-ttu-id="f3920-156">The **Precondition** element contains following elements:</span><span class="sxs-lookup"><span data-stu-id="f3920-156">The **Precondition** element contains following elements:</span></span>

| <span data-ttu-id="f3920-157">Element</span><span class="sxs-lookup"><span data-stu-id="f3920-157">Element</span></span> | <span data-ttu-id="f3920-158">Occurrences</span><span class="sxs-lookup"><span data-stu-id="f3920-158">Occurrences</span></span> | <span data-ttu-id="f3920-159">Description</span><span class="sxs-lookup"><span data-stu-id="f3920-159">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="f3920-160">Value</span><span class="sxs-lookup"><span data-stu-id="f3920-160">Value</span></span> | <span data-ttu-id="f3920-161">1:n</span><span class="sxs-lookup"><span data-stu-id="f3920-161">1:n</span></span> | <span data-ttu-id="f3920-162">The data that is used by the check.</span><span class="sxs-lookup"><span data-stu-id="f3920-162">The data that is used by the check.</span></span> <span data-ttu-id="f3920-163">If the type of this check is `ClaimsExist`, this field specifies a ClaimTypeReferenceId to query for.</span><span class="sxs-lookup"><span data-stu-id="f3920-163">If the type of this check is `ClaimsExist`, this field specifies a ClaimTypeReferenceId to query for.</span></span> <span data-ttu-id="f3920-164">If the type of check is `ClaimEquals`, this field specifies a ClaimTypeReferenceId to query for.</span><span class="sxs-lookup"><span data-stu-id="f3920-164">If the type of check is `ClaimEquals`, this field specifies a ClaimTypeReferenceId to query for.</span></span> <span data-ttu-id="f3920-165">While another value element contains the value to be checked.</span><span class="sxs-lookup"><span data-stu-id="f3920-165">While another value element contains the value to be checked.</span></span>|
| <span data-ttu-id="f3920-166">Action</span><span class="sxs-lookup"><span data-stu-id="f3920-166">Action</span></span> | <span data-ttu-id="f3920-167">1:1</span><span class="sxs-lookup"><span data-stu-id="f3920-167">1:1</span></span> | <span data-ttu-id="f3920-168">The action that should be taken if the precondition check within an orchestration step is true.</span><span class="sxs-lookup"><span data-stu-id="f3920-168">The action that should be taken if the precondition check within an orchestration step is true.</span></span> <span data-ttu-id="f3920-169">The value of the **Action** is set to `SkipThisValidationTechnicalProfile`.</span><span class="sxs-lookup"><span data-stu-id="f3920-169">The value of the **Action** is set to `SkipThisValidationTechnicalProfile`.</span></span> <span data-ttu-id="f3920-170">Specifies that the associated validation technical profile should not be executed.</span><span class="sxs-lookup"><span data-stu-id="f3920-170">Specifies that the associated validation technical profile should not be executed.</span></span> | 

### <a name="example"></a><span data-ttu-id="f3920-171">Example</span><span class="sxs-lookup"><span data-stu-id="f3920-171">Example</span></span>

<span data-ttu-id="f3920-172">Following example uses these validation technical profiles:</span><span class="sxs-lookup"><span data-stu-id="f3920-172">Following example uses these validation technical profiles:</span></span> 

1. <span data-ttu-id="f3920-173">The first validation technical profile checks user credentials and doesn't continue if an error occurs, such as invalid username or bad password.</span><span class="sxs-lookup"><span data-stu-id="f3920-173">The first validation technical profile checks user credentials and doesn't continue if an error occurs, such as invalid username or bad password.</span></span> 
2. <span data-ttu-id="f3920-174">The next validation technical profile, doesn't execute if the userType claim does not exist, or if the value of the userType is `Partner`.</span><span class="sxs-lookup"><span data-stu-id="f3920-174">The next validation technical profile, doesn't execute if the userType claim does not exist, or if the value of the userType is `Partner`.</span></span> <span data-ttu-id="f3920-175">The validation technical profile tries to read the user profile from the internal customer database and continue if an error occurs, such as REST API service not avaible, or any internal error.</span><span class="sxs-lookup"><span data-stu-id="f3920-175">The validation technical profile tries to read the user profile from the internal customer database and continue if an error occurs, such as REST API service not avaible, or any internal error.</span></span>
3. <span data-ttu-id="f3920-176">The last validation technical profile, doesn't execute if the userType claim has not existed, or if the value of the userType is `Customer`.</span><span class="sxs-lookup"><span data-stu-id="f3920-176">The last validation technical profile, doesn't execute if the userType claim has not existed, or if the value of the userType is `Customer`.</span></span> <span data-ttu-id="f3920-177">The validation technical profile tries to read the user profile from the internal partner database and continues if an error occurs, such as REST API service not avaible, or any internal error.</span><span class="sxs-lookup"><span data-stu-id="f3920-177">The validation technical profile tries to read the user profile from the internal partner database and continues if an error occurs, such as REST API service not avaible, or any internal error.</span></span>

```XML
<ValidationTechnicalProfiles>
  <ValidationTechnicalProfile ReferenceId="login-NonInteractive" ContinueOnError="false"  />
    
  <ValidationTechnicalProfile ReferenceId="REST-ReadProfileFromCustomertsDatabase" ContinueOnError="true" >
    <Preconditions>
       <Precondition Type="ClaimsExist" ExecuteActionsIf="false">
          <Value>userType</Value>
          <Action>SkipThisValidationTechnicalProfile</Action>
       </Precondition>
       <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
         <Value>userType</Value>
         <Value>Partner</Value>
         <Action>SkipThisValidationTechnicalProfile</Action>
       </Precondition>
    </Preconditions>          
  </ValidationTechnicalProfile>

  <ValidationTechnicalProfile ReferenceId="REST-ReadProfileFromPartnersDatabase" ContinueOnError="true" >
    <Preconditions>
       <Precondition Type="ClaimsExist" ExecuteActionsIf="false">
          <Value>userType</Value>
          <Action>SkipThisValidationTechnicalProfile</Action>
       </Precondition>
       <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
         <Value>userType</Value>
         <Value>Customer</Value>
         <Action>SkipThisValidationTechnicalProfile</Action>
       </Precondition>
    </Preconditions>          
  </ValidationTechnicalProfile>
</ValidationTechnicalProfiles>
```














