---
title: Add Twitter as an OAuth1 identity provider by using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Use Twitter as an identity provider by using the OAuth1 protocol.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 10/23/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 28679ef07c2625908f7b08f808ff49c48ddb625b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968586"
---
# <a name="azure-active-directory-b2c-add-twitter-as-an-oauth1-identity-provider-by-using-custom-policies"></a><span data-ttu-id="ad977-103">Azure Active Directory B2C: Add Twitter as an OAuth1 identity provider by using custom policies</span><span class="sxs-lookup"><span data-stu-id="ad977-103">Azure Active Directory B2C: Add Twitter as an OAuth1 identity provider by using custom policies</span></span>
[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ad977-104">This article shows you how to enable sign-in for users of a Twitter account by using [custom policies](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ad977-104">This article shows you how to enable sign-in for users of a Twitter account by using [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad977-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ad977-105">Prerequisites</span></span>
<span data-ttu-id="ad977-106">Complete the steps in the [Get started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="ad977-106">Complete the steps in the [Get started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

## <a name="step-1-create-a-twitter-account-application"></a><span data-ttu-id="ad977-107">Step 1: Create a Twitter account application</span><span class="sxs-lookup"><span data-stu-id="ad977-107">Step 1: Create a Twitter account application</span></span>
<span data-ttu-id="ad977-108">To use Twitter as an identity provider in Azure Active Directory B2C (Azure AD B2C), you must create a Twitter application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="ad977-108">To use Twitter as an identity provider in Azure Active Directory B2C (Azure AD B2C), you must create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="ad977-109">You can register a Twitter application by going to the [Twitter sign-up page](https://twitter.com/signup).</span><span class="sxs-lookup"><span data-stu-id="ad977-109">You can register a Twitter application by going to the [Twitter sign-up page](https://twitter.com/signup).</span></span>

1. <span data-ttu-id="ad977-110">Go to the [Twitter Developers](https://apps.twitter.com/) website, sign in with your Twitter account credentials, and then select  **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="ad977-110">Go to the [Twitter Developers](https://apps.twitter.com/) website, sign in with your Twitter account credentials, and then select  **Create New App**.</span></span>

    ![Twitter account - Create new app](media/active-directory-b2c-custom-setup-twitter-idp/adb2c-ief-setup-twitter-idp-new-app1.png)

2. <span data-ttu-id="ad977-112">In the **Create an application** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="ad977-112">In the **Create an application** window, do the following:</span></span>
 
    <span data-ttu-id="ad977-113">a.</span><span class="sxs-lookup"><span data-stu-id="ad977-113">a.</span></span> <span data-ttu-id="ad977-114">Type the **Name** and a **Description** for your new app.</span><span class="sxs-lookup"><span data-stu-id="ad977-114">Type the **Name** and a **Description** for your new app.</span></span> 

    <span data-ttu-id="ad977-115">b.</span><span class="sxs-lookup"><span data-stu-id="ad977-115">b.</span></span> <span data-ttu-id="ad977-116">In the **Website** box, paste **https://{tenant}.b2clogin.com**.</span><span class="sxs-lookup"><span data-stu-id="ad977-116">In the **Website** box, paste **https://{tenant}.b2clogin.com**.</span></span> <span data-ttu-id="ad977-117">Where **{tenant}** is your tenant's name (for example, https://contosob2c.b2clogin.com).</span><span class="sxs-lookup"><span data-stu-id="ad977-117">Where **{tenant}** is your tenant's name (for example, https://contosob2c.b2clogin.com).</span></span>

    <span data-ttu-id="ad977-118">c.</span><span class="sxs-lookup"><span data-stu-id="ad977-118">c.</span></span> <span data-ttu-id="ad977-119">4.</span><span class="sxs-lookup"><span data-stu-id="ad977-119">4.</span></span> <span data-ttu-id="ad977-120">For the **Callback URL**, enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/{policyId}/oauth1/authresp`.</span><span class="sxs-lookup"><span data-stu-id="ad977-120">For the **Callback URL**, enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/{policyId}/oauth1/authresp`.</span></span> <span data-ttu-id="ad977-121">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c) and **{policyId}** with your policy id (for example, b2c_1_policy).</span><span class="sxs-lookup"><span data-stu-id="ad977-121">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c) and **{policyId}** with your policy id (for example, b2c_1_policy).</span></span>  <span data-ttu-id="ad977-122">**The callback URL needs to be in all lowercase.**</span><span class="sxs-lookup"><span data-stu-id="ad977-122">**The callback URL needs to be in all lowercase.**</span></span> <span data-ttu-id="ad977-123">You should add a callback URL for all policies that use the Twitter login.</span><span class="sxs-lookup"><span data-stu-id="ad977-123">You should add a callback URL for all policies that use the Twitter login.</span></span> <span data-ttu-id="ad977-124">Make sure to use `b2clogin.com` instead of ` login.microsoftonline.com` if you are using it in your application.</span><span class="sxs-lookup"><span data-stu-id="ad977-124">Make sure to use `b2clogin.com` instead of ` login.microsoftonline.com` if you are using it in your application.</span></span>

    <span data-ttu-id="ad977-125">d.</span><span class="sxs-lookup"><span data-stu-id="ad977-125">d.</span></span> <span data-ttu-id="ad977-126">At the bottom of the page, read and accept the terms, and then select **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="ad977-126">At the bottom of the page, read and accept the terms, and then select **Create your Twitter application**.</span></span>

    ![Twitter account - Add a new app](media/active-directory-b2c-custom-setup-twitter-idp/adb2c-ief-setup-twitter-idp-new-app2.png)

3. <span data-ttu-id="ad977-128">In the **B2C demo** window, select **Settings**, select the **Allow this application to be used to sign in with Twitter** check box, and then select **Update Settings**.</span><span class="sxs-lookup"><span data-stu-id="ad977-128">In the **B2C demo** window, select **Settings**, select the **Allow this application to be used to sign in with Twitter** check box, and then select **Update Settings**.</span></span>

4. <span data-ttu-id="ad977-129">Select **Keys and Access Tokens**, and note the **Consumer Key (API Key)** and **Consumer Secret (API Secret)** values.</span><span class="sxs-lookup"><span data-stu-id="ad977-129">Select **Keys and Access Tokens**, and note the **Consumer Key (API Key)** and **Consumer Secret (API Secret)** values.</span></span>

    ![Twitter account - Set application properties](media/active-directory-b2c-custom-setup-twitter-idp/adb2c-ief-setup-twitter-idp-new-app3.png)

    >[!NOTE]
    ><span data-ttu-id="ad977-131">The consumer secret is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="ad977-131">The consumer secret is an important security credential.</span></span> <span data-ttu-id="ad977-132">Do not share this secret with anyone or distribute it with your app.</span><span class="sxs-lookup"><span data-stu-id="ad977-132">Do not share this secret with anyone or distribute it with your app.</span></span>

## <a name="step-2-add-your-twitter-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="ad977-133">Step 2: Add your Twitter account application key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ad977-133">Step 2: Add your Twitter account application key to Azure AD B2C</span></span>
<span data-ttu-id="ad977-134">Federation with Twitter accounts requires a consumer secret for the Twitter account to trust Azure AD B2C on behalf of the application.</span><span class="sxs-lookup"><span data-stu-id="ad977-134">Federation with Twitter accounts requires a consumer secret for the Twitter account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="ad977-135">To store the Twitter application's consumer secret in your Azure AD B2C tenant, do the following:</span><span class="sxs-lookup"><span data-stu-id="ad977-135">To store the Twitter application's consumer secret in your Azure AD B2C tenant, do the following:</span></span> 

1. <span data-ttu-id="ad977-136">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="ad977-136">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span></span>

2. <span data-ttu-id="ad977-137">To view the keys that are available in your tenant, select **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="ad977-137">To view the keys that are available in your tenant, select **Policy Keys**.</span></span>

3. <span data-ttu-id="ad977-138">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="ad977-138">Select **Add**.</span></span>

4. <span data-ttu-id="ad977-139">In the **Options** box, select **Manual**.</span><span class="sxs-lookup"><span data-stu-id="ad977-139">In the **Options** box, select **Manual**.</span></span>

5. <span data-ttu-id="ad977-140">In the **Name** box, select **TwitterSecret**.</span><span class="sxs-lookup"><span data-stu-id="ad977-140">In the **Name** box, select **TwitterSecret**.</span></span>  
    <span data-ttu-id="ad977-141">The prefix *B2C_1A_* might be added automatically.</span><span class="sxs-lookup"><span data-stu-id="ad977-141">The prefix *B2C_1A_* might be added automatically.</span></span>

6. <span data-ttu-id="ad977-142">In the **Secret** box, enter your Microsoft application secret from the [Application Registration Portal](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ad977-142">In the **Secret** box, enter your Microsoft application secret from the [Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

7. <span data-ttu-id="ad977-143">For **Key usage**, use **Encryption**.</span><span class="sxs-lookup"><span data-stu-id="ad977-143">For **Key usage**, use **Encryption**.</span></span>

8. <span data-ttu-id="ad977-144">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="ad977-144">Select **Create**.</span></span>

9. <span data-ttu-id="ad977-145">Confirm that you've created the `B2C_1A_TwitterSecret` key.</span><span class="sxs-lookup"><span data-stu-id="ad977-145">Confirm that you've created the `B2C_1A_TwitterSecret` key.</span></span>

## <a name="step-3-add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="ad977-146">Step 3: Add a claims provider in your extension policy</span><span class="sxs-lookup"><span data-stu-id="ad977-146">Step 3: Add a claims provider in your extension policy</span></span>

<span data-ttu-id="ad977-147">If you want users to sign in by using Twitter account, you must define Twitter as a claims provider.</span><span class="sxs-lookup"><span data-stu-id="ad977-147">If you want users to sign in by using Twitter account, you must define Twitter as a claims provider.</span></span> <span data-ttu-id="ad977-148">In other words, you must specify the endpoints that Azure AD B2C communicates with.</span><span class="sxs-lookup"><span data-stu-id="ad977-148">In other words, you must specify the endpoints that Azure AD B2C communicates with.</span></span> <span data-ttu-id="ad977-149">The endpoints provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="ad977-149">The endpoints provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="ad977-150">Define Twitter as a claims provider by adding `<ClaimsProvider>` node in your extension policy file:</span><span class="sxs-lookup"><span data-stu-id="ad977-150">Define Twitter as a claims provider by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="ad977-151">In your working directory, open the *TrustFrameworkExtensions.xml* extension policy file.</span><span class="sxs-lookup"><span data-stu-id="ad977-151">In your working directory, open the *TrustFrameworkExtensions.xml* extension policy file.</span></span> 

2. <span data-ttu-id="ad977-152">Search for the `<ClaimsProviders>` section.</span><span class="sxs-lookup"><span data-stu-id="ad977-152">Search for the `<ClaimsProviders>` section.</span></span>

3. <span data-ttu-id="ad977-153">In the `<ClaimsProviders>` node, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="ad977-153">In the `<ClaimsProviders>` node, add the following XML snippet:</span></span>  

    ```xml
    <ClaimsProvider>
        <Domain>twitter.com</Domain>
        <DisplayName>Twitter</DisplayName>
        <TechnicalProfiles>
        <TechnicalProfile Id="Twitter-OAUTH1">
            <DisplayName>Twitter</DisplayName>
            <Protocol Name="OAuth1" />
            <Metadata>
            <Item Key="ProviderName">Twitter</Item>
            <Item Key="authorization_endpoint">https://api.twitter.com/oauth/authenticate</Item>
            <Item Key="access_token_endpoint">https://api.twitter.com/oauth/access_token</Item>
            <Item Key="request_token_endpoint">https://api.twitter.com/oauth/request_token</Item>
            <Item Key="ClaimsEndpoint">https://api.twitter.com/1.1/account/verify_credentials.json?include_email=true</Item>
            <Item Key="ClaimsResponseFormat">json</Item>
            <Item Key="client_id">Your Twitter application consumer key</Item>
            </Metadata>
            <CryptographicKeys>
            <Key Id="client_secret" StorageReferenceId="B2C_1A_TwitterSecret" />
            </CryptographicKeys>
            <InputClaims />
            <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="user_id" />
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="screen_name" />
            <OutputClaim ClaimTypeReferenceId="email" />
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="twitter.com" />
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

4. <span data-ttu-id="ad977-154">Replace the *client_id*\` value with your Twitter account application consumer key.</span><span class="sxs-lookup"><span data-stu-id="ad977-154">Replace the *client_id*\` value with your Twitter account application consumer key.</span></span>

5. <span data-ttu-id="ad977-155">Save the file.</span><span class="sxs-lookup"><span data-stu-id="ad977-155">Save the file.</span></span>

## <a name="step-4-register-the-twitter-account-claims-provider-to-your-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="ad977-156">Step 4: Register the Twitter account claims provider to your sign-up or sign-in user journey</span><span class="sxs-lookup"><span data-stu-id="ad977-156">Step 4: Register the Twitter account claims provider to your sign-up or sign-in user journey</span></span>
<span data-ttu-id="ad977-157">You've set up the identity provider.</span><span class="sxs-lookup"><span data-stu-id="ad977-157">You've set up the identity provider.</span></span> <span data-ttu-id="ad977-158">However, it is not yet available in any of the sign-up or sign-in windows.</span><span class="sxs-lookup"><span data-stu-id="ad977-158">However, it is not yet available in any of the sign-up or sign-in windows.</span></span> <span data-ttu-id="ad977-159">Now you must add the Twitter account identity provider to your user `SignUpOrSignIn` user journey.</span><span class="sxs-lookup"><span data-stu-id="ad977-159">Now you must add the Twitter account identity provider to your user `SignUpOrSignIn` user journey.</span></span>

### <a name="step-41-make-a-copy-of-the-user-journey"></a><span data-ttu-id="ad977-160">Step 4.1: Make a copy of the user journey</span><span class="sxs-lookup"><span data-stu-id="ad977-160">Step 4.1: Make a copy of the user journey</span></span>
<span data-ttu-id="ad977-161">To make the user journey available, you create a duplicate of an existing user journey template and then add the Twitter identity provider:</span><span class="sxs-lookup"><span data-stu-id="ad977-161">To make the user journey available, you create a duplicate of an existing user journey template and then add the Twitter identity provider:</span></span>

>[!NOTE]
><span data-ttu-id="ad977-162">If you copied the `<UserJourneys>` element from the base file of your policy to the *TrustFrameworkExtensions.xml* extension file, you can skip to the next section.</span><span class="sxs-lookup"><span data-stu-id="ad977-162">If you copied the `<UserJourneys>` element from the base file of your policy to the *TrustFrameworkExtensions.xml* extension file, you can skip to the next section.</span></span>

1. <span data-ttu-id="ad977-163">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="ad977-163">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>

2. <span data-ttu-id="ad977-164">Search for the `<UserJourneys>` element, select the entire contents of the `<UserJourney>` node, and then select **Cut** to move the selected text to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="ad977-164">Search for the `<UserJourneys>` element, select the entire contents of the `<UserJourney>` node, and then select **Cut** to move the selected text to the clipboard.</span></span>

3. <span data-ttu-id="ad977-165">Open the extension file (for example, TrustFrameworkExtensions.xml), and then search for the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="ad977-165">Open the extension file (for example, TrustFrameworkExtensions.xml), and then search for the `<UserJourneys>` element.</span></span> <span data-ttu-id="ad977-166">If the element doesn't exist, add it.</span><span class="sxs-lookup"><span data-stu-id="ad977-166">If the element doesn't exist, add it.</span></span>

4. <span data-ttu-id="ad977-167">Paste the entire contents of the `<UserJourney>` node, which you moved to the clipboard in step 2, into the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="ad977-167">Paste the entire contents of the `<UserJourney>` node, which you moved to the clipboard in step 2, into the `<UserJourneys>` element.</span></span>

### <a name="step-42-display-the-button"></a><span data-ttu-id="ad977-168">Step 4.2: Display the "button"</span><span class="sxs-lookup"><span data-stu-id="ad977-168">Step 4.2: Display the "button"</span></span>
<span data-ttu-id="ad977-169">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span><span class="sxs-lookup"><span data-stu-id="ad977-169">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span> <span data-ttu-id="ad977-170">The `<ClaimsProviderSelection>` node is analogous to an identity provider button on a sign-up or sign-in page.</span><span class="sxs-lookup"><span data-stu-id="ad977-170">The `<ClaimsProviderSelection>` node is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="ad977-171">If you add a `<ClaimsProviderSelection>` node for a Twitter account, a new button is displayed when a user lands on the page.</span><span class="sxs-lookup"><span data-stu-id="ad977-171">If you add a `<ClaimsProviderSelection>` node for a Twitter account, a new button is displayed when a user lands on the page.</span></span> <span data-ttu-id="ad977-172">To add this element, do the following:</span><span class="sxs-lookup"><span data-stu-id="ad977-172">To add this element, do the following:</span></span>

1. <span data-ttu-id="ad977-173">Search for the `<UserJourney>` node that contains `Id="SignUpOrSignIn"` in the user journey that you copied.</span><span class="sxs-lookup"><span data-stu-id="ad977-173">Search for the `<UserJourney>` node that contains `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>

2. <span data-ttu-id="ad977-174">Locate the `<OrchestrationStep>` node that contains `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="ad977-174">Locate the `<OrchestrationStep>` node that contains `Order="1"`.</span></span>

3. <span data-ttu-id="ad977-175">In the `<ClaimsProviderSelections>` element, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="ad977-175">In the `<ClaimsProviderSelections>` element, add the following XML snippet:</span></span>

    ```xml
    <ClaimsProviderSelection TargetClaimsExchangeId="TwitterExchange" />
    ```

### <a name="step-43-link-the-button-to-an-action"></a><span data-ttu-id="ad977-176">Step 4.3: Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="ad977-176">Step 4.3: Link the button to an action</span></span>
<span data-ttu-id="ad977-177">Now that you have a button in place, you must link it to an action.</span><span class="sxs-lookup"><span data-stu-id="ad977-177">Now that you have a button in place, you must link it to an action.</span></span> <span data-ttu-id="ad977-178">The action, in this case, is for Azure AD B2C to communicate with the Twitter account to receive a token.</span><span class="sxs-lookup"><span data-stu-id="ad977-178">The action, in this case, is for Azure AD B2C to communicate with the Twitter account to receive a token.</span></span> <span data-ttu-id="ad977-179">Link the button to an action by linking the technical profile for your Twitter account claims provider:</span><span class="sxs-lookup"><span data-stu-id="ad977-179">Link the button to an action by linking the technical profile for your Twitter account claims provider:</span></span>

1. <span data-ttu-id="ad977-180">Search for the `<OrchestrationStep>` node that contains `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="ad977-180">Search for the `<OrchestrationStep>` node that contains `Order="2"` in the `<UserJourney>` node.</span></span>
2. <span data-ttu-id="ad977-181">In the `<ClaimsExchanges>` element, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="ad977-181">In the `<ClaimsExchanges>` element, add the following XML snippet:</span></span>

    ```xml
    <ClaimsExchange Id="TwitterExchange" TechnicalProfileReferenceId="Twitter-OAUTH1" />
    ```

    >[!NOTE]
    >* <span data-ttu-id="ad977-182">Ensure that `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="ad977-182">Ensure that `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
    >* <span data-ttu-id="ad977-183">Ensure that the `TechnicalProfileReferenceId` ID is set to the technical profile that you created earlier (Twitter-OAUTH1).</span><span class="sxs-lookup"><span data-stu-id="ad977-183">Ensure that the `TechnicalProfileReferenceId` ID is set to the technical profile that you created earlier (Twitter-OAUTH1).</span></span>

## <a name="step-5-upload-the-policy-to-your-tenant"></a><span data-ttu-id="ad977-184">Step 5: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="ad977-184">Step 5: Upload the policy to your tenant</span></span>
1. <span data-ttu-id="ad977-185">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="ad977-185">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span></span>

2. <span data-ttu-id="ad977-186">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="ad977-186">Select **Identity Experience Framework**.</span></span>

3. <span data-ttu-id="ad977-187">Select **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="ad977-187">Select **All Policies**.</span></span>

4. <span data-ttu-id="ad977-188">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="ad977-188">Select **Upload Policy**.</span></span>

5. <span data-ttu-id="ad977-189">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="ad977-189">Select the **Overwrite the policy if it exists** check box.</span></span>

6. <span data-ttu-id="ad977-190">Upload the *TrustFrameworkBase.xml* and *TrustFrameworkExtensions.xml* files, and ensure that they pass validation.</span><span class="sxs-lookup"><span data-stu-id="ad977-190">Upload the *TrustFrameworkBase.xml* and *TrustFrameworkExtensions.xml* files, and ensure that they pass validation.</span></span>

## <a name="step-6-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="ad977-191">Step 6: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="ad977-191">Step 6: Test the custom policy by using Run Now</span></span>

1. <span data-ttu-id="ad977-192">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="ad977-192">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="ad977-193">Run Now requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="ad977-193">Run Now requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="ad977-194">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="ad977-194">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>

2. <span data-ttu-id="ad977-195">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="ad977-195">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span></span>  
    <span data-ttu-id="ad977-196">You should now be able to sign in by using the Twitter account.</span><span class="sxs-lookup"><span data-stu-id="ad977-196">You should now be able to sign in by using the Twitter account.</span></span>

## <a name="step-7-optional-register-the-twitter-account-claims-provider-to-the-profile-edit-user-journey"></a><span data-ttu-id="ad977-197">Step 7: (Optional) Register the Twitter account claims provider to the profile-edit user journey</span><span class="sxs-lookup"><span data-stu-id="ad977-197">Step 7: (Optional) Register the Twitter account claims provider to the profile-edit user journey</span></span>
<span data-ttu-id="ad977-198">You might also want to add the Twitter account identity provider to your `ProfileEdit` user journey.</span><span class="sxs-lookup"><span data-stu-id="ad977-198">You might also want to add the Twitter account identity provider to your `ProfileEdit` user journey.</span></span> <span data-ttu-id="ad977-199">To make the user journey available, repeat "Step 4."</span><span class="sxs-lookup"><span data-stu-id="ad977-199">To make the user journey available, repeat "Step 4."</span></span> <span data-ttu-id="ad977-200">This time, select the `<UserJourney>` node that contains `Id="ProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="ad977-200">This time, select the `<UserJourney>` node that contains `Id="ProfileEdit"`.</span></span> <span data-ttu-id="ad977-201">Save, upload, and test your policy.</span><span class="sxs-lookup"><span data-stu-id="ad977-201">Save, upload, and test your policy.</span></span>


## <a name="optional-download-the-complete-policy-files"></a><span data-ttu-id="ad977-202">(Optional) Download the complete policy files</span><span class="sxs-lookup"><span data-stu-id="ad977-202">(Optional) Download the complete policy files</span></span>
<span data-ttu-id="ad977-203">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span><span class="sxs-lookup"><span data-stu-id="ad977-203">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span></span> <span data-ttu-id="ad977-204">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-twitter-app).</span><span class="sxs-lookup"><span data-stu-id="ad977-204">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-twitter-app).</span></span>
