---
title: TrustFrameworkPolicy - Azure Active Directory B2C | Microsoft Docs
description: Specify the TrustFrameworkPolicy element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 16e98811b65e215d8688e030ea8dcbb1f9446a5b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869121"
---
# <a name="trustframeworkpolicy"></a><span data-ttu-id="27b81-103">TrustFrameworkPolicy</span><span class="sxs-lookup"><span data-stu-id="27b81-103">TrustFrameworkPolicy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="27b81-104">A custom policy is represented as one or more XML-formatted files, which refer to each other in a hierarchical chain.</span><span class="sxs-lookup"><span data-stu-id="27b81-104">A custom policy is represented as one or more XML-formatted files, which refer to each other in a hierarchical chain.</span></span> <span data-ttu-id="27b81-105">The XML elements define elements of the policy, such as the claims schema, claims transformations, content definitions, claims providers, technical profiles, user journey, and orchestration steps.</span><span class="sxs-lookup"><span data-stu-id="27b81-105">The XML elements define elements of the policy, such as the claims schema, claims transformations, content definitions, claims providers, technical profiles, user journey, and orchestration steps.</span></span> <span data-ttu-id="27b81-106">Each policy file is defined within the top-level **TrustFrameworkPolicy** element of a policy file.</span><span class="sxs-lookup"><span data-stu-id="27b81-106">Each policy file is defined within the top-level **TrustFrameworkPolicy** element of a policy file.</span></span> 

```XML
<TrustFrameworkPolicy
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
  PolicySchemaVersion="0.3.0.0"
  TenantId="mytenant.onmicrosoft.com"
  PolicyId="B2C_1A_TrustFrameworkBase"
  PublicPolicyUri="http://mytenant.onmicrosoft.com/B2C_1A_TrustFrameworkBase">
  ...
```


<span data-ttu-id="27b81-107">The **TrustFrameworkPolicy** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="27b81-107">The **TrustFrameworkPolicy** element contains the following attributes:</span></span>

