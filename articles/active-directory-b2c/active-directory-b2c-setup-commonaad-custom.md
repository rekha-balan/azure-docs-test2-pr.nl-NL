---
title: Add a multi-tenant Azure AD identity provider using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Add a multi-tenant Azure AD identity provider using custom policies - Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/14/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 68eab85c7f67ad3af18c6066c29e1250e1be3d23
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856483"
---
# <a name="azure-active-directory-b2c-allow-users-to-sign-in-to-a-multi-tenant-azure-ad-identity-provider-using-custom-policies"></a><span data-ttu-id="effe0-103">Azure Active Directory B2C: Allow users to sign in to a multi-tenant Azure AD identity provider using custom policies</span><span class="sxs-lookup"><span data-stu-id="effe0-103">Azure Active Directory B2C: Allow users to sign in to a multi-tenant Azure AD identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="effe0-104">This article shows you how to enable sign-in for users using the multi-tenant endpoint for Azure Active Directory (Azure AD) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="effe0-104">This article shows you how to enable sign-in for users using the multi-tenant endpoint for Azure Active Directory (Azure AD) through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span> <span data-ttu-id="effe0-105">This allows users from multiple Azure AD tenants to sign into Azure AD B2C without configuring a technical provider for each tenant.</span><span class="sxs-lookup"><span data-stu-id="effe0-105">This allows users from multiple Azure AD tenants to sign into Azure AD B2C without configuring a technical provider for each tenant.</span></span> <span data-ttu-id="effe0-106">However, guest members in any of these tenants **will not** be able to sign in.</span><span class="sxs-lookup"><span data-stu-id="effe0-106">However, guest members in any of these tenants **will not** be able to sign in.</span></span> <span data-ttu-id="effe0-107">For that, you will have to [individually configure each tenant](active-directory-b2c-setup-aad-custom.md).</span><span class="sxs-lookup"><span data-stu-id="effe0-107">For that, you will have to [individually configure each tenant](active-directory-b2c-setup-aad-custom.md).</span></span>

>[!NOTE]
> <span data-ttu-id="effe0-108">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span><span class="sxs-lookup"><span data-stu-id="effe0-108">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="effe0-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="effe0-109">Prerequisites</span></span>

<span data-ttu-id="effe0-110">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span><span class="sxs-lookup"><span data-stu-id="effe0-110">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="effe0-111">These steps include:</span><span class="sxs-lookup"><span data-stu-id="effe0-111">These steps include:</span></span>
     
1. <span data-ttu-id="effe0-112">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span><span class="sxs-lookup"><span data-stu-id="effe0-112">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
1. <span data-ttu-id="effe0-113">Creating an Azure AD B2C application.</span><span class="sxs-lookup"><span data-stu-id="effe0-113">Creating an Azure AD B2C application.</span></span>    
1. <span data-ttu-id="effe0-114">Registering two policy-engine applications.</span><span class="sxs-lookup"><span data-stu-id="effe0-114">Registering two policy-engine applications.</span></span>  
1. <span data-ttu-id="effe0-115">Setting up keys.</span><span class="sxs-lookup"><span data-stu-id="effe0-115">Setting up keys.</span></span> 
1. <span data-ttu-id="effe0-116">Setting up the starter pack.</span><span class="sxs-lookup"><span data-stu-id="effe0-116">Setting up the starter pack.</span></span>

## <a name="step-1-create-a-multi-tenant-azure-ad-app"></a><span data-ttu-id="effe0-117">Step 1.</span><span class="sxs-lookup"><span data-stu-id="effe0-117">Step 1.</span></span> <span data-ttu-id="effe0-118">Create a multi-tenant Azure AD app</span><span class="sxs-lookup"><span data-stu-id="effe0-118">Create a multi-tenant Azure AD app</span></span>

