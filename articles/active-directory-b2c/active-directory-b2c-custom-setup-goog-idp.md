---
title: Add Google+ as an OAuth2 identity provider using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Sample using Google+ as identity provider using OAuth2 protocol.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/04/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: f076a906ba38e6c8e8c9530baba1607553b41ea6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856274"
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="b64d3-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span><span class="sxs-lookup"><span data-stu-id="b64d3-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="b64d3-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b64d3-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b64d3-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b64d3-105">Prerequisites</span></span>

<span data-ttu-id="b64d3-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="b64d3-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="b64d3-107">These steps include:</span><span class="sxs-lookup"><span data-stu-id="b64d3-107">These steps include:</span></span>

1.  <span data-ttu-id="b64d3-108">Creating a Google+ account application.</span><span class="sxs-lookup"><span data-stu-id="b64d3-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="b64d3-109">Adding the Google+ account application key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b64d3-109">Adding the Google+ account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="b64d3-110">Adding claims provider to a policy</span><span class="sxs-lookup"><span data-stu-id="b64d3-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="b64d3-111">Registering the Google+ account claims provider to a user journey</span><span class="sxs-lookup"><span data-stu-id="b64d3-111">Registering the Google+ account claims provider to a user journey</span></span>
5.  <span data-ttu-id="b64d3-112">Uploading the policy to an Azure AD B2C tenant and test it</span><span class="sxs-lookup"><span data-stu-id="b64d3-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="b64d3-113">Create a Google+ account application</span><span class="sxs-lookup"><span data-stu-id="b64d3-113">Create a Google+ account application</span></span>
<span data-ttu-id="b64d3-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="b64d3-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="b64d3-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="b64d3-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="b64d3-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span><span class="sxs-lookup"><span data-stu-id="b64d3-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="b64d3-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="b64d3-118">Click on the **Projects menu**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-118">Click on the **Projects menu**.</span></span>

    ![Google+ account - Select project](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="b64d3-120">Click on the **+** button.</span><span class="sxs-lookup"><span data-stu-id="b64d3-120">Click on the **+** button.</span></span>

    ![Google+ account - Create new project](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="b64d3-122">Enter a **Project name**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google+ account - New project](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="b64d3-124">Wait until the project is ready and click on the **Projects menu**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-124">Wait until the project is ready and click on the **Projects menu**.</span></span>

    ![Google+ account - Wait until new project is ready to use](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="b64d3-126">Click on your project name.</span><span class="sxs-lookup"><span data-stu-id="b64d3-126">Click on your project name.</span></span>

    ![Google+ account - Select the new project](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="b64d3-128">Click **API Manager** and then click **Credentials** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="b64d3-128">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
9.  <span data-ttu-id="b64d3-129">Click the **OAuth consent screen** tab at the top.</span><span class="sxs-lookup"><span data-stu-id="b64d3-129">Click the **OAuth consent screen** tab at the top.</span></span>

    ![Google+ account - Set OAuth consent screen](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="b64d3-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - Application credentials](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="b64d3-133">Click **New credentials** and then choose **OAuth client ID**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+ - Create new application credentials](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="b64d3-135">Under **Application type**, select **Web application**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - Select application type](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="b64d3-137">Provide a **Name** for your application, enter `https://{tenant}.b2clogin.com` in the **Authorized JavaScript origins** field, and `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in the **Authorized redirect URIs** field.</span><span class="sxs-lookup"><span data-stu-id="b64d3-137">Provide a **Name** for your application, enter `https://{tenant}.b2clogin.com` in the **Authorized JavaScript origins** field, and `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="b64d3-138">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span><span class="sxs-lookup"><span data-stu-id="b64d3-138">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span></span> <span data-ttu-id="b64d3-139">The **{tenant}** value is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="b64d3-139">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="b64d3-140">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-140">Click **Create**.</span></span>

    ![Google+ - Provide Authorized JavaScript origins and redirect URIs](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="b64d3-142">Copy the values of **Client Id** and **Client secret**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-142">Copy the values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="b64d3-143">You need both to configure Google+ as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="b64d3-143">You need both to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="b64d3-144">**Client secret** is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="b64d3-144">**Client secret** is an important security credential.</span></span>

    ![Google+ - Copy the values of client Id and Client secret](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-the-google-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="b64d3-146">Add the Google+ account application key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="b64d3-146">Add the Google+ account application key to Azure AD B2C</span></span>
<span data-ttu-id="b64d3-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span><span class="sxs-lookup"><span data-stu-id="b64d3-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="b64d3-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span><span class="sxs-lookup"><span data-stu-id="b64d3-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="b64d3-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span><span class="sxs-lookup"><span data-stu-id="b64d3-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="b64d3-150">Select **Policy Keys** to view the keys available in your tenant.</span><span class="sxs-lookup"><span data-stu-id="b64d3-150">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="b64d3-151">Click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="b64d3-152">For **Options**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="b64d3-153">For **Name**, use `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="b64d3-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="b64d3-154">The prefix `B2C_1A_` might be added automatically.</span><span class="sxs-lookup"><span data-stu-id="b64d3-154">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="b64d3-155">In the **Secret** box, enter your Google application secret from the [Google Developers Console](https://console.developers.google.com/) that you copied above.</span><span class="sxs-lookup"><span data-stu-id="b64d3-155">In the **Secret** box, enter your Google application secret from the [Google Developers Console](https://console.developers.google.com/) that you copied above.</span></span>
7.  <span data-ttu-id="b64d3-156">For **Key usage**, use **Signature**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="b64d3-157">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="b64d3-157">Click **Create**</span></span>
9.  <span data-ttu-id="b64d3-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="b64d3-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="b64d3-159">Add a claims provider in your extension policy</span><span class="sxs-lookup"><span data-stu-id="b64d3-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="b64d3-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span><span class="sxs-lookup"><span data-stu-id="b64d3-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span></span> <span data-ttu-id="b64d3-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span><span class="sxs-lookup"><span data-stu-id="b64d3-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="b64d3-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="b64d3-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="b64d3-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span><span class="sxs-lookup"><span data-stu-id="b64d3-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="b64d3-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span><span class="sxs-lookup"><span data-stu-id="b64d3-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="b64d3-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span><span class="sxs-lookup"><span data-stu-id="b64d3-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="b64d3-166">Find the `<ClaimsProviders>` section</span><span class="sxs-lookup"><span data-stu-id="b64d3-166">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="b64d3-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span><span class="sxs-lookup"><span data-stu-id="b64d3-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want the user to select his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-google-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="b64d3-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span><span class="sxs-lookup"><span data-stu-id="b64d3-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span></span>

<span data-ttu-id="b64d3-169">The identity provider has been set up.</span><span class="sxs-lookup"><span data-stu-id="b64d3-169">The identity provider has been set up.</span></span>  <span data-ttu-id="b64d3-170">However, it is not available in any of the sign-up/sign-in screens.</span><span class="sxs-lookup"><span data-stu-id="b64d3-170">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="b64d3-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span><span class="sxs-lookup"><span data-stu-id="b64d3-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="b64d3-172">To make it available, we create a duplicate of an existing template user journey.</span><span class="sxs-lookup"><span data-stu-id="b64d3-172">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="b64d3-173">Then we add the Google+ account identity provider:</span><span class="sxs-lookup"><span data-stu-id="b64d3-173">Then we add the Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="b64d3-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span><span class="sxs-lookup"><span data-stu-id="b64d3-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span></span>

1.  <span data-ttu-id="b64d3-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="b64d3-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="b64d3-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span><span class="sxs-lookup"><span data-stu-id="b64d3-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="b64d3-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="b64d3-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="b64d3-178">If the element doesn't exist, add one.</span><span class="sxs-lookup"><span data-stu-id="b64d3-178">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="b64d3-179">Paste the entire content of `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="b64d3-179">Paste the entire content of `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="b64d3-180">Display the button</span><span class="sxs-lookup"><span data-stu-id="b64d3-180">Display the button</span></span>
<span data-ttu-id="b64d3-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span><span class="sxs-lookup"><span data-stu-id="b64d3-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="b64d3-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span><span class="sxs-lookup"><span data-stu-id="b64d3-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="b64d3-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span><span class="sxs-lookup"><span data-stu-id="b64d3-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="b64d3-184">To add this element:</span><span class="sxs-lookup"><span data-stu-id="b64d3-184">To add this element:</span></span>

1.  <span data-ttu-id="b64d3-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span><span class="sxs-lookup"><span data-stu-id="b64d3-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="b64d3-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="b64d3-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="b64d3-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span><span class="sxs-lookup"><span data-stu-id="b64d3-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="b64d3-188">Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="b64d3-188">Link the button to an action</span></span>
<span data-ttu-id="b64d3-189">Now that you have a button in place, you need to link it to an action.</span><span class="sxs-lookup"><span data-stu-id="b64d3-189">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="b64d3-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span><span class="sxs-lookup"><span data-stu-id="b64d3-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span></span>

1.  <span data-ttu-id="b64d3-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="b64d3-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="b64d3-192">Add following XML snippet under `<ClaimsExchanges>` node:</span><span class="sxs-lookup"><span data-stu-id="b64d3-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="b64d3-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span><span class="sxs-lookup"><span data-stu-id="b64d3-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
> * <span data-ttu-id="b64d3-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="b64d3-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="b64d3-195">Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="b64d3-195">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="b64d3-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="b64d3-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="b64d3-197">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="b64d3-198">Open the **All Policies** blade.</span><span class="sxs-lookup"><span data-stu-id="b64d3-198">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="b64d3-199">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="b64d3-200">Check **Overwrite the policy if it exists** box.</span><span class="sxs-lookup"><span data-stu-id="b64d3-200">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="b64d3-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span><span class="sxs-lookup"><span data-stu-id="b64d3-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="b64d3-202">Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="b64d3-202">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="b64d3-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="b64d3-204">**Run now** requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="b64d3-204">**Run now** requires at least one application to be preregistered on the tenant.</span></span> 
    >    <span data-ttu-id="b64d3-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="b64d3-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="b64d3-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="b64d3-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="b64d3-207">Select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="b64d3-208">You should be able to sign in using Google+ account.</span><span class="sxs-lookup"><span data-stu-id="b64d3-208">You should be able to sign in using Google+ account.</span></span>

## <a name="optional-register-the-google-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="b64d3-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span><span class="sxs-lookup"><span data-stu-id="b64d3-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="b64d3-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span><span class="sxs-lookup"><span data-stu-id="b64d3-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="b64d3-211">To make it available, we repeat the last two steps:</span><span class="sxs-lookup"><span data-stu-id="b64d3-211">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="b64d3-212">Display the button</span><span class="sxs-lookup"><span data-stu-id="b64d3-212">Display the button</span></span>
1.  <span data-ttu-id="b64d3-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="b64d3-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="b64d3-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span><span class="sxs-lookup"><span data-stu-id="b64d3-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="b64d3-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="b64d3-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="b64d3-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span><span class="sxs-lookup"><span data-stu-id="b64d3-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="b64d3-217">Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="b64d3-217">Link the button to an action</span></span>
1.  <span data-ttu-id="b64d3-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="b64d3-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="b64d3-219">Add following XML snippet under `<ClaimsExchanges>` node:</span><span class="sxs-lookup"><span data-stu-id="b64d3-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="b64d3-220">Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="b64d3-220">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="b64d3-221">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="b64d3-221">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="b64d3-222">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-222">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="b64d3-223">Open the **All Policies** blade.</span><span class="sxs-lookup"><span data-stu-id="b64d3-223">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="b64d3-224">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-224">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="b64d3-225">Check the **Overwrite the policy if it exists** box.</span><span class="sxs-lookup"><span data-stu-id="b64d3-225">Check the **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="b64d3-226">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation.</span><span class="sxs-lookup"><span data-stu-id="b64d3-226">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation.</span></span>

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="b64d3-227">Test the custom Profile-Edit policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="b64d3-227">Test the custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="b64d3-228">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-228">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="b64d3-229">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="b64d3-229">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="b64d3-230">Select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="b64d3-230">Select **Run now**.</span></span>
3.  <span data-ttu-id="b64d3-231">You should be able to sign in using Google+ account.</span><span class="sxs-lookup"><span data-stu-id="b64d3-231">You should be able to sign in using Google+ account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="b64d3-232">Download the complete policy files</span><span class="sxs-lookup"><span data-stu-id="b64d3-232">Download the complete policy files</span></span>
<span data-ttu-id="b64d3-233">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span><span class="sxs-lookup"><span data-stu-id="b64d3-233">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="b64d3-234">Sample policy files for reference</span><span class="sxs-lookup"><span data-stu-id="b64d3-234">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
