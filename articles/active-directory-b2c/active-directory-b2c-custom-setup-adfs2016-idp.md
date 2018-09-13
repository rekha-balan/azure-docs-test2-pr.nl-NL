---
title: Add ADFS as a SAML identity provider using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Set up ADFS 2016 using the SAML protocol and custom policies in Azure Active Directory B2C
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/31/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 2c2e6861fda42a9e8c1aabcba303bfede47ac3c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966876"
---
# <a name="add-adfs-as-a-saml-identity-provider-using-custom-policies-in-azure-active-directory-b2c"></a><span data-ttu-id="4077b-103">Add ADFS as a SAML identity provider using custom policies in Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="4077b-103">Add ADFS as a SAML identity provider using custom policies in Azure Active Directory B2C</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="4077b-104">This article shows you how to enable sign-in for an ADFS user account by using [custom policies](active-directory-b2c-overview-custom.md) in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="4077b-104">This article shows you how to enable sign-in for an ADFS user account by using [custom policies](active-directory-b2c-overview-custom.md) in Azure Active Directory (Azure AD) B2C.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4077b-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4077b-105">Prerequisites</span></span>

<span data-ttu-id="4077b-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="4077b-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="4077b-107">Add the ADFS account application key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="4077b-107">Add the ADFS account application key to Azure AD B2C</span></span>

<span data-ttu-id="4077b-108">Federation with an ADFS account requires a client secret for the account to trust Azure AD B2C on behalf of the application.</span><span class="sxs-lookup"><span data-stu-id="4077b-108">Federation with an ADFS account requires a client secret for the account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="4077b-109">You need to store your ADFS certificate in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="4077b-109">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1. <span data-ttu-id="4077b-110">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4077b-110">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4077b-111">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4077b-111">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="4077b-112">Select **Switch Directory**, and then choose the directory that contains the tenant you created.</span><span class="sxs-lookup"><span data-stu-id="4077b-112">Select **Switch Directory**, and then choose the directory that contains the tenant you created.</span></span> <span data-ttu-id="4077b-113">In this tutorial, the *contoso* directory is used that contains the tenant named *contoso0522Tenant.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="4077b-113">In this tutorial, the *contoso* directory is used that contains the tenant named *contoso0522Tenant.onmicrosoft.com*.</span></span>

    ![Switch directories](./media/active-directory-b2c-custom-setup-adfs2016-idp/switch-directories.png)

3. <span data-ttu-id="4077b-115">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="4077b-115">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span> <span data-ttu-id="4077b-116">You should now be using your tenant.</span><span class="sxs-lookup"><span data-stu-id="4077b-116">You should now be using your tenant.</span></span>
4. <span data-ttu-id="4077b-117">On the Overview page, select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="4077b-117">On the Overview page, select **Identity Experience Framework**.</span></span>
5. <span data-ttu-id="4077b-118">Select **Policy Keys** to view the keys available in your tenant, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="4077b-118">Select **Policy Keys** to view the keys available in your tenant, and then click **Add**.</span></span>
6. <span data-ttu-id="4077b-119">Choose **Upload** as the Option.</span><span class="sxs-lookup"><span data-stu-id="4077b-119">Choose **Upload** as the Option.</span></span>
7. <span data-ttu-id="4077b-120">Enter `ADFSSamlCert` for the name.</span><span class="sxs-lookup"><span data-stu-id="4077b-120">Enter `ADFSSamlCert` for the name.</span></span> <span data-ttu-id="4077b-121">The prefix `B2C_1A_` might be added automatically.</span><span class="sxs-lookup"><span data-stu-id="4077b-121">The prefix `B2C_1A_` might be added automatically.</span></span>
8. <span data-ttu-id="4077b-122">Browse to and select your certificate .pfx file with the private key.</span><span class="sxs-lookup"><span data-stu-id="4077b-122">Browse to and select your certificate .pfx file with the private key.</span></span> <span data-ttu-id="4077b-123">This certificate with the private key should be the same one that was issued and used for the ADFS relying party.</span><span class="sxs-lookup"><span data-stu-id="4077b-123">This certificate with the private key should be the same one that was issued and used for the ADFS relying party.</span></span>
9. <span data-ttu-id="4077b-124">Click **Create** and confirm that you've created the `B2C_1A_ADFSSamlCert` key.</span><span class="sxs-lookup"><span data-stu-id="4077b-124">Click **Create** and confirm that you've created the `B2C_1A_ADFSSamlCert` key.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="4077b-125">Add a claims provider in your extension policy</span><span class="sxs-lookup"><span data-stu-id="4077b-125">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="4077b-126">If you want users to sign in by using an ADFS account, you need to define the account as a claims provider.</span><span class="sxs-lookup"><span data-stu-id="4077b-126">If you want users to sign in by using an ADFS account, you need to define the account as a claims provider.</span></span> <span data-ttu-id="4077b-127">You do this by specifying an endpoint that Azure AD B2C communicates with.</span><span class="sxs-lookup"><span data-stu-id="4077b-127">You do this by specifying an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="4077b-128">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="4077b-128">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="4077b-129">Define ADFS as a claims provider, by adding **ClaimsProvider** element in your extension policy file.</span><span class="sxs-lookup"><span data-stu-id="4077b-129">Define ADFS as a claims provider, by adding **ClaimsProvider** element in your extension policy file.</span></span>

