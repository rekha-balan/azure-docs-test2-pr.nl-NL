---
title: Define a Claims transformation technical profile in a custom policy in Azure Active Directory B2C | Microsoft Docs
description: Define a Claims transformation technical profile in a custom policy in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: fd1e2aa5162ce9263d521edf3ae11e0508353b46
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857880"
---
# <a name="define-a-claims-transformation-technical-profile-in-an-azure-active-directory-b2c-custom-policy"></a><span data-ttu-id="0b822-103">Define a claims transformation technical profile in an Azure Active Directory B2C custom policy</span><span class="sxs-lookup"><span data-stu-id="0b822-103">Define a claims transformation technical profile in an Azure Active Directory B2C custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

 <span data-ttu-id="0b822-104">A claims transformation technical profile enables you to call output claims transformations to manipulate claims values, validate claims, or set default values for a set of output claims.</span><span class="sxs-lookup"><span data-stu-id="0b822-104">A claims transformation technical profile enables you to call output claims transformations to manipulate claims values, validate claims, or set default values for a set of output claims.</span></span>

## <a name="protocol"></a><span data-ttu-id="0b822-105">Protocol</span><span class="sxs-lookup"><span data-stu-id="0b822-105">Protocol</span></span>

<span data-ttu-id="0b822-106">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span><span class="sxs-lookup"><span data-stu-id="0b822-106">The **Name** attribute of the **Protocol** element needs to be set to `Proprietary`.</span></span> <span data-ttu-id="0b822-107">The **handler** attribute must contain the fully qualified name of the protocol handler assembly that is used by Azure AD B2C: `Web.TPEngine.Providers.ClaimsTransformationProtocolProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`.</span><span class="sxs-lookup"><span data-stu-id="0b822-107">The **handler** attribute must contain the fully qualified name of the protocol handler assembly that is used by Azure AD B2C: `Web.TPEngine.Providers.ClaimsTransformationProtocolProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`.</span></span>

<span data-ttu-id="0b822-108">The following example shows a claims transformation technical profile:</span><span class="sxs-lookup"><span data-stu-id="0b822-108">The following example shows a claims transformation technical profile:</span></span>

```XML
<TechnicalProfile Id="Facebook-OAUTH-UnLink">
    <DisplayName>Unlink Facebook</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.ClaimsTransformationProtocolProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  ...    
```

## <a name="output-claims"></a><span data-ttu-id="0b822-109">Output claims</span><span class="sxs-lookup"><span data-stu-id="0b822-109">Output claims</span></span>

<span data-ttu-id="0b822-110">The **OutputClaims** element is mandatory.</span><span class="sxs-lookup"><span data-stu-id="0b822-110">The **OutputClaims** element is mandatory.</span></span> <span data-ttu-id="0b822-111">You should provide at least one output claim returned by the technical profile.</span><span class="sxs-lookup"><span data-stu-id="0b822-111">You should provide at least one output claim returned by the technical profile.</span></span> <span data-ttu-id="0b822-112">The following example shows how to set default values in the output claims:</span><span class="sxs-lookup"><span data-stu-id="0b822-112">The following example shows how to set default values in the output claims:</span></span>

```xml
<OutputClaims>
  <OutputClaim ClaimTypeReferenceId="ageGroup" DefaultValue="Undefined" />
  <OutputClaim ClaimTypeReferenceId="ageGroupValueChanged" DefaultValue="false" />
</OutputClaims>
```

## <a name="output-claims-transformations"></a><span data-ttu-id="0b822-113">Output claims transformations</span><span class="sxs-lookup"><span data-stu-id="0b822-113">Output claims transformations</span></span>

