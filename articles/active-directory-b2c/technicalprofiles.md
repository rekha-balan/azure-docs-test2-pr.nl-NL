---
title: TechnicalProfiles | Microsoft Docs
description: Specify the TechnicalProfiles element of a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: f1242b299c6d2278bd75b576f225987854a2d8a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966345"
---
# <a name="technicalprofiles"></a><span data-ttu-id="26b92-103">TechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="26b92-103">TechnicalProfiles</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="26b92-104">A **TechnicalProfiles** element contains a set of technical profiles supported by the claim provider.</span><span class="sxs-lookup"><span data-stu-id="26b92-104">A **TechnicalProfiles** element contains a set of technical profiles supported by the claim provider.</span></span> <span data-ttu-id="26b92-105">Every claims provider must have one or more technical profiles that determine the endpoints and the protocols needed to communicate with the claims provider.</span><span class="sxs-lookup"><span data-stu-id="26b92-105">Every claims provider must have one or more technical profiles that determine the endpoints and the protocols needed to communicate with the claims provider.</span></span> <span data-ttu-id="26b92-106">A claims provider can have multiple technical profiles.</span><span class="sxs-lookup"><span data-stu-id="26b92-106">A claims provider can have multiple technical profiles.</span></span>

```XML
<ClaimsProvider>
  <DisplayName>Display name</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="Technical profile identifier">
      <DisplayName>Display name of technical profile</DisplayName>
      <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
      <Metadata>
        <Item Key="ServiceUrl">URL of service</Item>
        <Item Key="AuthenticationType">None</Item>
        <Item Key="SendClaimsIn">Body</Item>
      </Metadata>
      <InputTokenFormat>JWT</InputTokenFormat>
      <OutputTokenFormat>JWT</OutputTokenFormat>
      <CryptographicKeys>
        <Key ID="Key identifier" StorageReferenceId="Storage key container identifier"/>
        ...
      </CryptographicKeys>
      <InputClaimsTransformations>
        <InputClaimsTransformation ReferenceId="Claims transformation identifier" />
        ...
      <InputClaimsTransformations>
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="givenName" DefaultValue="givenName" PartnerClaimType="firstName" />
        ...
      </InputClaims>
      <PersistedClaims>
        <PersistedClaim ClaimTypeReferenceId="givenName" DefaultValue="givenName" PartnerClaimType="firstName" />
        ...
      </PersistedClaims>
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="loyaltyNumber" DefaultValue="loyaltyNumber" PartnerClaimType="loyaltyNumber" />
      </OutputClaims>
      <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="Claims transformation identifier" />
        ...
      <OutputClaimsTransformations>
      <ValidationTechnicalProfiles>
        <ValidationTechnicalProfile ReferenceId="Technical profile identifier" />
        ...
      </ValidationTechnicalProfiles>
      <SubjectNamingInfo ClaimType="Claim type identifier" />
      <IncludeTechnicalProfile ReferenceId="Technical profile identifier" />
      <UseTechnicalProfileForSessionManagement ReferenceId="Technical profile identifier" />
    </TechnicalProfile>
  </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="26b92-107">The **TechnicalProfile** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-107">The **TechnicalProfile** element contains the following attribute:</span></span>

| <span data-ttu-id="26b92-108">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-108">Attribute</span></span> | <span data-ttu-id="26b92-109">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-109">Required</span></span> | <span data-ttu-id="26b92-110">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-110">Description</span></span> |
|---------|---------|---------|
| <span data-ttu-id="26b92-111">Id</span><span class="sxs-lookup"><span data-stu-id="26b92-111">Id</span></span> | <span data-ttu-id="26b92-112">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-112">Yes</span></span> | <span data-ttu-id="26b92-113">A unique identifier of the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-113">A unique identifier of the technical profile.</span></span> <span data-ttu-id="26b92-114">The technical profile can be referenced using this identifier from other elements in the policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-114">The technical profile can be referenced using this identifier from other elements in the policy file.</span></span> <span data-ttu-id="26b92-115">For example, **OrchestrationSteps** and **ValidationTechnicalProfile**.</span><span class="sxs-lookup"><span data-stu-id="26b92-115">For example, **OrchestrationSteps** and **ValidationTechnicalProfile**.</span></span> |

<span data-ttu-id="26b92-116">The **TechnicalProfile** contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="26b92-116">The **TechnicalProfile** contains the following elements:</span></span>

| <span data-ttu-id="26b92-117">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-117">Element</span></span> | <span data-ttu-id="26b92-118">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-118">Occurrences</span></span> | <span data-ttu-id="26b92-119">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-119">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-120">Domain</span><span class="sxs-lookup"><span data-stu-id="26b92-120">Domain</span></span> | <span data-ttu-id="26b92-121">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-121">0:1</span></span> | <span data-ttu-id="26b92-122">The domain name for the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-122">The domain name for the technical profile.</span></span> <span data-ttu-id="26b92-123">For example, if your technical profile specifies the Facebook identity provider, the domain name is Facebook.com.</span><span class="sxs-lookup"><span data-stu-id="26b92-123">For example, if your technical profile specifies the Facebook identity provider, the domain name is Facebook.com.</span></span> |
| <span data-ttu-id="26b92-124">DisplayName</span><span class="sxs-lookup"><span data-stu-id="26b92-124">DisplayName</span></span> | <span data-ttu-id="26b92-125">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-125">0:1</span></span> | <span data-ttu-id="26b92-126">The name of the technical profile that can be displayed to users.</span><span class="sxs-lookup"><span data-stu-id="26b92-126">The name of the technical profile that can be displayed to users.</span></span> |
| <span data-ttu-id="26b92-127">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-127">Description</span></span> | <span data-ttu-id="26b92-128">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-128">0:1</span></span> | <span data-ttu-id="26b92-129">The description of the technical profile that can be displayed to users.</span><span class="sxs-lookup"><span data-stu-id="26b92-129">The description of the technical profile that can be displayed to users.</span></span> |
| <span data-ttu-id="26b92-130">Protocol</span><span class="sxs-lookup"><span data-stu-id="26b92-130">Protocol</span></span> | <span data-ttu-id="26b92-131">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-131">0:1</span></span> | <span data-ttu-id="26b92-132">The protocol used for the communication with the other party.</span><span class="sxs-lookup"><span data-stu-id="26b92-132">The protocol used for the communication with the other party.</span></span> |
| <span data-ttu-id="26b92-133">Metadata</span><span class="sxs-lookup"><span data-stu-id="26b92-133">Metadata</span></span> | <span data-ttu-id="26b92-134">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-134">0:1</span></span> | <span data-ttu-id="26b92-135">A collection of key/value pairs that are utilized by the protocol for communicating with the endpoint in the course of a transaction.</span><span class="sxs-lookup"><span data-stu-id="26b92-135">A collection of key/value pairs that are utilized by the protocol for communicating with the endpoint in the course of a transaction.</span></span> |
| <span data-ttu-id="26b92-136">InputTokenFormat</span><span class="sxs-lookup"><span data-stu-id="26b92-136">InputTokenFormat</span></span> | <span data-ttu-id="26b92-137">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-137">0:1</span></span> | <span data-ttu-id="26b92-138">The format of the input token.</span><span class="sxs-lookup"><span data-stu-id="26b92-138">The format of the input token.</span></span> <span data-ttu-id="26b92-139">Possible values: `JSON`, `JWT`, `SAML11`, or `SAML2`.</span><span class="sxs-lookup"><span data-stu-id="26b92-139">Possible values: `JSON`, `JWT`, `SAML11`, or `SAML2`.</span></span> <span data-ttu-id="26b92-140">The `JWT` value represents a JSON Web Token as per IETF specification.</span><span class="sxs-lookup"><span data-stu-id="26b92-140">The `JWT` value represents a JSON Web Token as per IETF specification.</span></span> <span data-ttu-id="26b92-141">The `SAML11` value represents a SAML 1.1 security token as per OASIS specification.</span><span class="sxs-lookup"><span data-stu-id="26b92-141">The `SAML11` value represents a SAML 1.1 security token as per OASIS specification.</span></span>  <span data-ttu-id="26b92-142">The `SAML2` value represents a SAML 2.0 security token as per OASIS specification.</span><span class="sxs-lookup"><span data-stu-id="26b92-142">The `SAML2` value represents a SAML 2.0 security token as per OASIS specification.</span></span> |
| <span data-ttu-id="26b92-143">OutputTokenFormat</span><span class="sxs-lookup"><span data-stu-id="26b92-143">OutputTokenFormat</span></span> | <span data-ttu-id="26b92-144">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-144">0:1</span></span> | <span data-ttu-id="26b92-145">The format of the output token.</span><span class="sxs-lookup"><span data-stu-id="26b92-145">The format of the output token.</span></span> <span data-ttu-id="26b92-146">Possible values: `JSON`, `JWT`, `SAML11`, or `SAML2`.</span><span class="sxs-lookup"><span data-stu-id="26b92-146">Possible values: `JSON`, `JWT`, `SAML11`, or `SAML2`.</span></span> |
| <span data-ttu-id="26b92-147">CryptographicKeys</span><span class="sxs-lookup"><span data-stu-id="26b92-147">CryptographicKeys</span></span> | <span data-ttu-id="26b92-148">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-148">0:1</span></span> | <span data-ttu-id="26b92-149">A list of cryptographic keys that are used in the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-149">A list of cryptographic keys that are used in the technical profile.</span></span> |
| <span data-ttu-id="26b92-150">InputClaimsTransformations</span><span class="sxs-lookup"><span data-stu-id="26b92-150">InputClaimsTransformations</span></span> | <span data-ttu-id="26b92-151">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-151">0:1</span></span> | <span data-ttu-id="26b92-152">A list of previously defined references to claims transformations that should be executed before any claims are sent to the claims provider or the relying party.</span><span class="sxs-lookup"><span data-stu-id="26b92-152">A list of previously defined references to claims transformations that should be executed before any claims are sent to the claims provider or the relying party.</span></span> |
| <span data-ttu-id="26b92-153">InputClaims</span><span class="sxs-lookup"><span data-stu-id="26b92-153">InputClaims</span></span> | <span data-ttu-id="26b92-154">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-154">0:1</span></span> | <span data-ttu-id="26b92-155">A list of the previously defined references to claim types that are taken as input in the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-155">A list of the previously defined references to claim types that are taken as input in the technical profile.</span></span> |
| <span data-ttu-id="26b92-156">PersistedClaims</span><span class="sxs-lookup"><span data-stu-id="26b92-156">PersistedClaims</span></span> | <span data-ttu-id="26b92-157">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-157">0:1</span></span> | <span data-ttu-id="26b92-158">A list of the previously defined references to claim types that are persisted by the claims provider that relates to the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-158">A list of the previously defined references to claim types that are persisted by the claims provider that relates to the technical profile.</span></span> |
| <span data-ttu-id="26b92-159">OutputClaims</span><span class="sxs-lookup"><span data-stu-id="26b92-159">OutputClaims</span></span> | <span data-ttu-id="26b92-160">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-160">0:1</span></span> | <span data-ttu-id="26b92-161">A list of the previously defined references to claim types that are taken as output in the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-161">A list of the previously defined references to claim types that are taken as output in the technical profile.</span></span> |
| <span data-ttu-id="26b92-162">OutputClaimsTransformations</span><span class="sxs-lookup"><span data-stu-id="26b92-162">OutputClaimsTransformations</span></span> | <span data-ttu-id="26b92-163">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-163">0:1</span></span> | <span data-ttu-id="26b92-164">A list of previously defined references to claims transformations that should be executed after the claims are received from the claims provider.</span><span class="sxs-lookup"><span data-stu-id="26b92-164">A list of previously defined references to claims transformations that should be executed after the claims are received from the claims provider.</span></span> |
| <span data-ttu-id="26b92-165">ValidationTechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="26b92-165">ValidationTechnicalProfiles</span></span> | <span data-ttu-id="26b92-166">0:n</span><span class="sxs-lookup"><span data-stu-id="26b92-166">0:n</span></span> | <span data-ttu-id="26b92-167">A list of references to other technical profiles that the technical profile uses for validation purposes.</span><span class="sxs-lookup"><span data-stu-id="26b92-167">A list of references to other technical profiles that the technical profile uses for validation purposes.</span></span> <span data-ttu-id="26b92-168">For more information, see [validation technical profile](validation-technical-profile.md)</span><span class="sxs-lookup"><span data-stu-id="26b92-168">For more information, see [validation technical profile](validation-technical-profile.md)</span></span>|
| <span data-ttu-id="26b92-169">SubjectNamingInfo</span><span class="sxs-lookup"><span data-stu-id="26b92-169">SubjectNamingInfo</span></span> | <span data-ttu-id="26b92-170">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-170">0:1</span></span> | <span data-ttu-id="26b92-171">Controls the production of the subject name in tokens where the subject name is specified separately from claims.</span><span class="sxs-lookup"><span data-stu-id="26b92-171">Controls the production of the subject name in tokens where the subject name is specified separately from claims.</span></span> <span data-ttu-id="26b92-172">For example, OAuth or SAML.</span><span class="sxs-lookup"><span data-stu-id="26b92-172">For example, OAuth or SAML.</span></span>  |
| <span data-ttu-id="26b92-173">IncludeClaimsFromTechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="26b92-173">IncludeClaimsFromTechnicalProfile</span></span> | <span data-ttu-id="26b92-174">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-174">0:1</span></span> | <span data-ttu-id="26b92-175">An identifier of a technical profile from which you want all of the input and output claims to be added to this technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-175">An identifier of a technical profile from which you want all of the input and output claims to be added to this technical profile.</span></span> <span data-ttu-id="26b92-176">The referenced technical profile must be defined in the same policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-176">The referenced technical profile must be defined in the same policy file.</span></span> | 
| <span data-ttu-id="26b92-177">IncludeTechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="26b92-177">IncludeTechnicalProfile</span></span> |<span data-ttu-id="26b92-178">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-178">0:1</span></span> | <span data-ttu-id="26b92-179">An identifier of a technical profile from which you want all data to be added to this technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-179">An identifier of a technical profile from which you want all data to be added to this technical profile.</span></span> <span data-ttu-id="26b92-180">The referenced technical profile must exist in the same policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-180">The referenced technical profile must exist in the same policy file.</span></span> |
| <span data-ttu-id="26b92-181">UseTechnicalProfileForSessionManagement</span><span class="sxs-lookup"><span data-stu-id="26b92-181">UseTechnicalProfileForSessionManagement</span></span> | <span data-ttu-id="26b92-182">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-182">0:1</span></span> | <span data-ttu-id="26b92-183">A different technical profile to be used for session management.</span><span class="sxs-lookup"><span data-stu-id="26b92-183">A different technical profile to be used for session management.</span></span> |
|<span data-ttu-id="26b92-184">EnabledForUserJourneys</span><span class="sxs-lookup"><span data-stu-id="26b92-184">EnabledForUserJourneys</span></span>| <span data-ttu-id="26b92-185">0:1</span><span class="sxs-lookup"><span data-stu-id="26b92-185">0:1</span></span> |<span data-ttu-id="26b92-186">Controls if the technical profile is executed in a user journey.</span><span class="sxs-lookup"><span data-stu-id="26b92-186">Controls if the technical profile is executed in a user journey.</span></span>  |

### <a name="protocol"></a><span data-ttu-id="26b92-187">Protocol</span><span class="sxs-lookup"><span data-stu-id="26b92-187">Protocol</span></span>

<span data-ttu-id="26b92-188">The **Protocol** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="26b92-188">The **Protocol** element contains the following attributes:</span></span>

| <span data-ttu-id="26b92-189">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-189">Attribute</span></span> | <span data-ttu-id="26b92-190">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-190">Required</span></span> | <span data-ttu-id="26b92-191">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-191">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-192">Name</span><span class="sxs-lookup"><span data-stu-id="26b92-192">Name</span></span> | <span data-ttu-id="26b92-193">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-193">Yes</span></span> | <span data-ttu-id="26b92-194">The name of a valid protocol supported by Azure AD B2C that is used as part of the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-194">The name of a valid protocol supported by Azure AD B2C that is used as part of the technical profile.</span></span> <span data-ttu-id="26b92-195">Possible values: `OAuth1`, `OAuth2`, `SAML2`, `OpenIdConnect`, `WsFed`, `WsTrust`, `Proprietary`, `session management`, `self-asserted`, or `None`.</span><span class="sxs-lookup"><span data-stu-id="26b92-195">Possible values: `OAuth1`, `OAuth2`, `SAML2`, `OpenIdConnect`, `WsFed`, `WsTrust`, `Proprietary`, `session management`, `self-asserted`, or `None`.</span></span> |
| <span data-ttu-id="26b92-196">Handler</span><span class="sxs-lookup"><span data-stu-id="26b92-196">Handler</span></span> | <span data-ttu-id="26b92-197">No</span><span class="sxs-lookup"><span data-stu-id="26b92-197">No</span></span> | <span data-ttu-id="26b92-198">When the protocol name is set to `Proprietary`, specify the fully-qualified name of the assembly that is used by Azure AD B2C to determine the protocol handler.</span><span class="sxs-lookup"><span data-stu-id="26b92-198">When the protocol name is set to `Proprietary`, specify the fully-qualified name of the assembly that is used by Azure AD B2C to determine the protocol handler.</span></span> |

### <a name="metadata"></a><span data-ttu-id="26b92-199">Metadata</span><span class="sxs-lookup"><span data-stu-id="26b92-199">Metadata</span></span>

<span data-ttu-id="26b92-200">A **Metadata** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="26b92-200">A **Metadata** element contains the following elements:</span></span>

| <span data-ttu-id="26b92-201">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-201">Element</span></span> | <span data-ttu-id="26b92-202">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-202">Occurrences</span></span> | <span data-ttu-id="26b92-203">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-203">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-204">Item</span><span class="sxs-lookup"><span data-stu-id="26b92-204">Item</span></span> | <span data-ttu-id="26b92-205">0:n</span><span class="sxs-lookup"><span data-stu-id="26b92-205">0:n</span></span> | <span data-ttu-id="26b92-206">The metadata that relates to the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-206">The metadata that relates to the technical profile.</span></span> <span data-ttu-id="26b92-207">Each type of technical profile has a different set of metadata items.</span><span class="sxs-lookup"><span data-stu-id="26b92-207">Each type of technical profile has a different set of metadata items.</span></span> <span data-ttu-id="26b92-208">See the technical profile types section, for more information.</span><span class="sxs-lookup"><span data-stu-id="26b92-208">See the technical profile types section, for more information.</span></span> |

#### <a name="item"></a><span data-ttu-id="26b92-209">Item</span><span class="sxs-lookup"><span data-stu-id="26b92-209">Item</span></span>

<span data-ttu-id="26b92-210">The **Item** element of the **Metadata** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="26b92-210">The **Item** element of the **Metadata** element contains the following attributes:</span></span>

| <span data-ttu-id="26b92-211">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-211">Attribute</span></span> | <span data-ttu-id="26b92-212">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-212">Required</span></span> | <span data-ttu-id="26b92-213">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-213">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-214">Key</span><span class="sxs-lookup"><span data-stu-id="26b92-214">Key</span></span> | <span data-ttu-id="26b92-215">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-215">Yes</span></span> | <span data-ttu-id="26b92-216">The metadata key.</span><span class="sxs-lookup"><span data-stu-id="26b92-216">The metadata key.</span></span> <span data-ttu-id="26b92-217">See each technical profile type, for the list of metadata items.</span><span class="sxs-lookup"><span data-stu-id="26b92-217">See each technical profile type, for the list of metadata items.</span></span> |

### <a name="cryptographickeys"></a><span data-ttu-id="26b92-218">CryptographicKeys</span><span class="sxs-lookup"><span data-stu-id="26b92-218">CryptographicKeys</span></span>

<span data-ttu-id="26b92-219">The **CryptographicKeys** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="26b92-219">The **CryptographicKeys** element contains the following element:</span></span>

| <span data-ttu-id="26b92-220">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-220">Element</span></span> | <span data-ttu-id="26b92-221">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-221">Occurrences</span></span> | <span data-ttu-id="26b92-222">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-222">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-223">Key</span><span class="sxs-lookup"><span data-stu-id="26b92-223">Key</span></span> | <span data-ttu-id="26b92-224">1:n</span><span class="sxs-lookup"><span data-stu-id="26b92-224">1:n</span></span> | <span data-ttu-id="26b92-225">A cryptographic key used in this technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-225">A cryptographic key used in this technical profile.</span></span> |

#### <a name="key"></a><span data-ttu-id="26b92-226">Key</span><span class="sxs-lookup"><span data-stu-id="26b92-226">Key</span></span>

<span data-ttu-id="26b92-227">The **Key** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-227">The **Key** element contains the following attribute:</span></span>

| <span data-ttu-id="26b92-228">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-228">Attribute</span></span> | <span data-ttu-id="26b92-229">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-229">Required</span></span> | <span data-ttu-id="26b92-230">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-230">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-231">Id</span><span class="sxs-lookup"><span data-stu-id="26b92-231">Id</span></span> | <span data-ttu-id="26b92-232">No</span><span class="sxs-lookup"><span data-stu-id="26b92-232">No</span></span> | <span data-ttu-id="26b92-233">A unique identifier of a particular key pair referenced from other elements in the policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-233">A unique identifier of a particular key pair referenced from other elements in the policy file.</span></span> |
| <span data-ttu-id="26b92-234">StorageReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-234">StorageReferenceId</span></span> | <span data-ttu-id="26b92-235">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-235">Yes</span></span> | <span data-ttu-id="26b92-236">An identifer of a storage key container referenced from other elements in the policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-236">An identifer of a storage key container referenced from other elements in the policy file.</span></span> |

### <a name="inputclaimstransformations"></a><span data-ttu-id="26b92-237">InputClaimsTransformations</span><span class="sxs-lookup"><span data-stu-id="26b92-237">InputClaimsTransformations</span></span>

<span data-ttu-id="26b92-238">The **InputClaimsTransformations** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="26b92-238">The **InputClaimsTransformations** element contains the following element:</span></span>

| <span data-ttu-id="26b92-239">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-239">Element</span></span> | <span data-ttu-id="26b92-240">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-240">Occurrences</span></span> | <span data-ttu-id="26b92-241">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-241">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-242">InputClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="26b92-242">InputClaimsTransformation</span></span> | <span data-ttu-id="26b92-243">1:n</span><span class="sxs-lookup"><span data-stu-id="26b92-243">1:n</span></span> | <span data-ttu-id="26b92-244">The identifier of a claims transformation that should be executed before any claims are sent to the claims provider or the relying party.</span><span class="sxs-lookup"><span data-stu-id="26b92-244">The identifier of a claims transformation that should be executed before any claims are sent to the claims provider or the relying party.</span></span> <span data-ttu-id="26b92-245">A claims transformation can be used to modify existing ClaimsSchema claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="26b92-245">A claims transformation can be used to modify existing ClaimsSchema claims or generate new ones.</span></span> |

#### <a name="inputclaimstransformation"></a><span data-ttu-id="26b92-246">InputClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="26b92-246">InputClaimsTransformation</span></span>

<span data-ttu-id="26b92-247">The **InputClaimsTransformation** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-247">The **InputClaimsTransformation** element contains the following attribute:</span></span>

| <span data-ttu-id="26b92-248">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-248">Attribute</span></span> | <span data-ttu-id="26b92-249">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-249">Required</span></span> | <span data-ttu-id="26b92-250">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-250">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-251">ReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-251">ReferenceId</span></span> | <span data-ttu-id="26b92-252">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-252">Yes</span></span> | <span data-ttu-id="26b92-253">An identifier of a claims transformation already defined in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-253">An identifier of a claims transformation already defined in the policy file or parent policy file.</span></span> |

### <a name="inputclaims"></a><span data-ttu-id="26b92-254">InputClaims</span><span class="sxs-lookup"><span data-stu-id="26b92-254">InputClaims</span></span>

<span data-ttu-id="26b92-255">The **InputClaims** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="26b92-255">The **InputClaims** element contains the following element:</span></span>

| <span data-ttu-id="26b92-256">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-256">Element</span></span> | <span data-ttu-id="26b92-257">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-257">Occurrences</span></span> | <span data-ttu-id="26b92-258">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-258">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-259">InputClaim</span><span class="sxs-lookup"><span data-stu-id="26b92-259">InputClaim</span></span> | <span data-ttu-id="26b92-260">1:n</span><span class="sxs-lookup"><span data-stu-id="26b92-260">1:n</span></span> | <span data-ttu-id="26b92-261">An expected input claim type.</span><span class="sxs-lookup"><span data-stu-id="26b92-261">An expected input claim type.</span></span> |

#### <a name="inputclaim"></a><span data-ttu-id="26b92-262">InputClaim</span><span class="sxs-lookup"><span data-stu-id="26b92-262">InputClaim</span></span> 

<span data-ttu-id="26b92-263">The **InputClaim** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="26b92-263">The **InputClaim** element contains the following attributes:</span></span>

| <span data-ttu-id="26b92-264">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-264">Attribute</span></span> | <span data-ttu-id="26b92-265">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-265">Required</span></span> | <span data-ttu-id="26b92-266">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-266">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-267">ClaimTypeReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-267">ClaimTypeReferenceId</span></span> | <span data-ttu-id="26b92-268">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-268">Yes</span></span> | <span data-ttu-id="26b92-269">The identifier of a claim type already defined in the ClaimsSchema section in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-269">The identifier of a claim type already defined in the ClaimsSchema section in the policy file or parent policy file.</span></span> |
| <span data-ttu-id="26b92-270">DefaultValue</span><span class="sxs-lookup"><span data-stu-id="26b92-270">DefaultValue</span></span> | <span data-ttu-id="26b92-271">No</span><span class="sxs-lookup"><span data-stu-id="26b92-271">No</span></span> | <span data-ttu-id="26b92-272">A default value to use to create a claim if the claim indicated by ClaimTypeReferenceId does not exist so that the resulting claim can be used as an InputClaim by the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-272">A default value to use to create a claim if the claim indicated by ClaimTypeReferenceId does not exist so that the resulting claim can be used as an InputClaim by the technical profile.</span></span> |
| <span data-ttu-id="26b92-273">PartnerClaimType</span><span class="sxs-lookup"><span data-stu-id="26b92-273">PartnerClaimType</span></span> | <span data-ttu-id="26b92-274">No</span><span class="sxs-lookup"><span data-stu-id="26b92-274">No</span></span> | <span data-ttu-id="26b92-275">The identifier of the claim type of the external partner that the specified policy claim type maps to.</span><span class="sxs-lookup"><span data-stu-id="26b92-275">The identifier of the claim type of the external partner that the specified policy claim type maps to.</span></span> <span data-ttu-id="26b92-276">If the PartnerClaimType attribute is not specified, then the specified policy claim type is mapped to the partner claim type of the same name.</span><span class="sxs-lookup"><span data-stu-id="26b92-276">If the PartnerClaimType attribute is not specified, then the specified policy claim type is mapped to the partner claim type of the same name.</span></span> <span data-ttu-id="26b92-277">Use this property when your claim type name is different from the other party.</span><span class="sxs-lookup"><span data-stu-id="26b92-277">Use this property when your claim type name is different from the other party.</span></span> <span data-ttu-id="26b92-278">For example, the first claim name is 'givenName', while the partner uses a claim named 'first_name'.</span><span class="sxs-lookup"><span data-stu-id="26b92-278">For example, the first claim name is 'givenName', while the partner uses a claim named 'first_name'.</span></span> |

### <a name="persistedclaims"></a><span data-ttu-id="26b92-279">PersistedClaims</span><span class="sxs-lookup"><span data-stu-id="26b92-279">PersistedClaims</span></span>

<span data-ttu-id="26b92-280">The **PersistedClaims** element contains the following elements:</span><span class="sxs-lookup"><span data-stu-id="26b92-280">The **PersistedClaims** element contains the following elements:</span></span>

| <span data-ttu-id="26b92-281">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-281">Element</span></span> | <span data-ttu-id="26b92-282">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-282">Occurrences</span></span> | <span data-ttu-id="26b92-283">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-283">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-284">PersistedClaim</span><span class="sxs-lookup"><span data-stu-id="26b92-284">PersistedClaim</span></span> | <span data-ttu-id="26b92-285">1:n</span><span class="sxs-lookup"><span data-stu-id="26b92-285">1:n</span></span> | <span data-ttu-id="26b92-286">The claim type to persist.</span><span class="sxs-lookup"><span data-stu-id="26b92-286">The claim type to persist.</span></span> |

#### <a name="persistedclaim"></a><span data-ttu-id="26b92-287">PersistedClaim</span><span class="sxs-lookup"><span data-stu-id="26b92-287">PersistedClaim</span></span> 

<span data-ttu-id="26b92-288">The **PersistedClaim** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="26b92-288">The **PersistedClaim** element contains the following attributes:</span></span>

| <span data-ttu-id="26b92-289">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-289">Attribute</span></span> | <span data-ttu-id="26b92-290">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-290">Required</span></span> | <span data-ttu-id="26b92-291">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-291">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-292">ClaimTypeReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-292">ClaimTypeReferenceId</span></span> | <span data-ttu-id="26b92-293">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-293">Yes</span></span> | <span data-ttu-id="26b92-294">The identifier of a claim type already defined in the ClaimsSchema section in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-294">The identifier of a claim type already defined in the ClaimsSchema section in the policy file or parent policy file.</span></span> |
| <span data-ttu-id="26b92-295">DefaultValue</span><span class="sxs-lookup"><span data-stu-id="26b92-295">DefaultValue</span></span> | <span data-ttu-id="26b92-296">No</span><span class="sxs-lookup"><span data-stu-id="26b92-296">No</span></span> | <span data-ttu-id="26b92-297">A default value to use to create a claim if the claim indicated by ClaimTypeReferenceId does not exist so that the resulting claim can be used as an InputClaim by the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-297">A default value to use to create a claim if the claim indicated by ClaimTypeReferenceId does not exist so that the resulting claim can be used as an InputClaim by the technical profile.</span></span> |
| <span data-ttu-id="26b92-298">PartnerClaimType</span><span class="sxs-lookup"><span data-stu-id="26b92-298">PartnerClaimType</span></span> | <span data-ttu-id="26b92-299">No</span><span class="sxs-lookup"><span data-stu-id="26b92-299">No</span></span> | <span data-ttu-id="26b92-300">The identifier of the claim type of the external partner that the specified policy claim type maps to.</span><span class="sxs-lookup"><span data-stu-id="26b92-300">The identifier of the claim type of the external partner that the specified policy claim type maps to.</span></span> <span data-ttu-id="26b92-301">If the PartnerClaimType attribute is not specified, then the specified policy claim type is mapped to the partner claim type of the same name.</span><span class="sxs-lookup"><span data-stu-id="26b92-301">If the PartnerClaimType attribute is not specified, then the specified policy claim type is mapped to the partner claim type of the same name.</span></span> <span data-ttu-id="26b92-302">Use this property when your claim type name is different from the other party.</span><span class="sxs-lookup"><span data-stu-id="26b92-302">Use this property when your claim type name is different from the other party.</span></span> <span data-ttu-id="26b92-303">For example, the first claim name is 'givenName', while the partner uses a claim named 'first_name'.</span><span class="sxs-lookup"><span data-stu-id="26b92-303">For example, the first claim name is 'givenName', while the partner uses a claim named 'first_name'.</span></span> |

### <a name="outputclaims"></a><span data-ttu-id="26b92-304">OutputClaims</span><span class="sxs-lookup"><span data-stu-id="26b92-304">OutputClaims</span></span>

<span data-ttu-id="26b92-305">The **OutputClaims** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="26b92-305">The **OutputClaims** element contains the following element:</span></span>

| <span data-ttu-id="26b92-306">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-306">Element</span></span> | <span data-ttu-id="26b92-307">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-307">Occurrences</span></span> | <span data-ttu-id="26b92-308">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-308">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-309">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="26b92-309">OutputClaim</span></span> | <span data-ttu-id="26b92-310">1:n</span><span class="sxs-lookup"><span data-stu-id="26b92-310">1:n</span></span> | <span data-ttu-id="26b92-311">An expected output claim type.</span><span class="sxs-lookup"><span data-stu-id="26b92-311">An expected output claim type.</span></span> |

#### <a name="outputclaim"></a><span data-ttu-id="26b92-312">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="26b92-312">OutputClaim</span></span> 

<span data-ttu-id="26b92-313">The **OutputClaim** element contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="26b92-313">The **OutputClaim** element contains the following attributes:</span></span>

| <span data-ttu-id="26b92-314">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-314">Attribute</span></span> | <span data-ttu-id="26b92-315">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-315">Required</span></span> | <span data-ttu-id="26b92-316">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-316">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-317">ClaimTypeReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-317">ClaimTypeReferenceId</span></span> | <span data-ttu-id="26b92-318">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-318">Yes</span></span> | <span data-ttu-id="26b92-319">The identifier of a claim type already defined in the ClaimsSchema section in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-319">The identifier of a claim type already defined in the ClaimsSchema section in the policy file or parent policy file.</span></span> |
| <span data-ttu-id="26b92-320">DefaultValue</span><span class="sxs-lookup"><span data-stu-id="26b92-320">DefaultValue</span></span> | <span data-ttu-id="26b92-321">No</span><span class="sxs-lookup"><span data-stu-id="26b92-321">No</span></span> | <span data-ttu-id="26b92-322">A default value to use to create a claim if the claim indicated by ClaimTypeReferenceId does not exist so that the resulting claim can be used as an InputClaim by the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-322">A default value to use to create a claim if the claim indicated by ClaimTypeReferenceId does not exist so that the resulting claim can be used as an InputClaim by the technical profile.</span></span> |
|<span data-ttu-id="26b92-323">AlwaysUseDefaultValue</span><span class="sxs-lookup"><span data-stu-id="26b92-323">AlwaysUseDefaultValue</span></span> |<span data-ttu-id="26b92-324">No</span><span class="sxs-lookup"><span data-stu-id="26b92-324">No</span></span> |<span data-ttu-id="26b92-325">Force the use of the default value.</span><span class="sxs-lookup"><span data-stu-id="26b92-325">Force the use of the default value.</span></span>  |
| <span data-ttu-id="26b92-326">PartnerClaimType</span><span class="sxs-lookup"><span data-stu-id="26b92-326">PartnerClaimType</span></span> | <span data-ttu-id="26b92-327">No</span><span class="sxs-lookup"><span data-stu-id="26b92-327">No</span></span> | <span data-ttu-id="26b92-328">The identifier of the claim type of the external partner that the specified policy claim type maps to.</span><span class="sxs-lookup"><span data-stu-id="26b92-328">The identifier of the claim type of the external partner that the specified policy claim type maps to.</span></span> <span data-ttu-id="26b92-329">If the PartnerClaimType attribute is not specified, then the specified policy claim type is mapped to the partner claim type of the same name.</span><span class="sxs-lookup"><span data-stu-id="26b92-329">If the PartnerClaimType attribute is not specified, then the specified policy claim type is mapped to the partner claim type of the same name.</span></span> <span data-ttu-id="26b92-330">Use this property when your claim type name is different from the other party.</span><span class="sxs-lookup"><span data-stu-id="26b92-330">Use this property when your claim type name is different from the other party.</span></span> <span data-ttu-id="26b92-331">For example, the first claim name is 'givenName', while the partner uses a claim named 'first_name'.</span><span class="sxs-lookup"><span data-stu-id="26b92-331">For example, the first claim name is 'givenName', while the partner uses a claim named 'first_name'.</span></span> |

### <a name="outputclaimstransformations"></a><span data-ttu-id="26b92-332">OutputClaimsTransformations</span><span class="sxs-lookup"><span data-stu-id="26b92-332">OutputClaimsTransformations</span></span>

<span data-ttu-id="26b92-333">The **OutputClaimsTransformations** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="26b92-333">The **OutputClaimsTransformations** element contains the following element:</span></span>

| <span data-ttu-id="26b92-334">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-334">Element</span></span> | <span data-ttu-id="26b92-335">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-335">Occurrences</span></span> | <span data-ttu-id="26b92-336">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-336">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-337">OutputClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="26b92-337">OutputClaimsTransformation</span></span> | <span data-ttu-id="26b92-338">1:n</span><span class="sxs-lookup"><span data-stu-id="26b92-338">1:n</span></span> | <span data-ttu-id="26b92-339">The identifiers of claims transformations that should be executed before any claims are sent to the claims provider or the relying party.</span><span class="sxs-lookup"><span data-stu-id="26b92-339">The identifiers of claims transformations that should be executed before any claims are sent to the claims provider or the relying party.</span></span> <span data-ttu-id="26b92-340">A claims transformation can be used to modify existing ClaimsSchema claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="26b92-340">A claims transformation can be used to modify existing ClaimsSchema claims or generate new ones.</span></span> |

#### <a name="outputclaimstransformation"></a><span data-ttu-id="26b92-341">OutputClaimsTransformation</span><span class="sxs-lookup"><span data-stu-id="26b92-341">OutputClaimsTransformation</span></span>

<span data-ttu-id="26b92-342">The **OutputClaimsTransformation** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-342">The **OutputClaimsTransformation** element contains the following attribute:</span></span>

| <span data-ttu-id="26b92-343">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-343">Attribute</span></span> | <span data-ttu-id="26b92-344">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-344">Required</span></span> | <span data-ttu-id="26b92-345">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-345">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-346">ReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-346">ReferenceId</span></span> | <span data-ttu-id="26b92-347">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-347">Yes</span></span> | <span data-ttu-id="26b92-348">An identifier of a claims transformation already defined in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-348">An identifier of a claims transformation already defined in the policy file or parent policy file.</span></span> |

### <a name="validationtechnicalprofiles"></a><span data-ttu-id="26b92-349">ValidationTechnicalProfiles</span><span class="sxs-lookup"><span data-stu-id="26b92-349">ValidationTechnicalProfiles</span></span>

<span data-ttu-id="26b92-350">The **ValidationTechnicalProfiles** element contains the following element:</span><span class="sxs-lookup"><span data-stu-id="26b92-350">The **ValidationTechnicalProfiles** element contains the following element:</span></span>

| <span data-ttu-id="26b92-351">Element</span><span class="sxs-lookup"><span data-stu-id="26b92-351">Element</span></span> | <span data-ttu-id="26b92-352">Occurrences</span><span class="sxs-lookup"><span data-stu-id="26b92-352">Occurrences</span></span> | <span data-ttu-id="26b92-353">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-353">Description</span></span> |
| ------- | ----------- | ----------- |
| <span data-ttu-id="26b92-354">ValidationTechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="26b92-354">ValidationTechnicalProfile</span></span> | <span data-ttu-id="26b92-355">1:n</span><span class="sxs-lookup"><span data-stu-id="26b92-355">1:n</span></span> | <span data-ttu-id="26b92-356">The identifiers of technical profiles that are used validate some or all of the output claims of the referencing technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-356">The identifiers of technical profiles that are used validate some or all of the output claims of the referencing technical profile.</span></span> <span data-ttu-id="26b92-357">All of the input claims of the referenced technical profile must appear in the output claims of the referencing technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-357">All of the input claims of the referenced technical profile must appear in the output claims of the referencing technical profile.</span></span> |

#### <a name="validationtechnicalprofile"></a><span data-ttu-id="26b92-358">ValidationTechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="26b92-358">ValidationTechnicalProfile</span></span>

<span data-ttu-id="26b92-359">The **ValidationTechnicalProfile** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-359">The **ValidationTechnicalProfile** element contains the following attribute:</span></span>

| <span data-ttu-id="26b92-360">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-360">Attribute</span></span> | <span data-ttu-id="26b92-361">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-361">Required</span></span> | <span data-ttu-id="26b92-362">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-362">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-363">ReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-363">ReferenceId</span></span> | <span data-ttu-id="26b92-364">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-364">Yes</span></span> | <span data-ttu-id="26b92-365">An identifier of a technical profile already defined in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-365">An identifier of a technical profile already defined in the policy file or parent policy file.</span></span> |

###  <a name="subjectnaminginfo"></a><span data-ttu-id="26b92-366">SubjectNamingInfo</span><span class="sxs-lookup"><span data-stu-id="26b92-366">SubjectNamingInfo</span></span>

<span data-ttu-id="26b92-367">The **SubjectNamingInfo** contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-367">The **SubjectNamingInfo** contains the following attribute:</span></span>

| <span data-ttu-id="26b92-368">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-368">Attribute</span></span> | <span data-ttu-id="26b92-369">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-369">Required</span></span> | <span data-ttu-id="26b92-370">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-370">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-371">ClaimType</span><span class="sxs-lookup"><span data-stu-id="26b92-371">ClaimType</span></span> | <span data-ttu-id="26b92-372">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-372">Yes</span></span> | <span data-ttu-id="26b92-373">An identifier of a claim type already defined in the ClaimsSchema section in the policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-373">An identifier of a claim type already defined in the ClaimsSchema section in the policy file.</span></span> |

### <a name="includetechnicalprofile"></a><span data-ttu-id="26b92-374">IncludeTechnicalProfile</span><span class="sxs-lookup"><span data-stu-id="26b92-374">IncludeTechnicalProfile</span></span>

<span data-ttu-id="26b92-375">The **IncludeTechnicalProfile** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-375">The **IncludeTechnicalProfile** element contains the following attribute:</span></span>

| <span data-ttu-id="26b92-376">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-376">Attribute</span></span> | <span data-ttu-id="26b92-377">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-377">Required</span></span> | <span data-ttu-id="26b92-378">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-378">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-379">ReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-379">ReferenceId</span></span> | <span data-ttu-id="26b92-380">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-380">Yes</span></span> | <span data-ttu-id="26b92-381">An identifier of a technical profile already defined in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-381">An identifier of a technical profile already defined in the policy file or parent policy file.</span></span> |

### <a name="usetechnicalprofileforsessionmanagement"></a><span data-ttu-id="26b92-382">UseTechnicalProfileForSessionManagement</span><span class="sxs-lookup"><span data-stu-id="26b92-382">UseTechnicalProfileForSessionManagement</span></span>

<span data-ttu-id="26b92-383">The **UseTechnicalProfileForSessionManagement** element contains the following attribute:</span><span class="sxs-lookup"><span data-stu-id="26b92-383">The **UseTechnicalProfileForSessionManagement** element contains the following attribute:</span></span>

| <span data-ttu-id="26b92-384">Attribute</span><span class="sxs-lookup"><span data-stu-id="26b92-384">Attribute</span></span> | <span data-ttu-id="26b92-385">Required</span><span class="sxs-lookup"><span data-stu-id="26b92-385">Required</span></span> | <span data-ttu-id="26b92-386">Description</span><span class="sxs-lookup"><span data-stu-id="26b92-386">Description</span></span> |
| --------- | -------- | ----------- |
| <span data-ttu-id="26b92-387">ReferenceId</span><span class="sxs-lookup"><span data-stu-id="26b92-387">ReferenceId</span></span> | <span data-ttu-id="26b92-388">Yes</span><span class="sxs-lookup"><span data-stu-id="26b92-388">Yes</span></span> | <span data-ttu-id="26b92-389">An identifier of a technical profile already defined in the policy file or parent policy file.</span><span class="sxs-lookup"><span data-stu-id="26b92-389">An identifier of a technical profile already defined in the policy file or parent policy file.</span></span> |

### <a name="enabledforuserjourneys"></a><span data-ttu-id="26b92-390">EnabledForUserJourneys</span><span class="sxs-lookup"><span data-stu-id="26b92-390">EnabledForUserJourneys</span></span>
<span data-ttu-id="26b92-391">The **ClaimsProviderSelections** in a user journey defines the list of claims provider selection options and their order.</span><span class="sxs-lookup"><span data-stu-id="26b92-391">The **ClaimsProviderSelections** in a user journey defines the list of claims provider selection options and their order.</span></span> <span data-ttu-id="26b92-392">With the **EnabledForUserJourneys** element  you filter, which claims provider is avaible to the user.</span><span class="sxs-lookup"><span data-stu-id="26b92-392">With the **EnabledForUserJourneys** element  you filter, which claims provider is avaible to the user.</span></span> <span data-ttu-id="26b92-393">The **EnabledForUserJourneys** element contains one of the following values:</span><span class="sxs-lookup"><span data-stu-id="26b92-393">The **EnabledForUserJourneys** element contains one of the following values:</span></span>

- <span data-ttu-id="26b92-394">**Always**, execute the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-394">**Always**, execute the technical profile.</span></span>
- <span data-ttu-id="26b92-395">**Never**, skip the technical profile.</span><span class="sxs-lookup"><span data-stu-id="26b92-395">**Never**, skip the technical profile.</span></span> 
- <span data-ttu-id="26b92-396">**OnClaimsExistence** execute only when a certain claim, specified in the technical profile exists.</span><span class="sxs-lookup"><span data-stu-id="26b92-396">**OnClaimsExistence** execute only when a certain claim, specified in the technical profile exists.</span></span> 
- <span data-ttu-id="26b92-397">**OnItemExistenceInStringCollectionClaim**, execute only when an item exists in a string collection claim.</span><span class="sxs-lookup"><span data-stu-id="26b92-397">**OnItemExistenceInStringCollectionClaim**, execute only when an item exists in a string collection claim.</span></span> 
- <span data-ttu-id="26b92-398">**OnItemAbsenceInStringCollectionClaim** execute only when an item does not exist in a string collection claim.</span><span class="sxs-lookup"><span data-stu-id="26b92-398">**OnItemAbsenceInStringCollectionClaim** execute only when an item does not exist in a string collection claim.</span></span>

<span data-ttu-id="26b92-399">Using **OnClaimsExistence**, **OnItemExistenceInStringCollectionClaim** or **OnItemAbsenceInStringCollectionClaim**, requires you to provide the following metadata: **ClaimTypeOnWhichToEnable** specifies the claim's type that is to be evaluated, **ClaimValueOnWhichToEnable** specifies the value that is to be compared.</span><span class="sxs-lookup"><span data-stu-id="26b92-399">Using **OnClaimsExistence**, **OnItemExistenceInStringCollectionClaim** or **OnItemAbsenceInStringCollectionClaim**, requires you to provide the following metadata: **ClaimTypeOnWhichToEnable** specifies the claim's type that is to be evaluated, **ClaimValueOnWhichToEnable** specifies the value that is to be compared.</span></span>

<span data-ttu-id="26b92-400">The following technical profile is executed only if the **identityProviders** string collection contains the value of `facebook.com`:</span><span class="sxs-lookup"><span data-stu-id="26b92-400">The following technical profile is executed only if the **identityProviders** string collection contains the value of `facebook.com`:</span></span>

```XML
<TechnicalProfile Id="UnLink-Facebook-OAUTH">
  <DisplayName>Unlink Facebook</DisplayName>
...
    <Metadata>
        <Item Key="ClaimTypeOnWhichToEnable">identityProviders</Item>
        <Item Key="ClaimValueOnWhichToEnable">facebook.com</Item>
    </Metadata>        
...
  <EnabledForUserJourneys>OnItemExistenceInStringCollectionClaim</EnabledForUserJourneys>
</TechnicalProfile>  
```