1. <span data-ttu-id="4077b-130">Open the *TrustFrameworkExtensions.xml* policy file in your working directory.</span><span class="sxs-lookup"><span data-stu-id="4077b-130">Open the *TrustFrameworkExtensions.xml* policy file in your working directory.</span></span> <span data-ttu-id="4077b-131">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), which is a lightweight cross-platform editor.</span><span class="sxs-lookup"><span data-stu-id="4077b-131">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), which is a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="4077b-132">Add the following XML under the **ClaimsProviders** element and replace **your-ADFS-domain** with your ADFS domain name and replace the value of the **identityProvider** output claim with your DNS (Arbitrary value that indicates your domain), and save the file.</span><span class="sxs-lookup"><span data-stu-id="4077b-132">Add the following XML under the **ClaimsProviders** element and replace **your-ADFS-domain** with your ADFS domain name and replace the value of the **identityProvider** output claim with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

    ```xml
    <ClaimsProvider>
      <Domain>contoso.com</Domain>
      <DisplayName>Contoso ADFS</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="Contoso-SAML2">
          <DisplayName>Contoso ADFS</DisplayName>
          <Description>Login with your Contoso account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="PartnerEntity">https://your-ADFS-domain/federationmetadata/2007-06/federationmetadata.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

## <a name="register-the-claims-provider-for-sign-up-and-sign-in"></a><span data-ttu-id="4077b-133">Register the claims provider for sign-up and sign-in</span><span class="sxs-lookup"><span data-stu-id="4077b-133">Register the claims provider for sign-up and sign-in</span></span>

<span data-ttu-id="4077b-134">To make the ADFS account identity provider available in the sign-up and sign-in pages, you need to add it to your **SignUpOrSignIn** user journey.</span><span class="sxs-lookup"><span data-stu-id="4077b-134">To make the ADFS account identity provider available in the sign-up and sign-in pages, you need to add it to your **SignUpOrSignIn** user journey.</span></span> 

<span data-ttu-id="4077b-135">Make a copy of an existing template user journey and then modify it so that it includes the ADFS identity provider:</span><span class="sxs-lookup"><span data-stu-id="4077b-135">Make a copy of an existing template user journey and then modify it so that it includes the ADFS identity provider:</span></span>

>[!NOTE]
><span data-ttu-id="4077b-136">If you previously copied the **UserJourneys** element from the base file of your policy to the extension file (*TrustFrameworkExtensions.xml*) you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="4077b-136">If you previously copied the **UserJourneys** element from the base file of your policy to the extension file (*TrustFrameworkExtensions.xml*) you can skip this section.</span></span>

1. <span data-ttu-id="4077b-137">Open the base file of your policy.</span><span class="sxs-lookup"><span data-stu-id="4077b-137">Open the base file of your policy.</span></span> <span data-ttu-id="4077b-138">For example, *TrustFrameworkBase.xml*.</span><span class="sxs-lookup"><span data-stu-id="4077b-138">For example, *TrustFrameworkBase.xml*.</span></span>
2. <span data-ttu-id="4077b-139">Copy the entire content of **UserJourneys** element.</span><span class="sxs-lookup"><span data-stu-id="4077b-139">Copy the entire content of **UserJourneys** element.</span></span>
3. <span data-ttu-id="4077b-140">Open the extension file (*TrustFrameworkExtensions.xml*) and paste the entire content of **UserJourneys** element that you copied in the extension file.</span><span class="sxs-lookup"><span data-stu-id="4077b-140">Open the extension file (*TrustFrameworkExtensions.xml*) and paste the entire content of **UserJourneys** element that you copied in the extension file.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="4077b-141">Display the button</span><span class="sxs-lookup"><span data-stu-id="4077b-141">Display the button</span></span>

<span data-ttu-id="4077b-142">The **ClaimsProviderSelections** element defines the list of claims provider selections and their order.</span><span class="sxs-lookup"><span data-stu-id="4077b-142">The **ClaimsProviderSelections** element defines the list of claims provider selections and their order.</span></span>  <span data-ttu-id="4077b-143">The **ClaimsProviderSelection** element is analogous to an identity provider button on a sign-up and sign-in page.</span><span class="sxs-lookup"><span data-stu-id="4077b-143">The **ClaimsProviderSelection** element is analogous to an identity provider button on a sign-up and sign-in page.</span></span> <span data-ttu-id="4077b-144">If you add a **ClaimsProviderSelection** element for an ADFS account, a new button is displayed when a user sees the page.</span><span class="sxs-lookup"><span data-stu-id="4077b-144">If you add a **ClaimsProviderSelection** element for an ADFS account, a new button is displayed when a user sees the page.</span></span> <span data-ttu-id="4077b-145">To add this element:</span><span class="sxs-lookup"><span data-stu-id="4077b-145">To add this element:</span></span>

1. <span data-ttu-id="4077b-146">In the **UserJourney** element with an identifier of `SignUpOrSignIn` in the user journeys that you copied, locate the **OrchestrationStep** element of `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="4077b-146">In the **UserJourney** element with an identifier of `SignUpOrSignIn` in the user journeys that you copied, locate the **OrchestrationStep** element of `Order="1"`.</span></span>
2. <span data-ttu-id="4077b-147">Add following **ClaimsProviderSelection** element under the **ClaimsProviderSelections** element:</span><span class="sxs-lookup"><span data-stu-id="4077b-147">Add following **ClaimsProviderSelection** element under the **ClaimsProviderSelections** element:</span></span>

    ```xml
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="4077b-148">Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="4077b-148">Link the button to an action</span></span>

<span data-ttu-id="4077b-149">Now that you have a button in place, you need to link it to an action.</span><span class="sxs-lookup"><span data-stu-id="4077b-149">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="4077b-150">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span><span class="sxs-lookup"><span data-stu-id="4077b-150">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="4077b-151">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span><span class="sxs-lookup"><span data-stu-id="4077b-151">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1. <span data-ttu-id="4077b-152">Find the **OrchestrationStep** of `Order="2"` under the **UserJourney** element.</span><span class="sxs-lookup"><span data-stu-id="4077b-152">Find the **OrchestrationStep** of `Order="2"` under the **UserJourney** element.</span></span>
2. <span data-ttu-id="4077b-153">Add following **ClaimsExchange** element under the **ClaimsExchanges** element:</span><span class="sxs-lookup"><span data-stu-id="4077b-153">Add following **ClaimsExchange** element under the **ClaimsExchanges** element:</span></span>

    ```xml
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
    ```

> [!NOTE]
> * <span data-ttu-id="4077b-154">Make sure that the `Id` has the same value as `TargetClaimsExchangeId` in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="4077b-154">Make sure that the `Id` has the same value as `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="4077b-155">Make sure that the `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="4077b-155">Make sure that the `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>