<span data-ttu-id="effe0-119">To enable sign-in for users using the multi-tenant Azure AD endpoint, you need to have a multi-tenant application registered in one of your Azure AD tenants.</span><span class="sxs-lookup"><span data-stu-id="effe0-119">To enable sign-in for users using the multi-tenant Azure AD endpoint, you need to have a multi-tenant application registered in one of your Azure AD tenants.</span></span> <span data-ttu-id="effe0-120">In this article, we will show you how to create a multi-tenant Azure AD application in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="effe0-120">In this article, we will show you how to create a multi-tenant Azure AD application in your Azure AD B2C tenant.</span></span> <span data-ttu-id="effe0-121">Then enable sign-in for users through the use of that multi-tenant Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="effe0-121">Then enable sign-in for users through the use of that multi-tenant Azure AD application.</span></span>

1. <span data-ttu-id="effe0-122">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="effe0-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="effe0-123">On the top bar, select your account.</span><span class="sxs-lookup"><span data-stu-id="effe0-123">On the top bar, select your account.</span></span> <span data-ttu-id="effe0-124">From the **Directory** list, choose the Azure AD B2C tenant to register the Azure AD application (fabrikamb2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="effe0-124">From the **Directory** list, choose the Azure AD B2C tenant to register the Azure AD application (fabrikamb2c.onmicrosoft.com).</span></span>
1. <span data-ttu-id="effe0-125">Select **More services** in the left pane, and search for "App registrations."</span><span class="sxs-lookup"><span data-stu-id="effe0-125">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="effe0-126">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="effe0-126">Select **New application registration**.</span></span>
1. <span data-ttu-id="effe0-127">Enter a name for your application (for example, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="effe0-127">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="effe0-128">Select **Web app / API** for the application type.</span><span class="sxs-lookup"><span data-stu-id="effe0-128">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="effe0-129">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="effe0-129">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    >[!NOTE]
    ><span data-ttu-id="effe0-130">The value for "yourtenant" must be all lowercase in the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="effe0-130">The value for "yourtenant" must be all lowercase in the **Sign-on URL**.</span></span>

    ```
    https://yourtenant.b2clogin.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="effe0-131">Save the application ID.</span><span class="sxs-lookup"><span data-stu-id="effe0-131">Save the application ID.</span></span>
1. <span data-ttu-id="effe0-132">Select the newly created application.</span><span class="sxs-lookup"><span data-stu-id="effe0-132">Select the newly created application.</span></span>
1. <span data-ttu-id="effe0-133">Under the **Settings** blade, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="effe0-133">Under the **Settings** blade, select **Properties**.</span></span>
1. <span data-ttu-id="effe0-134">Set **Multi-tenanted** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="effe0-134">Set **Multi-tenanted** to **Yes**.</span></span>
1. <span data-ttu-id="effe0-135">Under the **Settings** blade, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="effe0-135">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="effe0-136">Create a new key, and save it.</span><span class="sxs-lookup"><span data-stu-id="effe0-136">Create a new key, and save it.</span></span> <span data-ttu-id="effe0-137">You will use it in the steps in the next section.</span><span class="sxs-lookup"><span data-stu-id="effe0-137">You will use it in the steps in the next section.</span></span>

## <a name="step-2-add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="effe0-138">Step 2.</span><span class="sxs-lookup"><span data-stu-id="effe0-138">Step 2.</span></span> <span data-ttu-id="effe0-139">Add the Azure AD key to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="effe0-139">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="effe0-140">You need to register the application key in the Azure AD B2C settings.</span><span class="sxs-lookup"><span data-stu-id="effe0-140">You need to register the application key in the Azure AD B2C settings.</span></span> <span data-ttu-id="effe0-141">To do this:</span><span class="sxs-lookup"><span data-stu-id="effe0-141">To do this:</span></span>

1. <span data-ttu-id="effe0-142">Go to the settings menu for Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="effe0-142">Go to the settings menu for Azure AD B2C</span></span>
1. <span data-ttu-id="effe0-143">Click on **Identity Experience Framework** > **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="effe0-143">Click on **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="effe0-144">Select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="effe0-144">Select **+Add**.</span></span>
1. <span data-ttu-id="effe0-145">Select or enter these options:</span><span class="sxs-lookup"><span data-stu-id="effe0-145">Select or enter these options:</span></span>
   * <span data-ttu-id="effe0-146">Select **Manual**.</span><span class="sxs-lookup"><span data-stu-id="effe0-146">Select **Manual**.</span></span>
   * <span data-ttu-id="effe0-147">For **Name**, choose a name that matches your Azure AD tenant name (for example, `AADAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="effe0-147">For **Name**, choose a name that matches your Azure AD tenant name (for example, `AADAppSecret`).</span></span>  <span data-ttu-id="effe0-148">The prefix `B2C_1A_` is added automatically to the name of your key.</span><span class="sxs-lookup"><span data-stu-id="effe0-148">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="effe0-149">Paste your application key in the **Secret** box.</span><span class="sxs-lookup"><span data-stu-id="effe0-149">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="effe0-150">Select **Signature**.</span><span class="sxs-lookup"><span data-stu-id="effe0-150">Select **Signature**.</span></span>
1. <span data-ttu-id="effe0-151">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="effe0-151">Select **Create**.</span></span>
1. <span data-ttu-id="effe0-152">Confirm that you've created the key `B2C_1A_AADAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="effe0-152">Confirm that you've created the key `B2C_1A_AADAppSecret`.</span></span>

## <a name="step-3-add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="effe0-153">Step 3.</span><span class="sxs-lookup"><span data-stu-id="effe0-153">Step 3.</span></span> <span data-ttu-id="effe0-154">Add a claims provider in your base policy</span><span class="sxs-lookup"><span data-stu-id="effe0-154">Add a claims provider in your base policy</span></span>

<span data-ttu-id="effe0-155">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span><span class="sxs-lookup"><span data-stu-id="effe0-155">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="effe0-156">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span><span class="sxs-lookup"><span data-stu-id="effe0-156">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="effe0-157">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="effe0-157">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="effe0-158">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span><span class="sxs-lookup"><span data-stu-id="effe0-158">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="effe0-159">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span><span class="sxs-lookup"><span data-stu-id="effe0-159">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="effe0-160">Find the `<ClaimsProviders>` section.</span><span class="sxs-lookup"><span data-stu-id="effe0-160">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="effe0-161">If it does not exist, add it under the root node.</span><span class="sxs-lookup"><span data-stu-id="effe0-161">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="effe0-162">Add a new `<ClaimsProvider>` node as follows:</span><span class="sxs-lookup"><span data-stu-id="effe0-162">Add a new `<ClaimsProvider>` node as follows:</span></span>

```XML
<ClaimsProvider>
  <Domain>commonaad</Domain>
  <DisplayName>Common AAD</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="Common-AAD">
      <DisplayName>Multi-Tenant AAD</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <Metadata>
        <!-- Update the Client ID below to the Application ID -->
        <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="METADATA">https://login.microsoftonline.com/common/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="scope">openid</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="DiscoverMetadataByTokenIssuer">true</Item>
        
        <!-- The key below allows you to specify each of the Azure AD tenants that can be used to sign in. Update the GUIDs below for each tenant. -->
        <Item Key="ValidTokenIssuerPrefixes">https://sts.windows.net/00000000-0000-0000-0000-000000000000,https://sts.windows.net/11111111-1111-1111-1111-111111111111</Item>

        <!-- The commented key below specifies that users from any tenant can sign-in. Uncomment if you would like anyone with an Azure AD account to be able to sign in. -->
        <!-- <Item Key="ValidTokenIssuerPrefixes">https://sts.windows.net/</Item> -->

      </Metadata>
      <CryptographicKeys>
      <!-- Make sure to update the reference ID of the client secret below you just created (B2C_1A_AADAppSecret) -->
        <Key Id="client_secret" StorageReferenceId="B2C_1A_AADAppSecret" />
      </CryptographicKeys>
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" PartnerClaimType="iss" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
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

1. <span data-ttu-id="effe0-163">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span><span class="sxs-lookup"><span data-stu-id="effe0-163">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="effe0-164">Under the `<TechnicalProfile>` node, update the value for `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="effe0-164">Under the `<TechnicalProfile>` node, update the value for `<DisplayName>`.</span></span> <span data-ttu-id="effe0-165">This value will be displayed on the sign-in button on your sign-in screen.</span><span class="sxs-lookup"><span data-stu-id="effe0-165">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="effe0-166">Update the value for `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="effe0-166">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="effe0-167">Set `<Item Key="client_id">` to the application ID from the Azure AD mulity-tenant app registration.</span><span class="sxs-lookup"><span data-stu-id="effe0-167">Set `<Item Key="client_id">` to the application ID from the Azure AD mulity-tenant app registration.</span></span>

### <a name="step-31-restrict-access-to-a-specific-list-of-azure-ad-tenants"></a><span data-ttu-id="effe0-168">Step 3.1 Restrict access to a specific list of Azure AD tenants</span><span class="sxs-lookup"><span data-stu-id="effe0-168">Step 3.1 Restrict access to a specific list of Azure AD tenants</span></span>

> [!NOTE]
> <span data-ttu-id="effe0-169">Using `https://sts.windows.net` as the value for **ValidTokenIssuerPrefixes** will allow ALL Azure AD users to sign into your app.</span><span class="sxs-lookup"><span data-stu-id="effe0-169">Using `https://sts.windows.net` as the value for **ValidTokenIssuerPrefixes** will allow ALL Azure AD users to sign into your app.</span></span>

<span data-ttu-id="effe0-170">You need to update the list of valid token issuers and restrict access to specific list of Azure AD tenants users can sign-in.</span><span class="sxs-lookup"><span data-stu-id="effe0-170">You need to update the list of valid token issuers and restrict access to specific list of Azure AD tenants users can sign-in.</span></span> <span data-ttu-id="effe0-171">To obtain the values, you will need to look at the metadata for each of the specific Azure AD tenants that you would like to have users sign in from.</span><span class="sxs-lookup"><span data-stu-id="effe0-171">To obtain the values, you will need to look at the metadata for each of the specific Azure AD tenants that you would like to have users sign in from.</span></span> <span data-ttu-id="effe0-172">The format of the data looks like the following: `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com or any other Azure AD tenant).</span><span class="sxs-lookup"><span data-stu-id="effe0-172">The format of the data looks like the following: `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com or any other Azure AD tenant).</span></span>
1. <span data-ttu-id="effe0-173">Open your browser and go to the metadata URL.</span><span class="sxs-lookup"><span data-stu-id="effe0-173">Open your browser and go to the metadata URL.</span></span>
1. <span data-ttu-id="effe0-174">In the browser, look for the 'issuer' object and copy its value.</span><span class="sxs-lookup"><span data-stu-id="effe0-174">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="effe0-175">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="effe0-175">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="effe0-176">Paste the value for the `ValidTokenIssuerPrefixes` key.</span><span class="sxs-lookup"><span data-stu-id="effe0-176">Paste the value for the `ValidTokenIssuerPrefixes` key.</span></span> <span data-ttu-id="effe0-177">You can add multiple by separating them using a comma.</span><span class="sxs-lookup"><span data-stu-id="effe0-177">You can add multiple by separating them using a comma.</span></span> <span data-ttu-id="effe0-178">An example of this is commented in the sample XML above.</span><span class="sxs-lookup"><span data-stu-id="effe0-178">An example of this is commented in the sample XML above.</span></span>

