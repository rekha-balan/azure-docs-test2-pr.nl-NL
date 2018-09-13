---
title: Date claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: Date claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 42090b8b55becc5e703e0e7180d0cbec0d48a3f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869248"
---
# <a name="date-claims-transformations"></a><span data-ttu-id="9e9ac-103">Date claims transformations</span><span class="sxs-lookup"><span data-stu-id="9e9ac-103">Date claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="9e9ac-104">This article provides examples for using the date claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-104">This article provides examples for using the date claims transformations of the Identity Experience Framework  schema in Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="9e9ac-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="9e9ac-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="assertdatetimeisgreaterthan"></a><span data-ttu-id="9e9ac-106">AssertDateTimeIsGreaterThan</span><span class="sxs-lookup"><span data-stu-id="9e9ac-106">AssertDateTimeIsGreaterThan</span></span> 

<span data-ttu-id="9e9ac-107">Checks that one date and time claim (string data type) is greater than a second date and time claim (string data type), and throws an exception.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-107">Checks that one date and time claim (string data type) is greater than a second date and time claim (string data type), and throws an exception.</span></span>

| <span data-ttu-id="9e9ac-108">Item</span><span class="sxs-lookup"><span data-stu-id="9e9ac-108">Item</span></span> | <span data-ttu-id="9e9ac-109">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="9e9ac-109">TransformationClaimType</span></span> | <span data-ttu-id="9e9ac-110">Data Type</span><span class="sxs-lookup"><span data-stu-id="9e9ac-110">Data Type</span></span> | <span data-ttu-id="9e9ac-111">Notes</span><span class="sxs-lookup"><span data-stu-id="9e9ac-111">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="9e9ac-112">inputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-112">inputClaim</span></span> | <span data-ttu-id="9e9ac-113">leftOperand</span><span class="sxs-lookup"><span data-stu-id="9e9ac-113">leftOperand</span></span> | <span data-ttu-id="9e9ac-114">string</span><span class="sxs-lookup"><span data-stu-id="9e9ac-114">string</span></span> | <span data-ttu-id="9e9ac-115">First claim's type, which should be greater than the second claim.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-115">First claim's type, which should be greater than the second claim.</span></span> |
| <span data-ttu-id="9e9ac-116">inputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-116">inputClaim</span></span> | <span data-ttu-id="9e9ac-117">rightOperand</span><span class="sxs-lookup"><span data-stu-id="9e9ac-117">rightOperand</span></span> | <span data-ttu-id="9e9ac-118">string</span><span class="sxs-lookup"><span data-stu-id="9e9ac-118">string</span></span> | <span data-ttu-id="9e9ac-119">Second claim's type, which should be less than the first claim.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-119">Second claim's type, which should be less than the first claim.</span></span> |
| <span data-ttu-id="9e9ac-120">InputParameter</span><span class="sxs-lookup"><span data-stu-id="9e9ac-120">InputParameter</span></span> | <span data-ttu-id="9e9ac-121">AssertIfEqualTo</span><span class="sxs-lookup"><span data-stu-id="9e9ac-121">AssertIfEqualTo</span></span> | <span data-ttu-id="9e9ac-122">boolean</span><span class="sxs-lookup"><span data-stu-id="9e9ac-122">boolean</span></span> | <span data-ttu-id="9e9ac-123">Specifies whether this assertion should pass if the left operand is equal to the right operand.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-123">Specifies whether this assertion should pass if the left operand is equal to the right operand.</span></span> |
| <span data-ttu-id="9e9ac-124">InputParameter</span><span class="sxs-lookup"><span data-stu-id="9e9ac-124">InputParameter</span></span> | <span data-ttu-id="9e9ac-125">AssertIfRightOperandIsNotPresent</span><span class="sxs-lookup"><span data-stu-id="9e9ac-125">AssertIfRightOperandIsNotPresent</span></span> | <span data-ttu-id="9e9ac-126">boolean</span><span class="sxs-lookup"><span data-stu-id="9e9ac-126">boolean</span></span> | <span data-ttu-id="9e9ac-127">Specifies whether this assertion should pass if the right operand is missing.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-127">Specifies whether this assertion should pass if the right operand is missing.</span></span> |
| <span data-ttu-id="9e9ac-128">InputParameter</span><span class="sxs-lookup"><span data-stu-id="9e9ac-128">InputParameter</span></span> | <span data-ttu-id="9e9ac-129">TreatAsEqualIfWithinMillseconds</span><span class="sxs-lookup"><span data-stu-id="9e9ac-129">TreatAsEqualIfWithinMillseconds</span></span> | <span data-ttu-id="9e9ac-130">int</span><span class="sxs-lookup"><span data-stu-id="9e9ac-130">int</span></span> | <span data-ttu-id="9e9ac-131">Specifies the number of milliseconds to allow between the two date times to consider the times equal (for example, to account for clock skew).</span><span class="sxs-lookup"><span data-stu-id="9e9ac-131">Specifies the number of milliseconds to allow between the two date times to consider the times equal (for example, to account for clock skew).</span></span> |