## <a name="optional-register-the-claims-provider-for-profile-edit"></a><span data-ttu-id="4077b-156">[Optional] Register the claims provider for profile edit</span><span class="sxs-lookup"><span data-stu-id="4077b-156">[Optional] Register the claims provider for profile edit</span></span>

<span data-ttu-id="4077b-157">You may also want to add the ADFS account identity provider to your profile edit user journey.</span><span class="sxs-lookup"><span data-stu-id="4077b-157">You may also want to add the ADFS account identity provider to your profile edit user journey.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="4077b-158">Display the button</span><span class="sxs-lookup"><span data-stu-id="4077b-158">Display the button</span></span>

1. <span data-ttu-id="4077b-159">Open the extension file of your policy.</span><span class="sxs-lookup"><span data-stu-id="4077b-159">Open the extension file of your policy.</span></span> <span data-ttu-id="4077b-160">For example, *TrustFrameworkExtensions.xml*.</span><span class="sxs-lookup"><span data-stu-id="4077b-160">For example, *TrustFrameworkExtensions.xml*.</span></span>
2. <span data-ttu-id="4077b-161">In the **UserJourney** element with an identifier `ProfileEdit` in the user journeys that you copied, locate the **OrchestrationStep** element of `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="4077b-161">In the **UserJourney** element with an identifier `ProfileEdit` in the user journeys that you copied, locate the **OrchestrationStep** element of `Order="1"`.</span></span>
3. <span data-ttu-id="4077b-162">Add following **ClaimsProviderSelection** element under **ClaimsProviderSelections** element:</span><span class="sxs-lookup"><span data-stu-id="4077b-162">Add following **ClaimsProviderSelection** element under **ClaimsProviderSelections** element:</span></span>

    ```xml
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="4077b-163">Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="4077b-163">Link the button to an action</span></span>

