---
title: Add LinkedIn as an OAuth2 identity provider by using custom policies in Azure Active Directory B2C | Microsoft Docs
description: A How-To article about setting up a LinkedIn application by using the OAuth2 protocol and custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 10/23/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 58a595c697b6e1a70089a6683493835e0d3a9780
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855767"
---
# <a name="azure-active-directory-b2c-add-linkedin-as-an-identity-provider-by-using-custom-policies"></a><span data-ttu-id="0cc6c-103">Azure Active Directory B2C: Add LinkedIn as an identity provider by using custom policies</span><span class="sxs-lookup"><span data-stu-id="0cc6c-103">Azure Active Directory B2C: Add LinkedIn as an identity provider by using custom policies</span></span>
[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="0cc6c-104">This article shows you how to enable sign-in for users of a LinkedIn account by using [custom policies](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-104">This article shows you how to enable sign-in for users of a LinkedIn account by using [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cc6c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0cc6c-105">Prerequisites</span></span>
<span data-ttu-id="0cc6c-106">Complete the steps in the [Get started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-106">Complete the steps in the [Get started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

## <a name="step-1-create-a-linkedin-account-application"></a><span data-ttu-id="0cc6c-107">Step 1: Create a LinkedIn account application</span><span class="sxs-lookup"><span data-stu-id="0cc6c-107">Step 1: Create a LinkedIn account application</span></span>
<span data-ttu-id="0cc6c-108">To use LinkedIn as an identity provider in Azure Active Directory B2C (Azure AD B2C), you must create a LinkedIn application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-108">To use LinkedIn as an identity provider in Azure Active Directory B2C (Azure AD B2C), you must create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="0cc6c-109">You can register a LinkedIn application by going to the [LinkedIn sign-up page](https://www.linkedin.com/start/join).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-109">You can register a LinkedIn application by going to the [LinkedIn sign-up page](https://www.linkedin.com/start/join).</span></span>

1. <span data-ttu-id="0cc6c-110">Go to the [LinkedIn application management](https://www.linkedin.com/secure/developer?newapp=) website, sign in with your LinkedIn account credentials, and then select **Create Application**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-110">Go to the [LinkedIn application management](https://www.linkedin.com/secure/developer?newapp=) website, sign in with your LinkedIn account credentials, and then select **Create Application**.</span></span>

    ![LinkedIn account - Create application](media/active-directory-b2c-custom-setup-li-idp/adb2c-ief-setup-li-idp-new-app1.png)

2. <span data-ttu-id="0cc6c-112">On the **Create a New Application** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-112">On the **Create a New Application** page, do the following:</span></span>

    <span data-ttu-id="0cc6c-113">a.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-113">a.</span></span> <span data-ttu-id="0cc6c-114">Type your **Company Name**, a descriptive **Name** for the company, and a **Description** of your new app.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-114">Type your **Company Name**, a descriptive **Name** for the company, and a **Description** of your new app.</span></span>

    <span data-ttu-id="0cc6c-115">b.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-115">b.</span></span> <span data-ttu-id="0cc6c-116">Upload your **Application Logo**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-116">Upload your **Application Logo**.</span></span>

    <span data-ttu-id="0cc6c-117">c.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-117">c.</span></span> <span data-ttu-id="0cc6c-118">Select an **Application Use**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-118">Select an **Application Use**.</span></span>

    <span data-ttu-id="0cc6c-119">d.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-119">d.</span></span> <span data-ttu-id="0cc6c-120">In the **Website URL** box, paste **https://{tenant}.b2clogin.com**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-120">In the **Website URL** box, paste **https://{tenant}.b2clogin.com**.</span></span>  <span data-ttu-id="0cc6c-121">Where {*tenant*} is your tenant name (for example contoso.b2clogin.com).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-121">Where {*tenant*} is your tenant name (for example contoso.b2clogin.com).</span></span>

    <span data-ttu-id="0cc6c-122">e.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-122">e.</span></span> <span data-ttu-id="0cc6c-123">Type your **Business Email** address and **Business Phone** number.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-123">Type your **Business Email** address and **Business Phone** number.</span></span>

    <span data-ttu-id="0cc6c-124">f.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-124">f.</span></span> <span data-ttu-id="0cc6c-125">At the bottom of the page, read and accept the terms of use, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-125">At the bottom of the page, read and accept the terms of use, and then select **Submit**.</span></span>

    ![LinkedIn account - Configure application properties](media/active-directory-b2c-custom-setup-li-idp/adb2c-ief-setup-li-idp-new-app2.png)

3. <span data-ttu-id="0cc6c-127">Select **Authentication**, and then note the **Client ID** and **Client Secret** values.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-127">Select **Authentication**, and then note the **Client ID** and **Client Secret** values.</span></span>

4. <span data-ttu-id="0cc6c-128">In the **Authorized Redirect URLs** box, paste **https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-128">In the **Authorized Redirect URLs** box, paste **https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp**.</span></span> <span data-ttu-id="0cc6c-129">Replace {*tenant*} with your tenant name (for example, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-129">Replace {*tenant*} with your tenant name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="0cc6c-130">Make sure that you are using the HTTPS scheme.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-130">Make sure that you are using the HTTPS scheme.</span></span> 

    ![LinkedIn account - Set authorized redirect URLs](media/active-directory-b2c-custom-setup-li-idp/adb2c-ief-setup-li-idp-new-app3.png)

    >[!NOTE]
    ><span data-ttu-id="0cc6c-132">The client secret is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-132">The client secret is an important security credential.</span></span> <span data-ttu-id="0cc6c-133">Do not share this secret with anyone or distribute it with your app.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-133">Do not share this secret with anyone or distribute it with your app.</span></span>

5. <span data-ttu-id="0cc6c-134">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-134">Select **Add**.</span></span>

6. <span data-ttu-id="0cc6c-135">Select **Settings**, change the **Application status** to **Live**, and then select **Update**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-135">Select **Settings**, change the **Application status** to **Live**, and then select **Update**.</span></span>

    ![LinkedIn account - Set application status](media/active-directory-b2c-custom-setup-li-idp/adb2c-ief-setup-li-idp-new-app4.png)

## <a name="step-2-add-your-linkedin-application-key-to-azure-ad-b2c"></a><span data-ttu-id="0cc6c-137">Step 2: Add your LinkedIn application key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="0cc6c-137">Step 2: Add your LinkedIn application key to Azure AD B2C</span></span>
<span data-ttu-id="0cc6c-138">Federation with LinkedIn accounts requires a client secret for the LinkedIn account to trust Azure AD B2C on behalf of the application.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-138">Federation with LinkedIn accounts requires a client secret for the LinkedIn account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="0cc6c-139">To store the LinkedIn application secret in your Azure AD B2C tenant, do the following:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-139">To store the LinkedIn application secret in your Azure AD B2C tenant, do the following:</span></span>  

1. <span data-ttu-id="0cc6c-140">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-140">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span></span>

2. <span data-ttu-id="0cc6c-141">To view the keys that are available in your tenant, select **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-141">To view the keys that are available in your tenant, select **Policy Keys**.</span></span>

3. <span data-ttu-id="0cc6c-142">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-142">Select **Add**.</span></span>

4. <span data-ttu-id="0cc6c-143">In the **Options** box, select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-143">In the **Options** box, select **Upload**.</span></span>

5. <span data-ttu-id="0cc6c-144">In the **Name** box, type **B2cRestClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-144">In the **Name** box, type **B2cRestClientCertificate**.</span></span>  
    <span data-ttu-id="0cc6c-145">The prefix *B2C_1A_* might be added automatically.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-145">The prefix *B2C_1A_* might be added automatically.</span></span>

6. <span data-ttu-id="0cc6c-146">In the **Secret** box, enter your LinkedIn application secret from the [Application Registration Portal](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-146">In the **Secret** box, enter your LinkedIn application secret from the [Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

7. <span data-ttu-id="0cc6c-147">For **Key usage**, select **Encryption**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-147">For **Key usage**, select **Encryption**.</span></span>

8. <span data-ttu-id="0cc6c-148">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-148">Select **Create**.</span></span> 

9. <span data-ttu-id="0cc6c-149">Confirm that you've created the `B2C_1A_LinkedInSecret`key.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-149">Confirm that you've created the `B2C_1A_LinkedInSecret`key.</span></span>

## <a name="step-3-add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="0cc6c-150">Step 3: Add a claims provider in your extension policy</span><span class="sxs-lookup"><span data-stu-id="0cc6c-150">Step 3: Add a claims provider in your extension policy</span></span>
<span data-ttu-id="0cc6c-151">If you want users to sign in by using their LinkedIn account, you must define LinkedIn as a claims provider.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-151">If you want users to sign in by using their LinkedIn account, you must define LinkedIn as a claims provider.</span></span> <span data-ttu-id="0cc6c-152">In other words, you must specify the endpoints that Azure AD B2C communicates with.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-152">In other words, you must specify the endpoints that Azure AD B2C communicates with.</span></span> <span data-ttu-id="0cc6c-153">The endpoints provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-153">The endpoints provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="0cc6c-154">Define LinkedIn as a claims provider by adding a `<ClaimsProvider>` node in your extension policy file:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-154">Define LinkedIn as a claims provider by adding a `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="0cc6c-155">In your working directory, open the *TrustFrameworkExtensions.xml* extension policy file.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-155">In your working directory, open the *TrustFrameworkExtensions.xml* extension policy file.</span></span> 

2. <span data-ttu-id="0cc6c-156">Search for the `<ClaimsProviders>` element.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-156">Search for the `<ClaimsProviders>` element.</span></span>

3. <span data-ttu-id="0cc6c-157">In the `<ClaimsProviders>` element, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-157">In the `<ClaimsProviders>` element, add the following XML snippet:</span></span> 

    ```xml
    <ClaimsProvider>
      <Domain>linkedin.com</Domain>
      <DisplayName>LinkedIn</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="LinkedIn-OAUTH">
          <DisplayName>LinkedIn</DisplayName>
          <Protocol Name="OAuth2" />
          <Metadata>
            <Item Key="ProviderName">linkedin</Item>
            <Item Key="authorization_endpoint">https://www.linkedin.com/oauth/v2/authorization</Item>
            <Item Key="AccessTokenEndpoint">https://www.linkedin.com/oauth/v2/accessToken</Item>
            <Item Key="ClaimsEndpoint">https://api.linkedin.com/v1/people/~:(id,first-name,last-name,email-address,headline)</Item>
            <Item Key="ClaimsEndpointAccessTokenName">oauth2_access_token</Item>
            <Item Key="ClaimsEndpointFormatName">format</Item>
            <Item Key="ClaimsEndpointFormat">json</Item>
            <Item Key="scope">r_emailaddress r_basicprofile</Item>
            <Item Key="HttpBinding">POST</Item>
            <Item Key="UsePolicyInRedirectUri">0</Item>
            <Item Key="client_id">Your LinkedIn application client ID</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="client_secret" StorageReferenceId="B2C_1A_LinkedInSecret" />
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="firstName" />
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="lastName" />
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="emailAddress" />
            <!--<OutputClaim ClaimTypeReferenceId="jobTitle" PartnerClaimType="headline" />-->
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="linkedin.com" />
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

4. <span data-ttu-id="0cc6c-158">Replace the *client_id* value with your LinkedIn application client ID.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-158">Replace the *client_id* value with your LinkedIn application client ID.</span></span>

5. <span data-ttu-id="0cc6c-159">Save the file.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-159">Save the file.</span></span>

## <a name="step-4-register-the-linkedin-account-claims-provider"></a><span data-ttu-id="0cc6c-160">Step 4: Register the LinkedIn account claims provider</span><span class="sxs-lookup"><span data-stu-id="0cc6c-160">Step 4: Register the LinkedIn account claims provider</span></span>
<span data-ttu-id="0cc6c-161">You've set up the identity provider.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-161">You've set up the identity provider.</span></span> <span data-ttu-id="0cc6c-162">However, it is not yet available in any of the sign-up or sign-in windows.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-162">However, it is not yet available in any of the sign-up or sign-in windows.</span></span> <span data-ttu-id="0cc6c-163">Now you must add the LinkedIn account identity provider to your user `SignUpOrSignIn` user journey.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-163">Now you must add the LinkedIn account identity provider to your user `SignUpOrSignIn` user journey.</span></span>

### <a name="step-41-make-a-copy-of-the-user-journey"></a><span data-ttu-id="0cc6c-164">Step 4.1: Make a copy of the user journey</span><span class="sxs-lookup"><span data-stu-id="0cc6c-164">Step 4.1: Make a copy of the user journey</span></span>
<span data-ttu-id="0cc6c-165">To make the user journey available, you create a duplicate of an existing user journey template and then add the LinkedIn identity provider:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-165">To make the user journey available, you create a duplicate of an existing user journey template and then add the LinkedIn identity provider:</span></span>

>[!NOTE]
><span data-ttu-id="0cc6c-166">If you copied the `<UserJourneys>` element from the base file of your policy to the *TrustFrameworkExtensions.xml* extension file, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-166">If you copied the `<UserJourneys>` element from the base file of your policy to the *TrustFrameworkExtensions.xml* extension file, you can skip this section.</span></span>

1. <span data-ttu-id="0cc6c-167">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-167">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>

2. <span data-ttu-id="0cc6c-168">Search for the `<UserJourneys>` element, select the entire contents of the `<UserJourney>` node, and then select **Cut** to move the selected text to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-168">Search for the `<UserJourneys>` element, select the entire contents of the `<UserJourney>` node, and then select **Cut** to move the selected text to the clipboard.</span></span>

3. <span data-ttu-id="0cc6c-169">Open the extension file (for example, TrustFrameworkExtensions.xml), and search for the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-169">Open the extension file (for example, TrustFrameworkExtensions.xml), and search for the `<UserJourneys>` element.</span></span> <span data-ttu-id="0cc6c-170">If the element doesn't exist, add it.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-170">If the element doesn't exist, add it.</span></span>

4. <span data-ttu-id="0cc6c-171">Paste the entire contents of the `<UserJourney>` node, which you moved to the clipboard in step 2, into the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-171">Paste the entire contents of the `<UserJourney>` node, which you moved to the clipboard in step 2, into the `<UserJourneys>` element.</span></span>

### <a name="step-42-display-the-button"></a><span data-ttu-id="0cc6c-172">Step 4.2: Display the "button"</span><span class="sxs-lookup"><span data-stu-id="0cc6c-172">Step 4.2: Display the "button"</span></span>
<span data-ttu-id="0cc6c-173">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-173">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span> <span data-ttu-id="0cc6c-174">The `<ClaimsProviderSelection>` node is analogous to an identity provider button on a sign-up or sign-in page.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-174">The `<ClaimsProviderSelection>` node is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="0cc6c-175">If you add a `<ClaimsProviderSelection>` node for a LinkedIn account, a new button is displayed when a user lands on the page.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-175">If you add a `<ClaimsProviderSelection>` node for a LinkedIn account, a new button is displayed when a user lands on the page.</span></span> <span data-ttu-id="0cc6c-176">To add this element, do the following:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-176">To add this element, do the following:</span></span>

1. <span data-ttu-id="0cc6c-177">Search for the `<UserJourney>` node that contains `Id="SignUpOrSignIn"` in the user journey that you copied.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-177">Search for the `<UserJourney>` node that contains `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>

2. <span data-ttu-id="0cc6c-178">Locate the `<OrchestrationStep>` node that includes `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-178">Locate the `<OrchestrationStep>` node that includes `Order="1"`.</span></span>

3. <span data-ttu-id="0cc6c-179">In the `<ClaimsProviderSelections>` element, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-179">In the `<ClaimsProviderSelections>` element, add the following XML snippet:</span></span>

    ```xml
    <ClaimsProviderSelection TargetClaimsExchangeId="LinkedInExchange" />
    ```

### <a name="step-43-link-the-button-to-an-action"></a><span data-ttu-id="0cc6c-180">Step 4.3: Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="0cc6c-180">Step 4.3: Link the button to an action</span></span>
<span data-ttu-id="0cc6c-181">Now that you have a button in place, you must link it to an action.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-181">Now that you have a button in place, you must link it to an action.</span></span> <span data-ttu-id="0cc6c-182">The action, in this case, is for Azure AD B2C to communicate with the LinkedIn account to receive a token.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-182">The action, in this case, is for Azure AD B2C to communicate with the LinkedIn account to receive a token.</span></span> <span data-ttu-id="0cc6c-183">Link the button to an action by linking the technical profile for your LinkedIn account claims provider:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-183">Link the button to an action by linking the technical profile for your LinkedIn account claims provider:</span></span>

1. <span data-ttu-id="0cc6c-184">Search for the `<OrchestrationStep>` node that contains `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-184">Search for the `<OrchestrationStep>` node that contains `Order="2"` in the `<UserJourney>` node.</span></span>

2. <span data-ttu-id="0cc6c-185">In the `<ClaimsExchanges>` element, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="0cc6c-185">In the `<ClaimsExchanges>` element, add the following XML snippet:</span></span>

    ```xml
    <ClaimsExchange Id="LinkedInExchange" TechnicalProfileReferenceId="LinkedIn-OAuth" />
    ```

    >[!NOTE]
    >* <span data-ttu-id="0cc6c-186">Ensure that `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-186">Ensure that `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
    >* <span data-ttu-id="0cc6c-187">Ensure that the `TechnicalProfileReferenceId` ID is set to the technical profile that you created earlier (LinkedIn-OAuth).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-187">Ensure that the `TechnicalProfileReferenceId` ID is set to the technical profile that you created earlier (LinkedIn-OAuth).</span></span>

## <a name="step-5-upload-the-policy-to-your-tenant"></a><span data-ttu-id="0cc6c-188">Step 5: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="0cc6c-188">Step 5: Upload the policy to your tenant</span></span>
1. <span data-ttu-id="0cc6c-189">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-189">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span></span>

2. <span data-ttu-id="0cc6c-190">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-190">Select **Identity Experience Framework**.</span></span>

3. <span data-ttu-id="0cc6c-191">Select **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-191">Select **All Policies**.</span></span>

4. <span data-ttu-id="0cc6c-192">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-192">Select **Upload Policy**.</span></span>

5. <span data-ttu-id="0cc6c-193">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-193">Select the **Overwrite the policy if it exists** check box.</span></span>

6. <span data-ttu-id="0cc6c-194">Upload the *TrustFrameworkBase.xml* and *TrustFrameworkExtensions.xml* files, and ensure that they pass validation.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-194">Upload the *TrustFrameworkBase.xml* and *TrustFrameworkExtensions.xml* files, and ensure that they pass validation.</span></span>

## <a name="step-6-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="0cc6c-195">Step 6: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="0cc6c-195">Step 6: Test the custom policy by using Run Now</span></span>
1. <span data-ttu-id="0cc6c-196">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-196">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="0cc6c-197">Run Now requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-197">Run Now requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="0cc6c-198">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-198">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>

2. <span data-ttu-id="0cc6c-199">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-199">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span></span>  
    <span data-ttu-id="0cc6c-200">You should now be able to sign in by using the LinkedIn account.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-200">You should now be able to sign in by using the LinkedIn account.</span></span>

## <a name="step-7-optional-register-the-linkedin-account-claims-provider-to-the-profile-edit-user-journey"></a><span data-ttu-id="0cc6c-201">Step 7: (Optional) Register the LinkedIn account claims provider to the Profile-Edit user journey</span><span class="sxs-lookup"><span data-stu-id="0cc6c-201">Step 7: (Optional) Register the LinkedIn account claims provider to the Profile-Edit user journey</span></span>
<span data-ttu-id="0cc6c-202">You might also want to add the LinkedIn account identity provider to your `ProfileEdit` user journey.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-202">You might also want to add the LinkedIn account identity provider to your `ProfileEdit` user journey.</span></span> <span data-ttu-id="0cc6c-203">To make the user journey available, repeat "Step 4."</span><span class="sxs-lookup"><span data-stu-id="0cc6c-203">To make the user journey available, repeat "Step 4."</span></span> <span data-ttu-id="0cc6c-204">This time, select the `<UserJourney>` node that contains `Id="ProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-204">This time, select the `<UserJourney>` node that contains `Id="ProfileEdit"`.</span></span> <span data-ttu-id="0cc6c-205">Save, upload, and test your policy.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-205">Save, upload, and test your policy.</span></span>

## <a name="optional-download-the-complete-policy-files"></a><span data-ttu-id="0cc6c-206">(Optional) Download the complete policy files</span><span class="sxs-lookup"><span data-stu-id="0cc6c-206">(Optional) Download the complete policy files</span></span>
<span data-ttu-id="0cc6c-207">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span><span class="sxs-lookup"><span data-stu-id="0cc6c-207">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span></span> <span data-ttu-id="0cc6c-208">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-li-app).</span><span class="sxs-lookup"><span data-stu-id="0cc6c-208">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-li-app).</span></span>
