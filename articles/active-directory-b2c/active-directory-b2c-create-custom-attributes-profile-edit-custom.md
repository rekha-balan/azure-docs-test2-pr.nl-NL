---
title: Add your own attributes to custom policies in Azure Active Directory B2C | Microsoft Docs
description: A walkthrough on using extension properties and custom attributes and including them in the user interface.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/04/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 5513e0ff434862ea7eee42cb94ff2a0f67f6d390
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866297"
---
# <a name="azure-active-directory-b2c-use-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="feb50-103">Azure Active Directory B2C: Use custom attributes in a custom profile edit policy</span><span class="sxs-lookup"><span data-stu-id="feb50-103">Azure Active Directory B2C: Use custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="feb50-104">In this article, you create a custom attribute in your Azure Active Directory (Azure AD) B2C directory.</span><span class="sxs-lookup"><span data-stu-id="feb50-104">In this article, you create a custom attribute in your Azure Active Directory (Azure AD) B2C directory.</span></span> <span data-ttu-id="feb50-105">You'll use this new attribute as a custom claim in the profile edit user journey.</span><span class="sxs-lookup"><span data-stu-id="feb50-105">You'll use this new attribute as a custom claim in the profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="feb50-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="feb50-106">Prerequisites</span></span>

<span data-ttu-id="feb50-107">Follow the steps in the article [Azure Active Directory B2C: Get started with custom policies](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="feb50-107">Follow the steps in the article [Azure Active Directory B2C: Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-to-collect-information-about-your-customers-in-azure-ad-b2c-by-using-custom-policies"></a><span data-ttu-id="feb50-108">Use custom attributes to collect information about your customers in Azure AD B2C by using custom policies</span><span class="sxs-lookup"><span data-stu-id="feb50-108">Use custom attributes to collect information about your customers in Azure AD B2C by using custom policies</span></span>
<span data-ttu-id="feb50-109">Your Azure AD B2C directory comes with a built-in set of attributes.</span><span class="sxs-lookup"><span data-stu-id="feb50-109">Your Azure AD B2C directory comes with a built-in set of attributes.</span></span> <span data-ttu-id="feb50-110">Examples are **Given Name**, **Surname**, **City**, **Postal Code**, and **userPrincipalName**.</span><span class="sxs-lookup"><span data-stu-id="feb50-110">Examples are **Given Name**, **Surname**, **City**, **Postal Code**, and **userPrincipalName**.</span></span> <span data-ttu-id="feb50-111">You often need to create your own attributes like these examples:</span><span class="sxs-lookup"><span data-stu-id="feb50-111">You often need to create your own attributes like these examples:</span></span>
* <span data-ttu-id="feb50-112">A customer-facing application needs to persist for an attribute like **LoyaltyNumber.**</span><span class="sxs-lookup"><span data-stu-id="feb50-112">A customer-facing application needs to persist for an attribute like **LoyaltyNumber.**</span></span>
* <span data-ttu-id="feb50-113">An identity provider has a unique user identifier like **uniqueUserGUID** that must be saved.</span><span class="sxs-lookup"><span data-stu-id="feb50-113">An identity provider has a unique user identifier like **uniqueUserGUID** that must be saved.</span></span>
* <span data-ttu-id="feb50-114">A custom user journey needs to persist for a state of a user like **migrationStatus**.</span><span class="sxs-lookup"><span data-stu-id="feb50-114">A custom user journey needs to persist for a state of a user like **migrationStatus**.</span></span>

<span data-ttu-id="feb50-115">Azure AD B2C extends the set of attributes stored on each user account.</span><span class="sxs-lookup"><span data-stu-id="feb50-115">Azure AD B2C extends the set of attributes stored on each user account.</span></span> <span data-ttu-id="feb50-116">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="feb50-116">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="feb50-117">Extension properties extend the schema of the user objects in the directory.</span><span class="sxs-lookup"><span data-stu-id="feb50-117">Extension properties extend the schema of the user objects in the directory.</span></span> <span data-ttu-id="feb50-118">The terms *extension property*, *custom attribute*, and *custom claim* refer to the same thing in the context of this article.</span><span class="sxs-lookup"><span data-stu-id="feb50-118">The terms *extension property*, *custom attribute*, and *custom claim* refer to the same thing in the context of this article.</span></span> <span data-ttu-id="feb50-119">The name varies depending on the context, such as application, object, or policy.</span><span class="sxs-lookup"><span data-stu-id="feb50-119">The name varies depending on the context, such as application, object, or policy.</span></span>

<span data-ttu-id="feb50-120">Extension properties can only be registered on an application object even though they might contain data for a user.</span><span class="sxs-lookup"><span data-stu-id="feb50-120">Extension properties can only be registered on an application object even though they might contain data for a user.</span></span> <span data-ttu-id="feb50-121">The property is attached to the application.</span><span class="sxs-lookup"><span data-stu-id="feb50-121">The property is attached to the application.</span></span> <span data-ttu-id="feb50-122">The application object must have write access to register an extension property.</span><span class="sxs-lookup"><span data-stu-id="feb50-122">The application object must have write access to register an extension property.</span></span> <span data-ttu-id="feb50-123">A hundred extension properties, across all types and all applications, can be written to any single object.</span><span class="sxs-lookup"><span data-stu-id="feb50-123">A hundred extension properties, across all types and all applications, can be written to any single object.</span></span> <span data-ttu-id="feb50-124">Extension properties are added to the target directory type and become immediately accessible in the Azure AD B2C directory tenant.</span><span class="sxs-lookup"><span data-stu-id="feb50-124">Extension properties are added to the target directory type and become immediately accessible in the Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="feb50-125">If the application is deleted, those extension properties along with any data contained in them for all users are also removed.</span><span class="sxs-lookup"><span data-stu-id="feb50-125">If the application is deleted, those extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="feb50-126">If an extension property is deleted by the application, it's removed on the target directory objects, and the values are deleted.</span><span class="sxs-lookup"><span data-stu-id="feb50-126">If an extension property is deleted by the application, it's removed on the target directory objects, and the values are deleted.</span></span>

<span data-ttu-id="feb50-127">Extension properties exist only in the context of a registered application in the tenant.</span><span class="sxs-lookup"><span data-stu-id="feb50-127">Extension properties exist only in the context of a registered application in the tenant.</span></span> <span data-ttu-id="feb50-128">The object ID of that application must be included in the **TechnicalProfile** that uses it.</span><span class="sxs-lookup"><span data-stu-id="feb50-128">The object ID of that application must be included in the **TechnicalProfile** that uses it.</span></span>

>[!NOTE]
><span data-ttu-id="feb50-129">The Azure AD B2C directory typically includes a web app named `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="feb50-129">The Azure AD B2C directory typically includes a web app named `b2c-extensions-app`.</span></span> <span data-ttu-id="feb50-130">This application is primarily used by the B2C built-in policies for the custom claims created via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="feb50-130">This application is primarily used by the B2C built-in policies for the custom claims created via the Azure portal.</span></span> <span data-ttu-id="feb50-131">We recommend that only advanced users register extensions for B2C custom policies by using this application.</span><span class="sxs-lookup"><span data-stu-id="feb50-131">We recommend that only advanced users register extensions for B2C custom policies by using this application.</span></span>  
<span data-ttu-id="feb50-132">Instructions are included in the **Next steps** section in this article.</span><span class="sxs-lookup"><span data-stu-id="feb50-132">Instructions are included in the **Next steps** section in this article.</span></span>


## <a name="create-a-new-application-to-store-the-extension-properties"></a><span data-ttu-id="feb50-133">Create a new application to store the extension properties</span><span class="sxs-lookup"><span data-stu-id="feb50-133">Create a new application to store the extension properties</span></span>

1. <span data-ttu-id="feb50-134">Open a browsing session and navigate to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="feb50-134">Open a browsing session and navigate to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="feb50-135">Sign in with the administrative credentials of the B2C directory you want to configure.</span><span class="sxs-lookup"><span data-stu-id="feb50-135">Sign in with the administrative credentials of the B2C directory you want to configure.</span></span>
2. <span data-ttu-id="feb50-136">Select **Azure Active Directory** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="feb50-136">Select **Azure Active Directory** on the left navigation menu.</span></span> <span data-ttu-id="feb50-137">You might need to find it by selecting **More services**.</span><span class="sxs-lookup"><span data-stu-id="feb50-137">You might need to find it by selecting **More services**.</span></span>
3. <span data-ttu-id="feb50-138">Select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="feb50-138">Select **App registrations**.</span></span> <span data-ttu-id="feb50-139">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="feb50-139">Select **New application registration**.</span></span>
4. <span data-ttu-id="feb50-140">Provide the following entries:</span><span class="sxs-lookup"><span data-stu-id="feb50-140">Provide the following entries:</span></span>
    * <span data-ttu-id="feb50-141">A name for the web application: **WebApp-GraphAPI-DirectoryExtensions**.</span><span class="sxs-lookup"><span data-stu-id="feb50-141">A name for the web application: **WebApp-GraphAPI-DirectoryExtensions**.</span></span>
    * <span data-ttu-id="feb50-142">The application type: **Web app/API**.</span><span class="sxs-lookup"><span data-stu-id="feb50-142">The application type: **Web app/API**.</span></span>
    * <span data-ttu-id="feb50-143">The sign-on URL: **https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions**.</span><span class="sxs-lookup"><span data-stu-id="feb50-143">The sign-on URL: **https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions**.</span></span>
5. <span data-ttu-id="feb50-144">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="feb50-144">Select **Create**.</span></span>
6. <span data-ttu-id="feb50-145">Select the newly created web application.</span><span class="sxs-lookup"><span data-stu-id="feb50-145">Select the newly created web application.</span></span>
7. <span data-ttu-id="feb50-146">Select **Settings** > **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="feb50-146">Select **Settings** > **Required permissions**.</span></span>
8. <span data-ttu-id="feb50-147">Select the API **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="feb50-147">Select the API **Windows Azure Active Directory**.</span></span>
9. <span data-ttu-id="feb50-148">Enter a checkmark in Application Permissions: **Read and write directory data**.</span><span class="sxs-lookup"><span data-stu-id="feb50-148">Enter a checkmark in Application Permissions: **Read and write directory data**.</span></span> <span data-ttu-id="feb50-149">Then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="feb50-149">Then select **Save**.</span></span>
10. <span data-ttu-id="feb50-150">Choose **Grant permissions** and confirm **Yes**.</span><span class="sxs-lookup"><span data-stu-id="feb50-150">Choose **Grant permissions** and confirm **Yes**.</span></span>
11. <span data-ttu-id="feb50-151">Copy the following identifiers to your clipboard and save them:</span><span class="sxs-lookup"><span data-stu-id="feb50-151">Copy the following identifiers to your clipboard and save them:</span></span>
    * <span data-ttu-id="feb50-152">**Application ID**.</span><span class="sxs-lookup"><span data-stu-id="feb50-152">**Application ID**.</span></span> <span data-ttu-id="feb50-153">Example: `103ee0e6-f92d-4183-b576-8c3739027780`.</span><span class="sxs-lookup"><span data-stu-id="feb50-153">Example: `103ee0e6-f92d-4183-b576-8c3739027780`.</span></span>
    * <span data-ttu-id="feb50-154">**Object ID**.</span><span class="sxs-lookup"><span data-stu-id="feb50-154">**Object ID**.</span></span> <span data-ttu-id="feb50-155">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`.</span><span class="sxs-lookup"><span data-stu-id="feb50-155">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`.</span></span>



## <a name="modify-your-custom-policy-to-add-the-applicationobjectid"></a><span data-ttu-id="feb50-156">Modify your custom policy to add the **ApplicationObjectId**</span><span class="sxs-lookup"><span data-stu-id="feb50-156">Modify your custom policy to add the **ApplicationObjectId**</span></span>

<span data-ttu-id="feb50-157">When you followed the steps in [Azure Active Directory B2C: Get started with custom policies](active-directory-b2c-get-started-custom.md), you downloaded and modified [sample files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) named **TrustFrameworkBase.xml**, **TrustFrameworkExtensions.xml**, **SignUpOrSignin.xml**, **ProfileEdit.xml**, and **PasswordReset.xml**.</span><span class="sxs-lookup"><span data-stu-id="feb50-157">When you followed the steps in [Azure Active Directory B2C: Get started with custom policies](active-directory-b2c-get-started-custom.md), you downloaded and modified [sample files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) named **TrustFrameworkBase.xml**, **TrustFrameworkExtensions.xml**, **SignUpOrSignin.xml**, **ProfileEdit.xml**, and **PasswordReset.xml**.</span></span> <span data-ttu-id="feb50-158">In this step, you make more modifications to those files.</span><span class="sxs-lookup"><span data-stu-id="feb50-158">In this step, you make more modifications to those files.</span></span>

* <span data-ttu-id="feb50-159">Open the **TrustFrameworkBase.xml** file and add the `Metadata` section as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="feb50-159">Open the **TrustFrameworkBase.xml** file and add the `Metadata` section as shown in the following example.</span></span> <span data-ttu-id="feb50-160">Insert the object ID that you previously recorded for the `ApplicationObjectId` value and the application ID that you recorded for the `ClientId` value:</span><span class="sxs-lookup"><span data-stu-id="feb50-160">Insert the object ID that you previously recorded for the `ApplicationObjectId` value and the application ID that you recorded for the `ClientId` value:</span></span> 

    ```xml
    <ClaimsProviders>
        <ClaimsProvider>
          <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
          <DisplayName>Azure Active Directory</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              
          <!-- Provide objectId and appId before using extension properties. -->
          <Metadata>
            <Item Key="ApplicationObjectId">insert objectId here</Item>
            <Item Key="ClientId">insert appId here</Item>
          </Metadata>
          <!-- End of changes -->
              
          <CryptographicKeys>
            <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
          </CryptographicKeys>
          <IncludeInSso>false</IncludeInSso>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
    ```

> [!NOTE]
> <span data-ttu-id="feb50-161">When the **TechnicalProfile** writes for the first time to the newly created extension property, you might experience a one-time error.</span><span class="sxs-lookup"><span data-stu-id="feb50-161">When the **TechnicalProfile** writes for the first time to the newly created extension property, you might experience a one-time error.</span></span> <span data-ttu-id="feb50-162">The extension property is created the first time it's used.</span><span class="sxs-lookup"><span data-stu-id="feb50-162">The extension property is created the first time it's used.</span></span>  

## <a name="use-the-new-extension-property-or-custom-attribute-in-a-user-journey"></a><span data-ttu-id="feb50-163">Use the new extension property or custom attribute in a user journey</span><span class="sxs-lookup"><span data-stu-id="feb50-163">Use the new extension property or custom attribute in a user journey</span></span>

1. <span data-ttu-id="feb50-164">Open the **ProfileEdit.xml** file.</span><span class="sxs-lookup"><span data-stu-id="feb50-164">Open the **ProfileEdit.xml** file.</span></span>
2. <span data-ttu-id="feb50-165">Add a custom claim `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="feb50-165">Add a custom claim `loyaltyId`.</span></span> <span data-ttu-id="feb50-166">By including the custom claim in the `<RelyingParty>` element, it's included in the token for the application.</span><span class="sxs-lookup"><span data-stu-id="feb50-166">By including the custom claim in the `<RelyingParty>` element, it's included in the token for the application.</span></span>
    
    ```xml
    <RelyingParty>
      <DefaultUserJourney ReferenceId="ProfileEdit" />
      <TechnicalProfile Id="PolicyProfile">
        <DisplayName>PolicyProfile</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <OutputClaims>
          <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
          <OutputClaim ClaimTypeReferenceId="city" />

          <!-- Provide the custom claim identifier -->
          <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
          <!-- End of changes -->
        </OutputClaims>
        <SubjectNamingInfo ClaimType="sub" />
      </TechnicalProfile>
    </RelyingParty>
    ```

3. <span data-ttu-id="feb50-167">Open the **TrustFrameworkExtensions.xml** file and add the`<ClaimsSchema>` element and its child elements to the `BuildingBlocks` element:</span><span class="sxs-lookup"><span data-stu-id="feb50-167">Open the **TrustFrameworkExtensions.xml** file and add the`<ClaimsSchema>` element and its child elements to the `BuildingBlocks` element:</span></span>

    ```xml
    <BuildingBlocks>
      <ClaimsSchema> 
        <ClaimType Id="extension_loyaltyId"> 
          <DisplayName>Loyalty Identification Tag</DisplayName> 
          <DataType>string</DataType> 
          <UserHelpText>Your loyalty number from your membership card</UserHelpText> 
          <UserInputType>TextBox</UserInputType> 
        </ClaimType> 
      </ClaimsSchema>
    </BuildingBlocks>
    ```

4. <span data-ttu-id="feb50-168">Add the same `ClaimType` definition to **TrustFrameworkBase.xml**.</span><span class="sxs-lookup"><span data-stu-id="feb50-168">Add the same `ClaimType` definition to **TrustFrameworkBase.xml**.</span></span> <span data-ttu-id="feb50-169">It's not necessary to add a `ClaimType` definition in both the base and the extensions files.</span><span class="sxs-lookup"><span data-stu-id="feb50-169">It's not necessary to add a `ClaimType` definition in both the base and the extensions files.</span></span> <span data-ttu-id="feb50-170">However, the next steps add the `extension_loyaltyId` to **TechnicalProfiles** in the base file.</span><span class="sxs-lookup"><span data-stu-id="feb50-170">However, the next steps add the `extension_loyaltyId` to **TechnicalProfiles** in the base file.</span></span> <span data-ttu-id="feb50-171">So the policy validator rejects the upload of the base file without it.</span><span class="sxs-lookup"><span data-stu-id="feb50-171">So the policy validator rejects the upload of the base file without it.</span></span> <span data-ttu-id="feb50-172">It might be useful to trace the execution of the user journey named **ProfileEdit** in the **TrustFrameworkBase.xml** file.</span><span class="sxs-lookup"><span data-stu-id="feb50-172">It might be useful to trace the execution of the user journey named **ProfileEdit** in the **TrustFrameworkBase.xml** file.</span></span> <span data-ttu-id="feb50-173">Search for the user journey with the same name in your editor.</span><span class="sxs-lookup"><span data-stu-id="feb50-173">Search for the user journey with the same name in your editor.</span></span> <span data-ttu-id="feb50-174">Observe that Orchestration step 5 invokes the **TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate**.</span><span class="sxs-lookup"><span data-stu-id="feb50-174">Observe that Orchestration step 5 invokes the **TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate**.</span></span> <span data-ttu-id="feb50-175">Search and inspect this **TechnicalProfile** to familiarize yourself with the flow.</span><span class="sxs-lookup"><span data-stu-id="feb50-175">Search and inspect this **TechnicalProfile** to familiarize yourself with the flow.</span></span>

5. <span data-ttu-id="feb50-176">Open the **TrustFrameworkBase.xml** file and add `loyaltyId` as an input and output claim in the **TechnicalProfile SelfAsserted-ProfileUpdate**:</span><span class="sxs-lookup"><span data-stu-id="feb50-176">Open the **TrustFrameworkBase.xml** file and add `loyaltyId` as an input and output claim in the **TechnicalProfile SelfAsserted-ProfileUpdate**:</span></span>

    ```xml
    <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
      <DisplayName>User ID signup</DisplayName>
      <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
      <Metadata>
        <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
      </Metadata>
      <IncludeInSso>false</IncludeInSso>
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
        <InputClaim ClaimTypeReferenceId="userPrincipalName" />
        <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />

        <!-- Add the loyalty identifier -->
        <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
        <!-- End of changes -->
      </InputClaims>
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        
        <!-- Add the loyalty identifier -->
        <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
        <!-- End of changes -->

      </OutputClaims>
      <ValidationTechnicalProfiles>
        <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
      </ValidationTechnicalProfiles>
    </TechnicalProfile>
    ```

6. <span data-ttu-id="feb50-177">In the **TrustFrameworkBase.xml** file, add the `loyaltyId` claim to **TechnicalProfile AAD-UserWriteProfileUsingObjectId**.</span><span class="sxs-lookup"><span data-stu-id="feb50-177">In the **TrustFrameworkBase.xml** file, add the `loyaltyId` claim to **TechnicalProfile AAD-UserWriteProfileUsingObjectId**.</span></span> <span data-ttu-id="feb50-178">This addition persists the value of the claim in the extension property for the current user in the directory:</span><span class="sxs-lookup"><span data-stu-id="feb50-178">This addition persists the value of the claim in the extension property for the current user in the directory:</span></span>

    ```xml
    <TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
      <Metadata>
        <Item Key="Operation">Write</Item>
        <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
        <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      </Metadata>
      <IncludeInSso>false</IncludeInSso>
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
      </InputClaims>
      <PersistedClaims>
        <PersistedClaim ClaimTypeReferenceId="objectId" />
        <PersistedClaim ClaimTypeReferenceId="givenName" />
        <PersistedClaim ClaimTypeReferenceId="surname" />

        <!-- Add the loyalty identifier -->
        <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />
        <!-- End of changes -->

      </PersistedClaims>
      <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    </TechnicalProfile>
    ```

7. <span data-ttu-id="feb50-179">In the **TrustFrameworkBase.xml** file, add the `loyaltyId` claim to **TechnicalProfile AAD-UserReadUsingObjectId** to read the value of the extension attribute every time a user signs in.</span><span class="sxs-lookup"><span data-stu-id="feb50-179">In the **TrustFrameworkBase.xml** file, add the `loyaltyId` claim to **TechnicalProfile AAD-UserReadUsingObjectId** to read the value of the extension attribute every time a user signs in.</span></span> <span data-ttu-id="feb50-180">So far, the **TechnicalProfiles** have been changed in the flow of local accounts only.</span><span class="sxs-lookup"><span data-stu-id="feb50-180">So far, the **TechnicalProfiles** have been changed in the flow of local accounts only.</span></span> <span data-ttu-id="feb50-181">If you want the new attribute in the flow of a social or federated account, a different set of **TechnicalProfiles** needs to be changed.</span><span class="sxs-lookup"><span data-stu-id="feb50-181">If you want the new attribute in the flow of a social or federated account, a different set of **TechnicalProfiles** needs to be changed.</span></span> <span data-ttu-id="feb50-182">See the **Next steps** section.</span><span class="sxs-lookup"><span data-stu-id="feb50-182">See the **Next steps** section.</span></span>

    ```xml
    <TechnicalProfile Id="AAD-UserReadUsingObjectId">
      <Metadata>
        <Item Key="Operation">Read</Item>
        <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      </Metadata>
      <IncludeInSso>false</IncludeInSso>
      <InputClaims>
        <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
      </InputClaims>
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="otherMails" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />

        <!-- Add the loyalty identifier -->
        <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
        <!-- End of changes -->

      </OutputClaims>
      <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    </TechnicalProfile>
    ```

## <a name="test-the-custom-policy"></a><span data-ttu-id="feb50-183">Test the custom policy</span><span class="sxs-lookup"><span data-stu-id="feb50-183">Test the custom policy</span></span>

1. <span data-ttu-id="feb50-184">Open the Azure AD B2C blade and navigate to **Identity Experience Framework** > **Custom policies**.</span><span class="sxs-lookup"><span data-stu-id="feb50-184">Open the Azure AD B2C blade and navigate to **Identity Experience Framework** > **Custom policies**.</span></span>
1. <span data-ttu-id="feb50-185">Select the custom policy that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="feb50-185">Select the custom policy that you uploaded.</span></span> <span data-ttu-id="feb50-186">Select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="feb50-186">Select **Run now**.</span></span>
1. <span data-ttu-id="feb50-187">Sign up by using an email address.</span><span class="sxs-lookup"><span data-stu-id="feb50-187">Sign up by using an email address.</span></span>

<span data-ttu-id="feb50-188">The ID token sent back to your application includes the new extension property as a custom claim preceded by **extension_loyaltyId**.</span><span class="sxs-lookup"><span data-stu-id="feb50-188">The ID token sent back to your application includes the new extension property as a custom claim preceded by **extension_loyaltyId**.</span></span> <span data-ttu-id="feb50-189">See the following example:</span><span class="sxs-lookup"><span data-stu-id="feb50-189">See the following example:</span></span>

```json
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://contoso.b2clogin.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="feb50-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="feb50-190">Next steps</span></span>

1. <span data-ttu-id="feb50-191">Add the new claim to the flows to sign in to social accounts by changing the following **TechnicalProfiles**.</span><span class="sxs-lookup"><span data-stu-id="feb50-191">Add the new claim to the flows to sign in to social accounts by changing the following **TechnicalProfiles**.</span></span> <span data-ttu-id="feb50-192">Social and federated accounts use these two **TechnicalProfiles** to sign in.</span><span class="sxs-lookup"><span data-stu-id="feb50-192">Social and federated accounts use these two **TechnicalProfiles** to sign in.</span></span> <span data-ttu-id="feb50-193">They write and read user data by using the **alternativeSecurityId** as the locator of the user object.</span><span class="sxs-lookup"><span data-stu-id="feb50-193">They write and read user data by using the **alternativeSecurityId** as the locator of the user object.</span></span>

  ```xml
    <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

    <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
  ```

2. <span data-ttu-id="feb50-194">Use the same extension attributes between built-in and custom policies.</span><span class="sxs-lookup"><span data-stu-id="feb50-194">Use the same extension attributes between built-in and custom policies.</span></span> <span data-ttu-id="feb50-195">When you add extension, or custom, attributes via the portal experience, those attributes are registered by using the **b2c-extensions-app** that exists in every B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="feb50-195">When you add extension, or custom, attributes via the portal experience, those attributes are registered by using the **b2c-extensions-app** that exists in every B2C tenant.</span></span> <span data-ttu-id="feb50-196">Take the following steps to use extension attributes in your custom policy:</span><span class="sxs-lookup"><span data-stu-id="feb50-196">Take the following steps to use extension attributes in your custom policy:</span></span>

  <span data-ttu-id="feb50-197">a.</span><span class="sxs-lookup"><span data-stu-id="feb50-197">a.</span></span> <span data-ttu-id="feb50-198">Within your B2C tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="feb50-198">Within your B2C tenant in portal.azure.com, navigate to **Azure Active Directory** and select **App registrations**.</span></span>  
  <span data-ttu-id="feb50-199">b.</span><span class="sxs-lookup"><span data-stu-id="feb50-199">b.</span></span> <span data-ttu-id="feb50-200">Find your **b2c-extensions-app** and select it.</span><span class="sxs-lookup"><span data-stu-id="feb50-200">Find your **b2c-extensions-app** and select it.</span></span>  
  <span data-ttu-id="feb50-201">c.</span><span class="sxs-lookup"><span data-stu-id="feb50-201">c.</span></span> <span data-ttu-id="feb50-202">Under **Essentials**, enter the **Application ID** and the **Object ID**.</span><span class="sxs-lookup"><span data-stu-id="feb50-202">Under **Essentials**, enter the **Application ID** and the **Object ID**.</span></span>  
  <span data-ttu-id="feb50-203">d.</span><span class="sxs-lookup"><span data-stu-id="feb50-203">d.</span></span> <span data-ttu-id="feb50-204">Include them in your **AAD-Common** TechnicalProfile metadata:</span><span class="sxs-lookup"><span data-stu-id="feb50-204">Include them in your **AAD-Common** TechnicalProfile metadata:</span></span>  

  ```xml
      <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
                <DisplayName>Azure Active Directory</DisplayName>
                <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
                <!-- Provide objectId and appId before using extension properties. -->
                <Metadata>
                  <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is the "Object ID" from the "b2c-extensions-app"-->
                  <Item Key="ClientId">insert appId here</Item> <!--This is the "Application ID" from the "b2c-extensions-app"-->
                </Metadata>
  ```

3. <span data-ttu-id="feb50-205">Stay consistent with the portal experience.</span><span class="sxs-lookup"><span data-stu-id="feb50-205">Stay consistent with the portal experience.</span></span> <span data-ttu-id="feb50-206">Create these attributes by using the portal UI before you use them in your custom policies.</span><span class="sxs-lookup"><span data-stu-id="feb50-206">Create these attributes by using the portal UI before you use them in your custom policies.</span></span> <span data-ttu-id="feb50-207">When you create an attribute **ActivationStatus** in the portal, you must refer to it as follows:</span><span class="sxs-lookup"><span data-stu-id="feb50-207">When you create an attribute **ActivationStatus** in the portal, you must refer to it as follows:</span></span>

  ```
  extension_ActivationStatus in the custom policy.
  extension_<app-guid>_ActivationStatus via Graph API.
  ```


## <a name="reference"></a><span data-ttu-id="feb50-208">Reference</span><span class="sxs-lookup"><span data-stu-id="feb50-208">Reference</span></span>

<span data-ttu-id="feb50-209">For more information on extension properties, see the article [Directory schema extensions | Graph API concepts](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).</span><span class="sxs-lookup"><span data-stu-id="feb50-209">For more information on extension properties, see the article [Directory schema extensions | Graph API concepts](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions).</span></span>

> [!NOTE]
> * <span data-ttu-id="feb50-210">A **TechnicalProfile** is an element type, or function, that defines an endpoint’s name, metadata, and protocol.</span><span class="sxs-lookup"><span data-stu-id="feb50-210">A **TechnicalProfile** is an element type, or function, that defines an endpoint’s name, metadata, and protocol.</span></span> <span data-ttu-id="feb50-211">The **TechnicalProfile** details the exchange of claims that the Identity Experience Framework performs.</span><span class="sxs-lookup"><span data-stu-id="feb50-211">The **TechnicalProfile** details the exchange of claims that the Identity Experience Framework performs.</span></span> <span data-ttu-id="feb50-212">When this function is called in an orchestration step or from another **TechnicalProfile**, the **InputClaims** and **OutputClaims** are provided as parameters by the caller.</span><span class="sxs-lookup"><span data-stu-id="feb50-212">When this function is called in an orchestration step or from another **TechnicalProfile**, the **InputClaims** and **OutputClaims** are provided as parameters by the caller.</span></span>  
> * <span data-ttu-id="feb50-213">Extension attributes in the Graph API are named by using the convention `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="feb50-213">Extension attributes in the Graph API are named by using the convention `extension_ApplicationObjectID_attributename`.</span></span>  
> * <span data-ttu-id="feb50-214">Custom policies refer to extension attributes as **extension_attributename**.</span><span class="sxs-lookup"><span data-stu-id="feb50-214">Custom policies refer to extension attributes as **extension_attributename**.</span></span> <span data-ttu-id="feb50-215">This reference omits the **ApplicationObjectId** in XML.</span><span class="sxs-lookup"><span data-stu-id="feb50-215">This reference omits the **ApplicationObjectId** in XML.</span></span>
