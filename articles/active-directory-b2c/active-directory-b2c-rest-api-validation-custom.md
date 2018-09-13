---
title: REST API claims exchanges as validation in Azure Active Directory B2C | Microsoft Docs
description: A topic on Azure Active Directory B2C custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/24/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: b4fda38834782be502e2581b7b3d1097000b07bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871374"
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="c7b5c-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span><span class="sxs-lookup"><span data-stu-id="c7b5c-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c7b5c-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="c7b5c-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="c7b5c-106">The IEF sends data in claims and receives data back in claims.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="c7b5c-107">The interaction with the API:</span><span class="sxs-lookup"><span data-stu-id="c7b5c-107">The interaction with the API:</span></span>

- <span data-ttu-id="c7b5c-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="c7b5c-109">Typically validates input from the user.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-109">Typically validates input from the user.</span></span> <span data-ttu-id="c7b5c-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="c7b5c-111">You can also design the interaction as an orchestration step.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="c7b5c-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c7b5c-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="c7b5c-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="c7b5c-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7b5c-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7b5c-115">Prerequisites</span></span>

- <span data-ttu-id="c7b5c-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c7b5c-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="c7b5c-117">A REST API endpoint to interact with.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="c7b5c-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="c7b5c-119">Step 1: Prepare the REST API function</span><span class="sxs-lookup"><span data-stu-id="c7b5c-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="c7b5c-120">Setup of REST API functions is outside the scope of this article.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="c7b5c-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="c7b5c-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="c7b5c-123">The function validates whether this claim exists.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="c7b5c-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="c7b5c-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="c7b5c-125">The IEF expects the `userMessage` claim that the Azure function returns.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="c7b5c-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="c7b5c-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span><span class="sxs-lookup"><span data-stu-id="c7b5c-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="c7b5c-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="c7b5c-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="c7b5c-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="c7b5c-131">Consider it as the function that will interact with the external service.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="c7b5c-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="c7b5c-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="c7b5c-134">In this example, the IEF does not expect claims back.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="c7b5c-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="c7b5c-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span><span class="sxs-lookup"><span data-stu-id="c7b5c-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="c7b5c-137">The most common use of the validation step is in the interaction with a user.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="c7b5c-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="c7b5c-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="c7b5c-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="c7b5c-141">To add the claims exchange to the self-asserted technical profile:</span><span class="sxs-lookup"><span data-stu-id="c7b5c-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="c7b5c-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="c7b5c-143">Review the configuration of this technical profile.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="c7b5c-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span><span class="sxs-lookup"><span data-stu-id="c7b5c-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="c7b5c-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 4 of `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 4 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="c7b5c-146">Step 4: Upload and test the profile edit RP policy file</span><span class="sxs-lookup"><span data-stu-id="c7b5c-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="c7b5c-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="c7b5c-148">Use **Run now** to test the profile edit RP policy file.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="c7b5c-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="c7b5c-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span><span class="sxs-lookup"><span data-stu-id="c7b5c-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7b5c-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7b5c-151">Next steps</span></span>

[<span data-ttu-id="c7b5c-152">Modify the profile edit and user registration to gather additional information from your users</span><span class="sxs-lookup"><span data-stu-id="c7b5c-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="c7b5c-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span><span class="sxs-lookup"><span data-stu-id="c7b5c-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
