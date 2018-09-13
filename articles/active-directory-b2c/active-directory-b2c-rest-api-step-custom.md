---
title: REST API claims exchanges as an orchestration step in Azure Active Directory B2C | Microsoft Docs
description: A topic on Azure Active Directory B2C custom policies that integrate with an API.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/24/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: dddb42f53d4bb59113df937799bd4de10d31491c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967135"
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="9077f-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span><span class="sxs-lookup"><span data-stu-id="9077f-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="9077f-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span><span class="sxs-lookup"><span data-stu-id="9077f-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="9077f-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span><span class="sxs-lookup"><span data-stu-id="9077f-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="9077f-106">The IEF sends data in claims and receives data back in claims.</span><span class="sxs-lookup"><span data-stu-id="9077f-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="9077f-107">The REST API claims exchange:</span><span class="sxs-lookup"><span data-stu-id="9077f-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="9077f-108">Can be designed as an orchestration step.</span><span class="sxs-lookup"><span data-stu-id="9077f-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="9077f-109">Can trigger an external action.</span><span class="sxs-lookup"><span data-stu-id="9077f-109">Can trigger an external action.</span></span> <span data-ttu-id="9077f-110">For instance, it can log an event in an external database.</span><span class="sxs-lookup"><span data-stu-id="9077f-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="9077f-111">Can be used to fetch a value and then store it in the user database.</span><span class="sxs-lookup"><span data-stu-id="9077f-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="9077f-112">You can use the received claims later to change the flow of execution.</span><span class="sxs-lookup"><span data-stu-id="9077f-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="9077f-113">You can also design the interaction as a validation profile.</span><span class="sxs-lookup"><span data-stu-id="9077f-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="9077f-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9077f-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="9077f-115">The scenario is that when a user performs a profile edit, we want to:</span><span class="sxs-lookup"><span data-stu-id="9077f-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="9077f-116">Look up the user in an external system.</span><span class="sxs-lookup"><span data-stu-id="9077f-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="9077f-117">Get the city where that user is registered.</span><span class="sxs-lookup"><span data-stu-id="9077f-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="9077f-118">Return that attribute to the application as a claim.</span><span class="sxs-lookup"><span data-stu-id="9077f-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9077f-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9077f-119">Prerequisites</span></span>

- <span data-ttu-id="9077f-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9077f-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="9077f-121">A REST API endpoint to interact with.</span><span class="sxs-lookup"><span data-stu-id="9077f-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="9077f-122">This walkthrough uses a simple Azure function app webhook as an example.</span><span class="sxs-lookup"><span data-stu-id="9077f-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="9077f-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9077f-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="9077f-124">Step 1: Prepare the REST API function</span><span class="sxs-lookup"><span data-stu-id="9077f-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="9077f-125">Setup of REST API functions is outside the scope of this article.</span><span class="sxs-lookup"><span data-stu-id="9077f-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="9077f-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span><span class="sxs-lookup"><span data-stu-id="9077f-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="9077f-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="9077f-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="9077f-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="9077f-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="9077f-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span><span class="sxs-lookup"><span data-stu-id="9077f-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="9077f-130">You can potentially use it as a message passed to the application and presented to the user later.</span><span class="sxs-lookup"><span data-stu-id="9077f-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

<span data-ttu-id="9077f-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span><span class="sxs-lookup"><span data-stu-id="9077f-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="9077f-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="9077f-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="9077f-133">You can use it for testing.</span><span class="sxs-lookup"><span data-stu-id="9077f-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="9077f-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span><span class="sxs-lookup"><span data-stu-id="9077f-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="9077f-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span><span class="sxs-lookup"><span data-stu-id="9077f-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="9077f-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span><span class="sxs-lookup"><span data-stu-id="9077f-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="9077f-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span><span class="sxs-lookup"><span data-stu-id="9077f-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="9077f-138">Consider it as the function that will interact with the external service.</span><span class="sxs-lookup"><span data-stu-id="9077f-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="9077f-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span><span class="sxs-lookup"><span data-stu-id="9077f-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="9077f-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span><span class="sxs-lookup"><span data-stu-id="9077f-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="9077f-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span><span class="sxs-lookup"><span data-stu-id="9077f-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="9077f-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span><span class="sxs-lookup"><span data-stu-id="9077f-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="9077f-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span><span class="sxs-lookup"><span data-stu-id="9077f-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="9077f-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span><span class="sxs-lookup"><span data-stu-id="9077f-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="9077f-145">The claim `city` is not yet defined anywhere in our schema.</span><span class="sxs-lookup"><span data-stu-id="9077f-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="9077f-146">So, add a definition inside the element `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="9077f-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="9077f-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span><span class="sxs-lookup"><span data-stu-id="9077f-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="9077f-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="9077f-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="9077f-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span><span class="sxs-lookup"><span data-stu-id="9077f-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="9077f-150">There are many use cases where the REST API call can be used as an orchestration step.</span><span class="sxs-lookup"><span data-stu-id="9077f-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="9077f-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span><span class="sxs-lookup"><span data-stu-id="9077f-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="9077f-152">In this case, it's used to augment the information provided to the application after the profile edit.</span><span class="sxs-lookup"><span data-stu-id="9077f-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="9077f-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="9077f-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="9077f-154">Then make the modification under step 6.</span><span class="sxs-lookup"><span data-stu-id="9077f-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="9077f-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="9077f-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="9077f-156">The final XML for the user journey should look like this:</span><span class="sxs-lookup"><span data-stu-id="9077f-156">The final XML for the user journey should look like this:</span></span>

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 to the user journey before the JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="9077f-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span><span class="sxs-lookup"><span data-stu-id="9077f-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="9077f-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="9077f-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="9077f-159">After you add the new claim, the technical profile looks like this:</span><span class="sxs-lookup"><span data-stu-id="9077f-159">After you add the new claim, the technical profile looks like this:</span></span>

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="9077f-160">Step 6: Upload your changes and test</span><span class="sxs-lookup"><span data-stu-id="9077f-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="9077f-161">Overwrite the existing versions of the policy.</span><span class="sxs-lookup"><span data-stu-id="9077f-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="9077f-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span><span class="sxs-lookup"><span data-stu-id="9077f-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="9077f-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span><span class="sxs-lookup"><span data-stu-id="9077f-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="9077f-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="9077f-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="9077f-165">Upload the extensions file.</span><span class="sxs-lookup"><span data-stu-id="9077f-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="9077f-166">Upload the policy edit RP file.</span><span class="sxs-lookup"><span data-stu-id="9077f-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="9077f-167">Use **Run Now** to test the policy.</span><span class="sxs-lookup"><span data-stu-id="9077f-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="9077f-168">Review the token that the IEF returns to the application.</span><span class="sxs-lookup"><span data-stu-id="9077f-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="9077f-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="9077f-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://contoso.b2clogin.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="9077f-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="9077f-170">Next steps</span></span>

[<span data-ttu-id="9077f-171">Use a REST API as a validation step</span><span class="sxs-lookup"><span data-stu-id="9077f-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="9077f-172">Modify the profile edit to gather additional information from your users</span><span class="sxs-lookup"><span data-stu-id="9077f-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
