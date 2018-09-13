---
title: Add an Azure AD provider by using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Learn about Azure Active Directory B2C custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/15/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: af97a85b4d5d9c38f0e2bf8947482a0585fa6ee1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857222"
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="cc020-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cc020-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="cc020-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="cc020-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc020-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc020-105">Prerequisites</span></span>

<span data-ttu-id="cc020-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="cc020-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="cc020-107">These steps include:</span><span class="sxs-lookup"><span data-stu-id="cc020-107">These steps include:</span></span>

1. <span data-ttu-id="cc020-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span><span class="sxs-lookup"><span data-stu-id="cc020-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="cc020-109">Creating an Azure AD B2C application.</span><span class="sxs-lookup"><span data-stu-id="cc020-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="cc020-110">Registering two policy-engine applications.</span><span class="sxs-lookup"><span data-stu-id="cc020-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="cc020-111">Setting up keys.</span><span class="sxs-lookup"><span data-stu-id="cc020-111">Setting up keys.</span></span>
5. <span data-ttu-id="cc020-112">Setting up the starter pack.</span><span class="sxs-lookup"><span data-stu-id="cc020-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="cc020-113">Create an Azure AD app</span><span class="sxs-lookup"><span data-stu-id="cc020-113">Create an Azure AD app</span></span>