## <a name="step-4-register-the-azure-ad-account-claims-provider"></a><span data-ttu-id="effe0-179">Step 4.</span><span class="sxs-lookup"><span data-stu-id="effe0-179">Step 4.</span></span> <span data-ttu-id="effe0-180">Register the Azure AD account claims provider</span><span class="sxs-lookup"><span data-stu-id="effe0-180">Register the Azure AD account claims provider</span></span>

### <a name="step-41-make-a-copy-of-the-user-journey"></a><span data-ttu-id="effe0-181">Step 4.1 Make a copy of the user journey</span><span class="sxs-lookup"><span data-stu-id="effe0-181">Step 4.1 Make a copy of the user journey</span></span>

<span data-ttu-id="effe0-182">You now need to add the Azure AD identity provider to one of your user journeys.</span><span class="sxs-lookup"><span data-stu-id="effe0-182">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="effe0-183">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span><span class="sxs-lookup"><span data-stu-id="effe0-183">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span>

<span data-ttu-id="effe0-184">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span><span class="sxs-lookup"><span data-stu-id="effe0-184">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="effe0-185">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="effe0-185">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="effe0-186">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="effe0-186">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="effe0-187">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="effe0-187">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="effe0-188">If the element doesn't exist, add one.</span><span class="sxs-lookup"><span data-stu-id="effe0-188">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="effe0-189">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="effe0-189">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="effe0-190">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingAzureAD`).</span><span class="sxs-lookup"><span data-stu-id="effe0-190">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingAzureAD`).</span></span> 

