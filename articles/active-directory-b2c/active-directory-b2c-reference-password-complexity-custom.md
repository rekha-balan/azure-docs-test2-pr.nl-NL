---
title: Password complexity in custom policies in Azure Active Directory B2C | Microsoft Docs
description: How to configure complexity requirements for passwords in Custom Policy.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/16/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: ed0001d8d88a2604e3128a4d5f7a365aeb7b00b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965724"
---
# <a name="configure-password-complexity-in-custom-policies"></a><span data-ttu-id="7a26e-103">Configure password complexity in custom policies</span><span class="sxs-lookup"><span data-stu-id="7a26e-103">Configure password complexity in custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7a26e-104">This article is an advanced description of how password complexity works and is enabled using Azure AD B2C custom policies.</span><span class="sxs-lookup"><span data-stu-id="7a26e-104">This article is an advanced description of how password complexity works and is enabled using Azure AD B2C custom policies.</span></span>

## <a name="azure-ad-b2c-configure-complexity-requirements-for-passwords"></a><span data-ttu-id="7a26e-105">Azure AD B2C: Configure complexity requirements for passwords</span><span class="sxs-lookup"><span data-stu-id="7a26e-105">Azure AD B2C: Configure complexity requirements for passwords</span></span>

<span data-ttu-id="7a26e-106">Azure Active Directory B2C (Azure AD B2C) supports changing the complexity requirements for passwords supplied by an end user when creating an account.</span><span class="sxs-lookup"><span data-stu-id="7a26e-106">Azure Active Directory B2C (Azure AD B2C) supports changing the complexity requirements for passwords supplied by an end user when creating an account.</span></span>  <span data-ttu-id="7a26e-107">By default, Azure AD B2C uses **Strong** passwords.</span><span class="sxs-lookup"><span data-stu-id="7a26e-107">By default, Azure AD B2C uses **Strong** passwords.</span></span>  <span data-ttu-id="7a26e-108">Azure AD B2C also supports configuration options to control the complexity of passwords that customers can use.</span><span class="sxs-lookup"><span data-stu-id="7a26e-108">Azure AD B2C also supports configuration options to control the complexity of passwords that customers can use.</span></span>  <span data-ttu-id="7a26e-109">This article talks about how to do configure password complexity in custom policies.</span><span class="sxs-lookup"><span data-stu-id="7a26e-109">This article talks about how to do configure password complexity in custom policies.</span></span>  <span data-ttu-id="7a26e-110">It is also possible to use [configure password complexity in built-in policies](active-directory-b2c-reference-password-complexity.md).</span><span class="sxs-lookup"><span data-stu-id="7a26e-110">It is also possible to use [configure password complexity in built-in policies](active-directory-b2c-reference-password-complexity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a26e-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a26e-111">Prerequisites</span></span>

<span data-ttu-id="7a26e-112">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7a26e-112">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="how-to-configure-password-complexity-in-custom-policy"></a><span data-ttu-id="7a26e-113">How to configure password complexity in custom policy</span><span class="sxs-lookup"><span data-stu-id="7a26e-113">How to configure password complexity in custom policy</span></span>

<span data-ttu-id="7a26e-114">To configure password complexity in custom policy, the overall structure of your custom policy must include a `ClaimsSchema`, `Predicates`, and `InputValidations` element inside `BuildingBlocks`.</span><span class="sxs-lookup"><span data-stu-id="7a26e-114">To configure password complexity in custom policy, the overall structure of your custom policy must include a `ClaimsSchema`, `Predicates`, and `InputValidations` element inside `BuildingBlocks`.</span></span>

```XML
  <BuildingBlocks>
    <ClaimsSchema>...</ClaimsSchema>
    <Predicates>...</Predicates>
    <InputValidations>...</InputValidations>
  </BuildingBlocks>
```

<span data-ttu-id="7a26e-115">The purpose of these elements is as follows:</span><span class="sxs-lookup"><span data-stu-id="7a26e-115">The purpose of these elements is as follows:</span></span>

- <span data-ttu-id="7a26e-116">Each `Predicate` element defines a basic string validation check that returns true or false.</span><span class="sxs-lookup"><span data-stu-id="7a26e-116">Each `Predicate` element defines a basic string validation check that returns true or false.</span></span>
- <span data-ttu-id="7a26e-117">The `InputValidations` element has one or more `InputValidation` elements.</span><span class="sxs-lookup"><span data-stu-id="7a26e-117">The `InputValidations` element has one or more `InputValidation` elements.</span></span>  <span data-ttu-id="7a26e-118">Each `InputValidation` is constructed by using a series of `Predicate` elements.</span><span class="sxs-lookup"><span data-stu-id="7a26e-118">Each `InputValidation` is constructed by using a series of `Predicate` elements.</span></span> <span data-ttu-id="7a26e-119">This element allows you to perform boolean aggregations (similar to `and` and `or`).</span><span class="sxs-lookup"><span data-stu-id="7a26e-119">This element allows you to perform boolean aggregations (similar to `and` and `or`).</span></span>
- <span data-ttu-id="7a26e-120">The `ClaimsSchema` defines which claim is being validated.</span><span class="sxs-lookup"><span data-stu-id="7a26e-120">The `ClaimsSchema` defines which claim is being validated.</span></span>  <span data-ttu-id="7a26e-121">It then defines which `InputValidation` rule is used to validate that claim.</span><span class="sxs-lookup"><span data-stu-id="7a26e-121">It then defines which `InputValidation` rule is used to validate that claim.</span></span>

### <a name="defining-a-predicate-element"></a><span data-ttu-id="7a26e-122">Defining a predicate element</span><span class="sxs-lookup"><span data-stu-id="7a26e-122">Defining a predicate element</span></span>

<span data-ttu-id="7a26e-123">Predicates have two method types: IsLengthRange or MatchesRegex.</span><span class="sxs-lookup"><span data-stu-id="7a26e-123">Predicates have two method types: IsLengthRange or MatchesRegex.</span></span> <span data-ttu-id="7a26e-124">Let's review an example of each.</span><span class="sxs-lookup"><span data-stu-id="7a26e-124">Let's review an example of each.</span></span>  <span data-ttu-id="7a26e-125">First we have an example of MatchesRegex, which is used to match a regular expression.</span><span class="sxs-lookup"><span data-stu-id="7a26e-125">First we have an example of MatchesRegex, which is used to match a regular expression.</span></span>  <span data-ttu-id="7a26e-126">In this example, it matches string that contains numbers.</span><span class="sxs-lookup"><span data-stu-id="7a26e-126">In this example, it matches string that contains numbers.</span></span>

```XML
      <Predicate Id="PIN" Method="MatchesRegex" HelpText="The password must be a pin.">
        <Parameters>
          <Parameter Id="RegularExpression">^[0-9]+$</Parameter>
        </Parameters>
      </Predicate>
```

<span data-ttu-id="7a26e-127">Next let's review an example of IsLengthRange.</span><span class="sxs-lookup"><span data-stu-id="7a26e-127">Next let's review an example of IsLengthRange.</span></span>  <span data-ttu-id="7a26e-128">This method takes a minimum and maximum string length.</span><span class="sxs-lookup"><span data-stu-id="7a26e-128">This method takes a minimum and maximum string length.</span></span>

```XML
      <Predicate Id="Length" Method="IsLengthRange" HelpText="The password must be between 8 and 16 characters.">
        <Parameters>
          <Parameter Id="Minimum">8</Parameter>
          <Parameter Id="Maximum">16</Parameter>
        </Parameters>
      </Predicate>
```

<span data-ttu-id="7a26e-129">Use the `HelpText` attribute to provide an error message for end users if the check fails.</span><span class="sxs-lookup"><span data-stu-id="7a26e-129">Use the `HelpText` attribute to provide an error message for end users if the check fails.</span></span>  <span data-ttu-id="7a26e-130">This string can be localized using the [language customization feature](active-directory-b2c-reference-language-customization.md).</span><span class="sxs-lookup"><span data-stu-id="7a26e-130">This string can be localized using the [language customization feature](active-directory-b2c-reference-language-customization.md).</span></span>

### <a name="defining-an-inputvalidation-element"></a><span data-ttu-id="7a26e-131">Defining an InputValidation element</span><span class="sxs-lookup"><span data-stu-id="7a26e-131">Defining an InputValidation element</span></span>

<span data-ttu-id="7a26e-132">An `InputValidation` is an aggregation of `PredicateReferences`.</span><span class="sxs-lookup"><span data-stu-id="7a26e-132">An `InputValidation` is an aggregation of `PredicateReferences`.</span></span> <span data-ttu-id="7a26e-133">Each `PredicateReferences` must be true in order for the `InputValidation` to succeed.</span><span class="sxs-lookup"><span data-stu-id="7a26e-133">Each `PredicateReferences` must be true in order for the `InputValidation` to succeed.</span></span>  <span data-ttu-id="7a26e-134">However, inside the `PredicateReferences` element use an attribute called `MatchAtLeast` to specify how many `PredicateReference` checks must return true.</span><span class="sxs-lookup"><span data-stu-id="7a26e-134">However, inside the `PredicateReferences` element use an attribute called `MatchAtLeast` to specify how many `PredicateReference` checks must return true.</span></span>  <span data-ttu-id="7a26e-135">Optionally, define a `HelpText` attribute to override the error message defined in the `Predicate` elements that it references.</span><span class="sxs-lookup"><span data-stu-id="7a26e-135">Optionally, define a `HelpText` attribute to override the error message defined in the `Predicate` elements that it references.</span></span>

```XML
      <InputValidation Id="PasswordValidation">
        <PredicateReferences Id="LengthGroup" MatchAtLeast="1">
          <PredicateReference Id="Length" />
        </PredicateReferences>
        <PredicateReferences Id="3of4" MatchAtLeast="3" HelpText="You must have at least 3 of the following character classes:">
          <PredicateReference Id="Lowercase" />
          <PredicateReference Id="Uppercase" />
          <PredicateReference Id="Number" />
          <PredicateReference Id="Symbol" />
        </PredicateReferences>
      </InputValidation>
```

### <a name="defining-a-claimsschema-element"></a><span data-ttu-id="7a26e-136">Defining a ClaimsSchema element</span><span class="sxs-lookup"><span data-stu-id="7a26e-136">Defining a ClaimsSchema element</span></span>

<span data-ttu-id="7a26e-137">The claim types `newPassword` and `reenterPassword` are considered special, so do not change the names.</span><span class="sxs-lookup"><span data-stu-id="7a26e-137">The claim types `newPassword` and `reenterPassword` are considered special, so do not change the names.</span></span>  <span data-ttu-id="7a26e-138">The UI validates the user correctly reentered their password during account creation based on these `ClaimType` elements.</span><span class="sxs-lookup"><span data-stu-id="7a26e-138">The UI validates the user correctly reentered their password during account creation based on these `ClaimType` elements.</span></span>  <span data-ttu-id="7a26e-139">To find the same `ClaimType` elements, look in the TrustFrameworkBase.xml in your starter pack.</span><span class="sxs-lookup"><span data-stu-id="7a26e-139">To find the same `ClaimType` elements, look in the TrustFrameworkBase.xml in your starter pack.</span></span>  <span data-ttu-id="7a26e-140">What's new in this example is that we are overriding these elements to define a `InputValidationReference`.</span><span class="sxs-lookup"><span data-stu-id="7a26e-140">What's new in this example is that we are overriding these elements to define a `InputValidationReference`.</span></span> <span data-ttu-id="7a26e-141">The `ID` attribute of this new element is pointing to the `InputValidation` element that we defined.</span><span class="sxs-lookup"><span data-stu-id="7a26e-141">The `ID` attribute of this new element is pointing to the `InputValidation` element that we defined.</span></span>

```XML
    <ClaimsSchema>
      <ClaimType Id="newPassword">
        <InputValidationReference Id="PasswordValidation" />
      </ClaimType>
      <ClaimType Id="reenterPassword">
        <InputValidationReference Id="PasswordValidation" />
      </ClaimType>
    </ClaimsSchema>
```

### <a name="putting-it-all-together"></a><span data-ttu-id="7a26e-142">Putting it all together</span><span class="sxs-lookup"><span data-stu-id="7a26e-142">Putting it all together</span></span>

<span data-ttu-id="7a26e-143">This example shows how all the pieces fit together to form a working policy.</span><span class="sxs-lookup"><span data-stu-id="7a26e-143">This example shows how all the pieces fit together to form a working policy.</span></span>  <span data-ttu-id="7a26e-144">To use this example:</span><span class="sxs-lookup"><span data-stu-id="7a26e-144">To use this example:</span></span>

1. <span data-ttu-id="7a26e-145">Follow the instructions in the pre-requisite [Getting started](active-directory-b2c-get-started-custom.md) to download, configure, and upload TrustFrameworkBase.xml and TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="7a26e-145">Follow the instructions in the pre-requisite [Getting started](active-directory-b2c-get-started-custom.md) to download, configure, and upload TrustFrameworkBase.xml and TrustFrameworkExtensions.xml</span></span>
1. <span data-ttu-id="7a26e-146">Create a SignUporSignIn.xml file using the example content in this section.</span><span class="sxs-lookup"><span data-stu-id="7a26e-146">Create a SignUporSignIn.xml file using the example content in this section.</span></span>
1. <span data-ttu-id="7a26e-147">Update SignUporSignIn.xml replacing `yourtenant` with your Azure AD B2C tenant name.</span><span class="sxs-lookup"><span data-stu-id="7a26e-147">Update SignUporSignIn.xml replacing `yourtenant` with your Azure AD B2C tenant name.</span></span>
1. <span data-ttu-id="7a26e-148">Upload the SignUporSignIn.xml policy file last.</span><span class="sxs-lookup"><span data-stu-id="7a26e-148">Upload the SignUporSignIn.xml policy file last.</span></span>

<span data-ttu-id="7a26e-149">This example contains a validation for pin passwords and one for strong passwords:</span><span class="sxs-lookup"><span data-stu-id="7a26e-149">This example contains a validation for pin passwords and one for strong passwords:</span></span>

- <span data-ttu-id="7a26e-150">Look for `PINpassword`.</span><span class="sxs-lookup"><span data-stu-id="7a26e-150">Look for `PINpassword`.</span></span> <span data-ttu-id="7a26e-151">This `InputValidation` element validates a pin of any length.</span><span class="sxs-lookup"><span data-stu-id="7a26e-151">This `InputValidation` element validates a pin of any length.</span></span>  <span data-ttu-id="7a26e-152">It is not used at the moment, because it is not referenced in the `InputValidationReference` element inside `ClaimType`.</span><span class="sxs-lookup"><span data-stu-id="7a26e-152">It is not used at the moment, because it is not referenced in the `InputValidationReference` element inside `ClaimType`.</span></span> 
- <span data-ttu-id="7a26e-153">Look for `PasswordValidation`.</span><span class="sxs-lookup"><span data-stu-id="7a26e-153">Look for `PasswordValidation`.</span></span> <span data-ttu-id="7a26e-154">This `InputValidation` element validates a password is 8 to 16 characters and contains 3 of 4 of numbers, uppercase, lowercase, or symbols.</span><span class="sxs-lookup"><span data-stu-id="7a26e-154">This `InputValidation` element validates a password is 8 to 16 characters and contains 3 of 4 of numbers, uppercase, lowercase, or symbols.</span></span>  <span data-ttu-id="7a26e-155">It is referenced in `ClaimType`.</span><span class="sxs-lookup"><span data-stu-id="7a26e-155">It is referenced in `ClaimType`.</span></span>  <span data-ttu-id="7a26e-156">Therefore, this rule is being enforced in this policy.</span><span class="sxs-lookup"><span data-stu-id="7a26e-156">Therefore, this rule is being enforced in this policy.</span></span>

```XML
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<TrustFrameworkPolicy
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
  PolicySchemaVersion="0.3.0.0"
  TenantId="yourtenant.onmicrosoft.com"
  PolicyId="B2C_1A_signup_signin"
  PublicPolicyUri="http://yourtenant.onmicrosoft.com/B2C_1A_signup_signin">
 <BasePolicy>
    <TenantId>yourtenant.onmicrosoft.com</TenantId>
    <PolicyId>B2C_1A_TrustFrameworkExtensions</PolicyId>
  </BasePolicy>
  <BuildingBlocks>
    <ClaimsSchema>
      <ClaimType Id="newPassword">
        <InputValidationReference Id="PasswordValidation" />
      </ClaimType>
      <ClaimType Id="reenterPassword">
        <InputValidationReference Id="PasswordValidation" />
      </ClaimType>
    </ClaimsSchema>
    <Predicates>
      <Predicate Id="Lowercase" Method="MatchesRegex" HelpText="a lowercase">
        <Parameters>
          <Parameter Id="RegularExpression">[a-z]+</Parameter>
        </Parameters>
      </Predicate>
      <Predicate Id="Uppercase" Method="MatchesRegex" HelpText="an uppercase">
        <Parameters>
          <Parameter Id="RegularExpression">[A-Z]+</Parameter>
        </Parameters>
      </Predicate>
      <Predicate Id="Number" Method="MatchesRegex" HelpText="a number">
        <Parameters>
          <Parameter Id="RegularExpression">[0-9]+</Parameter>
        </Parameters>
      </Predicate>
      <Predicate Id="Symbol" Method="MatchesRegex" HelpText="a symbol">
        <Parameters>
          <Parameter Id="RegularExpression">[!@#$%^*()]+</Parameter>
        </Parameters>
      </Predicate>
      <Predicate Id="Length" Method="IsLengthRange" HelpText="The password must be between 8 and 16 characters.">
        <Parameters>
          <Parameter Id="Minimum">8</Parameter>
          <Parameter Id="Maximum">16</Parameter>
        </Parameters>
      </Predicate>
      <Predicate Id="PIN" Method="MatchesRegex" HelpText="The password must be a pin.">
        <Parameters>
          <Parameter Id="RegularExpression">^[0-9]+$</Parameter>
        </Parameters>
      </Predicate>
    </Predicates>
    <InputValidations>
      <InputValidation Id="PasswordValidation">
        <PredicateReferences Id="LengthGroup" MatchAtLeast="1">
          <PredicateReference Id="Length" />
        </PredicateReferences>
        <PredicateReferences Id="3of4" MatchAtLeast="3" HelpText="You must have at least 3 of the following character classes:">
          <PredicateReference Id="Lowercase" />
          <PredicateReference Id="Uppercase" />
          <PredicateReference Id="Number" />
          <PredicateReference Id="Symbol" />
        </PredicateReferences>
      </InputValidation>
      <InputValidation Id="PINpassword">
        <PredicateReferences Id="PINGroup">
          <PredicateReference Id="PIN" />
        </PredicateReferences>
      </InputValidation>
    </InputValidations>
  </BuildingBlocks>
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration, DisableStrongPassword" />
      </InputClaims>
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
</TrustFrameworkPolicy>
```