<span data-ttu-id="cc020-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="cc020-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="cc020-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span><span class="sxs-lookup"><span data-stu-id="cc020-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="cc020-116">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc020-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cc020-117">On the top bar, select your account.</span><span class="sxs-lookup"><span data-stu-id="cc020-117">On the top bar, select your account.</span></span> <span data-ttu-id="cc020-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="cc020-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
3. <span data-ttu-id="cc020-119">Select **More services** in the left pane, and search for "App registrations."</span><span class="sxs-lookup"><span data-stu-id="cc020-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
4. <span data-ttu-id="cc020-120">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="cc020-120">Select **New application registration**.</span></span>
5. <span data-ttu-id="cc020-121">Enter a name for your application (for example, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="cc020-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
6. <span data-ttu-id="cc020-122">Select **Web app / API** for the application type.</span><span class="sxs-lookup"><span data-stu-id="cc020-122">Select **Web app / API** for the application type.</span></span>
7. <span data-ttu-id="cc020-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="cc020-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    >[!NOTE]
    ><span data-ttu-id="cc020-124">The value for "yourtenant" must be all lowercase in the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="cc020-124">The value for "yourtenant" must be all lowercase in the **Sign-on URL**.</span></span>

    ```
    https://yourtenant.b2clogin.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

8. <span data-ttu-id="cc020-125">Save the application ID.</span><span class="sxs-lookup"><span data-stu-id="cc020-125">Save the application ID.</span></span>
9. <span data-ttu-id="cc020-126">Select the newly created application.</span><span class="sxs-lookup"><span data-stu-id="cc020-126">Select the newly created application.</span></span>
10. <span data-ttu-id="cc020-127">Under the **Settings** blade, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="cc020-127">Under the **Settings** blade, select **Keys**.</span></span>
11. <span data-ttu-id="cc020-128">Enter the key description, select a duration, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cc020-128">Enter the key description, select a duration, and then click **Save**.</span></span> <span data-ttu-id="cc020-129">The value of the key is displayed.</span><span class="sxs-lookup"><span data-stu-id="cc020-129">The value of the key is displayed.</span></span> <span data-ttu-id="cc020-130">Copy it because you will use it in the steps in the next section.</span><span class="sxs-lookup"><span data-stu-id="cc020-130">Copy it because you will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="cc020-131">Add the Azure AD key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="cc020-131">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="cc020-132">You need to store the contoso.com application key in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="cc020-132">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="cc020-133">To do this:</span><span class="sxs-lookup"><span data-stu-id="cc020-133">To do this:</span></span>
1. <span data-ttu-id="cc020-134">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="cc020-134">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="cc020-135">Select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="cc020-135">Select **+Add**.</span></span>
1. <span data-ttu-id="cc020-136">Select or enter these options:</span><span class="sxs-lookup"><span data-stu-id="cc020-136">Select or enter these options:</span></span>
   * <span data-ttu-id="cc020-137">Select **Manual**.</span><span class="sxs-lookup"><span data-stu-id="cc020-137">Select **Manual**.</span></span>
   * <span data-ttu-id="cc020-138">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="cc020-138">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="cc020-139">The prefix `B2C_1A_` is added automatically to the name of your key.</span><span class="sxs-lookup"><span data-stu-id="cc020-139">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="cc020-140">Paste your application key in the **Secret** box.</span><span class="sxs-lookup"><span data-stu-id="cc020-140">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="cc020-141">Select **Signature**.</span><span class="sxs-lookup"><span data-stu-id="cc020-141">Select **Signature**.</span></span>
1. <span data-ttu-id="cc020-142">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc020-142">Select **Create**.</span></span>
1. <span data-ttu-id="cc020-143">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="cc020-143">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="cc020-144">Add a claims provider in your base policy</span><span class="sxs-lookup"><span data-stu-id="cc020-144">Add a claims provider in your base policy</span></span>

<span data-ttu-id="cc020-145">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span><span class="sxs-lookup"><span data-stu-id="cc020-145">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="cc020-146">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span><span class="sxs-lookup"><span data-stu-id="cc020-146">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="cc020-147">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="cc020-147">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="cc020-148">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span><span class="sxs-lookup"><span data-stu-id="cc020-148">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="cc020-149">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span><span class="sxs-lookup"><span data-stu-id="cc020-149">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="cc020-150">Find the `<ClaimsProviders>` section.</span><span class="sxs-lookup"><span data-stu-id="cc020-150">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="cc020-151">If it does not exist, add it under the root node.</span><span class="sxs-lookup"><span data-stu-id="cc020-151">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="cc020-152">Add a new `<ClaimsProvider>` node as follows:</span><span class="sxs-lookup"><span data-stu-id="cc020-152">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
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

1. <span data-ttu-id="cc020-153">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span><span class="sxs-lookup"><span data-stu-id="cc020-153">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="cc020-154">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span><span class="sxs-lookup"><span data-stu-id="cc020-154">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="cc020-155">This value is not currently used.</span><span class="sxs-lookup"><span data-stu-id="cc020-155">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="cc020-156">Update the technical profile</span><span class="sxs-lookup"><span data-stu-id="cc020-156">Update the technical profile</span></span>

<span data-ttu-id="cc020-157">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc020-157">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="cc020-158">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="cc020-158">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="cc020-159">Update the ID of the `<TechnicalProfile>` node.</span><span class="sxs-lookup"><span data-stu-id="cc020-159">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="cc020-160">This ID is used to refer to this technical profile from other parts of the policy.</span><span class="sxs-lookup"><span data-stu-id="cc020-160">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="cc020-161">Update the value for `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="cc020-161">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="cc020-162">This value will be displayed on the sign-in button on your sign-in screen.</span><span class="sxs-lookup"><span data-stu-id="cc020-162">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="cc020-163">Update the value for `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="cc020-163">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="cc020-164">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="cc020-164">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="cc020-165">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="cc020-165">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="cc020-166">In the XML file, update the metadata values as follows:</span><span class="sxs-lookup"><span data-stu-id="cc020-166">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="cc020-167">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="cc020-167">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="cc020-168">Open your browser and go to the `METADATA` URL that you just updated.</span><span class="sxs-lookup"><span data-stu-id="cc020-168">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="cc020-169">In the browser, look for the 'issuer' object and copy its value.</span><span class="sxs-lookup"><span data-stu-id="cc020-169">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="cc020-170">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="cc020-170">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="cc020-171">Paste the value for `<Item Key="ProviderName">` in the XML file.</span><span class="sxs-lookup"><span data-stu-id="cc020-171">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="cc020-172">Set `<Item Key="client_id">` to the application ID from the app registration.</span><span class="sxs-lookup"><span data-stu-id="cc020-172">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="cc020-173">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span><span class="sxs-lookup"><span data-stu-id="cc020-173">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="cc020-174">Ensure that `<Item Key="response_types">` is set to `id_token`.</span><span class="sxs-lookup"><span data-stu-id="cc020-174">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="cc020-175">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span><span class="sxs-lookup"><span data-stu-id="cc020-175">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="cc020-176">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span><span class="sxs-lookup"><span data-stu-id="cc020-176">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="cc020-177">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="cc020-177">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="cc020-178">Upload the extension file for verification</span><span class="sxs-lookup"><span data-stu-id="cc020-178">Upload the extension file for verification</span></span>

<span data-ttu-id="cc020-179">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="cc020-179">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="cc020-180">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span><span class="sxs-lookup"><span data-stu-id="cc020-180">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="cc020-181">To do so:</span><span class="sxs-lookup"><span data-stu-id="cc020-181">To do so:</span></span>

1. <span data-ttu-id="cc020-182">Open the **All Policies** blade in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="cc020-182">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="cc020-183">Check the **Overwrite the policy if it exists** box.</span><span class="sxs-lookup"><span data-stu-id="cc020-183">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="cc020-184">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span><span class="sxs-lookup"><span data-stu-id="cc020-184">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="cc020-185">Register the Azure AD claims provider to a user journey</span><span class="sxs-lookup"><span data-stu-id="cc020-185">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="cc020-186">You now need to add the Azure AD identity provider to one of your user journeys.</span><span class="sxs-lookup"><span data-stu-id="cc020-186">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="cc020-187">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span><span class="sxs-lookup"><span data-stu-id="cc020-187">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="cc020-188">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span><span class="sxs-lookup"><span data-stu-id="cc020-188">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="cc020-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="cc020-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="cc020-190">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="cc020-190">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="cc020-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="cc020-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="cc020-192">If the element doesn't exist, add one.</span><span class="sxs-lookup"><span data-stu-id="cc020-192">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="cc020-193">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="cc020-193">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="cc020-194">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="cc020-194">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="cc020-195">Display the "button"</span><span class="sxs-lookup"><span data-stu-id="cc020-195">Display the "button"</span></span>

<span data-ttu-id="cc020-196">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span><span class="sxs-lookup"><span data-stu-id="cc020-196">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="cc020-197">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span><span class="sxs-lookup"><span data-stu-id="cc020-197">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="cc020-198">To add this element:</span><span class="sxs-lookup"><span data-stu-id="cc020-198">To add this element:</span></span>

1. <span data-ttu-id="cc020-199">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span><span class="sxs-lookup"><span data-stu-id="cc020-199">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="cc020-200">Add the following:</span><span class="sxs-lookup"><span data-stu-id="cc020-200">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="cc020-201">Set `TargetClaimsExchangeId` to an appropriate value.</span><span class="sxs-lookup"><span data-stu-id="cc020-201">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="cc020-202">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="cc020-202">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="cc020-203">Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="cc020-203">Link the button to an action</span></span>

<span data-ttu-id="cc020-204">Now that you have a button in place, you need to link it to an action.</span><span class="sxs-lookup"><span data-stu-id="cc020-204">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="cc020-205">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span><span class="sxs-lookup"><span data-stu-id="cc020-205">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="cc020-206">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span><span class="sxs-lookup"><span data-stu-id="cc020-206">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="cc020-207">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="cc020-207">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="cc020-208">Add the following:</span><span class="sxs-lookup"><span data-stu-id="cc020-208">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="cc020-209">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="cc020-209">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="cc020-210">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="cc020-210">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="cc020-211">Upload the updated extension file</span><span class="sxs-lookup"><span data-stu-id="cc020-211">Upload the updated extension file</span></span>

<span data-ttu-id="cc020-212">You are done modifying the extension file.</span><span class="sxs-lookup"><span data-stu-id="cc020-212">You are done modifying the extension file.</span></span> <span data-ttu-id="cc020-213">Save it.</span><span class="sxs-lookup"><span data-stu-id="cc020-213">Save it.</span></span> <span data-ttu-id="cc020-214">Then upload the file, and ensure that all validations succeed.</span><span class="sxs-lookup"><span data-stu-id="cc020-214">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="cc020-215">Update the RP file</span><span class="sxs-lookup"><span data-stu-id="cc020-215">Update the RP file</span></span>

<span data-ttu-id="cc020-216">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span><span class="sxs-lookup"><span data-stu-id="cc020-216">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="cc020-217">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="cc020-217">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="cc020-218">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="cc020-218">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="cc020-219">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="cc020-219">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="cc020-220">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="cc020-220">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="cc020-221">Save your changes, and upload the file.</span><span class="sxs-lookup"><span data-stu-id="cc020-221">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cc020-222">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="cc020-222">Troubleshooting</span></span>

<span data-ttu-id="cc020-223">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span><span class="sxs-lookup"><span data-stu-id="cc020-223">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="cc020-224">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="cc020-224">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc020-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc020-225">Next steps</span></span>

<span data-ttu-id="cc020-226">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cc020-226">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