| <span data-ttu-id="27b81-108">Attribute</span><span class="sxs-lookup"><span data-stu-id="27b81-108">Attribute</span></span> | <span data-ttu-id="27b81-109">Required</span><span class="sxs-lookup"><span data-stu-id="27b81-109">Required</span></span> | <span data-ttu-id="27b81-110">Description</span><span class="sxs-lookup"><span data-stu-id="27b81-110">Description</span></span> |
|---------- | -------- | ----------- |
| <span data-ttu-id="27b81-111">PolicySchemaVersion</span><span class="sxs-lookup"><span data-stu-id="27b81-111">PolicySchemaVersion</span></span> | <span data-ttu-id="27b81-112">Yes</span><span class="sxs-lookup"><span data-stu-id="27b81-112">Yes</span></span> | <span data-ttu-id="27b81-113">The schema version that is to be used to execute the policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-113">The schema version that is to be used to execute the policy.</span></span> <span data-ttu-id="27b81-114">The value must be `0.3.0.0`</span><span class="sxs-lookup"><span data-stu-id="27b81-114">The value must be `0.3.0.0`</span></span> |
| <span data-ttu-id="27b81-115">TenantObjectId</span><span class="sxs-lookup"><span data-stu-id="27b81-115">TenantObjectId</span></span> | <span data-ttu-id="27b81-116">No</span><span class="sxs-lookup"><span data-stu-id="27b81-116">No</span></span> | <span data-ttu-id="27b81-117">The unique object identifier of the Azure Active Directory (Azure AD) B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="27b81-117">The unique object identifier of the Azure Active Directory (Azure AD) B2C tenant.</span></span> |
| <span data-ttu-id="27b81-118">TenantId</span><span class="sxs-lookup"><span data-stu-id="27b81-118">TenantId</span></span> | <span data-ttu-id="27b81-119">Yes</span><span class="sxs-lookup"><span data-stu-id="27b81-119">Yes</span></span> | <span data-ttu-id="27b81-120">The unique identifier of the tenant to which this policy belongs.</span><span class="sxs-lookup"><span data-stu-id="27b81-120">The unique identifier of the tenant to which this policy belongs.</span></span> |
| <span data-ttu-id="27b81-121">PolicyId</span><span class="sxs-lookup"><span data-stu-id="27b81-121">PolicyId</span></span> | <span data-ttu-id="27b81-122">Yes</span><span class="sxs-lookup"><span data-stu-id="27b81-122">Yes</span></span> | <span data-ttu-id="27b81-123">The unique identifier for the policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-123">The unique identifier for the policy.</span></span> <span data-ttu-id="27b81-124">This identifier must be prefixed by *B2C_1A_*</span><span class="sxs-lookup"><span data-stu-id="27b81-124">This identifier must be prefixed by *B2C_1A_*</span></span> |
| <span data-ttu-id="27b81-125">PublicPolicyUri</span><span class="sxs-lookup"><span data-stu-id="27b81-125">PublicPolicyUri</span></span> | <span data-ttu-id="27b81-126">Yes</span><span class="sxs-lookup"><span data-stu-id="27b81-126">Yes</span></span> | <span data-ttu-id="27b81-127">The URI for the policy, which is combination of the tenant ID and the policy ID.</span><span class="sxs-lookup"><span data-stu-id="27b81-127">The URI for the policy, which is combination of the tenant ID and the policy ID.</span></span> |
| <span data-ttu-id="27b81-128">DeploymentMode</span><span class="sxs-lookup"><span data-stu-id="27b81-128">DeploymentMode</span></span> | <span data-ttu-id="27b81-129">No</span><span class="sxs-lookup"><span data-stu-id="27b81-129">No</span></span> | <span data-ttu-id="27b81-130">Possible values: `Production`, `Debugging`, or `Development`.</span><span class="sxs-lookup"><span data-stu-id="27b81-130">Possible values: `Production`, `Debugging`, or `Development`.</span></span> <span data-ttu-id="27b81-131">`Production` is the default.</span><span class="sxs-lookup"><span data-stu-id="27b81-131">`Production` is the default.</span></span> <span data-ttu-id="27b81-132">Use this property to debug your policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-132">Use this property to debug your policy.</span></span> <span data-ttu-id="27b81-133">For more information, see [Collecting Logs](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="27b81-133">For more information, see [Collecting Logs](active-directory-b2c-troubleshoot-custom.md).</span></span> |
| <span data-ttu-id="27b81-134">UserJourneyRecorderEndpoint</span><span class="sxs-lookup"><span data-stu-id="27b81-134">UserJourneyRecorderEndpoint</span></span> | <span data-ttu-id="27b81-135">No</span><span class="sxs-lookup"><span data-stu-id="27b81-135">No</span></span> | <span data-ttu-id="27b81-136">The endpoint that is used when **DeploymentMode** is set to `Development`.</span><span class="sxs-lookup"><span data-stu-id="27b81-136">The endpoint that is used when **DeploymentMode** is set to `Development`.</span></span> <span data-ttu-id="27b81-137">The value must be `urn:journeyrecorder:applicationinsights`.</span><span class="sxs-lookup"><span data-stu-id="27b81-137">The value must be `urn:journeyrecorder:applicationinsights`.</span></span> <span data-ttu-id="27b81-138">For more information, see [Collecting Logs](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="27b81-138">For more information, see [Collecting Logs](active-directory-b2c-troubleshoot-custom.md).</span></span> |


<span data-ttu-id="27b81-139">The following example shows how to specify the **TrustFrameworkPolicy** element:</span><span class="sxs-lookup"><span data-stu-id="27b81-139">The following example shows how to specify the **TrustFrameworkPolicy** element:</span></span>

``` XML
<TrustFrameworkPolicy
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:xsd="http://www.w3.org/2001/XMLSchema"
   xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
   PolicySchemaVersion="0.3.0.0"
   TenantId="mytenant.onmicrosoft.com"
   PolicyId="B2C_1A_TrustFrameworkBase"
   PublicPolicyUri="http://mytenant.onmicrosoft.com/B2C_1A_TrustFrameworkBase">
```

## <a name="inheritance-model"></a><span data-ttu-id="27b81-140">Inheritance model</span><span class="sxs-lookup"><span data-stu-id="27b81-140">Inheritance model</span></span>

<span data-ttu-id="27b81-141">These types of policy files are typically used in a user journey:</span><span class="sxs-lookup"><span data-stu-id="27b81-141">These types of policy files are typically used in a user journey:</span></span>

- <span data-ttu-id="27b81-142">A **Base** file that contains most of the definitions.</span><span class="sxs-lookup"><span data-stu-id="27b81-142">A **Base** file that contains most of the definitions.</span></span> <span data-ttu-id="27b81-143">To help with troubleshooting and long-term maintenance of your policies, it is recommended that you make a minimum number of changes to this file.</span><span class="sxs-lookup"><span data-stu-id="27b81-143">To help with troubleshooting and long-term maintenance of your policies, it is recommended that you make a minimum number of changes to this file.</span></span>
- <span data-ttu-id="27b81-144">An **Extensions** file that holds the unique configuration changes for your tenant.</span><span class="sxs-lookup"><span data-stu-id="27b81-144">An **Extensions** file that holds the unique configuration changes for your tenant.</span></span> <span data-ttu-id="27b81-145">This policy file is derived from the Base file.</span><span class="sxs-lookup"><span data-stu-id="27b81-145">This policy file is derived from the Base file.</span></span> <span data-ttu-id="27b81-146">Use this file to add new functionality or override existing functionality.</span><span class="sxs-lookup"><span data-stu-id="27b81-146">Use this file to add new functionality or override existing functionality.</span></span> <span data-ttu-id="27b81-147">For example, use this file to federate with new identity providers.</span><span class="sxs-lookup"><span data-stu-id="27b81-147">For example, use this file to federate with new identity providers.</span></span>
- <span data-ttu-id="27b81-148">A **Relying Party (RP)** file that is the single task-focused file that is invoked directly by the relying party application, such as your web, mobile, or desktop applications.</span><span class="sxs-lookup"><span data-stu-id="27b81-148">A **Relying Party (RP)** file that is the single task-focused file that is invoked directly by the relying party application, such as your web, mobile, or desktop applications.</span></span> <span data-ttu-id="27b81-149">Each unique task such as sign-up or sign-in, password reset, or profile edit, requires its own RP policy file.</span><span class="sxs-lookup"><span data-stu-id="27b81-149">Each unique task such as sign-up or sign-in, password reset, or profile edit, requires its own RP policy file.</span></span> <span data-ttu-id="27b81-150">This policy file is derived from the Extensions file.</span><span class="sxs-lookup"><span data-stu-id="27b81-150">This policy file is derived from the Extensions file.</span></span> 

<span data-ttu-id="27b81-151">A relying party application calls the RP policy file to execute a specific task.</span><span class="sxs-lookup"><span data-stu-id="27b81-151">A relying party application calls the RP policy file to execute a specific task.</span></span> <span data-ttu-id="27b81-152">For example, to initiate the sign-in flow.</span><span class="sxs-lookup"><span data-stu-id="27b81-152">For example, to initiate the sign-in flow.</span></span> <span data-ttu-id="27b81-153">The Identity Experience Framework in Azure AD B2C adds all of the elements first from the Base file, and then from the Extensions file, and finally from the RP policy file to assemble the current policy in effect.</span><span class="sxs-lookup"><span data-stu-id="27b81-153">The Identity Experience Framework in Azure AD B2C adds all of the elements first from the Base file, and then from the Extensions file, and finally from the RP policy file to assemble the current policy in effect.</span></span> <span data-ttu-id="27b81-154">Elements of the same type and name in the RP file override those elements in the Extensions, and Extensions overrides Base.</span><span class="sxs-lookup"><span data-stu-id="27b81-154">Elements of the same type and name in the RP file override those elements in the Extensions, and Extensions overrides Base.</span></span> <span data-ttu-id="27b81-155">The following diagram shows the relationship between the policy files and the relying party applications.</span><span class="sxs-lookup"><span data-stu-id="27b81-155">The following diagram shows the relationship between the policy files and the relying party applications.</span></span>

![Inheritance model](./media/trustframeworkpolicy/custom-policy-Inheritance-model.png)

<span data-ttu-id="27b81-157">The inheritance model is as follows:</span><span class="sxs-lookup"><span data-stu-id="27b81-157">The inheritance model is as follows:</span></span>

- <span data-ttu-id="27b81-158">The parent policy and child policy are of the same schema.</span><span class="sxs-lookup"><span data-stu-id="27b81-158">The parent policy and child policy are of the same schema.</span></span>
- <span data-ttu-id="27b81-159">The child policy at any level can inherit from the parent policy and extend it by adding new elements.</span><span class="sxs-lookup"><span data-stu-id="27b81-159">The child policy at any level can inherit from the parent policy and extend it by adding new elements.</span></span>
- <span data-ttu-id="27b81-160">There is no limit on the number of levels.</span><span class="sxs-lookup"><span data-stu-id="27b81-160">There is no limit on the number of levels.</span></span>

<span data-ttu-id="27b81-161">For more information, see [Get started with custom policies](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="27b81-161">For more information, see [Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="base-policy"></a><span data-ttu-id="27b81-162">Base policy</span><span class="sxs-lookup"><span data-stu-id="27b81-162">Base policy</span></span>

<span data-ttu-id="27b81-163">To inherit a policy from another policy, a **BasePolicy** element must be declared under the **TrustFrameworkPolicy** element of the policy file.</span><span class="sxs-lookup"><span data-stu-id="27b81-163">To inherit a policy from another policy, a **BasePolicy** element must be declared under the **TrustFrameworkPolicy** element of the policy file.</span></span> <span data-ttu-id="27b81-164">The **BasePolicy** element is a reference to the base policy from which this policy is derived.</span><span class="sxs-lookup"><span data-stu-id="27b81-164">The **BasePolicy** element is a reference to the base policy from which this policy is derived.</span></span>  

<span data-ttu-id="27b81-165">The **BasePolicy** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="27b81-165">The **BasePolicy** element contains the following elements:</span></span>

| <span data-ttu-id="27b81-166">Element</span><span class="sxs-lookup"><span data-stu-id="27b81-166">Element</span></span> | <span data-ttu-id="27b81-167">Occurrences</span><span class="sxs-lookup"><span data-stu-id="27b81-167">Occurrences</span></span> | <span data-ttu-id="27b81-168">Description</span><span class="sxs-lookup"><span data-stu-id="27b81-168">Description</span></span> |
| ------- | ----------- | --------|
| <span data-ttu-id="27b81-169">TenantId</span><span class="sxs-lookup"><span data-stu-id="27b81-169">TenantId</span></span> | <span data-ttu-id="27b81-170">1:1</span><span class="sxs-lookup"><span data-stu-id="27b81-170">1:1</span></span> | <span data-ttu-id="27b81-171">The identifier of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="27b81-171">The identifier of your Azure AD B2C tenant.</span></span> |
| <span data-ttu-id="27b81-172">PolicyId</span><span class="sxs-lookup"><span data-stu-id="27b81-172">PolicyId</span></span> | <span data-ttu-id="27b81-173">1:1</span><span class="sxs-lookup"><span data-stu-id="27b81-173">1:1</span></span> | <span data-ttu-id="27b81-174">The identifier of the parent policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-174">The identifier of the parent policy.</span></span> |


<span data-ttu-id="27b81-175">The following example shows how to specify a base policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-175">The following example shows how to specify a base policy.</span></span> <span data-ttu-id="27b81-176">This **B2C_1A_TrustFrameworkExtensions** policy is derived from the **B2C_1A_TrustFrameworkBase** policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-176">This **B2C_1A_TrustFrameworkExtensions** policy is derived from the **B2C_1A_TrustFrameworkBase** policy.</span></span> 

``` XML
<TrustFrameworkPolicy
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns:xsd="http://www.w3.org/2001/XMLSchema"
   xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
   PolicySchemaVersion="0.3.0.0"
   TenantId="mytenant.onmicrosoft.com"
   PolicyId="B2C_1A_TrustFrameworkExtensions"
   PublicPolicyUri="http://mytenant.onmicrosoft.com/B2C_1A_TrustFrameworkExtensions">

  <BasePolicy>
    <TenantId>yourtenant.onmicrosoft.com</TenantId>
    <PolicyId>B2C_1A_TrustFrameworkBase</PolicyId>
  </BasePolicy>
  ...
</TrustFrameworkPolicy>
```

## <a name="policy-execution"></a><span data-ttu-id="27b81-177">Policy execution</span><span class="sxs-lookup"><span data-stu-id="27b81-177">Policy execution</span></span>

<span data-ttu-id="27b81-178">A relying party application, such as a web, mobile, or desktop application, calls the [relying party (RP) policy](relyingparty.md).</span><span class="sxs-lookup"><span data-stu-id="27b81-178">A relying party application, such as a web, mobile, or desktop application, calls the [relying party (RP) policy](relyingparty.md).</span></span> <span data-ttu-id="27b81-179">The RP policy file executes a specific task, such as signing in, resetting a password, or editing a profile.</span><span class="sxs-lookup"><span data-stu-id="27b81-179">The RP policy file executes a specific task, such as signing in, resetting a password, or editing a profile.</span></span> <span data-ttu-id="27b81-180">The RP policy configures the list of claims the relying party application receives as part of the token that is issued.</span><span class="sxs-lookup"><span data-stu-id="27b81-180">The RP policy configures the list of claims the relying party application receives as part of the token that is issued.</span></span> <span data-ttu-id="27b81-181">Multiple applications can use the same policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-181">Multiple applications can use the same policy.</span></span> <span data-ttu-id="27b81-182">All applications receive the same token with claims and the user goes through the same user journey.</span><span class="sxs-lookup"><span data-stu-id="27b81-182">All applications receive the same token with claims and the user goes through the same user journey.</span></span> <span data-ttu-id="27b81-183">A single application can use multiple policies.</span><span class="sxs-lookup"><span data-stu-id="27b81-183">A single application can use multiple policies.</span></span>

<span data-ttu-id="27b81-184">Inside the RP policy file, you specify the **DefaultUserJourney** element, which points to the [UserJourney](userjourneys.md).</span><span class="sxs-lookup"><span data-stu-id="27b81-184">Inside the RP policy file, you specify the **DefaultUserJourney** element, which points to the [UserJourney](userjourneys.md).</span></span> <span data-ttu-id="27b81-185">The user journey usually is defined in the Base or Extensions policy.</span><span class="sxs-lookup"><span data-stu-id="27b81-185">The user journey usually is defined in the Base or Extensions policy.</span></span>

<span data-ttu-id="27b81-186">B2C_1A_signup_signin policy:</span><span class="sxs-lookup"><span data-stu-id="27b81-186">B2C_1A_signup_signin policy:</span></span>

```XML
<RelyingParty>
  <DefaultUserJourney ReferenceId="SignUpOrSignIn">
  ...
```

<span data-ttu-id="27b81-187">B2C_1A_TrustFrameWorkBase or B2C_1A_TrustFrameworkExtensionPolicy:</span><span class="sxs-lookup"><span data-stu-id="27b81-187">B2C_1A_TrustFrameWorkBase or B2C_1A_TrustFrameworkExtensionPolicy:</span></span>

```XML
<UserJourneys>
  <UserJourney Id="SignOrSignIn">
  ...
```

<span data-ttu-id="27b81-188">A user journey defines the business logic of what a user goes through.</span><span class="sxs-lookup"><span data-stu-id="27b81-188">A user journey defines the business logic of what a user goes through.</span></span> <span data-ttu-id="27b81-189">Each user journey is a set of orchestration steps that performs a series of actions, in sequence in terms of authentication and information collection.</span><span class="sxs-lookup"><span data-stu-id="27b81-189">Each user journey is a set of orchestration steps that performs a series of actions, in sequence in terms of authentication and information collection.</span></span> 

<span data-ttu-id="27b81-190">The **SocialAndLocalAccounts** policy file in the [starter pack](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-get-started-custom#download-starter-pack-and-modify-policies) contains the SignUpOrSignIn, ProfileEdit, PasswordReset user journeys.</span><span class="sxs-lookup"><span data-stu-id="27b81-190">The **SocialAndLocalAccounts** policy file in the [starter pack](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-get-started-custom#download-starter-pack-and-modify-policies) contains the SignUpOrSignIn, ProfileEdit, PasswordReset user journeys.</span></span> <span data-ttu-id="27b81-191">You can add more user journeys for another scenarios, such as changing an email address, link and unlink a social account, or resetting a password.</span><span class="sxs-lookup"><span data-stu-id="27b81-191">You can add more user journeys for another scenarios, such as changing an email address, link and unlink a social account, or resetting a password.</span></span> 

<span data-ttu-id="27b81-192">The orchestration steps may call a [Technical Profile](technicalprofiles.md).</span><span class="sxs-lookup"><span data-stu-id="27b81-192">The orchestration steps may call a [Technical Profile](technicalprofiles.md).</span></span> <span data-ttu-id="27b81-193">A technical profile provides a framework with a built-in mechanism to communicate with different types of parties.</span><span class="sxs-lookup"><span data-stu-id="27b81-193">A technical profile provides a framework with a built-in mechanism to communicate with different types of parties.</span></span> <span data-ttu-id="27b81-194">For example, a technical profile can perform these actions among others:</span><span class="sxs-lookup"><span data-stu-id="27b81-194">For example, a technical profile can perform these actions among others:</span></span>

- <span data-ttu-id="27b81-195">Render a user experience.</span><span class="sxs-lookup"><span data-stu-id="27b81-195">Render a user experience.</span></span>
- <span data-ttu-id="27b81-196">Allow users to sign in with social or an enterprise account, such as Facebook, Microsoft account, Google, Salesforce or any other identity provider.</span><span class="sxs-lookup"><span data-stu-id="27b81-196">Allow users to sign in with social or an enterprise account, such as Facebook, Microsoft account, Google, Salesforce or any other identity provider.</span></span>
- <span data-ttu-id="27b81-197">Set up phone verification for MFA.</span><span class="sxs-lookup"><span data-stu-id="27b81-197">Set up phone verification for MFA.</span></span>
- <span data-ttu-id="27b81-198">Read and write data to and from an Azure AD B2C identity store.</span><span class="sxs-lookup"><span data-stu-id="27b81-198">Read and write data to and from an Azure AD B2C identity store.</span></span>
- <span data-ttu-id="27b81-199">Call a custom Restful API service.</span><span class="sxs-lookup"><span data-stu-id="27b81-199">Call a custom Restful API service.</span></span>

![Policy execution](./media/trustframeworkpolicy/custom-policy-execution.png)

 <span data-ttu-id="27b81-201">The **TrustFrameworkPolicy** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="27b81-201">The **TrustFrameworkPolicy** element contains the following elements:</span></span>

- <span data-ttu-id="27b81-202">BasePolicy as specified above</span><span class="sxs-lookup"><span data-stu-id="27b81-202">BasePolicy as specified above</span></span>
- [<span data-ttu-id="27b81-203">BuildingBlocks</span><span class="sxs-lookup"><span data-stu-id="27b81-203">BuildingBlocks</span></span>](buildingblocks.md)
- [<span data-ttu-id="27b81-204">ClaimsProviders</span><span class="sxs-lookup"><span data-stu-id="27b81-204">ClaimsProviders</span></span>](claimsproviders.md)
- [<span data-ttu-id="27b81-205">UserJourneys</span><span class="sxs-lookup"><span data-stu-id="27b81-205">UserJourneys</span></span>](userjourneys.md)
- [<span data-ttu-id="27b81-206">RelyingParty</span><span class="sxs-lookup"><span data-stu-id="27b81-206">RelyingParty</span></span>](relyingparty.md)