<span data-ttu-id="9e9ac-132">The **AssertDateTimeIsGreaterThan** claims transformation is always executed from a [validation technical profile](validation-technical-profile.md) that is called by a [self-asserted technical profile](self-asserted-technical-profile.md).</span><span class="sxs-lookup"><span data-stu-id="9e9ac-132">The **AssertDateTimeIsGreaterThan** claims transformation is always executed from a [validation technical profile](validation-technical-profile.md) that is called by a [self-asserted technical profile](self-asserted-technical-profile.md).</span></span> <span data-ttu-id="9e9ac-133">The **DateTimeGreaterThan** self-asserted technical profile metadata controls the error message that the technical profile presents to the user.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-133">The **DateTimeGreaterThan** self-asserted technical profile metadata controls the error message that the technical profile presents to the user.</span></span>

![AssertStringClaimsAreEqual execution](./media/date-transformations/assert-execution.png)

<span data-ttu-id="9e9ac-135">The following example compares the `currentDateTime` claim with the `approvedDateTime` claim.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-135">The following example compares the `currentDateTime` claim with the `approvedDateTime` claim.</span></span> <span data-ttu-id="9e9ac-136">An error is thrown if `currentDateTime` is greater than  `approvedDateTime`.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-136">An error is thrown if `currentDateTime` is greater than  `approvedDateTime`.</span></span> <span data-ttu-id="9e9ac-137">The transformation treats values as equal if they are within 5 minutes (30000 milliseconds) difference.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-137">The transformation treats values as equal if they are within 5 minutes (30000 milliseconds) difference.</span></span>

```XML
<ClaimsTransformation Id="AssertApprovedDateTimeLaterThanCurrentDateTime" TransformationMethod="AssertDateTimeIsGreaterThan">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="approvedDateTime" TransformationClaimType="leftOperand" />
    <InputClaim ClaimTypeReferenceId="currentDateTime" TransformationClaimType="rightOperand" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="AssertIfEqualTo" DataType="boolean" Value="false" />
    <InputParameter Id="AssertIfRightOperandIsNotPresent" DataType="boolean" Value="true" />
    <InputParameter Id="TreatAsEqualIfWithinMillseconds" DataType="int" Value="300000" />
  </InputParameters>
</ClaimsTransformation>
```

<span data-ttu-id="9e9ac-138">The `login-NonInteractive` validation technical profile calls the `AssertApprovedDateTimeLaterThanCurrentDateTime` claims transformation.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-138">The `login-NonInteractive` validation technical profile calls the `AssertApprovedDateTimeLaterThanCurrentDateTime` claims transformation.</span></span>
```XML
<TechnicalProfile Id="login-NonInteractive">
  ...
  <OutputClaimsTransformations>
    <OutputClaimsTransformation ReferenceId="AssertApprovedDateTimeLaterThanCurrentDateTime" />
  </OutputClaimsTransformations>
</TechnicalProfile>
```

<span data-ttu-id="9e9ac-139">The self-asserted technical profile calls the validation **login-NonInteractive** technical profile.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-139">The self-asserted technical profile calls the validation **login-NonInteractive** technical profile.</span></span>

```XML
<TechnicalProfile Id="SelfAsserted-LocalAccountSignin-Email">
  <Metadata>
    <Item Key="DateTimeGreaterThan">Custom error message if the provided left operand is greater than the right operand.</Item>
  </Metadata>
  <ValidationTechnicalProfiles>
    <ValidationTechnicalProfile ReferenceId="login-NonInteractive" />
  </ValidationTechnicalProfiles>
</TechnicalProfile>
```

### <a name="example"></a><span data-ttu-id="9e9ac-140">Example</span><span class="sxs-lookup"><span data-stu-id="9e9ac-140">Example</span></span>