### <a name="step-42-display-the-button"></a><span data-ttu-id="effe0-191">Step 4.2 Display the "button"</span><span class="sxs-lookup"><span data-stu-id="effe0-191">Step 4.2 Display the "button"</span></span>

<span data-ttu-id="effe0-192">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span><span class="sxs-lookup"><span data-stu-id="effe0-192">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="effe0-193">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span><span class="sxs-lookup"><span data-stu-id="effe0-193">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="effe0-194">To add this element:</span><span class="sxs-lookup"><span data-stu-id="effe0-194">To add this element:</span></span>

1. <span data-ttu-id="effe0-195">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you created.</span><span class="sxs-lookup"><span data-stu-id="effe0-195">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you created.</span></span>
1. <span data-ttu-id="effe0-196">Add the following:</span><span class="sxs-lookup"><span data-stu-id="effe0-196">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="AzureADExchange" />
    ```

1. <span data-ttu-id="effe0-197">Set `TargetClaimsExchangeId` to an appropriate value.</span><span class="sxs-lookup"><span data-stu-id="effe0-197">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="effe0-198">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="effe0-198">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="step-43-link-the-button-to-an-action"></a><span data-ttu-id="effe0-199">Step 4.3 Link the button to an action</span><span class="sxs-lookup"><span data-stu-id="effe0-199">Step 4.3 Link the button to an action</span></span>

<span data-ttu-id="effe0-200">Now that you have a button in place, you need to link it to an action.</span><span class="sxs-lookup"><span data-stu-id="effe0-200">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="effe0-201">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span><span class="sxs-lookup"><span data-stu-id="effe0-201">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="effe0-202">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span><span class="sxs-lookup"><span data-stu-id="effe0-202">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="effe0-203">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span><span class="sxs-lookup"><span data-stu-id="effe0-203">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="effe0-204">Add the following:</span><span class="sxs-lookup"><span data-stu-id="effe0-204">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="AzureADExchange" TechnicalProfileReferenceId="Common-AAD" />
    ```

