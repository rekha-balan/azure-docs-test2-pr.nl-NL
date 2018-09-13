---
title: Add Google as an identity provider for Azure Active Directory B2B | Microsoft Docs
description: Federate with Google to enable guest users to sign in to your Azure AD apps with their own Gmail account
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 08/20/2018
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: mal
ms.openlocfilehash: d36a4071dbbfb52e22a4e0ecc850da68ebeae6e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867429"
---
# <a name="add-google-as-an-identity-provider-for-b2b-guest-users"></a><span data-ttu-id="8690f-103">Add Google as an identity provider for B2B guest users</span><span class="sxs-lookup"><span data-stu-id="8690f-103">Add Google as an identity provider for B2B guest users</span></span>

<span data-ttu-id="8690f-104">By setting up federation with Google, you can allow invited users to sign in to your shared apps and resources with their own Google accounts, without having to create Microsoft Accounts (MSAs) or Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8690f-104">By setting up federation with Google, you can allow invited users to sign in to your shared apps and resources with their own Google accounts, without having to create Microsoft Accounts (MSAs) or Azure AD accounts.</span></span>  
> [!NOTE]
> <span data-ttu-id="8690f-105">Your Google guest users must sign in using a link that includes the tenant context, for example `https://myapps.microsoft.com/?tenantid=<tenant id>`.</span><span class="sxs-lookup"><span data-stu-id="8690f-105">Your Google guest users must sign in using a link that includes the tenant context, for example `https://myapps.microsoft.com/?tenantid=<tenant id>`.</span></span> <span data-ttu-id="8690f-106">Direct links to applications and resources also work as long as they include the tenant context.</span><span class="sxs-lookup"><span data-stu-id="8690f-106">Direct links to applications and resources also work as long as they include the tenant context.</span></span> <span data-ttu-id="8690f-107">Guest users are currently unable to sign in using endpoints that have no tenant context.</span><span class="sxs-lookup"><span data-stu-id="8690f-107">Guest users are currently unable to sign in using endpoints that have no tenant context.</span></span> <span data-ttu-id="8690f-108">For example, using `https://myapps.microsoft.com`, `https://portal.azure.com`, or the Teams common endpoint will result in an error.</span><span class="sxs-lookup"><span data-stu-id="8690f-108">For example, using `https://myapps.microsoft.com`, `https://portal.azure.com`, or the Teams common endpoint will result in an error.</span></span>
 
## <a name="what-is-the-experience-for-the-google-user"></a><span data-ttu-id="8690f-109">What is the experience for the Google user?</span><span class="sxs-lookup"><span data-stu-id="8690f-109">What is the experience for the Google user?</span></span>
<span data-ttu-id="8690f-110">When you send an invitation to a Google Gmail user, the guest user should access your shared apps or resources using a link that includes the tenant context.</span><span class="sxs-lookup"><span data-stu-id="8690f-110">When you send an invitation to a Google Gmail user, the guest user should access your shared apps or resources using a link that includes the tenant context.</span></span> <span data-ttu-id="8690f-111">Their experience varies depending on whether they're already signed in to Google:</span><span class="sxs-lookup"><span data-stu-id="8690f-111">Their experience varies depending on whether they're already signed in to Google:</span></span>
  - <span data-ttu-id="8690f-112">If the guest user is not signed in to Google, they're prompted to sign in to Google.</span><span class="sxs-lookup"><span data-stu-id="8690f-112">If the guest user is not signed in to Google, they're prompted to sign in to Google.</span></span>
  - <span data-ttu-id="8690f-113">If the guest user is already signed in to Google, they'll be prompted to choose the account they want to use.</span><span class="sxs-lookup"><span data-stu-id="8690f-113">If the guest user is already signed in to Google, they'll be prompted to choose the account they want to use.</span></span> <span data-ttu-id="8690f-114">They must choose the account you used to invite them.</span><span class="sxs-lookup"><span data-stu-id="8690f-114">They must choose the account you used to invite them.</span></span>

<span data-ttu-id="8690f-115">If the guest user sees a "header too long" error, they can try clearing their cookies, or they can open a private or incognito window and try signing in again.</span><span class="sxs-lookup"><span data-stu-id="8690f-115">If the guest user sees a "header too long" error, they can try clearing their cookies, or they can open a private or incognito window and try signing in again.</span></span>