- <span data-ttu-id="9e9ac-141">Input claims:</span><span class="sxs-lookup"><span data-stu-id="9e9ac-141">Input claims:</span></span>
    - <span data-ttu-id="9e9ac-142">**leftOperand**: 2018-10-01T15:00:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="9e9ac-142">**leftOperand**: 2018-10-01T15:00:00.0000000Z</span></span>
    - <span data-ttu-id="9e9ac-143">**rightOperand**: 2018-10-01T14:00:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="9e9ac-143">**rightOperand**: 2018-10-01T14:00:00.0000000Z</span></span>
- <span data-ttu-id="9e9ac-144">Result: Error thrown</span><span class="sxs-lookup"><span data-stu-id="9e9ac-144">Result: Error thrown</span></span>


## <a name="convertdatetodatetimeclaim"></a><span data-ttu-id="9e9ac-145">ConvertDateToDateTimeClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-145">ConvertDateToDateTimeClaim</span></span>

<span data-ttu-id="9e9ac-146">Converts a **Date** ClaimType to a **DateTime** ClaimTpye.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-146">Converts a **Date** ClaimType to a **DateTime** ClaimTpye.</span></span> <span data-ttu-id="9e9ac-147">The claims transformation converts the time format and adds 12:00:00 AM to the date.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-147">The claims transformation converts the time format and adds 12:00:00 AM to the date.</span></span>

| <span data-ttu-id="9e9ac-148">Item</span><span class="sxs-lookup"><span data-stu-id="9e9ac-148">Item</span></span> | <span data-ttu-id="9e9ac-149">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="9e9ac-149">TransformationClaimType</span></span> | <span data-ttu-id="9e9ac-150">Data Type</span><span class="sxs-lookup"><span data-stu-id="9e9ac-150">Data Type</span></span> | <span data-ttu-id="9e9ac-151">Notes</span><span class="sxs-lookup"><span data-stu-id="9e9ac-151">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="9e9ac-152">InputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-152">InputClaim</span></span> | <span data-ttu-id="9e9ac-153">inputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-153">inputClaim</span></span> | <span data-ttu-id="9e9ac-154">date</span><span class="sxs-lookup"><span data-stu-id="9e9ac-154">date</span></span> | <span data-ttu-id="9e9ac-155">The ClaimType to be converted.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-155">The ClaimType to be converted.</span></span> |
| <span data-ttu-id="9e9ac-156">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-156">OutputClaim</span></span> | <span data-ttu-id="9e9ac-157">outputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-157">outputClaim</span></span> | <span data-ttu-id="9e9ac-158">dateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-158">dateTime</span></span> | <span data-ttu-id="9e9ac-159">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-159">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span></span> |

<span data-ttu-id="9e9ac-160">The following example demonstrates the conversion of the claim `dateOfBirth` (date data type) to another claim `dateOfBirthWithTime` (dateTime data type).</span><span class="sxs-lookup"><span data-stu-id="9e9ac-160">The following example demonstrates the conversion of the claim `dateOfBirth` (date data type) to another claim `dateOfBirthWithTime` (dateTime data type).</span></span>

```XML
<ClaimsTransformation Id="ConvertToDateTime" TransformationMethod="ConvertDateToDateTimeClaim">
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="dateOfBirth" TransformationClaimType="inputClaim" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="dateOfBirthWithTime" TransformationClaimType="outputClaim" />
    </OutputClaims>
  </ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="9e9ac-161">Example</span><span class="sxs-lookup"><span data-stu-id="9e9ac-161">Example</span></span>

- <span data-ttu-id="9e9ac-162">Input claims:</span><span class="sxs-lookup"><span data-stu-id="9e9ac-162">Input claims:</span></span>
    - <span data-ttu-id="9e9ac-163">**inputClaim**: 2019-06-01</span><span class="sxs-lookup"><span data-stu-id="9e9ac-163">**inputClaim**: 2019-06-01</span></span>
- <span data-ttu-id="9e9ac-164">Output claims:</span><span class="sxs-lookup"><span data-stu-id="9e9ac-164">Output claims:</span></span>
    - <span data-ttu-id="9e9ac-165">**outputClaim**: 1559347200 (June 1, 2019 12:00:00 AM)</span><span class="sxs-lookup"><span data-stu-id="9e9ac-165">**outputClaim**: 1559347200 (June 1, 2019 12:00:00 AM)</span></span>

## <a name="getcurrentdatetime"></a><span data-ttu-id="9e9ac-166">GetCurrentDateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-166">GetCurrentDateTime</span></span>

<span data-ttu-id="9e9ac-167">Get the current UTC date and time and add the value to a ClaimType.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-167">Get the current UTC date and time and add the value to a ClaimType.</span></span>

| <span data-ttu-id="9e9ac-168">Item</span><span class="sxs-lookup"><span data-stu-id="9e9ac-168">Item</span></span> | <span data-ttu-id="9e9ac-169">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="9e9ac-169">TransformationClaimType</span></span> | <span data-ttu-id="9e9ac-170">Data Type</span><span class="sxs-lookup"><span data-stu-id="9e9ac-170">Data Type</span></span> | <span data-ttu-id="9e9ac-171">Notes</span><span class="sxs-lookup"><span data-stu-id="9e9ac-171">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="9e9ac-172">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-172">OutputClaim</span></span> | <span data-ttu-id="9e9ac-173">currentDateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-173">currentDateTime</span></span> | <span data-ttu-id="9e9ac-174">dateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-174">dateTime</span></span> | <span data-ttu-id="9e9ac-175">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-175">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span></span> |

```XML
<ClaimsTransformation Id="GetSystemDateTime" TransformationMethod="GetCurrentDateTime">
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="systemDateTime" TransformationClaimType="currentDateTime" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="9e9ac-176">Example</span><span class="sxs-lookup"><span data-stu-id="9e9ac-176">Example</span></span>