1. <span data-ttu-id="effe0-205">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span><span class="sxs-lookup"><span data-stu-id="effe0-205">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="effe0-206">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (Common-AAD).</span><span class="sxs-lookup"><span data-stu-id="effe0-206">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (Common-AAD).</span></span>

## <a name="step-5-create-a-new-rp-policy"></a><span data-ttu-id="effe0-207">Step 5: Create a new RP policy</span><span class="sxs-lookup"><span data-stu-id="effe0-207">Step 5: Create a new RP policy</span></span>

<span data-ttu-id="effe0-208">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span><span class="sxs-lookup"><span data-stu-id="effe0-208">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>
 
1. <span data-ttu-id="effe0-209">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="effe0-209">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>  
1. <span data-ttu-id="effe0-210">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="effe0-210">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <span data-ttu-id="effe0-211">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="effe0-211">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span> 
1. <span data-ttu-id="effe0-212">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingAzureAD).</span><span class="sxs-lookup"><span data-stu-id="effe0-212">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingAzureAD).</span></span> 
1. <span data-ttu-id="effe0-213">Save your changes, and upload the file.</span><span class="sxs-lookup"><span data-stu-id="effe0-213">Save your changes, and upload the file.</span></span> 

## <a name="step-6-upload-the-policy-to-your-tenant"></a><span data-ttu-id="effe0-214">Step 6: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="effe0-214">Step 6: Upload the policy to your tenant</span></span>