1. <span data-ttu-id="4077b-164">Find the **OrchestrationStep** of `Order="2"` under the **UserJourney** element.</span><span class="sxs-lookup"><span data-stu-id="4077b-164">Find the **OrchestrationStep** of `Order="2"` under the **UserJourney** element.</span></span>
2. <span data-ttu-id="4077b-165">Add following **ClaimsExchange** element under the **ClaimsExchanges** element:</span><span class="sxs-lookup"><span data-stu-id="4077b-165">Add following **ClaimsExchange** element under the **ClaimsExchanges** element:</span></span>

    ```xml
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
    ```

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="4077b-166">Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="4077b-166">Upload the policy to your tenant</span></span>

1. <span data-ttu-id="4077b-167">In the Azure portal, select **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="4077b-167">In the Azure portal, select **All Policies**.</span></span>
2. <span data-ttu-id="4077b-168">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="4077b-168">Select **Upload Policy**.</span></span>
3. <span data-ttu-id="4077b-169">Enable **Overwrite the policy if it exists**.</span><span class="sxs-lookup"><span data-stu-id="4077b-169">Enable **Overwrite the policy if it exists**.</span></span>
4. <span data-ttu-id="4077b-170">Browse to and select your *TrustFrameworkExtensions.xml* policy file, and then select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="4077b-170">Browse to and select your *TrustFrameworkExtensions.xml* policy file, and then select **Upload**.</span></span> <span data-ttu-id="4077b-171">Make sure that the validation is successful.</span><span class="sxs-lookup"><span data-stu-id="4077b-171">Make sure that the validation is successful.</span></span>


## <a name="configure-an-adfs-relying-party-trust"></a><span data-ttu-id="4077b-172">Configure an ADFS Relying Party Trust</span><span class="sxs-lookup"><span data-stu-id="4077b-172">Configure an ADFS Relying Party Trust</span></span>

<span data-ttu-id="4077b-173">To use ADFS as an identity provider in Azure AD B2C, you need to create an ADFS Relying Party Trust with the Azure AD B2C SAML metadata.</span><span class="sxs-lookup"><span data-stu-id="4077b-173">To use ADFS as an identity provider in Azure AD B2C, you need to create an ADFS Relying Party Trust with the Azure AD B2C SAML metadata.</span></span> <span data-ttu-id="4077b-174">The following example shows a URL address to the SAML metadata of an Azure AD B2C technical profile:</span><span class="sxs-lookup"><span data-stu-id="4077b-174">The following example shows a URL address to the SAML metadata of an Azure AD B2C technical profile:</span></span>