* <span data-ttu-id="9e9ac-177">Output claims:</span><span class="sxs-lookup"><span data-stu-id="9e9ac-177">Output claims:</span></span>
    * <span data-ttu-id="9e9ac-178">**currentDateTime**: 1534418820 (August 16, 2018 11:27:00 AM)</span><span class="sxs-lookup"><span data-stu-id="9e9ac-178">**currentDateTime**: 1534418820 (August 16, 2018 11:27:00 AM)</span></span>

## <a name="datetimecomparison"></a><span data-ttu-id="9e9ac-179">DateTimeComparison</span><span class="sxs-lookup"><span data-stu-id="9e9ac-179">DateTimeComparison</span></span>

<span data-ttu-id="9e9ac-180">Determine whether one dateTime is greater, lesser, or equal to another.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-180">Determine whether one dateTime is greater, lesser, or equal to another.</span></span> <span data-ttu-id="9e9ac-181">The result is a new boolean ClaimType boolean with a value of true or false.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-181">The result is a new boolean ClaimType boolean with a value of true or false.</span></span>

| <span data-ttu-id="9e9ac-182">Item</span><span class="sxs-lookup"><span data-stu-id="9e9ac-182">Item</span></span> | <span data-ttu-id="9e9ac-183">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="9e9ac-183">TransformationClaimType</span></span> | <span data-ttu-id="9e9ac-184">Data Type</span><span class="sxs-lookup"><span data-stu-id="9e9ac-184">Data Type</span></span> | <span data-ttu-id="9e9ac-185">Notes</span><span class="sxs-lookup"><span data-stu-id="9e9ac-185">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="9e9ac-186">InputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-186">InputClaim</span></span> | <span data-ttu-id="9e9ac-187">firstDateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-187">firstDateTime</span></span> | <span data-ttu-id="9e9ac-188">dateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-188">dateTime</span></span> | <span data-ttu-id="9e9ac-189">The first dateTime to compare.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-189">The first dateTime to compare.</span></span> <span data-ttu-id="9e9ac-190">Null value throws an exception.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-190">Null value throws an exception.</span></span> |
| <span data-ttu-id="9e9ac-191">InputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-191">InputClaim</span></span> | <span data-ttu-id="9e9ac-192">secondDateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-192">secondDateTime</span></span> | <span data-ttu-id="9e9ac-193">dateTime</span><span class="sxs-lookup"><span data-stu-id="9e9ac-193">dateTime</span></span> | <span data-ttu-id="9e9ac-194">The second dateTime to complete.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-194">The second dateTime to complete.</span></span> <span data-ttu-id="9e9ac-195">Null value treats as current datetTime.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-195">Null value treats as current datetTime.</span></span> |
| <span data-ttu-id="9e9ac-196">InputParameter</span><span class="sxs-lookup"><span data-stu-id="9e9ac-196">InputParameter</span></span> | <span data-ttu-id="9e9ac-197">operator</span><span class="sxs-lookup"><span data-stu-id="9e9ac-197">operator</span></span> | <span data-ttu-id="9e9ac-198">string</span><span class="sxs-lookup"><span data-stu-id="9e9ac-198">string</span></span> | <span data-ttu-id="9e9ac-199">One of following values: same, later than, or earlier than.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-199">One of following values: same, later than, or earlier than.</span></span> |
| <span data-ttu-id="9e9ac-200">InputParameter</span><span class="sxs-lookup"><span data-stu-id="9e9ac-200">InputParameter</span></span> | <span data-ttu-id="9e9ac-201">timeSpanInSeconds</span><span class="sxs-lookup"><span data-stu-id="9e9ac-201">timeSpanInSeconds</span></span> | <span data-ttu-id="9e9ac-202">int</span><span class="sxs-lookup"><span data-stu-id="9e9ac-202">int</span></span> | <span data-ttu-id="9e9ac-203">Add the timespan to the first datetime.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-203">Add the timespan to the first datetime.</span></span> |
| <span data-ttu-id="9e9ac-204">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="9e9ac-204">OutputClaim</span></span> | <span data-ttu-id="9e9ac-205">result</span><span class="sxs-lookup"><span data-stu-id="9e9ac-205">result</span></span> | <span data-ttu-id="9e9ac-206">boolean</span><span class="sxs-lookup"><span data-stu-id="9e9ac-206">boolean</span></span> | <span data-ttu-id="9e9ac-207">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-207">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span></span> |