![Sign in with Google](media/google-federation/google-sign-in.png)

## <a name="step-1-configure-a-google-developer-project"></a><span data-ttu-id="8690f-117">Step 1: Configure a Google developer project</span><span class="sxs-lookup"><span data-stu-id="8690f-117">Step 1: Configure a Google developer project</span></span>
<span data-ttu-id="8690f-118">First, create a new project in the Google Developers Console to obtain a client ID and a client secret that you can later add to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8690f-118">First, create a new project in the Google Developers Console to obtain a client ID and a client secret that you can later add to Azure AD.</span></span> 
1. <span data-ttu-id="8690f-119">Go to the Google APIs at https://console.developers.google.com, and sign in with your Google account.</span><span class="sxs-lookup"><span data-stu-id="8690f-119">Go to the Google APIs at https://console.developers.google.com, and sign in with your Google account.</span></span> <span data-ttu-id="8690f-120">We recommend that you use a shared team Google account.</span><span class="sxs-lookup"><span data-stu-id="8690f-120">We recommend that you use a shared team Google account.</span></span>
2. <span data-ttu-id="8690f-121">Create a new project: On the Dashboard, select **Create Project**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="8690f-121">Create a new project: On the Dashboard, select **Create Project**, and then select **Create**.</span></span> <span data-ttu-id="8690f-122">On the New Project page, enter a **Project Name**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="8690f-122">On the New Project page, enter a **Project Name**, and then select **Create**.</span></span>
   
   ![New Google project](media/google-federation/google-new-project.png)

3. <span data-ttu-id="8690f-124">Make sure your new project is selected in the project menu.</span><span class="sxs-lookup"><span data-stu-id="8690f-124">Make sure your new project is selected in the project menu.</span></span> <span data-ttu-id="8690f-125">Then open the menu in the upper left and select **APIs & Services** > **Credentials**.</span><span class="sxs-lookup"><span data-stu-id="8690f-125">Then open the menu in the upper left and select **APIs & Services** > **Credentials**.</span></span>

   ![Google API credentials](media/google-federation/google-api.png)
 
4. <span data-ttu-id="8690f-127">Choose the **Oauth consent screen** tab and enter a **Product name shown to users**.</span><span class="sxs-lookup"><span data-stu-id="8690f-127">Choose the **Oauth consent screen** tab and enter a **Product name shown to users**.</span></span> <span data-ttu-id="8690f-128">(Leave the other settings.) Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="8690f-128">(Leave the other settings.) Select **Save**.</span></span>

   ![Google OAuth consent screen](media/google-federation/google-oauth-consent-screen.png)

5. <span data-ttu-id="8690f-130">Choose the **Credentials** tab. In the **Create credentials** menu, choose **OAuth client ID**.</span><span class="sxs-lookup"><span data-stu-id="8690f-130">Choose the **Credentials** tab. In the **Create credentials** menu, choose **OAuth client ID**.</span></span>

   ![Google API credentials](media/google-federation/google-api-credentials.png)

6. <span data-ttu-id="8690f-132">Under **Application type**, choose **Web application**, and then under **Authorized redirect URIs**, enter the following URIs:</span><span class="sxs-lookup"><span data-stu-id="8690f-132">Under **Application type**, choose **Web application**, and then under **Authorized redirect URIs**, enter the following URIs:</span></span>
   - `https://login.microsoftonline.com` 
   - `https://login.microsoftonline.com/te/<directory id>/oauth2/authresp` <br><span data-ttu-id="8690f-133">(where `<directory id>` is your directory ID)</span><span class="sxs-lookup"><span data-stu-id="8690f-133">(where `<directory id>` is your directory ID)</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="8690f-134">To find your directory ID, go to https://portal.azure.com, and under **Azure Active Directory**, choose **Properties** and copy the **Directory ID**.</span><span class="sxs-lookup"><span data-stu-id="8690f-134">To find your directory ID, go to https://portal.azure.com, and under **Azure Active Directory**, choose **Properties** and copy the **Directory ID**.</span></span>

   ![Create OAuth client ID](media/google-federation/google-create-oauth-client-id.png)

7. <span data-ttu-id="8690f-136">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="8690f-136">Select **Create**.</span></span> <span data-ttu-id="8690f-137">Copy the client ID and client secret, which you'll use when you add the identity provider in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="8690f-137">Copy the client ID and client secret, which you'll use when you add the identity provider in the Azure AD portal.</span></span>

   ![OAuth client ID and client secret](media/google-federation/google-auth-client-id-secret.png)