```
https://login.microsoftonline.com/te/your-tenant/your-policy/samlp/metadata?idptp=your-technical-profile
```

<span data-ttu-id="4077b-175">Replace the following values:</span><span class="sxs-lookup"><span data-stu-id="4077b-175">Replace the following values:</span></span>

- <span data-ttu-id="4077b-176">**your-tenant** with your tenant name, such as your-tenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="4077b-176">**your-tenant** with your tenant name, such as your-tenant.onmicrosoft.com.</span></span>
- <span data-ttu-id="4077b-177">**your-policy** with your policy name.</span><span class="sxs-lookup"><span data-stu-id="4077b-177">**your-policy** with your policy name.</span></span> <span data-ttu-id="4077b-178">Use the policy where you configure the SAML provider technical profile, or a policy that inherits from that policy.</span><span class="sxs-lookup"><span data-stu-id="4077b-178">Use the policy where you configure the SAML provider technical profile, or a policy that inherits from that policy.</span></span>
- <span data-ttu-id="4077b-179">**your-technical-profile** with tha name of your SAML identity provider technical profile.</span><span class="sxs-lookup"><span data-stu-id="4077b-179">**your-technical-profile** with tha name of your SAML identity provider technical profile.</span></span>
 
<span data-ttu-id="4077b-180">Open a browser and navigate to the URL.</span><span class="sxs-lookup"><span data-stu-id="4077b-180">Open a browser and navigate to the URL.</span></span> <span data-ttu-id="4077b-181">Make sure you type the correct URL and that you have access to the XML metadata file.</span><span class="sxs-lookup"><span data-stu-id="4077b-181">Make sure you type the correct URL and that you have access to the XML metadata file.</span></span>

<span data-ttu-id="4077b-182">To add a new relying party trust by using the ADFS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span><span class="sxs-lookup"><span data-stu-id="4077b-182">To add a new relying party trust by using the ADFS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span> <span data-ttu-id="4077b-183">Membership in **Administrators** or equivalent on the local computer is the minimum required to complete this procedure.</span><span class="sxs-lookup"><span data-stu-id="4077b-183">Membership in **Administrators** or equivalent on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="4077b-184">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477).</span><span class="sxs-lookup"><span data-stu-id="4077b-184">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477).</span></span>

1. <span data-ttu-id="4077b-185">In Server Manager, select **Tools**, and then select **ADFS Management**.</span><span class="sxs-lookup"><span data-stu-id="4077b-185">In Server Manager, select **Tools**, and then select **ADFS Management**.</span></span>
2. <span data-ttu-id="4077b-186">Select **Add Relying Party Trust**.</span><span class="sxs-lookup"><span data-stu-id="4077b-186">Select **Add Relying Party Trust**.</span></span>
3. <span data-ttu-id="4077b-187">On the **Welcome** page, choose **Claims aware**, and then click **Start**.</span><span class="sxs-lookup"><span data-stu-id="4077b-187">On the **Welcome** page, choose **Claims aware**, and then click **Start**.</span></span>
4. <span data-ttu-id="4077b-188">On the **Select Data Source** page, select **Import data about the relying party publish online or on a local network**, provide your Azure AD B2C metadata URL, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4077b-188">On the **Select Data Source** page, select **Import data about the relying party publish online or on a local network**, provide your Azure AD B2C metadata URL, and then click **Next**.</span></span>
5. <span data-ttu-id="4077b-189">On the **Specify Display Name** page, enter a **Display name**, under **Notes**, enter a description for this relying party trust, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4077b-189">On the **Specify Display Name** page, enter a **Display name**, under **Notes**, enter a description for this relying party trust, and then click **Next**.</span></span>
6. <span data-ttu-id="4077b-190">On the **Choose Access Control Policy** page, select a policy, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4077b-190">On the **Choose Access Control Policy** page, select a policy, and then click **Next**.</span></span>
7. <span data-ttu-id="4077b-191">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span><span class="sxs-lookup"><span data-stu-id="4077b-191">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
8. <span data-ttu-id="4077b-192">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4077b-192">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
9. <span data-ttu-id="4077b-193">Select **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="4077b-193">Select **Add Rule**.</span></span>  
10. <span data-ttu-id="4077b-194">In **Claim rule template**, select **Send LDAP attributes as claims**.</span><span class="sxs-lookup"><span data-stu-id="4077b-194">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
11. <span data-ttu-id="4077b-195">Provide a **Claim rule name**.</span><span class="sxs-lookup"><span data-stu-id="4077b-195">Provide a **Claim rule name**.</span></span> <span data-ttu-id="4077b-196">For the **Attribute store**, select **Select Active Directory**, add the following claims, then click **Finish** and **OK**.</span><span class="sxs-lookup"><span data-stu-id="4077b-196">For the **Attribute store**, select **Select Active Directory**, add the following claims, then click **Finish** and **OK**.</span></span>

    ![Set rule properties](./media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)

