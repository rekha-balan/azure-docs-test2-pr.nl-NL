---
title: Quickstart - Set up sign-in for a desktop app using Azure Active Directory B2C | Microsoft Docs
description: Run a sample ASP.NET desktop application that uses Azure Active Directory B2C to provide account sign-in.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: quickstart
ms.custom: mvc
ms.date: 2/13/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: af4fe8ce4d9f5584241b56762ddf9c60aa28f0ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870885"
---
# <a name="quickstart-set-up-sign-in-for-a-desktop-app-using-azure-active-directory-b2c"></a><span data-ttu-id="d6780-103">Quickstart: Set up sign-in for a desktop app using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d6780-103">Quickstart: Set up sign-in for a desktop app using Azure Active Directory B2C</span></span> 

<span data-ttu-id="d6780-104">Azure Active Directory (Azure AD) B2C provides cloud identity management to keep your application, business, and customers protected.</span><span class="sxs-lookup"><span data-stu-id="d6780-104">Azure Active Directory (Azure AD) B2C provides cloud identity management to keep your application, business, and customers protected.</span></span> <span data-ttu-id="d6780-105">Azure AD B2C enables your apps to authenticate to social accounts, and enterprise accounts using open standard protocols.</span><span class="sxs-lookup"><span data-stu-id="d6780-105">Azure AD B2C enables your apps to authenticate to social accounts, and enterprise accounts using open standard protocols.</span></span>

<span data-ttu-id="d6780-106">In this quickstart, you use an Azure AD B2C enabled sample Windows Presentation Foundation (WPF) desktop app to sign in using a social identity provider and call an Azure AD B2C protected web API.</span><span class="sxs-lookup"><span data-stu-id="d6780-106">In this quickstart, you use an Azure AD B2C enabled sample Windows Presentation Foundation (WPF) desktop app to sign in using a social identity provider and call an Azure AD B2C protected web API.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="d6780-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6780-107">Prerequisites</span></span>

* <span data-ttu-id="d6780-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="d6780-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span></span> 
* <span data-ttu-id="d6780-109">A social account from either Facebook, Google, Microsoft, or Twitter.</span><span class="sxs-lookup"><span data-stu-id="d6780-109">A social account from either Facebook, Google, Microsoft, or Twitter.</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="d6780-110">Download the sample</span><span class="sxs-lookup"><span data-stu-id="d6780-110">Download the sample</span></span>