## <a name="step-2-configure-google-federation-in-azure-ad"></a><span data-ttu-id="8690f-139">Step 2: Configure Google federation in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8690f-139">Step 2: Configure Google federation in Azure AD</span></span> 
<span data-ttu-id="8690f-140">Now you'll set the Google client ID and client secret, either by entering it in the Azure AD portal or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8690f-140">Now you'll set the Google client ID and client secret, either by entering it in the Azure AD portal or by using PowerShell.</span></span> <span data-ttu-id="8690f-141">Be sure to test your Google federation configuration by inviting yourself using a Gmail address and trying to redeem the invitation with your invited Google account.</span><span class="sxs-lookup"><span data-stu-id="8690f-141">Be sure to test your Google federation configuration by inviting yourself using a Gmail address and trying to redeem the invitation with your invited Google account.</span></span> 

#### <a name="to-configure-google-federation-in-the-azure-ad-portal"></a><span data-ttu-id="8690f-142">To configure Google federation in the Azure AD portal</span><span class="sxs-lookup"><span data-stu-id="8690f-142">To configure Google federation in the Azure AD portal</span></span> 
1. <span data-ttu-id="8690f-143">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8690f-143">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8690f-144">In the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8690f-144">In the left pane, select **Azure Active Directory**.</span></span> 
2. <span data-ttu-id="8690f-145">Select **Organizational Relationships**.</span><span class="sxs-lookup"><span data-stu-id="8690f-145">Select **Organizational Relationships**.</span></span>
3. <span data-ttu-id="8690f-146">Select **Identity providers**, and then click the **Google** button.</span><span class="sxs-lookup"><span data-stu-id="8690f-146">Select **Identity providers**, and then click the **Google** button.</span></span>
4. <span data-ttu-id="8690f-147">Enter a name.</span><span class="sxs-lookup"><span data-stu-id="8690f-147">Enter a name.</span></span> <span data-ttu-id="8690f-148">Then enter the client ID and client secret you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="8690f-148">Then enter the client ID and client secret you obtained earlier.</span></span> <span data-ttu-id="8690f-149">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="8690f-149">Select **Save**.</span></span> 

   ![Add Google identity provider](media/google-federation/google-identity-provider.png)