12.  <span data-ttu-id="4077b-198">Based on your certificate type, you may need to set the HASH algorithm.</span><span class="sxs-lookup"><span data-stu-id="4077b-198">Based on your certificate type, you may need to set the HASH algorithm.</span></span> <span data-ttu-id="4077b-199">On the relying party trust (B2C Demo) properties window, select the **Advanced** tab and change the **Secure hash algorithm** to `SHA-1` or `SHA-256`, and click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="4077b-199">On the relying party trust (B2C Demo) properties window, select the **Advanced** tab and change the **Secure hash algorithm** to `SHA-1` or `SHA-256`, and click **Ok**.</span></span>  

### <a name="update-the-relying-party-metadata"></a><span data-ttu-id="4077b-200">Update the relying party metadata</span><span class="sxs-lookup"><span data-stu-id="4077b-200">Update the relying party metadata</span></span>

<span data-ttu-id="4077b-201">Changing the SAML technical profile requires you to update ADFS with the updated metadata version.</span><span class="sxs-lookup"><span data-stu-id="4077b-201">Changing the SAML technical profile requires you to update ADFS with the updated metadata version.</span></span> <span data-ttu-id="4077b-202">You don’t need to update the metadata when you create the relying party application, but when you make a change, you update the metadata in ADFS.</span><span class="sxs-lookup"><span data-stu-id="4077b-202">You don’t need to update the metadata when you create the relying party application, but when you make a change, you update the metadata in ADFS.</span></span>

1. <span data-ttu-id="4077b-203">In Server Manager, select **Tools**, and then select **ADFS Management**.</span><span class="sxs-lookup"><span data-stu-id="4077b-203">In Server Manager, select **Tools**, and then select **ADFS Management**.</span></span>
2. <span data-ttu-id="4077b-204">Select the relying party trust you created, select **Update from Federation Metadata**, and then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="4077b-204">Select the relying party trust you created, select **Update from Federation Metadata**, and then click **Update**.</span></span> 

### <a name="test-the-policy-by-using-run-now"></a><span data-ttu-id="4077b-205">Test the policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="4077b-205">Test the policy by using Run Now</span></span>

1.  <span data-ttu-id="4077b-206">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="4077b-206">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="4077b-207">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="4077b-207">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="4077b-208">Select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="4077b-208">Select **Run now**.</span></span> <span data-ttu-id="4077b-209">You should be able to sign in using ADFS account.</span><span class="sxs-lookup"><span data-stu-id="4077b-209">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="4077b-210">Download the complete policy files</span><span class="sxs-lookup"><span data-stu-id="4077b-210">Download the complete policy files</span></span>

<span data-ttu-id="4077b-211">Optional: You can build your scenario using your own custom policy files after completing the steps in [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="4077b-211">Optional: You can build your scenario using your own custom policy files after completing the steps in [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="4077b-212">For example files, see [Policy sample files for reference only](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app).</span><span class="sxs-lookup"><span data-stu-id="4077b-212">For example files, see [Policy sample files for reference only](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app).</span></span>