<span data-ttu-id="d6780-111">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop/archive/master.zip) or clone the sample web app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6780-111">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop/archive/master.zip) or clone the sample web app from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop.git
```

## <a name="run-the-app-in-visual-studio"></a><span data-ttu-id="d6780-112">Run the app in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6780-112">Run the app in Visual Studio</span></span>

<span data-ttu-id="d6780-113">In the sample application project folder, open the `active-directory-b2c-wpf.sln` solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6780-113">In the sample application project folder, open the `active-directory-b2c-wpf.sln` solution in Visual Studio.</span></span>

<span data-ttu-id="d6780-114">Press **F5** to debug the application.</span><span class="sxs-lookup"><span data-stu-id="d6780-114">Press **F5** to debug the application.</span></span>

## <a name="create-an-account"></a><span data-ttu-id="d6780-115">Create an account</span><span class="sxs-lookup"><span data-stu-id="d6780-115">Create an account</span></span>

<span data-ttu-id="d6780-116">Click **Sign in** to start the **Sign Up or Sign In** workflow based on an Azure AD B2C policy.</span><span class="sxs-lookup"><span data-stu-id="d6780-116">Click **Sign in** to start the **Sign Up or Sign In** workflow based on an Azure AD B2C policy.</span></span>

![Sample application](media/active-directory-b2c-quickstarts-desktop-app/wpf-sample-application.png)

<span data-ttu-id="d6780-118">The sample supports several sign-up options including using a social identity provider or creating a local account using an email address.</span><span class="sxs-lookup"><span data-stu-id="d6780-118">The sample supports several sign-up options including using a social identity provider or creating a local account using an email address.</span></span> <span data-ttu-id="d6780-119">For this quickstart, use a social identity provider account from either Facebook, Google, Microsoft, or Twitter.</span><span class="sxs-lookup"><span data-stu-id="d6780-119">For this quickstart, use a social identity provider account from either Facebook, Google, Microsoft, or Twitter.</span></span> 

### <a name="sign-up-using-a-social-identity-provider"></a><span data-ttu-id="d6780-120">Sign up using a social identity provider</span><span class="sxs-lookup"><span data-stu-id="d6780-120">Sign up using a social identity provider</span></span>

<span data-ttu-id="d6780-121">Azure AD B2C presents a custom login page for a fictitious brand called Wingtip Toys for the sample web app.</span><span class="sxs-lookup"><span data-stu-id="d6780-121">Azure AD B2C presents a custom login page for a fictitious brand called Wingtip Toys for the sample web app.</span></span> 

1. <span data-ttu-id="d6780-122">To sign up using a social identity provider, click the button of the identity provider you want to use.</span><span class="sxs-lookup"><span data-stu-id="d6780-122">To sign up using a social identity provider, click the button of the identity provider you want to use.</span></span> 

    ![Sign In or Sign Up provider](media/active-directory-b2c-quickstarts-desktop-app/sign-in-or-sign-up-wpf.png)

    <span data-ttu-id="d6780-124">You authenticate (sign-in) using your social account credentials and authorize the application to read information from your social account.</span><span class="sxs-lookup"><span data-stu-id="d6780-124">You authenticate (sign-in) using your social account credentials and authorize the application to read information from your social account.</span></span> <span data-ttu-id="d6780-125">By granting access, the application can retrieve profile information from the social account such as your name and city.</span><span class="sxs-lookup"><span data-stu-id="d6780-125">By granting access, the application can retrieve profile information from the social account such as your name and city.</span></span> 

2. <span data-ttu-id="d6780-126">Finish the sign-in process for the identity provider.</span><span class="sxs-lookup"><span data-stu-id="d6780-126">Finish the sign-in process for the identity provider.</span></span> <span data-ttu-id="d6780-127">For example, if you chose Twitter, enter your Twitter credentials and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="d6780-127">For example, if you chose Twitter, enter your Twitter credentials and click **Sign in**.</span></span>

    ![Authenticate and authorize using a social account](media/active-directory-b2c-quickstarts-desktop-app/twitter-authenticate-authorize-wpf.png)

    <span data-ttu-id="d6780-129">Your new account profile details are pre-populated with information from your social account.</span><span class="sxs-lookup"><span data-stu-id="d6780-129">Your new account profile details are pre-populated with information from your social account.</span></span> 

3. <span data-ttu-id="d6780-130">Modify the details if you wish and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d6780-130">Modify the details if you wish and click **Continue**.</span></span> <span data-ttu-id="d6780-131">The values you enter are used for your Azure AD B2C user account profile.</span><span class="sxs-lookup"><span data-stu-id="d6780-131">The values you enter are used for your Azure AD B2C user account profile.</span></span>

    ![New account sign-up profile details](media/active-directory-b2c-quickstarts-desktop-app/new-account-sign-up-profile-details-wpf.png)

    <span data-ttu-id="d6780-133">You have successfully created a new Azure AD B2C user account that uses an identity provider.</span><span class="sxs-lookup"><span data-stu-id="d6780-133">You have successfully created a new Azure AD B2C user account that uses an identity provider.</span></span> <span data-ttu-id="d6780-134">After sign-in, the access token is shown in the *Token info* text box.</span><span class="sxs-lookup"><span data-stu-id="d6780-134">After sign-in, the access token is shown in the *Token info* text box.</span></span> <span data-ttu-id="d6780-135">The access token is used when accessing the API resource.</span><span class="sxs-lookup"><span data-stu-id="d6780-135">The access token is used when accessing the API resource.</span></span>

## <a name="edit-your-profile"></a><span data-ttu-id="d6780-136">Edit your profile</span><span class="sxs-lookup"><span data-stu-id="d6780-136">Edit your profile</span></span>

<span data-ttu-id="d6780-137">Azure Active Directory B2C provides functionality to allow users to update their profiles.</span><span class="sxs-lookup"><span data-stu-id="d6780-137">Azure Active Directory B2C provides functionality to allow users to update their profiles.</span></span>  <span data-ttu-id="d6780-138">The sample web app uses an Azure AD B2C edit profile policy for the workflow.</span><span class="sxs-lookup"><span data-stu-id="d6780-138">The sample web app uses an Azure AD B2C edit profile policy for the workflow.</span></span> 

1. <span data-ttu-id="d6780-139">Click **Edit profile** to edit the profile you created.</span><span class="sxs-lookup"><span data-stu-id="d6780-139">Click **Edit profile** to edit the profile you created.</span></span>

    ![Edit profile](media/active-directory-b2c-quickstarts-desktop-app/edit-profile-wpf.png)

2. <span data-ttu-id="d6780-141">Choose the identity provider associated with the account you created.</span><span class="sxs-lookup"><span data-stu-id="d6780-141">Choose the identity provider associated with the account you created.</span></span> <span data-ttu-id="d6780-142">For example, if you used Twitter as the identity provider when you created your account, choose Twitter to modify the associated profile details.</span><span class="sxs-lookup"><span data-stu-id="d6780-142">For example, if you used Twitter as the identity provider when you created your account, choose Twitter to modify the associated profile details.</span></span>

3. <span data-ttu-id="d6780-143">Change your **Display name** or **City** and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="d6780-143">Change your **Display name** or **City** and click **Continue**.</span></span>

    <span data-ttu-id="d6780-144">A new access token is displayed in the *Token info* text box.</span><span class="sxs-lookup"><span data-stu-id="d6780-144">A new access token is displayed in the *Token info* text box.</span></span> <span data-ttu-id="d6780-145">If you want to verify the changes to your profile, copy and paste the access token into the token decoder https://jwt.ms.</span><span class="sxs-lookup"><span data-stu-id="d6780-145">If you want to verify the changes to your profile, copy and paste the access token into the token decoder https://jwt.ms.</span></span>

## <a name="access-a-protected-web-api-resource"></a><span data-ttu-id="d6780-146">Access a protected web API resource</span><span class="sxs-lookup"><span data-stu-id="d6780-146">Access a protected web API resource</span></span>

<span data-ttu-id="d6780-147">Click **Call API** to make a request to the Azure AD B2C protected resource.</span><span class="sxs-lookup"><span data-stu-id="d6780-147">Click **Call API** to make a request to the Azure AD B2C protected resource.</span></span> 

![Call API](media/active-directory-b2c-quickstarts-desktop-app/call-api-wpf.png)

<span data-ttu-id="d6780-149">The application includes the Azure AD access token in the request to the protected web API resource.</span><span class="sxs-lookup"><span data-stu-id="d6780-149">The application includes the Azure AD access token in the request to the protected web API resource.</span></span> <span data-ttu-id="d6780-150">The web API sends back the display name contained in the access token.</span><span class="sxs-lookup"><span data-stu-id="d6780-150">The web API sends back the display name contained in the access token.</span></span>

<span data-ttu-id="d6780-151">You have successfully used your Azure AD B2C user account to make an authorized call an Azure AD B2C protected web API.</span><span class="sxs-lookup"><span data-stu-id="d6780-151">You have successfully used your Azure AD B2C user account to make an authorized call an Azure AD B2C protected web API.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d6780-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d6780-152">Clean up resources</span></span>

<span data-ttu-id="d6780-153">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C quickstarts or tutorials.</span><span class="sxs-lookup"><span data-stu-id="d6780-153">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C quickstarts or tutorials.</span></span> <span data-ttu-id="d6780-154">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="d6780-154">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6780-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6780-155">Next steps</span></span>

<span data-ttu-id="d6780-156">The next step is to create your own Azure AD B2C tenant and configure the sample to run using your tenant.</span><span class="sxs-lookup"><span data-stu-id="d6780-156">The next step is to create your own Azure AD B2C tenant and configure the sample to run using your tenant.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6780-157">Create an Azure Active Directory B2C tenant in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d6780-157">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>](tutorial-create-tenant.md)