<span data-ttu-id="0b822-114">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify claims or generate new ones.</span><span class="sxs-lookup"><span data-stu-id="0b822-114">The **OutputClaimsTransformations** element may contain a collection of **OutputClaimsTransformation** elements that are used to modify claims or generate new ones.</span></span> <span data-ttu-id="0b822-115">The following technical profile calls the **RemoveAlternativeSecurityIdByIdentityProvider** claims transformation.</span><span class="sxs-lookup"><span data-stu-id="0b822-115">The following technical profile calls the **RemoveAlternativeSecurityIdByIdentityProvider** claims transformation.</span></span> <span data-ttu-id="0b822-116">This claims transformation removes a social identify from the collection of **AlternativeSecurityIds**.</span><span class="sxs-lookup"><span data-stu-id="0b822-116">This claims transformation removes a social identify from the collection of **AlternativeSecurityIds**.</span></span> <span data-ttu-id="0b822-117">The output claims of this technical profile are **identityProvider2**, which is set to `facebook.com`, and **AlternativeSecurityIds**, which contains the list of social identities associated with this user after facebook.com identity is removed.</span><span class="sxs-lookup"><span data-stu-id="0b822-117">The output claims of this technical profile are **identityProvider2**, which is set to `facebook.com`, and **AlternativeSecurityIds**, which contains the list of social identities associated with this user after facebook.com identity is removed.</span></span>

```XML
<ClaimsTransformations>
  <ClaimsTransformation Id="RemoveAlternativeSecurityIdByIdentityProvider" 
TransformationMethod="RemoveAlternativeSecurityIdByIdentityProvider">
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="IdentityProvider2"
TransformationClaimType="identityProvider" />
      <InputClaim ClaimTypeReferenceId="AlternativeSecurityIds" 
TransformationClaimType="collection" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="AlternativeSecurityIds" 
TransformationClaimType="collection" />
    </OutputClaims>
  </ClaimsTransformation>
</ClaimsTransformations>
...
<TechnicalProfile Id="Facebook-OAUTH-UnLink">
    <DisplayName>Unlink Facebook</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.ClaimsTransformationProtocolProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider2" DefaultValue="facebook.com" AlwaysUseDefaultValue="true" />
    </OutputClaims>
    <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="RemoveAlternativeSecurityIdByIdentityProvider" />
    </OutputClaimsTransformations>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
</TechnicalProfile>
```

<span data-ttu-id="0b822-118">The claims transformation technical profile enables you to execute a claims transformation from any user journey's orchestration step.</span><span class="sxs-lookup"><span data-stu-id="0b822-118">The claims transformation technical profile enables you to execute a claims transformation from any user journey's orchestration step.</span></span> <span data-ttu-id="0b822-119">In the following example, the orchestration step calls one of the unlink technical profiles, such as **UnLink-Facebook-OAUTH**.</span><span class="sxs-lookup"><span data-stu-id="0b822-119">In the following example, the orchestration step calls one of the unlink technical profiles, such as **UnLink-Facebook-OAUTH**.</span></span> <span data-ttu-id="0b822-120">This technical profile calls the claims transformation technical profile **RemoveAlternativeSecurityIdByIdentityProvider**, which generates  a new **AlternativeSecurityIds2** claim that contains the list of user social identities, while removing the Facebook identity from the collections.</span><span class="sxs-lookup"><span data-stu-id="0b822-120">This technical profile calls the claims transformation technical profile **RemoveAlternativeSecurityIdByIdentityProvider**, which generates  a new **AlternativeSecurityIds2** claim that contains the list of user social identities, while removing the Facebook identity from the collections.</span></span>

```XML
<UserJourney Id="AccountUnLink">
  <OrchestrationSteps>    
    ...
    <OrchestrationStep Order="8" Type="ClaimsExchange">
      <ClaimsExchanges>
        <ClaimsExchange Id="UnLinkFacebookExchange" TechnicalProfileReferenceId="UnLink-Facebook-OAUTH" />
        <ClaimsExchange Id="UnLinkMicrosoftExchange" TechnicalProfileReferenceId="UnLink-Microsoft-OAUTH" />
        <ClaimsExchange Id="UnLinkGitHubExchange" TechnicalProfileReferenceId="UnLink-GitHub-OAUTH" />
      </ClaimsExchanges>
    </OrchestrationStep>
    ...
  </OrchestrationSteps>
</UserJourney>
```


