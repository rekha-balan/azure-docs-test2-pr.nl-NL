---
title: Add Microsoft Account (MSA) as an identity provider using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Sample using Microsoft as identity provider using OpenID Connect (OIDC) protocol.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/04/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 6a981f112c97ee35b476c92f6f698e68a12a1363
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865383"
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="7c09c-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span><span class="sxs-lookup"><span data-stu-id="7c09c-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="7c09c-104">This article shows you how to enable sign-in for users from Microsoft account (MSA) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="7c09c-104">This article shows you how to enable sign-in for users from Microsoft account (MSA) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c09c-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7c09c-105">Prerequisites</span></span>
<span data-ttu-id="7c09c-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="7c09c-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="7c09c-107">These steps include:</span><span class="sxs-lookup"><span data-stu-id="7c09c-107">These steps include:</span></span>

1.  <span data-ttu-id="7c09c-108">Creating a Microsoft account application.</span><span class="sxs-lookup"><span data-stu-id="7c09c-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="7c09c-109">Adding the Microsoft account application key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7c09c-109">Adding the Microsoft account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="7c09c-110">Adding claims provider to a policy</span><span class="sxs-lookup"><span data-stu-id="7c09c-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="7c09c-111">Registering the Microsoft Account claims provider to a user journey</span><span class="sxs-lookup"><span data-stu-id="7c09c-111">Registering the Microsoft Account claims provider to a user journey</span></span>
5.  <span data-ttu-id="7c09c-112">Uploading the policy to an Azure AD B2C tenant and test it</span><span class="sxs-lookup"><span data-stu-id="7c09c-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="7c09c-113">Create a Microsoft account application</span><span class="sxs-lookup"><span data-stu-id="7c09c-113">Create a Microsoft account application</span></span>
<span data-ttu-id="7c09c-114">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="7c09c-114">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="7c09c-115">You need a Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="7c09c-115">You need a Microsoft account.</span></span> <span data-ttu-id="7c09c-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="7c09c-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="7c09c-117">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span><span class="sxs-lookup"><span data-stu-id="7c09c-117">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="7c09c-118">Click **Add an app**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-118">Click **Add an app**.</span></span>

    ![Microsoft account - Add an app](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="7c09c-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Microsoft account - Register your application](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="7c09c-122">Copy the value of **Application Id**. You need it to configure Microsoft account as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="7c09c-122">Copy the value of **Application Id**. You need it to configure Microsoft account as an identity provider in your tenant.</span></span>

    ![Microsoft account - Copy the value of Application Id](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="7c09c-124">Click on **Add platform**</span><span class="sxs-lookup"><span data-stu-id="7c09c-124">Click on **Add platform**</span></span>

    ![Microsoft account - Add platform](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="7c09c-126">From the platform list, choose **Web**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-126">From the platform list, choose **Web**.</span></span>

    ![Microsoft account - From the platform list choose Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="7c09c-128">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in the **Redirect URIs** field.</span><span class="sxs-lookup"><span data-stu-id="7c09c-128">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="7c09c-129">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span><span class="sxs-lookup"><span data-stu-id="7c09c-129">Replace **{tenant}** with your tenant's name (for example, contosob2c).</span></span>

    ![Microsoft account - Set redirect URLs](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="7c09c-131">Click on **Generate New Password** under the **Application Secrets** section.</span><span class="sxs-lookup"><span data-stu-id="7c09c-131">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="7c09c-132">Copy the new password displayed on screen.</span><span class="sxs-lookup"><span data-stu-id="7c09c-132">Copy the new password displayed on screen.</span></span> <span data-ttu-id="7c09c-133">You need it to configure Microsoft account as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="7c09c-133">You need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="7c09c-134">This password is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="7c09c-134">This password is an important security credential.</span></span>

    ![Microsoft account - Generate new password](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft account - Copy the new password](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="7c09c-137">Check the box that says **Live SDK support** under the **Advanced Options** section.</span><span class="sxs-lookup"><span data-stu-id="7c09c-137">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="7c09c-138">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-138">Click **Save**.</span></span>

    ![Microsoft account - Live SDK support](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-the-microsoft-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="7c09c-140">Add the Microsoft account application key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7c09c-140">Add the Microsoft account application key to Azure AD B2C</span></span>
<span data-ttu-id="7c09c-141">Federation with Microsoft accounts requires a client secret for Microsoft account to trust Azure AD B2C on behalf of the application.</span><span class="sxs-lookup"><span data-stu-id="7c09c-141">Federation with Microsoft accounts requires a client secret for Microsoft account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="7c09c-142">You need to store your Microsoft account application secert in Azure AD B2C tenant:</span><span class="sxs-lookup"><span data-stu-id="7c09c-142">You need to store your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="7c09c-143">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span><span class="sxs-lookup"><span data-stu-id="7c09c-143">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="7c09c-144">Select **Policy Keys** to view the keys available in your tenant.</span><span class="sxs-lookup"><span data-stu-id="7c09c-144">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="7c09c-145">Click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="7c09c-146">For **Options**, use **Manual**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="7c09c-147">For **Name**, use `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="7c09c-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="7c09c-148">The prefix `B2C_1A_` might be added automatically.</span><span class="sxs-lookup"><span data-stu-id="7c09c-148">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="7c09c-149">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="7c09c-149">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="7c09c-150">For **Key usage**, use **Signature**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="7c09c-151">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="7c09c-151">Click **Create**</span></span>
9.  <span data-ttu-id="7c09c-152">Confirm that you've created the key `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="7c09c-152">Confirm that you've created the key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="7c09c-153">Add a claims provider in your extension policy</span><span class="sxs-lookup"><span data-stu-id="7c09c-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="7c09c-154">If you want users to sign in by using Microsoft Account, you need to define Microsoft Account as a claims provider.</span><span class="sxs-lookup"><span data-stu-id="7c09c-154">If you want users to sign in by using Microsoft Account, you need to define Microsoft Account as a claims provider.</span></span> <span data-ttu-id="7c09c-155">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span><span class="sxs-lookup"><span data-stu-id="7c09c-155">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="7c09c-156">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="7c09c-156">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="7c09c-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span><span class="sxs-lookup"><span data-stu-id="7c09c-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="7c09c-158">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span><span class="sxs-lookup"><span data-stu-id="7c09c-158">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="7c09c-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span><span class="sxs-lookup"><span data-stu-id="7c09c-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="7c09c-160">Find the `<ClaimsProviders>` section</span><span class="sxs-lookup"><span data-stu-id="7c09c-160">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="7c09c-161">Add following XML snippet under the `ClaimsProviders` element:</span><span class="sxs-lookup"><span data-stu-id="7c09c-161">Add following XML snippet under the `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
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

4.  <span data-ttu-id="7c09c-162">Replace `client_id` value with your Microsoft Account application client Id</span><span class="sxs-lookup"><span data-stu-id="7c09c-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="7c09c-163">Save the file.</span><span class="sxs-lookup"><span data-stu-id="7c09c-163">Save the file.</span></span>

## <a name="register-the-microsoft-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="7c09c-164">Register the Microsoft Account claims provider to Sign up or Sign-in user journey</span><span class="sxs-lookup"><span data-stu-id="7c09c-164">Register the Microsoft Account claims provider to Sign up or Sign-in user journey</span></span>

<span data-ttu-id="7c09c-165">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span><span class="sxs-lookup"><span data-stu-id="7c09c-165">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="7c09c-166">Now you need to add the Microsoft Account identity provider to your user `SignUpOrSignIn` user journey.</span><span class="sxs-lookup"><span data-stu-id="7c09c-166">Now you need to add the Microsoft Account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="7c09c-167">To make it available, we create a duplicate of an existing template user journey.</span><span class="sxs-lookup"><span data-stu-id="7c09c-167">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="7c09c-168">Then we add the Microsoft Account identity provider:</span><span class="sxs-lookup"><span data-stu-id="7c09c-168">Then we add the Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="7c09c-169">If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file `TrustFrameworkExtensions.xml`, you can skip to this section.</span><span class="sxs-lookup"><span data-stu-id="7c09c-169">If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file `TrustFrameworkExtensions.xml`, you can skip to this section.</span></span>

1.  <span data-ttu-id="7c09c-170">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="7c09c-170">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="7c09c-171">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span><span class="sxs-lookup"><span data-stu-id="7c09c-171">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="7c09c-172">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="7c09c-172">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="7c09c-173">If the element doesn't exist, add one.</span><span class="sxs-lookup"><span data-stu-id="7c09c-173">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="7c09c-174">Paste the entire content of `<UserJourneys>` node that you copied as a child of the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="7c09c-174">Paste the entire content of `<UserJourneys>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="7c09c-175">Display the button</span><span class="sxs-lookup"><span data-stu-id="7c09c-175">Display the button</span></span>
<span data-ttu-id="7c09c-176">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span><span class="sxs-lookup"><span data-stu-id="7c09c-176">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="7c09c-177">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span><span class="sxs-lookup"><span data-stu-id="7c09c-177">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="7c09c-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on the page.</span><span class="sxs-lookup"><span data-stu-id="7c09c-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="7c09c-179">To add this element:</span><span class="sxs-lookup"><span data-stu-id="7c09c-179">To add this element:</span></span>

1.  <span data-ttu-id="7c09c-180">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span><span class="sxs-lookup"><span data-stu-id="7c09c-180">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="7c09c-181">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="7c09c-181">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="7c09c-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span><span class="sxs-lookup"><span data-stu-id="7c09c-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MicrosoftAccountExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="7c09c-183">Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="7c09c-183">Link the button to an action</span></span>
<span data-ttu-id="7c09c-184">Now that you have a button in place, you need to link it to an action.</span><span class="sxs-lookup"><span data-stu-id="7c09c-184">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="7c09c-185">The action, in this case, is for Azure AD B2C to communicate with Microsoft Account to receive a token.</span><span class="sxs-lookup"><span data-stu-id="7c09c-185">The action, in this case, is for Azure AD B2C to communicate with Microsoft Account to receive a token.</span></span> <span data-ttu-id="7c09c-186">Link the button to an action by linking the technical profile for your Microsoft Account claims provider:</span><span class="sxs-lookup"><span data-stu-id="7c09c-186">Link the button to an action by linking the technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="7c09c-187">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="7c09c-187">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="7c09c-188">Add following XML snippet under `<ClaimsExchanges>` node:</span><span class="sxs-lookup"><span data-stu-id="7c09c-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MicrosoftAccountExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="7c09c-189">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span><span class="sxs-lookup"><span data-stu-id="7c09c-189">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
>   * <span data-ttu-id="7c09c-190">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="7c09c-190">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="7c09c-191">Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="7c09c-191">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="7c09c-192">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="7c09c-192">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="7c09c-193">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="7c09c-194">Open the **All Policies** blade.</span><span class="sxs-lookup"><span data-stu-id="7c09c-194">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="7c09c-195">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="7c09c-196">Check **Overwrite the policy if it exists** box.</span><span class="sxs-lookup"><span data-stu-id="7c09c-196">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="7c09c-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span><span class="sxs-lookup"><span data-stu-id="7c09c-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="7c09c-198">Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="7c09c-198">Test the custom policy by using Run Now</span></span>

1.  <span data-ttu-id="7c09c-199">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-199">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="7c09c-200">**Run now** requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="7c09c-200">**Run now** requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="7c09c-201">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="7c09c-201">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="7c09c-202">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="7c09c-202">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="7c09c-203">Select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="7c09c-204">You should be able to sign in using Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="7c09c-204">You should be able to sign in using Microsoft account.</span></span>

## <a name="optional-register-the-microsoft-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="7c09c-205">[Optional] Register the Microsoft Account claims provider to Profile-Edit user journey</span><span class="sxs-lookup"><span data-stu-id="7c09c-205">[Optional] Register the Microsoft Account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="7c09c-206">You may want to add the Microsoft Account identity provider also to your user `ProfileEdit` user journey.</span><span class="sxs-lookup"><span data-stu-id="7c09c-206">You may want to add the Microsoft Account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="7c09c-207">To make it available, we repeat the last two steps:</span><span class="sxs-lookup"><span data-stu-id="7c09c-207">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="7c09c-208">Display the button</span><span class="sxs-lookup"><span data-stu-id="7c09c-208">Display the button</span></span>
1.  <span data-ttu-id="7c09c-209">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="7c09c-209">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="7c09c-210">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span><span class="sxs-lookup"><span data-stu-id="7c09c-210">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="7c09c-211">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="7c09c-211">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="7c09c-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span><span class="sxs-lookup"><span data-stu-id="7c09c-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="7c09c-213">Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="7c09c-213">Link the button to an action</span></span>
1.  <span data-ttu-id="7c09c-214">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="7c09c-214">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="7c09c-215">Add following XML snippet under `<ClaimsExchanges>` node:</span><span class="sxs-lookup"><span data-stu-id="7c09c-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="7c09c-216">Test the custom Profile-Edit policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="7c09c-216">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="7c09c-217">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-217">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="7c09c-218">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span><span class="sxs-lookup"><span data-stu-id="7c09c-218">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="7c09c-219">Select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="7c09c-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="7c09c-220">You should be able to sign in using Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="7c09c-220">You should be able to sign in using Microsoft account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="7c09c-221">Download the complete policy files</span><span class="sxs-lookup"><span data-stu-id="7c09c-221">Download the complete policy files</span></span>
<span data-ttu-id="7c09c-222">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span><span class="sxs-lookup"><span data-stu-id="7c09c-222">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="7c09c-223">Sample policy files for reference</span><span class="sxs-lookup"><span data-stu-id="7c09c-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