<span data-ttu-id="9e9ac-208">Use this claims transformation to determine if two ClaimTypes are  equal, greater, or lesser from each other.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-208">Use this claims transformation to determine if two ClaimTypes are  equal, greater, or lesser from each other.</span></span> <span data-ttu-id="9e9ac-209">For example, you may store the last time a user accepted your terms of services (TOS).</span><span class="sxs-lookup"><span data-stu-id="9e9ac-209">For example, you may store the last time a user accepted your terms of services (TOS).</span></span> <span data-ttu-id="9e9ac-210">After 3 months, you can ask the user to access the TOS again.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-210">After 3 months, you can ask the user to access the TOS again.</span></span>
<span data-ttu-id="9e9ac-211">To run the claim transformation, you first need to get the current dateTime and also the last time user accepts the TOS.</span><span class="sxs-lookup"><span data-stu-id="9e9ac-211">To run the claim transformation, you first need to get the current dateTime and also the last time user accepts the TOS.</span></span>

```XML
<ClaimsTransformation Id="CompareLastTOSAcceptedWithCurrentDateTime" TransformationMethod="DateTimeComparison">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="currentDateTime" TransformationClaimType="firstDateTime" />
    <InputClaim ClaimTypeReferenceId="extension_LastTOSAccepted" TransformationClaimType="secondDateTime" />
  </InputClaims>
  <InputParameters>
    <InputParameter Id="operator" DataType="string" Value="greater than" />
    <InputParameter Id="timeSpanInSeconds" DataType="int" Value="7776000" />
  </InputParameters>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="isLastTOSAcceptedGreaterThanNow" TransformationClaimType="result" />
  </OutputClaims>      
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="9e9ac-212">Example</span><span class="sxs-lookup"><span data-stu-id="9e9ac-212">Example</span></span>

- <span data-ttu-id="9e9ac-213">Input claims:</span><span class="sxs-lookup"><span data-stu-id="9e9ac-213">Input claims:</span></span>
    - <span data-ttu-id="9e9ac-214">**firstDateTime**: 2018-01-01T00:00:00.100000Z</span><span class="sxs-lookup"><span data-stu-id="9e9ac-214">**firstDateTime**: 2018-01-01T00:00:00.100000Z</span></span>
    - <span data-ttu-id="9e9ac-215">**secondDateTime**: 2018-04-01T00:00:00.100000Z</span><span class="sxs-lookup"><span data-stu-id="9e9ac-215">**secondDateTime**: 2018-04-01T00:00:00.100000Z</span></span>
- <span data-ttu-id="9e9ac-216">Input parameters:</span><span class="sxs-lookup"><span data-stu-id="9e9ac-216">Input parameters:</span></span>
    - <span data-ttu-id="9e9ac-217">**operator**: greater than</span><span class="sxs-lookup"><span data-stu-id="9e9ac-217">**operator**: greater than</span></span>
    - <span data-ttu-id="9e9ac-218">**timeSpanInSeconds**: 7776000 (90 days)</span><span class="sxs-lookup"><span data-stu-id="9e9ac-218">**timeSpanInSeconds**: 7776000 (90 days)</span></span>
- <span data-ttu-id="9e9ac-219">Output claims:</span><span class="sxs-lookup"><span data-stu-id="9e9ac-219">Output claims:</span></span> 
    - <span data-ttu-id="9e9ac-220">**result**: true</span><span class="sxs-lookup"><span data-stu-id="9e9ac-220">**result**: true</span></span>