#### <a name="to-configure-google-federation-by-using-powershell"></a><span data-ttu-id="8690f-151">To configure Google federation by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="8690f-151">To configure Google federation by using PowerShell</span></span>
1. <span data-ttu-id="8690f-152">Install the latest version of the Azure AD PowerShell for Graph module ([AzureADPreview](https://www.powershellgallery.com/packages/AzureADPreview)).</span><span class="sxs-lookup"><span data-stu-id="8690f-152">Install the latest version of the Azure AD PowerShell for Graph module ([AzureADPreview](https://www.powershellgallery.com/packages/AzureADPreview)).</span></span>
2. <span data-ttu-id="8690f-153">Run the following command: `Connect-AzureAD`.</span><span class="sxs-lookup"><span data-stu-id="8690f-153">Run the following command: `Connect-AzureAD`.</span></span>
3. <span data-ttu-id="8690f-154">At the sign-in prompt, sign in with the managed Global Administrator account.</span><span class="sxs-lookup"><span data-stu-id="8690f-154">At the sign-in prompt, sign in with the managed Global Administrator account.</span></span>  
4. <span data-ttu-id="8690f-155">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="8690f-155">Run the following command:</span></span> 
   
   `New-AzureADMSIdentityProvider -Type Google -Name Google -ClientId [Client ID] -ClientSecret [Client secret]`
 
   > [!NOTE]
   > <span data-ttu-id="8690f-156">Use the client id and client secret from the app you created in "Step 1: Configure a Google developer project."</span><span class="sxs-lookup"><span data-stu-id="8690f-156">Use the client id and client secret from the app you created in "Step 1: Configure a Google developer project."</span></span> <span data-ttu-id="8690f-157">For more information, see the [New-AzureADMSIdentityProvider](https://docs.microsoft.com/en-us/powershell/module/azuread/new-azureadmsidentityprovider?view=azureadps-2.0-preview) article.</span><span class="sxs-lookup"><span data-stu-id="8690f-157">For more information, see the [New-AzureADMSIdentityProvider](https://docs.microsoft.com/en-us/powershell/module/azuread/new-azureadmsidentityprovider?view=azureadps-2.0-preview) article.</span></span> 
 
## <a name="how-do-i-remove-google-federation"></a><span data-ttu-id="8690f-158">How do I remove Google federation?</span><span class="sxs-lookup"><span data-stu-id="8690f-158">How do I remove Google federation?</span></span>
<span data-ttu-id="8690f-159">You can delete your Google federation setup.</span><span class="sxs-lookup"><span data-stu-id="8690f-159">You can delete your Google federation setup.</span></span> <span data-ttu-id="8690f-160">If you do so, Google guest users who have already redeemed their invitation will not be able to sign in, but you can give them access to your resources again by deleting them from the directory and re-inviting them.</span><span class="sxs-lookup"><span data-stu-id="8690f-160">If you do so, Google guest users who have already redeemed their invitation will not be able to sign in, but you can give them access to your resources again by deleting them from the directory and re-inviting them.</span></span> 
 
### <a name="to-delete-google-federation-in-the-azure-ad-portal"></a><span data-ttu-id="8690f-161">To delete Google federation in the Azure AD portal:</span><span class="sxs-lookup"><span data-stu-id="8690f-161">To delete Google federation in the Azure AD portal:</span></span> 
1. <span data-ttu-id="8690f-162">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8690f-162">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8690f-163">In the left pane, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8690f-163">In the left pane, select **Azure Active Directory**.</span></span> 
2. <span data-ttu-id="8690f-164">Select **Organizational Relationships**.</span><span class="sxs-lookup"><span data-stu-id="8690f-164">Select **Organizational Relationships**.</span></span>
3. <span data-ttu-id="8690f-165">Select **Identity providers**, and then click the **Google** button.</span><span class="sxs-lookup"><span data-stu-id="8690f-165">Select **Identity providers**, and then click the **Google** button.</span></span>
4. <span data-ttu-id="8690f-166">Select **Google**, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8690f-166">Select **Google**, and then select **Delete**.</span></span> 
   
   ![Deleted the social identity provider](media/google-federation/google-social-identity-providers.png)

1. <span data-ttu-id="8690f-168">Select **Yes** to confirm deletion.</span><span class="sxs-lookup"><span data-stu-id="8690f-168">Select **Yes** to confirm deletion.</span></span> 

### <a name="to-delete-google-federation-by-using-powershell"></a><span data-ttu-id="8690f-169">To delete Google federation by using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8690f-169">To delete Google federation by using PowerShell:</span></span> 
1. <span data-ttu-id="8690f-170">Install the latest version of the Azure AD PowerShell for Graph module ([AzureADPreview](https://www.powershellgallery.com/packages/AzureADPreview)).</span><span class="sxs-lookup"><span data-stu-id="8690f-170">Install the latest version of the Azure AD PowerShell for Graph module ([AzureADPreview](https://www.powershellgallery.com/packages/AzureADPreview)).</span></span>
2. <span data-ttu-id="8690f-171">Run `Connect-AzureAD`.</span><span class="sxs-lookup"><span data-stu-id="8690f-171">Run `Connect-AzureAD`.</span></span>  
4. <span data-ttu-id="8690f-172">In the login in prompt, sign in with the managed Global Administrator account.</span><span class="sxs-lookup"><span data-stu-id="8690f-172">In the login in prompt, sign in with the managed Global Administrator account.</span></span>  
5. <span data-ttu-id="8690f-173">Enter the following command:</span><span class="sxs-lookup"><span data-stu-id="8690f-173">Enter the following command:</span></span>

    `Remove-AzureADMSIdentityProvider -Id Google-OAUTH`

   > [!NOTE]
   > <span data-ttu-id="8690f-174">For more information, see [Remove-AzureADMSIdentityProvider](https://docs.microsoft.com/en-us/powershell/module/azuread/Remove-AzureADMSIdentityProvider?view=azureadps-2.0-preview).</span><span class="sxs-lookup"><span data-stu-id="8690f-174">For more information, see [Remove-AzureADMSIdentityProvider](https://docs.microsoft.com/en-us/powershell/module/azuread/Remove-AzureADMSIdentityProvider?view=azureadps-2.0-preview).</span></span> 