## <a name="use-a-validation-technical-profile"></a><span data-ttu-id="0b822-121">Use a validation technical profile</span><span class="sxs-lookup"><span data-stu-id="0b822-121">Use a validation technical profile</span></span>

<span data-ttu-id="0b822-122">A claims transformation technical profile can be used to validate information.</span><span class="sxs-lookup"><span data-stu-id="0b822-122">A claims transformation technical profile can be used to validate information.</span></span> <span data-ttu-id="0b822-123">In the following example, the [self asserted technical profile](self-asserted-technical-profile.md) named **LocalAccountSignUpWithLogonEmail** asks the user to enter the email twice, then calls the [validation technical profile](validation-technical-profile.md) named **Validate-Email** to validate the emails.</span><span class="sxs-lookup"><span data-stu-id="0b822-123">In the following example, the [self asserted technical profile](self-asserted-technical-profile.md) named **LocalAccountSignUpWithLogonEmail** asks the user to enter the email twice, then calls the [validation technical profile](validation-technical-profile.md) named **Validate-Email** to validate the emails.</span></span> <span data-ttu-id="0b822-124">The **Validate-Email** technical profile calls the claims transformation **AssertEmailAreEqual** to compare the two claims **email** and **emailRepeat**, and throw an exception if they are not equal according to the specified comparison.</span><span class="sxs-lookup"><span data-stu-id="0b822-124">The **Validate-Email** technical profile calls the claims transformation **AssertEmailAreEqual** to compare the two claims **email** and **emailRepeat**, and throw an exception if they are not equal according to the specified comparison.</span></span>

```XML
<ClaimsTransformations>
  <ClaimsTransformation Id="AssertEmailAreEqual" TransformationMethod="AssertStringClaimsAreEqual">
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" TransformationClaimType="inputClaim1" />
      <InputClaim ClaimTypeReferenceId="emailRepeat" TransformationClaimType="inputClaim2" />
    </InputClaims>
    <InputParameters>
      <InputParameter Id="stringComparison" DataType="string" Value="ordinalIgnoreCase" />
    </InputParameters>
  </ClaimsTransformation>
</ClaimsTransformations>
```

<span data-ttu-id="0b822-125">The claims transformation technical profile calls the **AssertEmailAreEqual** claims transformation, which asserts that emails provided by the user are same.</span><span class="sxs-lookup"><span data-stu-id="0b822-125">The claims transformation technical profile calls the **AssertEmailAreEqual** claims transformation, which asserts that emails provided by the user are same.</span></span>

```XML
<TechnicalProfile Id="Validate-Email">
    <DisplayName>Unlink Facebook</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.ClaimsTransformationProtocolProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="emailRepeat" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="email" />
  </OutputClaims>          
  <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="AssertEmailAreEqual" />
    </OutputClaimsTransformations>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
</TechnicalProfile> 
```

<span data-ttu-id="0b822-126">A self-asserted technical profile can call the validation technical profile and show the error message as specified in the **UserMessageIfClaimsTransformationStringsAreNotEqual** metadata.</span><span class="sxs-lookup"><span data-stu-id="0b822-126">A self-asserted technical profile can call the validation technical profile and show the error message as specified in the **UserMessageIfClaimsTransformationStringsAreNotEqual** metadata.</span></span>

```XML
<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
  <DisplayName>User ID signup</DisplayName>
  <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  <Metadata>
    ...
    <Item Key="UserMessageIfClaimsTransformationStringsAreNotEqual">The email addresses you provided are not the same</Item>
  </Metadata>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="email" />
    <OutputClaim ClaimTypeReferenceId="emailRepeat" />
    ...
  </OutputClaims>
  <ValidationTechnicalProfiles>
    <ValidationTechnicalProfile ReferenceId="Validate-Email" />
  </ValidationTechnicalProfiles>
</TechnicalProfile>  
```