1. <span data-ttu-id="effe0-215">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="effe0-215">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span></span>
1. <span data-ttu-id="effe0-216">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="effe0-216">Select **Identity Experience Framework**.</span></span>
1. <span data-ttu-id="effe0-217">Select **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="effe0-217">Select **All Policies**.</span></span>
1. <span data-ttu-id="effe0-218">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="effe0-218">Select **Upload Policy**.</span></span>
1. <span data-ttu-id="effe0-219">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="effe0-219">Select the **Overwrite the policy if it exists** check box.</span></span>
1. <span data-ttu-id="effe0-220">Upload the `TrustFrameworkExtensions.xml` file and the RP file (e.g. `SignUpOrSignInWithAAD.xml`) and ensure they pass validation.</span><span class="sxs-lookup"><span data-stu-id="effe0-220">Upload the `TrustFrameworkExtensions.xml` file and the RP file (e.g. `SignUpOrSignInWithAAD.xml`) and ensure they pass validation.</span></span>

## <a name="step-7-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="effe0-221">Step 7: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="effe0-221">Step 7: Test the custom policy by using Run Now</span></span>

1. <span data-ttu-id="effe0-222">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="effe0-222">Select **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span></span>
    > [!NOTE]
    > <span data-ttu-id="effe0-223">Run Now requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="effe0-223">Run Now requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="effe0-224">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="effe0-224">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>

1. <span data-ttu-id="effe0-225">Open the relying party (RP) custom policy that you uploaded (*B2C\_1A\_SignUpOrSignInWithAAD*), and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="effe0-225">Open the relying party (RP) custom policy that you uploaded (*B2C\_1A\_SignUpOrSignInWithAAD*), and then select **Run now**.</span></span>
1. <span data-ttu-id="effe0-226">You should now be able to sign in by using the Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="effe0-226">You should now be able to sign in by using the Azure AD account.</span></span>

## <a name="optional-step-8-register-the-azure-ad-account-claims-provider-to-the-profile-edit-user-journey"></a><span data-ttu-id="effe0-227">(Optional) Step 8: Register the Azure AD account claims provider to the Profile-Edit user journey</span><span class="sxs-lookup"><span data-stu-id="effe0-227">(Optional) Step 8: Register the Azure AD account claims provider to the Profile-Edit user journey</span></span>

<span data-ttu-id="effe0-228">You might also want to add the Azure AD account identity provider to your `ProfileEdit` user journey.</span><span class="sxs-lookup"><span data-stu-id="effe0-228">You might also want to add the Azure AD account identity provider to your `ProfileEdit` user journey.</span></span> <span data-ttu-id="effe0-229">To make the user journey available, repeat Steps 4 through 6.</span><span class="sxs-lookup"><span data-stu-id="effe0-229">To make the user journey available, repeat Steps 4 through 6.</span></span> <span data-ttu-id="effe0-230">This time, select the `<UserJourney>` node that contains `Id="ProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="effe0-230">This time, select the `<UserJourney>` node that contains `Id="ProfileEdit"`.</span></span> <span data-ttu-id="effe0-231">Save, upload, and test your policy.</span><span class="sxs-lookup"><span data-stu-id="effe0-231">Save, upload, and test your policy.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="effe0-232">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="effe0-232">Troubleshooting</span></span>

<span data-ttu-id="effe0-233">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="effe0-233">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="effe0-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="effe0-234">Next steps</span></span>

<span data-ttu-id="effe0-235">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="effe0-235">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
